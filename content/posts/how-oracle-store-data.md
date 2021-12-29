---
title: "How Oracle store your data"
date: 2018-08-10T20:44:24+02:00
tags: ["oralce","database","disk","storage"]
lastmod: 2021-12-11T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
All of you probably at least once in your life try to insert some records to a database table, but is anyone of you ever tried to understand how Oracle actually saves the entries in the database? Last time I was making a small experiment and I want to share my results with you.

Step one, let's build a small table and insert a few records:

{{< highlight sql >}}
INSERT INTO tab1 VALUES('AAA',111);
INSERT INTO tab1 VALUES('AAA',222);
INSERT INTO tab1 VALUES('AAA',333);
INSERT INTO tab1 VALUES('AAA',444);

INSERT INTO tab1 VALUES('BBB',111);
INSERT INTO tab1 VALUES('BBB',222);
INSERT INTO tab1 VALUES('BBB',333);
INSERT INTO tab1 VALUES('BBB',444);

INSERT INTO tab1 VALUES('CCC',111);
INSERT INTO tab1 VALUES('CCC',222);
INSERT INTO tab1 VALUES('CCC',333);
INSERT INTO tab1 VALUES('CCC',444);
{{< /highlight >}}

Let’s start some fun and check how my dump from Oracle DB looks like. First of all, I need to find the block where the table is stored:

{{< highlight sql >}}
SELECT segment_name,header_file, header_block+1 FROM dba_segments WHERE segment_name = 'TAB1';
{{< /highlight >}}

Create a dump from the selected block:
{{< highlight sql >}}
alter system dump datafile 1 block 102161;
{{< /highlight >}}

Now I have to run the console, ssh into the remote system and check last files in Oracle directory:
{{< highlight bash >}}
cd /u01/app/oracle/diag/rdbms/orcl12c/orcl12c/trace
 
find $1 -type f -exec stat --format '%Y :%y %n' "{}" \; | sort -nr | cut -d: -f2- | head

# cat orcl12c_ora_10640.trc
 {{< /highlight >}}

Section of my dump looks like below:
{{< highlight bash >}}
block_row_dump:
tab 0, row 0, @0x1f95
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  41 41 41
col  1: [ 3]  c2 02 0c
tab 0, row 1, @0x1f8a
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  41 41 41
col  1: [ 3]  c2 03 17
tab 0, row 2, @0x1f7f
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  41 41 41
col  1: [ 3]  c2 04 22
tab 0, row 3, @0x1f74
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  41 41 41
col  1: [ 3]  c2 05 2d
tab 0, row 4, @0x1f69
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  42 42 42
col  1: [ 3]  c2 02 0c
tab 0, row 5, @0x1f5e
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  42 42 42
col  1: [ 3]  c2 03 17
tab 0, row 6, @0x1f53
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  42 42 42
col  1: [ 3]  c2 04 22
tab 0, row 7, @0x1f48
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  42 42 42
col  1: [ 3]  c2 05 2d
tab 0, row 8, @0x1f3d
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  43 43 43
col  1: [ 3]  c2 02 0c
tab 0, row 9, @0x1f32
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  43 43 43
col  1: [ 3]  c2 03 17
tab 0, row 10, @0x1f27
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  43 43 43
col  1: [ 3]  c2 04 22
tab 0, row 11, @0x1f1c
tl: 11 fb: --H-FL-- lb: 0x1  cc: 2
col  0: [ 3]  43 43 43
col  1: [ 3]  c2 05 2d
end_of_block_dump
 {{< /highlight >}}

If we look closer at block_row_dump, you will see some repeatability.  Let’s check what is the meaning of lines with c2 at the start.

To achieve this, we can just execute SQL statement below:
{{< highlight sql >}}
var n number;
exec dbms_stats.convert_raw_value('c2020c',:n);
print
and a result of this statement is:
{{< /highlight >}}

The value of raw 'c2 03 17′ is 222. You can check all these values and everything will look like our inserts at the beginning. To be more precise we are actually on "row" level of database storage:

<img src="/db_oracle_char.png" width="80%" />

That’s all for today, this is a basic knowledge related to database data save in tables. This knowledge is key to understanding how indexing or compression works on the database.

