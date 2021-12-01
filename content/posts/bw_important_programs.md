---
title: "BW important programs / Function modules "
date: 2021-11-04T11:15:20+01:00
tags: ["BW","ABAP","Function modules","Program"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Almost all of this programs are included into my github development "bw_toolbox". If you want, you can just implement this in easy way to your system. [Please check by clicking here](https://github.com/pawelwiejkut/bw_toolbox).


### Activate:

| Name                         	| Category 	| Description                                                                                                                    	|
|------------------------------	|----------	|--------------------------------------------------------------------------------------------------------------------------------	|
| RSDG_TRFN_ACTIVATE           	| TRFN     	| Activate transformations on the system.<br>If you are missing fields in source or target -<br>then it will not work correctly. 	|
| RSDS_DATASOURCE_ACTIVATE_ALL 	| RSDS     	| Activate data source                                                                                                           	|
| RSBKDTPREPAIR                	| DTP      	| Activate data transfer process                                                                                                 	|
| RSDG_HCPR_ACTIVATE           	| HCPR     	| Activate composite provider                                                                                                    	|
| RSDG_CUBE_ACTIVATE           	| CUBE     	| Activate cube                                                                                                                  	|
| RSDG_ADSO_ACTIVATE           	| ADSO     	| Activate Advanced Data Store Object                                                                                               |
| RSDG_IOBJ_ACTIVATE            | IOBJ      | Activate InfoObject                                                                                                               |      

## Maitenance:

| Name                       | Category | TYPE    | Description                         |
|----------------------------|----------|---------|-------------------------------------|
| RSDG_AFTER_IMPORT_FOR_CORR | N/A      | PROG | Reimport transport                  |
| RSBM_GUI_CHANGE_USTATE     | DTP      |         | Change DTP request status           |
| RSPC_VARIANT_DELETE        | RSPC     |         | Delete process chain variant        |
| RSPC_API_CHAIN_START       |          |  FM     |                                     |
| DB_DROP_TABLE              |          |         | Drop openhub tables                 |
| RSDG_IOBJ_REORG            | IOBJ     |         | Repair Infoobject                   |
| RSPC_PROCESS_FINISH        | RSPC     |         | Process chain variant status change |
| BAPI_USER_UNLOCK           | N/A      |         | Unlock user                         |
