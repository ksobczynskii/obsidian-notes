Netcat (*nc*) to wszechstronne narzędzie do czytania danych z sieci i wyrzucania do stdout. 
Potrafi też czytać z stdin i wyrzucać do sieci
![[nc_modes.png]]

Gdy klient netcata się wykonuje, musi użyć syscalla do powiedzenia hostowi OS, że chce się gdzieś połączyć. 

Jako odpowiedź OS generuje pakiety do wysłania na proces serwera, który pasywnie czeka na nadchodzące połączenia.

OS musi wysłać ten pakiet przez odpowiedni IF![[nc_usage.png]]