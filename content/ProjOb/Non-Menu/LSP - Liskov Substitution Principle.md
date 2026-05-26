

Idea:
Podklasy powinny być zamienialne za klasę bazową


Cele:
- Możemy użyć klasy niżej w hierarchii, gdzie klasa najwyżej może być użyta
- użytkownicy, którzy korzystali z klas wyższych, mogą kontynuować używając podklas

zgodność z LSP: 

```
class Point
	double x,y;
	
class Rectangle : Point
	double a;

void FunkcjaKlienta(Point p)


void InnaFunkcja()
{
	Rectangle r = new Rectangle();
	FunkcjaKlienta(r); // musi działać
}
```


Problemy: 

Podklasa może chcieć modyfikować funkcję nadklasy: 
![[Zrzut ekranu 2026-05-25 o 19.40.01.png]]