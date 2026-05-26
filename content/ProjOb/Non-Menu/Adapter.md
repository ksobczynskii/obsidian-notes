
Intencja:
Stworzyć interakcje dla dwóch niekompatybilnych klas

Struktura:
![[Zrzut ekranu 2026-05-25 o 17.10.25.png]]

Przykładowo:
- Klasa Loger ~ Target
- FileWriter ~ Adaptee

Tworzymy Adapter:
- Może on dziedziczyć lub mieć instancje klas.
- Wywołując Log chcemy też zapisać do pliku. Robimy więc przykładowo: 


```
class FileLoggerAdapter : IGameLogger
{
    private readonly FileWriter _fileWriter;
    public FileLoggerAdapter(FileWriter fileWriter)
    {
        _fileWriter = fileWriter;
    }
    public void Log(string message)
    {
        _fileWriter.WriteLineToFile(message);
    }
}
```

