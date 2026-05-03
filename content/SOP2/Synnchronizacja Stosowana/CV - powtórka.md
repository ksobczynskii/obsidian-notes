Zmienne warunkowe nie mają stanu, w przeciwieństwie do semaforów. Z perspektywy wywołującego, wait() na cv działa następująco:

- odblokuj mutex
- śpij w cv queue
- odzyskaj mutex po wybudzeniu
- obudź wywołującego

Bounded Buffer Problem można rozwiązać poprzez cv:
![[cv-bbp.png]]