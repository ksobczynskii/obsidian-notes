- Pewne aspekty aplikacji nie mogą być łatwo zdekomponowane za pomocą metod na obiektach. Należą do wielu klas, nie jednej.
- Jest to m.in. Synchronizacja, logowaniem , autoryzacja
- Pomocnym może być abstrafikacja tych działań od początku.
Idea:
- Zachowanie przekrawające (pojawiające się w wielu klasach) jest wyciągane do osobnego aspektu.