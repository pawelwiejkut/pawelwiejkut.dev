---
title: "AMDP ABAP Transformation execution"
date: 2021-10-17T21:44:24+02:00
tags: ["AMDP","BW","ABAP"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

You may wonder how to execute AMDP TRFN direclty via ABAP. It seems that the best idea is to use the method bellow:

{{< highlight abap >}}
cl_rstran_db_stat=>execute_haap(
    EXPORTING
        i_processing_phase      = lr_request->if_rsbk_request~get_stage( )-stage_id
        i_target_request        = lr_request->if_rsbk_request~get_requid( )
        i_dtp                   = lr_dtp->n_dtp
        i_t_trfn                = lr_request->if_rsbk_request~get_t_transformation( i_only_she_relevant = rs_c_true )
        i_r_log                 = lr_request->if_rsbk_request~get_log( )
        i_simulation            = lr_request->get_simulation( )
        i_th_bp                 = lt_bp
        i_r_outbound            = lr_outbound
    IMPORTING
        e_r_analysis_rt         = DATA(lr_analysis) ).

DATA(lr_segment_outbound) = lr_outbound->get_segment( i_segid = 001 ).

{{< /highlight >}}

What is funny - in oposite to standard ABAP execution, you need to put the "empty" outbound into execution and then you can pick up data from there. For complete usecase please [check out this repostiory](https://github.com/pawelwiejkut/bw_trfn_tester/blob/old/src/zcl_bw_trfn_tester_amdp.clas.abap).

