---
title: "SQL ON conditions in left join"
date: 2019-04-14T22:01:24+02:00
tags: ["NPL","ABAPTrial","SYBASE","License"]
lastmod: 2021-12-11T00:00:00+02:00
aliases : [ sql_on_join_conditions ]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Even if you use SQL for your daily work, it is possible that you might don’t know about two ways to set a condition: using "where" and .. put the condition into the join. The main issue is that they can return different results. Let me explain more.

1.Let’s assume that you have 2 tables. Content of first one
<img src="/sql_on_join_conditions/1.png" width="80%" />

2.Content of the second one
<img src="/sql_on_join_conditions/2.png" width="80%" />

3. Now let’s get only this employees with salary bigger than 4 000
{{< highlight sql >}}
select * from employees emp left join salaries sal on emp.id = sal.employee
where sal.salary > 4000
{{< /highlight >}}

4. Result shouldn’t impress anyone
<img src="/sql_on_join_conditions/3.png" width="80%" />

5. But now let’s change our query and move the condition to ON. Results will look different than before
<img src="/sql_on_join_conditions/4.png" width="80%" />


6. Of course, this behavior is correct and refers to the algebra of the relationship used in SQL. I have to paste here my favorite image
<img src="/sql_on_join_conditions/5.jpg" width="80%" />
Image source: https://external-preview.redd.it/M5QHWsp2vgZ-3QDZ4m-qS58lsOUgDNHau8trSFzS8H0.jpg?auto=webp&s=cae9cdc438b71c9025d40dad4650801fdcae1ef8

7. So as you see our statement without any restriction should return
<img src="/sql_on_join_conditions/6.png" width="80%" />


and because we just have only one entry which passes our criteria we just get empty rows in other cases. This also explains why our condition move doesn’t change anything in case of an inner join
<img src="/sql_on_join_conditions/7.png" width="80%" />
<img src="/sql_on_join_conditions/8.png" width="80%" />


If you created a infoset object on SAP BW System, you can see that there is an option called Left Outer: Add Filter Value to On-Condition.
<img src="/sql_on_join_conditions/9.png" width="80%" />


When you don’t check this option, evaluated SQL for ASE DB in my case will look like below
{{< highlight sql >}}
select
"T1"."TCTSYSID"  as "F1"
, "T1"."TCTJOBNAME"  as "F2"
from
"/BI0/ATCTHP24O00" "T1"
join
"/BI0/ATCT_O4100" "T2"
on
"T1" . "TCTSYSID"
= "T2" . "TCTSYSID"
join
"/BI0/ATCTHP24O00" "T3"
on
"T1" . "TCTSYSID"
= "T3" . "TCTSYSID"
where
( ( ( ( ( (
"T1"."TCTSYSID"
= 'NPLCLNT100'
) ) ) ) AND  ( ( ( (
"T1"."CALDAY"
= '20190414'
) ) ) ) ) )
group by
"T1"."TCTSYSID"
,"T1"."TCTJOBNAME"
order by
"F1" ASC
, "F2" ASC
plan '
(use optgoal sap_olap)
(use fact_table T3)
(use parallel 4)
(prop T3 (parallel 4))
'
/* BW-SYS-DB-SYB:I */
{{< /highlight >}}

And when we check flag:
{{< highlight sql >}}
select
"T1"."TCTSYSID"  as "F1"
, "T1"."TCTJOBNAME"  as "F2"
from
"/BI0/ATCTHP24O00" "T1"
join
"/BI0/ATCT_O4100" "T2"
on
"T1" . "TCTSYSID"
= "T2" . "TCTSYSID"
join
"/BI0/ATCTHP24O00" "T3"
on
"T1" . "TCTSYSID"
= "T3" . "TCTSYSID"
where
( ( ( ( ( (
"T1"."TCTSYSID"
= 'NPLCLNT100'
) ) ) ) AND  ( ( ( (
"T1"."CALDAY"
= '20190414'
) ) ) ) ) )
group by
"T1"."TCTSYSID"
,"T1"."TCTJOBNAME"
order by
"F1" ASC
, "F2" ASC
plan '
(use optgoal sap_olap)
(use fact_table T3)
(use parallel 4)
(prop T3 (parallel 4))
'
{{< /highlight >}}
That's all in this post, have a nice day and see you soon 🙂