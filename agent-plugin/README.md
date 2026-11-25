# ISZ Shiwake AI (仕訳AI) — Japanese tax & accounting plugin

Agent Plugins v1 package (plugin.json + mcp.json + skills/) that connects an agent to the free
ISZ Shiwake AI MCP server at `https://mcp.shiwake.ai/mcp`. Configuration only: there is no local code.

AI エージェントから日本の税務・会計の計算を使えるプラグインです。接続先は ISZ 仕訳AI の無料 MCP サーバー
（https://mcp.shiwake.ai/mcp ・登録不要・読み取り専用）です。

## Tools

All nine tools are read-only. Results are in Japanese and link to the matching calculator on
[shiwake.ai](https://shiwake.ai/).

| Tool | What it does |
|---|---|
| `nencho_kanpu_shisan` | Year-end adjustment refund or additional tax (年末調整の還付額・追加徴収額), Reiwa 8 / 7 |
| `gensen_kyuyo_zeigaku` | Monthly withholding tax on salary from the National Tax Agency table (源泉徴収税額, 甲欄・乙欄) |
| `kyuyo_tedori_keisan` | Take-home pay and social insurance with Kyokai Kenpo rates (手取り・社会保険料) |
| `furusato_nozei_jogen` | Furusato nozei deduction limit (ふるさと納税の控除上限額) |
| `genka_shokyaku_keisan` | Depreciation schedule, straight-line or 200% declining balance (減価償却) |
| `entaizei_keisan` | Late-payment tax on national taxes (延滞税) |
| `shohizei_hoshiki_hikaku` | Consumption tax under general, simplified, 20% and 30% special rules (消費税の方式比較) |
| `kanjo_kamoku_kensaku` | Account title and sample journal entry for a transaction (勘定科目・仕訳例) |
| `invoice_toroku_bango_check` | Qualified invoice registration number check against National Tax Agency data (インボイス登録番号) |

## Skills

- `japanese-tax-calculations`: which calculator to use for payroll, year-end adjustment, furusato nozei,
  depreciation, late-payment tax and consumption tax questions, and how to report the result.
- `japanese-bookkeeping-lookup`: account titles, journal entries and invoice registration numbers.

## Disclosure

Hosted-only connector. Every tool call goes to mcp.shiwake.ai, run by ISZ GROUP LLC (Japan).
The tools take amounts, dates and invoice numbers; do not enter names or My Number. The package marks
the server untrusted, so Hermes asks before any tool that is not annotated read-only. The tool set is
served by the remote server at runtime. Results are general calculations under Japanese tax rules, not
individual tax advice.

## About

[ISZ Shiwake AI](https://shiwake.ai/) is an AI accounting and tax filing app for Japanese accounting firms
and small businesses: bookkeeping, financial statements, payroll and tax returns with e-Tax / eLTAX data
are free, and only the AI features use AI credits. Developed by [ISZ.AI](https://isz.ai/), the enterprise AI
brand of [ISZ GROUP LLC](https://iszgroup.com/) (Japan).

[ISZ 仕訳AI](https://shiwake.ai/) は、税理士事務所・中小企業向けの AI 会計・申告ソフトです。
開発：[ISZ.AI](https://isz.ai/)（[ISZ GROUP LLC](https://iszgroup.com/)・日本）
