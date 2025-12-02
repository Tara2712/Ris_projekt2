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


---

CBO – Coupling Between Objects

WMC – Weighted Methods per Class

DIT – Depth of Inheritance Tree

RFC – Response for Class

LCOM – Lack of Cohesion of Methods

LOC – Lines of Code

NOF / NOM – število atributov in metod


| Razred               | LOC  | CBO | WMC | DIT | RFC | LCOM | Št. metod | Št. atributov | Interpretacija                                   |
| -------------------- | ---- | --- | --- | --- | --- | ---- | --------- | ------------- | ------------------------------------------------ |
| **Recept**           | 67   | 14  | 18  | 1   | 121 | 0.87 | 18        | 9             | Zelo kompleksen razred (RFC in LCOM zelo visoka) |
| **ReceptController** | 47   | 15  | 11  | 1   | 21  | 0    | 8         | 1             | Normalna kompleksnost controllerja               |
| **Komentar**         | 45   | 7   | 12  | 1   | 40  | 0.76 | 12        | 5             | Srednje kompleksno, visoka vključenost (RFC)     |
| **Uporabnik**        | 57   | 7   | 14  | 1   | 55  | 0.82 | 14        | 8             | Kompleksen entiteta z veliko logike              |
| **ReceptService**    | 56   | 8   | 13  | 1   | 27  | 0.42 | 7         | 2             | Normalna servisna kompleksnost                   |
| **KomentarService**  | 33   | 8   | 8   | 1   | 13  | 0.33 | 4         | 3             | Zelo normalno, nizka kompleksnost                |
| **UporabnikService** | 31   | 5   | 11  | 1   | 15  | 0    | 7         | 1             | Precej enostaven servis                          |
| **Sestavina**        | 37   | 9   | 10  | 1   | 35  | 0.80 | 10        | 5             | Kompleksen model                                 |
| **Korak**            | 30   | 10  | 8   | 1   | 20  | 0.75 | 8         | 4             | Srednja kompleksnost                             |
| **HranilnaVrednost** | 47   | 11  | 12  | 1   | 40  | 0.76 | 12        | 5             | Kompleksen model                                 |
| Ostali controllerji  | 5–10 | 2–4 | 1   | 1   | 0–2 | 0    | 1         | 0             | Minimalna kompleksnost (OK)                      |
---

| Metrika  | Mejna vrednost | Povprečje v projektu | Ocena                          |
| -------- | -------------- | -------------------- | ------------------------------ |
| **LOC**  | < 300          | 40–70                |   dobro                        |
| **CBO**  | < 14           | 5–15                 |   večinoma dobro               |
| **WMC**  | < 20           | 8–14                 |   dobro                        |
| **DIT**  | ≤ 5            | 1                    |   idealno                      |
| **RFC**  | < 50           | 10–30 (nekateri 120) |   nekateri razredi zelo visoki |
| **LCOM** | < 0.5          | 0.7–0.8              |   nizka kohesija pri entitetah |
| **NOM**  | 5–20           | 8–18                 |   normalno                     |
| **NOF**  | 0–10           | 1–9                  |   normalno                     |

---


| Razred                  | LOC | Št. metod |
| ----------------------- | --- | --------- |
| **ReceptController**    | 47  | 11        |
| **UporabnikController** | 240 | 12        |
| **KomentarController**  | 180 | 9         |
| **RisController**       | 60  | 2         |
| **TestController**      | 70  | 3         |

---

| Razred               | LOC | Št. metod |
| -------------------- | --- | --------- |
| **ReceptService**    | 260 | 10        |
| **UporabnikService** | 230 | 9         |
| **KomentarService**  | 200 | 8         |

---

| Razred               | LOC | Št. metod |
| -------------------- | --- | --------- |
| **Recept**           | 67  | 12        |
| **Sestavina**        | 120 | 10        |
| **Komentar**         | 45  | 11        |
| **Uporabnik**        | 160 | 13        |
| **HranilnaVrednost** | 140 | 11        |
| **Korak**            | 110 | 9         |

---

| Razred                         | LOC | Št. metod |
| ------------------------------ | --- | --------- |
| **ReceptRepository**           | 15  | 1         |
| **UporabnikRepository**        | 18  | 2         |
| **KomentarRepository**         | 18  | 2         |
| **SestavinaRepository**        | 12  | 1         |
| **KorakRepository**            | 12  | 1         |
| **HranilnaVrednostRepository** | 14  | 1         |

---

