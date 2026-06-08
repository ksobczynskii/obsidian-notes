Najprostszy model serwera TCP. Odpowiada jednemu klientowi na raz wewnątrz pojedynczego wątku.![[Zrzut ekranu 2026-06-7 o 10.59.19.png]]

Oczywistą wadą jest kompletny brak współbieżności.


#### Problem Blokowania
W iteracyjnym serwerze funkcja opisana wyżej jako *handle_client()* zazwyczaj zawiera blokujące I/O (*read/write*).
Jeżeli klient jest wolny lub nie wysyła danych, blokuje cały serwer. Mogą zdarzyć się przykładowo:
- długotrwałe I/O bound requesty
- CPU intensive requesty
- powolne odbieranie danych przez klienta
- powolne wysyłanie danych (*the slowloris attack*) 
