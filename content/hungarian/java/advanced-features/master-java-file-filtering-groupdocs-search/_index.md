---
date: '2026-09-06'
description: Ismerje meg, hogyan szűrhetünk java fájlkiterjesztéseket a GroupDocs.Search
  for Java segítségével, beleértve a logikai AND, OR, NOT operátorokat, dátumtartomány
  szűrőket és útvonal szűrőket.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Java fájlkiterjesztések szűrése a GroupDocs.Search használatával.
  Tanulja meg, hogyan kombinálhatja a kiterjesztés, a dátumtartomány és az útvonal
  szűrőket logikai operátorokkal Java-ban.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Java fájlkiterjesztések szűrése a GroupDocs.Search segítségével – Teljes
  útmutató
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Hogyan szűrhetünk java fájlkiterjesztéseket a GroupDocs.Search segítségével
type: docs
url: /hu/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Fájl kiterjesztések szűrése java-val a GroupDocs.Search segítségével

Ebben az átfogó útmutatóban megtanulja, hogyan **filter file extensions java** szűrje a fájl kiterjesztéseket a dokumentumok indexelése során a GroupDocs.Search segítségével. A útmutató végére képes lesz csak a szükséges fájltípusokat belefoglalni, a nem kívánt formátumokat kizárni, és ezeket a szabályokat dátumtartomány- és útvonal-szűrőkkel kombinálni logikai AND, OR és NOT operátorokkal. Ez a megközelítés karcsúbb indexet eredményez, felgyorsítja a kereséseket, és segít megfelelni az adatkezelési szabályzatoknak.

## Gyors válaszok
- **What is the java file extension filter?** Ez egy szabály, amely megmondja a GroupDocs.Search-nek, mely fájl kiterjesztéseket kell belefoglalni vagy kizárni az indexelés során.  
- **Which library provides this feature?** GroupDocs.Search for Java.  
- **Do I need a license?** Egy ingyenes próba a kiértékeléshez elegendő; a teljes licenc a termeléshez szükséges.  
- **Can I combine filters?** Igen – láncolhatja a kiterjesztés, dátum, méret és útvonal szűrőket AND, OR, NOT logikával.  
- **Is it Maven‑compatible?** Teljesen – adja hozzá a GroupDocs.Search függőséget a `pom.xml`-hez.

## Mi a java file extension filter?
A **java file extension filter** egy szabálykészlet, amely minden fájl kiterjesztését értékeli ki, mielőtt az indexelő motorhoz kerülne. Ha megadja a `.txt`, `.pdf` vagy `.epub` kiterjesztéseket, **include files by extension** vagy **exclude files by extension** segítségével szűkítheti az indexet és releváns keresési eredményeket érhet el.

## Miért használjon file‑extension szűrést a GroupDocs.Search‑ben?
A file‑extension szűrés javítja az indexelés hatékonyságát az irreleváns formátumok kizárásával, csökkenti a tárolási igényeket, és segít megfelelni a megfelelőségi szabályoknak azáltal, hogy megakadályozza a nem kívánt tartalom indexelését. Emellett gyorsabb lekérdezési válaszokat tesz lehetővé, mivel a keresőmotor egy kisebb, relevánsabb adathalmazt dolgoz fel.

- **Performance:** A nem kívánt fájlok kihagyása csökkenti az I/O-t és akár 40 %-kal gyorsítja az indexelést nagy tárolók esetén.  
- **Storage savings:** Csak a releváns dokumentumok kerülnek az indexbe, ami átlagosan 30 % lemezhasználat csökkenést eredményez.  
- **Compliance:** Megakadályozza a bizalmas vagy nem támogatott fájltípusok véletlen indexelését.  
- **Flexibility:** Kombinálható **date range filter java** funkciókkal a specifikus időszakban létrehozott vagy módosított fájlok célzásához.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy a következőkkel rendelkezik:

### Szükséges könyvtárak és függőségek
- **GroupDocs.Search for Java** – version 25.4 vagy újabb (támogat 60+ bemeneti formátumot).  
- **Java Development Kit (JDK)** – bármely kompatibilis verzió (8 vagy újabb).

### Fejlesztőkörnyezet beállítása
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse vagy bármely Maven‑compatible IDE.

### Tudás előfeltételek
- Alapvető Java programozás.  
- Fájl I/O ismerete Java-ban.  
- Reguláris kifejezések és dátum‑idő kezelés megértése.

## A GroupDocs.Search beállítása Java-hoz
A GroupDocs.Search használatához hozzá kell adnia azt függőségként a projektjéhez.

### Maven konfiguráció
Adja hozzá a következő tárolót és függőségkonfigurációt a `pom.xml` fájlhoz:

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
Alternatívaként töltse le a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

#### Licenc beszerzése
1. **Free trial** – a funkciók felfedezése költség nélkül.  
2. **Temporary license** – teljes funkcionalitás korlátozott időre.  
3. **Purchase** – állandó licenc a termelési használathoz.

### Alap inicializálás és beállítás
Miután a könyvtár hozzá lett adva, inicializálja az indexelési környezetet. Az `IndexSettings` osztály tartalmazza az összes konfigurációs lehetőséget, beleértve a szűrőket.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Implementációs útmutató
Az alábbiakban minden szűrőtípusra részletesen kitérünk, elmagyarázva **why it matters**, és lépésről‑lépésre útmutatást adunk, amelyet a projektjébe másolhat.

### Fájl kiterjesztés szűrés
Szűrje a fájlokat kiterjesztésük alapján az indexelés során. Ez tökéletes, ha csak e‑könyveket (`.fb2`, `.epub`) és egyszerű szövegfájlokat (`.txt`) szeretne feldolgozni.

#### Áttekintés
`DocumentFilter.createFileExtension` egy fehérlistát hoz létre a kiterjesztésekből.

#### Implementációs lépések
1. **Create filter** – határozza meg a megtartani kívánt kiterjesztéseket.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – alkalmazza a szűrőt az `IndexSettings` létrehozásakor.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logikai NOT szűrő
Zárjon ki bizonyos kiterjesztéseket, például weboldalakat és PDF-eket, ha azok nem szükségesek a keresési forgatókönyvéhez.

#### Implementációs lépések
1. **Create exclusion filter** – adja meg a kizárandó kiterjesztéseket.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – kombinálja a NOT szűrőt más szabályokkal.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – csak a kombinált szűrőt átmenő fájlok kerülnek indexelésre.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logikai AND szűrő
Kombináljon több feltételt – létrehozási dátum, kiterjesztés és fájlméret – úgy, hogy **only files that meet all criteria** kerülnek indexelésre.

#### Áttekintés
`DocumentFilter.createAnd` több szűrőt egyetlen szabályná egyesít.

#### Implementációs lépések
1. **Define filters** – hozzon létre egyedi szűrőket minden feltételhez.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – használja az AND operátort az összes feltétel megköveteléséhez.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – adja át a kombinált szűrőt az indexelési csővezetéknek.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logikai OR szűrő
Vegye fel a fájlokat, amelyek **any** a megadott feltételeknek megfelelnek – hasznos, ha kis szövegfájlokat és nagyobb nem‑szöveg fájlokat egyaránt szeretne lefedni.

#### Implementációs lépések
1. **Define filters** – hozzon létre különálló szűrőket minden alternatív feltételhez.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – használja az OR operátort.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – csatolja a kombinált szűrőt az index konfigurációjához.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Létrehozási idő szűrők
Célzottan indexeljen olyan fájlokat, amelyek egy adott időszakban lettek létrehozva – klasszikus **date range filter java** eset.

#### Implementációs lépések
1. **Define date‑range filter** – adja meg a kezdő és befejező dátumokat.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – csak azok a fájlok kerülnek indexelésre, amelyek létrehozási időbélyege a tartományon belül van.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Módosítási idő szűrők
Zárja ki azokat a fájlokat, amelyeket egy bizonyos határidő után módosítottak.

#### Implementációs lépések
1. **Define filter** – állítsa be a maximális módosítási időbélyeget.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – a határidőnél újabb fájlok figyelmen kívül maradnak.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Fájl útvonal szűrés
Korlátozza az indexelést olyan fájlokra, amelyek meghatározott mappákban vagy egy mintának megfelelően helyezkednek el – ideális **include files by extension** egy adott könyvtárhierarchián belül.

#### Implementációs lépések
1. **Define file‑path filter** – használjon glob vagy regex mintákat a könyvtárak egyezéséhez.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – alkalmazza az útvonal‑szűrőt a többi szabállyal együtt.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Gyakori buktatók és tippek

- **Never mix absolute and relative paths** ugyanabban a szűrőkonfigurációban – ez váratlan kizárásokhoz vezethet.  
- **Reset the `IndexSettings`** szűrők cseréjekor; ellenkező esetben a korábbi szűrők megmaradhatnak.  
- **Combine a length upper bound with an extension filter** nagy gyűjteményeknél a memóriahasználat csökkentése érdekében.  
- LoggingOptions szabályozza a GroupDocs.Search naplózási beállításait.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) a fájlok elutasításának okának megtekintéséhez.  

## Gyakran feltett kérdések

**Q: Can I change the filter criteria after the index is created?**  
A: Igen. Építse újra az indexet egy új `DocumentFilter` segítségével, vagy használjon inkrementális indexelést frissített beállításokkal.

**Q: Does the java file extension filter work on compressed archives (e.g., ZIP)?**  
A: A GroupDocs.Search képes indexelni a támogatott archívumformátumokat, de a kiterjesztés‑szűrő az archívumra, nem a belső fájlokra vonatkozik. Használjon beágyazott szűrőket a mélyebb vezérléshez.

**Q: How do I debug why a particular file was excluded?**  
A: Engedélyezze a könyvtár naplózását (`LoggingOptions.setEnabled(true)`) és ellenőrizze a naplót – az jelzi, melyik szűrő utasította el az adott fájlt.

**Q: Is it possible to combine the java file extension filter with custom regex filters?**  
A: Teljesen lehetséges. Egy regex szűrőt csomagoljon be a `DocumentFilter.createAnd()`‑be a kiterjesztés‑szűrő mellett.

**Q: What performance impact does adding many filters have?**  
A: Minden szűrő mérsékelt terhelést ad az indexeléshez, de a indexelt adatok csökkenése általában felülmúlja a költséget. Teszteljen egy reprezentatív mintán a legoptimálisabb egyensúly megtalálásához.

---

**Last Updated:** 2026-09-06  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Kapcsolódó útmutatók

- [Custom Date Format Java | Date Range Search with GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Master Boolean Searches with GroupDocs.Search for Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Optimize Search Performance with Advanced Indexing Techniques in GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

