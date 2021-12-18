---
title: "Cascade filtering in SAC"
date: 2021-12-12T15:42:26+01:00
tags: ["SAC","Dropdown","JavaScript","SACApp"]
description: 'In this part of the tutorial, we are focusing on creating a filter on the dropdown in SAC APP.'
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

In this part of the tutorial, we are focusing on creating a filter on the dropdown in SAC APP.

1. First of all lets put a two new dropdowns and three texts

{{<figure align=center src="/sac_app_dropdown_cascade/1.png"  width="80%" >}}

2. Resize a table, add more space at the top and align texts

{{<figure align=center src="/sac_app_dropdown_cascade/2.png"  width="80%" >}}

3. Rename all elements accordingly

{{<figure align=center src="/sac_app_dropdown_cascade/3.png"  width="30%" >}}

4. Please be informed that If your screen is to small to work with SAC, you can resize the page in Chrome settings:

{{<figure align=center src="/sac_app_dropdown_cascade/4.png"  width="50%" >}}


5. Put code to fill dropdowns into Canvas - onInitialization
{{< highlight js >}}
//Get all values from the table
var resultSet = Table_Games_Sales.getDataSource().getResultSet();
// Get all available years (as it is not included into table)
var yearSet = Table_Games_Sales.getDataSource().getMembers("Year");

//Loop at result set and fill Name and Publisher as they both are available in the table
for ( var i = 0; i< resultSet.length; i++ ){		
	Dropdown_Name.addItem(resultSet[i]["Name"].id,resultSet[i]["Name"].description);	
	Dropdown_Publisher.addItem(resultSet[i]["Publisher"].id,resultSet[i]["Publisher"].description);	
}
//Loop at year separately, and fill dropdown
for ( var z = 0; z< yearSet.length; z++ ){	
	Dropdown_Year.addItem(yearSet[z].id,yearSet[z].description);
}
{{< /highlight >}}

{{<figure align=center src="/sac_app_dropdown_cascade/5.png"  width="80%" >}}

6. Put code into the Dropdown_Publisher - onSelect

{{< highlight js >}}
//Remove existing Name filter form the table
Table_Games_Sales.getDataSource().removeDimensionFilter("Name");
//Remove existing Publisher filter form the table
Table_Games_Sales.getDataSource().removeDimensionFilter("Publisher");
//Get all values from the table
var resultSet = Table_Games_Sales.getDataSource().getResultSet();
// Get Publisher selected by user
var selectedPublisher = Dropdown_Publisher.getSelectedKey();
//Remove all items in the Name dropdown
Dropdown_Name.removeAllItems();

// Fill only Names relevant to chosen Publisher
for ( var i = 0; i< resultSet.length; i++ ){	
	if ( resultSet[i]["Publisher"].id === selectedPublisher ){
	Dropdown_Name.addItem(resultSet[i]["Name"].id,resultSet[i]["Name"].description);
	}
}
//Put the publisher dropdown value as a filter into table
Table_Games_Sales.getDataSource().setDimensionFilter("Publisher",selectedPublisher);
{{< /highlight >}}

{{<figure align=center src="/sac_app_dropdown_cascade/6.png"  width="80%" >}}

Now Publisher and Name should work pretty well 

{{<figure align=center src="/sac_app_dropdown_cascade/7.gif"  width="80%" >}}

7. Add missing code to the Year - onSelect. Here we just reading a value from the dropdown and put as a table filter. 

{{< highlight js >}}

var selectedYear = Dropdown_Year.getSelectedKey();
Table_Games_Sales.getDataSource().setDimensionFilter("Year",selectedYear);

{{< /highlight >}}

At the end all filters should works fine.






