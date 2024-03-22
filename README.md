# Šifre i kodovi - Analiza algoritama za kompresiju multimedije
### Izradili: Ivan Močilac, David Škrnički, Ivana Mikulić, Marko Galavić, Amar Ademi

# Sadržaj:

## Uvod
## Algoritmi kompresije
## Lossless kompresija
### 1. Lossless algoritmi za opće korištenje
### 2. Lossless algoritmi za audio zapise
### 3. Lossless algoritmi za slike

> U ovom dokumentu ćemo vam objasniti kako današnji algoritmi vrše kompresiju nad podacima multimedije. Prije nego što započnemo htjeli bih smo vam napraviti lagani uvod koji će objasniti osnovne koncepte o kojima ćemo pričati.

# Uvod

Što je kompresija multimedije u općoj definiciji? Kompresija multimedije je proces smanjivanja veličine audio, video, slikovne ili tekstualne datoteke radi manjeg zauzimanja memorije na računalu.
Osim što imamo korist za manje opterećenje memorije, kompresija je veoma bitna i kod slanja, to jeste transmisije multimedijalnih datoteka od jednog do drugog ili više računala i samog procesiranja takvih datoteka.
Slanjem kompresirane datoteke smanjujemo opterećenje na mreži i mogućnost pogreške tokom tranzita unutar mreže prije nego što stigne do primatelja te datoteke.
Kada jednom korisnik komprimira određenu datoteku ili cijelu mapu, mora postojati nekakav način kako vratiti taj isti sadržaj prije njezine kompresije, tu ulazi termin dekompresija.
Dekompresija je proces koji vraća kompresiranu datoteku ili mapu dali ona bila multimedijalna ili ne, u njezinu originalnu veličinu.
Mnogo je koristi od dekompresije, jedna od glavnih je da primatelj poslane datoteke može pogledati cijeli sadržaj u cijelosti kao što je bilo u originalu pošiljatelja.
Sada kada imamo nekakav dojam što čemu služi, pitanje je kako implementiramo navedene procese. Implementacija se vrši koristeći algoritme za kompresiju i dekompresiju, kod kojih jedan ne može raditi bez drugoga.
