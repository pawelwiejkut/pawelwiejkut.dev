---
title: "Cascade filtering in SAC"
date: 2021-12-12T15:42:26+01:00
tags: ["SAC","Dropdown","JavaScript","SACApp"]
Focus_Keyword: "Cascade filtering"
aliases : [ sac_app_dropdown_cascade]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
In this part of the tutorial, we are focusing on creating a cascade filter on the dropdown in SAC APP. 
Cascade means that filters on the dashboard will depend on each other. In the example, if you pick up the publisher name Nintendo then in the games list (Name) you should see only games that belong to Nintendo and no more others. To achieve this, we have to redesign our app a bit.

If you want to have a big picture, please check the rest of the tutorials.</br>
Pervious topic - [Create and fill a dropdown in SAC APP](/posts/sac-app-dropdown/)</br>
Next part - [SAC APP Design & clean the filter button](/posts/sac-app-design/)</br>
The complete list is available [here](/sac/).


1. Let's put two new dropdowns and three new texts. They will handle filters for Name (games list) and Year (when game was published).To add new elements please use bottom SAC panel.

{{<figure align=center src="/sac_app_dropdown_cascade/1.png"  width="80%" >}}

2. We have to resize the existing table, and add more space at the top and align texts. It is necessary to fits all elements on the dashboard. Check the image below for layout recommendations. To change the positions of the particular elements, simply click on it and drag and drop to the desired place. 

{{<figure align=center src="/sac_app_dropdown_cascade/2.png"  width="80%" >}}

3. Rename all elements accordingly. In the example, we are using a naming convention like Objecttype_Objectname. Keeping the one schema names is important, it allows us to easily find and access them.

{{<figure align=center src="/sac_app_dropdown_cascade/3.png"  width="30%" >}}

4. Please be informed that If your screen is too small to work with SAC, you can resize the page in Chrome settings. I recommend changing this setting, especially if you have a small screen with high resolution. To achieve this please click on the three dots icon in the right upper corner of Chrome, and change the zoom.

{{<figure align=center src="/sac_app_dropdown_cascade/4.png"  width="50%" >}}


5. Put code to fill dropdowns into Canvas - onInitialization. This piece of javascript will be responsible for filling our new dropdowns when the app starts. Our cascading filters are not working at this time, and we want to load all values. All magic starts when user choose one particular Publisher or Name.

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

6. Put code into the Dropdown_Publisher - onSelect. Here we need to first clean all the combined filters name and publisher on our table Table_Games_Sales. The next step is to fill Name only with corresponding values (like for Sega we want to display only belong games - names).

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

Run our application. Now Publisher and Name should work pretty well. We can see that the list is filled only by corresponding values.

{{<figure align=center src="/sac_app_dropdown_cascade/7.gif"  width="80%" >}}

7. Add missing code to the Year - onSelect. Here we just read a value from the dropdown and put it as a table filter. The year is not considered to be a cascading filter in our example, never the less we need it to be available.

{{< highlight js >}}

var selectedYear = Dropdown_Year.getSelectedKey();
Table_Games_Sales.getDataSource().setDimensionFilter("Year",selectedYear);

{{< /highlight >}}

8. Run the app once again. As you see, all filters are working fine now. Cascade filtering between the name and publisher should also behave as expected.

If everything is working as expected, please check out next tutorial from SAC series
[SAC APP Design & clean the filter button](/sac_app_design/).

When the initial app is ready, it is time to add some images and clean the filter button. See you there :) 







