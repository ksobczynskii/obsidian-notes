

Idea:

Każda klasa powinna mieć dokładnie jedną rolę w programie.

Cele:
- Klasa ma mieć jeden możliwy powód do bycia zmienioną
- Modularność
- Modyfikacje są łatwiejsze
- Nazwa Klasy === Rola

Przykłady:
Obiekt z dwoma rolami:

```
class Book:
	
	info getInfo();
	...
	
	void save(string file);
```

Jedna rola:

```
class Book:

	info getInfo();
	...

class FileSaver:
	void SaveBook(Book b);

```

