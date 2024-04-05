# Šifre i kodovi - Analiza algoritama za kompresiju multimedije
### Izradili: Ivan Močilac, David Škrnički, Ivana Mikulić, Marko Galavić, Amar Ademi

# Sadržaj:

### 1. Uvod
### 2. Algoritmi kompresije
### 3. Lossless kompresija
### 4. Huffmanovo kodiranje
### 5. Lossless algoritmi za opće korištenje
### 6. Audio kompresija
### 7. Što je bitrate i koliko je važan
### 8. Zaključak

---

> U ovom dokumentu ćemo vam objasniti kako današnji algoritmi vrše kompresiju nad podacima multimedije. Prije nego što započnemo htjeli bih smo vam napraviti lagani uvod koji će objasniti osnovne koncepte o kojima ćemo pričati.
---
### Uvod
---
Što je kompresija multimedije u općoj definiciji? Kompresija multimedije je proces smanjivanja veličine audio, video, slikovne ili tekstualne datoteke radi manjeg zauzimanja memorije na računalu.

Osim što imamo korist za manje opterećenje memorije, kompresija je veoma bitna i kod slanja, to jeste transmisije multimedijalnih datoteka od jednog do drugog ili više računala i samog procesiranja takvih datoteka.

Slanjem kompresirane datoteke smanjujemo opterećenje na mreži i mogućnost pogreške tokom tranzita unutar mreže prije nego što stigne do primatelja te datoteke.

Kada jednom korisnik komprimira određenu datoteku ili cijelu mapu, mora postojati nekakav način kako vratiti taj isti sadržaj prije njezine kompresije, tu ulazi termin dekompresija.

Dekompresija je proces koji vraća kompresiranu datoteku ili mapu dali ona bila multimedijalna ili ne, u njezinu originalnu veličinu.

Mnogo je koristi od dekompresije, jedna od glavnih je da primatelj poslane datoteke može pogledati cijeli sadržaj u cijelosti kao što je bilo u originalu pošiljatelja.

Sada kada imamo nekakav dojam što čemu služi, pitanje je kako implementiramo navedene procese.

Implementacija se vrši koristeći algoritme za kompresiju i dekompresiju, kod kojih jedan ne može raditi bez drugoga.

---
#### Algoritmi kompresije
Postoje dva tipa algoritama za kompresiju:
1. Lossless kompresija (Kompresija bez gubitka)
2. Lossy kompresija (Kompresija sa gubitkom)
---
#### Lossless kompresija:
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

#### Huffmanovo kodiranje:

---
U računalnoj znanosti i teoriji informacija, Huffmanov kod je posebna vrsta optimalnog prefiks koda koji se obično koristi za kompresiju podataka bez gubitaka. Proces pronalaženja ili korištenja takvog koda je Huffmanovo kodiranje. Izlaz iz Huffmanovog algoritma može se promatrati kao kodna tablica varijabilne duljine za kodiranje izvornog simbola.

Algoritam ovu tablicu izvodi iz procijenjene vjerojatnosti ili učestalosti pojavljivanja (težine) za svaku moguću vrijednost izvornog simbola. Kao i kod drugih metoda entropijskog kodiranja, češći simboli općenito se predstavljaju s manje bitova od manje uobičajenih simbola.

Huffmanovo kodiranje koristi specifičnu metodu za odabir reprezentacije za svaki simbol, što rezultira kodom prefiksa. Huffmanovo kodiranje je toliko raširena metoda za stvaranje prefiks kodova da se izraz "Huffmanov kod" naširoko koristi kao sinonim za "prefiks kod" čak i kada takav kod ne proizvodi Huffmanov algoritam.

Tehnika funkcionira stvaranjem binarnog stabla čvorova. Oni se mogu pohraniti u pravilnom nizu, čija veličina ovisi o broju simbola n.

Čvor može biti lisni čvor ili unutarnji čvor. U početku, svi čvorovi su lisni čvorovi, listovi, koji sadrže sam simbol, težinu (učestalost pojavljivanja) simbola i vezu na nadređeni čvor što olakšava čitanje koda (obrnuto) počevši od listova.

Unutarnji čvorovi sadrže težinu, veze na dva podređena čvora i izbornu vezu na nadređeni čvor. Kao uobičajena konvencija, bit '0' predstavlja praćenje lijevog djeteta, a bit '1' predstavlja praćenje desnog djeteta.

Proces počinje s čvorovima lista koji sadrže vjerojatnosti simbola koji predstavljaju. Zatim, proces uzima dva čvora s najmanjom vjerojatnošću i stvara novi interni čvor koji ima ta dva čvora kao djecu.

Težina novog čvora postavljena je na zbroj težine djece. Zatim ponovno primjenjujemo postupak, na novom unutarnjem čvoru i na preostalim čvorovima, ponavljamo ovaj postupak sve dok ne ostane samo jedan čvor, koji je korijen Huffmanovog stabla.

---
#### LZ77 kompresija:
---
Je algoritam kompresije temeljen na rječniku koji traži ponovljene obrasce u ulaznim podacima. Zamjenjuje ove obrasce referencama na prethodna pojavljivanja.

Algoritam koristi klizni prozor za traženje podudaranja. Traži najdulje podudaranje za svaku poziciju u ulaznim podacima.

Kada se pronađe podudaranje, algoritam zamjenjuje odgovarajući niz pokazivačem na prethodno pojavljivanje tog niza.

Kompresija PNG formata:
Algoritam kompresije koji se koristi u PNG-u zove se Deflate, što je kombinacija LZ77 (Lempel-Ziv 1977) i Huffmanovog kodiranja.

Prije kompresije, slikovni podaci se pretprocesiraju kako bi se optimizirali za kompresiju. To može uključivati pretvaranje slikovnih podataka u određeni prostor boja (kao što je RGB ili sive tonove) i izvođenje operacija filtriranja radi poboljšanja kompresivnosti.

Deflate kompresija je proces u dva koraka:

1. Kompresija LZ77: Ovaj korak uključuje pronalaženje ponovljenih uzoraka (nizova bajtova) unutar slikovnih podataka i njihovu zamjenu referencama na prethodna pojavljivanja.

2. Huffmanovo kodiranje: Nakon kompresije LZ77, rezultirajući tok podataka dalje se komprimira korištenjem Huffmanovog kodiranja. Huffmanovo kodiranje dodjeljuje kodove promjenjive duljine različitim simbolima na temelju njihove učestalosti pojavljivanja, pri čemu se simbolima koji se češće pojavljuju dodjeljuju kraći kodovi. Ovaj korak optimizira kodiranje komprimiranih podataka.

PNG organizira slikovne podatke u dijelove, od kojih svaki služi određenoj svrsi. Komprimirani slikovni podaci koje generira Deflate algoritam pohranjuju se u jedan ili više IDAT (Image Data) dijelova. Ovi dijelovi sadrže komprimirane podatke o pikselima, zajedno s metapodacima potrebnim za dekodiranje slike.

Kada se PNG slika dekodira, Deflate komprimirani slikovni podaci pohranjeni u IDAT dijelovima dekomprimiraju se obrnutim postupkom. To uključuje prvo primjenu Huffmanovog dekodiranja za dobivanje LZ77-komprimiranih podataka, a zatim izvođenje LZ77 dekompresije za rekonstrukciju izvornih slikovnih podataka.

LZW (Lempel-Ziv-Welch) algoritam kompresije:
Algoritam za kompresiju podataka bez gubitaka koji radi zamjenjivanje ponavljajućih uzoraka podataka kraćim kodovima. Razvili su ga Abraham Lempel, Jacob Ziv i Terry Welch 1980-ih.

Počinje s korakom inicijalizacije gdje stvara rječnik koji preslikava sve moguće ulazne simbole u njihove odgovarajuće binarne kodove. U početku, ovaj rječnik sadrži unose za svaki pojedinačni simbol u ulaznim podacima.

Nakon toga skenira ulazne podatke i traži ponovljene uzorke simbola. Kako nailazi na nizove simbola, provjerava jesu li ti nizovi već prisutni u rječniku.

Ako se niz pronađe u rječniku, LZW nastavlja skenirati najduži niz koji se već nalazi u rječniku. Zatim šalje kod koji odgovara tom nizu.

Ako niz nije pronađen u rječniku, LZW ga dodaje u rječnik i ispisuje kod koji odgovara najdužem nizu koji je do sada pronađen (isključujući trenutni simbol).

Ovaj proces se nastavlja dok se ne obrade cjelokupni ulazni podaci.

Tijekom dekodiranja, komprimirani podaci se čitaju, a kodovi se preslikavaju natrag u svoje odgovarajuće nizove simbola pomoću istog rječnika koji se koristi tijekom kodiranja. Kako se nailaze na nove kodove, oni se dodaju u rječnik.

Dekodiranje se nastavlja čitanjem kodova iz komprimiranih podataka i ispisivanjem odgovarajućih nizova simbola.

Izlaz LZW algoritma je tok kodova promjenjive duljine koji predstavljaju komprimirane podatke.

---

#### Lossless algoritmi za opće korištenje:

---
1. ANS
2. Aritmetičko enkodiranje
3. RLE
4. Huffmanovo enkodiranje

---
#### Lossless algoritmi za slike:
---
1. PNG (Portable Network Graphic) - PNG je naširoko korišten format kompresije bez gubitaka za slike. Koristi kombinaciju tehnika kompresije, uključujući Deflate kompresiju, za smanjenje veličine datoteke bez gubitka slikovnih podataka. Deflate kompresija nudi ravnotežu između učinkovitosti kompresije i računalne složenosti, što je čini prikladnom za širok raspon primjena. Njegova učinkovitost je u njegovoj sposobnosti identificiranja i uklanjanja suvišnih informacija uz očuvanje cjelovitosti izvornih podataka.

2. GIF (Graphics Interchange Format) - GIF podržava kompresiju bez gubitaka za slike s do 256 boja. Kompresiju postiže korištenjem LZW (Lempel-Ziv-Welch) algoritma kompresije, koji je učinkovit za slike s velikim područjima pune boje.

3. TIFF (Tagged Image File Format) -  podržava kompresiju bez gubitaka i kompresiju sa gubitcima, ali se često koristi s kompresijom bez gubitaka za potrebe arhiviranja ili kada se mora očuvati kvaliteta slike. Nudi različite metode kompresije uključujući LZW, ZIP i PackBits.

4. BMP ((Bitmap) -  datoteke koje se mogu komprimirati korištenjem tehnika kompresije bez gubitaka kao što je RLE (Run-Length Encoding). BMP datoteke obično su veće od drugih formata, čak i nakon kompresije.

5. WebP - WebP je relativno noviji format slike koji je razvio Google. Podržava i kompresiju s gubicima i bez gubitaka. WebP kompresija bez gubitaka temelji se na predviđanju vrijednosti piksela i entropijskom kodiranju.

---

Lossy algoritmi za slike:
1. JPEG
2. WebP
3. HEIF (High Efficiency Image File Format)
4. AVIF (AV1 Image File Format)

---
#### JPEG (Joint Photographhic Experts Group)
---
Ovo je jedan od najčešće korištenih formata za slike na internetu.

Lossy algoritam za kompresiju koji kao rezultat daje znatno manju količinu podataka sa vrlo malom (ako ikakvom) vizualnom promjenom kvalitete slike i rezolucije. 

JPEG funkcionira tako da se maknu informacije koje nije lako vidjeti golim okom te istovremeno zadržajući informacije koje se vrlo lako vide.

Koraci pretvorbe sliku u JPEG:

![image](https://github.com/IvanAbuzimbale/SifreiKodoviProjekt1/assets/58472137/f985660e-41f1-469b-8b7e-f441e7a11f14)

- Kako bi pogledali .jpg datoteku koristeći image viewer, tu datoteku moramo dekodirati. 
- Kako bi se ta slika morala prikazati image viewer mora proći po ovim gore navedenim koracima u obrnutom redoslijedu.
 
---
#### WebP
---
Ovaj lossy algoritam kompresije je napravio Google u 2013. da se natječe s jpg-om za format fotografija, pa zato i imaju nekoliko sličnosti između njih. 

Najprije se slika podijeli na makroblokove te se za svaki makroblok koristi model za predviđanje, odnosno filtriranje, WebP primjenjuje filtriranje koristeći medotu bloka, a to se postiže definiranjem dvaju skupova piksela oko bloka: redak iznad bloka A i stupac lijevo od bloka L.

![image](https://github.com/IvanAbuzimbale/SifreiKodoviProjekt1/assets/58472137/a5f3aacc-1f2a-420e-b058-516d9c245db4)


 
Koristeći A i L, koder će ispuniti testni blok od 4x4 piksela i odrediti koji će proizvesti vrijednosti koje su najsličnije izvoru.

Zatim se izračunava razlika između predviđenih i stvarnih vrijednosti piksela (residual), ova razlika predstavlja informacije koje se ne mogu precizno predvidjeti.

Nakon toga slijedi entropijsko kodiranje, koristeći najčešće tehnika poput arihmetičkog kodiranja koje će dodijeliti kraće kodove simbolima koje se češto pojavljuju, što će na kraju rezultirati daljnjoj kompresiji podataka. 

Prosjek u uštedi podataka između WebP i JPEG-a je između 20 i 35%.

---
#### HEIF (High Efficiency Image File Format)
---
HEIF je format koji koristi moderne tehnike kompresije kojima se pohranjuju pojedinačne slika na kompaktan i visokokvalitetan način.

Cilj HEIF-a je poboljšati postojeće formate slika poput JPEG-a, nudeći bolju kompresiju i naprednije značajke.

Kod ovog lossy načina HEIF koristi tehnike poput prediktivnog, trasformacijskog i entropijskog kodiranja za smanjenje veličina datoteka uz očuvanje vizualne kvalitete.

Ovim načinom se znatno brišu nepotrebne podatke i efikasnije se kompresiraju slike.

Prednosti HEIF-a su: veća efikasnost kompresije, poboljšana kvaliteta slike, podrška za napredne postavke, fleksibilnost i mogućnost prilagodbe za buduće tehnologije kompresije 

---
#### AVIF (AV1 Image File Format)
---
AVIF je moderan format slike koji implementira tehnologiju video kompresije kodeka AV1 kako bi se postigle učinkovite kompresije slika.

Kod ovog lossy načina AVIF kompresira sliku koristeći nekoliko tehnika. 

Najprije se koristi predviđanje unutar okvira (intra-frame prediction) kako bi se predvidjele vrijednosti unutra okvira na temelju susjednih piksela.

Onda se koristi transformacijsko kodiranje koje pomaže koncentrirati energiju slike u manje koeficijenata, time podaci postaju podložniji kompresiji.
Zatim slijedi kvantizacija. Ovim postupkom se transformirani koeficijenti zaokruže na manju skup vrijednosti. Kod ovog koraka se gube informacije (lossy).

Sljedeći korak je entropijsko kodiranje. Tu se koristeći tehnikama poput aritmetičkog kodiranja dodeljuju kraći kodovi simbolima koje se češto pojavljuju, što će na kraju rezultirati daljnjoj kompresiji podataka. 

---
### Audio kompresija:
---
Kompresija audio podataka, koju ne treba pomiješati s kompresijom dinamičkog raspona, ima potencijal smanjiti propusnost prijenosa i zahtjeve za pohranu audio podataka.

Formati kompresije zvuka implementirani su u softver kao audio kodeksi. U kompresiji s gubicima i bez gubitaka redundancija informacija je smanjena, korištenjem metoda kao što su kodiranje, kvantizacija, DCT i linearno predviđanje kako bi se smanjila količina informacija korištenih za predstavljanje nekomprimiranih podataka.

Linearno predviđanje je matematička operacija u kojoj se buduće vrijednosti signala u diskretnom vremenu procjenjuju kao linearna funkcija prethodnih uzoraka.

U digitalnoj obradi signala, linearno predviđanje često se naziva linearno prediktivno kodiranje (LPC) i stoga se može promatrati kao podskup teorije filtera.

Teorija filtera što je povezana sa dizajnom filtra je proces dizajniranja filtra za obradu signala koji zadovoljava skup zahtjeva, od kojih neki mogu biti proturječni. Svrha je pronaći realizaciju filtra koja zadovoljava svaki od zahtjeva u dovoljnoj mjeri da bude koristan.

---
#### Lossy algoritmi za audio zapise:
---
Kompresija zvuka s gubitkom koristi se u širokom rasponu aplikacija. Uz samostalne audio aplikacije za reprodukciju datoteka u MP3 playerima ili računalima. digitalno komprimirani audio tokovi koriste se u većini video DVD-ova, digitalnoj televiziji, strujanju medija na internetu, satelitskom i kabelskom radiju, a sve više kod zemaljskim radijskim emisijama.

Kompresija s gubicima obično postiže daleko veću kompresiju od kompresije bez gubitaka, odbacivanjem manje kritičnih podataka na temelju psihoakustičkih optimizacija. Ovi se algoritmi gotovo svi oslanjaju na psihoakustiku kako bi eliminirali ili smanjili vjernost manje čujnih zvukova, čime se smanjuje prostor potreban za njihovo pohranjivanje ili prijenos.

Psihoakustika je grana psihofizike koja uključuje znanstveno proučavanje percepcije zvuka i audiologije — kako ljudski slušni sustav percipira različite zvukove.

Psihoakustika prepoznaje da ljudski slušni sustav ne može percipirati sve podatke u audio streamu. Kompresija s najvećim gubitkom smanjuje redundanciju tako što prvo identificira perceptualno irelevantne zvukove, to jest zvukove koje je teško čuti.

Tipični primjeri uključuju visoke frekvencije ili zvukove koji se pojavljuju u isto vrijeme kad i glasniji zvukovi. Ti nevažni zvukovi kodirani su sa smanjenom točnošću ili uopće nisu kodirani.

Prihvatljivi kompromis između gubitka kvalitete zvuka i veličine prijenosa ili pohrane ovisi o aplikaciji.

Na primjer, jedan kompaktni disk (CD) od 640 MB sadrži otprilike jedan sat nekomprimirane glazbe visoke vjernosti, manje od 2 sata glazbe komprimirane bez gubitaka ili 7 sati glazbe komprimirane u MP3 formatu pri srednjoj bitnoj brzini.

Digitalni snimač zvuka obično može pohraniti oko 200 sati jasno razumljivog govora u 640 MB.

Zbog prirode algoritama s gubicima, kvaliteta zvuka trpi gubitak digitalne generacije kada se datoteka dekomprimira i ponovno komprimira.

Neprikladan za pohranjivanje međurezultata u profesionalnim audiotehničkim aplikacijama, kao što je uređivanje zvuka i snimanje s više zapisa.

Međutim, formati s gubitkom kao što je MP3 vrlo su popularni među krajnjim korisnicima jer je veličina datoteke smanjena na 5-20% izvorne veličine, a megabajt može pohraniti otprilike jednu minutu glazbe odgovarajuće kvalitete.

---
#### Metode audio algoritama kompresije sa gubitkom:
---
Kako bi se utvrdilo koje su informacije u audio signalu perceptivno irelevantne, većina algoritama kompresije s gubitkom koristi transformacije kao što je MDCT za pretvaranje uzorkovanih valnih oblika u vremenskoj domeni u domenu transformacije, obično frekvencijsku domenu.

MDCT: Modificirana diskretna kosinusna transformacija je dizajniran za izvođenje na uzastopnim blokovima većeg skupa podataka, pri čemu se naredni blokovi preklapaju tako da se zadnja polovica jednog bloka podudara s prvom polovicom sljedećeg bloka.

Ovo preklapanje, uz kvalitetu sažimanja energije DCT-a, čini MDCT posebno atraktivnim za aplikacije kompresije signala, budući da pomaže u izbjegavanju artefakata koji proizlaze iz granica blokova.

Artefakt kompresije je primjetno izobličenje medija (uključujući slike, zvuk i video) uzrokovano primjenom kompresije s gubitkom.

Nakon transformacije, frekvencije komponenti mogu se odrediti prema tome koliko su čujne.

Čujnost spektralnih komponenti procjenjuje se pomoću apsolutnog praga sluha i principa simultanog maskiranja, proces u kojem je signal maskiran drugim signalom odvojenim frekvencijom i, u nekim slučajevima, vremenskim maskiranjem, gdje je signal maskiran drugim signalom odvojenim vremenom.

1. MP3
2. AAC (Advanced Audio Coding)
3. Ogg Vorbis
4. Opus
5. WMA (Windows Media Audio)

---
#### MP3:
---
Audio signal se najprije uzorkuje na određenoj frekvenciji (npr. 44,1 kHz za zvuk CD kvalitete), a zatim se dijeli na male frame-ove. Svaki frame predstavlja kratki segment audio signala, dug oko 26 milisekundi.

Za svaki okvir, algoritam primjenjuje modificiranu diskretnu kosinusnu transformaciju (MDCT) za pretvaranje uzoraka u vremenskoj domeni u podatke u frekvencijskoj domeni
MP3 algoritam koristi psihoakustičke modele kako bi identificirao koji se dijelovi audio signala mogu sigurno ukloniti bez značajnog utjecaja na percipiranu kvalitetu zvuka.

Preostale frekvencijske komponente se zatim kvantiziraju, što znači da su njihove vrijednosti aproksimirane kako bi se smanjila količina podataka potrebnih za njihovo predstavljanje.

Nakon kvantizacije, algoritam koristi Huffmanovo kodiranje, oblik entropijskog kodiranja, za daljnju kompresiju podataka. Huffmanovo kodiranje dodjeljuje kraće kodove češćim elementima i duže kodove rjeđim elementima, optimizirajući ukupnu veličinu kodiranih podataka.

Komprimirani podaci, zajedno s potrebnim zaglavljem i informacijama za provjeru pogrešaka, zatim se kodiraju u MP3 okvir. Svaki okvir također sadrži malo preklapanje zvuka sa susjednim okvirima kako bi se spriječile zvučne praznine ili artefakti na granicama.

Razina kompresije može se podesiti putem bitrate (brzine prijenosa) postavke, mjereno u kilobitima po sekundi (kbps). Veći bitrate znače manju kompresiju (a time i veću kvalitetu), dok niži bitrate rezultiraju manjim datotekama i lošijom kvalitetom.

---
#### AAC:
---
Koristi tehnike perceptivnog kodiranja za uklanjanje suvišnih i manje čujnih dijelova audio signala.

Kao nadogradnja na MP3, AAC za analizu karakteristika audio signala koristeći psihoakustičke modele.

AAC dijeli audio signal u male blokove, obično 1024 ili 2048 uzoraka svaki. Za svaki blok primjenjuje transformaciju vremensko-frekvencijske domene, često koristeći modificiranu diskretnu kosinusnu transformaciju (MDCT), za pretvaranje audio uzoraka iz vremenske domene u frekvencijsku domenu.

U frekvencijskoj domeni, AAC kvantizira audio podatke kako bi smanjio broj bitova potrebnih za predstavljanje svakog uzorka. Kvantizacija uključuje aproksimaciju vrijednosti amplitude komponenti frekvencije, obično s većom preciznošću za komponente koje su perceptualno važnije i nižom preciznošću za one koje su manje čujne.

Nakon kvantizacije, AAC koristi tehnike entropijskog kodiranja, kao što su Huffmanovo kodiranje i aritmetičko kodiranje, za daljnju kompresiju audio podataka.

AAC podržava različite konfiguracije kanala, uključujući mono, stereo i višekanalni zvuk. Za stereo i višekanalni zvuk, koristi tehnike kao što su Joint Stereo i Mid-Side Stereo za učinkovito kodiranje prostornih audio informacija.

AAC podržava skalabilnost brzine prijenosa, što omogućuje kodiranje više verzija istog audio sadržaja pri različitim brzinama prijenosa unutar iste datoteke. To omogućuje prilagodljivo strujanje i učinkovitu isporuku audio sadržaja preko mreža s različitim uvjetima propusnosti.

---
#### Ogg Vorbis:
---
Ogg Vorbis je format kompresije zvuka otvorenog koda koju je razvila Zaklada Xiph.Org.
Slično drugim modernim algoritmima za kompresiju zvuka, Ogg Vorbis dijeli audio signal u male blokove i provodi transformaciju vremensko-frekvencijske domene.

Također kao prije navedeni algoritmi, Ogg Vorbis koristi psihoakustičke modele za analizu karakteristika audio signala i utvrđivanje koje su komponente manje čujne ili suvišne.

Ogg Vorbis podržava kodiranje s promjenjivom brzinom prijenosa (VBR), što omogućuje dinamičku dodjelu bitova na temelju složenosti audio signala. Tijekom kodiranja, više bitova se dodjeljuje složenim segmentima audio signala s visokofrekventnim sadržajem ili brzim promjenama, dok se manje bitova dodjeljuje jednostavnijim segmentima.

Ogg Vorbis koristi fleksibilnu veličinu bloka, obično u rasponu od 64 do 4096 uzoraka po bloku, što mu omogućuje prilagodbu različitim vrstama audio sadržaja. Preklapanje između susjednih blokova pomaže smanjiti artefakte na granicama blokova i poboljšati ukupnu kvalitetu zvuka.

Ogg Vorbis koristi tehniku zvanu residue coding za predstavljanje razlike između originalnog audio signala i rekonstruiranog signala nakon kvantizacije. Učinkovitim kodiranjem ostatka, Ogg Vorbis postiže bolju kompresiju uz zadržavanje kvalitete zvuka.

Za stereo i višekanalni zvuk, Ogg Vorbis koristi tehnike spajanja kanala kako bi smanjio redundantnost između kanala i poboljšao učinkovitost kompresije.

---
#### Opus:
---
Opus je vrlo svestran i učinkovit format kompresije zvuka koji je razvila Internet Engineering Task Force (IETF) kao RFC 6716. Optimiziran je za širok raspon audio aplikacija, uključujući komunikaciju u stvarnom vremenu, strujanje i pohranu. Kodek Opus postiže nisku latenciju, visoku učinkovitost kompresije i izvrsnu kvalitetu zvuka u širokom rasponu brzina prijenosa.

Opus koristi hibridni pristup kodiranja koji kombinira linearno prediktivno kodiranje (LPC) i tehnike kodiranja temeljene na transformaciji. Koristi SILK (Super wideband) i CELT (Constrained Energy Lapped Transform) kodekse koji su optimizirani za govor i opće audio signale.

Opus dijeli audio signal u kratke okvire koji se preklapaju i na svaki okvir primjenjuje transformaciju vremensko-frekvencijske domene. Koristi modificiranu diskretnu kosinusnu transformaciju (MDCT) za spektralnu analizu.

Opus dinamički dodjeljuje bitove različitim frekvencijskim pojasima i okvirima na temelju karakteristika audio signala. Prilagođava dodjelu bitova u stvarnom vremenu kako bi se prilagodio promjenama u audio sadržaju i postigao optimalnu učinkovitost kompresije.

Opus uključuje specifične algoritme za rukovanje prolaznim zvukovima, kao što su perkusijski ili brzo promjenjivi signali. Koristi tehnike kao što su prijelazno predviđanje i window switching za točan prikaz prolaznih događaja uz minimiziranje izobličenja.

Opus pakira komprimirane audio podatke u male okvire, obično u rasponu od 2,5 do 60 milisekundi. Uključuje robusne mehanizme za ispravljanje pogrešaka i prikrivanje za ublažavanje učinaka gubitka paketa i pogrešaka u prijenosu u umreženim okruženjima.

Opus podržava kodiranje s promjenjivom brzinom prijenosa (Variable Bitrate), što mu omogućuje dinamičku prilagodbu brzine prijenosa na temelju složenosti audio signala.
Izlaz algoritma kompresije Opus je komprimirani audio tok ili datoteka, obično kodirana ekstenzijom ".opus".

---
#### WMA:
---
Windows Media Audio (WMA) niz je vlasničkih audio kodeksa koje je razvio Microsoft.

WMA koristi psihoakustičke modele za analizu karakteristika audio signala. Kao i velika većina lossy algoritama kompresije, WMA koristi modificiranu diskretnu kosinusnu transformaciju (MDCT). Nakon transformacije frekvencijske domene, WMA kvantizira frekvencijske koeficijente kako bi smanjio broj bitova potrebnih za njihovo predstavljanje.

WMA koristi Huffmanovo kodiranje kao tehniku entropijskog kodiranja za daljnju kompresiju kvantiziranih podataka.

WMA podržava različite konfiguracije kanala, uključujući mono, stereo i višekanalni zvuk.
Za stereo i višekanalni zvuk, WMA može koristiti tehnike kao što je zajedničko stereo kodiranje ili stereo kodiranje srednje strane kako bi se smanjila redundantnost između kanala i poboljšala učinkovitost kompresije.

Izlaz algoritma WMA kompresije je komprimirana audio datoteka s nastavkom ".wma". Ova datoteka sadrži kodirane audio podatke, zajedno s metapodacima i informacijama zaglavlja potrebnim za dekodiranje.

---
### Lossless algoritmi za audio zapise:
---
Kompresija zvuka bez gubitaka stvara prikaz digitalnih podataka koji se mogu dekodirati u točan digitalni duplikat izvornika. Omjeri kompresije su oko 50-60% izvorne veličine.
1. MPEG-4 SLS
2. ALAC (Apple Lossless Codecs)
3. Dolby TrueHD
4. APE (Monkey's Audio)
5. WavPack

---
#### MPEG-4 SLS:
---
MPEG-4 SLS (Scalable Lossless Coding) algoritam je kompresije zvuka bez gubitaka standardiziran od strane Moving Picture Experts Group (MPEG) kao dio MPEG-4 skupa standarda za audio kodiranje. Dizajniran je za pružanje visokokvalitetne kompresije audio podataka bez gubitaka, što ga čini prikladnim za aplikacije u kojima je očuvanje vjernosti zvuka kritično.

MPEG-4 SLS koristi linearno predviđanje za modeliranje vremenskih i spektralnih karakteristika audio signala.
Linearno predviđanje uključuje predviđanje budućih uzoraka audio signala na temelju prošlih uzoraka, korištenjem modela linearnog filtera. Ovo pomaže u uklanjanju redundantnosti audio podataka.

Nakon linearnog predviđanja, MPEG-4 SLS primjenjuje tehnike entropijskog kodiranja za daljnju kompresiju preostalih audio podataka.

MPEG-4 SLS uključuje bešumne tehnike kodiranja za učinkovito kodiranje preostalih audio podataka bez unošenja bilo kakvog izobličenja ili gubitka informacija. To osigurava da kodirani zvuk ostaje vjeran izvornom, nekomprimiranom audio signalu.

MPEG-4 SLS omogućuje i sloj s gubicima i sloj za korekciju bez gubitaka sličan Wavpack Hybrid, OptimFROG DualStream i DTS-HD Master Audio, pružajući kompatibilnost unatrag s MPEG AAC-kompatibilnim bitstreamovima. MPEG-4 SLS također može raditi bez sloja s gubicima, u kojem slučaju neće biti kompatibilan s prethodnim verzijama.

---
#### ALAC:
---
Razvijen od strane Apple Inc. 2004. za kompresiju audio podataka bez gubitaka. Nakon što je prvotno bio zaštićen od svog početka 2004., Apple je krajem 2011. omogućio kodek otvorenog koda.

ALAC podržava do 8 audio kanala na 16, 20, 24 i 32 bita dubine s maksimalnom brzinom uzorkovanja od 384 kHz.

ALAC podaci često se pohranjuju unutar MP4 spremnika s nastavkom naziva datoteke ".m4a".

ALAC nije varijanta AAC-a (koji je format s gubicima), već nepovezani format bez gubitaka koji koristi linearno predviđanje (slično drugim kodeksima bez gubitaka).

ALAC koristi tehnike prediktivnog modeliranja za analizu audio signala i predviđanje budućih audio uzoraka na temelju prošlih uzoraka.

Predviđanjem vrijednosti audio uzoraka, ALAC može prepoznati i iskoristiti redundancije u audio podacima, što pomaže u postizanju kompresije bez gubitka informacija. 

Linearno predviđanje uobičajena je tehnika koja se koristi u algoritmima kompresije zvuka bez gubitaka, uključujući ALAC.

Uključuje modeliranje audio signala kao linearne kombinacije prošlih uzoraka, korištenjem filtra predviđanja. Koeficijenti filtra predviđanja optimizirani su za smanjenje pogreške predviđanja, što rezultira učinkovitom kompresijom.

Nakon linearnog predviđanja, rezidualni audio podaci (razlika između predviđenih i stvarnih audio uzoraka) kodirani su Riceovim kodiranjem ili sličnom tehnikom entropijskog kodiranja.

Rice kodiranje je vrsta kodiranja promjenjive duljine koja dodjeljuje kraće kodove simbolima koji se češće pojavljuju, a duže kodove rjeđim simbolima, čime se smanjuje ukupna brzina prijenosa kodiranog audio toka.

ALAC obrađuje audio podatke u blokovima uzoraka, umjesto da kodira cijeli audio tok kao jednu kontinuiranu sekvencu.

Dekomprimirani audio podaci su bit-po-bit identični izvornom nekomprimiranom zvuku, osiguravajući da nema gubitka kvalitete tijekom reprodukcije.
 
---
#### Dolby TrueHD:
---
Dolby TrueHD je višekanalni audio kodek bez gubitaka koji su razvili Dolby Laboratories, koji se uglavnom koristi u Blu-ray Disc i kompatibilnom hardveru. Dolby TrueHD specifikacija omogućuje do 16 diskretnih audio kanala, svaki s brzinom uzorkovanja do 192 kHz i dubinom uzorkovanja do 24 bita.

Dolbyjev mehanizam kompresije za TrueHD je Meridian Lossless Packing (MLP)

Meridian Lossless Packing - je standardna metoda kompresije bez gubitaka za DVD-Audio sadržaj i obično pruža oko 1,5:1 kompresiju na većini glazbenih materijala. Svi DVD-Audio uređaji opremljeni su sa MLP dekodiranjem.

Dolby TrueHD bitstream nosi programske metapodatke ili ne-audio informacije koje dekoder koristi za modificiranje svoje interpretacije audio podataka. Metapodaci mogu uključivati normalizaciju zvuka ili kompresiju dinamičkog raspona.

U specifikaciji Blu-ray Disca, Dolby TrueHD zapisi mogu prenositi do 8 diskretnih audio kanala (7.1 surround) 24-bitnog zvuka na 96 kHz ili do 6 kanala (5.1 surround) na 192 kHz. 

Maksimalna brzina prijenosa audio streama uključujući metapodatke je 18 Mbit/s (trenutačno, budući da je promjenjiva brzina prijenosa), a TrueHD okvir je dugačak 1/1200 sekundi.

Dolby TrueHD počinje s izvornim PCM zvukom, koji predstavlja nekomprimirani audio signal kao niz digitalnih uzoraka. PCM je standardni format za digitalni audio, koji se koristi za audio snimanje i reprodukciju visoke vjernosti.

Dolby TrueHD koristi tehnike kompresije bez gubitaka kako bi smanjio veličinu datoteke PCM zvuka bez gubitka kvalitete zvuka. Za razliku od algoritama kompresije s gubitkom, koji odbacuju neke audio informacije kako bi postigli kompresiju, Dolby TrueHD čuva sve izvorne audio podatke.

Dolby TrueHD podržava promjenjivu dubinu bitova, što mu omogućuje kodiranje zvuka s različitim razinama preciznosti.

Veća dubina bita omogućuje točniji prikaz audiodinamike i tiše odlomke, što rezultira poboljšanom vjernošću zvuka. 

Dolby TrueHD koristi tehnike prediktivnog modeliranja za analizu audio signala i predviđanje budućih audio uzoraka na temelju prošlih uzoraka, prepoznavanjem obrazaca i redundancija u audio podacima.

Nakon prediktivnog modeliranja, rezidualni audio podaci kodirani su pomoću tehnika entropijskog kodiranja.

Podržava različite konfiguracije kanala, uključujući stereo, surround zvuk i objektni zvuk.

Tijekom reprodukcije, zvuk kodiran Dolby TrueHD dekodira se pomoću kompatibilnog dekodera, poput Blu-ray playera ili AV prijemnika. Dekoder rekonstruira izvorni PCM zvuk iz komprimiranih podataka.

---
#### APE:
---
Datoteke kodirane u APE-u (Monkey's Audio) obično se smanjuju na otprilike polovicu izvorne veličine, s time da se vrijeme prijenosa podataka i zahtjevi za pohranu smanjuju u skladu s tim.

Kao i svaka shema kompresije bez gubitaka, Monkey's Audio format zauzima nekoliko puta više prostora od formata kompresije s gubitkom, otprilike dvostruko više od MP3 datoteke brzine 
prijenosa od 320 kbit/s. Dobra strana je da se podaci ne gube u usporedbi s ulaznom datotekom, što kodeksi bez gubitaka čine pogodnima za transkodiranje.

U odnosu na Apple Lossless Audio Codec ili WavPack, Monkey's Audio sporije kodira i dekodira datoteke. Iako Monkey's Audio može postići visoke omjere kompresije, cijena je dramatično povećanje zahtjeva na kraju dekodiranja.

Većina kodeksa bez gubitaka je asimetrična, što znači da posao obavljen radi postizanja viših omjera kompresije, usporava proces kodiranja, ali u biti nema učinka na zahtjeve dekodiranja.

U procesu kompresije Monkey's Audio koristi tehnike prediktivnog modeliranja za analizu audio signala i predviđanje budućih uzoraka na temelju prošlih uzoraka. Primjenjuje filtre linearnog predviđanja na audio signal s ciljem uklanjanja suvišnih informacija. Nakon predviđanja i filtriranja, rezidualni audio podaci kodirani su pomoću Riceovog kodiranja. 

Monkey's Audio obično obrađuje audio podatke u blokovima uzoraka, umjesto da kodira cijeli audio tok kao jednu kontinuiranu sekvencu. Monkey's Audio podržava različite konfiguracije kanala.

Izlaz algoritma Monkey's Audio kompresije je komprimirana audio datoteka s ekstenzijom ".ape".

Komprimirana datoteka sadrži kodirane audio podatke, zajedno s metapodacima i informacijama zaglavlja potrebnim za dekodiranje.

---
#### WavPack:
---
WavPack je besplatni format audio kompresije otvorenog koda bez gubitaka i aplikacija koja implementira format. Jedinstven je po tome što podržava hibridnu kompresiju zvuka uz normalnu kompresiju koja je slična načinu na koji radi FLAC. Također podržava komprimiranje širokog spektra formata bez gubitaka, uključujući različite varijante PCM-a i DSD-a koji se koriste u SACD-ovima, zajedno sa podrškom za surround zvuk.

WavPack kompresija može komprimirati 8, 16, 24 i 32-bitne PCM audio datoteke s fiksnom točkom i 32-bitne pokretne točke u formatu datoteke ".WAV".
Također može rukovati DSD ulazom u DSDIFF ili DSF formatu. Također podržava strujanje surround zvuka i visoke stope uzorkovanja.

Kako bi osigurao rad velike brzine, WavPack koristi prediktor koji je u potpunosti implementiran u cjelobrojnoj matematici. U "brzom" načinu rada predviđanje je jednostavno aritmetička ekstrapolacija prethodna dva uzorka.

Umjesto Rice kodiranja, koristi se poseban koder podataka za WavPack. Rice kodiranje je optimalno bit kodiranje za ovu vrstu podataka, a WavPackov koder je manje učinkovit, ali samo za oko 0,15 bita po uzorku (ili manje od 1% za 16-bitne podatke). Međutim, postoje neke prednosti u zamjeni. Prvi je da WavPackov koder ne zahtijeva da se podaci spremaju u međuspremnik prije kodiranja; umjesto toga pretvara svaki uzorak izravno u bit kodove.

Također uključuje "hibridni" način rada, koji i dalje pruža značajke kompresije bez gubitaka, ali stvara dvije datoteke: relativno malu, visokokvalitetnu datoteku s gubitkom (.wv) koja se može koristiti sama; i "ispravnu" datoteku (.wvc) koja, u kombinaciji s datotekom s gubitkom, omogućuje potpunu obnovu bez gubitaka. To omogućuje korištenje kodeksa bez gubitaka i kodeksa bez gubitaka zajedno.

Hibridni način rada može rukovati podacima s pomičnim zarezom, ali samo kada nisu prisutne "iznimke" kao što su beskonačnosti ili NaN. Ne može obraditi DSD jer ne postoji algoritam s gubicima za DSD.

U načinu rada bez gubitaka, WavPack koristi tehnike prediktivnog modeliranja za analizu audio signala i predviđanje budućih uzoraka na temelju prošlih uzoraka.

Koristi modeliranje konteksta i adaptivno entropijsko kodiranje za kodiranje preostalih audio podataka.

U načinu rada s gubitkom, WavPack generira ispravnu datoteku (.wvc) uz komprimiranu audio datoteku (.wv), koja sadrži dodatne informacije potrebne za rekonstrukciju izvornog audio signala.

Datoteka za ispravak omogućuje reverzibilnu konverziju zvuka komprimiranog s gubitkom natrag u izvorni audio signal, iako uz određeni gubitak kvalitete.

WavPack podržava različite konfiguracije kanala, uključujući mono, stereo i višekanalni zvuk.

---
# Što je bitrate i koliko je važan
---
Bitrate se odnosi na brzinu kojom se digitalni podaci prenose ili procesiraju. Izražava se u jedinici bitova po sekundi (symbol: bit/s), često u kombinaciji sa SI (Međunarodni sustav mjernih jedinica) prefiksom kao što su kilo (1 kbit/s = 1.000 bita/s) ili mega (1 Mbit/s = 1.000 kbit/s).

Bitrate je ključan koncept kod digitalnih audio i video datoteka jer direktno utječe na njihovu kvalitetu i veličinu.

Veći bitrate obično znači veću kvalitetu zvuka ili slike jer omogućava prijenos više digitalnih informacji po sekundi.

Niži bitrate rezultiraju manjim datotekama, ali i potencijalno lošijom kvalitetom.

Na primjer, audio datoteka s većim bitrateom će imati bogatiji zvuk i više detalja nego datoteka s nižim bitrateom. Slično tome, video datoteka s visokim bitrateom će pružiti oštrije i jasnije slike u odnosu na video s nižim bitrateom.

---
##### Usporedba bitratea:
---
Za usporedbu korištena je pjesma "Pubic Enemy" iz videoigre "Devil May Cry". Audio je uzet sa službenog CD-a s pjesmama. Izvorna kvaliteta zvuka je standardni CD (1411 kbps), te je kompresiran u tri različita bitrate-a:
1. 33 kbps
2. 78 kbps
3. 101 kbps

Audio se može pronaći na sljedećoj poveznici: [Šifre i kodovi - Analiza algoritama za kompresiju multimedije](https://drive.google.com/drive/folders/12xwZvfYPN3AL-ZPqupZ1JehIhrPCAiE8?usp=sharing)

Također, napravljena je usporedba audia kroz spektar koristeći program "Audacity".

<img width="1280" alt="image" src="https://github.com/IvanAbuzimbale/SifreiKodoviProjekt1/assets/58472137/b01ac6c6-f2ca-4cf9-a664-531191f415ec">

Spektri su posloženi od najlošije kvalitete prema najboljoj (od gore prema dolje).

- **33 kbps** (MP3): Ovo je najlošija kvaliteta zvuka zbog niskog bitrate-a. Spektar pokazuje značajan gubitak visokih frekvencija.

- **78 kbps** (MP3): Kvaliteta zvuka je malo bolja od 33 kbps, ali je i dalje loša. Spektar pokazuje malo više detalja nego prijašnji.

- **101 kbps** (MP3): Kvaliteta zvuka je dosta poboljšana u usporedbi sa prvotnim primjerom. Spektar pokazuje malo više detalja i bolje očuvanje visokih frekvencija.

- **1411 kbps** (WAV): Ovo je najveća kvaliteta zvuka od svih četiriju datoteka. WAV format je lossless, što znači da se čuvaju svi originalni podaci audio zapisa. Spektar je bogat i detaljan, predstavljajući izvorni audio signal.

---
### Zaključak
---


Izbor kompresije ovisi o specifičnim potrebama. Lossless je idealan za očuvanje originalne kvalitete zvuka, dok je lossy praktičniji za optimizaciju veličine datoteke. Razumijevanje prednosti i nedostataka obje metode pomaže u donošenju informirane odluke o kompresiji audio zapisa.



| Pitanje            | Lossless kompresija                          | Lossy kompresija                               |
|--------------------|----------------------------------------------|------------------------------------------------|
| Čuva kvalitetu?    | Da                                           | Ne, dio podataka se gubi                       |
| Smanjena veličina? | U manjoj količini (50% - 60%)                | U većoj količini (70% - 95%)                   |
| Korisno za?        | Ključne datoteke (dokumenti, programski kod) | Multimediju (fotografije, glazba, videozapisi) |


Neki od lossless algoritama su:

- WAV
- FLAC
- ALAC


Neki od lossy algoritama su:

- MP3
- OGG
- AAC
