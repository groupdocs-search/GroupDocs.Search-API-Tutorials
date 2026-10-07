---
date: '2026-10-07'
description: Ismerje meg, hogyan valósíthatja meg a custom date format java kereséseket
  a GroupDocs-szal, a date range queries, a custom patterns és a performance tips
  témákat lefedve.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: A Custom date format java tutorial bemutatja, hogyan konfigurálja
  a GroupDocs.Search for Java-t, futtassa a date range queries-t, és növelje a performance-ot.
  Kövesse a step‑by‑step példákat.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Custom date format java – útmutató a date range search-hez a GroupDocs-szal
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Custom date format java | dátumtartomány keresés a GroupDocs-szal
type: docs
url: /hu/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Egyedi dátumformátum Java | dátumtartomány keresés a GroupDocs-szal

A dokumentumok dátum szerinti keresése gyakori követelmény—legyen szó archiváló rendszerről, pénzügyi jelentéskészítő eszközről vagy tartalomkezelő portálról. Ebben az útmutatóban a **custom date format java** technikákat tanulod meg a GroupDocs.Search használatával, beleértve a dátumtartomány lekérdezéseket, egyedi mintadefiníciókat és tippeket a **a keresési teljesítmény optimalizálása**. A végére képes leszel a felhasználókat arra, hogy bármilyen dátumintervallumba eső rekordokat lekérjék, függetlenül a használt formátumtól.

## Gyors válaszok
- **Mi a fő osztály az indexeléshez?** `Index` a `com.groupdocs.search` csomagból.  
- **Hogyan definiálsz egy egyedi dátummintát?** Használd a `DateFormat`-ot `DateFormatElement` objektumokkal és egy elválasztóval.  
- **Kereshetek szöveges lekérdezéssel?** Igen, a `daterange(start ~~ end)` szintaxis közvetlenül a lekérdezés karakterláncában működik.  
- **Mely Maven koordináták szükségesek?** `com.groupdocs:groupdocs-search:25.4` (vagy újabb).  
- **Szükségem van licencre a fejlesztéshez?** Egy ingyenes próba vagy ideiglenes licenc elegendő a teszteléshez; a termeléshez kereskedelmi licenc szükséges.

## Mi az a custom date format java?
A custom date format java megmondja a GroupDocs.Search-nek, hogyan értelmezze a dátumkarakterláncokat, amelyek nem követik az alapértelmezett ISO mintát (YYYY‑MM‑DD). Saját minta definiálásával—például `MM/dd/yyyy` vagy `dd‑MM‑yyyy`—lehetővé teszed, hogy a motor felismerje a dokumentumokban beágyazott dátumokat, amelyek regionális vagy régi formátumokat használnak. Ez a képesség lehetővé teszi a dátumok konzisztens indexelését és lekérdezését heterogén források között, javítva a visszahívást és a pontosságot a dátum‑központú keresésekben.

## Miért használjuk a GroupDocs.Search-t dátumtartomány lekérdezésekhez?
A GroupDocs.Search a nagy sebességű indexelést rugalmas lekérdezésépítéssel kombinálja, így ideális a dátumtartományos helyzetekhez. A motor gyorsan megtalálja azokat a dokumentumokat, amelyek egy megadott intervallumban lévő dátumokat tartalmaznak, még akkor is, ha ezek a dátumok szabad szövegben vagy metaadatmezőkben jelennek meg. Beépített támogatása több fájlformátumhoz és testreszabható dátumértelmezőkhöz azt jelenti, hogy külön formátumra írt kód nélkül kezelheted a változatos dokumentumgyűjteményeket, miközben almásodperces válaszidőket érhetsz el nagy indexeknél.

## Hogyan keressünk dokumentumokat dátum szerint a GroupDocs.Search-szal
Beállítod a könyvtárat, indexelsz egy minta mappát, majd egyszerű szöveges lekérdezéseket és összetettebb objektumalapú lekérdezéseket is futtatsz. A folyamat egy `Index` példány létrehozásával kezdődik, a szükséges egyedi dátumformátumok konfigurálásával, majd a keresési API meghívásával akár egyszerű karakterlánccal, akár strukturált `SearchQuery`-val. Ez a megközelítés lehetővé teszi, hogy a alkalmazásod igényeihez illeszkedő vezérlési szintet válaszd.

### Előfeltételek
- Java 8 vagy újabb telepítve.  
- Maven a függőségkezeléshez.  
- Hozzáférés egy GroupDocs.Search licenchez (próba vagy ideiglenes licenc a fejlesztéshez megfelelő).

### A GroupDocs.Search beállítása Java-hoz

#### Telepítés Maven használatával
Add hozzá a tárolót és a függőséget a `pom.xml`-hez:

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

#### Közvetlen letöltés
Alternatívaként letöltheted a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

#### Alapvető inicializálás és beállítás
Hozz létre egy `Index` példányt, és add hozzá a dokumentumaidat:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** A `Index` osztály a fő tároló, amely minden hozzáadott fájl kereshető metaadatait tárolja, lehetővé téve a gyors keresést nagy gyűjteményekben.

## 1. funkció: dátumtartomány keresési lekérdezések létrehozása

### Szöveges lekérdezés használata
A legegyszerűbb mód, ha a dátumtartományt közvetlenül a lekérdezés karakterláncába ágyazod:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** Töltsd be az indexet, majd hívd meg a `search("daterange(2022-01-01 ~~ 2022-12-31)")` függvényt, hogy minden olyan dokumentumot lekérj, amelynek indexelt dátuma 2022. január 1. és 2022. december 31. között van. Ez az egy soros lekérdezés azonnal működik, és a relevancia szerint rendezett eredményeket ad.

**Explanation:** A `daterange` szintaxis `YYYY‑MM‑DD` formátumú dátumokat vár. Visszaadja az összes olyan dokumentumot, amelynek indexelt dátuma az intervallumba esik.

### Lekérdezés objektum használata
Programozott vezérlés és egyedi feldolgozás esetén építs egy `SearchQuery` objektumot. A `SearchQuery` osztály egy strukturált lekérdezést képvisel, amely több kritériumot kombinálhat, például kulcsszavakat, szűrőket és dátumtartományokat.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** Hozz létre egy `SearchQuery`-t a `createDateRangeQuery(startDate, endDate)` segítségével, ahol a `startDate` és `endDate` `java.util.Date` példányok; majd add át a lekérdezést az `index.search(query)`-nek, hogy pontos eredményeket kapj, amelyek figyelembe veszik az időzóna eltolásokat és a helyspecifikus naptárakat.

**Definition anchor:** A `SearchQuery` osztály magába foglalja az összes keresési kritériumot, lehetővé téve a dátumtartományok kombinálását kulcsszó szűrőkkel, logikai operátorokkal és erősítési szabályokkal.

**Explanation:** A `createDateRangeQuery` lehetővé teszi `java.util.Date` objektumok megadását, teljes rugalmasságot biztosítva az időzónák és a helyspecifikus kezelés tekintetében.

## 2. funkció: egyedi custom date format java minták megadása

### Egyedi dátumformátumok beállítása
A `DateFormat` osztály megmondja a motornak, hogyan bontsa fel és értelmezze a dátumkarakterláncot az elemek sorrendje és az elválasztó karakterek alapján. Definiálj egy `DateFormat`-ot, amely megfelel a dokumentumod dátumábrázolásának:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** Töröld a alapértelmezett formátumokat a `dateFormat.clear()`-val, majd adj hozzá egy új `DateFormat`-ot, amely `DateFormatElement` objektumokból (hónap, nap, év) épül, és állítsd be az elválasztót `/`-ra. Ezután a motor helyesen fogja értelmezni a `MM/dd/yyyy` formátumú dátumokat indexelés és lekérdezés során.

**Definition anchor:** A `DateFormat` egy konfigurációs objektum, amely megmondja a GroupDocs.Search-nek, hogyan bontsa fel és értelmezze a dátumkarakterláncot az elemek sorrendje és az elválasztó karakterek alapján.

**Explanation:** Az alapértelmezett formátumok törlésével és egy `/` elválasztót használó `DateFormat` hozzáadásával a motor most már érti a `MM/dd/yyyy` formátumú dátumokat. Ez elengedhetetlen a **search documents by date** funkcióhoz olyan régiókban, ahol a hónap‑első jelölés a preferált.

## Tippek a keresési teljesítmény optimalizálásához
- **Indexelés fokozatosan:** Új fájlokat adj hozzá a meglévő indexhez ahelyett, hogy a semmiből újraépítenéd; ez akár 70 %-kal csökkenti a CPU használatot a napi frissítéseknél.  
- **Elavult adatok eltávolítása:** Időnként távolíts el már nem szükséges dokumentumokat; egy karcsú index javítja a gyorsítótár találati arányát és csökkenti a lekérdezés késleltetését.  
- **Memória beállítások módosítása:** Növeld a JVM heap méretét (`-Xmx4g` vagy nagyobb) 5 GB-nál nagyobb indexek esetén, hogy elkerüld a memória kifogyását.  
- **Többszálú indexelés engedélyezése:** Használd a `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())`-t a dokumentumfeldolgozás párhuzamosításához, és csökkentsd az indexelési időt a CPU magok számával arányosan.

## Gyakori problémák és megoldások
- **Dátumértelmezési hibák:** Ellenőrizd, hogy a dokumentum dátumkarakterláncai pontosan megfelelnek a definiált egyedi mintának; a nem egyező elválasztók vagy a hiányzó vezető nullák hibákat okoznak.  
- **Hiányzó eredmények:** Győződj meg arról, hogy az indexelt mezők tartalmaznak dátum metaadatokat; ha egy dokumentum csak szabad szöveges bekezdésekben tartalmaz dátumokat, engedélyezd az `ExtractDateMetadata` opciót indexelés közben.  
- **Index hozzáférési kivételek:** Ellenőrizd, hogy az `indexFolder` útvonal írható és nincs más folyamat által zárolva; használj dedikált mappát környezetenként (dev, test, prod) a konfliktusok elkerülése érdekében.

## Gyakorlati alkalmazások
1. **Archiváló rendszerek** – Szerezd be a rekordokat egy adott történelmi időszakból anélkül, hogy manuálisan normalizálnád a dátumokat.  
2. **Tartalomkezelés** – Támogasd a regionális dátumformátumokat, például `dd/MM/yyyy`-t az európai felhasználók számára, növelve a felhasználói elégedettséget.  
3. **Pénzügyi szoftver** – Gyorsan szűrd a tranzakciókat pénzügyi negyedév vagy év szerint, lehetővé téve a valós idejű jelentéskészítő irányítópultokat.

## Miért fontos ez
A **custom date format java** kezelés bevezetése megszünteti a dokumentumok közötti egységtelen dátumábrázolásokkal kapcsolatos súrlódásokat. Lehetővé teszi, hogy egyetlen indexben **multiple date formats**-t kezelj, biztosítva, hogy a végfelhasználók pontos eredményeket kapjanak, függetlenül attól, hogyan rögzítették a dátumokat eredetileg. Ez a rugalmasság javítja a keresési relevanciát, csökkenti az előfeldolgozási munkát, és lerövidíti a dátum‑központú alkalmazások értékteremtési idejét.

## Következő lépések
- Fedezz fel fejlettebb lekérdezéskombinációkat a `AND`, `OR` és `NOT` operátorok használatával.  
- Kísérletezz egyedi elemzőkkel, ha további időbeli metaadatokat, például XML címkékbe ágyazott időbélyegeket kell indexelned.  
- Tekintsd át a teljesítményhangolási útmutatót a hivatalos dokumentációban, hogy megoldásodat millió dokumentumra és többbérlős környezetekre skálázhasd.

## Gyakran ismételt kérdések

**Q: Mi a különbség a szöveges és az objektumalapú dátumlekérdezések között?**  
A: A szöveges forma gyors és egyszerű, de csak az alapértelmezett ISO formátumra korlátozódik; az objektumalapú lekérdezések lehetővé teszik `Date` objektumok és egyedi formátumok megadását a nagyobb rugalmasság érdekében.

**Q: Kereshetek több dátumtartományt egyetlen lekérdezésben?**  
A: Igen, kombináld a `daterange` klauzulákat logikai operátorokkal, például `AND` vagy `OR`, hogy összetett lekérdezéseket építs.

**Q: Lassítják a keresést az egyedi dátumformátumok?**  
A: Van egy kisebb többletterhelés az extra feldolgozás miatt, de a hatás elhanyagolható a tipikus terhelések esetén, és felülmúlja a pontosságnövekedés előnye.

**Q: Alkalmas a GroupDocs.Search nagy léptékű telepítésekhez?**  
A: Teljes mértékben. Megfelelő indexelési stratégiákkal és JVM hangolással millió dokumentumra skálázható, miközben almásodperces lekérdezési válaszidőket tart fenn.

**Q: Hol találhatok több Java példát?**  
A: Tekintsd meg a [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) oldalt további minták és felhasználási esetek megvalósításához.

---

**Erőforrások**

- **Dokumentáció:** [GroupDocs Search dokumentáció](https://docs.groupdocs.com/search/java/)
- **API referencia:** [GroupDocs API referencia](https://reference.groupdocs.com/search/java)
- **Letöltés:** [A legújabb verzió letöltése itt](https://releases.groupdocs.com/search/java/)
- **GitHub tároló:** [GroupDocs GitHub tároló](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Megtekintés a GitHub-on:** [Megtekintés a GitHub-on](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ingyenes támogatási fórum:** [Csatlakozz a beszélgetéshez](https://forum.groupdocs.com/c/search/10)
- **Ideiglenes licenc:** [Ideiglenes licenc beszerzése itt](https://purchase.groupdocs.com/temporary-license/)

**Legutóbb frissítve:** 2026-10-07  
**Tesztelt verzió:** GroupDocs.Search Java 25.4  
**Szerző:** GroupDocs  

## Kapcsolódó oktatóanyagok

- [Groupdocs Search Java haladó keresési funkciók](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Java teljes szöveges keresőkönyvtár – Index optimalizálása a GroupDocs.Search-szal](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Hogyan adjunk dokumentumokat az indexhez metaadat-indexeléssel Java-ban a GroupDocs.Search használatával](/search/java/indexing/groupdocs-search-java-metadata-indexing/)