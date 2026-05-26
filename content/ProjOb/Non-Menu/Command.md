Intencja: 
	Operacja jest zenkapsulowana w obiekcie, który może ją manipulować przed wykonaniem (zakolejkować, zwalidować, ...)


Struktura:
![[Zrzut ekranu 2026-05-25 o 18.38.21.png]]


Przykładowo: 
- ICommand z metodą Execute();
- MoveCommand(player, int fields, string direction) : ICommand

```

Player p = ...;

Zamiast:
if(logika...)
...
p.Move(10,"up");


Mamy:

var mc = new MoveCommand(p, 10, "up");
mc.Execute();


-------------------- 
Execute:

if(somebodyMovingThere)
	enqueue(Move);
... reszta logiki
```

