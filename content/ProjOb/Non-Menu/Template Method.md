Intencja: 
Częściowa implementacja algorytmu jest zdefiniowana, a niektóre części są zaimplementowane w podklasach. Części alg. można zmieniać bez naruszania struktury.

Struktura:

![[Zrzut ekranu 2026-05-25 o 19.12.29.png]]



Przykładowo: 
- ScorePredictor(game) ~ klasa abstrakcyjna
- Predictor1 : ScorePredictor
- Predictor2: ScorePredictor


```

ScorePredictor:

public void DisplayGameData(GameData g) 
{
	// konkretna implementacja
}

public RetrievePreviousGames(GameData g){
	// konkret
}

public abstract CalculateStats(AllGamesData agd);
public abstract UsePredicitonModels(Stats s);
public Predict(GameData g){
	DisplayGameData(g);
	var all = RetrievePreviousGames(g);
	var stats = CalculateStats(all);
	UsePredicitonModels(stats);
}





---------------------------- 
Predictor1: ScorePredictor


public abstract CalculateStats(AllGamesData agd)
{
	MonteCarlo(agd);
	... cos innego
}
public abstract UsePredicitonModels(Stats s)
{
	KNN(s);
}


----------------------------- 

Predictor2: ScorePredictor


public abstract CalculateStats(AllGamesData agd)
{
	SamplingMethod(agd)
	... cos innego
}
public abstract UsePredicitonModels(Stats s)
{
	SVM(s);
}
```

