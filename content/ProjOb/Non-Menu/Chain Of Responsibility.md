Intencja:
Stworzyć łańcuch operacji na obiekcie, gdzie dany obiekt w łańcuchu stwierdza czy ten obiekt należy do niego i podejmuje decyzje co z nim zrobić. Usuwa potrzebę rozpoznawania wejścia na milion sposobów typu (if(x==1) else if(x==2) ... )

Struktura:
![[Zrzut ekranu 2026-05-25 o 18.33.04.png]]


Przykładowo:
- Handler ~ InputHandler z metoda pass = next.Work(data);
- NumberHandler : InputHandler
- CharHandler:  InputHandler
- OtherHandler : InputHandler

```
var h1 = NumberHandler();
var h2 = CharHandler();
var h3 = OtherHandler();

h1.setNext(h2);
h2.setNext(h3);
------------------------ 



while(input x = read)
	h1.Handle(x);
```


