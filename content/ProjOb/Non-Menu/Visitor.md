Intencja:
Reprezentacja operacji, która ma zostać wywołana na strukturze obiektów. Nowa operacja może być dodana bez zmieniania klasy na której polega.

Struktura:
 ![[Zrzut ekranu 2026-05-25 o 19.20.09.png]]

Przykładowo:
- Zamiast mieć strukturę Weapon i w niej trzymać metody potrzebne do np. usunięcia hp, typu calculateHowMuch(), Remove(), Effects() ... możemy stworzyć:

WeaponVisitor, który ma metodę visit i wykonuje dokładnie to przyjmując jako argument obiekt - Weapon.

W Weapon jedynie AcceptVisitor(v) => v.Visit(this);

i w visitor już logika co jak i gdzie.