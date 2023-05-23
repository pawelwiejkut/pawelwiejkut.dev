---
title: "How to trace BW BPC Authorization"
date: 2022-06-04T21:23:34+02:00
tags: ["bw","bpc","sap","auth"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
description:
---

Process of building authorization in BW with, and without BPC, is different. Reason is user authorization are enhanced by roles assigned to them in BPC administration panel. For more information about this process you can search for Data Access Profiles (DAPs).

## Common ways
Common ways to check the BW auth is:

1. Execute query on the affected user in rsudo - But it may not be enough, please check [more](#bpc)
2. Check authorization log using SU53
3. Trace authorization using ST01, STAUTHTRACE or similar

## BPC
Most important difference is that user is sometimes able to execute the query in rsrt, but in the same time is not able to execute the BPC Planing workbook laing on the same object. After opening the workbook, before the prompts user will see issue like:

You do not have sufficient authorization for the infoprovider.

But how to trace it to find the root cause ? Solution is very simple:

1. Go to RSUDO
2. Make sure that ABAP BICS is selected
3. In the text box bellow put: <br>
{{<highlight abap>}}
&environment=<yourenvironment>&model=<yourmodel>
{{</highlight>}}
4. If you do not know the enviroment and model - please open the BPC workbook: 
{{<figure align=center src="/check_bpc_authorization/1.png"  width="50%" alt="EXCEL AFO BPC tab" >}}
5. At the end it should look like on the image bellow:
{{<figure align=center src="/check_bpc_authorization/2.png"  width="70%" alt="EXCEL AFO BPC tab" >}}

Good blog about the BPC authorization:</br>
https://thirdrock.com.au/2017/10/01/demystifying-sap-bpc-embedded-security-blog-004/

Important SAP Note:</br>
https://launchpad.support.sap.com/#/notes/2366358


