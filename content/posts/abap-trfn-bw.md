---
title: "Useful modern ABAP statements for BW transformations"
date: 2022-01-11T21:21:22+01:00
tags: ["BW","ABAP"]
TocOpen: true
ShowToc: true
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Since ABAP 7.4 SAP introduced a lot of inline declarations. Never the less in BW world many developments are still written in very old syntax, where some of them are even not supported by the cloud version of ABAP (Steampunk). If you want to check out a modern ABAP statements that can be used in BW then this article is definatelly for you. Every example contains a previous and a new version to compare. If you want to check more information how to write a clean abap code, check out [check this website](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md) where is a official guide from SAP.

### Moving data from one internal table to another 

Move only required records from one table to another:

Previously: put a where into the LOOP
{{< highlight abap >}}
LOOP AT lt_source INTO ls_source WHERE column_a = 'value'.
 APPEND ls_source TO lt_result.
ENDLOOP.
{{< / highlight>}}

Now: use a VALUE with WHERE
{{< highlight abap >}}
lt_result = VALUE #( FOR ls_source IN lt_source WHERE ( column_a = 'value' ) ( ls_source )).
{{< / highlight>}}

### Fill table with data 

Previously: declare a structure and assign separately all values in new lines.
{{< highlight abap >}}

DATA: ls_source type ty_source,
      lt_result type t_ty_result.

ls_source-column_a = 'value'.
ls_source-column_b = 'value_b'.
ls_source-column_c = 'value_c'.

APPEND ls_source to lt_result.
{{< / highlight>}}

Now: create a table and insert the values in the same time
{{< highlight abap >}}
DATA(lt_result) = VALUE t_ty_result( ( column_a = 'value' column_b = 'value_b' column_c = 'value_c' ) ).
{{< / highlight>}}

OR insert the value to the existing table
{{< highlight abap >}}
DATA: lt_result type t_ty_result.
INSERT VALUE #( column_a = 'value' column_b = 'value_b' column_c = 'value_c' ) TO lt_result.
{{< / highlight>}}

### Read data from the table 

Previously: using READ TABLE
{{< highlight abap >}}
READ TABLE lt_result WITH KEY colum_a = 'value_a' INTO DATA ls_result.
{{< / highlight>}}

Now: use function and <mark>catch exception</mark>
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

It can be also nicely used in ABAP OO:

{{< highlight abap >}}
cl_test_class->method(EXPORTING iv_source = CORRESPONDING #(lt_result)).
{{< / highlight>}}

### Union of internal tables

Previously:
{{< highlight abap >}}
LOOP AT lt_table ASSIGING FIELD-SYMBOL(<ls_table>).
 APPEND <ls_table> TO lt_result.
ENDLOOP.
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
CONCATENATE lv_string_x 'aaa' lv_string_y INTO DATA(lv_result).
{{< / highlight>}}

Now:
{{< highlight abap >}}
DATA(lv_result) = |{ lv_string_x } 'aaa' { lv_string_y }|.
{{< / highlight>}}

### Upper case

Previously:
{{< highlight abap >}}
TRANSLATE lv_result TO UPPER-CASE.
{{< / highlight>}}

Now:
{{< highlight abap >}}
lv_result = to_upper( lv_result  ).
{{< / highlight>}}

Very similar approach also for:</br> [More](https://help.sap.com/doc/abapdocu_752_index_htm/7.52/en-US/abenprocess_functions.htm)
| function                                 | desciption                             |
|------------------------------------------|----------------------------------------|
| cmax, cmin                               | character-like extreme value functions |
| condense                                 | condense function                      |
| concat_lines_of                          | concatenation function                 |
| escape                                   | escape function                        |
| insert                                   | insert function                        |
| match                                    | match function                         |
| repeat                                   | repeat function                        |
| replace                                  | replace function                       |
| reverse                                  | reverse function                       |
| segment                                  | segment function                       |
| shift_left, shift_right                  | shift functions                        |
| substring, substring                     | substring functions                    |
| to_upper, to_lower, to_mixed, from_mixed | case functions                         |
| translate                                | translate function                     |

[More](https://help.sap.com/doc/abapdocu_752_index_htm/7.52/en-US/abenprocess_functions.htm)


### Table lines

Previously:
{{< highlight abap >}}
DESCRIBE lt_table LINES lv_table_lines.
{{< / highlight>}}

Now:
{{< highlight abap >}}
lv_table_lines = lines( lt_lines  ).
{{< / highlight>}}

[More](https://help.sap.com/doc/abapdocu_751_index_htm/7.51/en-us/abentable_functions.htm)

### Dynamic variable declarations

Previously:
Declare separately variable and assign value to it.
{{< highlight abap >}}
DATA : lv_integer type i.
lv_integer = 1.
{{< / highlight>}}

Now:
Declare and assign value in one line.
{{< highlight abap >}}
DATA(lv_integer) = 1.
{{< / highlight>}}

It can be also used in the context of the ABAP OO.<mark>Note that function modules are not supported</mark>.

Previously:
You have to declare separately variable lv_integer and then use it in the method. 
{{< highlight abap >}}
DATA : lv_integer type i.
cl_test_class->method( IMPORTING ev_integer = lv_integer  ).
{{< / highlight>}}

Now:
You can declare lv_integer directly after method IMPORTING, EXPORTING or RETURNING.
{{< highlight abap >}}
cl_test_class->method( IMPORTING ev_integer = DATA(lv_integer)  ).
{{< / highlight>}}

### Create a new object

Previously: Declare data reference and then create an object
{{< highlight abap >}}
DATA : lro_class type cl_test_class.
CREATE OBJECT lro_class 
   EXPORTING iv_integer = 1.
{{< / highlight>}}

Now: Create an object without the data declaration by the NEW parameter
{{< highlight abap >}}
DATA(lro_class) = NEW cl_test_class( iv_integer = 1 ).
{{< / highlight>}}
