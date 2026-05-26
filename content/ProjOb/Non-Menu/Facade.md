Intencja:
Wysokopoziomowa fasada ułatwiająca dostęp do skomplikowanego podsystemu za pomocą ułatwiającej to klasy.

struktura:
![[Zrzut ekranu 2026-05-25 o 18.18.10.png]]

Przykładowo:
Zamiast Metody próbującej łączyć się z jakimś endpointem i wywoływanie wielu metod typu:


connector.sendRequest(string);
receiver.getResponse();
checker.checkValidity(resp);
...

Masz Fasadę: 
```
ConnectionManager

public Connect(string where)
{
	connector.sendRequest(where);
	receiver.getResponse();
	checker.checkValidity(resp);
}

```


Przez co wystarczy wywołać jedną metodę enkapsulującą wszystko.

