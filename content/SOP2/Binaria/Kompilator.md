
Wywołanie kompilatora generuje pojedynczy ***plik obiektowy*** (.o) z pojedynczej ***jednostki translacji*** (zazwyczaj plik + headery).
Każdy taki unit zawiera wiele 'rezydentów pamięci': zmienne, funkcje, ...
![[Zrzut ekranu 2026-06-8 o 12.02.37.png]]

Plik obiektowe mogą odwoływać się do obiektów i funkcji z innym jednostek translacji (na ten moment bez wiedzy o ich relatywnym adresie). 

Skompilowany plik nie ma pojęcia gdzie on i inni wylądują w pamięci.