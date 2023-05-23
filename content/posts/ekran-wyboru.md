---
title: "Ekran Wyboru"
date: 2017-04-09T17:01:40+01:00
tags: ["ABAP","ABAP od podstaw"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Dzisiejsza instrukcja będzie nieco krótsza i dotyczyć będzie rozszerzenia naszego poprzedniego programu z tego wpisu o klika linijek kodu odpowiedzialnych za stworzenie ekranu. Nasz tworzony ekran będzie odpowiadał za umożliwienie nam wyboru wyników wyświetlanych w tabeli w zależności od numeru połączenia i numeru przewoźnika.

<mark>Jeżeli szukasz kompletnego kursu online abap od podstaw – zapraszam Cię do zapoznania się z ofertą: https://saponit.pl/kurs-abap/</mark>

1. Zaczynamy od skopiowania poprzedniego programu. Aby to zrobić, w transakcji se80 klikamy prawym przyciskiem myszy na nasz poprzedni program i klikamy na copy.

{{<figure align=center src="/ekran_wyboru/1.png"  width="70%" >}}


2. W Source Target podajemy ZFSCREEN, a następnie potwierdzamy, następnie zaznaczamy wszystkie check’i i wybieramy swoją paczkę oraz transport.

{{<figure align=center src="/ekran_wyboru/2.png"  width="50%" >}}
{{<figure align=center src="/ekran_wyboru/3.png"  width="50%" >}}


3. Następnie do kodu dopisujemy linijkę odpowiadającą za selection screen, oraz całość zapisujemy i aktywujemy. Kod powinien wyglądać tak jak poniżej:

{{< highlight abap >}}

DATA:
      l_tab_sflight TYPE STANDARD TABLE OF sflight.     "Tworzymy tabelę wewnętrzną
 
SELECTION-SCREEN BEGIN OF BLOCK b1.
 
PARAMETERS:
            p_conn TYPE sflight-connid,
            p_carr TYPE sflight-carrid.
 
SELECTION-SCREEN END OF BLOCK b1.
 
SELECT * FROM sflight INTO TABLE l_tab_sflight
  WHERE carrid EQ p_carr  AND connid EQ p_conn.         "Pobieramy dane z tabeli zewnętrzej do wewnętrznej
 
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

4. Uruchamiamy teraz program przy użyciu F8. Definitywnie widać,że coś poszło nie tak i nazwy nie są przypisane do parametrów więc wygląda to dość średnio. Cofamy się wiec z powrotem do poprzedniego ekranu przy użyciu klawisza F3.

{{<figure align=center src="/ekran_wyboru/4.png"  width="50%" >}}

5. Wchodzimy teraz w Goto-> Text Elements-> Slection Text 

{{<figure align=center src="/ekran_wyboru/5.png"  width="60%" >}}

6. Następnie przypisujemy tekst do parametrów tak jak na screenshoocie poniżej

{{<figure align=center src="/ekran_wyboru/6.png"  width="60%" >}}

7. Zapisujemy i aktywujemy program przy pomocy kombinacji klawiszy ctrl+s 
oraz ctrl+ f3. Następnie wracamy do poprzedniego ekranu poprzez naciśnięcie f3, i uruchamiamy program poprzez wybranie f8. Powinieneś zobaczyć ekran zbliżony do tego poniżej:

{{<figure align=center src="/ekran_wyboru/7.png"  width="50%" >}}

8. Spróbuj teraz wybrać parametry z pierwszego pola, kliknij w nie i naciśnij f4. Z okna wybierz interesujący numer połączenia (pamiętaj, że nasze ekrany mogą się różnić ze względu na to że dane do tej tabeli są losowo generowane przez system).

{{<figure align=center src="/ekran_wyboru/8.png"  width="60%" >}}

9. Uruchamiamy program poprzez f8. Teraz wyświetlone będą tylko te wyniki, które spełniają nasz warunek.

{{<figure align=center src="/ekran_wyboru/9.png"  width="50%" >}}



