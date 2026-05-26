Intencja:
Interfejs do tworzenia obiektów, gdzie konkretne instancje wybierane są w podklasach.

Struktura:
![[Zrzut ekranu 2026-05-25 o 13.06.55.png]]


Przykładowo:
- Factory ~ AnimalCreator.

użycie:
zamiast var x = new Rat()/ new Elephant() ... 
mamy: var x = AnimalCreator.Create(e.Rat)