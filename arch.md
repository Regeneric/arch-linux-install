# **Arch Linux - instalacja i konfiguracja**

Świat systemów GNU/Linux jest rozległy i fascynujący. Każda dystrybucja ma pomysł na siebie, potrafi zebrać rzeszę nie tyle zwykłych użytkowników, ile ludzi powiązanych mniej lub bardziej z systemem. Pingwinki są od ludzi, dla ludzi, o czym wielu często zapomina.  
Dlaczego więc Arch Linux owiany jest takim mistycyzmem? Co stoi za jego sukcesem i dlaczego jest to świetny system dla naszego desktopa?
Sprawdźmy to!

## Spis treści 

* [**Arch Linux**](#Arch-Linux)
  * [**Pochodne dystrybucje**](#Pochodne-dystrybucje-Archa)
  * [**Wstępna konfiguracja**](#Wstępna-konfiguracja)
* [**Partycjonowanie dysku**](#Partycjonowanie-i-formatowanie-dysków)
  * [**LVM**](#LVM)
  * [**LVM i LUKS**](#LVM-i-LUKS)
  * [**Klasycznie**](#Klasycznie)
* [**Instalacja i podstawowa konfiguracja**](#Instalacja-i-podstawowa-konfiguracja)
    * [**Bootloader**](#Bootloader-systemd-boot)
    * [**Pliki sudoers i pacman.conf**](#Pliki-sudoers-i-pacman.conf)  
* [**Środowiska graficzne - wstęp, które wybrać, GTK i Qt**](#Środowiska-graficzne)
* [**Środowisko graficzne XFCE**](#Środowisko-graficzne-XFCE)
  * [**Konfiguracja SDDM**](#Konfiguracja-SDDM)
  * [**Konfiguracja OpenBoxa**](#Konfiguracja-OpenBoxa)
  * [**Konfiguracja XFCE**](#Konfiguracja-XFCE)  
* [**Środowisko graficzne KDE**](#Środowisko-graficzne-KDE)
* [**Programy i aplikacje użytkowe**](#Programy-i-aplikacje-użytkowe)
  * [**Konfiguracja i3lock**](#Konfiguracja-i3lock)
  * [**Konfiguracja ZSH**](#Konfiguracja-ZSH)
  * [**Konfiguracja VIMa**](#Konfiguracja-VIMa)
* [**Podsumowanie**](#Podsumowanie)

## Arch Linux

###### [Do góry](#Spis-treści)
Dystrybucja została stworzona przez Judda Vineta. Obrała sobie za cel łatwość konfiguracji, użytkowania, a także szybkość, stabilność i aktualność.

Problemem z Linuksem dla osób początkujących  jest to, że cała prostota nie opiera się na graficznym reprezentowaniu parametrów i klikaniu myszą w odpowiednie miejsca.
Ideą jest przemyślane rozmieszczenie i zaprojektowanie skryptów, programów lub plików konfiguracyjnych.
To dzięki nim, przy pomocy terminalu, możemy stworzyć system idealny. Niczym nieograniczeni, z potężnym narzędziem na naszym PC, jesteśmy w stanie tak dobrać DE (Desktop Environment - środowisko graficzne), programy czy wszelkie inne paczki, by system stanowił naszą drugą naturę.

Przemyślany menadżer pakietów **pacman**, ogromna baza programów, jaką stanowi *AUR*, niezawodność i bezproblemowa praca – te i wiele, wiele innych czynników stanowią o tym, dlaczego ten system jest tak popularny w kręgu bardziej doświadczonych użytkowników Linuksa.

Co do samego **AUR** – warto powiedzieć, że jest to swoisty odpowiednik PPA z Ubuntu.
Działa jednak znacznie lepiej i sprawniej. Za pomocą [TEJ](https://aur.archlinux.org/)  strony, jesteśmy w stanie wyszukiwać, pobierać, a następnie instalować interesujące nas pakiety.
Co więcej – nie musimy tam nawet zaglądać, bo z pomocą przychodzi nam oprogramowanie *yay*, rozszerzające działanie *pacmana*.
Operuje on właśnie na repozytoriach AUR i usprawnia cały proces instalacji.

### Pochodne dystrybucje Archa

###### [Do góry](#Spis-treści)
Zanim przejdziemy do spraw instalacji i podstawowej konfiguracji systemu, trzeba jasno powiedzieć — nie musimy instalować Archa, by cieszyć się jego najlepszymi cechami.

Dystrybucje takie jak **Manjaro**, **Antergos** czy **Bridge Linux** pozwalają nam zaznać plusów systemu, ale bez całego żmudnego i niejako zaawansowanego procesu instalacji.

Nie są one idealne i nie oddają w 100% systemu, który sami skonfigurujemy od A do Z, ale są dobrym punktem zaczepienia dla ludzi, którzy nie są do końca przekonani o sensowności korzystania z Archa.

Z drugiej strony barykady stoją takie twory jak **Anarchy** lub **Revenge Installer**, które są graficznymi nakładkami na sam proces instalacyjny systemu, znacznie skracając czas potrzebny na np. wpisywanie komend. Nie są perfekcyjne i potrafią wysypać błędy w najmniej oczekiwanym momencie, jednak dla podstawowych zadań są niezastąpione.

To dzięki wynalazkom przedstawionym wyżej możemy w prosty sposób nauczyć się specyfiki systemu, pewnych wskazanych zachowań albo po prostu przyzwyczaić się do używania choćby *pacmana*.

Osobiście nie jestem ich zwolennikiem, bo uważam, że dobrze i samodzielnie postawiony Arch to ogrom doświadczenia, a także świadomość, co nam na dysku gra.
Mimo to każdej osobie o odmiennych poglądach polecam zapoznanie się z wymienionymi wyżej dystrybucjami. Jest to krok w dobrą stronę!

### Wstępna konfiguracja

###### [Do góry](#Spis-treści)
Metodę przygotowania medium instalacyjnego pozostawiam Wam. Sposobów i nośników jest tyle, ile osób instalujących system, a niech każdy wybierze to, co mu najbardziej odpowiada.

Osobiście skorzystam z bootowalnego pendrive’a, stworzonego za pomocą komendy **dd**, lub przy użyciu oprogramowania **Rufus**, dostępnego na systemy Windows, dla instalacji na dysku **GPT** pod PC wspierającym **UEFI**.

Nie ma co się oszukiwać — **MBR** to przestarzałe rozwiązanie, które powinno zniknąć już dłuższy czas temu. Trzeba wspierać nowe technologie i korzystać z ich dobrodziejstw — zwłaszcza wtedy, kiedy przynosi nam to wymierne korzyści.

Kiedy uda nam się już poprawnie uruchomić system w trybie live, naszym oczom ukaże się okno terminalu — to za jego pomocą podzielimy dyski na partycje, sformatujemy je, pobierzemy system bazowy, ustawimy najważniejsze pliki konfiguracyjne, by finalnie móc uruchomić system prosto z dysku, aby zainstalować DE.

Całość zaczynamy od sprawdzenia, czy aby na pewno udało nam się zbootować w trybie **UEFI**, wykorzystamy do tego komendę:

> $ ls /sys/firmware/efi/efivars

![efivars](https://i.imgur.com/V9bk0qx.png)

Jeśli folder nie istnieje, to najprawdopodobniej całość uruchomiła się w trybie legacy dla **BIOSu** lub w trybie **CSM**.
Musimy więc przerwać instalację i odpowiednio ustawić opcje na naszej płycie głównej.

Następnym krokiem będzie sprawdzenie naszego połączenia z internetem. W przypadku połączenia kablem ethernet, wszystko powinno być już gotowe, ponieważ instalacja w trybie live automatycznie uruchamia usługę dhcpcd.

> $ ping google.com

Jeśli nie udaje nam się poprawnie nawiązać połączenia, dobrze jest zatrzymać i uruchomić ponownie dhcpcd komendą:

> $ systemctl stop dhcpcd  
> $ systemctl start dhcpcd

![ping-fail](https://i.imgur.com/iBTp5u6.png)

Jeśli operacja ta nie przynosi żadnego efektu, na czas instalacji możemy ręcznie skonfigurować statyczne IP dla naszej karty sieciowej:

> $ ip address show  
> $ ip address add 192.168.122.10/24 broadcast + dev enp3s0  
> $ ip route add default via 192.168.122.1  
> $ echo "nameserver 1.1.1.1" >> /etc/resolv.conf  
> $ echo "nameserver 1.0.0.1" >> /etc/resolv.conf

Oczywiście podajemy adresy IP odpowiadające rzeczywistym wartościom używanym w naszej sieci. To samo dotyczy także nazwy naszej karty sieciowej (tutaj: *enp3s0*). W moim wypadku taki adres uwarunkowany jest ukryciem się za NATem, gdyż całość instalacji przeprowadzam na maszynie wirtualnej.

![ping-succ](https://i.imgur.com/edQ5dEI.png)

## Partycjonowanie i formatowanie dysków

###### [Do góry](#Spis-treści)

Następnym krokiem będzie partycjonowanie i przygotowanie dysków do instalacji systemu. Jest to nieco bardziej skomplikowany proces, mimo to, wcale nie należy się go bać.

Możemy zrobić to w klasyczny sposób, lub też przy użyciu mechanizmu LVM i/lub szyfrowania LUKS.
LVM pozwala na połączenie partycji znajdujących się na różnych urządzeniach pamięci masowej w jeden dysk wirtualny. Jego rozmiar nie jest zdefiniowany na stałe – jeśli zachodzi taka potrzeba, istnieje możliwość jego rozszerzenia o nową przestrzeń pamięciową. Jednak proces partycjonowania jest wówczas nieco trudniejszy. 

Oprócz tego dyski działające na LVM świetnie działają z szyfrowaniem LUKS, które zabezpieczy nasze dyski przed nieproszonymi gościami. Warto zastanowić się nad takim rozwiązaniem, szczególnie, jeżeli instalujemy system na komputerze przenośnym. Wówczas, w przypadku kradzieży, nawet przy użyciu specjalnego oprogramowania, dostęp do naszych danych będzie niemożliwy. Szyfrowanie LUKS możemy postawić pod lub nad LVM. Ta druga opcja jest znaczenie lepsza, ponieważ dzięki niej zachowujemy największą zaletę LVM, czyli możliwość prostej i bezproblemowej zmiany rozmiaru partycji. Dlatego też pokażę tę właśnie konfigruację.

Moim zdaniem warto poświęcić na instalację trochę więcej czasu i zastosować LVM, chociażby po to, żeby w przyszłości nie mieć problemu z brakiem miejsca na partycji systemowej.

 Mimo wszystko, gdyby okazało się, że nie radzimy sobie także z partycjonowaniem klasycznym, można przygotować partycje przed instalacją w programie graficznym **gparted**. Dostępny jest jako obraz iso, którego możemy użyć do utworzenia bootowalnego pendrive. Pojawia się także w takich dystrybucjach jak *Manjaro* czy *Anarchy*. Potrzebne nam będą przynajmniej dwie partycje - **root /** oraz **EFI /boot**. Ta druga wymaga systemu plików *vfat* lub *fat32* oraz flag *boot* oraz *esp*, które możemy nadać po naciśnięciu prawym przyciskiem myszy na partycję.

 ![gparted](https://i.imgur.com/TpUjedh.png)

##### [Partycjonowanie z użyciem LVM](#LVM)
##### [Partycjonowanie z użyciem LVM i LUKS](#LVM-i-Luks)
##### [Partycjonowanie klasyczne](#Klasycznie)

### LVM

###### [Do góry](#Spis-treści)
Na początek musimy odnaleźć dysk, na którym nasz system ma być zainstalowany, komendą:

> $ fdisk -l

![drives](https://i.imgur.com/zoUiCPs.png)

Wypisujemy na ekranie wszystkie dyski i partycje, jakie w danej chwili znajdują się na naszym PC. Następnie korzystając z komendy:

> $ gdisk /dev/sdX

Gdzie X oznacza literę interesującego nas dysku, przechodzimy do narzędzia umożliwiającego podzielenie dysku na partycje.

Tutaj korzystamy odpowiednio z takich komend jak:

* **o** - usuwa istniejącą tablicę partycji i tworzy nową w schemacie **GPT**
* **n** - umożliwia stworzenie nowej partycji
* **w** - zapisuje wszystkie zmiany wprowadzone na dysku twardym

Aby w ogóle móc zabrać się za stworzenie czegokolwiek, musimy dokładnie prześledzić nazwy, typy i rozmiary naszych dysków, aby się nie pomylić. Na tym etapie co prawda nie ma to żadnego znaczenia, bo nasz magazyn na dane jest pusty, jednak nie ma co sobie dodawać niepotrzebnie prac.

Po ustaleniu, który z dysków będzie przechowywał w sobie system, tworzymy nowy schemat partycjonowania, a następnie partycję **ESP**.

![gpt](https://i.imgur.com/5C4S8E5.png)

*EFI System Partition* - wykorzystywana w nowoczesnych systemach do przechowywania m.in. bootloaderów naszych OSów. Więc niezależnie od tego ile ich będzie na naszym PC, partycja **ESP** zawsze będzie (i ma być) tylko jedna.

Pierwsze zapytanie dotyczy numeru, z jakim będzie identyfikowana. Możemy pozostawić domyślną – **1**.

Następnie ustalamy, od którego sektora nasza partycja będzie się zaczynać.
Dobrym nawykiem jest instalacja systemu na końcowych sektorach naszego dysku, jeśli robimy to na klasycznym dysku talerzowym. W przypadku dysków SSD nie ma to większego znaczniea. Tutaj także nie musimy niczego zmieniać.
Dobrze jednak jest się upewnić, że domyślny sektor to 2048 – od niego powinniśmy zacząć partycjonowanie.

Trzecim krokiem jest ustalenie sektora, gdzie partycja ma się kończyć. Znacznie wygodniejszym wyjściem jest podać to w mega lub gigabajtach.
My wpiszemy tutaj **+512M** – zdecydowanie wystarczająco dużo, jesli chodzi o partycję **ESP**.

Ostatnim krokiem jest podanie kodu hex dla naszej partycji. Skąd mamy wiedzieć co tutaj wpisać?
Bardzo prostym sposobem — wstukanie **L** na klawiaturze pozwoli nam zobaczyć listę wszystkich, dostępnych dla nas kodów.
Coby jednak nie szukać — dla partycji **ESP** użyjemy kodu ***EF00***.

![esp](https://i.imgur.com/CRLfbKc.png)

Następnie musimy utworzyć odpowiednio partycje **/** i **/home**.
Ich rozmiar jest bezpośrednio związy z posiadaną przez nas przestrzenią dyskową.

Osobiście zalecam *minimalne* granice rozmiaru na **/** ustalić w przedziale **15 - 35GB**, oraz całą resztę dostępnej przestrzeni na **/home**.

Dla bardziej zaawansowanych użytkowników, całkiem dobrym wyjściem będzie także rozbicie **/var** oraz **/usr** na osobne punkty montowania z odpowiednią ilością przydzielonego im miejsca. W tym poradniku jednak nie będziemy się tym zajmować.

Jedyną różnicą, jaką zastosujemy przy partycjonowaniu naszego dysku będzie to, że teraz zamiast korzystać z kodu hex ~~*EF00*~~, użyjemy **8E00**, aby móc skorzystać z zalet **LVM**.

![lvm](https://i.imgur.com/OmGUzO1.png)

Na sam koniec wystarczy zatwierdzić zmiany i potwierdzić, że zdajemy sobie sprawę z ryzyka utratych ważnych danych z dysku. O ile oczywiście jakieś są.

![save](https://i.imgur.com/d3Yyp9w.png)

W tym miejscu warto wyświetlić sobie listę naszych partycji na poszczególnym dysku za pomocą:

> $ gdisk -l /dev/sdX

Lub wszystkich dostępnych w naszym systemie, ponawiając komendę:

> $ fdisk -l

Pozwoli nam to w łatwy sposób zorientować się, która partycja ma jaki numer.
Ja będę oznaczał je jako **/dev/sdXY** – gdzie pod te parametry musicie wstawić swoje rzeczywiste dane (np. */dev/sda1* lub w przypadku nowoczesnych dysków PCIe */dev/nvme0n1p1*).

![fdisk](https://i.imgur.com/movccGU.png)

Formatowanie partycji **ESP** jest krokiem najprostszym i wymagającym od nas najmniej. Wystarczy jedna, prosta komenda:

> $ mkfs.vfat /dev/sdXY

Aby załatwić sprawę i móc później zamontować ją później w odpowiednim miejscu.

W przypadku pozostałych dwóch partycji musimy się chwilę zastanowić nad tym, co posiadamy w naszym komputerze oraz jaki efekt finalny chcemy osiągnąć.
W moim wypadku dostępne są trzy, różne dyski twarde i partycje.

Dysk *256GB* będzie oznaczony jako **root**, ponieważ to na nim znajdzie się system.  
Kolejne dwa dyski *1024GB* dostają wspólne oznaczenie **home**, ponieważ chcę móc wykorzystać ich sumaryczną pojemność w jednym miejscu.

Kiedy mamy już wszystko ustalone, możemy zainicjować nasze fizyczne partycje tak, aby mogły one korzystać z zalet LVM. Potrzebujemy tutaj komendy:

> $ pvcreate /dev/sdXY

Wydajemy ją dla każdej partycji, którą chcemy wykorzystać. Jak już wyżej zostało ustalone, będą to kolejno trzy partycje, z trzech dysków.

![pvcreate](https://i.imgur.com/WE7lxCI.png)

Następnie musimy stworzyć odpowiednią grupę naszych wolumenów, aby możliwe było wykorzystanie dwóch, różnych dysków, jako jednej, ciągłej przestrzeni.  
Zanim jednak zabierzemy się za **home**, to pasuje odpowiednio skonfigurować naszego **root**, który jest jeden, jak widać.  
Nie jest to problem, ponieważa dzięki elastyczności **LVM** możemy do grupy w chwili tworzenia dodać tylko jedną partycję, aby w przyszłość, w razie ewentualnych potrzeb, móc ją rozszerzyć. W przypadku pomyłki, partycję można dodać komendą **vgextend**.

> $ vgcreate root /dev/sdXY  
> $ vgcreate home /dev/sdAB /dev/sdCD

Oczywiście oznaczenia */dev/sdAB* oraz */dev/sdCD* zostały zastosowane jedynie w celu rozróżnienia poszczególnych wolumenów.

![vgcreate](https://i.imgur.com/pd7zOXK.png)

Finalnie możemy się już zabrać za tworzenie logicznej struktury na naszym dysku. Jest to ostatni krok przed odpowiednim sformatowaniem oraz zamontowaniem naszych partycji.
Aby móc to uczynić wydajemy polecenie:

> $ lvcreate **-l** 100%FREE -n proot root  
> $ lvcreate **-l** 100%FREE -n phome home

LUB

> $ lvcreate **-L** 35GB -n proot root  
> $ lvcreate **-l** 100%FREE -n phome home

Pora na tłumaczenie:

* **-L 35GB** - określamy rozmiar naszego logicznego wolumenu, w tym wypadku 35GB
* **-l 100%FREE** - określamy rozmiar naszego logicznego wolumenu, w tym wypadku oznacza to wypełnienie całej wolnej przestrzeni na naszej partycji
* **-n proot** oraz **-n phome** - są to nazwy utworzonych partycji w obrębie grupy, p zostało zastosowane w celu doróżniania od siebie tych dwóch tworów
* **root** oraz **home** - nazwy utworzonych wcześniej grupy

![lvcreate](https://i.imgur.com/kxQw6FI.png)

Ostatnim krokiem jest już tylko wybranie systemu plików, jaki ma być obceny na naszych partycjach. Osobiście polecam zastanowić się nad trzema możliwościami:

* **btrfs**
* **xfs**
* **ext4**

***btrfs*** - korzystając z zalet i rozwiązań starszego i bardzo popularnego w środowiskach BSD ***zfs***, zapewnia możliwość kopiowania przy zapisie, tworzenia snapshotów, replikacji danych czy zwiększania swojego rozmiaru dynamicznie, nie potrzebując do tego mechanizmu **LVM**. Jednak ma to swoje odbicie w wydajności i zastosowanie go na klasycznym dysku talerzowym może drastycznie obniżyć szybkość działania naszego systemu.

***xfs*** - posiada szereg cech zaawansowanego systemu plików do zastosowań serwerowych oraz dla wydajnych stacji roboczych. Maksymalny rozmiar wolumenu to *16000000TB*, a pojedynczego pliku ponad *8000000TB*.  
Mimo dosyć zaawansowanego i groźnie brzmiącego opisu, nadaje się świetnie także do domowych zastosowań, jest trwały, stabilny oraz nowoczesny, dzięki implementacji techonoligii takich jak np, *sparse files*, *security labels* czy POSIXowych list dostępu (ACL)

***ext4*** - najpopularniejszy, linuksowy system plików stosowany szeroko zarówno w domowych warunkach, jak i na mniejszych, i większych serwerach. Sprawia to, że w razie problemów uzyskanie wsparcia i pomocy jest banalnie proste, a także sama dokumentacja jest bogata w szczegóły.

W domu wykorzystuję ***btrfs*** na dysku SSD oraz ***xfs*** na dysku HDD. Działają w świetnej symbiozie i jestem spokojny o swoje dane. Mimo doniesień o braku stabilności samego ***xfs*** w przypadkach nagłej utraty zasilania, nie doszukałem się żadnych informacji, aby był to problem palący i szeroko znany. Obstawiam lokalne problemy na komputerach pechowców, którzy swoje dane utracili.

Uprzedzając pytania o replikację plików i jej wpływie na dyski SSD - ***btrfs*** domyślnie w takim wypadku ją wyłącza (choć można wymusić jej ponowne włączenie). No i oczywiście takie mechanizmy jak **TRIM** lub technologie **NVMe** nie są tutaj nikomu obce, a całość działa odpowiednio stabilnie i responsywnie.

Na potrzeby tego poradnika przyjmuję, że mój dysk oznaczony jako **root** jest SSD, a te ukryte pod **home** są klasyczne, HDD.

> $ mkfs.btrfs /dev/root/proot  
> $ mkfs.xfs /dev/home/phome

W tym wypadku komendy dla **LVM** są dosłowne, więc podąrzając za poradnikiem i wpisując je w okno terminalu, nie powinniśmy uświadczyć żadnych błędów.

Jesteśmy gotowi, by przejść powoli do instalacji bazowego systemu.
Musimy zamontować swoje partycje w odpowiednich miejscach za pomocą komend:

> $ mount /dev/root/proot /mnt  
> $ mkdir /mnt/home  
> $ mkdir /mnt/boot  
> $ mount /dev/home/phome /mnt/home  
> $ mount /dev/sdXY /mnt/boot

### LVM i LUKS

###### [Do góry](#Spis-treści)
Na początek musimy odnaleźć dysk, na którym nasz system ma być zainstalowany, komendą:

> $ fdisk -l

![drives](https://i.imgur.com/zoUiCPs.png)

Wypisujemy na ekranie wszystkie dyski i partycje, jakie w danej chwili znajdują się na naszym PC. Następnie korzystając z komendy:

> $ gdisk /dev/sdX

Gdzie X oznacza literę interesującego nas dysku, przechodzimy do narzędzia umożliwiającego podzielenie dysku na partycje.

Tutaj korzystamy odpowiednio z takich komend jak:

* **o** - usuwa istniejącą tablicę partycji i tworzy nową w schemacie **GPT**
* **n** - umożliwia stworzenie nowej partycji
* **w** - zapisuje wszystkie zmiany wprowadzone na dysku twardym

Aby w ogóle móc zabrać się za stworzenie czegokolwiek, musimy dokładnie prześledzić nazwy, typy i rozmiary naszych dysków, aby się nie pomylić. Na tym etapie co prawda nie ma to żadnego znaczenia, bo nasz magazyn na dane jest pusty, jednak nie ma co sobie dodawać niepotrzebnie prac.

Po ustaleniu, który z dysków będzie przechowywał w sobie system, tworzymy nowy schemat partycjonowania, a następnie partycję **ESP**.

![gpt](https://i.imgur.com/5C4S8E5.png)

*EFI System Partition* - wykorzystywana w nowoczesnych systemach do przechowywania m.in. bootloaderów naszych OSów. Więc niezależnie od tego ile ich będzie na naszym PC, partycja **ESP** zawsze będzie (i ma być) tylko jedna.

Pierwsze zapytanie dotyczy numeru, z jakim będzie identyfikowana. Możemy pozostawić domyślną – **1**.

Następnie ustalamy, od którego sektora nasza partycja będzie się zaczynać.
Dobrym nawykiem jest instalacja systemu na końcowych sektorach naszego dysku, jeśli robimy to na klasycznym dysku talerzowym. W przypadku dysków SSD nie ma to większego znaczniea. Tutaj także nie musimy niczego zmieniać.
Dobrze jednak jest się upewnić, że domyślny sektor to 2048 – od niego powinniśmy zacząć partycjonowanie.

Trzecim krokiem jest ustalenie sektora, gdzie partycja ma się kończyć. Znacznie wygodniejszym wyjściem jest podać to w mega lub gigabajtach.
My wpiszemy tutaj **+512M** – zdecydowanie wystarczająco dużo, jesli chodzi o partycję **ESP**.

Ostatnim krokiem jest podanie kodu hex dla naszej partycji. Skąd mamy wiedzieć co tutaj wpisać?
Bardzo prostym sposobem — wstukanie **L** na klawiaturze pozwoli nam zobaczyć listę wszystkich, dostępnych dla nas kodów.
Coby jednak nie szukać — dla partycji **ESP** użyjemy kodu ***EF00***.

![esp](https://i.imgur.com/CRLfbKc.png)

Następnie musimy utworzyć odpowiednio partycje **/** i **/home**.
Ich rozmiar jest bezpośrednio związy z posiadaną przez nas przestrzenią dyskową.

Osobiście zalecam *minimalne* granice rozmiaru na **/** ustalić w przedziale **15 - 35GB**, oraz całą resztę dostępnej przestrzeni na **/home**.

Dla bardziej zaawansowanych użytkowników, całkiem dobrym wyjściem będzie także rozbicie **/var** oraz **/usr** na osobne punkty montowania z odpowiednią ilością przydzielonego im miejsca. W tym poradniku jednak nie będziemy się tym zajmować.

Jedyną różnicą, jaką zastosujemy przy partycjonowaniu naszego dysku będzie to, że teraz zamiast korzystać z kodu hex ~~*EF00*~~, użyjemy **8E00**, aby móc skorzystać z zalet **LVM**.

![lvm](https://i.imgur.com/OmGUzO1.png)

Na sam koniec wystarczy zatwierdzić zmiany i potwierdzić, że zdajemy sobie sprawę z ryzyka utratych ważnych danych z dysku. O ile oczywiście jakieś są.

![save](https://i.imgur.com/d3Yyp9w.png)

W tym miejscu warto wyświetlić sobie listę naszych partycji na poszczególnym dysku za pomocą:

> $ gdisk -l /dev/sdX

Lub wszystkich dostępnych w naszym systemie, ponawiając komendę:

> $ fdisk -l

Pozwoli nam to w łatwy sposób zorientować się, która partycja ma jaki numer.
Ja będę oznaczał je jako **/dev/sdXY** – gdzie pod te parametry musicie wstawić swoje rzeczywiste dane (np. */dev/sda1* lub w przypadku nowoczesnych dysków PCIe */dev/nvme0n1p1*).

![fdisk](https://i.imgur.com/movccGU.png)

Formatowanie partycji **ESP** jest krokiem najprostszym i wymagającym od nas najmniej. Wystarczy jedna, prosta komenda:

> $ mkfs.vfat /dev/sdXY

Aby załatwić sprawę i móc później zamontować ją później w odpowiednim miejscu.

W przypadku pozostałych dwóch partycji musimy się chwilę zastanowić nad tym, co posiadamy w naszym komputerze oraz jaki efekt finalny chcemy osiągnąć.
W moim wypadku dostępne są trzy, różne dyski twarde i partycje.

Dysk *256GB* będzie oznaczony jako **root**, ponieważ to na nim znajdzie się system.  
Kolejne dwa dyski *1024GB* dostają wspólne oznaczenie **home**, ponieważ chcę móc wykorzystać ich sumaryczną pojemność w jednym miejscu.

Kiedy mamy już wszystko ustalone, możemy zainicjować nasze fizyczne partycje tak, aby mogły one korzystać z zalet LVM. Potrzebujemy tutaj komendy:

> $ pvcreate /dev/sdXY

Wydajemy ją dla każdej partycji, którą chcemy wykorzystać. Jak już wyżej zostało ustalone, będą to kolejno trzy partycje, z trzech dysków.

![pvcreate](https://i.imgur.com/WE7lxCI.png)

Następnie musimy stworzyć odpowiednią grupę naszych wolumenów, aby możliwe było wykorzystanie dwóch, różnych dysków, jako jednej, ciągłej przestrzeni.  
Tworzymy grupę, którą potem podzielimy na partycje logiczne.
Nie jest to problem, ponieważa dzięki elastyczności **LVM** możemy do grupy w chwili tworzenia dodać tylko jedną partycję, aby w przyszłość, w razie ewentualnych potrzeb, móc ją rozszerzyć. W przypadku pomyłki, partycję można dodać komendą **vgextend**.
Do grupy możemy dodać dowolną ilość dysków.

> $ vgcreate VolGrp /dev/sdXY /dev/sdAB

Oczywiście oznaczenia */dev/sdAB* oraz */dev/sdXY* zostały zastosowane jedynie w celu rozróżnienia poszczególnych wolumenów.

![vgcreate](https://i.imgur.com/HbuV9Qf.png)

Finalnie możemy się już zabrać za tworzenie logicznej struktury na naszym dysku. Jest to ostatni krok przed odpowiednim sformatowaniem oraz zamontowaniem naszych partycji.
Aby móc to uczynić wydajemy polecenie:

> $ lvcreate **-l** 100%FREE -n cryptroot VolGrp /dev/sdXY  
> $ lvcreate **-l** 100%FREE -n crypthome VolGrp

LUB

> $ lvcreate **-L** 35GB -n cryptroot VolGrp /dev/sdXY  
> $ lvcreate **-l** 100%FREE -n crypthome VolGrp

Pora na tłumaczenie:

* **-L 35GB** - określamy rozmiar naszego logicznego wolumenu, w tym wypadku 35GB
* **-l 100%FREE** - określamy rozmiar naszego logicznego wolumenu, w tym wypadku oznacza to wypełnienie całej wolnej przestrzeni na naszej partycji
* **-n cryptroot** oraz **-n crypthome** - są to nazwy utworzonych partycji w obrębie grupy, crypt zostało zastosowane w celu zaznaczenia, że korzysta się tutaj z szyfrowania
* **VolGrp** - nazwy utworzonej wcześniej grupy
* **/dev/sdXY** - dokładne sprecyzowanie, na jakim fizycznym dysku ma zostać utworzona dana partycja, w tym wypadku chcemy, aby cryptroot był na dysku SSD

![lvcreate](https://i.imgur.com/lIfH9dy.png)

Następnym krokiem będzie ustawienie szyfrowania dysku. Podczas instalacji polecam zaszyfrować jedynie partycję **/**, a pozostałymi zająć się później.
Informacja o tym jak zaszyfrować partycję już po instalcji systemu znajduje się [tutaj](https://wiki.archlinux.org/index.php/Dm-crypt/Encrypting_an_entire_system#Encrypting_logical_volume_/home "Arch Wiki")

W tym celu używamy następujących komend:

> $ cryptsetup luksFormat --type luks2 /dev/VolGrp/cryptroot  
> $ cryptsetup open /dev/VolGrp/cryptroot root

Otrzymamy informacje o całkowitym usunięciu danych z partycji. W celu kontynuuowania należy wpisać **YES** Następnie należy podać wybrane przez nas hasło, które potrzebne będzie do odczytu danych z dysku. 

![cryptsetup](https://i.imgur.com/nBsr4cP.png)

Druga komenda pozwoli nam natomiast na dostęp do wolumenu już po uruchomieniu systemu. Potrzebne będzie to później, podczas montowania dysków.

Ostatnim krokiem jest już tylko wybranie systemu plików, jaki ma być obceny na naszych partycjach. Osobiście polecam zastanowić się nad trzema możliwościami:

* **btrfs**
* **xfs**
* **ext4**

***btrfs*** - korzystając z zalet i rozwiązań starszego i bardzo popularnego w środowiskach BSD ***zfs***, zapewnia możliwość kopiowania przy zapisie, tworzenia snapshotów, replikacji danych czy zwiększania swojego rozmiaru dynamicznie, nie potrzebując do tego mechanizmu **LVM**. Jednak ma to swoje odbicie w wydajności i zastosowanie go na klasycznym dysku talerzowym może drastycznie obniżyć szybkość działania naszego systemu.

***xfs*** - posiada szereg cech zaawansowanego systemu plików do zastosowań serwerowych oraz dla wydajnych stacji roboczych. Maksymalny rozmiar wolumenu to *16000000TB*, a pojedynczego pliku ponad *8000000TB*.  
Mimo dosyć zaawansowanego i groźnie brzmiącego opisu, nadaje się świetnie także do domowych zastosowań, jest trwały, stabilny oraz nowoczesny, dzięki implementacji techonoligii takich jak np, *sparse files*, *security labels* czy POSIXowych list dostępu (ACL)

***ext4*** - najpopularniejszy, linuksowy system plików stosowany szeroko zarówno w domowych warunkach, jak i na mniejszych, i większych serwerach. Sprawia to, że w razie problemów uzyskanie wsparcia i pomocy jest banalnie proste, a także sama dokumentacja jest bogata w szczegóły.

W domu wykorzystuję ***btrfs*** na dysku SSD oraz ***xfs*** na dysku HDD. Działają w świetnej symbiozie i jestem spokojny o swoje dane. Mimo doniesień o braku stabilności samego ***xfs*** w przypadkach nagłej utraty zasilania, nie doszukałem się żadnych informacji, aby był to problem palący i szeroko znany. Obstawiam lokalne problemy na komputerach pechowców, którzy swoje dane utracili.

Uprzedzając pytania o replikację plików i jej wpływie na dyski SSD - ***btrfs*** domyślnie w takim wypadku ją wyłącza (choć można wymusić jej ponowne włączenie). No i oczywiście takie mechanizmy jak **TRIM** lub technologie **NVMe** nie są tutaj nikomu obce, a całość działa odpowiednio stabilnie i responsywnie.

> $ mkfs.btrfs /dev/mapper/root  
> $ mkfs.xfs /dev/VolGrp/crypthome

W tym wypadku komendy dla **LVM** i **LUKS** są dosłowne, więc podąrzając za poradnikiem i wpisując je w okno terminalu, nie powinniśmy uświadczyć żadnych błędów. Różnica w zapisie wynika z tego, że **/** zostało wcześniej zaszyfrowanie, a **/home** nie.

Jesteśmy gotowi, by przejść powoli do instalacji bazowego systemu.
Musimy zamontować swoje partycje w odpowiednich miejscach za pomocą komend:

> $ mount /dev/mapper/root /mnt  
> $ mkdir /mnt/home  
> $ mkdir /mnt/boot  
> $ mount /dev/VolGrp/crypthome /mnt/home  
> $ mount /dev/sda1 /mnt/boot

### Klasycznie

###### [Do góry](#Spis-treści)

Na początek musimy odnaleźć dysk, na którym nasz system ma być zainstalowany, komendą:

> $ fdisk -l

![drives](https://i.imgur.com/zoUiCPs.png)

Wypisujemy na ekranie wszystkie dyski i partycje, jakie w danej chwili znajdują się na naszym PC. Następnie korzystając z komendy:

> $ gdisk /dev/sdX

Gdzie X oznacza literę interesującego nas dysku, przechodzimy do narzędzia umożliwiającego podzielenie dysku na partycje.

Tutaj korzystamy odpowiednio z takich komend jak:

* **o** - usuwa istniejącą tablicę partycji i tworzy nową w schemacie **GPT**
* **n** - umożliwia stworzenie nowej partycji
* **w** - zapisuje wszystkie zmiany wprowadzone na dysku twardym

Aby w ogóle móc zabrać się za stworzenie czegokolwiek, musimy dokładnie prześledzić nazwy, typy i rozmiary naszych dysków, aby się nie pomylić. Na tym etapie co prawda nie ma to żadnego znaczenia, bo nasz magazyn na dane jest pusty, jednak nie ma co sobie dodawać niepotrzebnie prac.

Po ustaleniu, który z dysków będzie przechowywał w sobie system, tworzymy nowy schemat partycjonowania, a następnie partycję **ESP**.

![gpt](https://i.imgur.com/5C4S8E5.png)

*EFI System Partition* - wykorzystywana w nowoczesnych systemach do przechowywania m.in. bootloaderów naszych OSów. Więc niezależnie od tego ile ich będzie na naszym PC, partycja **ESP** zawsze będzie (i ma być) tylko jedna.

Pierwsze zapytanie dotyczy numeru, z jakim będzie identyfikowana. Możemy pozostawić domyślną – **1**.

Następnie ustalamy, od którego sektora nasza partycja będzie się zaczynać.
Dobrym nawykiem jest instalacja systemu na końcowych sektorach naszego dysku, jeśli robimy to na klasycznym dysku talerzowym. W przypadku dysków SSD nie ma to większego znaczniea. Tutaj także nie musimy niczego zmieniać.
Dobrze jednak jest się upewnić, że domyślny sektor to 2048 – od niego powinniśmy zacząć partycjonowanie.

Trzecim krokiem jest ustalenie sektora, gdzie partycja ma się kończyć. Znacznie wygodniejszym wyjściem jest podać to w mega lub gigabajtach.
My wpiszemy tutaj **+512M** – zdecydowanie wystarczająco dużo, jesli chodzi o partycję **ESP**.

Ostatnim krokiem jest podanie kodu hex dla naszej partycji. Skąd mamy wiedzieć co tutaj wpisać?
Bardzo prostym sposobem — wstukanie **L** na klawiaturze pozwoli nam zobaczyć listę wszystkich, dostępnych dla nas kodów.
Coby jednak nie szukać — dla partycji **ESP** użyjemy kodu ***EF00***.

![esp](https://i.imgur.com/CRLfbKc.png)

Następnie musimy utworzyć odpowiednio partycje **/** i **/home**.
Ich rozmiar jest bezpośrednio związy z posiadaną przez nas przestrzenią dyskową.

Osobiście zalecam *minimalne* granice rozmiaru na **/** ustalić w przedziale **15 - 35GB**, oraz całą resztę dostępnej przestrzeni na **/home**.

Dla bardziej zaawansowanych użytkowników, całkiem dobrym wyjściem będzie także rozbicie **/var** oraz **/usr** na osobne punkty montowania z odpowiednią ilością przydzielonego im miejsca. W tym poradniku jednak nie będziemy się tym zajmować.

Jedyną różnicą, jaką zastosujemy przy partycjonowaniu naszego dysku będzie to, że użyjemy innego kodu HEX. Kod dla partycji to będzie w tym wypadku ***8300***.

![fs](https://i.imgur.com/7RKt2az.png)

Na sam koniec wystarczy zatwierdzić zmiany i potwierdzić, że zdajemy sobie sprawę z ryzyka utratych ważnych danych z dysku. O ile oczywiście jakieś są.

![save](https://i.imgur.com/d3Yyp9w.png)

W tym miejscu warto wyświetlić sobie listę naszych partycji na poszczególnym dysku za pomocą:

> $ gdisk -l /dev/sdX

Lub wszystkich dostępnych w naszym systemie, ponawiając komendę:

> $ fdisk -l

Pozwoli nam to w łatwy sposób zorientować się, która partycja ma jaki numer.
Ja będę oznaczał je jako **/dev/sdXY** – gdzie pod te parametry musicie wstawić swoje rzeczywiste dane (np. */dev/sda1* lub w przypadku nowoczesnych dysków PCIe */dev/nvme0n1p1*).

![fdisk](https://i.imgur.com/movccGU.png)

Formatowanie partycji **ESP** jest krokiem najprostszym i wymagającym od nas najmniej. Wystarczy jedna, prosta komenda:

> $ mkfs.vfat /dev/sdXY

Aby załatwić sprawę i móc później zamontować ją później w odpowiednim miejscu.

Ostatnim krokiem jest już tylko wybranie systemu plików, jaki ma być obceny na naszych pozostałych dwóch partycjach. Osobiście polecam zastanowić się nad trzema możliwościami:

* **btrfs**
* **xfs**
* **ext4**

***btrfs*** - korzystając z zalet i rozwiązań starszego i bardzo popularnego w środowiskach BSD ***zfs***, zapewnia możliwość kopiowania przy zapisie, tworzenia snapshotów, replikacji danych czy zwiększania swojego rozmiaru dynamicznie, nie potrzebując do tego mechanizmu **LVM**. Jednak ma to swoje odbicie w wydajności i zastosowanie go na klasycznym dysku talerzowym może drastycznie obniżyć szybkość działania naszego systemu.

***xfs*** - posiada szereg cech zaawansowanego systemu plików do zastosowań serwerowych oraz dla wydajnych stacji roboczych. Maksymalny rozmiar wolumenu to *16000000TB*, a pojedynczego pliku ponad *8000000TB*.  
Mimo dosyć zaawansowanego i groźnie brzmiącego opisu, nadaje się świetnie także do domowych zastosowań, jest trwały, stabilny oraz nowoczesny, dzięki implementacji techonoligii takich jak np, *sparse files*, *security labels* czy POSIXowych list dostępu (ACL)

***ext4*** - najpopularniejszy, linuksowy system plików stosowany szeroko zarówno w domowych warunkach, jak i na mniejszych, i większych serwerach. Sprawia to, że w razie problemów uzyskanie wsparcia i pomocy jest banalnie proste, a także sama dokumentacja jest bogata w szczegóły.

W domu wykorzystuję ***btrfs*** na dysku SSD oraz ***xfs*** na dysku HDD. Działają w świetnej symbiozie i jestem spokojny o swoje dane. Mimo doniesień o braku stabilności samego ***xfs*** w przypadkach nagłej utraty zasilania, nie doszukałem się żadnych informacji, aby był to problem palący i szeroko znany. Obstawiam lokalne problemy na komputerach pechowców, którzy swoje dane utracili.

Uprzedzając pytania o replikację plików i jej wpływie na dyski SSD - ***btrfs*** domyślnie w takim wypadku ją wyłącza (choć można wymusić jej ponowne włączenie). No i oczywiście takie mechanizmy jak **TRIM** lub technologie **NVMe** nie są tutaj nikomu obce, a całość działa odpowiednio stabilnie i responsywnie.

Na potrzeby tego poradnika przyjmuję, że partycja oznaczona jako **/dev/sdAB** jest przeznaczona na katalog główny /, a ta ukryta pod **/dev/sdCD** na /home. Dysk **/dev/sdXY** jest to natomiast partycja EFI /boot, którą sformatowaliśmy wcześniej.

> $ mkfs.btrfs /dev/sdAB  
> $ mkfs.xfs /dev/sdCD

Jesteśmy gotowi, by przejść powoli do instalacji bazowego systemu.
Musimy zamontować swoje partycje w odpowiednich miejscach za pomocą komend:

> $ mount /dev/sdAB /mnt  
> $ mkdir /mnt/home  
> $ mkdir /mnt/boot  
> $ mount /dev/sdCD /mnt/home  
> $ mount /dev/sdXY /mnt/boot  

## Instalacja i podstawowa konfiguracja

###### [Do góry](#Spis-treści)
Pobranie pakietów i instalacja systemu mieści się w jednej komendzie:

> $ pacstrap /mnt base base-devel linux linux-firmware linux-headers dhcpcd

Będąc szczerym, to do poprawnego działania systemu nie jest wymagana paczka *base-devel*. Mimo to silnie zalecam ją zainstalować – choćby po to, żeby ułatwić sobie korzystanie z *AUR* w przyszłości.

Gdy proces instalacji dobiegnie końca, możemy powoli przygotowywać się, by przełączyć się na pracę na zainstalowanym już systemie.
Zanim to jednak nastąpi musimy wygenerować plik **fstab** komendą:

> $ genfstab -U /mnt > /mnt/etc/fstab

Jest to plik generowany na podstawie **UUID** naszych partycji. Jest to wyjście mniej intuicyjne, niż **-L**, które opiera się na etykietach, jednak jest ono znacznie bezpieczniejsze.  
Tutaj mamy pewność, że dopóki nie sformatujemy naszej partycji, jej **UUID** pozostaje niezmienione. Przy etykietach problem jest taki, że dołożenie kolejnego, nowego dysku do naszego PC może całkowicie pomieszać ich kolejność co w efekcie może sprawić, że nasz system się nie podniesie.

Gdy operacja przebiegnie pomyślnie, wklepujemy:

> $ arch-chroot /mnt /bin/bash

I już działamy na naszym systemie.
Sama komenda chroot wzięła się od słów „*change root*”, co świetnie oddaje to, jak działa.

![chroot](https://i.imgur.com/YPlIF0j.png)

Następny krok, to edycja pliku **mkinitcpio.conf**, jest to wymagane dlatego, że nasza partycja główna zawiera się w ramach **LVM** i nasz system musi mieć informacje o tym, jak się poprawnie z niej bootować.  
Jeśli jednak ktoś stwierdził, że  **LVM** nie jest mu potrzebne i partycje zrobił klasycznie, można ten krok smiało pominąć.

Do edycji wymagany będzie jakikolwiek edytor. Osobiście preferuję **vima**, dlatego to jego tutaj będzie można zobaczyć, lecz **nano**, **vi**, **emacs** z opcją *-nw* czy cokolwiek innego, działającego w CLI się nada równie dobrze.

> $ pacman -S vim  
> $ vim /etc/mkinitcpio.conf

Następnie musimy odszukać linijkę "*HOOKS*", można to zrobić prosto takim oto skrótem w *vimie*:

> Esc `/` hooks Enter n

Gdzie  *n* oznacza przesuwanie się między kolejnymi wynikami. Można to także zrobić ręcznie, jeśli ktoś chce. Tekstu nie ma wiele.

Jeżeli używamy samego **LVM** musimy dopisać ***lvm2*** po wyrazie *block*. Trzeba uważać, bo kolejność ma znacznie. Może nie aż tak duże, w przypadku samego **LVM**, ale przy zabawie z choćby *VFIO* warto o tym pamiętać.  

![mkinit2](https://i.imgur.com/iv83i5G.png)

Aby to zrobić, należy na klawiaturze wcisnąć **I** (*jak igła*) i przejść do trybu **insert** edytora.

W przypadku używania **LVM** oraz **LUKS** zmian jest nieco więcej. Nasze wpisy powinny być następujące:

![mkinit1](https://i.imgur.com/FsvQPnc.png)

Należy pamiętać, że w tym wypadku kolejność ma ogromne znaczenie.

Wychodzimy z *vima* za pomocą:

> Esc :wq

I możemy teraz przebudować nasz obraz. Kiedy nie jesteśmy pewni, czy aby na pewno wprowadziliśmy wszystkie zmiany poprawnie, możemy wydać komendę testową i się przekonać:

> $ mkinitcpio linux

Jeśli całość wykona się poprawnie, z wyjątkiem błędu dotyczącego *Linux kernel*, możemy uzupełnić ją o brakujący parametr:

> $ mkinitcpio -p linux

Jeśli korzystamy z innego jądra, jak np. *linux-vfio*, *linux-zen* czy choćby *linux-zfs*, musimy to uwzględnić w komendzie wydanej wyżej i wpisać odpowiednią wartość!

Teraz możemy zadbać o to, aby nasza usługa DHCP w systemie uruchamiała się razem z nim:

> $ systemctl enable dhcpcd

Oraz podlinkować sobie odpowiednią dla naszego regionu strefę czasową:

> $ ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime  
> $ hwclock --systohc

Jeżeli jednak czas systemu nadal będzie niepoprawny, albo przesunięty o jedną godzinę, można go łatwo zmienić już po instalacji, w ustawieniach naszego środowiska graficznego.

Przy wykorzystaniu edytora *vim* ustawimy zarówno język jak i układ klawiatury dla naszego systemu.
Za pomocą komendy:

> $ vim /etc/locale.gen

Mamy możliwość edycji odpowiedniego pliku. Wyszukujemy tutaj interesujący nas język i usuwamy symbol #, jaki go poprzedza.  

![locale.gen](https://i.imgur.com/sTqwKCr.png)

Następnie do gry wchodzą komendy:

> $ locale-gen  
> $ echo "LANG=en_US.UTF-8" > /etc/locale.conf

Koniecznie w takiej kolejności!
Wykorzystując polecenie *echo* i strumienie, dodajemy do pliku **LANG=en_US.UTF-8** – gdzie zamiast *en_US* wstawiacie wybrany przez siebie wcześniej język.

Pozostając w temacie ustawiania podstawowych parametrów naszego systemu, wydajemy polecenia:

> $ echo "hkk-virt" > /etc/hostname  
> $ echo "127.0.0.1 hkk-virt.localdomain hkk-virt" >> /etc/hosts

Zamiast **hkk-virt** wstawiamy oczywiście własną, dowolną nazwę naszego PC.

Nadszedł czas na utworzenie użytkownika oraz nadania haseł rootowi i userowi.  
Na początek wystarczy wpisać:

> $ passwd

Dzięki któremu ustalimy hasło administratora.  
Następnie poleceniem:

> $ useradd -m -G users -s /bin/bash nazwa_usera

Tworzymy nowego użytkownika, a dzięki:

> $ passwd nazwa_usera

Ustalamy dla niego hasło.

### Bootloader systemd-boot

###### [Do góry](#Spis-treści)
Jednym z ostatnich kroków, jakie musimy podjąć, jest instalacja bootloadera na partycji EFI.  
Faktem co prawda jest, że w nowoczesnych rozwiązaniach stosowanych na platformach UEFI, żaden dodatkowy loader nie jest potrzebny, bo sam UEFI Shell jest w stanie sobie poradzić z zarządzaniem i bootwaniem naszych systemów, o ile poda się mu odpowiednie parametry i wskaże partycję ESP.

Jednak dla uproszczenia całego procesu oraz stosowania uniwersalnego dla różnych platform rozwiązania, dzisiaj nasza uwaga skupi się na systemd-boot.

Do tego celu skorzystamy z komendy:

> $ bootctl install

Następnie przechodzimy do odpowiedniego katalogu za pomocą polecenia:

> $ cd /boot/loader

Gdzie musimy edytować plik loader.conf. Oczywiście z wykorzystaniem niezawodnego *vima*.

> vim loader.conf

Usuwamy wszystko co znajduje się w pliku i dopisujemy:

> default arch  
> #timeout 5

*Timeout* odpowiada za to, jak długo będzie widoczne okno umożliwiające nam wybranie systemu, jaki chcemy wystartować. W tym wypadku taki jest tylko jeden, dlatego jest to linia zakomentowana. Warto jednak ją tutaj zostawić, w razie, jakby kiedyś była potrzebna, a pamięć zawiodła i nie potrafiła sobie przypomnieć o takim parametrze.

Zapisujemy dokonane zmiany i przechodzimy do edycji naszego wpisu do loadera:

> $ cd entries/  
> $ vim arch.conf

Zmiany które tutaj wprowadzimy powinny być różne, zależnie od rodzaju instalacji, na który się zdecydowaliśmy:

---

**LVM**:

**title Arch Linux  
linux /vmlinuz-linux  
initrd /initramfs-linux.img  
initrd /intel-ucode.img  
options root=/dev/mapper/root-proot rw**  



Nie możemy zapomnieć, by na końcu dopisać **rw**!


---

**LVM** oraz **LUKS**:

**title Arch Linux  
linux /vmlinuz-linux  
initrd /initramfs-linux.img  
initrd /intel-ucode.img  
options cryptdevice=UUID=3d9a2835-025a-4182-a5fd-a0372255db76:root root=/dev/mapper/root rw**

Tytuł możemy nadać dowolny, ale UUID musimy wpisać odpowiadające naszej **/dev/VolGrp/cryptroot**  
Za pomocą polecenia:.

> $ blkid /dev/VolGrp/cryptroot

Możemy na ekranie wyświetlić sobie informacje o naszych partycjach.

![blkid](https://i.imgur.com/MtyyPcX.png)

Nie możemy zapomnieć, by na końcu dopisać **rw**!

---

W przypadku partycjonowania **klasycznego**:

**title Arch Linux  
linux /vmlinuz-linux  
initrd /initramfs-linux.img  
initrd /intel-ucode.img  
options root=PARTUUID=6265d89d-d8b0-4809-9ce1-3a75796fd237 rw**

Tytuł możemy nadać dowolny, ale PARTUUID musimy wpisać odpowiadające naszej partycji roota!  
Zamiast PARTUUID można skorzystać z UUID.
Za pomocą polecenia:

> $ blkid /dev/sdXY

Możemy na ekranie wyświetlić sobie informacje o naszych partycjach.

Do tego możemy wykorzystać także:

> $ cat /etc/fstab

Używamy komend i wpisów zależnie od tego, jak nam wygodniej, choć ja *BARDZO* mocno zalecam użyć **PARTUUID**.
A to dlatego, że *UUID* identyfikuje system plików, a **PARTUUID** partycję *GPT*, z czego to drugie nie zmienia się przy formacie.

W pliku *arch.conf* musimy wpisać **PARTUUID** naszej głównej partycji – /


Ale także nie możemy zapomnieć, by na końcu dopisać **rw**!

### Pliki sudoers i pacman.conf

###### [Do góry](#Spis-treści)

Zanim zaczniemy cokolwiek więcej pobierać, warto skonfigurować odpowiednio menadżer pakietów *pacman* i zadbać o to, aby *yay* było dostępne na naszym dysku. W tym celu wpisujemy:

> $ vim /etc/pacman.conf

I odnajdujemy linie:

> #[multilib]  
> #Include = /etc/pacman.d/mirrorlist

> #Color

Usuwamy znaki #, a pod opcją "*Misc options*" dopisujemy:

> ILoveCandy

Możemy zapisać całość i korzystając z polecenia:

> $ pacman -Syu

Wprowadzić nasze zmiany w życie.

Co do wpisu o *intel-ucode*, są to mikrokody dla naszego procesora.
W przypadku AMD całość zawarta jest w linux-firmware, dla Intela trzeba je pobrać osobno, co jest mocno wskazane.
Używając polecenia:

> $ pacman -S intel-ucode

Możemy zrealizować tą czynność, wybierając pakiet z listy i zatwierdzając jego numer. I jeśli nasza partycja *ESP* zamontowana jest w /boot, sprawa załatwiona. W innym wypadku należy przenieść wszystko w miejsce, gdzie ona się znajduje.

Zanim będziemy gotowi zrestartować swój system, warto edytować odpowiednio plik *sudoers*, by móc korzystać z polecenia **sudo**.  
Do tego celu wpisujemy:

> $ vim /etc/sudoers

I pod użytkownikiem root dodajemy linijkę:

> nazwa_usera ALL=(ALL) ALL

![sudoers](https://i.imgur.com/qftGrac.png)

Zapisujemy, zamykamy i kiedy wszystko jest gotowe, wciskamy **Ctrl+D**, a następnie wpisujemy *reboot* i uruchamiamy Arch Linuxa prosto z naszego dysku!

Przed rozpoczęciem konfiguracji środowiska graficznego warto zaopatrzyć się w menadżer pakietów, który znacząco ułatwi pobieranie i instalację paczek.
Aktualnie najlepszym rozwiązaniem jest menadżer pakietów *yay*, który posiada integrację nie tylko z oficjalnym repozytorium Archa, ale także z *AUR*, na czym nam najbardziej zależy.  
Musimy wpisać więc:

> $ pacman -S git && git clone https://aur.archlinux.org/yay.git  
> $ cd yay/ && makepkg -sri

Takimi oto sposobem zaopatrzyliśmy się w rozwiązanie, z którego korzysta aktualnie większość społeczności Archa.  
Od teraz pobieranie pakietów i aktualizacja systemu zawiera się w tej jednej komendzie i jeśli sytuacja nas do tego nie zmusza, nie są wymagane żadne dodatkowe parametry.

I to wszystko. Przebrnęliśmy przez proces instalacji systemy od początku, aż do samego końca. Następnym krokiem jest już tylko konfiguracja DE i WM pod nasze osobiste potrzeby.  

## Środowiska graficzne

###### [Do góry](#Spis-treści)

Żeby w ogóle móc korzystać z jakiegokolwiek DE, potrzebujemy serwera X. Możemy go pobrać razem z terminalem XTerm za pomocą komendy:

> $ yay -S xorg xorg-xinit xterm

Parametr **-S** pojawił się przy *yay* tylko dlatego, że chcemy pobrać kilka pakietów naraz i nie chcemy wybierać ich po kolei z listy.

I w tym miejscu ogranicza nas tylko własny gust i upodobania.  
Wybór DE jest ogromny i to co wybierzemy, zależne jest tylko od nas.

Ja skupię się według mnie na dwóch najlepszych opcjach, jakimi są *KDE Plasma* oraz *XFCE* z menadżerem okien *Openbox*.  

Na które z nich się zdecydujemy, zależy tylko od nas. Najważniejszą różnicą są biblioteki, na których opiera się środowisko, a także możliwości konfiguracyjne i łatwość ich wprowadzania.  

To, na jakiej bibliotece opiera się nasz system, ma największe znaczenie, kiedy zamierzamy zająć się projektowaniem aplikacji, oraz kiedy zamierzamy wprowadzić unifikację aplikacji w systemie.

*XFCE* opiera się na bibliotece GTK+, napisanej przy użyciu języka C. Przestała być aktualizowana już kilka lat temu. Mimo wszystko nadal jest powszechnie używana. Większość programów, którą znajdziemy na repozytoriach naszego systemu, opiera się na tej bibliotece. 
Konfiguracja XFCE jest znacznie trudniejsza niż konfiguracja Plasmy, gdyż większość zmian dokonujemy przez edycję odpowiednich plików *xml*. Bez odpowiednich pomocy, konfiguracja naszego systemu może być bardzo ciężka. Przez to możemy jednak znacznie lepiej spersonalizować nasz system. Jeżeli czujemy się na siłach, to mocno zachęcam do spróbowania swoich sił. Poniżej przedstawiam swoją propozycję na zbudowanie wydajnego i eleganckiego systemu opartego o *XFCE*.

*KDE Plasma* opiera się za to na bibliotece Qt, którą zaprojetkowano w języku C++. Biblioteka jest stale aktualizowana, a ze względu na łatwość obsługi, liczba programów na niej opartych szybko rośnie. Mimo wszystko nadal GTK+ posiada szerszy wybór oprogramowania. Konfiguracja Plasmy jest znacznie prostsza. Większość odbywa się w specjalnej aplikacji przeznaczonej do tego. Szukanie motywów, widgetów czy schematów kolorów na Plasmie jest szybsze, a wszystko zainstalować możemy bez edycji plików tekstowych. Plasma domyślnie posiada ładny, podobny do Windowsa, układ, i nie wymaga tak dużej konfiguracji, żeby osiągnąć przyzwoity efekt, ale odrobina pracy pozwala na zmianę systemu nie do poznania. Żeby jednak osiągnąć taki poziom konfigurowalności, jaki oferuje XFCE, musimy się bardzo napracować.

Warto zaznaczyć. że nic nie stoi na przeszkodzie, żeby korzystać np. z aplikacji opartej na GTK+ na KDE Plasma, jednak jeżeli system nie zostanie odpowiednio skonfigurowany wówczas aplikacje mogą wyglądać inaczej, niż byśmy tego oczekiwali.

Jeżeli zdecydowałeś się na rozwiązanie cięższe, ale pozwalające na większą konfigurację, wybierz [**XFCE**](#Środowisko-graficzne-XFCE).

Jeżeli zdecydowałeś się na rozwiązanie łatwiejsze, gdzie domyślnie dostajemy całkiem przyzwoicie wyglądający system, konfiguracja nie jest tak potrzebna, wybierz [**KDE**](#Środowisko-graficzne-KDE).


## Środowisko graficzne XFCE

###### [Do góry](#Spis-treści)

Zaczynamy od pobrania odpowiednich paczek:

> $ yay -S xfce4 xfce4-goodies sddm i3lock-color-git

Paczka *xfce4-goodies* nie jest wymagana, ale waży zaledwie kilkanaście megabajtów i zapewnia zestaw podstawowych narzędzi ułatwiających start ze środowiskiem.
Zamiast *sddm* można równie dobrze używać *lightdm*, który także robi tutaj świetną robotę.

Następny krok, to dobór sterowników – tutaj trzeba je dobrać odpowiednio do posiadanej karty graficznej.  
Każdy musi poradzić sobie sam, opierając się na posiadanym sprzęcie oraz wymaganiach. Ponieważ na rynku znajduje się sporo sprzętu o różnym stopniu kompatybilności, zarówno z otwartymi, jak i własnościowymi sterownikami, nie opiszę tutaj procesu instalacji żadnej z tych paczek.  
Zamiast tego odsyłytam [TUTAJ](https://wiki.archlinux.org/), do Wiki Archa po więcej informacji.

Jeśli jednak totalnie nie mamy pojęcia co zainstalować, można pominąć ten krok i zdać się na Archa i jego kompatybilność z naszym sprzętem. W większości wypadków jakaś forma otwartych sterowników jest już zaimplementowana, więc finalnie powinniśmy mieć jakikolwiek obraz widoczny na naszym monitorze.

Jesteśmy już gotowi do pierwszego uruchomienia naszego środowiska graficznego.
Zanim to jednak nastąpi, musimy wpisać następujące polecenie:

> $ sudo systemctl enable --now sddm

![sddm](https://i.imgur.com/hC0eaiY.png)

![xfce](https://i.imgur.com/k1PYaHn.png)

#### Konfiguracja SDDM

###### [Do góry](#Spis-treści)
Jak widać na screenshotach wyżej, standardowy **SDDM**, który decydujemy się sami zainstalować nijak ma się do tego znanego choćby z *KDE*. W środowiskach FOSS (*Free and Open Source Software*) nie jest to jednak problemem i mamy niemalże pełną kontrolę nad systemem.

Swoje pierwsze kroki powinniśmy skierować na stronę https://store.kde.org/  
Co nie powinno być dla nikogo zaskoczniem. Przeglądając treści tam zawarte, bardzo szybko możemy natrafić na zakładkę "[*SDDM Login Themes*](https://store.kde.org/browse/cat/101/)", która w tym momencie najbardziej nas interesuje.

Pozwala nam ona przebierać w różnych stylach dla naszego menadżera logowania, lecz trzeba być tutaj ostrożnym, bo nie wszystkie działają one bez **Plasmy**! Najczęściej jednak występują dwa warianty, z czego jeden dla ludzi, którzy zdecydowali się na *SDDM* w wersji standalone.

Osobiście zdecydowałem się na theme "[*Chili*](https://store.kde.org/p/1240784/)", które zresztą całkiem nieźle imituje ekran logowania znany choćby z macOS. Nie do każdego musi ten styl trafiać, jednak sam poradnik powinien być nadal aktualny dla dowolnego, innego stylu.

Zanim jednak zabierzemy się za samo upiękrzanie *SDDM*, dobrze będzia zadbać o wymagane zależności podane przez twórcę:

> $ yay -S qt5 qt5-quickcontrols qt5-graphicaleffects

Nad różnicami między GTK, a Qt nie ma co się tutaj rozwodzić, więc dla uproszczenia polecam pokornie pokiwać głową i przyjąć, że skoro tego nam potrzeba do działania całości, to tak ma być i kropka.

Paczkę *.tar.gz* możemy pobrać ze strony sklepu lub odwiedzić repozytorium autora na GitHubie, co sam preferuję. Niemniej sam sposób zdobycia stylu nie ma tutaj znacznia, więc nie zmuszam nikogo do niczego.

**GitHub**
> $ git clone https://github.com/MarianArlt/sddm-chili.git   
> $ sudo mv sddm-chili/ /usr/share/sddm/themes/

**sddm-chili.tar.gz**
> $ sudo tar -xzvf ~/Downloads/sddm-chili.tar.gz -C /usr/share/themes/

Dobrze też zadbać o avatar naszego użytkowania. W tym celu potrzebujemy dowolnej grafiki, która musi mieć odpowiednią nazwę oraz znajdować się w odpowiednim miejscu.

Sam schemat jest całkiem prosty: *username.face.icon*  
Gdzie za *username* wstawiamy oczywiście nazwę naszego użytkownika.

Następnie wystarczy wydać polecenie:

> $ sudo mv username.face.icon /usr/share/sddm/faces/

Aby załatwić sprawę i mieć to z głowy, aby późniejsza konfiguracja przebiegła szybko i bezproblemowo.

Ostatnim krokiem przygotowań do pełnej jednolitości systemu, jest zadbanie o jednakowy styl naszego kursora na ekranie logowania oraz już w samym systemie. Mówię to oczywiście w kontekście jednego użytkownika, gdzie taka unifikacja jest jak najbardziej wskazana. W przypadku kilku różnych kont trzeba indywidualnie sprawę przemyśleć.

W moim wypadku zwycięskie theme nazywa się "*Capitaine*" i ponownie jest mocno inspirowane macOS, a dokładnie wersją 10.11, jak sama nazwa wskazuje.  
Dodatkowo sprawa jest na tyle prosta, że całość znajduje się w AUR, więc wystarczy komenda:

> $ yay capitaine-cursors

Aby mieć już wszystkie potrzebne składniki na miejscu.

Korzystając z tego, że mamy już postawione działające środowisko graficzne, odsyłam do opcji systemowych myszy, gdzie jednym kliknięciem i przeładowniem sesji logowania załatwiamy sprawę.

![cursors](https://i.imgur.com/nXqdRNa.png)


Następnym krokiem będzie konfiguracja samego *SDDM*, aby korzystał z pobranego theme. Można to natrulanie zrobić w CLI, lecz jest też całkiem prosta i przyjemna aplikacja, która nazywa się *SDDM Configurator*.  
Sama w sobie jest jedynie graficzną nakładką, ale znacznie usprawnia cały proces.

> $ yay sddm-config-editor-git  
> $ sddm-config-editor

Jedyne o co musimy zadbać, to wskazanie folderów, w których przechowywane są avatary oraz style, a następnie wpisać nazwy w odpowiednie pola.

![sddm-conf](https://i.imgur.com/Xa0RIah.png)

Możemy całość zapisać, lecz nie jest to koniec prac nan naszym *Chili*.  
Dobrze jest tutaj wydać komendę:

> $ sudo vim /usr/share/sddm/themes/sddm-chili/theme.conf

Gdzie powinniśmy odpowiednio ustawić następujące parametry:

**backgroud** - lokalizacja pliku graficznego, który będzie tłem na naszym ekranie logowania

**ScreenWidth** - w przypadku dwóch lub więcej monitorów, ustawić najwyższą, dostępną na wszystkich rozdzielczość  
*Opcjonalnie*: ustawić najwyższą dostępną rozdzielczość na pojedynczym monitorze, a następnie odpowiednio skonfigurować plik Xsetup

**ScreenHeight** - w przypadku dwóch lub więcej monitorów, ustawić najwyższą, dostępną na wszystkich rozdzielczość  
*Opcjonalnie*: ustawić najwyższą dostępną rozdzielczość na pojedynczym monitorze, a następnie odpowiednio skonfigurować plik Xsetup

**blur** - wartość "true" oznacza, że tło na ekranie logowanie będzie rozmazane o wartości zdefiniowane w dwóch, kolejnych liniach, stosować wedle gustu

**recursiveBlurLoops**  - odpowiednik zapisu AxB, gdzie za A należy podstawić wartość od 0 w górę

**recursiveBlurRadius** - odpowiednik zapisu AxB, gdzie za B nalezy podstawić wartość większą od 1

![theme.conf](https://i.imgur.com/M6cv1Q1.png)

**Xsetup** - do pliku znajdującego się w */usr/share/sddm/scripts/* należy dopisać:

 > *xrandr --output OUTPUT --off*

Gdzie za OUTPUT należy wstawić rzeczywistą wartość (*np. HDMI-2, DVI-1, VGA-3*).  
Wyłączone na czas logowania powinny zostać monitory, które nie obsługują rozdzielczości podanej w pliku *theme.conf*.  
Komenda niżej pomoże nam się rozeznać w naszej konfiguracji ekranów.

> $ xrandr

Następny krok to edycja pliku *Main.qml*.

> $ sudo vim /usr/share/sddm/themes/sdd-chili/Main.qml

To tak naprawdę całe serce naszego stylu, ja jednak ograniczę się tylko do odpowiedniego wyświetlania daty i godziny na ekranie logowania.

W tym celu należy odnaleźć linię:

> *text = new.Date().toLocalString(Qt.locale("en_US"), "ddd dd MMMM, hh:mm A")*

I zmodyfikować ją w taki sposób:

> *text = new.Date().toLocalString(Qt.locale("en_US"), "hh:mm  ddd  dd/MM/yyyy")*

Lub pobawić się formatem daty według własnego uznania i upodobania. Śmiało można zastąpić także *en_US* swoiskim *pl_PL*, aby wyświetlać nazwy dni tygodnia i miesięcy w naszym ojczystym języku.

Warto także zainteresować się standardem **ISO-8601**, który definiuje międzynarodowy, jednolity sposób zapisu daty, który wygląda następująco:

> YYYY-MM-DD hh:mm:ss ±hh:mm

Dopuszcza on rozdzielenie czasu od daty pojedynczą spacją i jest czytelny dla każdego człowieka na świecie, niezależnie od przyzwyczajeń (*jak np. w przypadku USA i zapisu MM-DD-YYYY*).

Kiedy całość jest już zapisana i odpowiednio edytowana, *SDDM Configurator* pozwala nam podejrzeć efekt pracy. Wystarczy wcisnąć przycisk *preview*, aby się przekonać, czy wszystko poszło po naszej myśli.

![preview](https://i.imgur.com/ZjC496G.png)

#### Konfiguracja OpenBoxa

###### [Do góry](#Spis-treści)
Pomimo świadomej i pewnej decyzji, jaką podjąłem instalując **XFCE**, oraz jaką sam polecam, mam pełną świadomość tego, że w chwili pisania tego tekstu, jest to jedno z najmniej przyszłościowych środowisk graficznych dostępnych na rynku.

Nie dzieje się tak przez czysty przypadek. Grupa ludzi pracująca na łataniem dziur i rozwijająca projekt jest tak niewielka, że często garażowe projekty czy kilkunastogodzinne game jamy posiadają liczniejszą załogę.  
Powoduje to dwojaką sytuację, w której aktualizacje są oddalone od siebie o całe dziesiątki tygodni nie wnosząc wcale tak dużo (następna duża aktualizacja, 4.14, jako swój killer feature przynosi jedynie pełną integracją z GTK3).

W stosunku do **KDE** czy **GNOME**, dwóch bardzo dużych projektów (ten drugi ma nawet fanowski fork nie wymagający do działania *systemd*), jest to aż smutne.  
Jednak druga strona medalu jest taka, że twórcy projektu *XFCE* doskonale zdają sobie sprawę z tego, jak ma się sytuacja, więc całe środowisko zbudowali w taki sposób, aby było bardzo silnie modyfikowalne przez zapalonych użytkowników.

To, czego oni nie są nam w stanie dostarczyć, naprawiamy i dodajemy sami.  
Wielu ludzi takie podejście odstrasza, ale według mnie jest to sytuacja niemal idealna do zabawy i zdobycia całkiem sporych umiejętności.

Czynniki wypisane w powyższych akapitach wpłynęły także na mnie i moje postrzeganie tego DE, a zwłaszcza menadżera okien *XFWM*.  
Mimo bycia potężnym, a zarazem lekkim kawałkiem oprogramowania, brakuje mu sporo funkcji znanych z choćby *KWin* lub... **OpenBoxa**.

**OpenBox** w przeciwieństwie do *FluxBoxa* lub *JWM* skupia się na jednym zadaniu.  
Byciu wydajnym, lekkim i bardzo mocno modyfikowalnym menadżerem okien (WM).  
Dzięki ogromnej społeczności zgromadzonej wokół niego oraz dzięki plikom konfiguracyjnym w formacie **XML**, jesteśmy w stanie zbudować nawet niezależny desktop, korzystając tylko i wyłącznie z *OpenBoxa*.

Ja jednak postanowiłem ograniczyć jego rolę tylko (i aż) do tego, aby trzymał moje środowisko graficzne w ryzach, zarządzając oknami czy pulpitami.  
Fakt, nie jest on tak przyjazny i intuicyjny, jak *XFWM*, jednak i na to są odpowiednie rady i aplikacje. Niemniej pasuje wziąć się do roboty, więc wydajemy komendy:

> $ yay -S openbox compton  
> $ openbox --replace &  
> $ compton &

I tak naprawdę tyle wystarczyło, aby pozbyć się XFWM. Oczywiście nie całkowicie!

Zdaję sobie sprawę, że w stanie surowym podmiana menadżera okien może wydawać się okropnym pomysłem, zwłaszcza kiedy ujrzymy, jaki bałagan to spowodowało na naszym pulpicie.

Jednak kolejny krok, to pobranie dwóch aplikacji, które sprawią, że cały proces konfiguracji stanie się zwykłą przyjmenością:

> $ yay -S obconf obkey compton-conf

Następnie dobrze jest zaopatrzyć się w porządne style graficzne dla naszego menadżera okien.  
Sposobów na zdobycie takowych jest kilka. Na przykład świetnym miejsce na złapanie inpiracji jest [/r/unixporn](https://www.reddit.com/r/unixporn/) - subreddit na którym ludzie dzielą się swoimi modyfikacjami i stylami na niemalże wszystkich środowiskach i dystrybucjach.

Do dyspozycji jest także strona [Box-Look.org](https://www.box-look.org/browse/cat/140/), która stara się katlogować mniej i bardziej popularne style graficzne. Warto się rozejrzeć, bo zarówno fan retro stylu, jak i futuryzmu znajdzie tutaj coś dla siebie.

Od siebie szczerze polecam [TO](https://github.com/addy-dclxvi/openbox-theme-collections) repozytorium na GitHubie użytkownika *addy-dclxvi*. Gość robi niesamowitą robotę na tak dużo różnych środowisk i menadżerów, że można tutaj wracać po kilkanaście razy i znajdować to, co nas najbardziej interesuje.

Aby zaopatrzyć się w paczkę, wpisujemy komendę:

> $ git clone https://github.com/addy-dclxvi/openbox-theme-collections.git  
> $ sudo mv openbox-theme-collections/ /usr/share/themes/

Folder, do którego trafiły nasze style, jest użyteczny także dla modyfikowania DE, oraz daje dostęp innym użytkownikom systemowym do pobranych skórek.

Następnie wydajemy prostą komendę:

> $ obconf

I jesteśmy gotowi na konfigurację *OpenBoxa*, którą pokrótce opiszę.

Na start w oczy rzuca się zakładka, która od razu zachęca do wybrania interesującego nas stylu. Osobiście zdecydowałem się tutaj na *Raven-Cyan*, przez kontrastowy title bar i dopasowanie reszty kolorystki do mojego aktualnego upodobania raczej zimnymi kolorami.

![themes](https://i.imgur.com/jnXLbhB.png)

W zakładce "*Appearance*" śmiało możemy zaszaleć z czcionką, jaka będzie reprezentować nasz system. Jak widać jestem razczej stonowany w tej kwestii, ale może kogoś fantazja poniesie?  
Jest to także miejsce, w którym możemy przearażnować ułożenie przycisków okien. Jeśli ktoś przywykł do *macOS* albo *Ubuntu*, to bez problemu może całość przenieść z prawej strony na lewą.

![appearance](https://i.imgur.com/LkK1tqe.png)

Zakładka "*Windows*" jest szczególnie przydatna dla konfiguracji z więcej, niż jednym monitorem. W łatwy sposób można zarządzać, gdzie i dlaczego mają pojawiać się nowe okna oraz powiadomienia. Na szczególną pochwałę zasługuje możliwość inteligentnego rozmieszczania rzeczy pod naszym kursorem myszy, ogromna wygoda.

![windows](https://i.imgur.com/c2LScVx.png)

W następnym polu mamy całkiem sporo kompleksowych opcji dotyczących migracji i zmiany rozmiaru okien aplikacji i folderów. W przypadku korzystania z kilku obszarów roboczych jest to tym bardziej ważne, aby odpowiednio dostosować wartości do naszych preferencji.

![moveres](https://i.imgur.com/HLAkKQ1.png)

Podobnie jest także w przypadku ustawień myszy, z których sam zdecydowałem się zrezygnować. Moim preferowanym urządzeniem wejścia jest klawiatura i to ona ma być mi najbardziej pomocna. Zadaniem myszki jest jedynie nie przeszkadzać.

![mouse](https://i.imgur.com/ZA7iw3P.png)

Obszary robocze to rozwiązanie, które sobie niezywkle cenię. Pozwalają sprawnie i wygodnie zarządzać pracą na naszym pulpicie, a przy okazji trzymają wszystko odpowiednio zorganizowane. Do tego odpowiednio skonfigurowane skróty klawiszowe pozwalają się między nimi sprawnie przełączać.  

![desktops](https://i.imgur.com/U97bMht.png)

Ostatnie dwie zakładki w mojej opinii nie są już warte przedstawienia dla systemu, jaki ten tekst buduje. Niemniej na własną rękę warto tam zajrzeć, może jednak znajdzie się tam opcja, której tak desperacko poszukujemy?

Następnie polecenie:

> $ obkey

Pozwala nam wywołać okno konfiguracyjne skrótów klawiszowych. Jednak jest to na tyle indywidualna opcja, że ciężko mi cokolwiek polecać. Warto jest jednak poświęcić chwilę i przewertować listę dostępnych akcji i samemu zdecydować, co nam będzie potrzebne.

Od siebie dodam, że kombinacje jak *Alt+Tab* czy *Alt+F4* są swego rodzaju standardem, który warto zaimplementować także u siebie.

![obkey](https://i.imgur.com/Lg6GXls.png)

Za pomocą plusa w lewym, górnym rogu aplikacji dodajemy definicję nowego skrótu. Klikając w nią, program zacznie oczekiwać na wciśnięcie odpowiedniej konfiguracji klawiszy. Jeśli jednak nie chce to działać poprawnie, zawsze można wpisać ręcznie porządany skrót w kolumnę **Key (text)**.

Nastęþnie używając zielonego plusa w prawym, dolnym rogu ekranu możemy do naszego skrótu podpiąć akcje, jakie ma on wykonywać. To jest najtrudniejsza część, bo wymagana od nas porządnego zastanowienia się. Niemniej bez strachu, zawsze można tutaj wrócić i dodać odpowiednie wpisy wedle potrzeb.

Całość konfiguracji zapisujemy niebieską strzałą w lewym, górnym rogu ekranu. Jest to moment, od którego wszystkie skróty powinny być już aktywne i funkcjonalne.

Ostatnią rzeczą jaką dobrze jest zrobić, to wrzucić polecenie podmieniające *XFWM* na *OpenBoxa*.  
Można to zrobić bezpośrednio w menu ustawień *XFCE*, zakładka "*Session and Startup*".

Wystarczy dodać nowy wpis, a w pole *command* wpisać:

> openbox --replace

I całość zapisać. Takim oto sposobem udało się wykonać dość poważną ingerencję w środowisko graficzne, jednak bez zbędnego bólu potrzebnego na edycję plików XML.

![startup](https://i.imgur.com/JVtWWOc.png)


#### Konfiguracja XFCE

###### [Do góry](#Spis-treści)
Ostatnim krokiem przed skończeniem budowania systemu, jest samo XFCE. Sprawa jest o tyle ułatwiona, że wszystko można ustawić z poziomu GUI.  
Warto spędzić tutaj chwilę dobierając interesujące nas theme, ikony czy font.  
Postaram się pokrótce opisać najważniejsze opcje i zakładki, a resztę pozostawię do własnej, dowolnej eksploracji i dostosowania pod osobiste preferencje.

Całość warto jednak zacząć od zaopatrzenia się w style graficzne z [TEGO](https://github.com/addy-dclxvi/xfwm4-theme-collections) repozytorium, które zostało już m.in. wspomniane przy OpenBoxie. 

> $ git clone https://github.com/addy-dclxvi/xfwm4-theme-collections.git  
> $ sudo mv xfwm4-theme-collections/ /usr/share/themes/

Następnie przechodzimy do ustawień systemowych i zakładki "*Appearance*".

![appe](https://i.imgur.com/MwRRSUh.png)

To tutaj pojawią się pobrane style graficzne, nad którymi mamy pełną wolność wyboru i ogranicza nas jedynie poczucie estetyki i własny gust.  
W razie problemów zawsze istnieje możliwość, aby ręcznie edytować pliki **CSS** w folderze /themes/ i ustawić interesujące nas wartości.

![numix-circle](https://i.imgur.com/5UstyKB.png)

Jako wielki fan okrągłych ikon mam słabość do stylu Numix Circle. Są to tak urocze i trafiające do mnie ikony, że czuję się źle, kiedy nie są one obecne w moim systemie. Oczywiście nie jest to jedyny dostępnt styl. Odwiedzając [TĘ](https://www.xfce-look.org/browse/cat/132/) stronę możemy przebierać i wybrzydzać do woli. 

Po pobraniu paczki należy ją wypakować poleceniem *tar*, a następnie umieścić całość w folderze **/usr/share/icons/**, aby pojawiły się one w menu wyboru.  
Można też spróbować znaleźć daną paczkę w AUR, a wtedy jedna komenda załatwia za nas sprawę:

> $ yay numix-circle-icon-theme-git

![font](https://i.imgur.com/eYll231.png)

Następna zakładka jest nie tylko miejsce, gdzie dostosujemy systemową czcionkę. Jest to miejsce szczególnie przydatne dla osób posiadających np. ekrany 4K lub korzystające z telewizorów, jako swoich codziennych monitorów.

To właśnie tutaj można dostosować DPI w taki sposób, aby wszystko było odpowiednio dopasowane i naturalne. W końcu nikt nie chce ramki szerokość 10% wysokość ekranu z fontem jak ziarna maku, prawda?  
Jednak dla większości wyświetlaczy 1080p wartość 96 DPI powinna być całkowicie wystarczająca.

Wychodząc z menu "*Appearance*" i przechodząc do "*Notifications*" mamy możlwiość ustawienia powiadomień systemowych oraz tych, które wychodzą od samych aplikacji.

![not](https://i.imgur.com/U7mAdgo.png)
![notapp](https://i.imgur.com/QeExAZS.png)

W zakładce "*Display*" w łatwy sposób możemy zarządzać rozdzielczością, częstotliwością odświeżania, orientacją czy ułożeniem naszych monitorów. Szczególnie przydatne w konfiguracjach 2+.

![display](https://i.imgur.com/MAUj18N.png)

"*Settings Editor*" to graficzna nakładka dla *Xfconf*. To, co normalnie robi się w linii komend, tutaj można odpowiednio wyklikać myszą.  
Jest to jednak już zaawansowany poziom edycji i polecam tutaj nie mieszać losowymi wpisami, jeśli nie wiemy co robimy.

Jeśli jednak nabierzemy ciut wprawy i doświadczenia, *Xfconf* staje się potężnym narzędziem przydatnym zwłaszcza podczas pisania skryptów rozszerzających funkcjonalność naszego DE.

![xfconf](https://i.imgur.com/rrVtoMt.png)

Na sam koniec zostawułem menu paneli. To tutaj jest cała esencja tego, jak wyglądać i zachowywać będzie się nasz pulpit. To na panelach umieszczane będą ikony, powiadomienia, akcje kontekstowe i co tak naprawdę dusza zapragnie.

Sam preferuję je jako jedyne źródło interakcji z programami i nie korzystam z ikon na pulpicie - pozwala to utrzymać porządek i jednolitą estetykę.  
Oczywiście nie zmuszam nikogo do takiego stylu pracy, to jedynie moja wizja na zbudowanie systemu.

![panel](https://i.imgur.com/Vp25FSO.png)

Pierwsza zakładka pozwala nam dodać kolejne panele do naszego systemu. Także tutaj określa się ich rozmiar, kolor, umieszczenie oraz zachowanie. Mogą one równie dobrze działać jako dock na aplikacje, który będzie się inteligentnie chował w momencie, kiedy jakaś inna aplikacja go zasłoni.

![launchers](https://i.imgur.com/xttPbTc.png)

Poszczególne aplikacje dodawane są na pasek za pośrednictwem zakładki "*Items*". To w tym miejscu budowana jest struktura i zastosowanie dla panelu.

Najpopularniejszy element to *launcher*, za pomocą którego możemy uruchamiać zdefiniowane w nim aplikacje, oraz *separator*, który rozdziela od siebie poszczególne elementy na pasku.

![myconf](https://i.imgur.com/W2unJTs.jpg)

Moja konfiguracja pulpitu przewiduje po 4 panele na jeden monitor, podzielone na poszczególne grupy:
 1. Launchery poszczególnych aplikacji - zastępują ikony na pulpicie
 2. Panel przeznaczony na wyświetlanie skróconego tytułu aktualnie otwartego okan na pełnym ekranie. 
 3. Podstawowe narzędzia systemowe pozwalające się wylogować, kontrolować głośność czy sprawdzić godzinę
 4. Panel przeznaczony na wyświetlanie otwartych aplikacji oraz powiadomień

Dodatkowo, aby całość mogła się integrować odpowiednio z aplikacjami, wymagany jest pakiet **Orcsome**, plugin **Windowck** i [TEN](https://pastebin.com/dGZUrrL9) skrypt Pythona napisany z jego wykorzystaniem:

> $ yay -S orcsome xfce4-windowck-plugin

Należy edytować plik **~./config/orcsome/rc.py**, do którego trzeba wkleić powyższe linie konfiguracyjne. 
Sprawia on, że aplikacje otwierane na pełnym ekranie nie posiadają paska z tytułem, czy przyciskami pozwalającymi na ich zamknięcie. 

Zamiast tego całość zintegrowana jest z panelami - oszczędza to miejsce na ekranie i poprawia estetykę. 
Należy także pamiętać, aby do interesujących nas paneli dodać następujące elemnty:

> Window Header - Title  
> Window Header - Buttons 

![windowck](https://i.imgur.com/xp9uT9R.jpg)

I tak naprawdę to wszystko, co mogę przekazać z najważniejszych aspektów XFCE.  Cała reszta konfiguracji spoczywa na użytkowniku, jego odczuciach, potrzebach i preferencjach. A że każdy jest inny, to nie jestem w stanie przewidzieć każdej możliwości.

Jednak co mogę zalecić, to nie bać się zmieniać rzeczy i z nimi eksperymentować. Po to własnie Pingwiny są otwartymi systemami, aby z tego korzystać!

## Środowisko graficzne KDE

###### [Do góry](#Spis-treści)

Zaczynamy od pobrania odpowiednich paczek:

> $ yay -S plasma sddm

Jeżeli przeszkadza nam duża ilość paczek, zamiast paczki *plasma* możemy użyć *plasma-desktop*, która nie zawiera aplikacji przygotowanych do rozpoczęcia działania z systemem. Wówczas możemy interesujące nas paczki pobrać ręcznie, a do przeglądania ich można użyć chociażby *Octopi*. Mimo wszystko ja zalecam instalację paczki *plasma*, szczególnie jeśli jest to nasza pierwsza przygoda z systemem Linux.

Następny krok, to dobór sterowników – tutaj trzeba je dobrać odpowiednio do posiadanej karty graficznej.  
Każdy musi poradzić sobie sam, opierając się na posiadanym sprzęcie oraz wymaganiach. Ponieważ na rynku znajduje się sporo sprzętu o różnym stopniu kompatybilności, zarówno z otwartymi, jak i własnościowymi sterownikami, nie opiszę tutaj procesu instalacji żadnej z tych paczek.  
Zamiast tego odsyłytam [TUTAJ](https://wiki.archlinux.org/), do Wiki Archa po więcej informacji.

Jeśli jednak totalnie nie mamy pojęcia co zainstalować, można pominąć ten krok i zdać się na Archa i jego kompatybilność z naszym sprzętem. W większości wypadków jakaś forma otwartych sterowników jest już zaimplementowana, więc finalnie powinniśmy mieć jakikolwiek obraz widoczny na naszym monitorze.

Jesteśmy już gotowi do pierwszego uruchomienia naszego środowiska graficznego.
Zanim to jednak nastąpi, musimy wpisać następujące polecenie:

> $ sudo systemctl enable --now sddm

![sddm](https://i.imgur.com/hC0eaiY.png)

![kde](https://i.imgur.com/yRTCWSP.png)

Prawie cała konfiguracja odbywa się w aplikacji *systemsettings*, którą możemy uruchomić przy użyciu launchera KDE, lub komendy *systemsettings5*. Możemy zmienić to praktycznie wszystko, od czasu systemowego, czcionki, motywu, aż do schematu kolorów czy ustawień myszy.
Aplikacja może być też roszerzana przez odpowiednie moduły, które możemy pobrać przy użyciu komendy *yay*. Jeżeli jednak zdecydowaliśmy się na instalację systemu z paczki *plasma*, wówczas te najważniejsze moduły powinny być już zainstalowane.

KDE Plasma domyślnie posiada dwa motywy, Breeze Light oraz Breeze Dark, a także odpowiadające im motywy pod GTK. Warto dbać o to, żeby motyw ustawiony dla aplikacji Qt był taki sam, jak dla aplikacji GTK. Możemy zmienić go w sekcji *Application Style > GNOME Application Style*.

![gtktheme](https://i.imgur.com/Jw9QObQ.png)

Jeżeli domyślne motywy nam nie odpowiadają, bardzo prosto możemy pobrać inne, używając opcji *Get New Looks...*. Dzięki temu przy użyciu kilku kliknięć jesteśmy w stanie uzyskać system wyglądem przypominający chociażby Ubuntu.

Mnóstwo motywów, zarówno tych przeznaczonych dla Qt i GTK+ możemy znaleźć w sieci, na specjalnych stronach, takich jak np. [KDE Store](https://store.kde.org/ "KDE store").
Duża część motywów znajduje się jednak na prywatnych stronach lub repozytoriach github twórców.

Warto wyłączyć także gesty ekranu dotykowego w sekcji *Touch Screen*, które mogą sprawiać problemy. W razie gdyby pojawiły się problemy z aplikacjami otwierającymi się w złych rozdzielczościach, wyłączyć można też funkcje krawędzi ekraniu w sekcji *Screen Edges*.

![screenedge](https://i.imgur.com/upxJOab.png)

Jeżeli nie zamierzamy korzystać z systemu KDE Wallet, który szyfruje i zapisuje nasze hasła, możemy go wyłączyć w sekcji *Account Details*

![kcm](https://i.imgur.com/4KUws6G.png)

Możemy łatwo także skonfigurować nasz menadżer logowania, *SDDM*. Służy do tego specjalna sekcja w aplikacji *systemsettings*. Pozwala też na pobieranie motywów, zmienianie ich, autologowanie, a nawet zmianę kursoru myszy w menadżerze.

![sddmkde](https://i.imgur.com/wNM6CGB.png)

Reszta konfiguracji odbywa się w już konkretnych aplikacjach KDE, takich jak np. Konsole, Dolphin, Okular, Spectacle, czy Kate.

Tak prezentuje się Plasma po prostej konfiguracji, na domyślnym motywie, Breeze-Dark.

![kdebase](https://i.imgur.com/gOVJQYP.jpg)

Oczywiście można system spersonalizować bardziej, chociażby przy użyciu Latte-Docka, albo oprogramowania Kvantum, ale to wymaga od nas nieco więcej pracy.

Oto dwie konfiguracje, które udało mi się stworzyć:

![kde1](https://i.imgur.com/fFEZuVH.png)
Motyw GTK + Qt: OneDark OSX Transparent  
Ikony: Papirus Dark  
Kvantum: KvOneDark  

![kde2](https://i.redd.it/d7usc6ia5tg01.png)
Dock: Latte-Dock  
Motyw GTK + Qt: Maia Transparent  
Kvantum: brak  

## Programy i aplikacje użytkowe
#### Konfiguracja i3lock

###### [Do góry](#Spis-treści)
Dobrze jest posiadać w systemie możliwość zablokowania ekranu i wymagania od użytkownika wprowadzenia hasła, ale bez konieczności wylogowania się.  
Do tego posłuży nam właśnie *i3lock*, który jest jedną wielu alternatyw dla tego typu rozwiązań.

Wybrałem go dlatego, że społeczność skupiona wokół samego i3wm, oraz ogromna skalowalność i podatność na proste modyfikacje to coś, z czego warto skorzystać w swoim domowym (i nie tylko) zaciszu.

Zanim zaczniemy, musimy zaopatrzyć się w dwa narzędzia, które pozwolą nam bawić się obrazem, który zostanie podłożny jako tło naszego ekranu blokady:

> $ yay -S scrot imagemagick

Pierwszy z nich, to prosta aplikacja terminalowa, która pozwala nam przechwytywać zrzuty ekranu. Drugi umożliwi nam modyfikację uzyskanego obrazu, co wykorzystamy do nałożenia bluru czy rozpikselowania obrazu.

Pokuszę się ponownie o pracę wykonaną przez innych użytkowników. Chodzi mi o skrypt, który nie ma problemu z obsługą więcej, niż jednego monitora. Jest zrobiony lekko i z głową, a do tego napisany w BASHu, co pozwala go silnie modyfikować i podglądać zmiany na żywo.

Można się w moją, przerobioną już wersję zaopatrzyć [TUTAJ](https://pastebin.com/msvB9hQb).  
Dodatkowo potrzebne będę [TE](https://imgur.com/a/o9iZpxB) dwa obrazki, które się pojawią na naszym ekranie blokowania.

Pokrótce także wytłumaczę najważniejsze linijki kodu:

> LOCK="/usr/share/i3lock-fancy/icons/lock.png"  
> TEXT="/usr/bin/text.png"

To tutaj definiujemy miejsce przechowywania naszych grafik, oraz możemy całkowicie zrezygnować z moich, gotowych i spróbować stworzyć coś własnego.  
Dodatkowo zamiast */usr/share/* dobrze by było wpisać *$FOLDER*, zmienną zdefiniowaną wcześniej. Lecz zauważyłem, że nie jest to na tyle dokładne, na ile bym chciał i czasem coś nie działa, temu znacznie bezpieczniej jest tutaj napisać bezpośrednią ścieżkę do pliku.

> OUTPUT_IMAGE="/tmp/i3lock.png"  
> DISPLAY_TEXT=false  
> PIXELATE=false  
> BLURTYPE="0x4"  

Najważniejsze parametry tutaj, jakie nas interesują to to, jakiego efektu oczekujemy na naszym zrzucie ekranu. Ja zdecydowałem się na blur o dość soczystej wartości 0x4, lecz nic nie stoi na przeszkodzie zastosować 0x13, lub łagodniejsze 3x4.  
Dobrze jest się pobawić tymi wartościami i dostosować je pod nasz gust i możliwości sprzętowe.

Warto również wspomnieć o dwóch liniach, które mówią same za siebie, więc jeśli nie pasuje nam domyślna lokalizacja na zapis naszej grafiki, możemy ją śmiało zmienić.

> scrot -z $OUTPUT_IMAGE

Tutaj sytuacja jest prosta. Ot, dwa parametry, które określają miejsce zapisu pliku oraz to, że chcemy uchwycić cały dostępny pulpit na wszystkich monitorach. Uważam, że nie ma sensu się tutaj bardziej rozwodzić.

> i3lock -i $OUTPUT_IMAGE -t -e --composite --radius 55 --ring-width 5.0 --veriftext="Wait" --wrongtext="Wrong" --noinputtext="N/I"

Oto i główne danie naszego skryptu, sam *i3lock*. Idąc po kolei z parametrami wychodzi to tak:

**-i $OUTPUT_IMAGE** - ścieżka do obrazu  
**-t** - rozciągnięcie zrzutu na całą dostępną przesteń ekranową  
**-e** - ignoruje puste hasła, w których nie wprowadzono żadnych znaków  
**--composite** - w zależności od używanego kompozytora parametr ten należy zostawić lub usunąć. Jeśli obraz nie jest wyświetlany poprawnie, to wtedy należy bawić się z tą opcją  
**--radius 55** - promień koła, które wyświetla się przy wpisywaniu hasła  
**--ring-width 5.0** - szerokość obwódki na kole  
**--veriftext="Wait"** - tekst wyświetlany podczas sprawdzania poprawności wpisanego hasła  
**--wrongtext="Wrong"** - tekst wyświetlany, jeśli podane hasło jest nieprawidłowe  
**--noinputtext="N/I"** - teksty wyświetlany, jeśli żadna wartość nie została wpisana

Takimi oto sposobem otrzymaliśmy prosty, lekki i schludny skrypt, który pozwala nam zablokować ekran na czas naszej nieobecności przy komputrze, aby nieporządane ręce i oczy nie miały dostępu do naszego pulpitu, plików i zawartości.  
W dalszej części podepniemy to pod jakiś wygodny skrót klawiszowy.

Oczywiście, efekt blur jest stosunkowo prosto odwracalny w programach graficznych, ale *i3lock* nie ma robić tutaj za zabezpieczenie definitywne, a jedynie za ograniczenie zbyt ciekawskich ludzi.

![i3lock](https://i.imgur.com/lsfs2PS.jpg)

#### Konfiguracja ZSH

###### [Do góry](#Spis-treści)
> ZSH (Z shell) – uniksowa powłoka (ang. shell) nadająca się zarówno do interaktywnej pracy z systemem jak i do wykonywania skryptów. Spośród standardowych powłok, ZSH najbardziej przypomina Korn Shell, ale zawiera wiele ulepszeń. zsh posiada edycję wiersza poleceń, wbudowaną korekcję pisowni, programowalne dopełnianie poleceń, funkcje (z automatycznym ładowaniem), historię poleceń i mnóstwo innych cech.

Tyle tytułem wstępu, dzięki uprzejmości polskiej Wikipedi. Nie mówi to co prawda zbyt wiele, ale nie szkodzi, śpieszę z wyjaśnieniem.

Pierwsza sprawa, jaka rzuca się w oczy, to popularność samego ZSH. W stosunku do *BASHA*, czy nawet czystego *TCSH*, samo *ZSH* nie wydaje się mieć jakiegoś szczególnego miejsca w sercu użytkowników. Może na to wpływać kilka różnych czynników, z czego osobiście dwa uznaję za najbardziej prawdopodobne:

* Ograniczenie roli terminala w życiu użytkownika - żyjemy w czasach, w których ciężko jest sobie wyobrazić domowy system operacyjny, który nie będzie posiadał wygodnego i przyjaznego użytkownikowi GUI. Dzięki czemu wielu ludzi w linuksowych społecznościach decyduje się niemal całkowicie zrezygnować z używania CLI na rzecz wyklikania wszystkiego myszą. Jest im tak wygodniej i tak właśnie lubią pracować ze swoim systemem. Dla takich ludzi powłoka, z jakiej korzystają, nie ma większego znaczenia. A już na pewno nie na tyle, żeby jeszcze próbować ją zmieniać.

* Zbyt małe doświadczenie i strach przed zmianami - często i gęsto podnoszym argumentem za wyższością Pingwinków nad innymi systemami jest ich otwartość. Że użytkownik ma pełną dowolność i kontrolę nad swoim systemem. Jest to prawda, jak najbardziej, lecz co z tego, skoro spora rzesza początkujących i średnio-zaawansowanych użytkowników boi się cokolwiek zmieniać w obawie przed zepsuciem swojego OSu? Lub najwzywczajniej w świecie nie odczuwa potrzeby do żadnych większych modyfikacji? Jako, że tej grupie w większości wypadków wystarcza to, co dostają z dystrybucją (a takich przecież nie brakuje na rynku), nijak nie ma tutaj większych szans na próbę przejścia z BASHa na ZSH.

Są to oczywiście tylko domysły prostego użytkownika, do tego obarczone sporymi skrótami myślowymi i ogromną generalizacją. Jednak spędzając czas na przeróżnych grupach wsparcia technicznego czy czysto linuksowego, są powody, które przewijają się najczęściej w dyskusjach.

Jest też grupa ludzi, do której sam się zaliczam, która lubi podejmowane akcje racjonalizować potrzebami i wymaganiami, które napotka na swojej drodze. Jako długoletni użytkownik *BASHa* ani myślałem go zmieniać. Był wszechstronny, prosty, wygodny i popularny. Jednak z każdym kolejnym skryptem dodawanym do mojego systemu, każdym kolejnym ficzerem, mój terminal przestał spełniać pokładane w nim nadzieje. Psuł cały flow i unifikację mojego systemu. W każdym razie, w moim odczuciu.  
Jestem także typem osoby, który mimo względnego upodobania do stabliności, lubi pobawić się swoim systemem. I to chyba ta wrodzona w każdego człowieka ciekawość i zmysł estetyczny popchnęły mnie do zmian.

Efekt, do którego będziemy tutaj dążyć, wygląda następująco:

![zsh](https://i.imgur.com/o0iTNLu.png)

Całość konfiguracji trzeba zacząć od pobrania samego *ZSH*:

> $ yay zsh

A następnie dobrze jest zaopatrzyć się we framework **Oh My ZSH**. Nie jest on co prawda w żaden sposób wymagany, ale jego popularność i prostota obsługi sprawiają, że warto go mieć w swoim systemie, aby sprawnie konfigurować swój nowy shell.

Sam pakiet co prawda znajduje się repozytorium, lecz polecam zainteresować się poleceniem prosto z Gita twórcy:

> $ yay wget  
> $ sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

Pozwala nam ono nie tylko pobrać samo *ZSH*, ale także ustawić jako aktywną powłokę dla naszego użytkownika.  
Już teraz można pokusić się o zaglądnięcie do pliku ~/.zshrc, jednak polecam się z tym wstrzymać.

Następny krok to pobranie odpowiednio stylu oraz PowerLine'a:

> $ yay -S powerline powerline-fonts powerline-common awesome-terminal-fonts  
> $ git clone https://github.com/bhilburn/powerlevel9k && mv powerlevel9k/ ~/.oh-my-zsh/themes/

Następnie w pliku ~/.zshrc należy odnaleźć linię **ZSH_THEME** i dopisać do niej *powerlevel9k/powerlevel9k*

![9klvl](https://i.imgur.com/KnYcIEe.png)

Ktoś może zapytać: "*Ala dlaczego akurat powerlevel9k, a nie np. agnoster?*".  
Odpowiedź na tak postawione pytanie jest bardzo prosta, a mianowicie możliwości konfiguracyjne. Agnoster nie dostarcza ich w odpowiednim stopniu. A już na pewno nie są one tak łatwo dostępne.

Osobiście zdecydowałem się na dość skromne stylowanie, jednak [TUTAJ](https://github.com/bhilburn/powerlevel9k) śmiało można odnaleźć pełną listę obsługiwanych słów kluczowych i dostosować całość wedle własnego uznania.

> POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(user dir_writable dir ssh vcs)  
> POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status root_indicator background_jobs host)


![zshconf](https://i.imgur.com/dgfX56B.png)

Sama składnia myślę jest na tyle prosta, że nie ma coś się nad całością rozwodzić, niemniej warto wspomnieć o najważniejszych rzeczach:

* **dir_writable** - komunikuje użytkownikowi, czy ma uprawnienia pozwalające na zapis plików w folderze, w którym się znajduje

* **ssh** - mały indykator informujący użytkownika, że jest to sesja ustanowiona za pomocą SSH

* **vcs** - pozwala korzystać z symboli zawartych w paczce *Awesome Terminal Fonts*

* **status** - zwraca status wykonania się ostatniej komendy

Dobrze by też było dopasować styl kolorystyczny terminala do naszej aktualnej palety kolorów dostępnej na pulpicie. Tutaj będzie nam potrzebna aplikacja:

> $ yay python-pywal  

Jeśli posiadamy środowisko graficzne XFCE, możemy wpisać:

> $ wal -n -i $(xfconf-query -c xfce4-desktop -p /backdrop/screen0/monitor0/workspace0/last-image)

W taki oto sposób program sam odczyta i ustawi w naszej konsoli pasujący styl, opierając się na tapecie z głównego monitora i pierwszego obszaru roboczego. Nie jest to jeszcze permanentne i wykorzystujemy tylko ułamek możliwości całej aplikacji, ale bardziej zaawansowane rozwiązanie są świetnie opisanie w manualu, do którego warto zajrzeć.  
W przypadku innego środowiska graficznego, wydajemy komendę:

> $ wal -n -i /sciezka/do/zdjecia.png

Następnie trzeba dopisać w pliku ~/.zshrc linię:

> (cat ~/.cache/wal/sequences &)

Co sprawi, że każdy nowo otwarty terminal będzie korzystał z wygenerowanego schemtu kolorystycznego.

Jedną z ostatnich rzeczy do zrobienia, jest pobranie dwóch bardzo przydatnych pluginów:

> $ git clone https://github.com/zsh-users/zsh-autosuggestions `$`{ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

> $ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git `$`{ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

Pierwszy z nich śledzi historię wprowadzonych poleceń, aby następnie na podstawie słów kluczowych, czy nawet pierwszych liter, podpowiadać całe, długie komendy. Przydatne przy powtarzających się terminalowych czynnościach.

Drugi podkreśla składnię poleceń i odpowiednimi kolorami sygnalizuje nam pomyłkę (lub tez sukces) przy wprowadzaniu komendy do CLI. Osobiście nie potrafię już żyć bez tych dwóch pluginów.

Aby zmusić je do działania, wymagana jest edycja linii *plugins* i dopisanie tam odpowiednich wartości:

> plugins=(  
  git  
  zsh-autosuggestions  
  zsh-syntax-highlighting  
  )

![plugins](https://i.imgur.com/B0SvK7q.png)

Oraz wykonanie polecenia:

> $ source ~/.zshrc

W ten oto sposób, już nawet restart naszego systemu nie powinien mieć negatywnego wpływu na shell i odwrotnie. Zaś my, jako użytkownicy, możemy nacieszyć oko całkiem ładnym i nowoczesnym wyglądem terminala.

#### Konfiguracja VIMa

###### [Do góry](#Spis-treści)
**VIM** to jeden z najpopularniejszych i najlepszych edytorów tekstu działający w CLI. Jego największymi zaletami są m.in. pełna konfigurowalności, ogromne możliwości skryptowe oraz ogromne zaawansowanie, które pozwala na jego podstawie zbudować pełnoprawne IDE do pracy z C++, Javą, C# i czym tylko człowiek zapragnie.

Są to też niestety rzeczy, które na starcie bardzo mocno odrzucają początkujących. Słynny żart o tym "*jak wyjść z vima*" stał się tak popularny, że nawet ludzie nie korzystający z tego edytora w ogóle, całkiem dobrze go znają.  
Osobiście twierdzę, że znajomość *vima* (a tak właściwie, to jeszcze lepiej *vi*) to na tyle przydatna umiejętność, że warto poświęcić kilka chwil na zaznajomienie się podstawami. W przyszłości może to przynieść sporo korzyści i oszczędzić jeszcze więcej czasu.

W tej sekcji głównym celem będzie integracja PowerLine'a z edytorem, aby zachować jednolitość i unifikację z samym terminalem, w którym *vim* pracuje oraz wytłumaczenie podstawowych komend i możliwości konfiguracyjnych.

Na sam początek dobrze będzie pobrać następujące paczki:

> $ yay -S vim-runtime powerline-vim vim-pathogen python

Pathogen w prosty i przyjemny sposób pozwala nam integrować pluginy z *vimem*, co podobnie jak w przypadku *Oh My ZSH* znacznie usprawni naszą pracę nad konfiguracją.

Następnie należy edytować plik **~/.vimrc** i wkleić do niego [TEN](https://pastebin.com/m1Hu4ag1) config za pomocą skrótu klawiszowego **Shift + Insert** lub środkowego przycisku myszy. Ale to w zależności w którym schowku zapisaliśmy linie konfiguracyjne.  
Pokrótce objaśniam:

Początkowe linie determinują obsługę i działanie Pathogena oraz sprawdzają, czy Python został poprawnie zainstalowany. Jeśli wszystko przebiegło tak, jak trzeba, nie powinniśmy uświadczyć żadnych błędów.

> " colorscheme gruvbox

Linijki zaczynające się od znaku **"** to komentarze. W pliku jest ich całkiem sporo przez to, że każdy musi dobrać ustawienia wedle własnego uznania i tego, co potrzebuje. W tym wypadku determinowany jest schemat kolorów *gruvbox*. Zakomentowanie tej linii sprawi, że *vim* będzie korzystać z systemowego schematu ustawionego w naszym terminalu.

> set tabstop=4       " number of visual spaces per TAB  
> set softtabstop=4   " number of spaces in tab when editing  
> set shiftwidth=4    " number of spaces used for autoindent, command: <<, >>, == (auto entire doc: gg=G )  
> set expandtab       " tabs are converted into spaces  

Wpisy szczególnie przydatne dla programistów, czy ogólnie ludzi edytujących np. pliki XML. Określają to, jak program ma interpretować wciśnięcie przycisku Tab na klawiaturze, oraz jak ma reprezentować swoje akcje nam, użytkownikom.  
Bardzo ważną linią jest *expandtab*, która automatycznie zamienia taby na spacje. Należy ją ustawić odpowiednio do wykorzystywanego języka, bo w niektórych, jak np. *Pascal*, ma to duże znaczenie.

> set number          " show line numbers  
> " set relativenumber  " show relative distances to make commands such as 8dd faster. Abslut number is still shown on curor line

Pierwszy wpis mówi sam za siebie, natomiast drugi jest już ciut bardziej enigmatyczny. Usunięcie komentarza sprawi, że numer linii będzie pokazywany względem naszego wskaźnika do początku i końca dokumentu. Oznacza to, że nasz wskaźnik zawsze jest linią numer 0, a wszystko poniżej i powyżej liczone jest od niego. 

> set showmatch       " Highlight matching {[()]} probably enabled by deffault as well

Podświetlanie klamer zaczynających i kończących dany blok w programie, czy dowolnym innym pliku. Przydatne, żeby szybko i wizualnie móc rozeznać się  między blokami w np. podwójnej pętli for.

> map `<C-c> :s/^/\/\//<Enter>`  
> map `<C-u> :s/^\/\///<Enter>`
 
Definiowanie skrótów klawiszowych w pliku konfiguracyjnym może być na starcie dosyć mylące, jednak należy pamiętać, że są to zwykłe wyrażenia regularne, których zrozumienie procentuje także w takich językach, jak np. JavaScript.  
W tym wypadku za pomocą kombinacji **Ctr+C** i **Ctrl+U** możemy komentować całe bloki kodu i te komentarze usuwać. Ino należy mieć na uwadze, że jest to komentarz w stylu **`//`**, więc jeśli dany typ pliku takowego nie obsługuje, on sam nie zadziała. 

> map `<C-e> :q!<Enter>`  
> map `<C-w> :wq<Enter>`
 
Kombinacja **Ctrl+E** umożliwia opuszczenie edytora bez zapisywania jakichkolwiek zmian, a **Ctrl+W** najpierw zmiany zapisze, a dopiero potem wyjdzie z programu.

> map `<F9> :make<Enter>`  
> map `<F5> :w<Enter>`

Skróty znane z wielu popularnych IDE. **F9** pozwala skompliować aktualnie pisany kod, a **F5** zapisuje zmiany bez wychodzenia z edytora.

Podstawowe skróty klawiszowe można rozpisać w następujący sposób:

Poruszanie się po tekście:  
* h - przesunięcie kursora w lewo
* l - przesunięcie kursora w prawo
* j - przesunięcie kursora w dół
* k - przesunięcie kursora w górę

Edycja i wstawianie:
* i - przejście w tryb *insert*
* s - przejście w tryb *insert* z usunięciem aktualnego znaku 
* a - przejście w tryb *insert* z przesunięciem kursora w prawo
* o - dodanie nowej linii poniżej aktualnej i przejście w tryb *insert*
* I - przejście w tryb *insert* z przesunięciem kursora na pierwszy znak w linii
* A - przejście w tryb *insert* z przesunięciem kursora na ostatni znak w linii
* Esc - wyjście z dowolnego trybu i przejście w tryb *normal*

Zapis i wyjście (w trybie *normal*):
* :w - zapis pliku
* :w <NAZWA> - zapis pliku pod daną nazwą
* :wq - zapis i wyjście z pliku
* :q - wyjście z pliku
* :q! - wyjście z pliku, nawet jeśli zmiany nie zostały zapisane

Na start jest to w 100% wystarczające. W trakcie dalszego korzystania z *vima* nasze umiejętności będą w naturalny sposób się rozwijać. Od siebie mogę jeszcze polecić aplikację **vim master** dostępną na telefony z Androidem, która od samego podstaw, aż do najbardziej skomplikowanych wyrażeń jest w stanie nas nauczyć korzystania z tego programu.

![vim](https://i.imgur.com/c8QCMSw.png)

## Podsumowanie

###### [Do góry](#Spis-treści)

Świat systemów spod znaku jakże rozpoznawalnego pingwina Tuxa jest ogromny i otwarty, czekający tylko na to, aby przyciągnąć do siebie nowych użytkowników.  
Zarówno pasjonaci, jak i zwykli użytkownicy komputerów, mogą znaleźć tutaj coś dla siebie.

Kiedy decyzja przychodzi naturalnie, od naszej własnej chęci na spróbowanie czegoś nowego, a sam proces porzucania Windowsa (lub tylko ograniczania jego roli w naszym życiu), jest spokojny, powolny i odpowiednio rozciągnięty w czasie, aby nie powodować niepotrzebnego szoku, i zamieszania, Linux okazuje się być bardzo wdzięczny.

Szansę na sprawdzenie samych siebie lub podzielenie się ze światem swoimi umiejętnościami mają zarówno graficy i web developerzy, którzy mogą tworzyć pamiętne i ładne style dla naszych systemów, jak i programiści. Ci drudzy mogą brać czynny udział nie tylko w rozwijaniu konkretnej dystrybucji, czy samego jądra systemu, ale także wspierać pomniejsze, fanowskie projekty (jak np. spotify-cli) lub tworzyć własne.  
A nawet nie będąc w żadnej z tych grup, a jedynie korzystając z ich dorobku i otwartości systemu, możemy stworzyć setup, który docenią inni.

Sposoby przedstawione w tym wpisie na budowę systemu są w wielu aspektach uniwersalne. Bo formatowanie dysków, czy sam proces instalacji systemu raczej pozostaje niezmienny.  
Największe różnice zachodzą podczas konfiguracji DE czy WM, gdzie ogranicza nas tylko gust i wyobraźnia.  
Tutaj pokazano tylko dwie propozycje, na dwóch całkowicie odmiennych od siebie środowiskach, zbudowane z inną myślą przewodnią oraz pod różny typ użytkownika.
Może ktoś odnajdzie w tym inspirację? W końcu nauka na gotowych przykładach przynosi ludziom ogrom korzyści, do późniejszego, samodzielnego wykorzystania. 

**Autorzy:** Hubert Batkiewicz, Gabriel Król  
**Korekta:** Julia Trychta  
**Testy i wsparcie:** Radosław Kołodziejski
