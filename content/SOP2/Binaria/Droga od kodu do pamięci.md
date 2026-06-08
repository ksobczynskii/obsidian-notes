![[Zrzut ekranu 2026-06-8 o 11.53.53.png]]

Drogę od kodu do pamięci można rozdzielić na 3 etapy, które w jakiś sposób bindują adresy do pamięci (mniej lub bardziej):
- **Kompliacja**: Na tym etapie program decyduje jak zmienne *lokalne* są umieszczane względem siebie (zmienne w funkcjach, nie global, extern itp)
- **Linker** decyduje gdzie trafiają zmienne zdefiniowane przez program (już cały, czyli extern, sam adres funkcji a nie zmiennych wewn. funkcji etc.)
- **Loader** Wsadza program do miejsca w pamięci wraz z innymi ładowalnymi obiektami (biblioteki dynamiczne, moduły etc.)
