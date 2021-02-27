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

### Tehtävät

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

Tietorakenne `set` on tasapainoiseen binääripuuhun perustuva joukkorakenne. Siinä alkion lisäys, poisto ja haku toimivat tehokkaasti logaritmisessa ajassa. Koska sama alkio voi esiintyä joukossa enintään kerran, funktio `count` palauttaa aina arvon 0 (alkio ei ole joukossa) tai 1 (alkio on joukossa).

```cpp
set<int> s;
s.insert(5);
s.insert(2);
s.insert(8);
s.insert(3);

cout << s.count(3) << "\n"; // 1
cout << s.count(4) << "\n"; // 0

s.erase(3);

cout << s.count(3) << "\n"; // 1
```

Joukkoa on usein kätevää käsitellä iteraattorin avulla. Iteraattori on erityinen muuttuja, joka osoittaa tiettyyn joukon alkioon. Se toimii melko samalla tavalla kuin osoitin.

Funktio `begin` antaa iteraattorin joukon ensimmäiseen alkioon ja funktio `end` antaa iteraattorin joukon viimeisen alkion _jälkeiseen_ kohtaan. Koska binääripuun sisältö on järjestyksessä, tämän avulla voidaan selvittää joukon pienin ja suurin alkio. Huomaa, että jälkimmäisessä tapauksessa iteraattorin kohtaa täytyy vähentää yhdellä, jotta päästään viimeiseen alkioon.

Funktio `lower_bound` antaa iteraattorin pienimpään alkioon, joka on yhtä suuri tai suurempi kuin annettu alkio. Funktio `upper_bound` puolestaan antaa iteraattorin alkioon, joka on suurempi kuin annettu alkio. Jos alkiota ei ole olemassa, iteraattori osoittaa viimeisen alkion jälkeiseen alkioon.

```cpp
set<int> s;
s.insert(5);
s.insert(2);
s.insert(8);
s.insert(3);

auto it1 = s.begin();
cout << *it1 << "\n"; // 2
auto it2 = s.end();
it2--;
cout << *it2 << "\n"; // 8

auto it3 = s.lower_bound(3);
cout << *it3 << "\n"; // 3
auto it4 = s.upper_bound(3);
cout << *it4 << "\n"; // 5
```

Tietorakenne `map` on avain-arvo-rakenne, joka perustuu myös tasapainoiseen binääripuuhun. Sitä voidaan käyttää seuraavasti:

```cpp
map<string,int> m;
m["apina"] = 1;
m["banaani"] = 2;
m["cembalo"] = 3;

cout << m["banaani"] << "\n"; // 1
cout << m["gorilla"] << "\n"; // 0
```

Huomaa, että kun haettu alkio puuttuu, se lisätään mukaan automaattisesti oletusarvolla. Tämän takia yllä olevassa koodissa haku avaimella "gorilla" tuottaa arvon 0.

Muita käteviä C++:n tietorakenteita ovat `deque` eli taulukkolista, jota pystyy muokkaamaan tehokkaasti sekä alusta että lopusta, sekä `multiset` eli joukkorakenne, jossa sama alkio voi esiintyä useammin kuin yhden kerran.

### Tehtävät

* [Concert Tickets](https://cses.fi/alon/task/1091)
* [Movie Festival](https://cses.fi/alon/task/1629)
* [Missing Coin Sum](https://cses.fi/alon/task/2183)
* [Room Allocation](https://cses.fi/alon/task/1164)
* [Josephus Problem I](https://cses.fi/alon/task/2162)
* [Josephus Problem II](https://cses.fi/alon/task/2163)
* [Subarray Distinct Values](https://cses.fi/alon/task/2162)

## Dynaaminen ohjelmointi

Dynaaminen ohjelmointi on keskeinen tekniikka algoritmien suunnittelussa. Siinä on ideana muotoilla ongelman ratkaisu rekursiivisesti niin, että vastaus saadaan laskemalla ratkaisut pienempiin osaongelmiin. Dynaaminen ohjelmointi on tehokasta, kunhan erilaisten osaongelmien määrä on niin pieni, että niiden vastaukset voidaan tallentaa muistiin taulukkoon.

Jos et muista hyvin, miten dynaamista ohjelmointia käytetään, sinun kannattaa lukea [Tirakirjasta](https://www.cs.helsinki.fi/u/ahslaaks/tirakirja/) luku 9, joka käsittelee kattavasti dynaamista ohjelmointia.

### Tehtävät

* [Two Sets II](https://cses.fi/alon/task/1093)
* [Rectangle Cutting](https://cses.fi/alon/task/1744)

## X

### Pienin muutos

Annettuna on `n` lukua `a[0]`, `a[1]`, ..., `a[n-1]` ja tehtävänä on löytää luku `x`, joka minimoi summan `abs(a[0]-x)+abs(a[1]-x)+...+abs(a[n-1]-x)` (tässä `abs` tarkoittaa itseisarvoa).

Osoittautuu, että sopiva `x` on aina _mediaani_ luvuista `a[0]`, `a[1]`, ..., `a[n-1]`. Tämä johtuu siitä, että jos `x` olisi pienempi kuin mediaani, sen kasvattaminen parantaisi ratkaisua, koska etäisyys pienenisi useampaan lukuun kuin suurenisi. Samasta syystä jos `x` olisi suurempi kuin mediaani, sen vähentäminen parantaisi ratkaisua.

### Lähimmät pienimmät

Annettuna on taulukko, jossa on `n` alkiota, ja tehtävänä on selvittää jokaiseen kohtaan lähin edellinen kohta, jossa on pienempi alkio. Tehtävä olisi helppo ratkaista neliöllisessä ajassa, mutta myös lineaarinen ratkaisu on mahdollinen.

Ideana on käydä läpi taulukko vasemmalta oikealle ja pitää yllä pinoa, jossa on taulukon kohtia. Joka kohdassa pinosta poistetaan kohtia niin kauan kuin nykyisessä kohdassa oleva luku on pienempi tai yhtä suuri kuin pinon kohdassa oleva luku. Tämän jälkeen tiedetään, että lähin pienempi alkio on pinossa ylimpänä olevassa kohdassa (tai pienempää alkiota ei ole, jos pino on tyhjä). Lopuksi nykyinen kohta lisätään pinoon.

Tämä algoritmi toimii lineaarisessa ajassa, koska jokainen kohta lisätään pinoon ja poistetaan pinosta vain kerran.

### Binäärihaku

Binäärihaun avulla voidaan etsiä logaritmisessa ajassa haluttu alkio järjestetystä taulukosta. Kätevä tapa toteuttaa binäärihaku on seuraava:

```cpp
int k = 0;
for (int b = n; b >= 1; b /= 2) {
     while (k+b < n && a[k+b] <= x) k += b;
}
if (a[k] == x) // alkio x löytyi kohdasta k
```

Tämä koodi etsii lukua `x` taulukosta `a`, jossa on `n` lukua. Haku lähtee liikkeelle taulukon alusta ja joka vaiheessa hypätään eteenpäin `b` askelta, jos kohteena oleva indeksi on taulukossa ja sen kohdalla oleva arvo on enintään `x`. Koodin aikavaativuus on logaritminen, koska `b` puolittuu joka kierroksella.

Käytännössä binäärihakua ei kuitenkaan tarvitse toteuttaa yleensä alkion etsimistä varten, koska C++:n standardikirjastossa on paljon valmiita työkaluja tähän (mukaan lukien funktio `binary_search`). Binäärihaun todellinen hyöty on kuitenkin siinä, että sen avulla voidaan etsiä funktion _muutoskohta_.

Oletetaan, että funktio `f(x)` saa arvon 0, kun `x` on enintään `k`, ja arvon 1, kun `x` on yli `k`. Binäärihaun avulla voidaan löytää tehokkaasti muutoskohta `k` seuraavasti:

```cpp
int k = 0;
for (int b = n; b >= 1; b /= 2) {
    while (f(k+b) == 0) k += b;
}
```

Tässä tapauksessa `n` on sopivasti valittu riittävän suuri luku, jonka tiedetään olevan suurempi kuin muutoskohta `k`.

Muutoskohdan etsimisestä on hyötyä, koska monen ongelman voi esittää muodossa "etsi ensimmäinen kohta, jossa tapahtuu jotakin" (esimerkiksi pienin aika, jossa tehdas saa valmistettua halutun määrän tuotteita). Binäärihaun avulla riittää kokeilla vain logaritminen määrä vaihtoehtoja kyseiselle kohdalle.

### Tehtävät

* [Stick Lengths](https://cses.fi/alon/task/1074)
* [Nearest Smaller Values](https://cses.fi/alon/task/1645)
* [Factory Machines](https://cses.fi/alon/task/1620)
* [Array Division](https://cses.fi/alon/task/1085)

## Verkkojen käsittely

### Tehtävät

* [Building Roads](https://cses.fi/alon/task/1666)
* [Flight Discount](https://cses.fi/alon/task/1195)
* [Investigation](https://cses.fi/alon/task/1202)
* [Mail Delivery](https://cses.fi/alon/task/1691)
* [Planets Queries I](https://cses.fi/alon/task/1750)
* [Planets Queries II](https://cses.fi/alon/task/1160)

## Segmenttipuu

Segmenttipuu on tietorakenne, jonka avulla voi toteuttaa tehokkaita välikyselyitä taulukkoon. Tavallisia välikyselyitä ovat välin summan laskeminen sekä välin pienimmän/suurimman alkion etsiminen.

### Esimerkki

Tarkastellaan esimerkkinä tilannetta, jossa haluamme tehdä välikyselyitä, joissa lasketaan taulukon alkioiden summa tietyllä välillä.

Segmenttipuu on mukavinta toteuttaa niin, että taulukon koko on 2:n potenssi. Taulukon loppuun voi tarvittaessa lisätä ylimääräisiä alkioita, jotta tämä toteutuu.

Seuraava segmenttipuu vastaa taulukkoa `[5,8,6,3,2,7,2,6]`:

TODO

Puun lehtinä ovat taulukon alkiot ja muilla tasoilla jokaisessa solmussa on kahden alemman tason solmun summa.

### Puun tallentaminen

Segmenttipuu tallennetaan taulukkona, jossa on `2n` alkiota, kun `n` on alkuperäisen taulukon koko. Kohdassa 1 on puun juuren alkio, kohdissa 2 ja 3 ovat seuraavan tason alkiot, jne. Alkuperäisen taulukon sisältö alkaa kohdasta `n`.

Esimerkin taulukkoa vastaa seuraava segmenttipuu:

```
int tree[] = {0,39,22,17,13,9,9,8,5,8,6,3,2,7,2,6};
```

Huomaa, että taulukon kohta 0 ei ole käytössä segmenttipuussa.

Tässä tallennustavassa kohdassa `k` olevan solmun vasen lapsi on kohdassa `2k`, oikea lapsi on kohdassa `2k+1` ja vanhempi on kohdassa `k/2` (pyöristys alaspäin kokonaisluvuksi). Tämä on sama tallennustapa kuin binäärikeossa käytetty.

### Alkion muuttaminen

Kun taulukon alkio muuttuu, tämän tulee heijastua kaikkiin puun solmuihin, jotka ovat polulla juuresta alkioon. Esimerkiksi seuraavassa kuvassa alkion 7 muuttuminen vaikuttaa kaikkiin harmaisiin solmuihin:

TODO

Seuraava koodi toteuttaa alkion muuttamisen:

```cpp
// muuta kohdan k arvoksi x
void change(int k, int x) {
    k += n;
    tree[k] = x;
    for (k /= 2; k >= 1; k /= 2) {
        tree[k] = tree[2*k]+tree[2*k+1];
    }
}
```

Koodi vie aikaa `O(log n)`, koska puussa on logaritminen määrä tasoja.

### Välikysely

Välikyselyssä väli muodostetaan mahdollisimman korkealla puussa olevista solmuista. Esimerkiksi kun haluamme laskea välin `[6,3,2,7,2,6]` summan, saamme sen kahdesta ylemmästä solmusta laskemalla `9+17=26`:

TODO

Seuraava koodi laskee summan annetun välin alkioiden summan:

```cpp
// laske välin a...b alkioiden summa
int getSum(int a, int b) {
    a += n; b += n;
    int s = 0;
    while (a <= b) {
        if (a%2 == 1) s += tree[a++];
        if (b%2 == 0) s += tree[b--];
        a /= 2; b /= 2;
    }
    return s;
}
```

Koodi käy läpi puun tasoja pohjalta alkaen ja lisää vasemman ja oikean alkion summaan, jos ylemmän tason solmu on välin ulkopuolella. Koodi vie aikaa `O(log n)`, koska tasojen määrä on logaritminen.

### Muut kyselyt

Segmenttipuun avulla voi toteuttaa tehokkaasti minkä tahansa kyselyn, jossa kyselyn vastauksen voi laskea jakamalla välin kahteen osaan ja yhdistämällä kummankin osan kyselyjen vastaukset.

Esimerkiksi seuraavan segmenttipuun avulla voi etsiä välin pienimmän alkion. Ideana on, että jokaisessa solmussa on minimi sen kahden lapsen arvoista.

TODO

Tällaista puuta voi käsitellä näillä funktioilla:

```cpp
// muuta kohdan k arvoksi x
void change(int k, int x) {
    k += n;
    tree[k] = x;
    for (k /= 2; k >= 1; k /= 2) {
        tree[k] = min(tree[2*k],tree[2*k+1]);
    }
}

// etsi välin a...b pienin alkio
int getMin(int a, int b) {
    a += n; b += n;
    int x = tree[a];
    while (a <= b) {
        if (a%2 == 1) x = min(x,tree[a++]);
        if (b%2 == 0) x = min(x,tree[b--]);
        a /= 2; b /= 2;
    }
    return x;
}
```

### Binäärihaku puussa

Segmenttipuuta voi myös käsitellä binäärihaun tyylisesti aloittamalla haku puun juuresta ja liikkumalla joka askeleella alaspäin vasemmalle tai oikealle.

Seuraava kuva näyttää esimerkin, kuinka äskeisestä puusta voi löytää tehokkaasti pienimmän alkion:

TODO

Vastaavalla tavalla voi esimerkiksi ylläpitää taulukkoa, jossa jokainen arvo on bitti 0 tai 1, ja etsiä summien avulla, missä on `k`:nnes bitti 1.

### Tehtävät

* [Dynamic Range Sum Queries](https://cses.fi/alon/task/1648)
* [Dynamic Range Minimum Queries](https://cses.fi/alon/task/1649)
* [Hotel Queries](https://cses.fi/alon/task/1143)
* [List Removals](https://cses.fi/alon/task/1749)
* [Increasing Subsequence](https://cses.fi/alon/task/1145)
* [Range Update Queries](https://cses.fi/alon/task/1651)
* [Nested Ranges Count](https://cses.fi/alon/task/2169)
* [Distinct Values Queries](https://cses.fi/alon/task/1734)

## Puiden käsittely

### Tehtävät

* [Tree Diameter](https://cses.fi/alon/task/1131)
* [Tree Distances I](https://cses.fi/alon/task/1132)
* [Tree Distances II](https://cses.fi/alon/task/1133)
* [Company Queries I](https://cses.fi/alon/task/1687)
* [Company Queries II](https://cses.fi/alon/task/1688)
* [Distance Queries](https://cses.fi/alon/task/1135)
* [Finding a Centroid](https://cses.fi/alon/task/2079)
