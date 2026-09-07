---
date: '2026-07-07'
description: Ismerje meg, hogyan törölje az indexet, végezzen full text search Java-t,
  és optimalizálja a keresési teljesítményt a GroupDocs.Search for Java segítségével.
  Lépésről‑lépésre útmutató network setup és indexing.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Hogyan töröljük az indexet és végezzünk full text search Java-t a
  GroupDocs.Search használatával. Kövesse ezt az útmutatót a search network beállításához,
  a searchable index létrehozásához, és a keresési teljesítmény optimalizálásához.
og_title: Hogyan töröljük az indexet és végezzünk Text Search-et a GroupDocs.Search
  for Java használatával
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Hogyan töröljük az indexet és végezzünk Text Search-et a GroupDocs.Search for
  Java használatával
type: docs
url: /hu/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Hogyan töröljük az indexet és végezzünk szöveges keresést a GroupDocs.Search for Java segítségével

A mai adat‑központú világban a **how to delete index** gyors elvégzése, miközben villámgyors teljes‑szöveges keresést biztosít Java‑ban, versenyelőnyt jelent. Akár belső tudásbázist, jogi esetek tárolóját, vagy e‑kereskedelmi termékkatalógust épít, egy jól hangolt keresési hálózat drámaian javíthatja a felhasználói elégedettséget. Ebben az útmutatóban megtanulja, hogyan **set up a search network**, **create a searchable index**, **optimize search performance**, és **delete documents from the index** szükség esetén – mindezt a GroupDocs.Search for Java használatával.

## Gyors válaszok
- **Mi a fő célja a GroupDocs.Search for Java-nak?** Teljes‑szöveges keresést biztosít több mint 50 dokumentumformátumban, lehetővé téve a gyors kulcsszó‑lekérdezést.  
- **Hogyan végezhetek szöveges keresést elosztott környezetben?** Telepítsen egy keresési hálózatot, indexelje a dokumentumokat egy master csomóponton, majd kérdezzen le bármelyik csomópontot.  
- **Törölhetek dokumentumokat az indexből anélkül, hogy újraépíteném?** Igen, használja a Delete API‑t a kiválasztott fájlok eltávolításához, hatékonyan *how to delete index* teljes újra‑indexelés nélkül.  
- **Milyen Java verzió szükséges?** JDK 8 vagy újabb.  
- **Szükséges licenc a termeléshez?** Érvényes GroupDocs.Search licenc szükséges; ingyenes próba elérhető.

## Mi a “perform text search”?
A szöveges keresés végrehajtása azt jelenti, hogy egy teljes‑szöveges indexben keresünk, hogy visszakeressük azokat a dokumentumokat, amelyek a megadott kulcsszavakat vagy kifejezéseket tartalmazzák. A GroupDocs.Search egy fordított indexet épít, amely ezeket a lekérdezéseket rendkívül gyorsá teszi, még több ezer fájl esetén is.

## Miért érdemes keresési hálózatot beállítani?
A keresési hálózat elosztja az indexelési és lekérdezési terhelést több csomópont között, lehetővé téve a **optimize search performance**, vízszintes skálázást és a magas rendelkezésre állás fenntartását. Ez az architektúra ideális vállalati szintű dokumentumtárakhoz, ahol a késleltetés és az áteresztőképesség fontos.

## Hogyan valósítsuk meg és optimalizáljuk a keresési hálózatot a GroupDocs.Search for Java segítségével
Töltse be a konfigurációt, indítson el egy master csomópontot, majd adjon hozzá munkavállaló csomópontokat, amelyek ugyanazt az alapútvonalat és portot használják. A hálózat ilyen módon történő telepítése lehetővé teszi, hogy bármely csomópont kezelje az indexelési vagy lekérdezési kéréseket, konzisztens válaszidőket biztosítva még akkor is, ha a dokumentumok száma több százezerre nő.

### Lépés‑ről‑lépésre áttekintés
1. **Alapkonfiguráció meghatározása** amely tartalmaz egy megosztott könyvtárat és egy TCP portot.  
2. **A master csomópont indítása** az index kezeléséhez és a munkavállaló csomópontok koordinálásához.  
3. **Munkavállaló csomópontok hozzáadása**, amelyek a masterhez csatlakoznak, lehetővé téve a párhuzamos indexelést és keresést.  
4. **Erőforrás-használat monitorozása** és a JVM heap beállítások finomhangolása a késleltetés alacsonyan tartásához.

## Hogyan töröljük az indexet a GroupDocs.Search for Java-ban
`SearchNode` egy csomópont a GroupDocs.Search hálózatban, amely kezeli az indexelési és lekérdezési műveleteket. A `delete` metódus eltávolítja a megadott dokumentumokat az indexből.

### Közvetlen törlési lépések
- Hívja meg a `delete` metódust a `SearchNode` példányon.  
- Adjon meg egy tömböt relatív fájlútvonalakkal.  
- Kötelezővé tegye a változtatásokat; az index azonnal frissül, és a későbbi keresések már nem adják vissza az eltávolított fájlokat.

## Mi az a Search Network?
A **search network** egy összekapcsolt csomópontokból álló klaszter, amely közös index tárolót oszt meg, lehetővé téve az elosztott indexelést és lekérdezés végrehajtását. Lehetővé teszi a vízszintes skálázást és a hibatűrést nagy méretű dokumentumgyűjtemények esetén.

## Hogyan hozzunk létre kereshető indexet (index documents java)
A `add` metódus egy dokumentumot indexel a keresési indexbe. Dokumentumokat adjon hozzá a master csomóponthoz a `add` metódus használatával; a hálózat a változásokat minden munkavállaló csomópontra továbbítja. Ez a megközelítés biztosítja, hogy minden csomópont a legfrissebb index ellen kérdezzen le további szinkronizációs lépések nélkül.

### Kulcsfontosságú műveletek
- Mutassa a master csomópontot a forrásfájlokat tartalmazó mappára.  
- Hívja meg az indexelési rutinot; a hálózat feldolgozza minden fájlt és frissíti a fordított indexet.  
- Ellenőrizze, hogy az index fájlok megjelennek a kijelölt tárolókönyvtárban.

## Hogyan távolítsuk el az indexelt fájlokat (remove indexed files)
Amikor egy dokumentum elavulttá válik, hívja meg a `delete` API‑t az útvonalával. A rendszer eltávolítja a fájl bejegyzéseit a fordított indexből, felszabadítva a tárhelyet és megakadályozva a régi eredményeket.

## A GroupDocs.Search for Java beállítása
A kezdéshez integrálja a GroupDocs.Search‑t a Java projektjébe az alábbi beállításokkal:

### Maven beállítás
Adja hozzá a tárolót és a függőséget a `pom.xml` fájlhoz:

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

### Közvetlen letöltés
Alternatív megoldásként letöltheti a legújabb verziót közvetlenül a GroupDocs‑től [letöltheti a legújabb verziót közvetlenül a GroupDocs‑től](https://releases.groupdocs.com/search/java/).

### Licenc megszerzése
A GroupDocs ingyenes próbaidőszakot kínál, amely lehetővé teszi a funkciók értékelését vásárlás előtt. Ideiglenes licencet szerezhet a [vásárlási oldal](https://purchase.groupdocs.com/temporary-license/) lépéseinek követésével. Ez teljes funkcionalitást biztosít a tesztelési fázis során.

### Alap inicializálás és beállítás
Inicializálja a GroupDocs.Search‑t a Java alkalmazásában a következővel:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Implementációs útmutató

### A keresési hálózat konfigurálása
**Áttekintés:** Állítson be egy alap útvonalat és portot a keresési hálózat számára, lehetővé téve a csomópontok hatékony kommunikációját.

#### 1. lépés: Alapkonfiguráció meghatározása
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Paraméterek:**  
  - `basePath`: Könyvtár útvonal a hálózati műveletekhez.  
  - `basePort`: A keresési hálózat által használt portszám.

#### 2. lépés: Hibaelhárítás
Győződjön meg arról, hogy a megadott portot nem blokkolja a tűzfal beállítása, vagy nem használja más alkalmazás. Szükség szerint állítsa be a konfliktusok elkerülése érdekében.

### Keresési hálózati csomópontok telepítése
**Áttekintés:** A konfiguráció használatával telepítsen csomópontokat a hálózaton elosztott indexelés és keresés céljából.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Kulcsfontosságú konfigurációs beállítások:**  
  - **Base Path & Port:** Ezeknek az értékeknek meg kell egyezniük az első konfigurációban használtakkal a konzisztencia érdekében.

### Dokumentumok indexelése (`create searchable index`)
**Áttekintés:** Dokumentumok hatékony hozzáadása a keresési indexhez egy master csomópont használatával.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Cél:**  
  - `masterNode`: Az elsődleges csomópont, amely a dokumentumok indexelését kezeli.  
  - `documentsPath`: Az a könyvtár útvonal, amely a dokumentumokat tartalmazza.

#### Hibaelhárítási tippek
Ellenőrizze, hogy a dokumentum útvonalak helyesek és elérhetők. Győződjön meg arról, hogy a jogosultságok engedélyezik az olvasást ezekből a könyvtárakból.

### Szöveg keresése a hálózatban (`perform text search`)
**Áttekintés:** Végrehajtani átfogó szöveges kereséseket az indexelt hálózaton.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Paraméterek:**  
  - `query`: A keresett szöveg.  
  - `masterNode`: A keresést végző csomópont.

### Dokumentumok törlése az indexből (`delete documents index`)
**Áttekintés:** Specifikus dokumentumok eltávolítása az indexből a fájlútvonaluk alapján.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Metódus célja:**  
  - `node`: A cél csomópont a törlési műveletekhez.  
  - `filePaths`: Az indexből eltávolítandó dokumentumok útvonalai.

#### Hibaelhárítás
Győződjön meg arról, hogy a fájlútvonalak pontosak és a fájlok léteznek a könyvtárban. Ha a problémák továbbra is fennállnak, ellenőrizze a hálózati jogosultságokat és a kapcsolódást.

## Gyakorlati alkalmazások
1. **Enterprise Document Management:** Belső tudáslekérdezés egyszerűsítése.  
2. **Legal Case Analysis:** Gyorsan megtalálni a releváns ügyiratokat több tárolóban.  
3. **E‑commerce Platforms:** A termékkeresés sebességének növelése a leírások és vélemények indexelésével.  
4. **Academic Research:** Hatékony keresés nagy digitális könyvtárakban, papírok és szakdolgozatok között.  
5. **Customer Support Systems:** Válaszidő csökkentése azáltal, hogy az ügyintézők azonnal kereshetnek a korábbi jegyek között.

## Teljesítményfontosságú szempontok
- **Optimize Indexing Speed:** Új dokumentumok fokozatos hozzáadása csúcsidőn kívül a késleltetés alacsonyan tartása érdekében.  
- **Resource Usage Guidelines:** CPU és memória monitorozása, különösen a csomópontok számának növelésekor.  
- **Java Memory Management:** A JVM heap beállítások finomhangolása a terhelés alapján (pl. `-Xmx2g` közepes méretű indexekhez).

## Következtetés
Ezzel az útmutatóval megtanulta, hogyan **set up a search network**, **create a searchable index**, **perform text search**, és **delete documents index** a GroupDocs.Search for Java használatával. Ezek a képességek gyors és megbízható dokumentumlekérdezést tesznek lehetővé elosztott környezetekben.

**Következő lépések**
- Kísérletezzen különböző csomópont konfigurációkkal, hogy megtalálja az optimális egyensúlyt a terheléshez.  
- Mélyedjen el a fejlett indexelési lehetőségekben, mint a saját elemzők és a relevancia finomhangolása.  
- Fedezze fel a integrációt más GroupDocs termékekkel a teljes körű dokumentumfeldolgozáshoz.

## Gyakran Ismételt Kérdések

**Q: Mi a fő felhasználási eset a GroupDocs.Search for Java esetén?**  
A: Teljes‑szöveges keresést biztosít számos dokumentumformátumban, lehetővé téve a **perform text search** nagy tárolókban.

**Q: Hogyan javíthatom a keresési sebességet egy nagy hálózatban?**  
A: Telepítsen további csomópontokat, finomhangolja a JVM heapet, és ütemezze az indexelést alacsony forgalmú időszakokra a **optimize search performance** érdekében.

**Q: Lehetséges egyetlen dokumentumot törölni anélkül, hogy újraindexelné az egész gyűjteményt?**  
A: Igen, használja a **delete documents index** API‑t a kódpéldában bemutatott módon a specifikus fájlok eltávolításához.

**Q: Szükségem van licencre fejlesztéshez?**  
A: Az ingyenes próba licenc elegendő a teszteléshez; a termelési környezethez kereskedelmi licenc szükséges.

**Q: Indexelhetek PDF‑eket, Word fájlokat és e‑mail üzeneteket együtt?**  
A: Teljesen—A GroupDocs.Search natívan támogat sokféle formátumot.

---

**Utoljára frissítve:** 2026-07-07  
**Tesztelve a következővel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Hogyan indexeljünk szöveget Java-ban a GroupDocs.Search útmutatóval](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Keresési teljesítmény optimalizálása fejlett indexelési technikákkal a GroupDocs.Search for Java-ban](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Lekérdezési teljesítmény javítása a GroupDocs.Search Java-val: Index és keresés optimalizálása](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)