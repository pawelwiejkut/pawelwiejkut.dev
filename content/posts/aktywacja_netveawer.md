---
title: "Aktywacja SAP Netveawer 7.5"
date: 2017-03-04T21:44:24+02:00
tags: ["ABAP","ABAP od podstaw"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Kiedy mamy już zainstalowanego SAP NetWeavera, należy aktywować naszą instalację SAP. Proces ten jest o wiele łatwiejszy niż instalacja, wymaga jednak pewnego oswojenia z interfejsem. Aktywacja instalacji jest niezbędna aby można było tworzyć programy w ABAPie. Przejdźmy do rzeczy.
<mark>Od jakiegoś czasu tworzę kurs online poświęcony właśnie pogramowaniu w ABAPie, jeżeli jesteś zainteresowany, zostaw e-mail ponizej </mark>
<!-- Begin Mailchimp Signup Form -->
<link href="//cdn-images.mailchimp.com/embedcode/horizontal-slim-10_7.css" rel="stylesheet" type="text/css">
<div id="mc_embed_signup">
<form action="https://saponit.us19.list-manage.com/subscribe/post?u=ead4e0dc04f1f8c07403a39ac&amp;id=b53be8fac4" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">
	<input type="email" value="" name="EMAIL" class="email" id="mce-EMAIL" placeholder="email" required>
    <!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
    <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_ead4e0dc04f1f8c07403a39ac_b53be8fac4" tabindex="-1" value=""></div>
    <div class="clear"><input type="submit" value="Zapisz się" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
    </div>
</form>
</div>

<!--End mc_embed_signup-->

1. Logujemy się do systemu i wchodzimy w transakcję SLICENSE.
<img src="/slicense.png" width="80%" />
2. Kopiujemy  active hardware key.
<img src="/hardware_key-1.png" width="80%" />
3. Przechodzimy na stronę https://go.support.sap.com/minisap/ , wybieramy NPL i klikamy Generate. Krok ten dobrze jest wykonać w przeglądarce Internet Exploler.
<img src="/generate-1.png" width="80%" />
4. Po zapisaniu wygenerowanego pliku, wracamy do transakcji SLICENSE gdzie klikamy na Install. Po zakończeniu procesu nasz numer instalacji powinien zostać zmieniony na DEMOSYSTEM.
<img src="/demosystem-1.png" width="80%" />
5. Teraz należy wpisać Acces Key, aby to zrobić stworzymy od razu paczkę w której możemy następnie umieszczać swoje programy. W tym celu przechodzimy do transakcji se80.
<img src="/se80.png" width="80%" />
6. Żeby stworzyć paczkę, należy w wpisać jej nazwę zaczynającą się od Z albo Y, następnie nacisnąć enter.
<img src="/package.png" width="80%" />
7. Uzupełniamy wymagane pola
<img src="/package_desc.png" width="80%" />
8. Następnie klikamy prawym klawiszem myszy na paczce i wybieramy Create -> Program.
<img src="/create_program.png" width="80%" />
9. Uzupełniamy nazwę programu.
<img src="/create_program_desc.png" width="80%" />
10. Następnie przechodzimy do folderu z rozpakowanymi plikami i otwieramy plik readme.html, skąd kopiujemy klucz.
<img src="/key.png" width="80%" />
11. Na końcu wklejamy klucz do SAPA i klikamy Continue
<img src="/register.png" width="80%" />
12. Potwierdzamy utworzenie programu poprzez kliknięcie save
<img src="/save.png" width="80%" />
13. Na końcu klikamy na ikonę dyskietki
<img src="/save2.png" width="80%" />
14. Gotowe ! System jest teraz w pełni aktywny i gotowy do działania.
