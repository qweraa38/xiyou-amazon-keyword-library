# Keyword-library workbook schema

The workbook is designed for an operator who needs both a reusable keyword pool and traceable evidence.

## Keyword library columns

The primary current/peak library tables should contain, in this order or an equivalent readable order:

1. 序号
2. Exact Keyword
3. 中文释义
4. coverage ASIN count and covered ASINs
5. union total, organic, advertising traffic
6. total acquisition rate and observed organic/ad ranks
7. latest observation time and rank details
8. each ASIN's total/organic/ad traffic and organic/ad rank
9. keyword market metrics: weekly search volume, ABA frequency rank, report dates, competitive difficulty, CPC, suggested bid range, click-conversion rate, organic rotation, top-ASIN shares
10. handling decision and period label

Evidence sheets should keep the same Exact Keyword -> 中文释义 adjacency and show the source ASIN, marketplace, window, and whether the phrase is a shared term or a single-ASIN observation.

## Trend and source pages

Use typed numeric cells for orders, traffic, ranks, prices, ratings, search volume, CPC, and ratios. Keep URLs and exact keyword phrases as text. Use a visible title, source subtitle, dark header row, wrapped long text, filters, frozen headers, and a reasonable column width. Large trend pages may be rendered to a representative first 40 rows for QA only; the workbook must retain the full data.

## Translation policy

Translate common German/English domain terms using a map. Preserve exact phrase spelling and keep unresolved fragments in the Chinese cell with a note such as 专名/词形保留：.... Do not translate away brand names, movie/IP names, typo variants, or opaque fragments. A non-empty Chinese cell is required even when the best result is a retained-term note.

## Peak-season policy

The peak sheet and per-ASIN peak evidence pages must show the requested prior-year window and actual returned count. If the keyword endpoint returns no historical rows, leave the table empty after the header, show 0 returned rows, and keep any separately returned monthly orders/traffic/ABA trends in their own pages.


