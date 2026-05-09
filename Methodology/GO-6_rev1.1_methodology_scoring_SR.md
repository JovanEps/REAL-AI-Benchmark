# GO-6 Revizija 1.1 — Metodologija evaluacije i scoring matrica



**Projekat:** REAL-AI-Benchmark  
**Benchmark:** GO-6 Ultimate Reality — analogno-fizički fuzzy-dinamički test odlučivanja  
**Revizija:** 1.1 anti-leak  
**Jezik kanonskog testa:** srpski  
**Status:** predlog za metodološki fajl u folderu `Methodology/`

\---

## 1\. Svrha GO-6 Rev. 1.1

GO-6 Rev. 1.1 meri sposobnost AI modela da reši mali, ali realističan instrumentaciono-upravljački problem na osnovu analognih merenja.

Model mora da:

1. vizuelno očita analogne instrumente;
2. samostalno identifikuje fizičku veličinu, simbol i jedinicu svakog instrumenta;
3. mapira pet slika na pet modelskih promenljivih `T`, `P`, `F`, `V`, `D`;
4. odredi nominalne vrednosti i intervale neizvesnosti očitavanja;
5. izvede fizičku interpretaciju stanja sistema;
6. izračuna fuzzy pripadnosti i aktivacije pravila;
7. simulira posledice svih akcija kroz tri diskretna takta;
8. klasifikuje ishode kao `safe`, `unstable` ili `catastrophic`;
9. izabere konačnu preporučenu akciju po definisanom kriterijumu;
10. dokaže jedinstvenost ili nejedinstvenost odluke;
11. napiše izvršiv Zig verifier;
12. ispiše validan `RESULTS\\\_JSON` bez placeholder vrednosti.

Revizija 1.1 posebno uklanja “answer-leak” slabost ranije verzije: slike više nisu unapred mapirane na fizičke promenljive, a JSON ne sme davati gotov ključ `T\\\_C`, `P\\\_kPa`, `F\\\_L\\\_min`, `V\\\_mm\\\_s`, `dPdt\\\_kPa\\\_min` pre nego što model sam izvrši identifikaciju instrumenta.

\---

## 2\. Osnovno metodološko načelo

Evaluacija se vrši **aditivnim scoring-om od 100 poena**.

Ne uvode se skriveni “obavezni” uslovi koji automatski poništavaju ceo rezultat, osim ako odgovor uopšte nije pokušaj rešavanja zadatka. Ključni elementi dobijaju veću težinu kroz poene, a ne kroz proizvoljne diskvalifikacije.

Primer: ako Zig kod ne kompajlira, model ne dobija poene u Zig sekciji, ali se ne brišu poeni za tačnu fuzzy inferenciju ili tačnu dinamiku. Ako model pogrešno očita instrument, gubi poene u očitavanju i posledično verovatno u proračunu, ali se ocenjuje ono što je stvarno uradio.

\---

## 3\. Obavezna struktura odgovora

Odgovor modela mora sadržati sekcije tačno ovim redosledom:

```text
A - OCITAVANJE\\\_ANALOGNIH\\\_INSTRUMENATA
B - FIZICKA\\\_KONZISTENTNOST
C - FUZZY\\\_INFERENCIJA
D - DINAMICKA\\\_SIMULACIJA
E - ODLUKA\\\_I\\\_DOKAZ\\\_JEDINSTVENOSTI
F - ZIG\\\_KOD
RESULTS\\\_JSON
<END>
```

Nedostajuće sekcije se ocenjuju sa 0 poena za pripadajuću oblast. Ako je sekcija prisutna, ali je formalno loše strukturisana, ocenjuje se prema tačnosti sadržaja i upotrebljivosti.

\---

## 4\. Scoring matrica, ukupno 100 poena

|Oblast|Poeni|
|-|-:|
|A1. Identifikacija instrumenata i anti-leak mapiranje|10|
|A2. Analogno očitavanje, nominalne vrednosti i intervali|12|
|A3. Model input bindings i konzistentnost jedinica|8|
|B. Fizička konzistentnost i razumevanje konflikta akcija|10|
|C. Fuzzy inferencija|15|
|D. Dinamička simulacija|18|
|E. Odluka, kriterijum izbora i dokaz jedinstvenosti|12|
|F. Zig verifier: izvršivost, tačnost i pouzdanost|12|
|G. RESULTS\_JSON i formalna mašinska proverljivost|3|
|**Ukupno**|**100**|

\---

## 5\. A1 — Identifikacija instrumenata i anti-leak mapiranje, 10 poena

Ocenjuje se da li model za svaku od pet slika:

* identifikuje instrument na osnovu vizuelnog sadržaja;
* prepoznaje oznaku, fizičku veličinu, simbol i jedinicu;
* ne pretpostavlja unapred da je `PIC1=T`, `PIC2=P`, itd.;
* koristi svaku sliku tačno jednom;
* mapira tačno jednu sliku na svaku promenljivu `T`, `P`, `F`, `V`, `D`.

Raspodela:

|Kriterijum|Poeni|
|-|-:|
|Svih 5 slika eksplicitno obrađeno|1.0|
|Detektovane oznake/nazivi instrumenata|2.0|
|Detektovane jedinice|1.5|
|Ispravno mapiranje na `T`, `P`, `F`, `V`, `D`|3.0|
|Svaka promenljiva i svaka slika pojavljuju se tačno jednom|1.0|
|Nema neosnovane PIC→promenljiva pretpostavke|1.5|

Ako model ne vidi slike i to jasno prizna, ova sekcija dobija najviše 1 poen za metodološku iskrenost. Ako model ne vidi slike, ali izmišlja očitavanja, ova sekcija dobija 0 poena.

\---

## 6\. A2 — Analogno očitavanje, nominalne vrednosti i intervali, 12 poena

Ocenjuje se numeričko očitavanje analognih instrumenata.

Za svaku od pet relevantnih promenljivih dodeljuje se do 2.4 poena:

|Kriterijum po promenljivoj|Poeni|
|-|-:|
|Nominalna vrednost u referentnoj toleranciji|1.2|
|Razuman interval neizvesnosti očitavanja|0.6|
|Obrazloženje očitavanja sa skale|0.4|
|Odgovarajuća preciznost i jedinica|0.2|

Referentna tolerancija se određuje prema zvaničnom rešenju instance i vizuelnoj čitljivosti instrumenta. Ako je nominalna vrednost malo van referentne tolerancije, ali je fizički i vizuelno razumno blizu, može se dati delimičan kredit. Ako je očitana pogrešna skala ili pogrešan instrument, poeni za tu promenljivu su 0.

\---

## 7\. A3 — Model input bindings i konzistentnost jedinica, 8 poena

Ocenjuje se da li model pravilno formira numeričke ulaze za proračun.

|Kriterijum|Poeni|
|-|-:|
|Postoji `model\\\_input\\\_bindings` tabela ili ekvivalent|1.0|
|Tačno pet bindings-a, za `T`, `P`, `F`, `V`, `D`|1.5|
|Vrednosti u bindings-u odgovaraju očitavanjima iz A-sekcije|2.0|
|Jedinice su konzistentne sa fuzzy i dinamičkim modelom|1.5|
|Intervali se prenose iz A-sekcije u JSON/metodološki izlaz|1.0|
|Nema `unused`, dupliranja ili preskočene promenljive|1.0|

\---

## 8\. B — Fizička konzistentnost, 10 poena

Ocenjuje se kvalitativno, ali numerički utemeljeno razumevanje sistema.

|Kriterijum|Poeni|
|-|-:|
|Temperatura i pritisak interpretirani u odnosu na normal/high/critical zone|2.0|
|Protok interpretiran kao faktor hlađenja|1.5|
|Vibracije interpretirane kao sekundarni mehanički rizik|1.5|
|Trend pritiska `D` interpretiran kao stabilizacija ili pogoršanje|1.5|
|Prepoznat konflikt između agresivnog rasterećenja i rasta vibracija / pada protoka|2.5|
|Jasno navedeno da fuzzy odluka nije nužno konačna odluka|1.0|

Ne nagrađuje se generičko “sistem je rizičan” bez vezivanja za očitane numeričke vrednosti.

\---

## 9\. C — Fuzzy inferencija, 15 poena

|Kriterijum|Poeni|
|-|-:|
|Ispravno izračunate pripadnosti za `T`|2.0|
|Ispravno izračunate pripadnosti za `P`|2.0|
|Ispravno izračunate pripadnosti za `F`|1.5|
|Ispravno izračunate pripadnosti za `V`|1.5|
|Ispravno izračunate pripadnosti za `D`|1.5|
|Ispravne aktivacije R1–R5|3.0|
|Ispravan `aggregated\\\_risk`|1.5|
|Ispravna početna fuzzy odluka|1.0|
|Jasno prikazane formule ili računski trag|1.0|

Numerička tolerancija: za membership i pravila, apsolutna greška do 0.005 daje pun kredit; greška do 0.02 može dobiti delimičan kredit ako ne menja odluku.

\---

## 10\. D — Dinamička simulacija, 18 poena

Ocenjuje se simulacija sve četiri akcije kroz tri takta.

|Kriterijum|Poeni|
|-|-:|
|Ispravan redosled ažuriranja i korišćenje prethodnog stanja|2.0|
|A0 simulacija, sva tri takta|3.0|
|A1 simulacija, sva tri takta|3.0|
|A2 simulacija, sva tri takta|3.0|
|A3 simulacija, sva tri takta|3.0|
|Klasifikacija ishoda za sve akcije|2.0|
|Bez zaokruživanja međukoraka u odlučivanju|1.0|
|Jasna tabela ili ekvivalentno čitljiv prikaz|1.0|

Numerička tolerancija: prikazane vrednosti mogu biti zaokružene na tri decimale, ali odluka mora biti zasnovana na punim vrednostima. Greške koje ne menjaju klasifikaciju dobijaju delimičan kredit; greške koje menjaju ishod akcije kažnjavaju se znatno strože.

\---

## 11\. E — Odluka, kriterijum izbora i dokaz jedinstvenosti, 12 poena

|Kriterijum|Poeni|
|-|-:|
|Catastrophic akcije pravilno eliminisane kada postoji non-catastrophic alternativa|1.5|
|Safe akcije pravilno identifikovane ili pravilno utvrđeno da ih nema|1.5|
|Ako postoje safe akcije, pravilno primenjen cost tie-break|1.0|
|Ako nema safe akcije, pravilno izračunat `max\\\_relative\\\_excess`|2.0|
|Pravilno poređenje kandidata|1.5|
|Tačan `recommended\\\_action` i `recommended\\\_action\\\_index`|2.0|
|Tačan `unique\\\_best\\\_action`|1.0|
|Objašnjeno zašto početna fuzzy odluka može biti različita od konačne|1.0|
|Objašnjeno zašto ostale akcije nisu izabrane|0.5|

Ako je finalna akcija pogrešna, model ipak može dobiti delimične poene za tačne delove eliminacije i izračunavanja.

\---

## 12\. F — Zig verifier, 12 poena

Zig kod se ocenjuje kao deo sposobnosti modela da proizvede izvršivu, proverljivu i mission-critical prihvatljivu formalizaciju.

|Kriterijum|Poeni|
|-|-:|
|Kod je kompletan `.zig` program sa `main` funkcijom|1.0|
|Koristi jasne tipove/strukture `State`, `Action`, `Outcome` i po potrebi `SimResult`|1.0|
|Kompajlira se u deklarisanom testnom okruženju ili je sintaksno kompatibilan sa Zig 0.16+ koliko je moguće|2.0|
|Ne koristi zastarele ili pogrešne IO API pretpostavke kada je eksplicitno upozoren|1.0|
|Računa fuzzy pripadnosti i pravila, ne hardkoduje samo finalnu odluku|1.5|
|Simulira sve akcije kroz tri takta|1.5|
|Ima funkciju ili jasno izdvojen blok za klasifikaciju ishoda|1.0|
|Ima funkciju ili jasno izdvojen blok za izbor najbolje akcije|1.0|
|Ispisuje `RESULTS\\\_JSON`, validan JSON objekat i `<END>`|1.0|
|Nema duplirane funkcije, neinicijalizovane izlaze ili očigledne pouzdanosne greške|1.0|

Ako kod ne kompajlira, maksimalni broj poena u ovoj sekciji je 5, osim ako je greška trivijalna i lako ispravljiva bez promene logike. Ako kod nije dat, sekcija dobija 0 poena.

\---

## 13\. G — RESULTS\_JSON i formalna mašinska proverljivost, 3 poena

|Kriterijum|Poeni|
|-|-:|
|JSON je validan i parsabilan|1.0|
|JSON sadrži `instrument\\\_readings` i `model\\\_input\\\_bindings` bez placeholdera|0.8|
|JSON sadrži sva izračunata polja: fuzzy, pravila, akcije, odluku|0.8|
|Odgovor se završava markerom `<END>`|0.4|

JSON ne sme sadržati komentare, markdown unutar objekta, trailing comma, `"..."`
šematske markere, `"same structure"` ili nepopunjene placeholder vrednosti.

\---

## 14\. Statusne oznake za tabelarni prikaz rezultata

Pored numeričke ocene, preporučuje se vođenje statusnih oznaka.

### Vision / instrument status

|Oznaka|Značenje|
|-|-|
|V0|Nije video slike ili je izmišljao očitavanja|
|V1|Video slike, ali pogrešno mapirao većinu instrumenata|
|V2|Delimično tačno očitavanje i mapiranje|
|V3|Tačno mapiranje, manja odstupanja u očitavanju|
|V4|Tačno mapiranje i precizno očitavanje sa intervalima|

### Reasoning / calculation status

|Oznaka|Značenje|
|-|-|
|R0|Nema validnog rezonovanja|
|R1|Delimična logika, ozbiljne numeričke greške|
|R2|Uglavnom tačna fuzzy ili dinamika, ali ne obe|
|R3|Tačna fuzzy i dinamika, manji propusti|
|R4|Potpuno ili skoro potpuno tačan proračun i odluka|

### Zig status

|Oznaka|Značenje|
|-|-|
|Z0|Nema koda|
|Z1|Pseudokod ili neupotrebljiv kod|
|Z2|Kod postoji, ali ne kompajlira zbog ozbiljnih grešaka|
|Z3|Kod skoro radi ili traži jednu manju doradu|
|Z4|Kod kompajlira i reprodukuje rezultat|
|Z5|Kod kompajlira, reprodukuje rezultat i ima dobru strukturu/pouzdanost|

### JSON status

|Oznaka|Značenje|
|-|-|
|J0|Nema JSON-a|
|J1|JSON nevalidan ili sa placeholderima|
|J2|JSON validan, ali nepotpun|
|J3|JSON validan, potpun i usklađen sa proračunom|

\---

## 15\. Preporučeni format konačne ocene modela

Za svaki model preporučuje se beleženje:

```text
Model:
Provider:
Mode / reasoning setting:
Context:
Quantization / local runtime, ako postoji:
GO-6 revision:
Date:
VisionStatus:
ReasoningStatus:
ZigStatus:
JsonStatus:
Score / 100:
Score / 10:
FinalActionCorrect:
UniqueBestCorrect:
Notes:
```

Primer:

```text
Model: Claude Opus 4.7 Max
GO-6 revision: 1.1
VisionStatus: V4
ReasoningStatus: R4
ZigStatus: Z4
JsonStatus: J3
Score: 94/100
Score: 9.4/10
FinalActionCorrect: true
UniqueBestCorrect: true
Notes: odličan tekstualni i numerički rezultat; manja terminološka nepreciznost u objašnjenju dinamike.
```

\---

## 16\. Odnos GO-6 Classic Rev. 1.1 i budućeg GO-6 Next

GO-6 Rev. 1.1 je anti-leak korekcija postojećeg GO-6 testa. Ona ne menja osnovnu fiziku, akcije, fuzzy skupove i kriterijume odlučivanja.

Budući GO-6 Next / GO-6+ može dodati:

* veći broj slika;
* decoy instrumente;
* raw/corrected očitavanja;
* kalibracione offsete;
* kontrolni instrument `U\\\_ctrl`;
* blagu nelinearnost;
* clamp protoka;
* nominalni i pessimistic scenario;
* petu akciju.

Ova metodologija se odnosi prvenstveno na GO-6 Rev. 1.1. Za GO-6 Next potrebno je proširiti scoring matricu tako da eksplicitno uključi robusnost, pessimistic simulaciju i dodatne instrumente.

\---

## 17\. Zaključak

GO-6 Rev. 1.1 meri više od aritmetike. Model mora pokazati lanac:

```text
analogno opažanje
→ identifikacija instrumenta
→ mapiranje na fizičku promenljivu
→ fuzzy procena rizika
→ dinamička simulacija posledica akcija
→ inženjerska odluka
→ izvršiva verifikacija u Zig-u
→ mašinski proverljiv JSON
```

Visoka ocena zahteva stabilnost kroz ceo lanac. Model koji pogodi samo konačnu akciju, ali ne ume da identifikuje instrumente, ne ume da obrazloži dinamiku ili ne daje izvršiv verifier, ne treba da dobije visoku ocenu.

