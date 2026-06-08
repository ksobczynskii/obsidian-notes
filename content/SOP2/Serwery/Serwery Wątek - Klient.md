Stare podejście do obsługi wielu klientów. Aby zatrzymać iteracyjne blokowanie, tworzymy nowy wątek za każdym wywołaniem *accept()*.![[Zrzut ekranu 2026-06-7 o 11.27.21.png]]


##### Problemy takiego podejścia
Czy tworzenie. 10k wątków dla 10k klientów to dobry pomysł?

- ***Pamięć*** - Każdy wątek musi mieć stos (2-8 MB). 10k wątków ~ 20-80GB RAM-u na same stosu
- ***Context Switching*** - Scheduler musi rozporządzać tysiącami wątków. CPU spędza więcej czasu na zmianę tasków niż prawdziwą pracę.

Ten problem to C10k Problem.
