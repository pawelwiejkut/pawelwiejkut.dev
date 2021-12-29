---
title: "Create and fill a dropdown in SAC APP"
date: 2021-12-12T14:13:53+01:00
tags: ["SAC","Dropdown","JavaScript","SACApp"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

1. Firstly we have to move our table a few lines down. This can be done by moving the mouse between the table and toolbar and drag and dropping when the cursor changes the icon:
{{<figure align=center src="/sac_app_dropdown/1.png"  width="80%" >}}

2. Click on the plus icon on the toolbar
{{<figure align=center src="/sac_app_dropdown/2.png"  width="80%" >}}

3. Select Dropdown form the list 
{{<figure align=center src="/sac_app_dropdown/3.png"  width="80%" >}}

4. Lets rename the Table by click on tree dots -> Rename, and set new name to Table_Games_Sales
{{<figure align=center src="/sac_app_dropdown/5.png"  width="80%" >}}

5. Same with Dropdown, and put new name Dropdown_Name

{{<figure align=center src="/sac_app_dropdown/6.png"  width="80%" >}}

5. Find the fx icon near to the Canvas in the left panel and click on onInitialization
{{<figure align=center src="/sac_app_dropdown/4.png"  width="80%" >}}


6. This will move us to the code editor where the party begins 💃 🕺 but no worries, JavaScript in the SAC is very developer-friendly and restricted. It is very easy to learn - and you can hear this from me, an ABAP fanboy. If you want to learn more about JS in SAC, please check out the handbook [here](https://community.sap.com/topics/cloud-analytics/analytic-applications-api) (search for Developer Handbook)

7. Firstly we have to create a variable which will hold the content from our table

{{< highlight js >}}
var resultSet = Table_Games_Sales.getDataSource().getResultSet();
{{< /highlight >}}

8. Then we have to loop by the resultSet and assign all Names into our dropdown

{{< highlight js >}}
for ( var i = 0; i< resultSet.length; i++ ){		
	Dropdown_Name.addItem(resultSet[i]["Name"].id,resultSet[i]["Name"].description);		
}{{< /highlight >}}

<mark>If you want to fill the dropdown by data not included into your table (Table_Games_Sales) you should use getMembers()</mark>
{{< highlight js >}}
var resultSet = Table_Games_Sales.getDataSource().getMembers("Name");

for ( var i = 0; i< resultSet.length; i++ ){		
 Dropdown_Name.addItem(resultSet[i].id,resultSet[i].description);		
}{{< /highlight >}}

Nevertheless in this example will will stay with getResultSet(), because Name is available in our table and according to the [handbook](https://d.dam.sap.com/a/3Y16uka/SAPAnalyticsCloud_AnalyticsDesigner_DeveloperHandbook.pdf) this is better solution because of the performance
{{<figure align=center src="/sac_app_dropdown/11.png"  width="80%" >}}

9. Ate the end our code should look like this 
{{<figure align=center src="/sac_app_dropdown/7.png"  width="80%" >}}

10. Now it is a time to save and run our app
{{<figure align=center src="/sac_app_dropdown/8.png"  width="80%" >}}

11. As you can see dropdown looks good, but it ends at "A" - this is because of the limitation. Our file contain much more games.
{{<figure align=center src="/sac_app_dropdown/9.png"  width="80%" >}}

Easies way to fix this is to create a additional filter on Publisher and make them cascading, but this will be described in the next post. </br>

12. Dropdown is filled, bu it is not working - not filtering any values in the table. To enable this, lest go back to the editor, and click on fx near to Dropdown_Name

{{<figure align=center src="/sac_app_dropdown/10.png"  width="80%" >}}

13. There is only one event - onSelect. In the code we need to get the selection from dropdown and set up a filter. Lets assign key to the new variable, and then use setDimentionFilter to put a filter.

{{< highlight js >}}
var selectedName = Dropdown_Name.getSelectedKey();
Table_Games_Sales.getDataSource().setDimensionFilter("Name",selectedName);
{{< /highlight >}}

{{<figure align=center src="/sac_app_dropdown/12.png"  width="80%" >}}

14. Please check your app. Dropdown Filter should work fine now. I have a bit different layout but no worries. I will explain how to do it step by step in my nex post.

{{<figure align=center src="/sac_app_dropdown/13.gif"  width="80%" >}}








