---
title: "BW important programs / Function modules "
date: 2021-11-04T11:15:20+01:00
tags: ["BW","ABAP","Function modules","Program"]
lastmod: 2021-12-10T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Almost all of these programs are included in my GitHub development "bw_toolbox". If you want, you can just implement this in an easy way to your system. [Please check by clicking here](https://github.com/pawelwiejkut/bw_toolbox).


### Activate:

| Name                         | Category | Type | Description                                                                                                                |
|------------------------------|----------|------|----------------------------------------------------------------------------------------------------------------------------|
| RSDG_TRFN_ACTIVATE           | TRFN     | PROG | Activate transformations on the system. If you are missing fields in source or target - then it will not work correctly. |
| RSDS_DATASOURCE_ACTIVATE_ALL | RSDS     | PROG | Activate data source                                                                                                       |
| RSBKDTPREPAIR                | DTP      | PROG | Activate data transfer process                                                                                             |
| RSDG_HCPR_ACTIVATE           | HCPR     | PROG | Activate composite provider                                                                                                |
| RSDG_CUBE_ACTIVATE           | CUBE     | PROG | Activate cube                                                                                                              |
| RSDG_ADSO_ACTIVATE           | ADSO     | PROG | Activate Advanced DataStore Object                                                                                        |
| RSDG_IOBJ_ACTIVATE           | IOBJ     | PROG | Activate InfoObject                                                                                                        |

## Maintenance:

| Name                       | Category | Type | Description                                         |
|----------------------------|----------|------|-----------------------------------------------------|
| RSDG_AFTER_IMPORT_FOR_CORR | N/A      | PROG | Reimport transport                                  |
| RSBM_GUI_CHANGE_USTATE     | DTP      | FM   | Change DTP request status                           |
| RSPC_VARIANT_DELETE        | RSPC     | FM   | Delete process chain variant                        |
| RSPC_API_CHAIN_START       | RSPC     |  FM  | Start process chain  immediately ( even scheduled ) |
| DB_DROP_TABLE              | DEST     | PROG | Drop tables under the OpenHub                       |
| RSDG_IOBJ_REORG            | IOBJ     | PROG | Repair Infoobject                                   |
| RSPC_PROCESS_FINISH        | RSPC     | PROG | Process chain  variant status change                |
| BAPI_USER_UNLOCK           | N/A      | FM   | Unlock user                                         |