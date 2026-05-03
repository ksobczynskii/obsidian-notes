### Tworzenie Socketów

Do uzyskania dostępu do dowolnej sieci, aplikacja POSIX musi stworzyć socket za pomocą syscalla *socket()*. Zwraca fd nowo utworzonego socketa.
![[socket().png]]
- **Domain** - typ adresowania, np. AF_INET - IPv4. (AF_BLUETOOTH, AF_INET6...)
- **Type** - typ komunikacji, np. SOCK_DGRAM - datagram, SOCK_STREAM - strumień.
- **Protocol** - zazwyczaj podaje się zero, OS wybiera protokół na podstawie dwóch powyżej (AF_INET + SOCK_DGRAM = UDP).

Po otworzeniu z sukcesem socket istnieje w kernelu, lecz nie ma przypisanego portu, adresu i nie umie jeszcze wysyłać/odbierać danych. Chwilowo jest pustym obiektem z wybranym stackiem sieciowym.

### Nadanie adresu

Do nadania adresu używa się syscalla *bind()*
![[bind().png]]

Aplikacja serwerowa zawsze wywołuje *bind()*. Oczekuje się od nich odbierania komunikatów na znanych portach np. 53 dla DNS

Aplikacja kliencka często pomija *bind()* - OS automatycznie wybiera randomowy, nieużywany port podczas pierwszej wysyłki.

Adresy Socketów zawierają część IP. Może być to adres jednego z dostępnych interfejsów sieciowych lub wildcard jak 0.0.0.0 (INADDR_ANY) - odbieranie danych z wszystkich dostępnych podsieci. 

##### Struktura adresu
Różne rodziny adresowania używają rożnych struktur adresowania. Istnieje jedna klasa bazowa dla adresów których oczekuje bind:
![[sokcaddr_t.png]]


Ale można rzutować struktury dla konkretnych adresować na *sockaddr*, jak![[sockaddr_in.png]]


### Kolejność bajtów

Dwie maszyny komunikujące się w sieci mogą mieć inne naturalne endiany. 
![[endianess.png]]Konwencja w sieci to **NBO** - Network Byte Order w Big Endian.
Aplikacje muszą zamieniać kolejność manualnie. Kernel nie ma prawa wiedzieć jak interpretować bajty z aplikacji w L5+. API Socketów oczekuje adresów struktur w NBO.

#### Pomoc w adresacji

- *inet_pton()* - konwersja text->binary address
- *inet_ntop()* - binary adres -> text![[pton.png]]
- *getsockname()* - zwraca adres przypisany do socketa
- *getpeername()* - zwraca adres remote'a, połączonego współkomunikatora (TCP)
![[getsockname.png]]


### Wysyłanie i odbieranie bajtów

![[send_to.png]]

- Wysyła pojedynczy datagram
- Musisz podać destination addres dla każdej wysyłki.
- Zwraca numer bajtów wysłanych ( NIE ODEBRANYCH!)
![[recv.png]]
- Odbierz jeden nadchodzący datagram
- **addrlen** - in/out parameter, podajesz capacity a kernel zwraca length
- Zwraca liczbę bajtów odebraną do void* buf.