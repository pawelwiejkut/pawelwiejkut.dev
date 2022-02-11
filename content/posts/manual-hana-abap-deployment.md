---
title: "Manual deployment from ABAP to SAP HANA"
date: 2022-02-11T17:45:44+01:00
tags: ["BW","ABAP","HANA"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
description: "Bellow you can find my notes about the manual deployment from ABAP Application Server to the HANA Database. This kind of activity can be done in example for Calculation Views."
Victor_Hugo: "true"
Focus_Keyword: "Manual deployment from ABAP to SAP HANA"
---
Normally BW objects are transported to HANA using a transportation system, but what can be done when transport fails? When you have authorization to repat the import - it is still ok. You can go to Sap Transport Management system (transaction: STMS) and reimport. Thinks get much more complicated when you do not have the necessary rights. Let me share with you my notes about this process.


## Authorization 
To manually deploy ABAP objects to SAP Hana databse you need a following authorization:

{{<highlight abap>}}
  AUTHORITY-CHECK OBJECT 'S_DEVELOP' ID 'ACTVT' FIELD '07' ID 'OBJTYPE' FIELD 'HOTA' ID 'OBJNAME' DUMMY ID 'DEVCLASS' DUMMY ID 'P_GROUP' DUMMY.
{{</highlight>}}

which is checked in all described in this article cases. This is because finally all executions comes through rddhanadeployment report. It contains method "execute_hana_deployment" used in all processes.

## How to deploy
If you want o deploy some object manually, then the easiest method is to use transaction **SCTS_HTA_DEPLOY** or report **SCTS_HOTA_ORGANIZER**. Lets consider a following scenario: Your transport with the Hana Views failed because of the issues with the source. You can't see new calculation views on the database. After fixing the issues with the view sources, you can just run this transaction and reimport missing views manually.

{{<figure align=center src="/manual_hana_abap_deployment/1.png"  width="100%" alt="Transaction screen" >}}

## Technical way
If you can't (or don't want to) use transaction, then you have a few other ways of manual execution. Please check report **RDDHANADEPLOYMENT** which can be used to manually deploy all objects included into the ABAP transport.

{{<figure align=center src="/manual_hana_abap_deployment/2.png"  width="90%" alt="RDDHANADEPLOYMENT" >}}

For other alternatives check class **CL_HOT_WB_ACCESS** used for transports of HANA objects. Here method "ACTIVATE_OBJECTS" can be usefull. Most complicated possibility is to use class **CL_CTS_HTA_API_FACTORY** and run i.e. "CREATE_OBJECTS_BY_TROBJ_NAME" method. As a attribute it takes the object name in ABAP transport format, so with space (but not trimmed).

More informations about the deployment transaction can be found in the [offical SAP documentation](https://help.sap.com/doc/saphelp_nw75/7.5.5/en-US/1a/63b656853844698cdff4d908808906/content.htm?no_cache=true).If you want to read more about the ransport concepts, check also [this blog](https://blog.maruskin.eu/2020/08/few-words-about-sap-transports.html).

