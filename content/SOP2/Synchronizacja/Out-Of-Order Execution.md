CPU może przearanżować linijki kodu jak chce (nawet już kodu maszynowego), jeżeli jednowątkowe wykonanie programu ma to samo działanie dla każdego z tych przearanżowań.

Przykład:

![[OOOE.png]]


Z tego powodu dostawcy hardware'u zmuszeni byli wyjaśnić ichniejszy model działania pamięci i czego programista może się spodziewać. Przykładowo:
- [[TSO - Total Store Order]] 
- [[Weak Memory Model]] 

Aby zaimplementować algorytmu opierające się na kolejności działań na pamięci należy użyć specjalnych instrukcji (bariera / fence):
![[mfence.png]]