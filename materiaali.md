# Materiaali

## Johdanto

Tervetuloa kurssille _Algoritmit ongelmanratkaisussa_! Tämän materiaalin tarkoituksena on auttaa sinua kurssin suorittamisessa.

Materiaali olettaa, että osaat hyvin kurssin _Tietorakenteet ja algoritmit_ asiat. Voit tarvittaessa käyttää [Tirakirjaa](https://www.cs.helsinki.fi/u/ahslaaks/tirakirja/) näiden asioiden kertaamiseen. Lisäksi materiaali olettaa, että osaat C++-kielen perusteet. Jos et ole käyttänyt ennen C++-kieltä, voit opetella perusteet esimerkiksi [Tie koodariksi -kurssilta](https://tie.koodariksi.fi/cpp/).

Voit käyttää kurssilla halutessasi C++:n sijasta myös Haskell- tai Rust-kieliä, jos olet valmis opettelemaan näihin kieliin liittyviä asioita itsenäisesti. Tämä materiaali on tehty olettaen, että käytössä on C++.

**Varoitus: Monet kurssin tehtävistä ovat vaikeita, ja kurssin suorittaminen vaatii paljon työtä ja aikaa.**

## Aloittaminen

Tarvitset kurssilla tekstieditorin, jolla voi kirjoittaa koodia, sekä C++-kääntäjän. Suositeltava kääntäjä on `g++`, joka on käytössä myös CSES-järjestelmässä, johon kurssin tehtävät palautetaan.

Tässä on esimerkkinä C++-ohjelma, joka tulostaa rivin tekstiä:

```cpp
#include <iostream>

using namespace std;

int main() {
    cout << "aybabtu\n";
}
```

Seuraavat komennot kääntävät ja suorittavat ohjelman Linux-ympäristössä:

```
$ g++ test.cpp -o test -O2
$ ./test
aybabtu
```

Tässä ohjelman koodi on tiedostossa `test.cpp` ja siitä käännetään binääritiedosto `test`. Komennon lopussa oleva `-O2` tarkoittaa, että koodi käännetään optimointitasolla 2.

## Syöte ja tuloste

Hyvä tapa lukea syötettä on käyttää `cin`-virtaa. Oletetaan esimerkiksi, että ohjelman tulee lukea ensimmäiseltä riviltä kaksi kokonaislukua `n` ja `k` ja sitten toiselta riviltä `n` kokonaislukua. Tämän voi toteuttaa seuraavasti:

```cpp
int n, k;
cin >> n >> k;
for (int i = 1; i <= n; i++) {
    int x;
    cin >> x;
}
```

Huomaa, että luettavien alkioiden välillä voi olla vapaasti tyhjää tilaa (kuten välilyöntejä ja rivinvaihtoja). Tämän ansiosta sama koodi toimii riippumatta siitä, miten tiedot on jaettu riveille.

Vastaavasti tietoa voidaan tulostaa `cout`-virtaan näin:

```cpp
cout << "aybabtu\n";
int a = 1, b = 2;
cout << a << " " << b << " " << a+b << "\n";
```

Koodin tulostus on seuraava:

```
aybabtu
1 2 3
```

Voit nyt ratkoa seuraavat tehtävät:

* [Weird Algorithm](https://cses.fi/alon/task/1068)
* [Increasing Array](https://cses.fi/alon/task/1094)
* [Two Sets](https://cses.fi/alon/task/1092)
* [Collecting Numbers](https://cses.fi/alon/task/2216)

## Tietorakenteet

C++:n tärkeä tietorakenne on `vector` eli taulukkolista, jossa on tehokasta lisätä alkio loppuun tai poistaa alkio lopusta. Vektorin käyttämiseksi koodin alussa tulee olla rivi `#include <vector>`. Seuraava koodi esittelee vektorin käyttämistä:

```cpp
vector<int> v;
v.push_back(5);
v.push_back(2);
v.push_back(8);

cout << v.size() << "\n"; // 3

cout << v[0] << "\n"; // 5
cout << v[1] << "\n"; // 2
cout << v[2] << "\n"; // 8

sort(v.begin(), v.end());

cout << v[0] << "\n"; // 2
cout << v[1] << "\n"; // 5
cout << v[2] << "\n"; // 8
```

Tietorakenne `pair` eli pari mahdollistaa kahden alkion tallentamisen. Kun vektorissa on pareja, sen sisältö järjestetään ensisijaisesti parin ensimmäisen alkion mukaan ja toissijaisesti toisen alkion mukaan:

```
vector<pair<int,int>> v;
v.push_back({5,1});
v.push_back({1,5});
v.push_back({1,2});
v.push_back({4,3});

sort(v.begin(),v.end());

cout << v[0].first << "\n"; // 1
cout << v[0].second << "\n"; // 2
cout << v[1].first << "\n"; // 1
cout << v[1].second << "\n"; // 5
cout << v[2].first << "\n"; // 4
cout << v[2].second << "\n"; // 3
cout << v[3].first << "\n"; // 5
cout << v[3].second << "\n"; // 1
```

Voit nyt ratkoa seuraavat tehtävät:

* [Concert Tickets](https://cses.fi/alon/task/1091)
* [Movie Festival](https://cses.fi/alon/task/1629)
* [Missing Coin Sum](https://cses.fi/alon/task/2183)
* [Room Allocation](https://cses.fi/alon/task/1164)
* [Josephus Problem I](https://cses.fi/alon/task/2162)
* [Subarray Distinct Values](https://cses.fi/alon/task/2162)

## Dynaaminen ohjelmointi

## Verkkojen käsittely

## Nopea eteneminen

## Pienin muutos mediaani

## Lähimmät pienimmät

## Binäärihaku

## Policy-based rakenne

## Eulerin polku

## Segmenttipuu

## Etäisyydet puussa
