# SistemskI test – Performance test (Apache JMeter)

## Datum izvedbe
**10. november 2025**

## Opis postopka izvedbe testa

### Test: Stress test
Za preverjanje nefunkcionalnih zahtev sistema (odzivnost, zmogljivost, stabilnost) je bil izveden sistemski performance test s pomočjo orodja **Apache JMeter 5.6.3**. Test je bil izveden na lokalnem okolju, kjer teče Spring Boot REST API za upravljanje receptov.

Cilj testa je bil preveriti, kako se endpoint `/api/recepti/all` odziva pod obremenitvijo več uporabnikov.

### Nastavitve testa:
- **Orodje:** Apache JMeter 5.6.3  
- **HTTP metoda:** `GET`  
- **URL:** `http://localhost:8080/api/recepti/all`  
- **Število virtualnih uporabnikov:** 50  
- **Ramp-up čas:** 10 sekund  
- **Število ponovitev:** 5  
- **Skupno število zahtev:** 250

- **Število virtualnih uporabnikov:** 100  
- **Ramp-up čas:** 5 sekund  
- **Število ponovitev:** 5  
- **Skupno število zahtev:** 500

### Uporabljeni JMeter elementi:
- `Thread Group` – določitev uporabnikov in ponovitev  
- `HTTP Request` – izvedba zahteve na API endpoint  
- `View Results Tree` – prikaz posameznih odzivov  
- `View Results in Table` – prikaz meritev  
- `Summary Report` – statistični rezultati  
- `Graph Results` – vizualni prikaz hitrosti in stabilnosti sistema  

---

## Rezultati testa

| Metrika | Vrednost |
|----------|-----------|
| Skupno število zahtev | **250** |
| Povprečen odzivni čas | **36 ms** |
| Najmanjši odzivni čas | **18 ms** |
| Največji odzivni čas | **85 ms** |
| Standardna deviacija | **9.9 ms** |
| Napake | **0 %** |
| Throughput | **25 zahtev/s** |
| Preneseni podatki (Received KB/sec) | **157.41** |
| Poslani podatki (Sent KB/sec) | **3.54** |

| Metrika | Vrednost |
|----------|-----------|
| Skupno število zahtev | **500** |
| Povprečen odzivni čas | **140 ms** |
| Najmanjši odzivni čas | **41 ms** |
| Največji odzivni čas | **270 ms** |
| Standardna deviacija | **49.6 ms** |
| Napake | **0 %** |
| Throughput | **90.3 zahtev/s** |
| Preneseni podatki (Received KB/sec) | **568.79** |
| Poslani podatki (Sent KB/sec) | **16.94** |

Vse zahteve so bile uspešno izvedene brez napak (Error % = 0 %). Povprečen odzivni čas (36 ms) je nizek, kar pomeni hitro odzivnost strežnika. Standardna deviacija 9.9 ms kaže, da so odzivni časi zelo stabilni. Throughput 25 zahtev/sekundo pomeni, da sistem zmore visoko obremenitev. 

Sistem za upravljanje receptov je odziven, stabilen in zmogljiv tudi pri 50 sočasnih uporabnikih. Endpoint `/api/recepti/all` se v povprečju odziva v manj kot 50 ms, brez napak ali upočasnitev.  


# FlavourfulFinds — Cypress Test Report

Ta dokument opisuje avtomatizirane teste, izvedene z **Cypress** za projekt *FlavourfulFinds*.  
Testi preverjajo ključne funkcionalnosti spletne aplikacije: prijavo, iskanje, nalaganje receptov in brisanje receptov z administratorskimi pravicami.

---

## Uporabljena tehnologija

| Orodje | Namen |
|--------|-------|
| **Cypress** | Avtomatizirano end-to-end testiranje |
| **JavaScript / Fetch API** | Odjemalska komunikacija s backendom |
| **Spring Boot (REST API)** | Backend storitve (avtentikacija, recepti, brisanje) |

---

## 1) Uspešna prijava uporabnika

Test preveri, ali se uporabnik z veljavnimi podatki lahko uspešno prijavi, prejme sporočilo o uspehu, shrani v localStorage in je preusmerjen na domačo stran.

## 2) Neuspešna prijava z napačnimi podatki

Test preveri, ali aplikacija pravilno zavrne napačne prijavne podatke in prikaže sporočilo o napaki (Invalid email or password).

## 3) Iskanje obstoječega recepta

Test preveri delovanje iskalnika. Po vnosu iskalnega niza mora aplikacija prikazati recept, ki ustreza vnešenemu imenu.

## 4) Prikaz receptov ob nalaganju strani

Test preveri, ali aplikacija ob odpiranju domače strani samodejno naloži recepte iz API-ja in prikaže vsaj en recept v seznamu.

## 5) Brisanje recepta (ADMIN)

Test simulira prijavljenega administratorja, preveri prikaz gumba Delete, klikne nanj in potrdi brisanje. Na koncu preveri, da recept izgine iz seznama na strani.
