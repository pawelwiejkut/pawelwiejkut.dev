---
title: "Działania na plikach"
date: 2019-05-06T17:53:34+01:00
tags: ["ABAP","ABAP od podstaw"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Potrafimy już tworzyć podstawowe struktury danych, wiemy też jak zalogować informację przy użyciu Balloga. Czas więc przejść do kolejnego kroku i dowiedzieć się w jaki sposób możemy przeprocesować dane zewnętrzne w ABAPie. Weźmy na przykład taki plik .csv, z którego chcielibyśmy przenieść do tabeli:

employees [Pobierz](/dzialania_na_plikach/employees.csv)</br>

Procedura jest ogólnie będzie dość prosta – jedną tabelkę już przecież mamy. Nasz program będzie potrafił:

- wczytać dane od użytkownika,
- wprowadzić nowe wpisy od użytkownika do bazy ,
- wprowadzić wpisy z serwera aplikacji do bazy.</br>

Fajnie byłoby aby program był tak dynamicznie napisany, że nie będziemy musieli go zmieniać nawet jeżeli będziemy chcieć „wpisać” dane do tabeli określonej w pierwszej kolumnie naszego pliku. Jeżeli otworzymy zbiór danych, zobaczymy że prezentują się one następująco:

{{<figure align=center src="/dzialania_na_plikach/1.png"  width="60%" >}}


Uwaga, w tym artykule przedstawiam dwa ważne rozdziały: operacje na plikach i programowanie obiektowe. Jeśli niektóre rozwiązania są dla Ciebie niejasne, bądź też chcesz dowiedzieć się więcej to <mark>
zapraszam Cię do zapoznania się z ofertą: https://saponit.pl/kurs-abap/ </mark>

# Tworzymy dodatkową tabelę
Pierwszą kolumną w pliku csv oznaczona jest nazwa tabeli do której chcemy wpisać dane. Dwie kolejne zawierają dane które chcemy do podanych tabel wpisać. Potrzebujemy zatem poza tabelką ZEMPLOYEES jeszcze tabelę ZSALARIES. Możemy ją szybko utworzyć w eclipse:

{{<figure align=center src="/dzialania_na_plikach/2.png"  width="60%" >}}
{{<figure align=center src="/dzialania_na_plikach/3.png"  width="60%" >}}


{{<highlight abap>}}
@EndUserText.label : 'Employees salaries'
@AbapCatalog.enhancementCategory : #NOT_EXTENSIBLE
@AbapCatalog.tableCategory : #TRANSPARENT
@AbapCatalog.deliveryClass : #A
@AbapCatalog.dataMaintenance : #LIMITED
define table zsalaries {
  key id : char3 not null;
  amount : integer64; }
{{</highlight>}}


Tabele mamy gotowe, fajnie byłoby gdybyśmy mogli nie tylko używać plików pobranych od użytkownika, ale również tych które są dostępne na app serwerze. O tym ostatnim jeszcze nie pisałem w żadnych z poprzednich poradników. Nowością jest tu transakcja al11, która służy w NetVeawer do przechowywania plików. Można powiedzieć, że jest ona odpowiednikiem windowsowego explorera, widać w niej foldery odpowiadające tym faktycznie umieszczonym na dysku twardym wirtualnej maszyny:

{{<figure align=center src="/dzialania_na_plikach/4.png"  width="80%" >}}


Dostęp do plików z poziomu ABAPa odpowiada dostępowi z poziomu systemu operacyjnego. Jest to o tyle ważne, że jeżeli używamy Windowsa to wielkość znaków w ścieżce do pliku nie ma znaczenia, <mark>natomiast w przypadku Linuxa jest odwrotnie. Nasz serwer aplikacji zainstalowany jest na maszynie z Linuxem</mark>, natomiast serwer prezentacji (czyli SAP GUI) możemy mieć zainstalowany na dowolnym systemie operacyjnym, np. Windows.
Nasz development będzie składać się z dwóch klas i raportu służącego do uruchomienia. Wykorzystamy tutaj dziedziczenie, czyli jedną z zalet programowania obiektowego. Jeżeli chcielibyśmy przedstawić klasy graficznie wyglądałoby to następująco:

{{<figure align=center src="/dzialania_na_plikach/5.png"  width="80%" >}}


# Klasa po której będziemy dziedziczyć

1. Zacznijmy od eclipse i stwórzmy pierwszą klasę ZCL_FILE. Po pierwsze musimy zadeklarować potrzebne typy danych:

{{<highlight abap>}}
CLASS zcl_file DEFINITION
  PUBLIC
  CREATE PUBLIC .
 
  PUBLIC SECTION.
 
    TYPES t_string_tab  TYPE string.
    TYPES tt_string_tab TYPE STANDARD TABLE OF t_string_tab.
 
    METHODS insert_to_table
      IMPORTING iv_table_name TYPE string
                it_table      TYPE STANDARD TABLE.
 
  PROTECTED SECTION.
    METHODS process_table
      IMPORTING is_line_to_insert TYPE t_string_tab
      EXPORTING et_processed_data TYPE tt_string_tab
                ev_table_name     TYPE string.
 
  PRIVATE SECTION.
 
ENDCLASS.

{{</highlight>}}

Określamy najpierw własne typy: strukturę zwierającą tylko stringi i tabelę do niej. W sekcji publicznej tworzymy również dwie metody. Pierwsza z nich ma za zadanie wpisać nasze dane do tabeli, natomiast druga jest odpowiedzialna za odczytanie przekazanej lini z tabeli i określenia do jakiej tabeli wpis powinien trafić.

2. Implementacja:

{{<highlight abap>}}
CLASS zcl_file IMPLEMENTATION.
 
  METHOD insert_to_table.
    "deklarujemy tabele stringów
    DATA:lt_tab  TYPE tt_string_tab.
    "oraz dwie referencje, do danych i do opisu struktury
    DATA:
      lr_str  TYPE REF TO data,
      lr_strd TYPE REF TO cl_abap_structdescr.
    "tworzymy sobie referencje
    CREATE DATA lr_str TYPE (iv_table_name).
    "i przypisujemy ją do field-sybolu
    ASSIGN lr_str->* TO FIELD-SYMBOL(<ls_str>).
    "pobieramy refernecję do opisu naszej struktury na podstawie field-symbolu
    "(można było również pobrać ją po nazwie)
    lr_strd ?= cl_abap_tabledescr=>describe_by_data_ref( lr_str ).
    "wykonujemy petle po wszytskich komponentach naszej struktury
    "(w przypadku zemployees będzie tu:ID,NAME,LAST_NAME)
    LOOP AT lr_strd->components ASSIGNING FIELD-SYMBOL(<ls_comp>).
      "każdy z komponentów przypisujemy do zmiennej
      ASSIGN COMPONENT <ls_comp>-name OF STRUCTURE <ls_str> TO FIELD-SYMBOL(<lv_comp>).
      "z odczytanej lini z danymi bierzemy odpowiednią wartość, o takiej samej kolejności
      "jak ta odczytana z kompnentu
      "(w przypadku naszego pliku pierwsze będzie tu: JNO ")
      ASSIGN it_table[ sy-tabix ] TO FIELD-SYMBOL(<ls_ctab>) .
      "do struktury przypisujemy dane z odczytanej lini, teraz nasze dane
      "powinny być w poprawnym typie w <ls_str>
      <lv_comp> = <ls_ctab>.
    ENDLOOP.
    "wpisujemy dane do tabeli w bazie danych
    MODIFY (iv_table_name) FROM <ls_str>.
    "jeśli wystąpi błąd, zwróć wiadomość
    IF sy-subrc = 2.
      MESSAGE 'Error occured while modify' TYPE 'E'.
    ENDIF.
  ENDMETHOD.
 
 
  METHOD process_table.
    "podziel linie po przecinku tak żeby powstała z nich tabela
    SPLIT is_line_to_insert AT ',' INTO TABLE DATA(lt_split).
    "wybierz pierwszą wartość, która opisuje tabelę do której
    "trafią dane
    DATA(lv_tab_name) = lt_split[ 1 ].
    "usuwany tą wartość z tabeli
    DELETE lt_split INDEX 1.
    et_processed_data = lt_split.
    ev_table_name = lv_tab_name.
  ENDMETHOD.
ENDCLASS.
{{</highlight>}}

Jeżeli mimo opisu nie do końca rozumiesz co dzieje się w kodzie to się nie przejmuj. Jak program będzie już gotowy po prostu przedebugguj się przez niego.

# Obsługa plików z serwera aplikacji
Zacznijmy od umieszczenia pliku na serwerze aplikacji. Jak wspominałem wcześniej w al11 możemy zobaczyć pliki w tym samym miejscu w którym widać je z poziomu systemu operacyjnego. Możemy więc przenieść je tam za pomocą ssh i nadając im uprawnienia dla npladm, lub użyć modułu funkcyjnego ARCHIVFILE_CLIENT_TO_SERVER. Ważne jest aby koniecznie przed wprowadzaniem danych zaznaczyć flagę Uppercase/Lowercase.

{{<figure align=center src="/dzialania_na_plikach/6.png"  width="80%" >}}

Następnie w path podajemy ścieżkę do pliku na naszym systemie operacyjnym (w Windows będzie ona zaczynać się prawdopodobnie od C:), natomiast w targetpath ścieżkę w której chcemy zapisać plik na serwerze aplikacji. Następnie uruchamiamy modół i sprawdzamy czy plik faktycznie znajduje się w katalogu /usr/sap/NPL/D00/work/.

{{<figure align=center src="/dzialania_na_plikach/7.png"  width="60%" >}}

Jeżeli dwa razy klikniemy w plik powinniśmy zobaczyć jego zawartość:

{{<figure align=center src="/dzialania_na_plikach/8.png"  width="40%" >}}


3. Przejdźmy teraz do definicji klasy ZCL_FILE_SERVER

{{<highlight abap>}}
CLASS zcl_file_server DEFINITION
INHERITING FROM zcl_file
  PUBLIC
  FINAL
  CREATE PUBLIC.
  PUBLIC SECTION.
    METHODS constructor
      IMPORTING iv_path TYPE string.
 
    METHODS process_server_data.
    METHODS: get_ov_path RETURNING VALUE(r_result) TYPE string,
      set_ov_path IMPORTING iv_ov_path TYPE string.
 
  PROTECTED SECTION.
  PRIVATE SECTION.
    DATA: ov_path TYPE string.
ENDCLASS.
{{</highlight>}}

Klasa dziedziczy po klasie ZCL_FILE i dlatego potrzebujemy INHERITING FROM. Po naszej klasie nie będzie można dziedziczyć, dlatego posiada dopisek „final”. Wewnątrz klasy tworzymy prywatny parametr path, który odczytać możemy za pomocą gettera a zapisać za pomocą settera. Jest to zgodne z zasadami programowania obiektowego, i umożliwia nam stworzenie np. dodatkowej walidacji w setterze gdzie możemy sprawdzić czy nasza ścieżka zawiera charakterystyczne znaki jak np. „/”. Do parametru prywatnego nie mamy dostępu zarówno z poziomu obiektu klasy, jak i w przypadku dziedziczenia. Implementacja będzie wyglądać następująco:

{{<highlight abap>}}
CLASS zcl_file_server IMPLEMENTATION.
 
  METHOD constructor.
    "konstruktor jest wywoływany podczas tworzenia obiektu i ustawia argument klasy
    "ov_path przy użyciu settera
    "zgodnie z wymaganimi musimy zawsze wywołać konstruktor nadrzędny, który mimo
    "tego że nie jest przez nas zadeklarowany to niejawnie istnieje
    super->constructor( ).
    set_ov_path( iv_ov_path = iv_path  ).
  ENDMETHOD.
 
  METHOD process_server_data.
    "tworzymy strukturę typu string
    DATA ls_data TYPE t_string_tab.
    "pobieramy ścieżkę do pliku z atrybutu ov_path
    DATA(lv_path) = get_ov_path( ).
    "otwieramy nasz plik z danymi do odczytu w trybie tekstowym
    OPEN DATASET lv_path FOR INPUT IN TEXT MODE ENCODING DEFAULT.
    "jeśli pojawi się błąd, pokaż wiadomość o błędzie
    IF sy-subrc <> 0.
      MESSAGE 'Can not open file for read' TYPE 'E'.
      EXIT.
    ENDIF.
    DO.
      "czytaj plik linia po linii
      READ DATASET lv_path INTO ls_data.
      "jeśli wystąpił błąd to plik prawdopodobnie został już odczytany do końca
      IF sy-subrc <> 0.
        EXIT.
      ENDIF.
      "wywołaj metodę process_table z ZCL_FILE (dziedziczymy ją)
      "do tabeli wyeksportuj linie z naszego pliku i pobierz
      "danę oraz tabele do ktorej należy je wpisać.
      process_table(
        EXPORTING
          is_line_to_insert = ls_data
        IMPORTING
          et_processed_data = DATA(lt_ctab)
          ev_table_name     = DATA(lv_tab) ).
      "wywołaj metodę insert_to_table z ZCL_FILE (dziedziczymy ją)
      "do tabeli wyeksportuj dane, oraz nazwę tabeli
      "do której należy je wpisać
      insert_to_table(
        EXPORTING
          iv_table_name   = lv_tab
          it_table        = lt_ctab ).
    ENDDO.
    "jeśli wszystko poszło ok, wyświetl komunikat o błędzie
    MESSAGE 'Processing succesfull' TYPE 'S'.
  ENDMETHOD.
 
  METHOD get_ov_path.
    r_result = me->ov_path.
  ENDMETHOD.
 
  METHOD set_ov_path.
    me->ov_path = iv_ov_path.
  ENDMETHOD.
 
ENDCLASS.

{{</highlight>}}

# Raport uruchamiający przetważanie
Finalnie możemy przejść do stworzenia raportu który będzie odpowiedzialny za uruchamianie naszej implementacji:

{{<highlight abap>}}

REPORT zload_data.
 
PARAMETERS:
  pa_path TYPE dxfields-longpath LOWER CASE,
  pa_sapp RADIOBUTTON GROUP rb1 USER-COMMAND gr1 DEFAULT 'X',
  pa_sagu RADIOBUTTON GROUP rb1.
 
"Obsługa evetu który umożliwia nam wyświetlenie menu z pomocą we wprowadzeniu
"ściezki do parametru path
AT SELECTION-SCREEN ON VALUE-REQUEST FOR pa_path.
 
  DATA(lv_loc) = SWITCH dxfields-location( pa_sapp
                                           WHEN abap_true THEN 'A'
                                           WHEN abap_false THEN 'P' ).
 
  CALL FUNCTION 'F4_DXFILENAME_TOPRECURSION'
    EXPORTING
      i_location_flag = lv_loc
      i_path          = pa_path
    IMPORTING
      o_path          = pa_path
    EXCEPTIONS
      rfc_error       = 1
      error_with_gui  = 2
      OTHERS          = 3.
  IF sy-subrc &lt;> 0.
    MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
               WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
  ENDIF.
 
AT SELECTION-SCREEN.
  IF sy-ucomm &lt;> 'GR1' AND pa_path IS INITIAL.
    MESSAGE 'File path is required' TYPE 'E'.
  ENDIF.
 
START-OF-SELECTION.
 
  DATA: lt_tab TYPE  zcl_file=>tt_string_tab.
 
  IF pa_sagu = abap_true.
    "tworzymy nowy obiekt
    DATA(lobj_app_server) = NEW zcl_file_gui( ).
    "chcemy znać powód dla którego nie możemy zauploadować pliku
    "z GUI, dlatego EXCEPTIONS są odkomentowane w całości
    cl_gui_frontend_services=>gui_upload(
    EXPORTING
    filename                = CONV #( pa_path )
    CHANGING
    data_tab                =  lt_tab
    EXCEPTIONS
    file_open_error         = 1
    file_read_error         = 2
    no_batch                = 3
    gui_refuse_filetransfer = 4
    invalid_type            = 5
    no_authority            = 6
    unknown_error           = 7
    bad_data_format         = 8
    header_not_allowed      = 9
    separator_not_allowed   = 10
    header_too_long         = 11
    unknown_dp_error        = 12
    access_denied           = 13
    dp_out_of_memory        = 14
    disk_full               = 15
    dp_timeout              = 16
    not_supported_by_gui    = 17
    error_no_gui            = 18
    OTHERS                  = 19 ).
 
    IF sy-subrc &lt;> 0.
      MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
                 WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
    ENDIF.
    "uruchamiamy metodę process_gui_data i przekazuemy dane wczytane z GUI
    lobj_app_server->process_gui_data( lt_table = lt_tab  ).
  ELSE.
    "tworzymy obiekt i przekazujemy wymagne dane do konstruktora
    DATA(lobj_file_server) = NEW zcl_file_server( iv_path = CONV #( pa_path ) ).
    "uruchamiamy metodę do przetwarzania danych z serwera apikacji
    lobj_file_server->process_server_data( ).
  ENDIF.

 {{</highlight>}}
 
Text elementy do raportu powinny wyglądać następująco:

{{<figure align=center src="/dzialania_na_plikach/8a.png"  width="70%" >}}

Finalnie powinniśmy mieć trzy nowe klasy i raport oraz dwie tabele i plik widoczny w al11:

{{<figure align=center src="/dzialania_na_plikach/9.gif"  width="70%" >}}

Przed uruchomieniem programu tabele powinny być puste, natomiast po jego uruchomieniu powinny wypełnić się danymi:

{{<figure align=center src="/dzialania_na_plikach/10.gif"  width="70%" >}}


W tej lekcji to już wszystko. Jeśli plik przeprocesował się poprawnie, wpisy w obu tabelach powinny pojawić się natychmiast po uruchomieniu. Pliki utworzone podczas tej lekcji możecie znaleźć też na githubie:

https://github.com/pawelwiejkut/abap_operacje_na_plikach.git


