# Blokų grandinių technologijos 1 užduotis
# Hash generatorius

## Užduotis

* Maišos funkcijos įėjimas (angl. input) gali būti bet kokio dydžio simbolių eilutė (angl. string).
* Maišos funkcijos išėjimas (angl. output) visuomet yra to paties, fiksuoto, dydžio rezultatas (pageidautina 256 bit'ų ilgio, t.y., 64 simbolių
hex'as).
* Maišos funkcija yra deterministinė, t. y., tam pačiam įvedimui (input'ui) išvedimas (output'as) visuomet yra tas pats.
* Maišos funkcijos reikšmė/kodas (hash‘as) bet kokiai input'o reikšmei yra apskaičiuojamas greitai - efektyviai.
* Iš hash funkcijos rezultato (output'o) praktiškai neįmanoma atgaminti pradinio įvedimo (input'o).
* Maišos funkcija yra atspari "kolizijai" (angl. collision resistance), t.y., praktiškai neįmanoma surasti tokių dviejų skirtingų argumentų
, kad jiems gautume tą patį hash'ą.
* Bent minimaliai pakeitus įvedimą, pvz.vietoj "Lietuva" pateikus "lietuva", maišos funkcijos rezultatas-kodas turi skirtis iš esmės, t.y.,
tenkinamas taip vadinamas lavinos efektas (angl. Avalanche effect).

## Įdiegimo ir naudojimo instrukcija

* Įdiegimas
  * Iš skilties "releases" pasirinkti norimą programos versiją ir atsisiųsti
  * Atsisiųstą kodą sukompiliuoti per komandinę eilutę (CMD) arba naudojamu IDE
  ```
  g++ main.cpp functions.cpp md5.cpp sha256.cpp -o programa
  ```
  * Paleisti gautą vykdomąjį failą (.exe)
  ```
  ./programa
  Arba tiesiog atidaryti .exe failą tame aplanke kur atsisiuntėte programą
  ```
  
* Naudojimas
  * Pasirinkti vieną iš programos pradžioje pateikiamų funkcijų:
  * Įvedant failo pavadinimą galūnės ".txt" pridėti nereikia.

## Eksperimentinis tyrimas-analizė
* #### Palyginame dviejų failų "test1a.txt"  ir "test1b.txt", kuriuose įvesta po vieną skirtingą simbolį, gaunamą hex'ą:
![image](https://user-images.githubusercontent.com/72629961/135138277-d9784bd4-7c57-46dc-92d2-eaa8c5218ca3.png)
* #### Palyginame dviejų failų "testRandom2000a.txt" ir "testRandom2000b.txt", atsitiktinai sugeneruotų simbolių eilučių susidedančių iš 2000 simbolių, gaunamą hex'ą:
```
"testRandom2000a.txt" Hex: c06297a6c0a4f67083b280c869a568f2f281c8c0d6c9d5e472b8a999609175c6
"testRandom2000b.txt" Hex: c59383e87997b1b8b8b9627167d9677967f9a4b6c4766088b68074c3c4a0c584
```
* #### Palyginame dviejų failų "test1500a.txt" ir "test1500b.txt", simbolių eilučių susidedančių iš 1500 simbolių, tačiau besiskiriančiu tik vienu simboliu, gaunamą hex'ą:
![test1500ab](https://user-images.githubusercontent.com/72629961/135327181-e31775e7-d637-4560-896e-b610187ea86c.png)
```
"test1500a.txt" Hex: e48478c3c167f6f5a0b4a0f3f5f387857272b2959562b0b775e2a36894f384b1
"test1500b.txt" Hex: d064e595837175a8d2b0e86586c0b4e29089a7a7b0f8737477d4f7d7879999c6
```
* #### Patikriname tuščio failo gaunamą hex'ą:
![image](https://user-images.githubusercontent.com/72629961/135327426-c1de32ab-cf07-4adb-8730-51082ab2d972.png)
* #### Išmatuojame kiek laiko užtruko failo "konstitucija.txt" kiekvienos eilutės hash'inimas ir palyginame su MD5, bei SHA-256 hash funkcijų sparta:
![image](https://user-images.githubusercontent.com/72629961/135489591-9a1d2450-157e-494e-a594-50b345d50aa3.png)
* #### Tikriname hash funkcijos atsparumą kolizijai
Sugeneruota 100 000 atsitiktinių simbolių eilučių porų. 25 000 porų po 10 simbolių, 25 000 porų po 100 simbolių, 25 000 porų po 500 simbolių ir 25 000 porų po 1000 simbolių.
Neivienos poros hash'as nesutapo
![image](https://user-images.githubusercontent.com/72629961/135348904-644cf468-8bc8-4aca-9c8c-b5bf4e7c397d.png)
* #### Tikriname ar hash funkcija tenkina "Avalanche effect":
Sugeneruota 100 000 atsiktinių simbolių eilučių porų kurių ilgis 700 ir kurios skirtusi tik pirmu simboliu. Randame mažiausius ir didžiausius skirtumus bit'ų, bei hex'ų lygmenyje ir apskaičiuojame vidurkines skirtingumo reikšmes
![image](https://user-images.githubusercontent.com/72629961/135496622-a75f6b1f-ddc9-4169-8101-e04ea633f1a4.png)
## Išvados
Sukurta hash funkcija atitinka visus užduoties keliamus reikalavimus t.y:
* Hash funkcijos įvedimas galit būti bet kokio ilgio, tačiau išvedimas yra visuomet tokio paties dydžio - 64 simbolių hex'as.
* Hash funkcija yra deterministinė. Tam pačiam įvedimui visuomet toks pat išvedimas.
* Hash funkcija yra sąlyginai greita ir efektyvi, tačiau mano sukurta hash funkcija yra letesnė, nei MD5 ir SHA-256 hash funkcijos. 
* Iš hash funkcijos išvedimo, neįmanoma surasti įvesties reikšmės.
* Hash funkcija yra atspari kolizijai.
* Bent minimaliai pakeitus įvedimą, gaunama išvestis visiškai skirtinga
