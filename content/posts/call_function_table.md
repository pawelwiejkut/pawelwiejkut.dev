---
title: "Call SAP HANA function with table"
date: 2021-11-11T11:44:24+02:00
tags: ["SQL","HANA"]
lastmod: 2021-12-11T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

How to run HANA SQL function where output table is required ?
Example function ([from this tutorial](https://developers.sap.com/tutorials/hana-graph-overview-graphscript.html)):
{{< highlight sql >}}
CREATE TYPE "TT_RESTAURANTS" AS TABLE ("node_id" INTEGER, "distance" INTEGER, "hops" BIGINT);


CREATE OR REPLACE PROCEDURE "NEAREST_RESTAURANT"(IN startV INT, OUT res "TT_RESTAURANTS")
LANGUAGE GRAPH READS SQL DATA AS
BEGIN
	GRAPH g = Graph("SKIING");
	VERTEX v_s = Vertex(:g, :startV);
	MULTISET<Vertex> rests = v IN Vertices(:g) WHERE :v."restaurant" == N'TRUE';
	ALTER g ADD TEMPORARY VERTEX ATTRIBUTE (INT "distance" = 0);
	ALTER g ADD TEMPORARY VERTEX ATTRIBUTE (BIGINT "hops" = 0L);
	FOREACH rest in :rests {
		VERTEX v_rest = Vertex(:g, :rest."node_id");
		WeightedPath<INT> p = Shortest_Path(:g, :v_s, :v_rest, (Edge conn) => INTEGER { return :conn."length"; } );
		rest."hops" = Length(:p);
		rest."distance" = Weight(:p);
	}
	res = SELECT :v."node_id", :v."distance", :v."hops" FOREACH v IN :rests;
END;
{{< /highlight >}}

How to run it easily in SQL environment ?

{{< highlight sql >}}
DO 
BEGIN
DECLARE lt_tab "TT_RESTAURANTS";
CALL "SKIING"."NEAREST_RESTAURANT"(15,lt_tab);
SELECT * FROM :lt_tab;
END;
{{< /highlight >}}



