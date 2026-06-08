Przez C10k problem, świat odszedł od poprzednich implementacji do architektur sterowanych zdarzeniami, za pomocą *epoll()* 

Zamiast "Jeden wątek na klienta" chcemy "Jeden wątek dla wielu klientów"
![[Zrzut ekranu 2026-06-7 o 11.31.58.png]]

Używanie Epolla pozbywa się dwóch problemów: pamięć i CS.

- context switch pomiędzy klientami obsługuje epoll - nie kernel
- jeden stos na wszystkich.


#### Rozwiązanie nr. 1 - Współdzielony EPOLL

Korzysta z EPOLLET | EPOLLONESHOT. Edge-triggered mode sprawia, że dostaniemy eventy tylko podczas zmiany stanu. Każda zmiana jest wysylana do jednego wątku wybranego przez kernel.

One-shot sprawia, że deskryptor będzie zblokowany. Jest to potrzebne, aby nie wysyłać dwóch chunków danych jednego streama/klienta do innych wątków. po obsłudze streama odblokowywujemy fd.

Ten schemat działa dobrze dla już połączonych socketów. Nie skaluje się jednak za dobrze z *accept()*. Nie możemy akceptować, gdy mamy zdisarmowany socket (kolejka akceptów).


#### Rozwiązanie nr. 2 - Prywatne EPOLL-e

Każdy Thread ma prywatny epoll. Dedykowany thread akceptujący przypisuje zaakceptowany wątek jednemu z threadówvia *Round-robin* i poprzez *epoll_ctl_add()* ![[Zrzut ekranu 2026-06-7 o 11.38.54.png]]

##### Skalowanie accept
Akceptowanie tysięcy połączeń na sekunde jest trudne. Jeden akcepter z backlogiem to bottleneck.

Współczesne SO_REUSEPORT sprawia, że możemy mieć wiele nasłuchujących socketów na tym samym porcie. Każdy thread może mieć własny accept backlog dla tego samego portu.![[Zrzut ekranu 2026-06-7 o 11.41.23.png]]

##### Event Loop Structure
O ile epoll rozwiązuje problemy z performancem, stwarza problem dla programistów.

Epoll based event loop to duża monolityczna struktura z wielkim if/switch blockiem, wybierająca odpowiedni even handling na podstawie nadchodzącego eventu.
![[Zrzut ekranu 2026-06-7 o 11.42.59.png]]


##### Wzorzec Reactor
Jest to design oparty na zasadzie Inversion of Control.
1. **Event Demultiplecer** OS-level mechanizm, który czeka na eventy
2. **Reactor/Dispatcher** - Nieskończony event-loop, czeka na epoll_wait -> wybiera ztriggerowane eventy i je routuje
3. **Handlery** maszyny stanów na poziomie aplikacji. Zajmują się nieblokującym I/O![[Zrzut ekranu 2026-06-7 o 11.46.08.png]]


##### State Machines Problem

Jeden wątek multiplexuje wiele niezależnych flow klientów![[Zrzut ekranu 2026-06-7 o 11.49.24.png]]

Jest to rozwiązane w wzorcu:

![[Zrzut ekranu 2026-06-7 o 11.49.39.png]]

##### Suspendable functions

State Machine rozwiązuje problem niezdolności do zawieszenia funkcji, gdzie potrzebne jest I/O
![[Zrzut ekranu 2026-06-7 o 11.51.07.png]]

##### Korutyny
w kontraście do normalnych funkcji które są wywoływane i zwracają wartość, korutyny są tworzone, wznawiane suspendowane i wychodzą.![[Zrzut ekranu 2026-06-7 o 11.52.40.png]]
*co_await* - funkcja zawieszana i zwraca do callera coś. 
Stan korutyn nie może być trzymany na stacku threada, który mógłby być używany przez inne korutyny podczas zatrzymywania kodu. Ramki korutyn znajdują się na heapie.



##### Zero-Copy Solutions
Serwery spędzają dużó czasu kopiując bufor z kernelspace lub do niego.

*io_uring* eliminuje double copy problem. Dobrze współdziała z *epoll()*

Są osobne syscalle stworzone, by poradzić sobie z problemem copying overhead: 
sendfile(), splice().