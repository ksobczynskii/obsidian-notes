Ostatnim podejściem do problemu jest porzucenie różniących się rozmiarów chunków. Polega na podzieleniu PAS na ustalone odgórnie ramki (np. 4kb)

Logiczny addres space jest podobnie dzielony na ramki.

Logiczny adres jest więc skomponowany z 2 części: numer strony/ramki oraz offset w ramce.
Translacja adresów nie dotyka offsetu. Mapuje jedynie stronę logiczną do fizycznej.

Paging wymaga wewnętrznej fragmentacji. Niektóre mogą nie być wykorzystywane.![[Zrzut ekranu 2026-06-8 o 14.06.56.png]]



#### Page Table
Aby MMU mogło wykonać translację, używa ono Os-maintained per-process ***Page Table***. Jest traktowana jak tablica indeksów, komórka to index ramki.![[Zrzut ekranu 2026-06-8 o 14.10.24.png]]

Page table entries mogą być uznane za niewłaściwe. Próba dostępu poza Page Table skutkuje CPU exception



##### Translaction Lookaside Buffer

Naiwnie zaimplementowany paging wprowadza podwójnie wolniejsze obciążenie dostępu do pamięci, przez Page Table Lookup. Aby to ominąć MMU zawiera TLB (szybka pamięć), które cachuje entries.![[Zrzut ekranu 2026-06-8 o 14.13.13.png]]

#### Memory Protection

Page Table (i TLB) zawierają atrybuty stron.

- Valid bit: jeżeli nie ustawiony to strona nie jest częścią logicznej przestrzeni adresowej. Dostęp do logicznego adresu wewnątrz strony sprawia, że MMU generuje CPU exception 
- Readonly bit: zapobiega write'om
- Executable bit: pozwala brać instrukcje z strony

Używanie bitów wspomaga bezpieczeństwo strony. Przykładowo, stack jest często zmapowany z non-executable pages, eliminując całą klasę ataków typu buffer-overflow


#### Struktury Danych Page Table

Rozważmy 32-bitowy system używający 4KB stron. Każdy proces może mieć 2^20 rekordów w page-table. Większość pagy typowo zawierają niewłaściwe rekordy, chyba że proces rzeczywiście potrzebuje i używa gigabajtów pamięci.

Każdy rekord ma minimum 4 bajty. Page Table każdej strony więc, gdyby przechowywana ciągle w pamięci kernela, zawierałaby max 4MB

Kernel potrzebuje lepszej struktury danych niż zwykły array do sprawnego przechowywania tabeli stron.


##### Hierarchiczne Page Tables

Częstym podejściem jest implementacja owej struktury danych jako drzewko wyszukań. Węzły to tabele, a liście wskazują na ramki.![[Zrzut ekranu 2026-06-8 o 14.30.56.png]]

##### Zhaszowane Page Tables

Dla dużych address spaceów, słownik może być zaimplementowany jako tablica haszująca.

- page number jest zahaszowany, output to index page table
- kazdy rekord w tabeli to linked lista, kazdy node zawiera strone i numery ramek
- podczas translacji MMu musi iść za łańcuchem dopóki nie znajdzie dopasowania![[Zrzut ekranu 2026-06-8 o 14.32.43.png]]
- 
- 
![[Zrzut ekranu 2026-06-8 o 14.33.04.png]]![[Zrzut ekranu 2026-06-8 o 14.33.25.png]]