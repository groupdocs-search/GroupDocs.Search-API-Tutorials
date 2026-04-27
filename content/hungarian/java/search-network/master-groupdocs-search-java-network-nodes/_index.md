---
date: '2026-01-19'
description: Tanulja meg, hogyan szerezhet ideiglenes licencet, telepítheti és kezelheti
  a keresőhálózati csomópontokat a GroupDocs.Search for Java-val, javítva a dokumentumkeresést.
keywords:
- GroupDocs.Search for Java
- search network nodes
- document management system
title: Ideiglenes licenc beszerzése a GroupDocs.Search Java csomópontokhoz
type: docs
url: /hu/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

Docs.Search for Java segítségé feligvezeti a konfiguráció beállításán, több csomópont telepítésén, valamint mindent a könyvtárak indexelésétől a saját dokumentumattribútumok hozzáadásáig – miközben pontosan megmutatja, hogyan szerezhet ideiglenes licencet, amikor készen áll a megoldás tesztelésére.

## Gyors válaszok
- **Mi a első lépés a GroupDocs.Search használatának megkezdéséhez?** Szerezzen be egy ideiglenes licencet a GroupDocs portálról.  
- **Melyik Maven tároló tartalmazza a könyvtárat?** `https://releases.groupdocs.com/search/java/`.  
- **Hogyan adhatok könyvtárakat az indexeléshez?** Használja a `addDirectoriesToIndex` segédfüggvényt a master csomóponton.  
- **Hozzáadhatok saját dokumentumattribútumokat?** Igen – hívja meg az `addAttribute` metódust a dokument tisztán a cs meg a `closeNodes` metódust az erőforrások felszabadításához.

of‑concept projektekhez, mielőtt teljes vásárlásra kerülne sor.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg arról, hogy az alábbi előfeltételek rendelkezésre állnak:

### Szükséges könyvtárak és függőségek
A GroupDocs.Search for Java használatához adja hozzá a szükséges Maven függőségeket:
```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```
A legújabb verziót letöltheti közvetlenül a [GroupDocs.Search for Java kiadások](https://releases.groupdocs.com/search/java/) oldaláról.

### Környezet beállítása
- Győződjön meg róla, hogy kompatibilos lesz. Ha újonc kezdéshez.

## Hogyan szerezhet ideiglenes licencet
1. Látogassa meg a **[GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)** oldalt.  
2. Töltse ki a rövid kérvényformot e‑mail címmel és a projekt részleteivel.  
3. Kapja meg a licencfájlt e‑mailben, és helyezze el a projekt **resources** mappájában.  
4. Töltse be a licencet az alkalmazás indításakor (az alábbi kódrészlet egy tipikus inicializálást mutat).

## A GroupDocs.Search for Java beállítása

### Telepítési információk
A GroupDocs.Search for Java projektbe való integrálásához kövesse a fentebb leírt Maven lépéseket, vagy töltse le a legújabb verziót közvetlenül a hivatalos kiadási oldalról.

#### Licenc beszerzési lépések
1. **Ingyenes próba** – Fedezze fel a funkciókat kötelezettség nélkül.  
2. **Ideiglenes licenc** – Szerezzen rövid távú kulcsot a teszteléshez (lásd a fenti szakaszt).  
3. **Vásárlás** – Termeléshez vásároljon teljes licencet a **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)** oldalon.

### Alapvető inicializálás és beállítás
Inicializálja a projektet a GroupDocs.Search segítségével a következő módon:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```
Ez az inicializálási lépés elengedhetetlen ahhoz, hogy minden komponens zökkenőmentesen működjön a keresési hálózatban.

## Implementációs útmutató
Most bontsuk le a folyamatot kezelhető szakaszokra, amelyek mindegyike egy adott funkcióra fókuszál a keresési hálózati csomópontok telepítésében és kezelésében.

### Funkció 1: Konfiguráció beállítása
**Áttekintés:** A keresési hálózat konfigurációjának beállítása az első lépés a csomópontok telepítésekor. Ez a beállítás magában foglalja az útvonalak és portok megadását, amelyek kritikusak a csomópontok telepítéséhez.

#### Implementációs lépések:
##### 1. lépés: Alapútvonal és port meghatározása
```java
String basePath = "/path/to/config";
int basePort = 8080;
```
##### 2. lépés: Keresési hálózat konfigurálása
A `configureSearchNetwork` függvény előkészíti a csomópontok telepítéséhez szükséges konfigurációs objektumot.
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```
- **Paraméterek:** Az alapútvonal és a port a források megtalálásához és a kommunikációs csatornák létrehozásához szükséges.  
- **Visszatérési érték:** Egy konfigurált `Configuration` objektum, amely az Ön telepítési igényeire van szabva.

### Funkció 2: Keresési hálózat telepítése
**Áttekintés:** A csomópontok telepítése elengedhetetlen a keresési képességek skálázásához különböző környezetekben vagy adatcsoportokban.

#### Implementációs lépések:
##### 1. lépés: Csomópontok telepítése
A `deploySearchNetwork` függvény inicializálja és egy tömböt ad vissza a keresési hálózati csomópontokkal.
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```
- **Paraméterek:** Alapútvonal, port és konfiguráció határozza meg a telepítési környezetet.  
- **Visszatérési érték:** Egy tömb, amely a inicializált `SearchNetworkNodes` elemeket tartalmazza.

### Funkció 3: Hálózati eseményekre való feliratkozás
**Áttekintés:** A keresési hálózat tevékenységeinek nyomon követése kulcsfont és a megbízhpés: Feliratkozás a master csomópont eseményeire
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```
- **Cél:** Ez a lépés biztosítja, hogy értesüljön a keresési hálózat jelentős eseményeiről vagy változásairól Dokumentumok indexelése
**Áttekintés:** A dokumentumokat tartalmazó könyvtárak hozzáadása az indexeléshez lehetővé teszi az adatok hatékony visszakeresését a hálózaton belomóponton lévő segédmetódust, hogy a motor a kívánt mappákra mutasson.
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```
- **Cél:** Gyors hozzáférést és kereshetőséget biztosít a megadott könyvtárakban lévő összes dokumentumhoz.

### Funkció 5: Attribútumok hozzáadása dokumentumokhoz
**Áttekintés:** Az egyedi attribútumok bővítik a dokumentum metaadatait, így a keresések rugalmasabbak és informatívabbak lesznek.

#### Hogyan adjon egyedi dokumentumattribútumokat
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```
- **Paraméterek:** Adja meg a csomópontot, a dokumentum kulcsát és a hozzáadandó attribútumot.  
- **Cél:** A keresési funkcionalitás kiterjesztése további metaadatokkal gazdagított dokumentumokkal.

### Funkció 6: Indexelt dokumentumok lekérdezése
**Áttekintés:** Hatékonyan lekérdezheti és felsorolhatja az indexelt dokumentumokat, biztosítva az adat pontosságát és teljességét.

#### Implementációs lépések:
##### 1. lépés: Indexelt dokumentumok lekérése
```java
getIndexedDocuments(nodes[0]);
```
- **Cél:** Ellenőrzi, hogy a szükséges összes dokumentum sikeresen indexelve lett-e a keresési hálózatban.

### Funkció 7: Hálózati csomópontok lezárása
**Áttekintés:** A csomópontok megfelelő lezárása elengedhetetlen az erőforrások kezelése és a memória‑szivárgások megelőzése érdekében.

#### Implementációs lépések:
##### 1. lépés: Minden csomópont lezárása
```java
closeNodes(nodes);
```
- **Cél:** Felszabadítja az egyes csomópontok által foglalt erőforrásokat, biztosítva a tiszta leállási folyamatot.

## Gyakorlati alkalmazások
Néhány valós példát sorolunk fel, ahol a GroupDocs.Search for Java segítségével a keresési hálózati csomópontok kezelése rendkívül hasznos lehet:
1. **Vállalati dokumentumkezelés** – Javítsa a dokumentumkeresést nagy szervezetekben, több részleg között történő indexeléssel és kereséssel.  
2. **E‑commerce platformok** – Növelje a termékkeresés hatékonyságát azáltal, hogy gyorsan hozzáfér a különböző szervereken tárolt kiterjedt katalógusokhoz.  
3. **Jogász irodák** – Könnyítse a peres ügyek kutatását azáltal, hogy hatalmas mennyiségű jogi dokumentumot rendez áttekinthetően kereshető foglalják a CRM platformokat, tartalomkezelő rendszereket (CMS) és adat‑analitikai eszközöket, kihasználva a GroupDocs.Search for Java által nyújtott robusztus indexelési és keresési funkciókatbeli megfontolások
A GroupDocs.Search for Java használatakor a teljesítmény optimalizálásához:
- **Konfiguráció optimalizálása** – Igazíts szűkében.  
- **Legjobb gyakorlatok követése** – Tartsa be a Java memória‑kezelési irányelveket, biztosítva aak hatékony felhasználását.

## Gyakran ismételt kérdések

**K: Mennyi ideig érvényes egy ideiglenes licenc?**  
V: Az ideiglenes licencek általában 30 napig érvényesek,K: Át tudok-e váltani egy ideiglenes licencből, licenc csak a felhasználási jogokat szabályozza.

**K: Mi történik, ha elfelejtem lezárni a csomópontokat?**  
V: A felszabadítatlan erőforrások memória‑szivárgáshoz vezethetnek; mindig hívja meg a `closeNodes` metódust a leállításkor.

**K: Lehet-e egy dokumentumhoz egynél több egyedi attribútumot hozzáadni?**  
V: Természetesen – hívja meg az `addAttribute` metódust többször különböző attribútumnevekkel.

## Összegzés
Ebben az oktatóanyagban megtanulta, hogyan **szerezzen ideiglenes licencet**, állítson be és kezeljen keresési hálózati csomópontokat, adjon könyvtárakat az indexeléshez, és hogyan adjon egyedi dokumentumattribútumokat a GroupDocs.Search for Java használatával. A lépések követésével javíthatja szervezete információkeresési képességét, gyorsan és pontosan. Kezdje el alkalmazni ezeket a technikákat projektjeiben még ma, és tapasztalja meg a teljesítményjavulást saját szemével.

 frissítve:** 2026-01-19  
**Tesztelve a következővel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs