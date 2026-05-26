Intencja: 
Stworzenie nowego obiektu to stworzenie generycznego prototypu. Nowe obiekty tworzone są przez generyczne prototypy

![[Zrzut ekranu 2026-05-25 o 13.17.00.png]]


Przykładowo:
- Prototyp ~ AnimalPrototype()
Użycie:
```
var aProt = new Cat("mruczek", 10, ...);
var cat1 = aProt.Clone();
...
```

Cel: Nie musimy wielokrotnie wywoływać konstruktorów z powtarzającymi się danymi.