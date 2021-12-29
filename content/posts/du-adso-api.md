---
title: "Direct Update ADSO ABAP API"
date: 2021-10-17T19:35:53+02:00
tags: ["BW","ABAP"]
aliases : [ du_adso_api ]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

How to insert the data into the BW ADSO on the BW on Hana and BW4HANA ?
The easy way is just to use the official function module [delivered by SAP](https://help.sap.com/viewer/107a6e8a38b74ede94c833ca3b7b6f51/2.0.5/en-US/72e16c936fb94cffb71ce90edd5f8f8e.html)

Example ADSO:
<img src="/adso_api_1.png" width="80%" />

Example code:

{{< highlight abap >}}

REPORT zadsoamdp.

DATA: lt_data TYPE STANDARD TABLE OF /bic/aadsoamdp2,
      lt_msg  TYPE rs_t_msg.

APPEND VALUE #( field1 = '1' field2 = '2'  ) TO lt_data.

CALL FUNCTION 'RSDSO_DU_WRITE_API'
  EXPORTING
    i_adsonm            = 'ADSOAMDP'
    it_data             = lt_data
  IMPORTING
    et_msg              = lt_msg
  EXCEPTIONS
    write_failed        = 1
    datastore_not_found = 2
    OTHERS              = 3.
IF sy-subrc <> 0.
  MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
    WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
ENDIF.

cl_demo_output=>display(
  EXPORTING
    data = lt_msg
).

{{< /highlight >}}