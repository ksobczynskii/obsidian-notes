Współdzielone biblioteki i ich położenie nie jest znany w czasie linkowania. Linker musi przygotować binarię dla loadera i zapewnić odpowiednie instrukcje

Linker Generuje ***Global Offset Table***. Jest to sekcja, gdzie mają znaleźć się function pointery w czasie ładowania. Loader następnie może dodać poprawki do tabeli bez dotykania dużego kodu z dużą ilością calli.
![[Zrzut ekranu 2026-06-8 o 12.30.11.png]]

Rozwiązywanie dużej ilości funkcji spowalnia start programu. Dlatego używając ***lazy-initialization*** tworzyony jest ***.got***. Linker generuje małe funkcje-trampoliny w sekcji ***.plt *Procedure Linkage Table)***, które skaczą do funkcji odpowiedniej, jeżeli .got już jest relocated lub do reslovera, jeżeli nie.![[Zrzut ekranu 2026-06-8 o 12.32.56.png]]