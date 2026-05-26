Intencja:
Oddzielenie abstrakcji od implementacji aby oba mogły być zmieniane niezależnie

Struktura:

![[Zrzut ekranu 2026-05-25 o 17.55.17.png]]

Przykład:
- RefinedAbstraction ~ IDevice z metodami turnOn i turnOff
- ConcreteImplementor ~ Tv implementujace IDevice, Radio implementujace IDevice
- Abstraction ~ Remote z polem typu IDevice i metodami turnOn i turnOff.

Gdy chcemy za pomocą remote włączyć device, robimy:
```
var remote = new Remote(concreteDevice);
remote.turnOn();
```
gdzie:
```
public void turnOn()
{
	_device.turnOn();
}
```

w ten sposób tworzymy sobie jakieś device i implementujemy jak działa oraz abstrakcyjne remote które robi co chce i wywołuje akcje device. Jedno po drugim nie dziedziczy i są niezależne.


