Sieci Lokalne (L2)

L2 rozwiązuje prosty problem: wysyłanie ramek pomiędzy grupą fizycznie połączonych hostów, które formują LAN (Local Area Network). Nie ma za zadanie wysyłać danych na skalę globalną.

![[l2_workflow.png]]

Ethernet to standard dzisiejszych czasów.

#### Nagłówek ethernetowy

Warstwa L2 i jej protokół interesuje się jedynie nagłówkiem L2.
![[ethernet_header.png]]

- 6 bajtów - destination address
- 6 bajtów - source address
- 2 bajty - protokół warstwy L3 (0x0800 - IPv4, 0x86DD - IPv6 etc.)

Ethernet specyfikuje 48 bitowy adres MAC, który odpowiada interfejsowi hosta.
Te są zazwyczaj globalnie unikatowe w formacie:
Manufacturer ID (24b) : Serial ID(24b)

Adresy MAC nie formułują geograficznej hierarchii, więc nie pozwalają na budowę skalowalnych, globalnych sieci.

Adres src jest kodowany jako adres lokalnego IF, który sygnalizuje miejsce gdzie odpowiadać innymi pakietami. Musisz znać adres dest, zazwyczaj kernel znajduje go automatycznie.

#### Operacje switcha

Switch myśli w bardzo prosty sposób:
coś z A1 (adresu) przyszło przez eth2 -> wszystko idące do A1 musi iść do eth2!
![[switch ops.png]]