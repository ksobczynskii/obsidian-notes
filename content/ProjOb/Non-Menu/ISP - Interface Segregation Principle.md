

Idea:
Wiele client-specific interfejsów są lepsze niż jeden o generalnym użytku.


Cele:
- Klasy implementują to co muszą. Nie mają dostępu do dziwnych funkcji które akurat dla tej konkretnej klasy nie powinny być dostępne:

![[Zrzut ekranu 2026-05-25 o 19.42.54.png]]
przykładowo, nie chcemy: 

```
Class Animal:
	void Walk();
	void Eat();
	...
	

Class Fish:
	override Walk => NotImplementedException();
```

