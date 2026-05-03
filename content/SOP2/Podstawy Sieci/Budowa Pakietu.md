Przykładowa budowa pakietu wygląda następująco:
![[packet_ex.png]]

ma 74 bajty i wygenerowane automatycznie nagłówki. został wysłany z maszyny lokalnej do serwera jako początek zawierania połączenia.

Dane aplikacji są zawsze zawinięte przez OS i poprzedzone nagłówkami![[packet_encaps.png]]


Podczas przesyłu z userspace, dane przechodzą przez różne warstwy kernela. Tam powyższe headery są prependowane. (Podczas odbioru odwrotna kolejność i headery ściągane).
![[networking_stack.png]]