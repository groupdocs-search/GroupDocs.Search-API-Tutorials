---
date: '2025-12-26'
description: Ismerje meg, hogyan kereshet és emelhet ki szöveget a dokumentumokban
  a GroupDocs.Search for Java segítségével. Fedezze fel a teljes dokumentum és a részletkiemelés
  technikáit.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Szöveg keresése és kiemelése a GroupDocs.Search for Java segítségével
type: docs
url: /hu/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Keresés és szövegkiemelés dokumentumokban a GroupDocs.Search for Java használatával

A mai digitális korban a **search and highlight text** (szöveg keresése és kiemelése) hatalmas dokumentumgyűjteményekben gyakori követelmény. Akár jogi felülvizsgálati eszközt, akár tudományos kutatási portált, vagy ügyfélszolgálati irányítópultot építesz, a kulcsszavak azonnali megtalálása és kiemelése jelentősen javítja a használhatóságot. Ebben az átfogó útmutatóban megtudod, hogyan valósítható meg a **search and highlight text** a GroupDocs.Search for Java segítségével – lefedve a teljes dokumentum kiemelését és a fragment‑level (töredék‑szintű) kiemelést a fókuszált kontextus érdekében.

## Gyors válaszok
- **What does “search and highlight text” mean?** Azt jelenti, hogy a lekérdezési kifejezéseket egy dokumentumban megtalálják, és vizuálisan kiemelik őket (például háttérszínnel).  
- **Which library provides this capability?** GroupDocs.Search for Java.  
- **Do I need a license?** Egy ingyenes próba verzió használható értékelésre; a teljes licenc szükséges a termeléshez.  
- **Can I customize highlight colors?** Igen – bármely RGB szín beállítható a `HighlightOptions` segítségével.  
- **Is fragment highlighting supported?** Teljesen támogatott; meghatározhatod a találat előtt/után megjelenő szavak számát, hogy tömör kivonatot hozz létre.

## Mi a Search and Highlight Text?
A search and highlight text a folyamat, amely során egy dokumentumindexet átvizsgálnak egy adott lekérdezésre, visszakeresik a megfelelő dokumentumokat, majd megjelölik a lekérdezési kifejezés minden előfordulását a dokumentum kimenetében (HTML, PDF stb.). Ez a vizuális jelzés segíti a felhasználókat, hogy azonnal megtalálják a releváns információt.

## Miért használjuk a GroupDocs.Search for Java-t?
- **High‑performance indexing** a konfigurálható tömörítéssel.  
- **Rich highlighting API** amely egész dokumentumokon és egyedi fragmentumokon is működik.  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT, and more).  
- **Easy Maven integration** és tiszta Java‑központú API.

## Előfeltételek
- Java Development Kit (JDK) 8 vagy újabb.  
- Maven a függőségek kezeléséhez.  
- IntelliJ IDEA vagy Eclipse típusú IDE.  
- Alapvető ismeretek a Java szintaxisban.

## A GroupDocs.Search for Java beállítása

Add the GroupDocs repository and dependency to your `pom.xml`:

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

You can also download the latest JAR directly from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
Kezdd egy ingyenes próba verzióval, vagy szerezz be egy ideiglenes licencet az értékeléshez. Termelési környezetben vásárolj teljes licencet a teljes funkcionalitás feloldásához.

## Implementációs útmutató

A megvalósítás két gyakorlati részre oszlik: **highlighting in entire documents** és **highlighting in fragments**. Mindkét rész tartalmazza a lényeges lépéseket a **how to highlight Java** dokumentumok GroupDocs.Search használatával történő kiemeléséhez.

### Index beállítások konfigurálása
Before indexing, configure the storage to use high compression—this reduces disk usage while preserving search speed.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Kiemelés egész dokumentumokban

#### 1. lépés: Index létrehozása és feltöltése
Create an index folder and add all source files you want to search.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### 2. lépés: Keresés végrehajtása és kiemelés alkalmazása
Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted matches.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Key options explained** Kulcsfontosságú beállítások magyarázata
- **Compression** – a magas tömörítés helyet takarít meg.  
- **HighlightColor** – állíts be bármilyen RGB értéket, hogy illeszkedjen a UI palettádhoz.  
- **UseInlineStyles** – a `false` tiszta HTML-t generál, amelyet globálisan lehet CSS‑sel stílusozni.

### Kiemelés fragmentumokban

#### 1. lépés: Indexelés és keresés (ugyanaz, mint fent)

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### 2. lépés: Fragmentum kontextus meghatározása és kiemelés
Specify how many terms before and after the match should appear in each fragment.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### 3. lépés: Kiemelt fragmentumok lekérése és írása
Collect the generated fragments and write them to an HTML file.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Gyakorlati alkalmazások
1. **Legal Document Review** – azonnal kiemeli a törvényeket, záradékokat vagy esethivatkozásokat.  
2. **Academic Research** – megjeleníti a kulcsfontosságú terminológiát több tucat PDF és Word fájlban.  
3. **Customer Support** – pontosan megtalálja a rendelési számokat vagy hiba kódokat a jegytörténetekben.

## Teljesítmény szempontok
- **Index Size** – a magas tömörítés (`Compression.High`) csökkenti a lemezhasználatot.  
- **Fragment Context** – a nagyobb `termsBefore/After` értékek növelik a pontosságot, de befolyásolhatják a sebességet.  
- **Memory Management** – figyeld a JVM heap memóriát nagy korpuszok indexelésekor; nagyon nagy adathalmazok esetén fontold meg az inkrementális indexelést.

## Gyakori problémák és megoldások
- **Indexing Errors** – ellenőrizd a fájl útvonalakat, és győződj meg arról, hogy az alkalmazásnak van olvasási/írási jogosultsága.  
- **No Highlights Appear** – ellenőrizd, hogy a `UseInlineStyles` megfelel a kimeneti formátumnak (HTML vs. PDF).  
- **Color Not Applied** – győződj meg arról, hogy az RGB értékek 0‑255 tartományban vannak, és hogy az HTML néző támogatja a stílust.

## Gyakran ismételt kérdések

**Q: Mik a GroupDocs.Search for Java használatának előnyei?**  
A: Gyors, skálázható indexelést, testreszabható kiemelést és számos dokumentumformátum támogatását kínál.

**Q: Hogyan integrálhatom a GroupDocs.Search-t egy REST API-val?**  
A: A keresési és kiemelési metódusokat Spring Boot kontrollereken keresztül teheted elérhetővé, HTML vagy JSON payload-ot visszaadva.

**Q: Kezeli a könyvtár a jelszóval védett fájlokat?**  
A: Igen – add meg a jelszót a dokumentum indexeléséhez.

**Q: Testreszabhatom a kiemelés jelölését a színen kívül?**  
A: Természetesen; CSS osztályokat injektálhatsz a `HighlightOptions` segítségével, vagy módosíthatod a HTML-t a generálás után.

**Q: Melyik verzió lett tesztelve ebben az útmutatóban?**  
A: A kód a GroupDocs.Search 25.4 verzióval lett validálva.

---

**Utolsó frissítés:** 2025-12-26  
**Tesztelt verzió:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs