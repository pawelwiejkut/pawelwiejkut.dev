---
title: "Create ADSO from ABAP"
date: 2022-01-06T12:52:44+01:00
tags: ["ABAP","BW","ADSO"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Creating ADSO from ABAP can be easily achieved by **cl_rso_adso_api=>create**
{{< highlight abap >}}

DATA(ls_flags) = VALUE cl_rso_adso_api=>tn_s_adsoflags( direct_update = abap_true  ).

TRY.
          cl_rso_adso_api=>create(
            EXPORTING
              i_adsonm                      = "Name of the ADSO
              i_infoarea                    = "Infoarea name
              i_s_adsoflags                 = ls_flags
              i_t_object                    = "Table with all fields
              i_t_dimension                 = "Dimension
              i_t_key                       = "String table with key
          IMPORTING
            e_t_msg                       =  DATA(lt_msg)
          ).

        CATCH cx_rs_all_msg INTO DATA(lr_msg).

          cl_demo_output=>display(
            EXPORTING
              data = lr_msg->get_longtext( )
              name = 'Error'  ).
      ENDTRY.
{{< /highlight >}}

Full usage examples can be found [here](https://github.com/pawelwiejkut/bw_adso_bof/blob/main/src/zbw_adso_bof.prog.abap)