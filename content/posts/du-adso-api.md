---
title: "Direct Update ADSO ABAP API"
date: 2021-10-17T19:35:53+02:00
draft: false
---

{{< highlight abap >}}

REPORT zalvgrid.
 
DATA:
      l_tab_sflight TYPE STANDARD TABLE OF sflight.     "Tworzymy tabelę wewnętrzną
 
SELECT * FROM sflight INTO TABLE l_tab_sflight.         "Pobieramy dane z tabeli zewnętrzej do wewnętrznej
 
CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'                  "Wywołujemy funkcję odpowiedzialną za użycie tabeli
  EXPORTING
    i_structure_name = 'SFLIGHT'                        "Nazwa struktury tabeli
    i_grid_title     = 'Moja pierwsza tabela'           "Tytuł tabeli
  TABLES
    t_outtab         = l_tab_sflight                    "Zmieniana tabela
  EXCEPTIONS                                            "Wyjątki
    program_error    = 1
    OTHERS           = 2.
{{< /highlight >}}