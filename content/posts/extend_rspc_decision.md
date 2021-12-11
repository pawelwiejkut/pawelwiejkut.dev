---
title: "How to extend decision​ tree in process chain?"
date: 2019-05-15T20:44:24+02:00
tags: ["BW","RSPC","Decision"]
lastmod: 2021-12-11T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Toady short tutorial about extending the decision tree in the process chain. As you probably know decision three blocks can be extended. In our example, we want to run delta info package in everyday processing, and depending on our customizing perform a full load.
Process chain example:
<img src="/extend_rspc_decision/1.jpg" width="80%" />
Customization table:
<img src="/extend_rspc_decision/2.png" width="80%" />

Basically, if the value of param ISIP in our customer table is set to DELTA, we want to execute the delta info package. If param will be set to the FULL, execute ISIP in full mode.

Main object used to achieve our goal is **BAPI: RSAR_CONNECTOR**, where we need to create the function, which can be later used in formula:
<img src="/extend_rspc_decision/3.png" width="80%" />

Lets go to se18, and create new implementation
<img src="/extend_rspc_decision/4.png" width="80%" />

The best idea now is to **DO NOT ACTIVATE** this implementation before fully fill implementing the class. Let’s just double click on the class name
<img src="/extend_rspc_decision/5.png" width="80%" />

<mark>If you activate implementation with wrong function definition, then you have to clear entries in table: SFBMETHSIG before enable implementation once again. In other way function structure will be not updated.</mark>

Basic class should look like below:

{{< highlight abap >}}
class ZCL_IM_ISIP_CUST definition
  public
  final
  create public .
 
public section.
 
  interfaces IF_EX_RSAR_CONNECTOR .
 
  class-methods CHECK_CUST
    importing
      !IV_CUST_ID type STRING
    returning
      value(RV_RUN_MODE) type STRING .
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.
 
 
 
CLASS ZCL_IM_ISIP_CUST IMPLEMENTATION.
 
 
  METHOD check_cust.
 
    SELECT SINGLE param FROM zexcust
    WHERE id = @iv_cust_id
    INTO @rv_run_mode.
 
  ENDMETHOD.
 
 
  METHOD if_ex_rsar_connector~get.
 
    DATA: ls_cust_function TYPE sfbeoprnd.
 
    CASE i_key.
      WHEN 'CUSTOM'.
        CLEAR ls_cust_function.
        ls_cust_function-tech_name = 'C_CHECK_CUST'.
        ls_cust_function-descriptn = 'Check cust table to define correct ISIP'.
        ls_cust_function-class = 'ZCL_IM_ISIP_CUST'.
        ls_cust_function-method = 'CHECK_CUST'.
        APPEND ls_cust_function TO c_operands.
    ENDCASE.
 
  ENDMETHOD.
ENDCLASS.
{{< /highlight >}}

After using our new function C_CHECK_CUST in the process chain, we get desired result
<img src="/extend_rspc_decision/6.jpg" width="80%" />
