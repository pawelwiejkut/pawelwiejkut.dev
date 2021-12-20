---
title: "BW formula parameters"
date: 2021-12-20T09:13:49+01:00
tags: ["BW","BWFunctions","Class","Parameters"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

BW contains many standard formulas which can be used in TRFN's and RSPC's. The main issue is that sometimes you need to know default values / data types. 

All available formulas can be checked in class **CL_RSAR_FUNCTION**. Bellow, you can find a table with explained importing and returning parameters.
| Formula / Method Name  | Description                                                                                                     | Importing<br>Types<br>(Example)                      | Returning<br>Types<br>(Example<br>result) |
|------------------------|-----------------------------------------------------------------------------------------------------------------|------------------------------------------------------|-------------------------------------------|
| ABORT_PACKAGE          | Returns exception <br>cx_rfso_abort_package to stop<br>processing                                               | N/A                                                  | N/A                                       |
| ADD_TO_DATE            | Add days to the provided date                                                                                   | DATS,INT<br>(20201201,1)                             | DATS<br>20201202                          |
| ALPHA                  | Add leading zeros base on<br>provided length                                                                    | STRING,INT <br>(123,5)                               | STRING<br>00123                           |
| CALMONTH_FISCPER       | Convert calendar month <br>to the fiscal period                                                                 |                                                      |                                           |
| CONDENSE               | Trim text (left site)                                                                                           | STRING<br>( 43)                                      | STRING<br>'43'                            |
| CONDENSE_NO_GAPS       | Trim text + remove spaces inside                                                                                | STRING<br>( 43 55 33)                                | STRING<br>'435533'                        |
| DATECONV               | Change date format to internal                                                                                  | CHAR10,CHAR10,CHAR1<br>(12/07/1992,<br>MM/DD/YYYY,/) | DATS<br>19921207                          |
| DATE_DIFF              | Calculate differences between dates                                                                             | DATS,DATS<br>(20211212,20211215)                     | INT<br>3                                  |
| DATE_FISCPER           |                                                                                                                 |                                                      |                                           |
| DATE_FISCPER3          |                                                                                                                 |                                                      |                                           |
| DATE_FISCYEAR          |                                                                                                                 |                                                      |                                           |
| DATE_HALFYEAR          | Check is given date in first or <br>second half of the year                                                     | DATS<br>(20210212)                                   | NUMC<br>1                                 |
| DATE_MONTH             | Get calendar month from given date                                                                              | DATS<br>(20201201)                                   | NUMC<br>202012                            |
| DATE_MONTH2            | Get month number from given date                                                                                | DATS<br>(20201201)                                   | NUMC<br>12                                |
| DATE_QUATER            | Get quarter from given date                                                                                     | DATS<br>(20210909)                                   | NUMC<br>20213                             |
| DATE_QUATER1           | Get quarter number from given date                                                                              | DATS<br>(20210909)                                   | NUMC<br>3                                 |
| DATE_WEEK              | Get week from given date                                                                                        | DATS<br>(20210731)                                   | NUMC<br>202130                            |
| DATE_WEEKDAY           | Get day from given date                                                                                         | DATS<br>(20211220)                                   | STRING<br>Monday                          |
| DATE_WEEKDAY1          | Get day number from given date                                                                                  | DATS<br>(20211220)                                   | NUMC<br>1<br>[more](#explanations)        |
| DATE_YEAR              | Get year from given date                                                                                        | DATS<br>(20210101)                                   | NUMC<br>4                                 |
| FIRST_WORKINGDAY_MONTH | Get first workday from a given date <br>and calendar                                                            | DATS,CHAR<br>(20210425,01)                           | DATS<br>20210401                          |
| FIRST_WORKINGDAY_YEAR  | Get first workday from a given year<br>and calendar                                                             | DATS,CHAR<br>(20210525,01)                           | DATS<br>20210104                          |
| FISCPER_CALMONTH       |                                                                                                                 |                                                      |                                           |
| FISCPER_FISCPER3       |                                                                                                                 |                                                      |                                           |
| FISCPER_FISCYEAR       |                                                                                                                 |                                                      |                                           |
| IF                     | Check condition - <br>If I_Arg1 = X then Arg2 else Arg3                                                         | BOOLEAN,ANY,ANY<br>(X,1,10)                          | ANY<br>1                                  |
| IS_INITIAL             | Check is string initial                                                                                         | ANY<br>('')                                          | BOOLEAN<br>X                              |
| IS_INTEGER             | Check is string contains <br>only integers                                                                      | STRING<br>(9)                                        | BOOLEAN<br>X                              |
| LAST_WORKINGDAY_MONTH  | Get last workday from given date                                                                                | DATS,CHAR<br>(20210101,01)                           | DATS<br>(20210129)                        |
| LAST_WORKINGDAY_YEAR   | Get last year workday from <br>given date                                                                       | DATS,CHAR<br>(20210101,01)                           | DATS<br>(20211231)                        |
| LEFT                   | Get first X charters from the string                                                                            | INT,STRING<br>(4,123456)                             | STRING<br>1234                            |
| LTRIM                  | Trim text (left site), <br>by given regexp                                                                      | STRING,STRING<br>(' ABCD','\s')                      | STRING<br>'ABCD'                          |
| L_TRIM                 | Trim text (left site)                                                                                           | STRING<br>(' ABCD')                                  | STRING<br>'ABCD'                          |
| MAPPING                | Looks like deprecated <br>- almost all code inside commented<br>Result = Arg4                                   |                                                      |                                           |
| MONTH2_HALFYEAR        | Check is given month in first <br>or second half of the year                                                    | ANY<br>(202112)                                      | NUMC<br>2                                 |
| MONTH2_QUARTER1        | Check quarter of given month                                                                                    | ANY<br>(202208)                                      | NUMC<br>3                                 |
| MONTH_HALFYEAR         | Check is given month in the first <br>or second half of the year.<br>MONTH2_HALFYEAR has better <br>input check | ANY<br>(202112)                                      | NUMC<br>2                                 |

<h3>Explanations:</h3>
DATE_WEEKDAY1(): </br>
1 - Monday </br>
2 - Tuesday </br>
3 - Wednesday </br>
4 - Thursday </br>
5 - Friday </br>
6 - Saturday </br>
7 - Sunday </br> </br> 

If result of functions with names ending at '2' is same, then it is better to choose this one becouse usually the have better input check. MONTH2_QUARTER1 in example is checking month and year:</br> 

{{< highlight abap >}} 
 IF strlen( i_month ) EQ 6.
    l_month = i_month+4(2).
  ELSEIF strlen( i_month ) EQ 2.
    l_month = i_month.
  ELSE.
    RAISE EXCEPTION TYPE cx_foev_error_in_function.
  ENDIF.
{{< /highlight >}}
  
{{< highlight abap >}} 
    l_check = i_month+4(2).
  IF l_check < '01' OR l_check > '12'.

    RAISE EXCEPTION TYPE cx_foev_error_in_function.
  ELSE.
{{< /highlight >}}
