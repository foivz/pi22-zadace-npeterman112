# Softver za rezervaciju smještaja u kampu

## Podaci o studentu

Ime i prezime | E-mail adresa (FOI) | JMBAG | Github korisničko ime
------------  | ------------------- | ----- | ---------------------
Nikola Peterman | npeterman@foi.hr | 0016137228  | npeterman112

## Svrha

Svrha ovog dokumenta je specifikacicja softverskih zahtjeva softvera namjenjenog rezervaciji smještajnih jedinica. Te dokument je namjenjen programerima, dizajnerima i testerima za navođenje u izradi i testiranju softvera. Isto tako dokument se koristi i kao ugovor između naručitelja i izvršivaća rada.

## Opis domene
Problem: napraviti aplikaciju za rezervaciju smještaja u kampu, podacima zbog privatnosti mogu pristupiti samo vlasnici a cijena se formira zavisno o sezoni te vrsti smještaja i količini osoba, te ponovni gosti dobivaju 5% popusta. Vlasnicima treba omogućiti izmjenu podataka poput cijene i kapaciteta, te oogućiti im izradu statistika za tijek godine/sezone te uvid u ukupni popis gostiju i trenutnu popunjenost kampa. 

##### Cjenik smještajnih jedinica(kn/dan)
 Sezona|izvan sezone|                |
 ---------------|------|-------------|
Vrsta smještaja |      |            |
Kamp prikolica  | 150  |     80     |
Šator          |  50   |     35     |
Mobilna kućica  | 900 |      500    |
Gost            |     |             |
Odrasli        |  60  |     40      |
Djeca 5-12 godina|  30  |   20       |
Djeca 0-4 godine|  0     |     0     |

##### Izračun cijene

Izračun cijene ovisi o kombinaciji vrste smještaja, vremenskome razdoblju, te broju gostiju.
U slučaju kamp prikolice ili šatora cijena se definira zbrajanjem cijene smještaja  i cijene po gostu, a u slučaju odabira mobilne kućice plaća se samo cijena smještaja neovisno o broju gostiju, uz napomenu da je maksimalan broj gostiju 6. Ako je gost već koristio usluge kampa, ukupna cijena se smanjuje za 5%.

## Specifikacija projekta
Login za vlasnike
Unos gostiju
Mogućnost izmjene ponude
Omogućeno pretraživanje prema popunjenosti, terminu i potrebnom kapacitetu
Omogućiti godišnju, sezonsku statistiku, ostvareni prihod te prosječnu popunjenost.


## Zadatak
https://github.com/foivz/pi22-zadace-npeterman112/blob/master/Zadatak%20-%20kampovi.pdf

## Resursi
Github Markdown sintaksa dostupna je na [ovom linku](https://guides.github.com/features/mastering-markdown/) ali i na Moodleu u sekciji Zadaće.
Zadaće je obvezno predati u obliku Wiki stranica na ovom repozitoriju. Slike i druge artefakte koje ćete trabati na wiki stranicama smjestite u mapu dokumentacije u repozitoriju. 
