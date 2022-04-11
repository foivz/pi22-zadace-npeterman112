# Softver za rezervaciju smještaja u kampu

## Podaci o studentu

Ime i prezime | E-mail adresa (FOI) | JMBAG | Github korisničko ime
------------  | ------------------- | ----- | ---------------------
Nikola Peterman | npeterman@foi.hr | 0016137228  | npeterman112

## 1. Uvod
## Svrha

Svrha ovog dokumenta je specifikacicja softverskih zahtjeva softvera namjenjenog rezervaciji smještajnih jedinica. Te dokument je namjenjen programerima, dizajnerima i testerima za navođenje u izradi i testiranju softvera. 

## Opis domene
Potrebno je napraviti aplikaciju za rezervaciju smještaja u kampu, podacima zbog privatnosti mogućnost pristupa imaju samo vlasnici a cijena se formira zavisno o sezoni te vrsti smještaja i količini osoba, te ponovni gosti dobivaju 5% popusta. Vlasnicima treba omogućiti izmjenu podataka poput cijene i kapaciteta, te omogućiti im izradu statistika za tijek godine/sezone te uvid u ukupni popis gostiju i trenutnu popunjenost kampa. Sam naziv aplikacije će biti "Kampiranje"

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

## Definicije, akronimi i skraćenice

- sezona : vremensko razdoblje od 1. lipnja do 30. kolovoza.

## Reference
https://github.com/foivz/pi22-zadace-npeterman112/blob/master/Zadatak%20-%20kampovi.pdf

## Struktura dokumenta
U drugome poglavlju opisuje se perspektiva proizvoda, njegove funkcije i ograničenja, te interakcija sa korisnicima.

U trećemu poglavlju definiraju se funkcionalni zahtjevi softvera.

U četvrtom poglavlju definirani su nefunkcionalni zahtjevi koji se uzimaju u obzir tijekom osmišljavanja arhitekture i odabira pristupa i implementacijskih tehnologija.

U petom poglavlju vizualno prikazujemo aplikaciju te njenu interakciju sa korisnicima.

## 2. Općeniti opis

## Perspektiva proizvoda

Kampiranje je zamišljen kao softversko rješenje koje bi olakšalo poslovanje u kampu, fokusirajući se na rezervacije.
Nije predviđena interakcija sa drugim sustavima, a softversko rješenje će se izvoditi na računalu krajnjeg korisnika.
A baza podataka bi trebala biti centralizirana, zbog potrebe dijeljenja podataka između vlasnika.

## Funkcije proizvoda

Od softvera Kampiranje očekuje se :

  - Ograničavanje pristupa zbog privatnosti podataka.
  - Izračun cijene.
  - Promjenjiv cjenik.
  - Pretraživanje slobodnih smještajnih jedinica ovisno o datumu.
  - Pretraživanje slobodnih smještajnih jedinica ovisno o slobodnom kapacitetu.
  - Uvid u statistiku različitih vrsta smještajnih jedinica.
  - Prikaz trenutno slobodnih/zauzetih smještajnih jedinica.
 
 
## Karakteristike korisnika
Korisnici Kampiranja su vlasnici u kampu, što znači da postoji jedna korisnička uloga, a zbog snošenja odgovornosti, svaki vlasnik će imati svoje podatke za prijavu.

## Ograničenja

Softver radi sa privatnim podacima korisnika kampa.

## Pretpostavke i ovisnosti
Cjenik je podložan promjenama, te se očekuje da promjene cjenika prate promjene potražnje i ekonomske situacije.

## Ostalo

Nema potrebe za dodatnm objašnjavanjem


## 3. Specifični funkcionalni zahtjevi

Identifikator|FZ-1|
-------------|----|
Zahtjev|Sustav omogućuje pristup samo autenficiranim korisnicima|
Obrazloženje|Zbog rada sa osjetljivim privatnim podacima gostiju, pristup podacima treba biti ograničen na vlasnike.|
Način provjere|U slučaju upisa ispravnih korisničkih podataka sustav dopušta pristup podatcima, a u slučaju upisa pogrešnih korisničkih podataka izbacuje opomenu te ne dozvoljava pristup podatcima|
Prioritet[1-5]|1|
Izvor|"Korisnički zahtjevi"|

Identifikator|FZ-2|
-------------|----|
Zahtjev| Sustav će omogućiti unos podataka o smještaju |
Obrazloženje| Vlasnici žele imati omogućen unos podataka o smještaju zbog razloga kao što je proširenje poslovanja na nove smještajne jedinice. |
Način provjere| Nakon unosa podatci trebaju biti vidljivi na listi, moguća provjera uz pomoć FZ-6 |
Prioritet[1-5]| 2 |
Izvor| "Korisnički zahtjevi" |

Identifikator|FZ-3|
-------------|----|
Zahtjev| Sustav će omogućiti izmjenu podataka o smještaju |
Obrazloženje| Zbog mogućih proširenja kampa, kvarova u kamp kućicama ili drugih razloga, vlasnici moraju biti u mogućnosti mjenjati podatke o vrsti i kapacitetu te broju smještajnih jedinica. |
Način provjere| Ako se podatak o smještaju promjeni ili izbriše, promjena treba biti vidljiva na listi ili pomoću FZ-6. |
Prioritet[1-5]| 2 |
Izvor| "Korisnički zahtjevi" |

Identifikator|FZ-4|
-------------|----|
Zahtjev| Sustav će omogućiti obračun cijene |
Obrazloženje| Obračun cijene je važna stavka za naplatu usluge. |
Način provjere| Sustav ispisuje točnu cijenu nakon rezervacije smještaja pomoću testnih podataka.|
Prioritet[1-5]| 2 |
Izvor| "Korisnički zahtjevi" |

Identifikator|FZ-5|
-------------|----|
Zahtjev| Sustav će omogućiti unost podataka o gostima |
Obrazloženje| Za rezervaciju potrebno je unijeti podatke o gostima. |
Način provjere| Nakon unosa testni podatci su vidljivi na listi ili uz pomoć FZ-8. |
Prioritet[1-5]| 2 |
Izvor| "Korisnički zahtjevi" |

Identifikator|FZ-6|
-------------|----|
Zahtjev| Sustav će omogućiti pretraživanje smještajnih jedinica |
Obrazloženje| Zbog rezerviranja, te kontrole stanja kampa, vlasnicima treba biti omogućeno pretraživanje slobodnih jedinica prema željenom kapacitetu i vremenskom periodu. Uz to je omogućen uvid u zauzete jedinice. |
Način provjere| Nakon unosa testnih podataka vidljivo je koje su jedinice ostale slobodne a koje su zauzete. |
Prioritet[1-5]| 2 |
Izvor| "Korisnički zahtjevi" |

Identifikator|FZ-7|
-------------|----|
Zahtjev| Sustav će omogućiti uvid u statistiku smještajnih jedinica |
Obrazloženje| Zbog praćenja rada kampa, te pojedinih smještajnih jedinica. |
Način provjere| Sustav treba prikazati izvještaj, kao što je ostvareni prihod, iz testnih podataka.|
Prioritet[1-5]| 3 |
Izvor| "Korisnički zahtjevi" |

Identifikator|FZ-8|
-------------|----|
Zahtjev| Sustav će omogućiti uvid u popis svih gostiju kampa |
Obrazloženje| Zbog sigurnosnih razloga potreban je uvid u trenutan popis gostiju kampa, a popis pokazuje u kojoj jedinici smještaja se gost nalazi. |
Način provjere| Sustav prikazuje popis testnih podataka. |
Prioritet[1-5]| 2 |
Izvor| "Korisnički zahtjevi" |

## Dinamika realizacije zahtjeva

 - FZ-1 -Sustav će omogućiti pristup samo autenficiranim korisnicima.
 - FZ-2 -Sustav će omogućiti unos podataka o smještaju.
 - FZ-3 -Sustav će omogućiti izmjenu podataka o smještaju.
 - FZ-4 -Sustav će omogućiti obračun cijene.
 - FZ-6 -Sustav će omogućiti pretraživanje smještajnih jedinica.
 - FZ-5 -Sustav će omogućiti unost podataka o gostima.
 - FZ-8 -Sustav će omogućiti uvid u popis svih gostiju kampa.
 - FZ-7 -Sustav će omogućiti uvid u statistiku smještajnih jedinica.

## 4. Nefunkcionalni zahtjevi

## Izgled softvera
 - NFZ-1 -Sustav će interakciju s korisnikom provoditi preko grafičkog sučelja.

## Upotrebljivost softvera
 - NFZ-2 -Sustav će ponuditi mehanizme za smanjenje mogućnosti grešaka prilikom unosa podataka.

## Performanse softvera
- NFZ-3 -Sustav će osigurati preciznost za decimalne brojeve na razini 2 decimalna mjesta.
- NFZ-4 -Sustav će biti dostupan 24 sata na dan 365 dana u godini.
- NFZ-5 -Sustav će osigurati mogućnost simultanog korištenja minimalno 4 korisnika.

## Izvođenje softvera i okruženje
- NFZ-6 -Sustav treba raditi na računalima sa instaliranim Windows 7 ili novijim operacijskim sustavima.

## Sigurnost i privatnost
- NFZ-7 -Sustav će samo vlasnicima omogućuje pristup podacima.
- NFZ-8 -Sustav će upotrebljavati podatke o gostima u skladu s odredbama GDPR-a

## Ostalo
- Nema definiranih dodatnih nefunkcionalnih zahtjeva


## 5. SKice zaslona

## Skica zaslona za prijavu u sustav



![LOGIN](https://user-images.githubusercontent.com/100710176/162805786-c6eb3ac6-0332-472f-8872-ce929b0c606e.png)


## Skica za izbornik


![izbornik](https://user-images.githubusercontent.com/100710176/162806002-5faa671d-ead1-4a89-ac49-e77583c90a82.PNG)


## Skica za unos smještajnih jedinica u sustav



![USJ](https://user-images.githubusercontent.com/100710176/162805840-877bd302-2e45-48e0-909d-b8afa29f9fa8.png)



## Skica za popis jedinica smještaja


![PJS](https://user-images.githubusercontent.com/100710176/162805869-7dcffc28-8beb-422f-a021-c95617240939.png)


## Skica za pretraživanje jedinica smještaja


![PSMJ](https://user-images.githubusercontent.com/100710176/162809907-bd2e26c1-aa17-47db-bb8c-dc8cc6017b18.PNG)



## Skica za unos gosta



![UG](https://user-images.githubusercontent.com/100710176/162805896-6d18f89c-fdcc-487f-b461-900248f90e78.PNG)

## Skica za izračun cijene

![izracuncijene](https://user-images.githubusercontent.com/100710176/162805960-df1e6e40-dc7d-49ae-9d9b-3eeae4494e5b.PNG)


## Skica za statistiku kampusa


![statistika kampusa](https://user-images.githubusercontent.com/100710176/162806113-9ef1ba2b-411a-4d4d-bac0-8e64cf6e8bfe.PNG)


## Skica za statistiku smještajne jedinice



![Statistika smještaja](https://user-images.githubusercontent.com/100710176/162806166-44580819-c303-4c49-8e43-5256bbb0b739.PNG)



## Zadatak
https://github.com/foivz/pi22-zadace-npeterman112/blob/master/Zadatak%20-%20kampovi.pdf

## Resursi
Github Markdown sintaksa dostupna je na [ovom linku](https://guides.github.com/features/mastering-markdown/) ali i na Moodleu u sekciji Zadaće.
Zadaće je obvezno predati u obliku Wiki stranica na ovom repozitoriju. Slike i druge artefakte koje ćete trabati na wiki stranicama smjestite u mapu dokumentacije u repozitoriju. 
