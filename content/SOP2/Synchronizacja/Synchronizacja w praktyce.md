Rozwiązanie problemu współbieżnego dostępu do pamięci samo w sobie dotyka współdzielonej pamięci!

Rozwiązanie to komunikacja międzyrdzeniowa poprzez RAM
![[INTER CPU Communication.png]]



#### Dlaczego stare założenia pozwalały nam myśleć o poprawności Petersona? Bo zakładaliśmy, że:
- Kod jest 1:1 zamieniany na kod maszynowy, zachowując kolejność operacji - [[Proces Kompilacji]] 
- Read/Write na integerze jest atomowy - [[Atomowość zmian]] 
- Zmiany w pamięci są konsekwentne - rdzeń wpisał a a później b, to inni powinni mieć możliwość zauważenia tych zmian w tej dokładnie kolejności - [[Out-Of-Order Execution]] 

Oczywiście nic z powyższych nie zachodzi na współczesnych komputerach.

Jednym ze standardów przybliżających nas do stwierdzenia, że kod jest poprawnie zaimplementowany do synchronicznego użytku jest [[Litmus Test]].





