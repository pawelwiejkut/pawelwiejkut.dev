---
title: "ABAP1909 HANA Login Details"
date: 2022-01-28T14:53:45+01:00
tags: ["HANA","Login","Password"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

If you want to login into HANA DB on ABAP1909 platform - in the example to create a calculation view, change something please use bellow details:

For the tentant database **SYSTEMDB** (i.e to make some administrative changes):</br> 
user SYSTEM with the password Ldtf5432</br></br>
For the single-container database **HDB** (i.e to make some development):</br> 
user SAPA4H with the password Ldtf5432

In both cases, the instance number is 02. Example in Eclipse:

{{<figure align=center src="/abap1909_hana_login_details/1.png"  width="80%" >}}

{{<figure align=center src="/abap1909_hana_login_details/2.png"  width="80%" >}}









