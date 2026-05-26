LSP i assertions nieco są sprzeczne ze sobą, gdyż 
- invariant i postcondition nie mogą być posłabiane względem klasy super. ( Nie może wymagać mniej, bo wywołanie z klasy bazowej failuje)
- precondition może być osłabiane, ale nie polepszane (nie może wymagać więcej, bo wywołanie z klasy bazowej zfailuje)