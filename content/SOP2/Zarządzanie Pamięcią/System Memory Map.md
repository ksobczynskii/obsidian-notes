OS zarządza fizyczną przestrzenią adresową (PAS). Musi determinować gdzie umieścić każdy program oraz gdzie umieścić samego siebie. Można sobie wyobrazić PAS jako duży, ciągły blok pamięci rozpinający się od 0 do rozmiaru chipu RAM. Jednak prawda jest dużo bardziej skomplikowana.

/proc/iomem:
![[Zrzut ekranu 2026-06-8 o 13.14.21.png]]

#### Memory Mapped IO

Dlaczego PAS jest tak poszatkowana? Musielibyśmy zobaczyć jak ewoluował hardware.

Procesory chcą mapować urządzenia do PAS aby nie marnować miejsca na płytce. W wczesnych procesorach Intela - 8086 - wszystko było połączone do tej samej magistrali (20 bitowej) pamięci.![[Zrzut ekranu 2026-06-8 o 13.16.53.png]]

#### Intel 8086 memory map
Wtedy, procesory mogły adresować maksymalnie 1MB, częściowo zajmowane przez urządzenia. Wybór urządzenia jest sporządzony na podstawie 4 największych bitów adresu. Na pierwszy rzut oka ciągły 1MB (0x0000 - 0xFFFF) ma różne blocki funkcjonalne:![[Zrzut ekranu 2026-06-8 o 13.18.48.png]]