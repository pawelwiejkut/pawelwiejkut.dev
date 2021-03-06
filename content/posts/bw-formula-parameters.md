---
title: "BW formula parameters"
date: 2021-12-20T09:13:49+01:00
tags: ["BW","BWFunctions","Class","Parameters"]
aliases : [ bw_formula_parameters ]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
BW contains many standard formulas which can be used in TRFN's and RSPC's. The main issue is that sometimes you need to know default values/data types. 

All available formulas can be checked in class **CL_RSAR_FUNCTION**. Bellow, you can find a table with explained importing and returning parameters.

| Formula / Method Name       | Description                                                                                                                                        | Importing<br>Types<br>(Example)                      | Returning<br>Types<br>(Example<br>result) |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|-------------------------------------------|
| ABORT_PACKAGE               | Returns exception <br>cx_rfso_abort_package to stop<br>processing                                                                                  | N/A                                                  | N/A                                       |
| ADD_TO_DATE                 | Add days to the specified date                                                                                                                     | DATS,INT<br>(20201201,1)                             | DATS<br>20201202                          |
| ALPHA                       | Add leading zeros base on<br> the provided length                                                                                                       | STRING,INT <br>(123,5)                               | STRING<br>00123                           |
| CALMONTH_FISCPER            | Convert calendar month <br>to the fiscal period                                                                                                    |                                                      |                                           |
| CONDENSE                    | Trim text (left site)                                                                                                                              | STRING<br>( 43)                                      | STRING<br>'43'                            |
| CONDENSE_NO_GAPS            | Trim text + remove spaces inside                                                                                                                   | STRING<br>( 43 55 33)                                | STRING<br>'435533'                        |
| DATECONV                    | Change date format to internal                                                                                                                     | CHAR10,CHAR10,CHAR1<br>(12/07/1992,<br>MM/DD/YYYY,/) | DATS<br>19921207                          |
| DATE_DIFF                   | Calculate differences between dates                                                                                                                | DATS,DATS<br>(20211212,20211215)                     | INT<br>3                                  |
| DATE_FISCPER                |                                                                                                                                                    |                                                      |                                           |
| DATE_FISCPER3               |                                                                                                                                                    |                                                      |                                           |
| DATE_FISCYEAR               |                                                                                                                                                    |                                                      |                                           |
| DATE_HALFYEAR               | Check if the date is in the first <br> or second part of the year                                                                                       | DATS<br>(20210212)                                   | NUMC<br>1                                 |
| DATE_MONTH                  | Get the calendar month from the given date                                                                                                                | DATS<br>(20201201)                                   | NUMC<br>202012                            |
| DATE_MONTH2                 | Get the month number from the given date                                                                                                                   | DATS<br>(20201201)                                   | NUMC<br>12                                |
| DATE_QUATER                 | Get the quarter from the given date                                                                                                                        | DATS<br>(20210909)                                   | NUMC<br>20213                             |
| DATE_QUATER1                | Get the quarter number from the given date                                                                                                                 | DATS<br>(20210909)                                   | NUMC<br>3                                 |
| DATE_WEEK                   | Get the week from the given date                                                                                                                           | DATS<br>(20210731)                                   | NUMC<br>202130                            |
| DATE_WEEKDAY                | Get the day from the given date                                                                                                                            | DATS<br>(20211220)                                   | STRING<br>Monday                          |
| DATE_WEEKDAY1               | Get the day number from given date                                                                                                                     | DATS<br>(20211220)                                   | NUMC<br>1<br>[more](#explanations)        |
| DATE_YEAR                   | Get the year from the given date                                                                                                                           | DATS<br>(20210101)                                   | NUMC<br>4                                 |
| FIRST_WORKINGDAY_MONTH      | Get the first working day from the given date <br>and calendar                                                                                               | DATS,CHAR<br>(20210425,01)                           | DATS<br>20210401                          |
| FIRST_WORKINGDAY_YEAR       | Get the first working day of the year<br>and calendar                                                                                                | DATS,CHAR<br>(20210525,01)                           | DATS<br>20210104                          |
| FISCPER_CALMONTH            |                                                                                                                                                    |                                                      |                                           |
| FISCPER_FISCPER3            |                                                                                                                                                    |                                                      |                                           |
| FISCPER_FISCYEAR            |                                                                                                                                                    |                                                      |                                           |
| IF                          | Check condition - <br>If I_Arg1 = X then Arg2 else Arg3                                                                                            | BOOLEAN,ANY,ANY<br>(X,1,10)                          | ANY<br>1                                  |
| IS_INITIAL                  | Check if the string is initial                                                                                                                            | ANY<br>('')                                          | BOOLEAN<br>X                              |
| IS_INTEGER                  | Check if the string contains <br>only integers                                                                                                         | STRING<br>(9)                                        | BOOLEAN<br>X                              |
| LAST_WORKINGDAY_MONTH       | Get the last working day from the given date                                                                                                                   | DATS,CHAR<br>(20210101,01)                           | DATS<br>20210129                          |
| LAST_WORKINGDAY_YEAR        | Get the last working day of the year from <br>the date given                                                                                                           | DATS,CHAR<br>(20210101,01)                           | DATS<br>20211231                          |
| LEFT                        | Get the first X characters from the string                                                                                                               | INT,STRING<br>(4,123456)                             | STRING<br>1234                            |
| LTRIM                       | Trim text (left site), <br>by given regexp                                                                                                         | STRING,STRING<br>( ABCD,\s)                          | STRING<br>'ABCD'                          |
| L_TRIM                      | Trim text (left site)                                                                                                                              | STRING<br>( ABCD)                                    | STRING<br>'ABCD'                          |
| MAPPING                     | Looks like deprecated <br>- almost all code inside commented out<br>Result = Arg4                                                                      |                                                      |                                           |
| MONTH2_HALFYEAR             | Check if the month is in the first or second half of the year                                                                                       | ANY<br>(202112) or (11)                              | NUMC<br>2                                 |
| MONTH2_QUARTER1             | Check the quarter of the month                                                                                                                       | ANY<br>(202208) or (08)                              | NUMC<br>3                                 |
| MONTH_HALFYEAR              | Check if the month is in the first <br>or second half of the year.                                                                                  | ANY<br>(202112)                                      | NUMC<br>2                                 |
| MONTH2_QUARTER1             | Get the quarter based on the given date                                                                                                                    | ANY<br>(202106) or (06)                              | NUMC<br>2                                 |
| MONTH_HALFYEAR              | Check is given month in first or <br>second half of the year                                                                                       | ANY<br>(20211)                                       | NUMC<br>2                                 |
| MONTH_QUARTER               | Check the quarter of the given month                                                                                                                       | ANY<br>(202208)                                      | NUMC<br>202003                            |
| MONTH_QUARTER1              | Check the quarter of the given month                                                                                                                       | ANY<br>(202208)                                      | NUMC<br>3                                 |
| MONTH_YEAR                  | Check the month of the given date                                                                                                                          | ANY<br>(202111) or (20211125)                        | NUMC<br>2021                              |
| NEGATIVE                    | Return number with negative sing                                                                                                                   | F<br>(1)                                             | F<br>-1                                   |
| QUARTER1_HALFYEAR           | Check if given quarter is in first or<br>second half of the year                                                                                      | ANY<br>(202101)                                      | NUMC<br>1                                 |
| QUARTER_HALFYEAR            | Check if given quarter is in first or <br>second half of the year                                                                                     | ANY<br>(20214)                                       | NUMC<br>2                                 |
| QUARTER_QUARTER1            | Get the quarter from the given quarter                                                                                                                     | ANY<br>(20214)                                       | NUMC<br>4                                 |
| QUARTER_YEAR                | Get the year from the given quarter                                                                                                                        | ANY<br>(20211)                                       | NUMC<br>2021                              |
| REPLACE_ALL                 | Replace selected charter <br>to different one                                                                                                      | C,C,STRING<br>(4,9,A4B4C4)                           | STRING<br>A9B9C9                          |
| REPLACE_FIRST               | Replace first occurrences of the <br>charters to different one                                                                                     | C,C,STRING<br>(4,9,A4B4C4)                           | STRING<br>A9B4C4                          |
| RIGHT                       | Get first few numbers from right                                                                                                                   | I,STRING<br>(4,123456)                               | STRING<br>3456                            |
| RTRIM                       | Trim white charters from right <br>based on provided regexp                                                                                        | STRING,STRING<br>(ABC,\s)                         | STRING<br>'ABC'                           |
| R_TRIM                      | ?                                                                                                                                                  | C<br>(D)                                           | STRING<br>D                               |
| SHIFT_LEFT                  | Remove first few <br>charters from the left site<br>of the string [more](https://help.sap.com/doc/abapdocu_751_index_htm/7.51/en-us/abapshift.htm) | I,STRING<br>(2,abcdef)                               | STRING<br>cdef                            |
| SHIFT_RIGHT                 | Add few<br>charters from the left site<br>of the string [more](https://help.sap.com/doc/abapdocu_751_index_htm/7.51/en-us/abapshift.htm)           | I,STRING<br>(2,abcdef)                               | STRING<br>'  abcdef'                      |
| SKIP_RECORD                 | Raise CX_RSFO_SKIP_RECORD <br>exception to skip <br>processing of current record                                                                   | N/A                                                  | N/A                                       |
| SKIP_RECORD_AS_ERROR        | Raise CX_RSFO_SKIP_RECORD<br>_AS_ERROR exception to <br>skip current record <br>processing with error                                              | N/A                                                  | N/A                                       |
| STR_LEN                     | Returns the length of the string                                                                                                                   | STRING<br>abcdef                                     | INT<br>6                                  |
| UNIT_CONVERSION             | Convert units                                                                                                                                      | UNIT,UNIT,ANY<br>(TO,KG,100)                         | F<br>100000                               |
| UTC_LONG_TO_<br>LOCAL_DATE  | Convert timestamp based on <br>selected timezone <br>to get the date                                                                               | DEC,CHAR<br>(20161030053000,EST)                     | DATS<br>20161030                          |
| UTC_LONG_TO_<br>LOCAL_TIME  | Convert timestamp based on <br>selected timezone <br>to  get the hour                                                                              | DEC,CHAR<br>(20161030053000,EST)                     | F<br>5.40                                 |
| UTC_SHORT_TO_<br>LOCAL_DATE | Convert timestamp based on <br>selected timezone <br>to get the date <br>(same code like for long <br>version)                                     | DEC,CHAR<br>(20161030053000,EST)                     | DATS<br>20161030                          |
| UTC_SHORT_TO_<br>LOCAL_TIME | Convert timestamp based on <br>selected timezone <br>to get the hour                                                                               | DEC,CHAR<br>(20161030053000,EST)                     | TIMS<br>013000                            |
| WEEK_FIRST_DAY              | Get the first day of the week                                                                                                                          | NUMC<br>(202104)                                     | DATS<br>20210125                          |
| WORKINGDAY_MONTH            | Get the number of working <br>days based on <br>month                                                                                              | DATS,CHAR,CHAR<br>(20211220,01,+)                    | INT<br>14                                 |
| WORKINGDAY_YEAR             | Get the number of working day <br>base on<br>year                                                                                                      | DATS,CHAR,CHAR<br>(20211220,01,+)                    | INT<br>243                                |

### Explanations:
DATE_WEEKDAY1(): </br>
1 - Monday </br>
2 - Tuesday </br>
3 - Wednesday </br>
4 - Thursday </br>
5 - Friday </br>
6 - Saturday </br>
7 - Sunday </br> </br> 

If the result of functions with names ending at '2' is the same, then probably the version with 2 at the end can handle both inputs (with a year or without). MONTH2_QUARTER1 in the example is checking both month and a year + month :</br> 
 
{{< highlight abap >}} 
 IF strlen( i_month ) EQ 6.
    l_month = i_month+4(2).
  ELSEIF strlen( i_month ) EQ 2.
    l_month = i_month.
  ELSE.
    RAISE EXCEPTION TYPE cx_foev_error_in_function.
  ENDIF.
{{< /highlight >}}

MONTH_QUARTER1 is checking only the year + month like 202106
  
{{< highlight abap >}} 
    l_check = i_month+4(2).
  IF l_check < '01' OR l_check > '12'.

    RAISE EXCEPTION TYPE cx_foev_error_in_function.
  ELSE.
{{< /highlight >}}
