Praca z sieciami to zwyczajnie IPC, gdzie procesy odpalane są wewnątrz różnych OS-ów.
![[sieci.png]]
Procesy nie mogą jednak współdzielić pamięci, gdyż mogą one leżeć na innych fizycznych (lub wirtualnych) maszynach.

OS ma za zadanie ukryć złożoność sieci i zapewnić API do uzyskiwania dostępu do sieci i łatwej i bezpiecznej implementacji.

Sieci (fizyczne i wirtualne) transmitują wiadomości zwane **pakietami**.
Pakiet - ciąg bajtów kodujący dane aplikacji oraz metadane dla przesyłu w sieci.
![[pakiet.png]]
OS przekierowuje odebrany pakiet do odpowiedniej aplikacji.