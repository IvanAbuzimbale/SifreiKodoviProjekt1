# Šifre i kodovi - Analiza algoritama za kompresiju multimedije
### Izradili: Ivan Močilac, David Škrnički, Ivana Mikulić, Marko Galavić, Amar Ademi

# Sadržaj:

### 1. Uvod
### 2. Algoritmi kompresije
### 3. Lossless kompresija:
---
#### 1. Lossless algoritmi za opće korištenje
#### 2. Lossless algoritmi za audio zapise
#### 3. Lossless algoritmi za fotografije
---
### Što je bitrate i koliko je važan
---
#### Razlika između lossy i lossless u praksi
---


> U ovom dokumentu ćemo vam objasniti kako današnji algoritmi vrše kompresiju nad podacima multimedije. Prije nego što započnemo htjeli bih smo vam napraviti lagani uvod koji će objasniti osnovne koncepte o kojima ćemo pričati.

# Uvod
---
Što je kompresija multimedije u općoj definiciji? Kompresija multimedije je proces smanjivanja veličine audio, video, slikovne ili tekstualne datoteke radi manjeg zauzimanja memorije na računalu.
Osim što imamo korist za manje opterećenje memorije, kompresija je veoma bitna i kod slanja, to jeste transmisije multimedijalnih datoteka od jednog do drugog ili više računala i samog procesiranja takvih datoteka.
Slanjem kompresirane datoteke smanjujemo opterećenje na mreži i mogućnost pogreške tokom tranzita unutar mreže prije nego što stigne do primatelja te datoteke.
Kada jednom korisnik komprimira određenu datoteku ili cijelu mapu, mora postojati nekakav način kako vratiti taj isti sadržaj prije njezine kompresije, tu ulazi termin dekompresija.
Dekompresija je proces koji vraća kompresiranu datoteku ili mapu dali ona bila multimedijalna ili ne, u njezinu originalnu veličinu.
Mnogo je koristi od dekompresije, jedna od glavnih je da primatelj poslane datoteke može pogledati cijeli sadržaj u cijelosti kao što je bilo u originalu pošiljatelja.
Sada kada imamo nekakav dojam što čemu služi, pitanje je kako implementiramo navedene procese. Implementacija se vrši koristeći algoritme za kompresiju i dekompresiju, kod kojih jedan ne može raditi bez drugoga.

# Algoritmi kompresije
---
Postoje dva tipa algoritama za kompresiju:
1. Lossless compression (Kompresija bez gubitka)
2. Lossy compression (Kompresija sa gubitkom)

## Lossless kompresija:
---
Ova vrsta kompresije smanjuje veličinu podataka bez gubitka informacija. Kada se podaci dekomprimiraju, identični su izvornoj informaciji. Najbolji primjer takvog algoritma su Run-lenght encoding (RLE), Huffman enkodiranje, Deflate i Burrows – Wheeler transformacijski algoritam.
Kompresija bez gubitaka je moguća jer većina podataka iz stvarnog svijeta pokazuju statističku redundantnost.

Statistička redundantnost u kompresiji bez gubitka odnosi se na ponavljajuće obrasce ili predvidljive strukture koje postoje unutar podataka.

Na primjer, u tekstualnim podacima, određena slova ili kombinacije slova mogu se pojavljivati češće od drugih. Algoritam za kompresiju može dodijeliti kraće kodove ovim uobičajenim obrascima, čime se smanjuje ukupna veličina podataka.

Većina programa za kompresiju bez gubitaka radi dvije stvari u nizu: prvi korak generira statistički model za ulazne podatke, a drugi korak koristi ovaj model za mapiranje ulaznih podataka u sekvence bitova.

Primarni algoritmi kodiranja koji se koriste za proizvodnju nizova bitova su Huffmanovo kodiranje (također ga koristi algoritam deflate) i aritmetičko kodiranje.

Aritmetičko kodiranje postiže stope kompresije blizu najboljih mogućih za određeni statistički model, dok je Huffmanova kompresija jednostavnija i brža, ali daje loše rezultate za modele koji se bave vjerojatnostima simbola blizu 1.

Postoje dva primarna načina konstruiranja statističkih modela: u statičkom modelu podaci se analiziraju i konstruira se model, zatim se taj model pohranjuje s komprimiranim podacima.

Ovaj pristup je jednostavan i modularan, ali ima nedostatak što sam model može biti skup za skladištenje tj. zauzimati će više memorije. Forsira korištenje jednog modela za sve podatke koji se komprimiraju, pa ima lošu izvedbu na datotekama koje sadrže heterogene podatke.

Za razliku od statičkih modela, prilagodljivi modeli (adaptive models) dinamički ažuriraju model kako se podaci komprimiraju.

Nijedan algoritam kompresije bez gubitaka ne može učinkovito komprimirati sve moguće podatke. Iz tog razloga postoje mnogi različiti algoritmi koji su dizajnirani po vrsti ulaznih podataka ili s određenim pretpostavkama o tome koju će vrstu redundantnosti nekomprimirani podaci vjerojatno sadržavati.

---

## Lossless algoritmi za opće korištenje:
1.	ANS
2.	Aritmetičko enkodiranje
3.	Burrows – Wheeler transformacijski algoritam
4.	RLE
5.	Huffmanovo enkodiranje

## Lossless algoritmi za audio zapise:
1.	ATRAC
2.	Apple lossless (ALAC)
3.	Free Lossless Audio Codec (FLAC)
4.	Waveform Audio Format (WAV)
5.	DTS-HD Master
6.	Meridian lossless packing
7.	Monkeys audio
8.	Direct system transfer (DST)
9.	Dolby TrueHD

## Lossless algoritmi za fotografije:
1.	HEIF
2.	JPEG-XL
3.	JPEG-XR
4.	PNG
5.	WebP
6.	AVIF

# Što je bitrate i koliko je važan
---
Bitrate se odnosi na brzinu kojom se digitalni podaci prenose ili procesiraju. Izražava se u jedinici bitova po sekundi (symbol: bit/s), često u kombinaciji sa SI prefiksom kao što su kilo (1 kbit/s = 1.000 bita/s) ili mega (1 Mbit/s = 1.000 kbit/s).

Bitrate je ključan koncept kod digitalnih audio i video datoteka jer direktno utječe na njihovu kvalitetu i veličinu.

Viši bitrate obično znači veću kvalitetu zvuka ili slike jer omogućava prenos više digitalnih informacji po sekundi.

Niži bitrate rezultiraju manjim datotekama, ali i potencijalno lošijom kvalitetom.

Na primjer, audio datoteka s većim bitrateom će imati bogatiji zvuk i više detalja nego datoteka s nižim bitrateom. Slično tome, video datoteka s visokim bitrateom će pružiti oštrije i jasnije slike u odnosu na video s nižim bitrateom.

## Razlika između lossy i lossless u praksi

### Lossless kompresija:

Čuva sve originalne podatke, osiguravajući identičnu kvalitetu zvuka kao i nekomprimirani zapis. Očekivani omjer kompresije je 20-30% smanjenja veličine datoteke.

### Lossy kompresija:

Koriste se tehnike poput PAC-a za odbacivanje podataka koje ljudsko uho teško ili uopće ne može čuti. To rezultira značajno manjim datotekama (obično 70-95% smanjenja), idealnim za pohranu i streaming. Očekivati je gubitak kvalitete zvuka, posebno na visokim frekvencijama.

#### Primjeri:

Lossless formati:
1. FLAC
2. ALAC
3. WAV

Lossy formati:
1. MP3
2. AAC
3. OGG

Zaključak:

Izbor kompresije ovisi o specifičnim potrebama. Lossless je idealan za očuvanje originalne kvalitete zvuka, dok je lossy praktičniji za optimizaciju veličine datoteke. Razumijevanje prednosti i nedostataka obje metode pomaže u donošenju informirane odluke o kompresiji audio zapisa.


| Pitanje           | Lossless kompresija                          | Lossy kompresija                               |
|-------------------|----------------------------------------------|------------------------------------------------|
| Čuva kvalitetu?   | Da                                           | Ne, dio podataka se gubi                       |
| Smanjna veličina? | U manjoj količini (20% - 30%)                | U većoj količini (70% - 95%)                   |
| Korisno za?       | Ključne datoteke (dokumenti, programski kod) | Multimediju (fotografije, glazba, videozapisi) |

