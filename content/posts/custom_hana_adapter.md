---
title: "Developing custom HANA adapter – quickstart"
date: 2020-10-18T20:44:24+02:00
tags: ["HANA","Adapter","Java","Eclipse","Data provisioning"]
lastmod: 2021-12-11T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

In this blog post, I will show you how you can fast start with developing custom HANA adapters in JAVA.

1. S-User is required to download data provisioning agent:
https://launchpad.support.sap.com/#/softwarecenter/template/products/%20_APP=00200682500000001943&_EVENT=DISPHIER&HEADER=Y&FUNCTIONBAR=N&EVENT=TREE&NE=NAVIGATE&ENR=73555000100200005999&V=MAINT&TA=ACTUAL&PAGE=SEARCH/HANA%20DP%20AGENT%202.0
I downloaded the Linux version, but windows should work too (I’m on Mac OS).

<img src="/custom_hana_adapter/1.png" width="80%" />

2. I will proceed in SAP Hana Studio because Eclipse is missing some packages. If you don’t have SAP Hana Studio, please check: https://launchpad.support.sap.com/#/softwarecenter/template/products/%20_APP=00200682500000001943&_EVENT=DISPHIER&HEADER=Y&FUNCTIONBAR=N&EVENT=TREE&NE=NAVIGATE&ENR=73554900100200000585&V=MAINT&TA=ACTUAL&PAGE=SEARCH/SAP%20HANA%20STUDIO%202

<img src="/custom_hana_adapter/2.png" width="80%" />

3. Download missing plugins: https://mvnrepository.com/artifact/javax.xml.bind/jaxb-api/2.3.0 https://mvnrepository.com/artifact/com.sun.xml.bind/jaxb-impl/2.3.3
and put into the plugins folder

<img src="/custom_hana_adapter/3.png" width="80%" />

4. Unpack dpagent.tar.gz

<img src="/custom_hana_adapter/4.png" width="80%" />

5. Run Hana Studio and go to the Help -> Install new Software. Then click on Add, Local and choose patch to UI folder from extracted DPAGENT.TGZ

<img src="/custom_hana_adapter/5.png" width="80%" />

6. Install the plugin.
7. Create a hello world adapter. Change perspective to Plug-in development. Click on File->New->Plugin Project.

<img src="/custom_hana_adapter/6.png" width="80%" />

8. Check to Generate an activator flag.

<img src="/custom_hana_adapter/7.png" width="80%" />

9. Right-click on the project, Debug As ->Debug Configurations

<img src="/custom_hana_adapter/8.png" width="80%" />

10. Unselect Target Platform and click on Add Required Bundles

<img src="/custom_hana_adapter/9.png" width="80%" />

11. Select org.eclipse.equinox.console and com.sap.hana.dpagent. Next click on Add Required Bundles

<img src="/custom_hana_adapter/10.png" width="80%" />
<img src="/custom_hana_adapter/11.png" width="80%" />

12. Click on Apply, then Debug. When this is finished, everything should work perfectly. Now we can use dplogin to deploy plugin into your Hana system. If you are using HANA Express, dpagent can be activated on HXE instance from SYSTEM connection by:
{{< highlight sql >}}
ALTER DATABASE HXE ADD 'dpserver' 
{{< / highlight >}}
<img src="/custom_hana_adapter/12.png" width="80%" />


13. And finally, you should be able to use it in Hana 🙂
<img src="/custom_hana_adapter/14.png" width="80%" />
<img src="/custom_hana_adapter/13.png" width="80%" />

Good article on SAP Blog regarding this topic: https://blogs.sap.com/2015/08/26/hana-adapter-sdk-the-adapter-code/

