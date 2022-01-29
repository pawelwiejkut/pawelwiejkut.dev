---
title: "Ballog czyli logowanie danych w ABAPie"
date: 2019-04-14T17:01:40+01:00
tags: ["ABAP","ABAP od podstaw"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Każdy język programowania posiada możliwość zapisania informacji technicznej, czy też zdarzenia które może być pomocna później na przykład podczas sprawdzenia poprawności działania napisanego programu. W wielu językach czynność ta sprowadza się często do napisania jednej linijki kodu, np:

{{< highlight js >}}
console.log("Oh, coś poszło nie tak!");
{{< /highlight >}}

W ABAPie sytuacja jest trochę bardziej skomplikowana. Zacznijmy może od napisania prostego programu, który będzie opierać się na stworzonych przez nas wcześniej obiektach DDICowych. Żeby nauczyć się czegoś nowego polecam razem ze mną wykonać wszystko w eclipse, oczywiście równie dobrze każdy krok będzie działać też bezpośrednio w SAP GUI.

Uwaga, w tym artykule przedstawiam tylko jeden sposób na obsługę balloga. Nie omawiam tu również szczegółowo wiadomości które wyświetlamy na ekranie użytkownika. 

<mark>Jeżeli szukasz kompletnego kursu online abap od podstaw – zapraszam Cię do zapoznania się z ofertą: https://saponit.pl/kurs-abap/</mark>

# Tworzymy program

1. Odpalmy sobie eclipse, kliknijmy prawym przyciskiem na pakiecie $TMP w naszym projekcie i wybierzmy New->Other ABAP Repository Object

{{<figure align=center src="/ballog_abap_logowanie/1.png"  width="70%" >}}

2. Wpisujemy „program” i wybieramy ABAP program

{{<figure align=center src="/ballog_abap_logowanie/2.png"  width="50%" >}}

3. Wypełniamy konieczne pola

{{<figure align=center src="/ballog_abap_logowanie/3.png"  width="50%" >}}

4. Programujemy sobie teraz raport który będzie umożliwiał wpisanie nam jednego rekordu do naszej tabelki:

{{< highlight abap >}}

REPORT zemp_add.
 
PARAMETERS:
  pa_id  TYPE char3,
  pa_nam TYPE zemp_name,
  pa_lnm TYPE zemp_name.
 
 
END-OF-SELECTION.
 
  DATA:
  ls_employees TYPE zstr_employees.
 
  ls_employees-id = pa_id.
  ls_employees-name = pa_nam.
  ls_employees-last_name = pa_lnm.
 
  insert zemployees from ls_employees.
  
  Write: | { pa_nam } was successfully added into table| .

{{< /highlight >}}


5. Uzupełnijmy sobie jeszcze text elementy, żeby nazwy naszych parametrów były wyświetlane poprawnie, w tym celu kliknijmy prawym przyciskiem i wbierzmy Open Others-> Text Elements

{{<figure align=center src="/ballog_abap_logowanie/4.png"  width="70%" >}}
{{<figure align=center src="/ballog_abap_logowanie/5.png"  width="70%" >}}


# Debbugujemy

6. Zapisujemy,aktywujemy i uruchamiamy program z wybranymi parametrami np. poprzez F8

{{<figure align=center src="/ballog_abap_logowanie/6.png"  width="70%" >}}


7. Sprawdźmy teraz zawartość naszej tabeli, żeby tego dokonać, musimy rozwinąć naszą paczkę $TMP, i poszukać tabeli w katalogu „Database Tables”. Następnie klikamy na tabeli prawym przyciskiem myszy i wybieramy „Open With”->”Data Preview”.

{{<figure align=center src="/ballog_abap_logowanie/7.png"  width="70%" >}}

8. Finalnie w tabeli powinien pojawić się nowy rekord

{{<figure align=center src="/ballog_abap_logowanie/8.png"  width="70%" >}}

9. Niestety jeżeli jeszcze raz uruchomimy program z tymi samymi parametrami to znów dostaniemy komunikat o poprawnym wprowadzeniu rekordu mimo tego że nic się nie zmieni i w tabeli będziemy mieć wciąż tylko jeden rekord. Dlaczego tak się stało ? Ustawmy breake-point poprzez dwukrotne kliknięcie w pole obok ostatniej lini. Spowodowuje to wyświetlenie w tym miejscu niebieskiej kropki.

{{<figure align=center src="/ballog_abap_logowanie/9.png"  width="70%" >}}

10. Teraz kiedy uruchomimy raport znów z tymi samymi parametrami co na początku zobaczymy że wartość sy-subrc jest równa 4, ale co to właściwie oznacza ?

{{<figure align=center src="/ballog_abap_logowanie/10.png"  width="70%" >}}

11. Wartość sy-subrc jest aktualizowana każdorazowo po wykonaniu niektórych instrukcji w ABAPie . Aby sprawdzić co oznacza sy-subrc 4 w przypadku insert, pozwólmy zakończyć się programowi poprzez naciśnięcie F8 i wróćmy do perspektywy abapowej naszego raportu.

{{<figure align=center src="/ballog_abap_logowanie/11.png"  width="70%" >}}

12. Najedźmy teraz kursorem na insert i kliknijmy F1, następnie wybierzmy INSERT dbtab

{{<figure align=center src="/ballog_abap_logowanie/12.png"  width="70%" >}}

13. Po zescrolowniu na dół zobaczymy informacje o sy-subrc mówiącą że nasz wiersz nie jest unikatowy, ale jak to możliwe ? Po porostu nasza tabela którą stworzyliśmy w DDICu podczas ostatniej lekcji ma w kluczu jedno pole: ID i ta wartość musi być unikatowa. Oczywiście po niepoprawnym sy-subrc możemy jedynie wyświetlić użytkownikowi informacje że taki wpis już istnieje, jednak nam zależy również na zalogowaniu tej informacji gdzieś na stałe.

{{<figure align=center src="/ballog_abap_logowanie/13a.png"  width="50%" >}}

# Tworzymy obiekt ballogowy

14. Przejdżmy zatem do transakcji slg0 i kliknijmy na „New Entries”

{{<figure align=center src="/ballog_abap_logowanie/13.png"  width="70%" >}}

15. Wypełniamy nazwę obiektu

{{<figure align=center src="/ballog_abap_logowanie/14.png"  width="70%" >}}


16. Zapisujemy i dodajemy nasz wpis do transportu

{{<figure align=center src="/ballog_abap_logowanie/15.png"  width="70%" >}}

17. Zaznaczamy stworzony obiekt i klikamy na Sub-objects

{{<figure align=center src="/ballog_abap_logowanie/16.png"  width="70%" >}}

18. Klikamy znowu na „New Entries”

{{<figure align=center src="/ballog_abap_logowanie/17.png"  width="70%" >}}

19. Wypełniamy sub-obiekt i zapisujemy

{{<figure align=center src="/ballog_abap_logowanie/18.png"  width="70%" >}}

# Używamy balloga w raporcie

20. Zmieńmy teraz nasz program tak aby wyglądał następująco

{{< highlight abap >}}

REPORT zemp_add.
 
PARAMETERS:
  pa_id  TYPE char3,
  pa_nam TYPE zemp_name,
  pa_lnm TYPE zemp_name.
 
 
END-OF-SELECTION.
 
  DATA:
  ls_employees TYPE zstr_employees.
 
  ls_employees-id = pa_id.
  ls_employees-name = pa_nam.
  ls_employees-last_name = pa_lnm.
 
  INSERT zemployees FROM ls_employees.
 
  IF sy-subrc = 0.
    MESSAGE |{ pa_nam } was successfully added into table| TYPE 'S'.
  ELSEIF sy-subrc = 4.
 
    DATA: ls_header  TYPE bal_s_log,
          lt_handler TYPE bal_t_logh,
          lv_handle  TYPE balloghndl,
          lv_text    TYPE c LENGTH 50.
 
    ls_header-object    = 'ZB_EMP'.
    ls_header-subobject = 'ZB_EMP_ADD'.
    ls_header-extnumber = 'Employees insert report log'.
 
    "tworzymy obiekt ballogowy
    CALL FUNCTION 'BAL_LOG_CREATE'
      EXPORTING
        i_s_log      = ls_header
      IMPORTING
        e_log_handle = lv_handle.
 
    "dodajemy wiadomość o niepowodzeniu naszego programu
    lv_text = |Entry with key { pa_id } already exists|.
 
    CALL FUNCTION 'BAL_LOG_MSG_ADD_FREE_TEXT'
      EXPORTING
        i_log_handle = lv_handle
        i_msgty      = 'E'
        i_text       = lv_text.
 
    APPEND lv_handle TO lt_handler.
 
    "zapisujemy informacje o niepowodzeniu w ballogu
    CALL FUNCTION 'BAL_DB_SAVE'
      EXPORTING
        i_t_log_handle = lt_handler.
 
    MESSAGE: lv_text TYPE 'E'.
 
  ENDIF.

{{< / highlight >}}

22. Uruchamiamy nasz program znów z poprzednimi wartościami. Tym razem powinnismy dostać message z informacją o błędzie

{{<figure align=center src="/ballog_abap_logowanie/19a.png"  width="70%" >}}


23. Przejdźmy teraz do transakcji slg1 i wypełnijmy nazwę naszego obiektu. Warto też zwrócić uwagę na przedział czasowy w jakim wyświetlają się nasze logi, czasami jeżeli nie wyłączamy całkowicie naszej wirtualnej maszyny to data i godzina mogą się różnić od tych ustawionych na naszym systemie. Po wprowadzeniu wartości uruchamiamy program.

{{<figure align=center src="/ballog_abap_logowanie/19.png"  width="70%" >}}

24. Finalnie powinniśmy zobaczyć jeden błąd w górnej części programu i po kliknięciu na niego pojawią się nam szczegóły. Od teraz nasze błędne wprowadzenia są już logowane i można do nich wrócić.

{{<figure align=center src="/ballog_abap_logowanie/20.png"  width="70%" >}}

To już wszystko w tym artykule poświęconym ballogowi. Od teraz znasz już podstawowy sposób na zalogowanie informacji.