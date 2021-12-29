---
title: "SAC APP Design & clean the filter button"
date: 2021-12-13T12:15:41+01:00
tags: ["SAC","Dropdown","JavaScript","SACApp","SACAppFilter"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

<h3>Button</h3>


1. To clean the filter we need a button. Let's get one from the plus in the toolbar

{{<figure align=center src="/sac_app_design/1.png"  width="30%" >}}

2. Put the button near the Year dropdown and rename it

{{<figure align=center src="/sac_app_design/2.png"  width="80%" >}}

3. Go to the Button_Clean_Filters - onClick

{{<figure align=center src="/sac_app_design/3.png"  width="40%" >}}

4. Put the following code

{{< highlight js >}}
// Remove all filters from the model
Table_Games_Sales.getDataSource().removeDimensionFilter("Name");
Table_Games_Sales.getDataSource().removeDimensionFilter("Publisher");
Table_Games_Sales.getDataSource().removeDimensionFilter("Year");

//Set all dropdowns selection to empty
Dropdown_Name.setSelectedKey('');
Dropdown_Publisher.setSelectedKey('');
Dropdown_Year.setSelectedKey('');
{{< / highlight >}}

{{<figure align=center src="/sac_app_design/4.png"  width="80%" >}}

5. Button should now work properly

{{<figure align=center src="/sac_app_design/5.gif"  width="80%" >}}

<h3>Design</h3>

1. Please download image dataset from [here](/sac_app_design/graphic.zip)

2. Insert images using the plus in the toolbar

{{<figure align=center src="/sac_app_design/6.png"  width="40%" >}}

3. Put images together, and move existing elements to align together

{{<figure align=center src="/sac_app_design/7.gif"  width="80%" >}}
{{<figure align=center src="/sac_app_design/8.gif"  width="80%" >}}

After that it should look like on the image bellow

{{<figure align=center src="/sac_app_design/9.png"  width="80%" >}}

4. Add a new chart in the right corner

{{<figure align=center src="/sac_app_design/10.png"  width="80%" >}}

5.  Change the type to numeric point

{{<figure align=center src="/sac_app_design/11.png"  width="80%" >}}

6. Choose the measure

{{<figure align=center src="/sac_app_design/12.png"  width="80%" >}}

7. Rename the measure

{{<figure align=center src="/sac_app_design/13.gif"  width="40%" >}}

8. Hide chart title

{{<figure align=center src="/sac_app_design/14.png"  width="60%" >}}

9. Add two missing images: Mario and coin

{{<figure align=center src="/sac_app_design/15.png"  width="60%" >}}

10. Create a linked analysis between table and chart

{{<figure align=center src="/sac_app_design/16.png"  width="60%" >}}

11. Click on Only Selected Widget and click Select widget button

{{<figure align=center src="/sac_app_design/17.png"  width="60%" >}}

12. Select Chart_1

{{<figure align=center src="/sac_app_design/18.png"  width="60%" >}}

13. Add account to the dimensions  on the table

{{<figure align=center src="/sac_app_design/19.png"  width="60%" >}}

14. Click on Manage Filter

{{<figure align=center src="/sac_app_design/20.png"  width="80%" >}}

15. Select Global Sales

{{<figure align=center src="/sac_app_design/21.png"  width="80%" >}}

16. At the end everything should works and looks fine 😏

{{<figure align=center src="/sac_app_design/22.gif"  width="80%" >}}


















