Intencja:
Implementacja relacji jeden-do-wielu. Kiedy obiekt zmienia stan, pozostałe połączone obiekty są o tym informowane / stan jest zmieniany.

Struktura:
![[Zrzut ekranu 2026-05-25 o 19.06.38.png]]


Przykładowo:
- IObserver ~ Interfejs z metodą: onGoal(dane), onAssist(dane)... , oraz listą subskrybentów
- BettingStudio : IObserver. Metoda 


```
var bs1 = new BettingStudio("MGM Bets");
var bs2 = new BettingStudio("STS");
var bs3 = new BettingStudio("Betclic");

Game g = new Game("LPO", "WIS");

g.Subscribe(bs1);
g.Subscribe(bs2);
g.Subscribe(bs3);



----------------------------- 

Game: 

List<IObserver> subscribers;

void Subscribe(IObserver o) => subscribers.Add(o);

void ScoreGoal(data)
{
	foreach(var s in subscribers)
		onGoal(data);
}

```

