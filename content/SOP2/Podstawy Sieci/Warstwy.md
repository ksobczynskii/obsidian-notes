**L5, L6, L7**  - Aplikacja tworzy opcjonalne payloady i używa syscalli do przesyłu do warstwy transportu.

**L4 Transport** (Np. TCP) - Rozpatruje w jaki sposób dane będą przesyłane, dokleja headery mówiące o tym jaka aplikacja ma otrzymać dane. Przesyła do L3

**L3 Network** (Np. IP) - Rozdrabnia dane na pakiety, zajmuje się adresowaniem i szukaniem routingu. Zajmuje się też dostarczeniem danych do hosta wewnątrz sieci. Prependuje L3 header i wysyła do L2.

**L2 Data Link** (Ethernet) - Owija pakiety w "frames" które mogą zostać wysłane w fizycznej sieci do urządzenia podłączonego do tej samej sieci. Zajmuje się adresowaniem urządzeń, medium transmisyjnego i wykrywaniem errorów. Wysyła w L1 Frame poprzez medium.