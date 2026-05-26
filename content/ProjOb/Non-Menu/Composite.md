Intencja:
Skomponowanie obiektów jako struktury drzewiaste. Klient może traktować każdy Leaf tak samo.

Struktura:

![[Zrzut ekranu 2026-05-25 o 18.03.47.png]]
Przykład:

- Component ~ FileSystemElement()
- Elem1~ File
- Elem2 ~ Folder

```
File : FileSystemElement
string name;
public void show()
{
	print(name);
}
```

```
Folder : FileSystemElement
string name;
List<FileSystemElement> elems;
public void show()
{
	print(name);
	for( e in elems)
		e.show();
}
```

Teraz klient nie wiedząc z czego składa się Component, może wywołac funkcję spodziewając się poprawnego działania dla Komponentu lub jeżeli to zbiór Komponentów - każdego z nich.![[Zrzut ekranu 2026-05-25 o 18.08.32.png]]


Tu klient wywołując show może liczyć na pokazanie zarówno podzdjęcia jak i linii.

