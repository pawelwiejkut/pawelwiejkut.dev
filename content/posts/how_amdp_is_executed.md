---
title: "How AMDP TRFN is executed"
date: 2021-11-11T22:58:24+02:00
tags: ["AMDP","TRFN","BW"]
editPost:
draft: true
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
ADSO definition:


TRFN definition:

In general execution looks like:
ABAP Method->Call SQL on HANA->Execute ... -> select

Step by step:
1. From ABAP site:
cl_rstran_db_stat=>execute_haap() is executed with SQL like:

{{< highlight sql >}}
SELECT "FIELD1"  AS "FIELD1" , "0RECORDMODE"  AS "RECORDMODE" , "RECORD"  AS "RECORD"  FROM "SAPA4H"."/1BCAMDP/0BW:DAP:TR_04TFNXDAAVG5T5E8AZJ239HYT"  ('PLACEHOLDER'=('$$aggregation$$','"BW_HAP__________DB_AGGREGATION"='''''), 'PLACEHOLDER'=('$$client$$','001'), 'PLACEHOLDER'=('$$keydate$$','20211110'), 'PLACEHOLDER'=('$$langu$$','E'), 'PLACEHOLDER'=('$$objvers$$','"OBJVERS" = ''A'''), 'PLACEHOLDER'=('$$shift_decimal_places$$','"BW_HAP__________SHIFT_DECIMAL_PLACES"=''I'''), 'PLACEHOLDER'=('TR_04TFNXDAAVG5T5E8AZJ239HYT.$$adso_dtp_extraction_mode$$','"_IS_FULL_KEY" = 1 AND ( ("1TECHPROV_KEY" = ''ZAMDP$C'' OR "1TECHPROV_KEY" = ''ZAMDP'' ) )'), 'PLACEHOLDER'=('TR_04TFNXDAAVG5T5E8AZJ239HYT.$$runid$$','"BW_HAP__________RUNID"=''96SBW6PMF5XU9CAGGGHRMDRSY'' AND "BW_HAP__________HAP_SEQ_NUMBER"=''0'''),'PLACEHOLDER' = ('ce_settings', '{"enable_partitioned_execution": "0", "ceqo_enable_rownum_expr_general": "1"}')  )   WITH HINT ( ROUTE_BY_CARDINALITY("/BIC/AZAMDP2") )
{{< /highlight >}}

This is a 

2.

