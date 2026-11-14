---
name: xiyou-amazon-keyword-library
description: Research Amazon.de competitor ASIN keywords with 西柚/Xiyou, including current and prior-year peak-season data, sales, traffic, market metrics, trends, and a Chinese-translation keyword-library workbook. Use when the user asks to research ASIN keywords, build a keyword library, or requests all available 西柚 data interfaces.
---

# 西柚 Amazon.de 关键词词库

Use this skill for a repeatable Amazon Germany ASIN-research workflow. The deliverable is a reviewable .xlsx keyword library, not a listing upload and not a claim that competitor facts apply to the user's product.

## Required defaults

- Marketplace: DE.
- Current window: the latest snapshot returned by 西柚.
- Peak-season comparison: October–December of the prior year. With the current 2026 workflow, use 2025-10 through 2025-12; if the user gives another year, follow the user.
- Keep the user's exact raw request in user_task on every 西柚 call in the same task. Put only the purpose of the individual call in intent_summary.
- Deduplicate repeated ASINs for analysis, but preserve inputAsins, inputCount, uniqueCount, and duplicateAsins in the workbook.
- Never pad missing rows, infer historical keywords from current data, or turn a traffic/BSR estimate into revenue.

## Research coverage

For each unique ASIN, run all applicable 西柚 interfaces and retain the raw-return meaning:

1. Product info and category tree.
2. Current multi-ASIN keyword comparison and prior-year monthly comparison.
3. Single-ASIN current keywords, prior-year monthly keywords, and a recent 30-day daily keyword reverse lookup.
4. Batch keyword market info for every unique current/peak term, in batches of at most 100: weekly search volume, ABA rank, CPC/suggested bids, competitive difficulty, click-conversion rate, organic rotation, and top-ASIN shares.
5. Current 30-day orders and prior-year monthly order trends.
6. Current overall traffic plus daily, weekly, and monthly traffic trends.
7. Keyword-count trends, BSR trends, price/rating/product-info trends, product-info changes, ad changes, and variations.
8. ABA weekly trends for the highest-traffic combined terms in both the prior-year peak window and the current comparison window.

Read references/endpoint-matrix.md before making calls when the tool schema or returned field names are unfamiliar. If an interface returns an explicit date-range limitation or empty historical result, preserve the notice and label the result as unavailable rather than substituting another period.

## Call and data-handling rules

- Use the xydc MCP tools. Every call must include country: "DE", the exact user_task, and a concise intent_summary.
- Use page_size: 10000 with page: 1 when the endpoint supports full retrieval. For get_keyword_info and get_keyword_aba_trends, batch at 100 terms.
- Sort keyword lists by total traffic descending unless the user requests another sort.
- Treat searchTerm as an exact phrase for duplicate and coverage analysis. Compare case-insensitively, but do not split phrases, normalize spelling, stem, or merge typo variants.
- Preserve numeric values as numeric spreadsheet cells where possible. Preserve strings such as Infinity, NaN, and empty values as returned, with a nearby note when they affect interpretation.
- Keep current and prior-year peak data in separate source structures and separate workbook sheets. If a peak keyword endpoint is empty, show zero returned rows and the interface notice.
- Keep per-ASIN evidence separate. A keyword that appears in a union table must not be copied into an ASIN evidence page unless that ASIN is present in the row's per-ASIN result.
- Treat orders as 西柚 order/sales estimates for the stated window, not sales revenue, profit, or confirmed Seller Central data.
- Treat keyword market metrics as keyword-level market data, not as the ASIN's own traffic.

## Workbook requirements

Use the spreadsheet skill and @oai/artifact-tool for authoring. Before the first create/edit operation, run the current runtime's mark_artifact_operation_started.mjs once with --operation-kind create --expected-output-count 1 --output-format xlsx. Recalculate before checks and export.

At minimum, the workbook should contain:

- 关键词总览: ASIN input/dedup summary, current/peak keyword counts, market-metric count, current 30-day orders, peak monthly order summary, and a current top-keyword view.
- 关键词库_当前 and 关键词库_去年旺季: deduplicated exact phrases, coverage, total/organic/ad traffic, rank observations, market metrics, handling decision, and Chinese translation.
- One current and one peak evidence sheet per ASIN.
- 销量与商品信息, 流量结构, 商品全量信息, 单品关键词计数, 日级反查关键词, 关键词数量趋势, 订单趋势, 流量趋势_月度, 流量趋势_周度, 流量趋势_日度, BSR趋势, 商品信息趋势, 商品信息变更, 广告变更, 变体关系, ABA趋势_去年旺季, ABA趋势_当前, 接口返回状态, and 口径与说明 when the corresponding endpoint returned data.

Every keyword-bearing page must place 中文释义 immediately to the right of Exact Keyword. Keep the original German phrase unchanged. Use a controlled translation map for common domain terms, and mark unresolved brand names, spelling variants, and opaque fragments as retained rather than inventing a translation.

The workbook should state the collection date, marketplace, current-window definition, peak window, requested versus actual row counts, interface limitations, and the fact that competitor keywords and titles are observations rather than proof of the user's product facts.

## Validation before delivery

1. Check the input/dedup ASIN counts and every supplied ASIN's current/peak evidence.
2. Reconcile current/peak keyword totals, market-metric totals, per-ASIN keyword counts, current orders, and prior-year monthly orders against the saved research structures.
3. Verify that keyword translation columns are present and immediately adjacent on every keyword-bearing sheet.
4. Scan for formula errors such as #REF!, #DIV/0!, #VALUE!, #N/A, and #NAME?.
5. Render and inspect every worksheet. Fix clipped headers, broken tables, unreadable wrapped text, ####, missing repeated headers, and blank ABA data caused by nested batch-return structures.
6. Export only the requested final .xlsx unless the user asks for intermediate files. In the final response, cite the final workbook once with purpose="output".


