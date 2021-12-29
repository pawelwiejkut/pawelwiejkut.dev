---
title: "Select dimensions by CheckBox and Button"
date: 2021-12-13T15:12:24+01:00
tags: ["SAC","JavaScript","SACApp","SACButton"]
aliases : [ sac_button_checkbox ]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
1. We need a CheckBox, it can be added from the toolbar

{{<figure align=center src="/sac_button_checkbox/1.png"  width="40%" >}}

2. Let's change the background color of the CheckboxGroup. To do this, please click on the brush icon, bucket icon and then on more

{{<figure align=center src="/sac_button_checkbox/2.png"  width="80%" >}}

3. Change color to hex 1f303f

{{<figure align=center src="/sac_button_checkbox/3.png"  width="40%" >}}

4. Next change the font color 

{{<figure align=center src="/sac_button_checkbox/4.png"  width="40%" >}}

5. Set new color to white, hex ffffff

{{<figure align=center src="/sac_button_checkbox/5.png"  width="30%" >}}

6. Remove the values from the Checkbox

{{<figure align=center src="/sac_button_checkbox/7.gif"  width="50%" >}}

7. Rename checkbox to CheckboxGroup_Dimensions, bu click on the keys icon

{{<figure align=center src="/sac_button_checkbox/6.png"  width="30%" >}}

8. Add additional code to the Application - onInitialization

{{< highlight js >}}
// Get all dimensions
var dimensions = Table_Games_Sales.getDataSource().getDimensions();

//Loop by dimensions and fill Checkbox
for ( var y = 0; y < dimensions.length; y++ ){
    CheckboxGroup_Dimensions.addItem(dimensions[y].id,dimensions[y].description);
}
{{< /highlight >}}

{{<figure align=center src="/sac_button_checkbox/8.png"  width="90%" >}}

9. Last but not least - we need a button

{{<figure align=center src="/sac_button_checkbox/9.png"  width="40%" >}}

10. Rename the button

{{<figure align=center src="/sac_button_checkbox/13.png"  width="40%" >}}

10. Let's also add a code to handle it 

{{<figure align=center src="/sac_button_checkbox/10.png"  width="80%" >}}

{{< highlight js >}}
// Get current list of dimensions to remove it
var currentDimensionsSet= Table_Games_Sales.getDimensionsOnRows();
// Get selected fields from CheckBox
var selectedDimensions = CheckboxGroup_Dimensions.getSelectedKeys();

// Delete all existing dimensions
for (var r = 0; r < currentDimensionsSet.length; r++){
	Table_Games_Sales.removeDimension(currentDimensionsSet[r]);
}
// Add all new dimensions
for (var i = 0; i < selectedDimensions.length; i++){
	Table_Games_Sales.addDimensionToRows(selectedDimensions[i]);
}
{{< /highlight >}}

{{<figure align=center src="/sac_button_checkbox/11.png"  width="80%" >}}

11. At the end-user should be able to pick up interesting dimensions by themself

{{<figure align=center src="/sac_button_checkbox/12.gif"  width="90%" >}}
