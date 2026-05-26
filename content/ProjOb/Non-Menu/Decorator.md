Intencja
Dodanie możliwości dynamicznego rozszerzania działania obiektu. Elastyczna alternatywa dziedziczenia.

Struktura:
![[Zrzut ekranu 2026-05-25 o 18.13.08.png]]


Przykładowo:
- Bazowa klasa Weapon.
- Konkretna klasa Sword : Weapon.
- Decorator dziedziczący po Weapon, np. MagicWeapon.

Wtedy Decorator zawiera w środku instancję weapon i zoverridowane metody z klasy bazowej wywołuje w taki sposób, że wywołuje ją na instancji wewnątrz i dodaje coś swojego. Przykładowo:

```
Weapon

public abstract string GetName()

-----------------------


Sword : Weapon

public override string GetName => "Sword";


------------------------

MagicWeapon

Weapon w;

public override string GetName()
{
	return "Magical " + w.GetName();
}
```

