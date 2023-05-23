---
title: "Tworzymy ALV Grid"
date: 2017-03-19T17:01:40+01:00
tags: ["ABAP","ABAP od podstaw"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Witajcie w kolejnej części kursu programowania w ABAPie. Dzisiaj pokaże po krótce jak stworzyć ALV GRID, czyli przekładając na język polski – tabelę. Ustawimy też od razu formatowanie kodu przy użyciu pretty printer.

<mark>Jeżeli szukasz kompletnego kursu online abap od podstaw – zapraszam Cię do zapoznania się z ofertą: https://saponit.pl/kurs-abap/</mark>

1. Wchodzimy w transakcję se38 odpowiedzialną za zarządzanie programami.

{{<figure align=center src="/tworzymy_alv_grid/1.png"  width="70%" >}}

2. Wpisujemy nazwę programu ZALVGRID i klikamy na „Create”.

{{<figure align=center src="/tworzymy_alv_grid/2.png"  width="70%" >}}

3. Wpisujemy opis i wybieramy typ programu jako „Executable program”

{{<figure align=center src="/tworzymy_alv_grid/3.png"  width="70%" >}}

4. Wybieramy stworzoną przez nas wcześniej paczkę programu i zapisujemy.

{{<figure align=center src="/tworzymy_alv_grid/4.png"  width="50%" >}}

5. Klikamy na Pattern. Przycisk ten jest odpowiedzialny za wywoływanie funkcji, metod itp.

{{<figure align=center src="/tworzymy_alv_grid/5.png"  width="70%" >}}

6. Wpisujemy nazwę funkcji: „REUSE_ALV_GRID_DISPLAY”.

{{<figure align=center src="/tworzymy_alv_grid/6.png"  width="50%" >}}

7. Aby skonfigurować funkcję Pretty Printer czyli formatowanie kodu, klikany na „Utilities” a następnie na „Settings”.

{{<figure align=center src="/tworzymy_alv_grid/7.png"  width="70%" >}}

8. Następnie ustawiamy opcje w zakładce „Abap editor” „Pretty printer” tak jak na ekranie poniżej.

{{<figure align=center src="/tworzymy_alv_grid/8.png"  width="60%" >}}

9. Wracamy do naszego programu, zmieniłam nieco funkcję usuwając niepotrzebne argumenty które nie będą wykorzystywane. W momencie kiedy będziesz pisać ten program spróbuj użyć skrótu klawiszowego alt + spacja, który jest odpowiedzialny za uzupełnianie i podpowiadanie.

{{<figure align=center src="/tworzymy_alv_grid/9.png"  width="60%" >}}

10. Spróbuj teraz sformatować kod programu. Służy do tego  skrót klawiszowy shift + f1.

{{<figure align=center src="/tworzymy_alv_grid/10.png"  width="60%" >}}

11. GUI Zapewnia jeszcze jeden ważny feature, mianowicie możliwość sprawdzenia poprawności programu. Aby użyć tej funkcji należy kliknąć ikonę u góry bądź nacisnąć skrót klawiszowy ctrl+ F2.

{{<figure align=center src="/tworzymy_alv_grid/11.png"  width="60%" >}}

12. Końcowy program powinien wyglądać tak jak na ekranie poniżej. Następnie zapisujemy, aktywujemy i uruchamiamy program.

{{<figure align=center src="/tworzymy_alv_grid/12.png"  width="70%" >}}

{{< highlight abap >}}
*&---------------------------------------------------------------------*
*& Report ZALVGRID
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
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

13. Końcowy efekt powinien wyglądać tak jak na zrzucie ekranu poniżej

{{<figure align=center src="/tworzymy_alv_grid/13.png"  width="70%" >}}


Gratulacje, właśnie napisałeś program który korzysta z modułu funcyjnego. Wiesz już też jak działa poprawianie czytelności kodu, sprawdzanie błędów, aktywacja, czy jego uruchamianie. W kolejnych poradnikach zajmiemy się modyfikacją tego pomysłu oraz jego rozbudowywaniem.

