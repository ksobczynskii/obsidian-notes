### Transmission Control Protocol
- Inny od Udp, znacznie się różni i bardziej zaawansowany w użyciu.
- Próba umożliwienia niezawodnej, posortowanej, dwustronnej transmisji danych połączonych hostów. ![[tcp_traffic.png]]
Połączona para to unikatowy 4-tuple (IP, port, IP,port).

Hosty transmitują strumienie danych, a nie wiadomości. TCP to strumieniowo-zorientowany protokół. Dane wpisane w write() mogą być odczytywane przez wiele read().


### Nagłówek TCP

TCP nadbudowuje zawodny IP layer. Wiadomości TCP zenkapsulowane w pakietach IP są nazywane **segmentami**. Segment zawiera nagłówek i opcjonalnie payload aplikacji.
![[tcp_header.png]]
##### Sequence Number![[seq_nr.png]]
- Identyfikuje pozycję początku aktualnego segmentu w uporządkowanym strumieniu danych.
- Do diagnozowania straconych segmentów.
- Każdy segmet ma 4-bajtowy seq number, który oznacza offset w streamie.
##### Acknowledgement Number
![[acknr.png]]
- W przypadku straconego segmentu, musi być on zretransmitowany. Odbiorca zaznacza odbiór poprzez wysłanie *acknowledment number* z powrotem w segmantach. 
- W ten sposób piszący wie które segmenty dotarły a które nie. 


##### TX/RX Buffer
- Odebrane segmenty mogą nie być natychmiastowo dostarczone do aplikacji w przypadku gdy np. poprzedzające segmenty zostały zgubione lub jeszcze nie dotarły. 
- Segmenty wysyłane mogą nie zostać wypchnięte do sieci od razu - sender czeka na ACK.
- Każdy socket zawiera 2 bufory w kernelu - **receive (Rx) buffer** oraz **send (Tx) buffer** odpowiednio na nadchodzące i wychodzące segmenty. ![[txrx buffers.png]]

##### Flagi segmentów.
Każdy segment może zawierać ileś flag mówiące o tym jak rozumieć nadchodzący segment:
- SYN - początek nowego strumienie (synchronize)
- FIN - koniec strumienia (finish)
- RST - reset connection
- PSH - zwykły segment danych nadchodzi (nr sekwencji mówi który)
- ACK - zaznaczenie, że poprzednie dane zostały odebrane
- URG - dane nadzwyczajne, urgent (obsolete)
Możliwe są kombinacje powyzszych (PSH+ACK...)




##### Początek połączenia
Aby rozpocząć, oba hosty muszą zgodzić się na numer sekwencji byc rozpocząć połączenie. Nazywa się to **3-way Handshake**
![[tcp_handshake.png]]

- host A wysyła do hosta B segment z początkowym numerem sekwencji i flagą SYN.
- B acknowledguje A i w ramach tego wysyła nr ack seq_A + 1. dodatkowo sam wysyła SYN z własnym nr sekwencji.
- A acknowledguje już wysyłając tylko ACK z nr ack = seq_B + 1.
Numery sekwencji dla nowych połączeń mają nieprzewidywalne wartości:
![[ISN.png]]

##### Backlog Połączenia

TCP serwer konstruuje *nasłuchujący socket* który utrzymuje connection backlog - siatkę z danymi połączeń. syscall *listen()* dodaje socketa do backlogu i zaczyna odpowiadać na wiadomości.
![[tcp backlog.png]]

##### Sockety Klienckie
Ustanowione połączenie jest zakolejkowane i może być uzyskane przez *accept()*, który zwraca deskryptor socketa dedykowany poszczególnemu klientowi.

Serwer TCP ma minimum jeden nasłuchujący socket oraz n połączonych klientów. Wszystkie sockety współdzielą lokalny adres. Sockety klientów są identyfikowane przez stack kernela używając 4-tupli (localAddr, localPort, peerAddr, peerPort) obecne w każdym segmencie.


##### Połączenie
Strona próbująca aktywnie się połączyć nazywana jest klientem. Tworzy socket używając SOCK_STREAM i wywołuje connect() do zwrócenia połączenia.
![[Zrzut ekranu 2026-05-1 o 16.15.17.png]]

Syscall ten blokuje dopóki serwer nie odpowie z SYN+ACK segmentem. OS klienta automatycznie odpowiada z ACK i zwraca połączony socket.

Jeśli *connect()* zwraca przedwcześnie (sygnał lub inne przerwanie), proces rozpoczęcia połączenia wciąż trwa w tle.

##### TCP State Diagram
![[tcp state diagram.png]]
status połączenia jest utrzymywany w kernelsace. sieć sama w sobie nie wie o połączeniu.

##### Zamykanie Połączenia![[fin_tcp.png]]
Wywołanie *close()* mówi kernelowi  dwie rzeczy:
- Nie chce już więcej wysyłać.
- Nie obchodzi mnie co remote wciąż wysyła.
*close()* nie blokuje czekając na opróżnienie Tx bufera. Instruuje kernel do flushowania w tle.

Jeśli *close()* jest zawołane z nieskonsumowanymi danymi w Rx buforze, kernel traktuje to jako nieprotokołową terminację. Wyśle segment RST w drugą stronę.

Można użyć *shutdown(fd, SHUT_WR)* do zamknięcia  output stream ale pozostawiając możliwość odbioru danych. 

Standardowe zamknięcie:
*shutdown()* -> read until EOF -> close()

##### Timed Wait State
Strone aktywnie zamykająca połączenie wchodzi w stan TIME_WAIT po teardownie.

Socket pozostaje w tym stanie 2* MSL (Maximum Segment Lifetime = 60 sek w linux).
- jeżeli ostatni ACK jest zgubiony, remote może retransmitować FIN.
- To może zepsuć nowe połączenie używające tego samego portu.
- Powoduje to failing syscalla *bind()* po restarcie

Aplikacje klienckie typowo nie doświadczają tego problemu przez wybór portu przez OS. Należy więc konstruować protokoły aby klient zamykał się pierwszy.

Można użyć SO_REUSEADDR przy szybkich iteracjach przed bindem socketa nasłuchującego

##### Transfer Danych
Niepodobnie do UDP, TCP modeluje dwustronny strumień danych. Syscalle readują i writują lokalne bufory kernela:
![[tcp_send_rcv.png]]

Oba mogą zwrócić 0<x<len jeżeli są puste/pełne. Należy więc do odczytu używać pętli.

- **Protokołowe zakończenie**
	- recv() zwraca 0 po konsumpcji strumienia.
	- send() zwróci sukces, FIN nie oznacza koniec nasłuchu drugiej strony
- **Nagłe zakończenie**
	- recv() i send() zwrócą ECONNRESET
	- jeżeli send() wysłane po RST, triggeruje SIGPIPE.