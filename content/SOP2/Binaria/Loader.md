#### Jak Loader widzi ELF
Główną robotą Loadera jest wsadzić elementy ELF do pamięci. To jest osiągane przez ***mmap()*** istotne elementy pliku ELF to addres space'a. Nie obchodzi go znaczenie sekcji/symboli, interesuje go jedynie rozmiar, alignment i zabezpieczenia (RWX) mapowanego regionu. 

Ładowalny plik ELF definiuje segmenty wraz z sekcjami, które służą za wgląd loadera do zawartości pliku:![[Zrzut ekranu 2026-06-8 o 12.35.35.png]]![[Zrzut ekranu 2026-06-8 o 12.35.42.png]]

writable ma większy size przez sekcję .bss.


#### ASLR
Address Space Layout Randomization to sposób wkładania pliku do pamięci. Dzięki kodowi posiiton-independent, kernel może mapować binarię na dowolny adres. Wybiera go losowo poprzez ASLR base address, dzięki któremu program ładuje się w inny miejsce za każdym razem![[Zrzut ekranu 2026-06-8 o 12.38.00.png]]
Pojedynczy LOAD segment z GOT i RW jest dzielona na ostatnie 2 mappingi. To się dzieje dzięki loaderowi i wywołaniu mprotect() po zapełnieniu .got, zapewniając, że program nie nadpisze adresów pamięci.


##### Dynamiczny Loader

Loader sam w sobie jest typu 'DYN' ELF userspace program. Zlinkowana binarka pointuje do loadera z ścieżką w sekcji ***.interp***
![[Zrzut ekranu 2026-06-8 o 12.41.20.png]]

sekcja ***.dynamic*** zawiera instrukcje dla loadera jak:
- tu są realokacje, (.rela.dyn), proszę zajmij się nimi
- tu jest .got.plt, uzupełnij go
- tu są zainicjalizowane rutyny, które musisz odpalić (.init_array)

Loader sam w sobie jest załadowany na niezależny adres ALSR od programu. OD mówi loaderowi, gdzie został umieszczony i gdzie jest program przez wektor pomocniczy, położony na stacku, przed wywołaniem loadera.


#### Proces execute
Handling syscalla execve(), czyli wykonania pliku binarnego, wygląda następująco:
1. Cleanup - czyszczenie mappingów pamięci
2. wybór ALSR dla programu, bibliotek, stosu, ...
3. parsuje ELF headery i mapuje ładowalne segmenty do pamięci
4. czyta .interp sekcje zawierającą ścieżkę do loadera
5. mapuje loader (ld-linux-arch.so)
6. mapuje anonimowy prywatny stos jako segment pamięci.
7. umieszcza argc, argv i envp na stosie
8. umieszcza wektor pomocniczy załadowany parametrami na stosie: 
	-  `AT_BASE`: `0x7f6a62062000` (library base)
	- `AT_ENTRY`: `0x5606657f3040` (program base)
	- `AT_PHDR`: `0x5606657f2040` (program headers)
9. Oddaje kontrole do entrypointu loadera.

#### Robota loadera:
Loader zaczyna samorelokację wiedząc, gdzie został umieszczony (AT_BASE)

Loader czyta adresy zmapowane w AT_PHDR i znajduje segmentu typu dynamiczny (.dynamic)
zawierający instrukcje loadingu:
1. biblioteki typu **NEEDED** są załadowane, drzewko zależności zmapowane i rekursywnie zainicjalizowane
2. Relokacje typu **RELA** są wywołane, uzupełniając .got
3. relokacje **JMPREL** są wywołane (if **BIND NOW**)
4. specjalne **PLTGOT** są tworzone
5. **INIT_ARRAY** functions są wywoływane i inicjalizują dzrewko od dołu do góry

Na końcu loader skacze do AT_ENTRY oddając kontrolę programowi.


##### Runtime Library Loading

Proces może explicite zawołać loadera funkcją z <dlfcn.h>:
![[Zrzut ekranu 2026-06-8 o 12.52.18.png]]

to dynamicznie mapuje nowy shared object do adres space i pozwala na runtime symbol resolution.