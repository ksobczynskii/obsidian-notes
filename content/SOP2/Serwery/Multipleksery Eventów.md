Jest to mechanika sterowania powiadomieniami.

Pierwszym API multiplexującym był *select()*. Używa on bitmaski do reprezentowania zestawu file descriptorów.
![[Zrzut ekranu 2026-06-7 o 11.07.24.png]]

Wady:
- limit FD_SETSIZE = 1024
- O(N) za każdym razem gdy chociaż jeden z deskryptorów zwróci.
- Bezstanowy - kernel nie pamięta zestawu, musisz stworzyć bitmaskę na nowo za każdym razem.


#### Poll()
Aby rozwiązać niektóre wady *select()* stworzono syscall *poll()*
![[Zrzut ekranu 2026-06-7 o 11.09.21.png]]

- Brak limitu 1024 FD
- Niestety zostaje O(N)

#### Epoll()
Współczesne, dopracowane rozwiązanie. Zawiera **Stan** i jest **event-triggered** 
Instancja Epolla to obiekt na poziomie OS-a zawierający dwie listy:
- **Interest List** - Monitorowane FD (Drzewo Czerwono Czarne)
- **Ready List** - Ztriggerowane FD (Dwukierunkowa lista)

Tworzymy epoll i manipulujemy nim poprzez następujący syscalle:
- *epoll_create()* - zwraca instancje epolla
- *epoll_ctl()* - Dodaj/Usuń/Zmień FD z listy Interest List
- *epoll_wait()* - Zkonsumuj eventy z listy Ready List

Gdy wywołany jest epoll_wait(), kernel nie szuka niczego, tylko sprawdza czy Ready List jest pusta. Jeżeli nie, kopiuje jej zawartość do User-Space. 



##### Reprezentacja Eventów 
![[Zrzut ekranu 2026-06-7 o 11.14.45.png]]
- **events** - odpowiada za to jakie eventy mają przychodzić
- **data** - aplication-specific context, często po prostu czytamy z fd co przyszło w prostych aplikacjach.


##### Typy eventów
- EPOLLIN - Read ready
- EPOLLOUT - Write ready
- EPOLLRDHUP - Zamknięty peer
- EPOLLPRI - Priorytetowe dane
- EPOLLERR - nastąpił błąd (np. RST) *
- EPOLLHUP - niestandardowy koniec *
można łączyć ze sobą eventy, np. EPOLLIN | EPOLLOUT. 
Eventy z * są monitorowane automatycznie.


##### Jak Odbierać Eventy?
Aplikacja może podać pomocnicze flagi do *epoll_ctl()* aby powiedzieć OS-owi kiedy i jak odbierać eventy.

- **EPOLLET** - zmienia zachowanie z defaultowego *level-triggered* na *edge-triggered*. Event będzie wygenerowany jedynie, gdy zmieni się stan.
- **EPOLLONESHOT** - Automatycznie blokuje deskryptor gdy znajduje się w Ready-List. po obsłudze można zwrócić go do interest-list za pomocą EPOLL_CTL_MOD
- **EPOLLEXCLUSIVE** - budzi max jednego callera *epoll_wait()* gdy przyjdzie wiele na raz.