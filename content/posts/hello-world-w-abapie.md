---
title: "Hello World W ABAPie"
date: 2017-03-12T10:08:21+01:00
tags: ["ABAP","ABAPodPodstaw"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
Witajcie w kolejnym poradniku dotyczącym SAPa na blogu. Dzisiejszy wpis będzie dotyczyć uzupełnienia tabel przykładowymi danymi oraz napisania prostego programu w ABAPie, zapraszam do lektury 🙂

<mark>
Jeżeli szukasz kompletnego kursu online abap od podstaw – zapraszam Cię do zapoznania się z ofertą: https://saponit.pl/kurs-abap/
</mark></br></br>

1. Uruchamiamy naszą instalację. Pamiętaj o tym że po uruchomieniu maszyny wirtualnej, trzeba jeszcze zalogować się na odpowiedniego użytkownika i uruchomić odpowiednie procesy. Opis tego jak to zrobić możesz sprawdzić w jednym z poprzednich wpisów. Przechodzimy teraz do transakcji se38. Jest to transakcja odpowiedzialna za zarządzanie programami, nazywanymi też zamiennie w SAPie raportami.

{{<figure align=center src="/hello_world_w_abapie/1.png"  width="80%" >}}


2. Po przejściu do transakcji w polu „Program” wpisujemy SAPBC_DATA_GENERATOR . Jest to nazwa programu odpowiedzialnego za wypełnienie przykładowych tabel danymi na których można później swobodnie operować . Następnie uruchamiamy program poprzez kliknięcie ikonki Execute (skrót klawiszowy F8).

{{<figure align=center src="/hello_world_w_abapie/2.png"  width="80%" >}}


3. Wybieramy opcję „Standard data record”, a następnie klikamy znów execute.

{{<figure align=center src="/hello_world_w_abapie/3.png"  width="80%" >}}


4. Potwierdzamy komunikat o nadpisywaniu danych w tabeli (te tabele aktualnie i tak są puste).

{{<figure align=center src="/hello_world_w_abapie/4.png"  width="80%" >}}


5. Żeby sprawdzić czy dane w tabeli naprawdę istnieją, przechodzimy do transakcji se16. Aby uruchomić transakcję będąc w innej, należy poprzedzić kod transakcji „/n”. Zwróć uwagę że program wypełnił 3 tabele: SPFLI,SFLIGHT i SBOOK. W tym SPFLI ma 26 rekordów.

{{<figure align=center src="/hello_world_w_abapie/5.png"  width="80%" >}}


6. Wpisujemy nazwę tabeli którą chcemy sprawdzić i naciskamy enter.

{{<figure align=center src="/hello_world_w_abapie/6.png"  width="80%" >}}


7. Żeby sprawdzić liczbę rekordów należy nacisnąć klawisz Number of Enteries. Można też sprawdzić zawartość tabeli przez kliknięcie execute.

{{<figure align=center src="/hello_world_w_abapie/7.png"  width="80%" >}}


8. Po kinięciu na number of enteries, wyświetlony zostanie komunikat.

{{<figure align=center src="/hello_world_w_abapie/8.png"  width="80%" >}}


9. Przechodzimy teraz do transakcji se80, która jest wspólną transakcją do tworzenia oprogramowania w SAPie.

{{<figure align=center src="/hello_world_w_abapie/9.png"  width="80%" >}}


10. Wchodzimy teraz w program utworzony w poprzednim kroku, i włączamy edycję poprzez naciśnięcie zaznaczonej ikonki.

{{<figure align=center src="/hello_world_w_abapie/10.png"  width="80%" >}}


11. W prawej stronie ekranu wpisujemy kod odpowiedzialny za wyświetlenie Hello World. Następnie zapisujemy, aktywujemy i uruchamiamy program.

{{<figure align=center src="/hello_world_w_abapie/11.png"  width="80%" >}}

12. Wynik działania programu powinien być taki jak przedstawiono na ekranie poniżej.

{{<figure align=center src="/hello_world_w_abapie/12.png"  width="80%" >}}

13. Wracamy teraz do naszego programu i zmieniamy jego zawartość, tak żeby wykorzystać dane z tabel, które wcześniej uzupełniliśmy.

{{< highlight js >}}
*&---------------------------------------------------------------------*
*& Report ZHELLOWORLD
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT zhelloworld.
 
DATA:                                                               "Deklaracje typów
  g_tab_spfli TYPE TABLE OF spfli,                                  "Deklaracja tabeli lokalnej
  g_str_spfli TYPE spfli.                                           "Deklaracja struktury (pojedyńczego rekordu tabeli)
 
SELECT * FROM spfli INTO CORRESPONDING FIELDS OF TABLE g_tab_spfli. "Pobranie danych z głownej tabeli
 
LOOP AT g_tab_spfli INTO g_str_spfli.                               "Pętla wybierająca dane do struktury
  WRITE:/ g_str_spfli-countryfr,'-',g_str_spfli-countryto.          "Wypisywanie danych na ekran
ENDLOOP.                                                            "Koniec pętli
 
WRITE:/ 'Hello World'.

{{< /highlight >}}

{{<figure align=center src="/hello_world_w_abapie/13.png"  width="80%" >}}


Wynik działania naszego programu powinien wyglądać tak jak na obrazku poniżej.

{{<figure align=center src="/hello_world_w_abapie/14.png"  width="80%" >}}

<mark>
Prawdopodobnie na twoim ekranie widoczne będą inne wyniki, jest to spowodowane tym że dane są randomowo generowane do tabeli.
</mark>
Jeżeli twój efekt końcowy jest zbliżony do tego na ostatnim screenschocie to gratuluję ! Napisałeś właśnie pierwszy program w ABAPie.
