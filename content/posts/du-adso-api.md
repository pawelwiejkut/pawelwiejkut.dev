---
title: "Direct Update ADSO ABAP API"
date: 2021-10-17T19:35:53+02:00
tags: ["BW","ABAP"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

How to insert the data into the BW ADSO on the BW on Hana and BW4HANA ?
Easy way is just to use official function module [delivered by SAP](https://help.sap.com/viewer/107a6e8a38b74ede94c833ca3b7b6f51/2.0.5/en-US/72e16c936fb94cffb71ce90edd5f8f8e.html)


{{< highlight abap >}}

CALL FUNCTION 'RSDSO_DU_WRITE_API'

{{< /highlight >}}

Example ADSO:


Example code:
