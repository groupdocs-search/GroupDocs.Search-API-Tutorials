---
date: '2026-07-02'
description: Tanulja meg, hogyan szerezhet temporary license-t a GroupDocs.Search-hez,
  hogyan adhat hozzá könyvtárakat az indexhez, és hogyan adhat hozzá custom document
  attributes-t, miközben a Java search network nodes-ot kezeli.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Ideiglenes licenc beszerzése a GroupDocs – Master Search Nodes (Java) számára
type: docs
url: /hu/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Ideiglenes licenc beszerzése GroupDocs – Master keresőcsomópontok (Java)

Ebben az átfogó útmutatóban **ideiglenes licencet szerezhet a GroupDocs.Search-hez**, konfigurál egy többcsomópontos keresőhálózatot, és megtanulja, hogyan **adjunk könyvtárakat az indexhez** és **egyedi dokumentum attribútumokat adjunk hozzá** Java használatával. Akár vállalati dokumentumkezelő rendszert, akár kereshető termékkatalógust épít, ezeknek a lépéseknek a elsajátítása lehetővé teszi a platform korlátozások nélküli kiértékelését és a keresési képességek gyors skálázását.

## Gyors válaszok
- **Mi az első lépés a GroupDocs.Search használatának megkezdéséhez?** Szerezzen be egy ideiglenes licencet a GroupDocs portálról.  
- **Mely Maven tároló tartalmazza a könyvtárat?** `https://releases.groupdocs.com/search/java/`.  
- **Hogyan adhatok hozzá könyvtárakat az indexhez?** Hívja meg a `addDirectoriesToIndex` segédfüggvényt a master csomóponton.  
- **Hozzáadhatok egyedi dokumentum attribútumokat?** Igen—hívja meg a `addAttribute` függvényt a dokumentum kulcsával és az attribútum nevével.  
- **Hogyan állíthatom le tisztán a csomópontokat?** `closeNodes` meghívásával szabadíthatja fel az erőforrásokat.

## Mi az az ideiglenes licenc és miért van rá szükség?
Az ideiglenes licenc lehetővé teszi a GroupDocs.Search kiértékelését korlátozások nélkül. Tökéletes fejlesztéshez, teszteléshez vagy koncepciókészítő projektekhez, mielőtt teljes vásárlásra kerülne sor. A licenc korlátozott időre teljes funkcióhozzáférést biztosít, lehetővé téve a teljesítmény mérését, az integrációs pontok tesztelését és annak biztosítását, hogy a megoldás megfelel az igényeinek anyagi elkötelezettség nélkül.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy a következő előfeltételek rendelkezésre állnak:

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
Letöltheti a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Környezet beállítása
- Győződjön meg róla, hogy kompatibilis JDK van telepítve (Java 8 vagy újabb).  
- Állítsa be az IDE-jét a Maven projektek támogatására.

### Tudás előfeltételek
Alapvető Java programozási ismeretek és Maven projektkezelés ismerete hasznos lesz. Ha újonc ezekben a koncepciókban, fontolja meg bevezető források tanulmányozását a kezdéshez.

## Ideiglenes licenc beszerzése
Az ideiglenes licenc a GroupDocs portál felkeresésével, egy rövid kérvény űrlap kitöltésével és a kapott `.lic` fájl projekt `resources` mappájába helyezésével szerezhető be. Ezután néhány kódsorral inicializálja a licencet (lásd az alábbi kódrészletet). A kérvény űrlaphoz használja a hivatalos oldalt: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## GroupDocs.Search beállítása Java-hoz

### Telepítési információk
A GroupDocs.Search for Java projektjébe való integrálásához kövesse a fentebb leírt Maven lépéseket, vagy töltse le a legújabb verziót közvetlenül a hivatalos kiadási oldalról.

#### Licenc beszerzési lépések
1. **Ingyenes próba** – Fedezze fel a funkciókat kötelezettség nélkül.  
2. **Ideiglenes licenc** – Szerezzen be egy rövid távú kulcsot a teszteléshez (lásd a fenti szekciót).  
3. **Vásárlás** – Gyártási használathoz vásároljon teljes licencet a **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)** oldalról.

### Alap inicializálás és beállítás
Inicializálja a projektet a GroupDocs.Search segítségével a következő módon:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Ez az inicializálási lépés kulcsfontosságú annak biztosításához, hogy minden komponens zökkenőmentesen működjön a keresőhálózatban.

## Megvalósítási útmutató
Most bontsuk le a folyamatot kezelhető szakaszokra, mindegyik egy adott funkcióra összpontosítva a keresőhálózati csomópontok telepítésében és kezelésében.

### 1. funkció: Konfiguráció beállítása
**Áttekintés:** A keresőhálózat konfigurációjának beállítása az első lépés a csomópontok telepítése során. Ez a beállítás magában foglalja az útvonalak és portok meghatározását, amelyek kritikusak a csomópont telepítéséhez.

#### Megvalósítási lépések:
##### 1. lépés: Alapút és port meghatározása
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### 2. lépés: Keresőhálózat konfigurálása
A `configureSearchNetwork` függvény előkészíti a csomópontok telepítéséhez szükséges konfigurációs objektumot.  
A `Configuration` egy osztály, amely minden beállítást tartalmaz, például az index mappát, a hálózati portokat és a csomópont szerepköröket.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Paraméterek:** Az alapút és a port a források megtalálásához és a kommunikációs csatornák létrehozásához használatos.  
- **Visszatérési érték:** Egy konfigurált `Configuration` objektum, amely az Ön telepítési igényeire van szabva.

### 2. funkció: Keresőhálózat telepítése
**Áttekintés:** A csomópontok telepítése elengedhetetlen a keresési képességek skálázásához különböző környezetekben vagy adatcsoportokban.

#### Megvalósítási lépések:
##### 1. lépés: Csomópontok telepítése
A `deploySearchNetwork` függvény inicializálja és visszaad egy tömböt a keresőhálózati csomópontokból.  
A `SearchNetworkNodes` minden egyes csomópont példányt képvisel, amely részt vesz a elosztott keresőklaszterben.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Paraméterek:** Az alapút, a port és a konfiguráció a telepítési környezet meghatározásához használatos.  
- **Visszatérési érték:** Egy tömb, amely inicializált `SearchNetworkNodes`-t tartalmaz.

### 3. funkció: Hálózati eseményekre feliratkozás
**Áttekintés:** A keresőhálózat tevékenységeinek monitorozása kulcsfontosságú az optimális teljesítmény és megbízhatóság fenntartásához.

#### Megvalósítási lépések:
##### 1. lépés: Feliratkozás a master csomópont eseményeire
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Cél:** Ez a lépés biztosítja, hogy értesüljön a keresőhálózat jelentős eseményeiről vagy változásairól.

### 4. funkció: Dokumentumok indexelése
**Áttekintés:** Könyvtárak hozzáadása, amelyek dokumentumokat tartalmaznak az indexeléshez, lehetővé teszi a hatékony adatlekérdezést a hálózaton belül.

#### Hogyan adjon hozzá könyvtárakat az indexhez
Az `addDirectoriesToIndex` egy segédfüggvény, amely regisztrálja a mappák útvonalait az indexeléshez a master csomóponton.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Cél:** Lehetővé teszi a gyors hozzáférést és kereshetőséget az összes dokumentumhoz a megadott könyvtárakban.

### 5. funkció: Attribútumok hozzáadása dokumentumokhoz
**Áttekintés:** Egyedi attribútumok gazdagítják a dokumentum metaadatait, rugalmasabbá és informatívabbá téve a kereséseket.

#### Hogyan adjon hozzá egyedi dokumentum attribútumokat
Az `addAttribute` egy egyedi metaadat attribútumot ad hozzá egy meghatározott dokumentumhoz az indexben.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Paraméterek:** Adja meg a csomópontot, a dokumentum kulcsát és a hozzáadandó attribútumot.  
- **Cél:** Kiterjeszti a keresési funkciót a dokumentumok további metaadatokkal való gazdagításával.

### 6. funkció: Indexelt dokumentumok lekérdezése
**Áttekintés:** Hatékonyan lekérheti és listázhatja az indexelt dokumentumokat az adatpontosság és teljesség biztosítása érdekében.

#### Megvalósítási lépések:
##### 1. lépés: Indexelt dokumentumok lekérése
```java
getIndexedDocuments(nodes[0]);
```  
- **Cél:** Ellenőrzi a szükséges dokumentumok sikeres indexelését a keresőhálózatban.

### 7. funkció: Hálózati csomópontok lezárása
**Áttekintés:** A csomópontok megfelelő lezárása kulcsfontosságú az erőforrás-kezelés és a memória szivárgások megelőzése érdekében.

#### Megvalósítási lépések:
##### 1. lépés: Minden csomópont lezárása
A `closeNodes` leállítja az összes aktív keresőcsomópontot és felszabadítja a lefoglalt erőforrásokat.  
```java
closeNodes(nodes);
```  
- **Cél:** Felszabadítja a csomópontok által elfoglalt erőforrásokat, biztosítva a tiszta leállási folyamatot.

## Miért használjunk ideiglenes licencet a GroupDocs.Search-hez?
Az ideiglenes licenc **30 napos teljes funkcióhozzáférést** biztosít, és akár **50 000 indexelt dokumentumot** támogat teljesítménykorlátozás nélkül. Ez lehetővé teszi az indexelési sebesség, a lekérdezési késleltetés és a skálázhatóság valós adatokon történő mérését a termék licenc vásárlása előtt. Emellett eltávolítja a kiértékelési vízjeleket, így a végtermék képességeit valós körülmények között láthatja.

## Gyakori felhasználási esetek
1. **Vállalati dokumentumkezelés** – Indexeljen milliókat belső fájlok között a részlegekben, azonnali teljes szöveges keresést biztosítva.  
2. **E‑kereskedelmi platformok** – Készítsen kereshető termékkatalógust, amely több raktárat és harmadik fél adatforrásait is lefedi.  
3. **Jogász irodák** – Szervezze az ügyiratokat, szerződéseket és bizonyítékokat egyedi metaadatokkal a gyors visszakereséshez.

Az integrációs lehetőségek más rendszerekkel magukban foglalják a CRM platformokat, tartalomkezelő rendszereket (CMS) és adat-analitikai eszközöket, kihasználva a GroupDocs.Search for Java által nyújtott robusztus indexelési és keresési funkciókat.

## Teljesítmény szempontok
A GroupDocs.Search for Java használatakor a teljesítmény optimalizálásához:
- **Konfiguráció optimalizálása** – Igazítsa a konfigurációs beállításokat a konkrét telepítési környezethez.  
- **Erőforrás-használat monitorozása** – Rendszeresen ellenőrizze a CPU, memória és I/O használatot a szűk keresztmetszetek vagy memória szivárgások elkerülése érdekében.  
- **Legjobb gyakorlatok követése** – Tartsa be a Java memória‑kezelési irányelveket, biztosítva a rendszer erőforrásainak hatékony kihasználását.

## Gyakran ismételt kérdések

**Q: Mennyi ideig érvényes egy ideiglenes licenc?**  
A: Az ideiglenes licencek általában 30 napig érvényesek, elegendő időt biztosítva a termék kiértékeléséhez.

**Q: Át tudok váltani egy ideiglenes licencről teljes licencre újratelepítés nélkül?**  
A: Igen—cserélje le az ideiglenes licencfájlt a teljes licencfájlra, és indítsa újra az alkalmazást.

**Q: Újra kell indexelni a dokumentumokat új licenc alkalmazása után?**  
A: Nem, az index érintetlen marad; a licenc csak a használati jogokat szabályozza.

**Q: Mi történik, ha elfelejtem lezárni a csomópontokat?**  
A: A felszabadítatlan erőforrások memória szivárgáshoz vezethetnek; mindig hívja meg a `closeNodes`-t a leállítás során.

**Q: Lehetséges egy dokumentumhoz több egyedi attribútumot hozzáadni?**  
A: Természetesen—hívja meg a `addAttribute`-t többször különböző attribútumnevekkel.

---

**Utolsó frissítés:** 2026-07-02  
**Tesztelve a következővel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Keresőhálózati csomópont telepítése .NET-ben a GroupDocs használatával a hatékony dokumentum indexelés és lekérdezés érdekében](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Hogyan valósítsunk meg egy keresőhálózatot a GroupDocs.Search .NET-ben dokumentumkezelő rendszerekhez](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Aspose.Search hálózat konfigurálása és dokumentum attribútumok hozzáadása a GroupDocs.Redaction .NET-hez: Átfogó útmutató](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)