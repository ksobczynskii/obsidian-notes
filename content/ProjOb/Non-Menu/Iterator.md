Intencja:
Możliwość iteracji po kolekcji w jakimś obiekcie bez podawania struktury wewnętrznej

Struktura:
![[Zrzut ekranu 2026-05-25 o 19.00.58.png]]

Przykładowo:
- BankAccount ~ Klasa zawierająca transakcje. Nie chcemy aby lista transakcji była publicznie brana na raz z dowolnej klasy, a dodatkowo transakcje są rozmieszczone po rożnych listach i strukturach

```

BankAccount

List<Transactions> ts;
int cur; 

public TransacitonInfo Next()
{
	return new TransactionInfo(ts[cur++], ts[cur-1]/ts.Sum(), ts.GetTax(info));
}



----------------------- 
Struct TransactionInfo
{
	Transaction t;
	double percentageOfAll;
	double tax;
}
```

