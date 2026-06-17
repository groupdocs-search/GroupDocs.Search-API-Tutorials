---
date: '2026-02-27'
description: Tanulja meg, hogyan emeljen ki szöveget Java-ban a GroupDocs.Search for
  Java használatával, beleértve a dokumentumok keresését Java-ban, a dokumentumok
  indexelését Java-ban és a töredékek kiemelését.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Szöveg kiemelése Java-val a GroupDocs.Search segítségével
type: docs
url: /hu/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Szövegkiemelés Java-val a GroupDocs.Search segítségével

A mai gyors tempójú digitális környezetben a **highlight text java** képesség nagy fájlkészletekben elengedhetetlen funkció. Akár jogi felülvizsgálati platformot, akár tudományos kutatási motorot, vagy ügyfélszolgálati konzolt építesz, a felhasználók által keresett kifejezések azonnali megtalálása sokkal hatékonyabbá teszi a tapasztalatot. Ez az útmutató végigvezet a **GroupDocs.Search for Java** használatán a **search documents java**, **index documents java** funkciókhoz, és a gazdag kiemelés alkalmazásához – mind teljes dokumentumokra, mind fókuszált fragmentumokra.

## Gyors válaszok
- **Mi jelent a “search and highlight text” kifejezés?** Ez a lekérdezési kifejezések dokumentumban történő megtalálását és vizuális kiemelését jelenti (pl. háttérszínnel).  
- **Melyik könyvtár biztosítja ezt a képességet?** GroupDocs.Search for Java.  
- **Szükségem van licencre?** Az ingyenes próba a kiértékeléshez működik; a teljes licenc szükséges a termeléshez.  
- **Testreszabhatom a kiemelés színeit?** Igen—bármely RGB szín beállítható a `HighlightOptions` segítségével.  
- **Támogatott a fragmentum kiemelés?** Teljes mértékben; meghatározhatja a találat előtt és után megjelenő kifejezéseket a tömör kivonatok létrehozásához.

## Hogyan emeljünk ki szöveget Java-ban dokumentumokban
A szövegkiemelés Java-ban három alapvető lépést tartalmaz:

1. **Indexelje a forrásfájlokat** úgy, hogy azok gyorsan kereshetők legyenek.  
2. **Futtasson egy lekérdezést** az indexen, hogy megtalálja a megfelelő dokumentumokat.  
3. **Ábrázolja az eredményeket vizuális jelekkel** a highlighter API használatával.  

Az alábbiakban részletesen megvizsgáljuk az egyes lépéseket, először a teljes dokumentum kimenethez, majd a fragmentumszintű kivonatokhoz.

## Mi az a Search and Highlight Text?
A Search and Highlight Text a folyamat, amely során egy dokumentum indexet vizsgál egy adott lekérdezésre, visszaadja a megfelelő dokumentumokat, majd megjelöli a lekérdezési kifejezés minden előfordulását a dokumentum kimenetében (HTML, PDF, stb.). Ez a vizuális jel segíti a végfelhasználókat, hogy azonnal megtalálják a releváns információkat.

## Miért használjuk a GroupDocs.Search for Java-t?
- **Nagy teljesítményű indexelés** konfigurálható tömörítéssel (`index documents java`).  
- **Gazdag kiemelés API** amely teljes dokumentumokon és egyedi fragmentumokon is működik (`highlight search terms java`).  
- **Keresztformátumú támogatás** (DOCX, PDF, PPTX, TXT és továbbiak).  
- **Egyszerű Maven integráció** és tiszta Java‑központú tervezés.

## Előkövetelmények
- Java Development Kit (JDK) 8 vagy újabb.  
- Maven a függőségkezeléshez.  
- IntelliJ IDEA vagy Eclipse típusú IDE.  
- Alapvető ismeretek a Java szintaxisról.

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

A legújabb JAR-t közvetlenül a hivatalos oldalról is letöltheti: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc megszerzése
Kezdje egy ingyenes próbalicencével, vagy szerezzen be egy ideiglenes licencet a kiértékeléshez. A termelési környezetben teljes licenc vásárlása szükséges az összes funkció feloldásához.

## Implementációs útmutató

A megvalósítás két gyakorlati szakaszra oszlik: **highlighting in entire documents** és **highlighting in fragments**. Mindkét szakasz tartalmazza a **how to highlight Java** dokumentumokhoz szükséges alapvető lépéseket a GroupDocs.Search használatával.

### Index beállítások konfigurálása
Az indexelés előtt konfigurálja a tárolót magas tömörítés használatára – ez csökkenti a lemezhasználatot, miközben megőrzi a keresési sebességet.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Kiemelés teljes dokumentumokban

#### 1. lépés: Az index létrehozása és feltöltése
Hozzon létre egy index mappát, és adja hozzá az összes forrásfájlt, amelyet keresni szeretne.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### 2. lépés: Keresés végrehajtása és kiemelés alkalmazása
Keresse meg a kifejezést (pl. `ipsum`), és generáljon egy HTML fájlt a kiemelt találatokkal.

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

**Kulcsfontosságú beállítások magyarázata**  
- **Compression** – a magas tömörítés helyet takarít meg.  
- **HighlightColor** – állítson be bármilyen RGB értéket, hogy illeszkedjen a UI színpalettájához.  
- **UseInlineStyles** – `false` tiszta HTML-t generál, amelyet globálisan CSS‑szel lehet stílusozni.  

### Kiemelés fragmentumokban

#### 1. lépés: Indexelés és keresés (ugyanaz, mint fent)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### 2. lépés: Fragmentum kontextus definiálása és kiemelés
Adja meg, hány kifejezés jelenjen meg a találat előtt és után minden egyes fragmentumban.

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
Gyűjtse össze a generált fragmentumokat, és írja őket egy HTML fájlba.

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
1. **Jogi dokumentum felülvizsgálat** – azonnal kiemeli a törvényeket, záradékokat vagy esetreferenciákat.  
2. **Tudományos kutatás** – megjeleníti a kulcsfontosságú terminológiát több tucat PDF és Word fájlban.  
3. **Ügyfélszolgálat** – pontosan megtalálja a rendelési számokat vagy hiba kódokat a jegytörténetekben.

## Teljesítménybeli megfontolások
- **Index Size** – a magas tömörítés (`Compression.High`) csökkenti a lemezterületet.  
- **Fragment Context** – a nagyobb `termsBefore/After` értékek növelik a pontosságot, de befolyásolhatják a sebességet.  
- **Memory Management** – figyelje a JVM heapet nagy korpuszok indexelésekor; nagyon nagy adathalmazok esetén fontolja meg az inkrementális indexelést.

## Gyakori problémák és megoldások
- **Indexing Errors** – ellenőrizze a fájlutakat és győződjön meg arról, hogy az alkalmazásnak olvasási/írási jogosultsága van.  
- **No Highlights Appear** – erősítse meg, hogy a `UseInlineStyles` megfelel a kimeneti formátumnak (HTML vs. PDF).  
- **Color Not Applied** – ellenőrizze, hogy az RGB értékek 0‑255 tartományon belül vannak, és hogy a HTML‑megtekintő támogatja a stílust.

## Gyakran ismételt kérdések

**Q: Milyen előnyei vannak a GroupDocs.Search for Java használatának?**  
A: Gyors, skálázható indexelést, testreszabható kiemelést és számos dokumentumformátum támogatását kínál.

**Q: Hogyan integrálhatom a GroupDocs.Search‑t egy REST API‑val?**  
A: Tegye elérhetővé a keresési és kiemelési metódusokat Spring Boot kontrollereken keresztül, HTML vagy JSON payload‑ot visszaadva.

**Q: Kezeli a könyvtár a jelszóval védett fájlokat?**  
A: Igen—adja meg a jelszót a dokumentum indexhez való hozzáadásakor.

**Q: Testreszabhatom a kiemelés jelölését a színen túl?**  
A: Teljes mértékben; CSS‑osztályokat injektálhat a `HighlightOptions`‑on keresztül, vagy módosíthatja a HTML‑t a generálás után.

**Q: Melyik verziót tesztelték ehhez az útmutatóhoz?**  
A: A kódot a GroupDocs.Search 25.4 verzióval validálták.

**Q: Hogyan állíthatom be a highlight options java‑t, hogy CSS‑osztályt használjon inline stílusok helyett?**  
A: Állítsa be `options.setUseInlineStyles(false)`‑t, és adjon hozzá egy CSS‑szabályt a `options.setCssClass("myHighlight")`‑val megadott osztályhoz.

**Q: Van mód arra, hogy a highlight terms pdf java‑t közvetlenül PDF‑ból kiemeljem?**  
A: Igen— a GroupDocs.Search PDF bemenettel is működik, a highlighter pedig HTML‑t ad ki, amelyet beágyazhat PDF‑megtekintőbe vagy visszaalakíthat PDF‑vé a GroupDocs.Conversion segítségével.

---

**Legutóbb frissítve:** 2026-02-27  
**Tesztelt verzió:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs