#SistemskI test – Performance test (Apache JMeter)

##Datum izvedbe
**10. november 2025**

## Opis postopka izvedbe testa

Za preverjanje **nefunkcionalnih zahtev** sistema (odzivnost, zmogljivost, stabilnost) je bil izveden **sistemski performance test** s pomočjo orodja **Apache JMeter 5.6.3**.  
Test je bil izveden na lokalnem okolju, kjer teče **Spring Boot REST API** za upravljanje receptov.

Cilj testa je bil preveriti, kako se endpoint `/api/recepti/all` odziva pod obremenitvijo več uporabnikov.

### Nastavitve testa:
- **Orodje:** Apache JMeter 5.6.3  
- **HTTP metoda:** `GET`  
- **URL:** `http://localhost:8080/api/recepti/all`  
- **Število virtualnih uporabnikov (threads):** 50  
- **Ramp-up čas:** 10 sekund  
- **Število ponovitev (loop count):** 5  
- **Skupno število zahtev:** 250  

### Uporabljeni JMeter elementi:
- `Thread Group` – določitev uporabnikov in ponovitev  
- `HTTP Request` – izvedba zahteve na API endpoint  
- `View Results Tree` – prikaz posameznih odzivov  
- `View Results in Table` – prikaz meritev  
- `Summary Report` – statistični rezultati  
- `Graph Results` – vizualni prikaz hitrosti in stabilnosti sistema  

---

## 📊 Rezultati testa

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

---

## 📈 Interpretacija rezultatov

- Vse zahteve so bile **uspešno izvedene** brez napak (Error % = 0 %).  
- Povprečen odzivni čas (36 ms) je **izjemno nizek**, kar pomeni hitro odzivnost strežnika.  
- Standardna deviacija 9.9 ms kaže, da so odzivni časi **zelo stabilni**.  
- Throughput 25 zahtev/sekundo pomeni, da sistem **zmore visoko obremenitev**.  
- Grafični rezultati potrjujejo **stabilno in zanesljivo delovanje** med celotnim testom.

---

## ✅ Sklep

Sistem za upravljanje receptov je **odziven, stabilen in zmogljiv** tudi pri 50 sočasnih uporabnikih.  
Endpoint `/api/recepti/all` se v povprečju odziva v manj kot 50 ms, brez napak ali upočasnitev.  

Aplikacija tako izpolnjuje **nefunkcionalne zahteve** glede hitrosti in stabilnosti.  
Za nadaljnje preverjanje bi bilo smiselno izvesti:
- **Stress test** z večjim številom uporabnikov (npr. 200–500)  
- **Dolgotrajni stabilnostni test**, da se preveri delovanje skozi čas  

---

## 🖼️ Posnetki rezultatov (opcijsko)

Če dodajaš slike v mapo `screenshots/`, lahko vključiš naslednje:

```markdown
![Graph Results](screenshots/graph-results.png)
![Summary Report](screenshots/summary-report.png)
![View Results Table](screenshots/results-table.png)
