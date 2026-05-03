Inaczej Bounded Buffer Problem.

Problem polega na tym, że:
Producent chce wysłać dane do konsumentów poprzez współdzielony bufor o rozmiarze *N*.
![[BoundedBuffer.png]]

Ten może być pusty lub pełny. To musi być rozpatrzone i odpowiednio pokierowane dalej.

Implementujemy bufor jako **Circular Buffer**:
![[Circular Buffer.png]]

Problem przesyłania danych przez bufor można rozwiązać używając semaforów, gdyż te wewnętrznie zliczają zasoby. Użyjemy:
1. mutex - semafor z inicjalizacją = 1.
2. empty_sem - inicjalizacja na N, zlicza wolne sloty.
3. full_sem - inicializacja na 0, zlicza nieprzeczytane wartości.

Wtedy:
![[bbp-sem-sol.png]]
