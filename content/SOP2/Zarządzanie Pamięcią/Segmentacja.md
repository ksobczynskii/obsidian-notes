Późniejsze próby traktowania logicznego adresu pamięci jako zbiór niezależnych logicznych chunków zwanych segmentami to miała być odpowiedź na problem fragmentacji przy podejściu ciągłym.![[Zrzut ekranu 2026-06-8 o 13.36.07.png]]

#### Segmentacja w MMU
System zawiera i monitoruje informacje o layoucie segmentów każdego taska wewnątrz tabeli segmentów. Logiczny adres to tuple (segment; offset). MMU weryfikuje offset i dodaje segment base do wykalkulowania adresu fizycznego:
![[Zrzut ekranu 2026-06-8 o 13.37.51.png]]

#### Segmentacja w 8086

Intel 8086 to był 16-bitowy procesor w 20-bitową magistralą. Aby mieć dostęp do więcej niż 64K pamięci, rdzeń używał dedykowanego rejestru segmentu, tj:
- CS (Code Segment)
- DS (Data Segment)
- SS (Stack Segment)
- ES (Extra Segment)

rdzeń tłumaczył logiczny adres 16-bitowy używając offsetu segmentu:
![[Zrzut ekranu 2026-06-8 o 13.45.51.png]]
To pozwalało na łatwą relokację programów i rozszerzyło adresowalną przestrzeń, ale nie dawało żadnych zabezpieczeń (sprawdzenia dostępu).


#### Segmentacja w 80386

Nowszy procesor wprowadził tryb protected. Rejestry Segmentów (CS,DS,SS) zamiast prostych offsetów stały się ***selectorami*** - indexami w Globalnej Tabeli Deskryptorów lub Lokalnej Tabeli Deskryptorów.

Selectory były 16-bitowa i zawierały. index (13n), flagi GDT/LDT (1b) i Requested Privelage Level (2b), który był determinowany przez code segment.

LDT opisywało segmenty procesów prywatnych, GDT - globalnych. OS zmieniał jedynie LDT pointer podczas context switcha. Entries w obu tabelach są 8 bajtowymi wartościami i zawierają offset segmentu i limit, Descriptor Privelage Level oraz dozwolone operacje (rwx)

Procesor był wciąż 16-bitową maszyną. Program musiał manipulować rejestrami segmentów aby adresować więcej ni 64K pamięci. Store do rejestru segmentu podlegał weryfikacji (RPL, DTL, CPL)![[Zrzut ekranu 2026-06-8 o 13.52.56.png]]

Wady:
- 64kB - limit na ciągłą alokację, nie można mieć większych arrayów.
- Segment switch overhead - zmienianie segmentów za pomocą instrukcji ma zawiłe walidacje
- Zewnętrzna fragmentacjia: długość zmiennych segmentów wciąż cierpi na fragmentacje jak podejście ciągłe
- Zawiły model pamięci: programy muszą być świadome segmentowanej pamięc i docierać do pamięci w różny sposób w zależności czy potrzebują dostać się do innego rejestru![[Zrzut ekranu 2026-06-8 o 13.59.55.png]]