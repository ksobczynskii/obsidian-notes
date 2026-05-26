Intencja:
Oddziela złożoną strukturę obiektu od jej reprezentacji. Ten sam proces konsrtukcji może tworzyć różne reprezentacje.

Struktura:

![[Zrzut ekranu 2026-05-25 o 12.58.48.png]]

![[Zrzut ekranu 2026-05-25 o 12.59.18.png]]
Przykładowo:

- Builder ~ RoomBuilder. Metody: AddObjects(type, count), Widthen(int), Heighten(int), AddChairs(x),
- Concrete1 ~ MinimalisticRoomBuilder, Heighten(3m), WIdthen(20m), AddObjects(painting, 1), AddChairs(1)
- Concrete2 ~ ExpensiveRoomBuilder, Heighten(7m), Widthen(100m), AddObjects(ExpensivePainting, 5), AddChairs(2).
- Director (Opcjonalny). Może na przykład mieć metody: BuildFullRoom(), BuildRoomNotFinishedYet()...
