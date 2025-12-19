---
date: '2025-12-19'
description: Tanulja meg, hogyan adhat dokumentumokat az indexhez, és hogyan tilthatja
  le a stop szavakat a GroupDocs.Search for Java-ban, ezáltal javítva a keresési pontosságot
  és a lekérdezés pontosságát.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: Dokumentumok hozzáadása az indexhez és a stop szavak letiltása a GroupDocs.Search
  Java-ban a keresési pontosság javítása érdekében
type: docs
url: /hu/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Dokumentumok hozzáadása az indexhez és a stop‑szavak letiltása a GroupDocs.Search Java-ban a keresési pontosság javítása érdekében

Arra törekszik, hogy **dokumentumokat adjon hozzá az indexhez**, miközben biztosítja, hogy semmilyen kritikus kifejezés ne maradjon figyelmen kívül? Ez az útmutató végigvezet a keresési élmény finomhangolásán a GroupDocs.Search for Java segítségével. A **stop‑szavak letiltása Java‑ban** megtanulásával pontosabb keresési lekérdezéseket érhet el, és a lehető legtöbbet hozhatja ki minden indexelt dokumentumból.

## Gyors válaszok
- **Mit jelent a „dokumentumok hozzáadása az indexhez”?** Ez azt jelenti, hogy a forrásfájlokat betölti egy kereshető indexbe, hogy hatékonyan lekérdezhetők legyenek.  
- **Miért kellene letiltani a stop‑szavakat?** Hogy a gyakori szavakat (pl. „on”, „the”) is belefoglalja a keresésbe, amikor ezek a kifejezések a saját területén jelentősek.  
- **Melyik könyvtárverzió szükséges?** GroupDocs.Search for Java 25.4 vagy újabb.  
- **Szükség van licencre?** Egy ingyenes próba a kiértékeléshez elegendő; a termeléshez állandó licenc szükséges.  
- **Használható Maven projektben?** Igen – csak adja hozzá az alább látható tárolót és függőséget.

## Mi az a „dokumentumok hozzáadása az indexhez” a GroupDocs.Search‑ben?
A dokumentumok indexhez adása azt jelenti, hogy fájlokat importál egy mappából (vagy stream‑ből) egy olyan adatstruktúrába, amelyet a keresőmotor gyorsan lekérdezhet. Az indexelés után minden szó – beleértve a normál esetben stop‑szónak tekintett szavakat is – kereshetővé válik.

## Miért kell letiltani a stop‑szavakat Java‑ban?
A stop‑szavak letiltása lehetővé teszi, hogy minden tokenet jelentősnek tekintsen. Ez kulcsfontosságú olyan területeken, mint a jogi kutatás, az e‑kereskedelmi termékkatalógusok vagy bármely olyan szituáció, ahol a „on” vagy „by” szavak jelentéssel bírnak.

## Előfeltételek

- **Szükséges könyvtárak**: GroupDocs.Search for Java 25.4 (vagy újabb).  
- **Fejlesztői környezet**: IntelliJ IDEA, Eclipse vagy bármely kedvenc Java IDE.  
- **Alapvető ismeretek**: Java szintaxis és az indexelés fogalmának ismerete.

## GroupDocs.Search for Java beállítása

### Maven telepítés

Ha Maven‑t használ, adja hozzá a következőt a `pom.xml`‑hez:

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

Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

#### Licenc megszerzésének lépései
- **Ingyenes próba** – azonnal elkezdheti a tesztelést.  
- **Ideiglenes licenc** – időkorlátos kulcs a teljes funkcionalitáshoz.  
- **Vásárlás** – állandó licenc a termelési használathoz.

## Alapvető inicializálás és beállítás

Hozzon létre egy `IndexSettings` példányt az index viselkedésének szabályozásához:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Hogyan tiltsuk le a stop‑szavakat Java‑ban

Az alábbi sor kikapcsolja a beépített stop‑szó szűrőt:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Paraméterek*: a `setUseStopWords` logikai értéket vár.  
*Cél*: biztosítja, hogy minden szó – beleértve a gyakori stop‑szavakat is – indexelve legyen és kereshető legyen.

## Hogyan adjuk hozzá a dokumentumokat az indexhez

### Kimeneti könyvtár meghatározása

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Dokumentumkönyvtár megadása

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Most minden fájl a `YOUR_DOCUMENT_DIRECTORY`‑ben **dokumentumok hozzáadása az indexhez** történik, és készen áll a lekérdezésre.

## Keresési lekérdezés végrehajtása

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Mivel a stop‑szavak le vannak tiltva, a `"on"` kifejezés is figyelembe lesz véve a keresés során, így olyan találatokat is visszaad, amelyeket egyébként figyelmen kívül hagynának.

## Gyakorlati alkalmazások

1. **Vállalati dokumentumkeresés** – Biztosítsa, hogy a kritikus terminológiát ne szűrje ki.  
2. **E‑kereskedelmi platformok** – Javítsa a termékek felfedezését azáltal, hogy minden szót indexel a termékleírásokban.  
3. **Jogi kutatási eszközök** – Rögzítse minden jogi kifejezést, még azokat is, amelyeket általában stop‑szónak tekintenek.

## Teljesítménybeli megfontolások

- **Optimalizálási tippek**: Rendszeresen frissítse és tisztítsa meg az indexet a keresési sebesség fenntartása érdekében.  
- **Erőforrás-használat**: Figyelje a JVM heap méretét; nagy indexek esetén szükség lehet a szemétgyűjtés beállításainak finomhangolására.  
- **Java memória-kezelés**: Használjon hatékony adatstruktúrákat, és fontolja meg az off‑heap tárolást nagyon nagy korpuszok esetén.

## Gyakori problémák és megoldások

| Tünet | Valószínű ok | Megoldás |
|---|---|---|
| Nincs találat a gyakori szavakra | `setUseStopWords(true)` (alapértelmezett) | Hívja meg a `setUseStopWords(false)`‑t a fenti módon. |
| Memória‑hiány hiba indexelés közben | Túl sok nagy fájl egyszerre indexelése | Indexelje a fájlokat kötegekben; növelje a `-Xmx` JVM opciót. |
| A keresés elavult adatokat ad vissza | Az index nem frissült új fájlok hozzáadása után | Hívja meg az `index.update()`‑t vagy adja hozzá újra a módosított dokumentumokat. |

## Gyakran feltett kérdések

**K: Mik azok a stop‑szavak?**  
V: A stop‑szavak gyakori kifejezések (pl. „the”, „is”, „on”), amelyeket sok keresőmotor kihagy a lekérdezések felgyorsítása érdekében. Letiltásukkal minden token kereshetővé válik.

**K: Miért kell letiltani a stop‑szavakat a keresőindexekben?**  
V: Amikor pontos kifejezés‑illesztésre van szükség – például jogi vagy műszaki dokumentumok esetén – minden szó jelentéssel bír, ezért a stop‑szavakat is bele kell foglalni.

**K: Hogyan kezeli a GroupDocs.Search a nagy adatállományokat?**  
V: A könyvtár optimalizált adatstruktúrákat és inkrementális indexelést használ, hogy alacsony memóriahasználatot biztosítson még milliók dokumentuma esetén is.

**K: Integrálhatom a GroupDocs.Search‑t más Java‑alkalmazásokkal?**  
V: Igen, az API úgy van tervezve, hogy könnyen beágyazható legyen bármely Java‑alapú rendszerbe, legyen az webszolgáltatás vagy asztali alkalmazás.

**K: Mit tegyek, ha a keresési eredmények nem pontosak?**  
V: Ellenőrizze, hogy az index tartalmazza-e az összes szükséges dokumentumot (`add documents to index`), győződjön meg arról, hogy a stop‑szó szűrés le van tiltva, ha szükséges, és fontolja meg az index újraépítését jelentős változások után.

## Források

- **Dokumentáció**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API referencia**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Letöltés**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- **GitHub tároló**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ingyenes támogatás**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Ideiglenes licenc**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Ezzel az útmutatóval most már tudja, hogyan **adjon hozzá dokumentumokat az indexhez** és **tiltsa le a stop‑szavakat Java‑ban**, hogy pontosabb keresési eredményeket érjen el Java‑alkalmazásaiban.

---

**Utoljára frissítve:** 2025-12-19  
**Tesztelve a következővel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs  

---