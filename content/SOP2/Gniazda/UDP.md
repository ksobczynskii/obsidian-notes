### User Datagram Protocol
- *Nie wymaga połączenia*
- *Szybki, zawodny* 
- *Posługuje się wiadomościami typu Datagram* 


Datagram UDP rozpoczyna się od prostego, 8-bajtowego nagłówka![[udp_header.png]]
- **Source Port** - z jakiego portu wewnątrz hosta wysłano datagram
- **Dest Port** - do jakiego portu mamy wysłać datagram wewnątrz odbierającego hosta
- **Length** - długość datagramu
- **Checksum** - informacja o uszkodzeniu danych

Maksymalna długość datagramu to 64KiB.

#### Szczegóły UDP:

- **Bezpołączeniowy** - nie występuje żaden rodzaj handshake'a, Implementacja w kernelu jest w większości bezstanowa. 
	- Wysyłający specyfikuje dest dla każdej wiadomości.
	- Jeden UDP socket może czytać nadchodzące datagramy z wielu różnych wysyłających.
- **Multicast, Broadcast** - Wspiera wysyłanie jednego pakietu do wielu hostów,
- **Zawodny, bez gwarancji sukcesu** - sieć lub OS może napotkać:
	- ***Zanik*** - Datagramy po cichu zgubione bez informacji o tym.
	- ***Duplikacja*** - ten sam datagram odebrany podwójnie
	- ***Reorder*** - brak gwarancji ciągłości odbioru pakietów, mogą przyjść w innej kolejności niż wysłane.


