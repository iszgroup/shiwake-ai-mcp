---
name: japanese-tax-calculations
description: Calculate Japanese payroll and tax figures with the free ISZ Shiwake AI (仕訳AI) MCP server - year-end adjustment refund or additional tax (年末調整), monthly withholding tax from the National Tax Agency table (源泉徴収税額), take-home pay and social insurance (手取り・社会保険料), furusato nozei deduction limit (ふるさと納税), depreciation (減価償却), late-payment tax (延滞税) and the consumption tax method comparison (一般課税・簡易課税・2割特例・3割特例). Use for questions like "how much will my year-end adjustment refund be", "what is the withholding tax on a 300,000 yen salary" or "is the 20% special rule cheaper for me".
---

# Japanese tax calculations

Every tool named below comes from the free ISZ Shiwake AI MCP server, `https://mcp.shiwake.ai/mcp`
(Streamable HTTP, no sign-in, no API key, all tools read-only). If `nencho_kanpu_shisan` is not available,
add the server first: `claude mcp add --transport http shiwake-ai https://mcp.shiwake.ai/mcp` (Claude Code),
or point any other MCP client at the URL. Tool results are in Japanese; translate them for the user when
the conversation is in another language.

## Choose the tool

- Year-end adjustment refund or shortfall: `nencho_kanpu_shisan`. Needs the annual `salary`; pass
  `social_insurance` and `withheld_tax` from the payslips or withholding slip, plus spouse, dependents and
  insurance deductions when the user has them. Defaults to Reiwa 8 (2026); `year: 2025` for Reiwa 7. Salary
  income only.
- Monthly withholding tax on salary: `gensen_kyuyo_zeigaku` with `amount_after_social_insurance` (gross pay
  minus non-taxable commuting allowance and the employee's social insurance), `dependents`, and
  `column: kou` (dependents declaration filed) or `otsu`. Give `pay_date` so the right tax year's table is used.
- Take-home pay and social insurance: `kyuyo_tedori_keisan` with `monthly_pay`, `age` and `prefecture`
  (Kyokai Kenpo rates). Returns health insurance, pension, employment insurance, income tax and the
  employer's share.
- Furusato nozei limit: `furusato_nozei_jogen` with `salary` (or `other_income`) and family details.
  Covers donations made in 2026.
- Depreciation schedule: `genka_shokyaku_keisan` with `cost`, `useful_life`, `in_service_date`, `method`
  (`straight` or `declining` for 200% declining balance) and `closing_month`.
- Late-payment tax: `entaizei_keisan` with `tax`, `legal_due_date` and `paid_date`; set `kind` and
  `filed_date` for late, amended or corrected returns.
- Consumption tax method comparison: `shohizei_hoshiki_hikaku` with `taxpayer`, the period, taxable sales
  by rate and purchases. It computes general, simplified, 20% and 30% special rule amounts and marks the
  lowest method the business can actually use.

## Reporting rules

- Every result links to the matching calculator page on shiwake.ai. Pass that link on so the user can
  check the same numbers.
- Results are general calculations under Japanese tax rules, not individual tax advice. Say so when the
  user is about to act on a figure, and suggest a zeirishi (tax accountant) for edge cases.
- Never ask for or pass names, My Number or other personal identifiers; the tools only need amounts and
  dates.
- When an input is missing, ask for it or state the assumption you used (for example social insurance
  estimated at 15% of salary in `furusato_nozei_jogen`).

ISZ Shiwake AI (https://shiwake.ai/) is an AI accounting and tax filing app for Japanese accounting firms
and small businesses, developed by ISZ.AI (ISZ GROUP LLC, Japan).
