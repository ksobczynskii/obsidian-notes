Linker odpowiada za sklejanie sekcji wspólnych sekcji z wielu pilków obiektowych razem. Robiąc to, wybiera relatywne obiekty i adresy instrukcji. Linker alokuje przestrzeń adresową (binduje adresy)
![[Zrzut ekranu 2026-06-8 o 12.25.06.png]]
Buduja zagregowaną tabele symboli, opowiadającą gdzie obiekty i funkcje wylądowały.


#### Poprawki Linkera
Następnie Linker podąża za instrukcjami relokacji, dodając poprawki tam, gdzie powinny iść adresy już całego kodu.![[Zrzut ekranu 2026-06-8 o 12.26.26.png]]