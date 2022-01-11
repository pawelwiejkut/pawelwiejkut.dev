---
title: "Usefull ABAP statements for TRFNs"
date: 2022-01-11T21:09:22+01:00
tags: ["BW","ABAP"]
TocOpen: true
ShowToc: true
draft : true
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Useful modern ABAP statements for TRFNs.

### Moving data from one internal table to another 

Move only required records from one table to another:

Previously:
{{< highlight abap >}}
LOOP AT lt_source INTO ls_source WHERE column_a = 'value'.
 APPEND ls_source TO lt_result.
ENDLOOP.
{{< / highlight>}}

Now:
{{< highlight abap >}}
lt_result = VALUE #( FOR ls_source IN lt_source WHERE ( column_a = 'value' ) ( ls_source )).
{{< / highlight>}}

### Fill table with data 

Previously:
{{< highlight abap >}}
ls_source-column_a = 'value'.
ls_source-column_b = 'value_b'.
ls_source-column_c = 'value_c'.

APPEND ls_source to lt_result.
{{< / highlight>}}

Now (create):
{{< highlight abap >}}
lt_result = VALUE #( ( column_a = 'value' column_b = 'value_b' column_c = 'value_c' ) ).
{{< / highlight>}}

Second good example (add new values):
{{< highlight abap >}}
INSERT VALUE #( column_a = 'value' column_b = 'value_b' column_c = 'value_c' ) TO lt_result.
{{< / highlight>}}

### Read data from the table 

Previously:
{{< highlight abap >}}
READ TABLE lt_result WITH KEY colum_a = 'value_a' INTO DATA ls_result.
{{< / highlight>}}

Now:
{{< highlight abap >}}
TRY.
 ls_result = lt_result[ colum_a = 'value_a' ].
CATCH cx_sy_itab_line_not_found.
ENDTRY.
{{< / highlight>}}

### Pass corresponding data between internal tables

Previously:
{{< highlight abap >}}
MOVE-CORRESPONDING lt_source to lt_result.
{{< / highlight>}}

Now:
{{< highlight abap >}}
lt_result = CORRESPONDING #( lt_source ).
{{< / highlight>}}

### Union of internal tables

Previously:
{{< highlight abap >}}
{{< / highlight>}}

Now:
{{< highlight abap >}}
lt_result = corresponding #(  base ( lt_result )  lt_table ).
{{< / highlight>}}

### Get number of lines in the table

Previously:
{{< highlight abap >}}
DESCRIBE lt_result INTO lv_number_of_entries.
{{< / highlight>}}

Now:
{{< highlight abap >}}
v_number_of_entries = lines( lt_result  ).
{{< / highlight>}}

### Concatenate strings

Previously:
{{< highlight abap >}}

{{< / highlight>}}

Now:
{{< highlight abap >}}

{{< / highlight>}}


