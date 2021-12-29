---
title: "Aktywacja SAP Netveawer 7.5"
date: 2017-03-04T21:44:24+02:00
tags: ["ABAP","ABAP od podstaw"]
aliases : [ aktywacja_netveawer]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Kiedy mamy już zainstalowanego SAP NetWeavera, należy aktywować naszą instalację SAP. Proces ten jest o wiele łatwiejszy niż instalacja, wymaga jednak pewnego oswojenia z interfejsem. Aktywacja instalacji jest niezbędna aby można było tworzyć programy w ABAPie. Przejdźmy do rzeczy.
<mark>Od jakiegoś czasu tworzę kurs online poświęcony właśnie pogramowaniu w ABAPie, jeżeli jesteś zainteresowany, sprawdź proszę kursy.saponit.pl </mark>


<!--End mc_embed_signup-->

1. Logujemy się do systemu i wchodzimy w transakcję SLICENSE.
<img src="/aktywacja_netveawer/slicense.png" width="80%" />
2. Kopiujemy  active hardware key.
<img src="/hardware_key-1.png" width="80%" />
3. Przechodzimy na stronę https://go.support.sap.com/minisap/ , wybieramy NPL i klikamy Generate. Krok ten dobrze jest wykonać w przeglądarce Internet Exploler.
<img src="/aktywacja_netveawer/generate-1.png" width="80%" />
4. Po zapisaniu wygenerowanego pliku, wracamy do transakcji SLICENSE gdzie klikamy na Install. Po zakończeniu procesu nasz numer instalacji powinien zostać zmieniony na DEMOSYSTEM.
<img src="/aktywacja_netveawer/demosystem-1.png" width="80%" />
5. Teraz należy wpisać Acces Key, aby to zrobić stworzymy od razu paczkę w której możemy następnie umieszczać swoje programy. W tym celu przechodzimy do transakcji se80.
<img src="/se80.png" width="80%" />
6. Żeby stworzyć paczkę, należy w wpisać jej nazwę zaczynającą się od Z albo Y, następnie nacisnąć enter.
<img src="/aktywacja_netveawer/package.png" width="80%" />
7. Uzupełniamy wymagane pola
<img src="/aktywacja_netveawer/package_desc.png" width="80%" />
8. Następnie klikamy prawym klawiszem myszy na paczce i wybieramy Create -> Program.
<img src="/aktywacja_netveawer/create_program.png" width="80%" />
9. Uzupełniamy nazwę programu.
<img src="/aktywacja_netveawer/create_program_desc.png" width="80%" />
10. Następnie przechodzimy do folderu z rozpakowanymi plikami i otwieramy plik readme.html, skąd kopiujemy klucz.
<img src="/aktywacja_netveawer/key.png" width="80%" />
11. Na końcu wklejamy klucz do SAPA i klikamy Continue
<img src="/aktywacja_netveawer/register.png" width="80%" />
12. Potwierdzamy utworzenie programu poprzez kliknięcie save
<img src="/aktywacja_netveawer/save.png" width="80%" />
13. Na końcu klikamy na ikonę dyskietki
<img src="/aktywacja_netveawer/save2.png" width="80%" />
14. Gotowe ! System jest teraz w pełni aktywny i gotowy do działania.
