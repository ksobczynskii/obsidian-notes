Intencja:
Zapewnienie jednej instancji obiektu w projekcie

Struktura:
![[Zrzut ekranu 2026-05-25 o 13.21.05.png]]

Przykład:
- Logger ~ singleton.
Użycie:
```
var logger = Logger.Instance.Log(); // Mamy pewność że to ta dbrajedyna instancja logująca dane gdzie chcemy. Inaczej podczas tworzenia loggera za każdym razem musielibyśmy dawać mu info dokad ma logować dane plus dodatkowo musiałby powstać sposób komunikacji między loggerami aby wiedzieć gdzie wolno pisać
```

