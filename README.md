# ISZ™ 仕訳AI MCP サーバー（shiwake.ai）

[![npm](https://img.shields.io/npm/v/shiwake-ai-mcp)](https://www.npmjs.com/package/shiwake-ai-mcp) [![MCP endpoint](https://img.shields.io/badge/MCP-mcp.shiwake.ai-blue)](https://shiwake.ai/guide/kaikei-mcp/)

日本語 | [English](#english)

> 提供: [ISZ™ 仕訳AI](https://shiwake.ai/)（記帳から決算・申告までをひとつで進められる AI 会計・申告ソフト）・姉妹プロダクト [DenwaFlow](https://denwaflow.jp/)（AI 電話受付）

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

聞き方の例: 「給与収入480万円、社会保険料72万円、源泉徴収税額12万円。年末調整でいくら戻る？」「ChatGPT の利用料の勘定科目は？」「T1120001160730 は正しい登録番号？」

## データの扱い

- ログイン・API キーは不要です。
- ツールに入力した金額・番号・取引の内容と、計算の結果は記録しません。記録するのは、どのツールが使われたか・成否などの利用状況だけです（[プライバシーポリシー](https://shiwake.ai/mcp/privacy/)）。
- 利用の集中を防ぐため、接続元ごとに 1分あたり 60回までに制限しています。

## ISZ™ 仕訳AI について

[ISZ™ 仕訳AI（シワケAI／Shiwake AI）](https://shiwake.ai/)は、税理士事務所・中小企業向けの AI 会計・申告ソフトです。
領収書・請求書・通帳を AI が読み取って仕訳にし、帳簿・決算書から、法人税・消費税・地方税・所得税の申告書と e-Tax・eLTAX 用データ、給与計算・年末調整・法定調書まで、同じ画面で作成できます。仕訳は JDL・TKC・弥生など16社の会計ソフトの取込形式でも出力できるので、いまの会計ソフトのまま AI 仕訳だけ取り入れることもできます。会計・申告の基本機能は無料、AI は利用量に応じた料金です。

**すべての機能を、立場に合わせて使えます。**

- **税理士事務所・会計事務所**：顧問先の記帳から決算・申告まで、事務所の中で完結。顧問先からの証憑回収、AI が分けた「要確認」だけのチェック、今の会計ソフト（JDL・TKC・弥生など16社）への書き出しにも対応（[事務所向けの料金比較](https://shiwake.ai/guide/jimusho-ai-kicho-ryokin-hikaku/)）
- **自社で経理・申告する中小法人・ひとり社長**：帳簿から決算書、法人税・消費税の申告、e-Tax まで自社で（[自社申告プラン](https://shiwake.ai/self/)）
- **個人事業主**：帳簿から青色申告決算書・確定申告書、e-Tax まで（[個人事業主の確定申告のやり方](https://shiwake.ai/guide/kojin-kakutei-shinkoku-app/)）

あわせて：[MCP サーバーの解説](https://shiwake.ai/guide/kaikei-mcp/)・[無料ツール（40種類以上）](https://shiwake.ai/tools/)・[税金・会計の解説](https://shiwake.ai/guide/)

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

### Data handling

- No login or API key required.
- Amounts, registration numbers, transaction details and results are not logged. We record only usage information such as which tool was called and whether it succeeded ([privacy policy](https://shiwake.ai/mcp/privacy/)).
- Requests are limited to 60 per minute per client.

### About ISZ™ Shiwake AI

[ISZ™ Shiwake AI (シワケAI)](https://shiwake.ai/) is AI accounting and tax filing software for Japanese accounting firms (zeirishi offices) and small businesses.
AI reads receipts, invoices and bank statements and turns them into journal entries. From there you can produce ledgers and financial statements, corporate, consumption, local and income tax returns with e-Tax/eLTAX data, and payroll, year-end adjustment and statutory reports, all on the same screen. Journal entries can also be exported in the import formats of 16 Japanese accounting packages including JDL, TKC and Yayoi, so you can add AI bookkeeping without changing your current software. Core accounting and tax filing features are free; AI is priced by usage.

**Every feature, used the way you work:**

- **Tax accountants and accounting firms**: handle clients from bookkeeping to closing and tax filing in-house, with receipt collection from clients, review of only the entries AI flags, and export to 16 accounting software formats including JDL, TKC and Yayoi ([pricing for firms, Japanese](https://shiwake.ai/guide/jimusho-ai-kicho-ryokin-hikaku/))
- **Small companies and solo founders filing their own returns**: from bookkeeping to financial statements, corporate and consumption tax returns, and e-Tax ([self-filing plan](https://shiwake.ai/self/))
- **Sole proprietors**: from bookkeeping to blue-return statements, income tax returns, and e-Tax ([guide, Japanese](https://shiwake.ai/guide/kojin-kakutei-shinkoku-app/))

More: [free tools (40+)](https://shiwake.ai/tools/) · [tax & accounting guides](https://shiwake.ai/guide/)

Guide (Japanese): [https://shiwake.ai](https://shiwake.ai/guide/kaikei-mcp/)


## 提供 / About us

[ISZ GROUP](https://iszgroup.com/) の AI チーム（[ISZ.AI](https://isz.ai/)）です。企業向けの AI システム開発と、2つの自社プロダクトを手がけています。

**[ISZ™ 仕訳AI](https://shiwake.ai/)** — 記帳から決算・申告までをひとつで進められる AI 会計・申告ソフト（この MCP サーバーの提供元）

**[DenwaFlow](https://denwaflow.jp/)** — 予約・受注・問い合わせの電話を AI が受けて、最後まで完了する AI 電話受付
- [電話の予約受付・変更・キャンセルを自動化](https://denwaflow.jp/ai-phone-reservation/)
- 導入事例: [歯科クリニック（予約受付を24時間化）](https://denwaflow.jp/cases/dental-clinic-ai-phone/)・[美容室（電話対応時間を約70%削減）](https://denwaflow.jp/cases/salon-ai-phone/)

The AI team of [ISZ GROUP](https://iszgroup.com/) ([ISZ.AI](https://isz.ai/)). We build AI systems for businesses and two products of our own: **[ISZ™ Shiwake AI](https://shiwake.ai/)** (AI accounting and tax filing software that takes you from bookkeeping to year-end closing and tax returns in one place; the provider of this MCP server) and **[DenwaFlow](https://denwaflow.jp/)** (an AI phone agent that takes reservations, orders and inquiries end to end).

提供: ISZ GROUP合同会社 / ISZ GROUP LLC
