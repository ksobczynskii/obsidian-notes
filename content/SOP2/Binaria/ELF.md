#### Executable Linkable Format

W skrócie ELF. Jest to standardowy format pliku Linux stworzony do przechowywania wielu binarii. Header wyznacza dokładniejszy typ pliku![[Zrzut ekranu 2026-06-8 o 12.05.58.png]]
Każdy ELF może mieć wiele overlappujących sekcji i segmentów.
- Sekcje są nazwanymi częściami pliku konsumowanymi przez linker
- Segmenty są regionami pliku ładowane do pamięci przez loader

##### Relocatables
Pliki obiektowe z kompilatora mają typ ***Relocatable*** i zawierają jedynie sekcje. Każda sekcja ma nazwę, typ, rozmiar i offset wewn. pliku.![[Zrzut ekranu 2026-06-8 o 12.08.19.png]]
##### Dane
W szczególności interesuję nas sekcja **Danych**. Zdefiniowane i zainicjalizowane obiekty globalne są umieszczane w sekcji ***.data***, a niezainicjalizowane w ***.bss***. Stałe znajdują się w ***.rodata***
Rozmiar każdego z nich jest równy zsumowanemu rozmiarowi wszystkich zawartych wewn. obiektów. Patrząc na zawartość sekcji już można stwierdzić co jest czym:
![[Zrzut ekranu 2026-06-8 o 12.11.08.png]]

sekcja ***.bss*** nie jest przechowywana fizycznie (optymalizacja disk-space).

##### Kod
Kolejną ciekawą sekcją jest sekcja ***.text***. W niej znajdują się skompilowane funkcję, zkonkatenowane jedna po drugiej: ![[Zrzut ekranu 2026-06-8 o 12.12.32.png]]

##### Symbol Tables

Aby linker mógł szukać obiektów i funkcji po nazwach, istnieje dedykowana sekcja ***.symtab***, wygenerowana przez kompilator

![[Zrzut ekranu 2026-06-8 o 12.15.07.png]]


##### Sekcja Tabel Relokacji
Wygenerowany kod potrzebuje móc później wprowadzać zmiany. Relatywne układanie kodu i sekcji danych jest nieznane. Lokalizacja obiektów zewnętrznych również jest nieznana.![[Zrzut ekranu 2026-06-8 o 12.19.43.png]]
Relokacje są złożonymi instrukcjami przez kompilator dla linkera. Przykładowo, pierwsza z nich mówi: Włoż do .text na offsecie 001a ostatni adres symbolu a - 4 - 001a