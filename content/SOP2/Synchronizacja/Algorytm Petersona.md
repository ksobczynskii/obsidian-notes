![[ALGORYTM PETERSONA.png]]
Skutecznia sprawia, że wszystkie 3 wymogi poprawnej synchronizacji są spełnione, ale niestety naiwnie zakodowane w C nie zadziała.


MuTex - działa bo jak turn == me to drugi proces musi czekac (nie moze byc turn =0 && turn =1)

Process - działa z tego samego powodu

Bounded waiting - kolejność wejść to P1 -> P2 ->P1 -> P2 .. bo gdy jeden przestawia flage drugi czeka w while

Algorytm petersona zakłada, atomowość zapisu i odczytu integerów.