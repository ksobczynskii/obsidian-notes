Intencja:

Definicja Gramatyki jakiegoś języka/ formuły.


Struktura:

![[Zrzut ekranu 2026-05-25 o 18.46.35.png]]

Przykład:
- IExpression ~ interfejs definiujący Interpret()
- MoveCommandInterpreter : IExpression
- HTTPErrorMessageInterpreter: IExpression

```
MoveCommandInterpreter:

Interpret(string s)
{
	ifs[..2] "up" ... 
	...
}

------------------------- 
HTTPErrorMessageInterpreter

Interpret(string s)
{
	if s[0] == '4' => Error processing ...
	...
}

```

