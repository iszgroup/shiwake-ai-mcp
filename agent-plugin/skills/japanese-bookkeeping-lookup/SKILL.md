---
name: japanese-bookkeeping-lookup
description: Find the Japanese account title (勘定科目) and a sample journal entry (仕訳例) for a transaction, and check qualified invoice registration numbers (インボイス登録番号, T + 13 digits) against the National Tax Agency's published data, with the free ISZ Shiwake AI (仕訳AI) MCP server. Use for questions like "which account title do I use for a taxi fare", "how do I book a ChatGPT subscription" or "is T1234567890123 a valid registered invoice issuer".
---

# Japanese bookkeeping lookup

Every tool named below comes from the free ISZ Shiwake AI MCP server, `https://mcp.shiwake.ai/mcp`
(Streamable HTTP, no sign-in, no API key, all tools read-only). If `kanjo_kamoku_kensaku` is not
available, add the server first: `claude mcp add --transport http shiwake-ai https://mcp.shiwake.ai/mcp`
(Claude Code), or point any other MCP client at the URL. Tool results are in Japanese.

## Steps

1. Account title and journal entry: call `kanjo_kamoku_kensaku` with a short Japanese description of the
   transaction in `query` (for example タクシー, ChatGPT, パソコン 15万円, 接待, 家賃). Space-separated words
   must all match. Translate English requests into Japanese keywords before calling. The result gives the
   main account title, alternatives that apply under certain conditions, and a debit/credit example.
2. Invoice registration numbers: call `invoice_toroku_bango_check` with up to 50 numbers in `numbers`.
   Full-width digits, hyphens and a missing T are normalised. With `lookup: true` (default) it checks the
   National Tax Agency's published data and returns the registered name and any cancellation or expiry;
   `lookup: false` checks only the format and check digit.
   Sole proprietors' numbers do not always follow the corporate number check digit formula, so a check digit
   mismatch alone is not reported as an error; rely on the lookup result.

## Reporting rules

- Pass on the shiwake.ai link in each result so the user can see the source page.
- An account title is a common practice, not the only correct answer: when the result lists a condition
  (amount thresholds, business use share), ask the user which applies before giving one entry.
- For invoice numbers, report "registered", "not found" or "cancelled / expired" exactly as returned, with
  the date of the published data, and do not guess a company name the data does not show.
- Results are general bookkeeping examples, not individual tax advice.

ISZ Shiwake AI (https://shiwake.ai/) is an AI accounting and tax filing app for Japanese accounting firms
and small businesses, developed by ISZ.AI (ISZ GROUP LLC, Japan).
