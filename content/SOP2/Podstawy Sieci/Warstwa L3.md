#### Czy L2 to za mało?
Tak bo:
- Płaskie adresowanie - MAC nie ma hierarchii and znaczenia w geografii. Są połączone z hardwarem a nie lokalizacją w sieci.
- Flooding - Switche uczą się floodując nieznane kierunki. 
- Zależność od mediów - L2 jest zależne od konkretnego kabla/sygnału. Musimy mieć uniwersalny protokół do spinania wszystkiego razem.


#### Jak warstwa L3 rozwiązuje te problemy?
- Hierarchiczna adresacja - adresy IP tworzą podsieci, podsumowują miliony hostów do jednej danej w routing table.
- Routing zamiast floodingu - Router łączy inne sieci. W przeciwieństwie do switchy, jeśli router nie zna dst - nie broadcastuje. Przesyła pakiet do *Default Gateway* lub zwyczajnie nie przesyła.
- IP to most między technologiami przesyłu. ![[routing_ops.png]]


#### Header L3 - IP
Pakiet IP ma zazwyczaj 20 bajtów wliczając src i dest adresów IP (nie Mac jak w L2)

![[L3_packet.png]]


#### Operacje urządzeń L3

Urządzenie IP (router/host) może mieć wiele interfejsów połączonych z sieciami L2. Procesuje pakiety IP nadchodzące z podwiązanych sieci:

- Odbieram ramkę L2 od innego hosta związanego z siecią L2.
	- src hardware address to L2 address tego innego hosta
	- dst hardware address to L2 address odbierającego portu
- Odpinam nagłówek L2 by wyjąć pakiet IP.
- Decyduje co z nim robię:
	- Zatrzymaj się jeśli nie dla mnie.
	- Wyrzuć jeśli nie dla mnie.
	- Wyślij gdzieś indziej jeśli nie dla mnie (router)

**Send**

- Na podstawie dst IP wybieramy tzw *outbound port*
- Wybieramy target host na sieci L2 osiągalny z outbound portu (nie musi być IP host destination)
- Wrapujemy pakiet w network-specific ramkę L2
	- src hardware address == outbound port adresu L2
	- dst hardware address == adres w L2 hosta doeclowego.
- Wysyłamy!


#### Operacje Routera

Generalnie rolą routera jest forwardowanie pakietów pomiędzy sieciami. Po odbiorze pakietu router wykonuje następujące:
- Na podstawie dst IP address - wybierz gdzie wyforwardować pakiet
	- (a) jakiś host wewnątrz jednej z bezpośrednio podłączonych sieci
	- (b) jakiś host pośrednio uzyskiwalny za pomocą przesyłu do innego routera
- Wrapujemy pakiet z powrotem w ramkę L2 i wysyłamy
	- IP src oraz IP dst pozostają niezmienione
	- L2 src address to outbound interface routera
	- (a) L2 dst address jest bezpośrednio adresem hardwarowym hosta do którego chcemy wysłać
	- (b) L2 dst address jest tzw *next hop* router adresem.


![[routing_example.png|697]]

![[routing_example_2.png]]

Zauważmy, że o ile L3 Addressing się nie zmienia, o tyle L2 addressing nie tylko może przyjmować inne dane ale nawet inne schematy adresowania (w jednym MAC w innym co innego).


#### Address Resolution Protocol 

Kiedy już wiemy, że pakiet powinien zostać wysłany do hosta a1 (adres 1 IP) poprzez interface eth0, lub do routera do a2 poprzez eth1 musimy odnaleźć adres L2 urządzenia, któremu wysyłamy wiadomość.

Sender wysyła ARP request do boradcast L2 address: 
![[arp_req.png]]

Host z odpowiednim adresem odpowiada: 
![[arp_res.png]]


Pakiet ARP wysyłany jest w formacie: 
![[arp_packet.png]]


#### Tabela routingu

Dezycja gdzie wysyłać pakiety IP podejmowana jest na podstawie tabeli routingu:

![[routing table.png]]


- 192.168.1.0/24 - podłączona sieć, jeśli dst zaczyna się od pefixu sieciowego 192.168.1 - wyślij po eth0
- 10.0.0.0/24 - konkretna ścieżka. Jeśli adres zaczyna się od 10.0.0. - wyślij do routera po eth1 na 192.168.2.254
- default lub 0.0.0.0/0 - destynacja IP nie jest znana - wyślij po eth0 do 192.168.1.1 i miej nadzieje, że uaktualnisz wiedzę


#### Fragmentacja IP
Urządzenia L3 mogą rozdzielić i sklejać w całość pakiety IP. Jest to znane jako fragmentacja i rekonstrukcja (*fragmentation and reassembly*). IP header zawiera **Identification, Flags i Fragment Offset** - te mówią nam o stanie fragmentacji.![[fragmentacja.png]]

#### TTL - Time To Live

Jest to pole w nagłówku IP, mówiące o tym jak długo pakiet może być w transmisji do wyrzucenia na 'śmietnik'. Za każdym forwardingiem routery dekrementują tenże counter o 1 i wysyłają ICMP message do oryginalnego wysyłającego.


#### ICMP - Internet Control Message Protocol

Jest to protokół warstwy L3 do raportowania błędów w warstwie IP. Definiuje typy wiadomości:
- **Echo Request & Reply** - do weryfikowania podstawowego połączenia i opóźnienia przesyłu (ping).
- **Destination Network/ Host unreachable** - Generowana przez router gdy nie ma ścieżki w tablicy routingu.
- **Destination Port Unreachable** - Generowana przez hosta odbiorce gdy pakiet dotarł, ale aplikacja nie nasłuchuja na konkretnym porcie TCP/UDP
- **Time Exceeded** - Generowana przez router gdy TTL spadł do zera.