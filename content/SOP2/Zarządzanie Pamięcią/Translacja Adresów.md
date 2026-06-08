Wewnątrz poszatkowanego bloku Systemowego RAM, kernal musi umieścić siebie i wszystkie programy użytkownika. Taski te, nie powinny móc mieć dostępu do pamięci innych tasków tak jak i pamięci kernela. Poza tym, nie powinno mieć znaczenia gdzie taski fizycznie leżą.


![[Zrzut ekranu 2026-06-8 o 13.25.59.png]]

CPU Wprowadziło Memory Management Unit (MMU), który tłumaczy logiczne adresy emitowane przez taski na adresy fizyczne. Kernel kontroluje proces translacji przez rejestru MMU.

##### Ciągła alokacja

Najprostszym podejściem byłoby używać alokacji ciągłej. Każdy task dostaje osobny chunk fizycznego RAMU. MMU w tym systemie wygląda prosto:![[Zrzut ekranu 2026-06-8 o 13.27.40.png]]

#### Wybór odpowiedniego miejsca

Taski powstają i umierają dynamicznie, pozostawiając dziury o różnych rozmiarach. OS allocator wybiera dziurę w jakiś sposób, zazwyczaj best-fit, first-fit. ![[Zrzut ekranu 2026-06-8 o 13.32.00.png]]


Kernel trzyma informacje na temat kadego taska trwającego w strukturce opisu tasków. Iteruje po TCB szukając odpowiedniej dziury.