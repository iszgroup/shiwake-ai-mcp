# ISZ™ 仕訳AI MCP サーバー（shiwake.ai）

[![npm](https://badgen.net/npm/v/shiwake-ai-mcp)](https://www.npmjs.com/package/shiwake-ai-mcp) [![MCP endpoint](https://badgen.net/badge/MCP/mcp.shiwake.ai/blue)](https://shiwake.ai/mcp/) [![iszgroup/shiwake-ai-mcp MCP server](https://glama.ai/mcp/servers/iszgroup/shiwake-ai-mcp/badges/score.svg)](https://glama.ai/mcp/servers/iszgroup/shiwake-ai-mcp)

日本語 | [English](#english)

> 提供: [ISZ™ 仕訳AI](https://shiwake.ai/)（記帳から決算・申告までをひとつで進められる AI 会計・申告ソフト）

日本の税務・会計の計算を、AI アシスタント（Claude・ChatGPT・Cursor など）から使えるようにする MCP サーバーです。
[ISZ™ 仕訳AI（shiwake.ai）](https://shiwake.ai/) の無料ツールと同じ計算エンジンで、登録・ログインは不要です。

- 公開エンドポイント（Streamable HTTP）: `https://mcp.shiwake.ai/mcp`
- ローカル（stdio）: `npx -y shiwake-ai-mcp`（登録番号の公表データとの照合は公開エンドポイントだけ。ローカルでは形式と検算）

## ツール

| ツール | 内容 | 同じ計算の Web ツール |
| :--- | :--- | :--- |
| `nencho_kanpu_shisan` | 年末調整の還付額・追加徴収額の試算（令和8年分・令和7年分） | https://shiwake.ai/tools/nencho/ |
| `kanjo_kamoku_kensaku` | 取引の内容から勘定科目・仕訳例・税区分を検索 | https://shiwake.ai/tools/kanjo-kamoku/ |
| `invoice_toroku_bango_check` | インボイス登録番号（T＋13桁）の形式・チェックディジットの確認と、国税庁の公表データとの照合（登録の有無・名称・取消／失効） | https://shiwake.ai/tools/invoice-number/ |
| `shohizei_hoshiki_hikaku` | 消費税の納付税額の比較（一般課税・簡易課税・2割特例・3割特例。仕入は積上げ・割戻しの両方） | https://shiwake.ai/tools/shohizei-hikaku/ |
| `gensen_kyuyo_zeigaku` | 給与の源泉徴収税額（月額表 甲欄・乙欄、電算機計算の特例。令和7〜9年分） | https://shiwake.ai/tools/gensen-kyuyo/ |
| `furusato_nozei_jogen` | ふるさと納税の控除上限額の目安（自己負担2,000円で済む寄附額と控除の内訳） | https://shiwake.ai/tools/furusato/ |
| `entaizei_keisan` | 延滞税の計算（2か月以内・2か月を過ぎた後の割合を年ごとに。期限後申告・修正申告・更正、一部納付に対応） | https://shiwake.ai/tools/entaizei/ |
| `genka_shokyaku_keisan` | 減価償却費（定額法・200%定率法）の各年度の償却額と期末帳簿価額、少額資産・一括償却の判定 | https://shiwake.ai/tools/genka-shokyaku/ |
| `kyuyo_tedori_keisan` | 給与の手取り額と社会保険料（協会けんぽ・厚生年金・雇用保険・源泉所得税。会社負担も） | https://shiwake.ai/tools/kyuyo-tedori/ ・ https://shiwake.ai/tools/shakai-hoken/ |

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

Antigravity CLI（`~/.gemini/config/mcp_config.json`。接続先は `serverUrl`）:

```json
{
  "mcpServers": {
    "shiwake-ai": { "serverUrl": "https://mcp.shiwake.ai/mcp" }
  }
}
```

Gemini CLI（拡張機能として追加。このリポジトリの `gemini-extension.json` を読み込みます）:

```sh
gemini extensions install https://github.com/iszgroup/shiwake-ai-mcp
```

ほかのアプリの手順: [MCP サーバーの案内（shiwake.ai/mcp/）](https://shiwake.ai/mcp/)

聞き方の例: 「給与収入480万円、社会保険料72万円、源泉徴収税額12万円。年末調整でいくら戻る？」「ChatGPT の利用料の勘定科目は？」「T1120001160730 は正しい登録番号？」

## ISZ 仕訳AI と MCP / ISZ Shiwake AI and MCP

ISZ 仕訳AI（https://shiwake.ai/）は、日本の税理士事務所と、自社で記帳・決算・申告を行う中小企業（一人社長の法人を含む）・個人事業主向けの AI 記帳・会計・申告ソフトです。この MCP サーバーは、その計算エンジンを AI アシスタントから登録なしで使えるようにしたものです。

### 機能の対応表

| 機能 | ISZ 仕訳AI（アプリ） | ISZ 仕訳AI MCP |
|---|---|---|
| 税金の計算（年末調整の還付額・源泉徴収税額・手取りと社会保険料・ふるさと納税・減価償却・延滞税・消費税の方式比較） | ○ | ○ |
| 勘定科目・仕訳例の検索 | ○ | ○ |
| インボイス登録番号のチェック（国税庁の公表データと照合） | ○ | ○ |
| レシート・領収書・請求書・通帳の AI OCR 読み取りと自動仕訳（スマホ撮影を含む） | ○ | 計画中 |
| 仕訳の誤り・税務リスクの点検 | ○ | 計画中 |
| JDL・TKC・弥生・freee・マネーフォワードなどとの仕訳データ連携（CSV など各社形式の書き出し・取り込み。顧問先と事務所でソフトが違うときの受け渡しや乗り換えを含む） | ○ | 計画中 |
| 決算書と、法人税・消費税・所得税（青色申告決算書・確定申告書）の申告書・e-Tax 用データ | ○ | 計画中 |
| 従業員の年末調整（申告書の回収・まとめて確定・源泉徴収票） | ○ | 1人分の試算のみ |
| 複数の顧問先・職員（担当と権限）の管理 | ○ | 計画中 |

MCP の「計画中」は、ログイン版（限定テスト中）で対応を予定している機能です。いまの公開版は登録不要・読み取り専用です。

### よくある質問
**この MCP は会計ソフトに書き込みますか？**
いまの公開版は読み取り専用で、書き込みません。

**計算結果をそのまま申告に使えますか？**
この MCP の出力は一般的な計算・処理の例で、申告書ではなく、個別の税務判断でもありません。

### English
ISZ Shiwake AI (https://shiwake.ai/) is an AI bookkeeping, accounting and tax filing app for Japanese accounting firms (zeirishi offices), SMBs (including one-person companies) and sole proprietors. This MCP server makes its calculation engine available to AI assistants without sign-in. The table above compares the app and the MCP: the MCP currently offers tax calculations, account title search and invoice number lookup; the other features are available in the app and planned for the sign-in MCP (in limited testing).

開発：ISZ.AI（ISZ GROUP合同会社・大阪）https://isz.ai/ ／ Developed by ISZ.AI (ISZ Group LLC, Osaka, Japan).

## データの扱い

- ログイン・API キーは不要です。
- ツールに入力した金額・番号・取引の内容と、計算の結果は記録しません。記録するのは、どのツールが使われたか・成否などの利用状況だけです（[プライバシーポリシー](https://shiwake.ai/mcp/privacy/)）。
- 利用の集中を防ぐため、接続元ごとに 1分あたり 60回までに制限しています。

## お問い合わせ

不具合・ご質問は contact@isz.ai（ISZ GROUP合同会社）までご連絡ください。GitHub の Issues でも受け付けます。

## English

An MCP server that lets AI assistants (Claude, ChatGPT, Cursor, etc.) run Japanese tax and accounting calculations.
It uses the same calculation engine as the free tools on [ISZ™ Shiwake AI (shiwake.ai)](https://shiwake.ai/). No sign-up or API key required.

- Public endpoint (Streamable HTTP): `https://mcp.shiwake.ai/mcp`
- Local (stdio): `npx -y shiwake-ai-mcp` (matching against the National Tax Agency's published invoice registry is available only on the public endpoint; locally, the tool checks format and check digit only)

### Tools

| Tool | What it does | Web version |
| :--- | :--- | :--- |
| `nencho_kanpu_shisan` | Estimates the year-end tax adjustment (nenmatsu chosei) refund or additional withholding for Reiwa 8 (2026) and Reiwa 7 (2025) | https://shiwake.ai/tools/nencho/ |
| `kanjo_kamoku_kensaku` | Finds the account title (kanjo kamoku), sample journal entry and consumption tax category for a transaction | https://shiwake.ai/tools/kanjo-kamoku/ |
| `invoice_toroku_bango_check` | Validates qualified invoice registration numbers (T + 13 digits) and matches them against the National Tax Agency's published data (registered or not, name, cancellation/expiry) | https://shiwake.ai/tools/invoice-number/ |
| `shohizei_hoshiki_hikaku` | Compares consumption tax payable under the general method, simplified method, 20% special rule and 30% special rule | https://shiwake.ai/tools/shohizei-hikaku/ |
| `gensen_kyuyo_zeigaku` | Monthly income tax withholding on salary (NTA monthly table, columns A and B, 2025 to 2027) | https://shiwake.ai/tools/gensen-kyuyo/ |
| `furusato_nozei_jogen` | Estimates the furusato nozei (hometown tax donation) limit where the out-of-pocket cost stays at 2,000 yen | https://shiwake.ai/tools/furusato/ |
| `entaizei_keisan` | Calculates delinquent tax (entaizei) on national taxes, split into the first two months and after, with yearly rates | https://shiwake.ai/tools/entaizei/ |
| `genka_shokyaku_keisan` | Depreciation schedule (straight-line or 200% declining-balance) with yearly amounts and book values, plus small-asset options | https://shiwake.ai/tools/genka-shokyaku/ |
| `kyuyo_tedori_keisan` | Monthly take-home pay with social insurance premiums (Kyokai Kenpo health insurance, pension, employment insurance) and withholding tax | https://shiwake.ai/tools/kyuyo-tedori/ |

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

Antigravity CLI (`~/.gemini/config/mcp_config.json`, use `serverUrl`):

```json
{
  "mcpServers": {
    "shiwake-ai": { "serverUrl": "https://mcp.shiwake.ai/mcp" }
  }
}
```

Gemini CLI (as an extension, using this repository's `gemini-extension.json`):

```sh
gemini extensions install https://github.com/iszgroup/shiwake-ai-mcp
```

### Data handling

- No login or API key required.
- Amounts, registration numbers, transaction details and results are not logged. We record only usage information such as which tool was called and whether it succeeded ([privacy policy](https://shiwake.ai/mcp/privacy/)).
- Requests are limited to 60 per minute per client.

### Support

For bugs or questions, contact contact@isz.ai (ISZ GROUP LLC) or open a GitHub issue.

Guide (Japanese): [https://shiwake.ai/mcp/](https://shiwake.ai/mcp/)


## 提供 / About us

[ISZ GROUP](https://iszgroup.com/) の AI チーム（[ISZ.AI](https://isz.ai/)）です。自社プロダクト：[ISZ 仕訳AI](https://shiwake.ai/)（この MCP サーバーの提供元）・[DenwaFlow](https://denwaflow.jp/)（AI 電話受付）。

The AI team of [ISZ GROUP](https://iszgroup.com/) ([ISZ.AI](https://isz.ai/)). Our products: [ISZ Shiwake AI](https://shiwake.ai/) (the provider of this MCP server) and [DenwaFlow](https://denwaflow.jp/) (AI phone agent).

提供: ISZ GROUP合同会社 / ISZ GROUP LLC
