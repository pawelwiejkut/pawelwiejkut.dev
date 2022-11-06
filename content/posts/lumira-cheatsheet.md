---
title: "Lumira cheatsheet"
date: 2022-11-06T17:30:24+01:00
tags: ["Lumira","Cheatsheet","language"]
aliases : [ call_function_table ]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## How to check dahsboard in different language ?

To check the dashboard display in different language, please add following parameters to the URL:</br></br>
LANGUAGE=EN</br>
COUNTRY=US</br></br>
Example: http://example.com:9999//BOE/OpenDocument/opendoc/openDocument.jsp?sIDType=CUID&iDocID=xji8HAJksao<mark>&LANGUAGE=EN&COUNTRY=US</mark>

## How to set up query template

In Lumira, you don't have to create separate dashboard for each query if it should look and work the same way. You can crate one dahsboard with one datasource and use following parameters:</br></br>
XQUERY=technical_name_of_bw_query</br>
XSYSTEM=cuid:olap_connection_cuid</br></br>
Example: http://example.com:9999//BOE/OpenDocument/opendoc/openDocument.jsp?sIDType=CUID&iDocID=xji8HAJksao<mark>&XQUERY=ZBW_FI_Q001&XSYSTEM=cuid:jKIoa98a</mark>
</br></br>
Also a small entry in the startup script of the template is required:
{{< highlight js >}}
DS_1.assignDataSource(XSYSTEM, DataSourceType.QUERY, XQUERY);
{{< /highlight >}}
</br>
More:</br>
[https://answers.sap.com/questions/409169/datasource-generic-global-template-in-lumira-21.html](https://answers.sap.com/questions/409169/datasource-generic-global-template-in-lumira-21.html)</br>
[https://answers.sap.com/questions/13310814/report-to-report-interface-in-lumira.html](https://answers.sap.com/questions/13310814/report-to-report-interface-in-lumira.html)








