---
title: "Create a popup to change dimensions order"
date: 2021-12-15T22:01:41+01:00
tags: ["SAC","JavaScript","SACApp","SACPopup"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

1. Let's start by creating the popup

{{<figure align=center src="/sac_popup_order/1.png"  width="80%" >}}

2. Rename new window

{{<figure align=center src="/sac_popup_order/2.png"  width="80%" >}}

3. Definitely we should arrange this new space. Start with a new List Box

{{<figure align=center src="/sac_popup_order/3.png"  width="80%" >}}

4. Add tree new buttons: UP, DOWN, Save and Close

{{<figure align=center src="/sac_popup_order/4.png"  width="80%" >}}

5. Change style on List Box to add borders

{{<figure align=center src="/sac_popup_order/5.png"  width="80%" >}}

6. Rename new elements

{{<figure align=center src="/sac_popup_order/6.png"  width="60%" >}}

7. Create a new button on the Canvas

{{<figure align=center src="/sac_popup_order/7.png"  width="80%" >}}

8. Create a script variable

{{<figure align=center src="/sac_popup_order/9.png"  width="80%" >}}

9. Change name and set as array

{{<figure align=center src="/sac_popup_order/10.png"  width="80%" >}}


10. Create onClick event for the new - Change Layout button


{{<figure align=center src="/sac_popup_order/8.png"  width="80%" >}}

{{< highlight js >}}

// Get current dimensions
var currentDimensions = Table_Games_Sales.getDimensionsOnRows();
// Assign values to the global variable
ScriptVariable_Dimensions_Values = Table_Games_Sales.getDimensionsOnRows();

// Clear the current list
ListBox_Dimensions_Order.removeAllItems();
// Add current dimensions to the list
for ( var i = 0; i < currentDimensions.length; i++ ){
	ListBox_Dimensions_Order.addItem(currentDimensions[i]);
}
// Open popup
Popup_Dimensions_Order.open();
{{< / highlight >}}

{{<figure align=center src="/sac_popup_order/11.png"  width="90%" >}}

11. Add code for Button_Save_And_close - onClick
{{< highlight js >}}
// Get all current dimensions
var allDimensions = Table_Games_Sales.getDimensionsOnRows();
// Delete all dimensions
for (var i = 0; i < allDimensions.length; i++){
	Table_Games_Sales.removeDimension(allDimensions[i]);
}
// Set new dimensions
for (var r = 0; r < ScriptVariable_Dimensions_Values.length; r++){
	Table_Games_Sales.addDimensionToRows(ScriptVariable_Dimensions_Values[r]);
}
// Close popup
Popup_Dimensions_Order.close();
{{< / highlight >}}

{{<figure align=center src="/sac_popup_order/12.png"  width="90%" >}}

12. Add code for Button_Down - onClick
{{< highlight js >}}
// Get all selected Keys
var selectedValue = ListBox_Dimensions_Order.getSelectedKey();
// Change the order on the list and update List Box
if (selectedValue){
	var valueIndex  = ScriptVariable_Dimensions_Values.indexOf(selectedValue);
	ScriptVariable_Dimensions_Values.splice(valueIndex,1);
	ScriptVariable_Dimensions_Values.splice(  valueIndex + 1,0, selectedValue );
	ListBox_Dimensions_Order.removeAllItems();

	for ( var i = 0; i < ScriptVariable_Dimensions_Values.length; i++){
		ListBox_Dimensions_Order.addItem(ScriptVariable_Dimensions_Values[i]);
	}
}
{{< / highlight >}}

{{<figure align=center src="/sac_popup_order/13.png"  width="90%" >}}

13. Add code for Button_Up - onClick
{{< highlight js >}}
// Get all selected Keys
var selectedValue = ListBox_Dimensions_Order.getSelectedKey();
// Change the order on the list and update List Box
if (selectedValue){
	var valueIndex  = ScriptVariable_Dimensions_Values.indexOf(selectedValue);
	ScriptVariable_Dimensions_Values.splice(valueIndex,1);
	ScriptVariable_Dimensions_Values.splice(  valueIndex - 1,0, selectedValue );
	ListBox_Dimensions_Order.removeAllItems();

	for ( var i = 0; i < ScriptVariable_Dimensions_Values.length; i++){
		ListBox_Dimensions_Order.addItem(ScriptVariable_Dimensions_Values[i]);
	}
}
{{< / highlight >}}

{{<figure align=center src="/sac_popup_order/14.png"  width="90%" >}}

14. At the end we have a complete and working solution. Congratulations 🍾 !

{{<figure align=center src="/sac_popup_order/15.gif"  width="90%" >}}

{{<figure align=center src="/sac_popup_order/16.gif"  width="90%" >}}
