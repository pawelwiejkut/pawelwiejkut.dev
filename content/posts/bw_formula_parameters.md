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

| Formula / Method Name | Description                                                       | Importing<br>Types<br>(Example)                      | Returning<br>Types<br>(Example<br>result) |
|-----------------------|-------------------------------------------------------------------|------------------------------------------------------|-------------------------------------------|
| ABORT_PACKAGE         | Returns exception <br>cx_rfso_abort_package to stop<br>processing | N/A                                                  | N/A                                       |
| ADD_TO_DATE           | Add days to the provided date                                     | DATS,INT<br>(20201201,1)                             | DATS<br>20201202                          |
| ALPHA                 | Add leading zeros base on<br>provided length                      | STRING,INT <br>(123,5)                               | STRING<br>00123                           |
| CALMONTH_FISCPER      | Convert calendar month <br>to the fiscal period                   |                                                      |                                           |
| CONDENSE              | Trim text (left site)                                             | STRING<br>( 43)                                      | STRING<br>'43'                            |
| CONDENSE_NO_GAPS      | Trim text + remove spaces inside                                  | STRING<br>( 43 55 33)                                | STRING<br>'435533'                        |
| DATECONV              | Change date format to internal                                    | CHAR10,CHAR10,CHAR1<br>(12/07/1992,<br>MM/DD/YYYY,/) | DATS<br>19921207                          |
| DATE_DIFF             | Calculate differences between dates                               | DATS,DATS<br>(20211212,20211215)                     | INT<br>3                                  |
| DATE_FISCPER          |                                                                   |                                                      |                                           |
| DATE_FISCPER3         |                                                                   |                                                      |                                           |
| DATE_FISCYEAR         |                                                                   |                                                      |                                           |
| DATE_HALFYEAR         | Check is given date in first or second<br>half of the year        | DATS<br>(20210212)                                   | NUMC<br>1                                 |
| DATE_MONTH            | Get calendar month from given date                                | DATS<br>(20201201)                                   | NUMC<br>202012                            |
| DATE_MONTH2           | Get month number from given date                                  | DATS<br>(20201201)                                   | NUMC<br>12                                |
| DATE_QUATER           | Get quarter from given date                                       | DATS<br>(20210909)                                   | NUMC<br>20213                             |
| DATE_QUATER1          | Get quarter number from given date                                | DATS<br>(20210909)                                   | NUMC<br>3                                 |
| DATE_WEEK             | Get week from given date                                          | DATS<br>(20210731)                                   | NUMC<br>202130                            |
| DATE_WEEKDAY          | Get day from given date                                           | DATS<br>(20211220)                                   | STRING<br>Monday                          |
| DATE_WEEKDAY1         | Get day number from given date                                    | DATS<br>(20211220)                                   | NUMC<br>1<br>[more](#explanations)        |

<h3>Explanations:</h3>
DATE_WEEKDAY1(): </br>
1 - Monday </br>
2 - Tuesday </br>
3 - Wednesday </br>
4 - Thursday </br>
5 - Friday </br>
6 - Saturday </br>
7 - Sunday </br>
