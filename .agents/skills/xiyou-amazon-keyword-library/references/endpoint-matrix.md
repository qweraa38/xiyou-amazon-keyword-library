# 西柚 endpoint matrix

Use this as a routing checklist. Tool names are the xydc MCP names; field names can vary slightly by endpoint version, so preserve the returned shape in the raw research JSON and map only the fields needed for the workbook.

| Research area | Interface(s) | Required window / notes |
|---|---|---|
| Product facts | get_asin_info | Current product title, brand, price, rating, category tree, size/weight, dates, URL |
| Multi-ASIN current keywords | get_multi_asin_keyword_comparison | Latest available current snapshot; keep exact searchTerm, ranks, traffic, coverage |
| Multi-ASIN peak keywords | get_multi_asin_keyword_comparison_monthly | Prior-year October–December by default |
| Single-ASIN keywords | get_asin_keywords | Current full page |
| Single-ASIN peak keywords | get_asin_keywords_monthly | Prior-year October–December |
| Daily keyword reverse lookup | get_asin_keywords_daily | Recent 30 days; endpoint max is 30 days per call |
| Keyword market metrics | get_keyword_info | Every unique current/peak term, max 100 terms per call |
| Keyword ABA trends | get_keyword_aba_trends | Top combined terms, max 100 terms per call; run current and peak windows |
| Orders | get_asin_orders_last_30_days, get_asin_order_trends | Current 30 days and prior-year October–December monthly orders |
| Overall traffic | get_asin_traffic | Current organic/ad term counts and traffic |
| Traffic trends | get_asin_traffic_trends, get_asin_traffic_trends_monthly, get_asin_traffic_trends_weekly | From prior-year October to latest available current date |
| Keyword-count trends | get_asin_keyword_count_trends | From prior-year October to latest available current date |
| BSR | get_asin_bsr_trends | From prior-year October to latest available current date |
| Product-info trends | get_asin_info_trends | Price, deal, promotion, stars, ratings |
| Product-info changes | get_asin_info_change_trends | Title/image changes and date notices |
| Advertising changes | get_asin_ad_change_trends | Preserve added campaign/activity arrays |
| Variations | get_asin_variations | Parent, children, dimensions, distribution |

## Interface-status handling

For every call, retain status code, date-range notice, returned row count, and a compact raw-size/status record. A successful HTTP/business status with zero rows is still a valid result and must be shown as zero returned rows. Do not silently replace it with current data.


