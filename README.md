# ISZ™ 仕訳AI MCP サーバー（shiwake.ai）

[![npm](https://img.shields.io/npm/v/shiwake-ai-mcp)](https://www.npmjs.com/package/shiwake-ai-mcp) [![MCP endpoint](https://img.shields.io/badge/MCP-mcp.shiwake.ai-blue)](https://shiwake.ai/guide/kaikei-mcp/)

日本語 | [English](#english)

> 提供: [ISZ™ 仕訳AI](https://shiwake.ai/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-top)（AI税務会計プラットフォーム。税理士・会計事務所、自社で申告する中小法人・個人事業主に）・姉妹プロダクト [DenwaFlow](https://denwaflow.jp/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-top)（AI 電話受付）

日本の税務・会計の計算を、AI アシスタント（Claude・ChatGPT・Cursor など）から使えるようにする MCP サーバーです。
[ISZ™ 仕訳AI（shiwake.ai）](https://shiwake.ai/?utm_source=mcp&utm_medium=referral&utm_campaign=readme) の無料ツールと同じ計算エンジンで、登録・ログインは不要です。

- 公開エンドポイント（Streamable HTTP）: `https://mcp.shiwake.ai/mcp`
- ローカル（stdio）: `npx -y shiwake-ai-mcp`（登録番号の公表データとの照合は公開エンドポイントだけ。ローカルでは形式と検算）

## ツール

| ツール | 内容 | 同じ計算の Web ツール |
| :--- | :--- | :--- |
| `nencho_kanpu_shisan` | 年末調整の還付額・追加徴収額の試算（令和8年分・令和7年分） | https://shiwake.ai/tools/nencho/ |
| `kanjo_kamoku_kensaku` | 取引の内容から勘定科目・仕訳例・税区分を検索 | https://shiwake.ai/tools/kanjo-kamoku/ |
| `invoice_toroku_bango_check` | インボイス登録番号（T＋13桁）の形式・チェックディジットの確認と、国税庁の公表データとの照合（登録の有無・名称・取消／失効） | https://shiwake.ai/tools/invoice-number/ |
| `shohizei_hoshiki_hikaku` | 消費税の納付税額の比較（一般課税・簡易課税・2割特例・3割特例。仕入は積上げ・割戻しの両方） | https://shiwake.ai/tools/shohizei-hikaku/ |

どのツールも読み取り専用で、結果には根拠となる shiwake.ai のページへのリンクが付きます。結果は一般的な計算・処理の例で、個別の税務判断ではありません。

## 使い方

Claude Code:

```sh
claude mcp add --transport http shiwake-ai https://mcp.shiwake.ai/mcp
```

Claude Desktop・Cursor など（設定ファイル）:

```json
{
  "mcpServers": {
    "shiwake-ai": { "type": "http", "url": "https://mcp.shiwake.ai/mcp" }
  }
}
```

stdio で動かす場合:

```json
{
  "mcpServers": {
    "shiwake-ai": { "command": "npx", "args": ["-y", "shiwake-ai-mcp"] }
  }
}
```

聞き方の例: 「給与収入480万円、社会保険料72万円、源泉徴収税額12万円。年末調整でいくら戻る？」「ChatGPT の利用料の勘定科目は？」「T1120001160730 は正しい登録番号？」

## データの扱い

- ログイン・API キーは不要です。
- サーバーが記録するのは、呼ばれたツールの名前と成否だけです。入力した金額・番号・IP アドレスは記録しません。
- 利用の集中を防ぐため、接続元ごとに 1分あたり 60回までに制限しています。

## ISZ™ 仕訳AI について

**証憑から申告まで、ひとつのAIで。** [ISZ™ 仕訳AI](https://shiwake.ai/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-about) は、税理士・会計事務所のための AI税務会計プラットフォームです。自社で決算・申告をする中小法人・個人事業主も使えます。

- **証憑から申告まで1つで**：領収書・請求書・通帳の読み取り、仕訳、銀行照合、決算書、申告書と e-Tax・eLTAX 用データ、証憑の保管まで同じ画面で。人が見るのは、AI が理由つきで分けた「要確認」の仕訳だけです
- **会計・申告の機能は無料**：初期費用0円・月額の基本料金0円。帳簿・決算・申告・給与計算・年末調整の機能は無料（1人で使う場合）で、料金は AI の読み取り枚数とユーザーの追加だけです
- **乗り換えなくても始められる**：JDL・TKC・弥生・freee・マネーフォワードなど16社の会計ソフトの形式で書き出せるので、今のソフトのまま入力だけ任せられます
- **自社申告・個人事業主の確定申告にも**：[自社申告プラン](https://shiwake.ai/self/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-about)なら、中小法人の決算書・法人税・消費税、個人事業主の所得税の確定申告まで、申告書と e-Tax 用データを自社で作れます（[個人事業主の確定申告の流れ](https://shiwake.ai/guide/kojin-kakutei-shinkoku-app/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-about)）
- **委託先の審査に通せる**：日税連「AI・クラウド活用ガイドライン」の確認項目に対応。データは国内で保管し、AI の学習には使いません

- [MCP サーバーの解説（つなぎ方・freee／マネーフォワードの MCP との違い）](https://shiwake.ai/guide/kaikei-mcp/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-about)
- [会計事務所向け AI 記帳サービスの料金比較](https://shiwake.ai/guide/jimusho-ai-kicho-ryokin-hikaku/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-about)
- [税理士・経理のための無料ツール（40種類）](https://shiwake.ai/tools/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-about)
- [税金・会計の解説](https://shiwake.ai/guide/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-about)

## English

An MCP server that lets AI assistants (Claude, ChatGPT, Cursor, etc.) run Japanese tax and accounting calculations.
It uses the same calculation engine as the free tools on [ISZ™ Shiwake AI (shiwake.ai)](https://shiwake.ai/?utm_source=mcp&utm_medium=referral&utm_campaign=readme-en). No sign-up or API key required.

- Public endpoint (Streamable HTTP): `https://mcp.shiwake.ai/mcp`
- Local (stdio): `npx -y shiwake-ai-mcp` (matching against the National Tax Agency's published invoice registry is available only on the public endpoint; locally, the tool checks format and check digit only)

### Tools

| Tool | What it does | Web version |
| :--- | :--- | :--- |
| `nencho_kanpu_shisan` | Estimates the year-end tax adjustment (nenmatsu chosei) refund or additional withholding for Reiwa 8 (2026) and Reiwa 7 (2025) | https://shiwake.ai/tools/nencho/ |
| `kanjo_kamoku_kensaku` | Finds the account title (kanjo kamoku), sample journal entry and consumption tax category for a transaction | https://shiwake.ai/tools/kanjo-kamoku/ |
| `invoice_toroku_bango_check` | Validates qualified invoice registration numbers (T + 13 digits) and matches them against the National Tax Agency's published data (registered or not, name, cancellation/expiry) | https://shiwake.ai/tools/invoice-number/ |
| `shohizei_hoshiki_hikaku` | Compares consumption tax payable under the general method, simplified method, 20% special rule and 30% special rule | https://shiwake.ai/tools/shohizei-hikaku/ |

All tools are read-only, and every result links to the shiwake.ai page it is based on. Results are general calculation examples, not individual tax advice. Tool descriptions and results are in Japanese.

### Setup

Claude Code:

```sh
claude mcp add --transport http shiwake-ai https://mcp.shiwake.ai/mcp
```

Claude Desktop, Cursor, etc. (config file):

```json
{
  "mcpServers": {
    "shiwake-ai": { "type": "http", "url": "https://mcp.shiwake.ai/mcp" }
  }
}
```

### Data handling

- No login or API key required.
- The server logs only the tool name and whether the call succeeded. Amounts, registration numbers and IP addresses are not logged.
- Requests are limited to 60 per minute per client.

Guide (Japanese): https://shiwake.ai/guide/kaikei-mcp/


## 提供 / About us

[ISZ GROUP](https://iszgroup.com/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer) の AI チーム（[ISZ.AI](https://isz.ai/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer)）です。企業向けの AI システム開発と、2つの自社プロダクトを手がけています。

**[ISZ™ 仕訳AI](https://shiwake.ai/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer)** — 証憑から申告まで、ひとつのAIで。税理士・会計事務所、自社で申告する中小法人・個人事業主のための AI税務会計プラットフォーム（この MCP サーバーの提供元）

**[DenwaFlow](https://denwaflow.jp/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer)** — 予約・受注・問い合わせの電話を AI が受けて、最後まで完了する AI 電話受付
- [電話の予約受付・変更・キャンセルを自動化](https://denwaflow.jp/ai-phone-reservation/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer)
- 導入事例: [歯科クリニック（予約受付を24時間化）](https://denwaflow.jp/cases/dental-clinic-ai-phone/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer)・[美容室（電話対応時間を約70%削減）](https://denwaflow.jp/cases/salon-ai-phone/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer)

The AI team of [ISZ GROUP](https://iszgroup.com/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer) ([ISZ.AI](https://isz.ai/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer)). We build AI systems for businesses and two products of our own: **[ISZ™ Shiwake AI](https://shiwake.ai/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer-en)** (from receipts to tax filing, in one AI: an AI tax & accounting platform for tax accountants and accounting firms, and for small companies and sole proprietors filing their own returns; the provider of this MCP server) and **[DenwaFlow](https://denwaflow.jp/?utm_source=mcp-readme&utm_medium=referral&utm_campaign=readme-footer-en)** (an AI phone agent that takes reservations, orders and inquiries end to end).

提供: ISZ GROUP合同会社 / ISZ GROUP LLC
