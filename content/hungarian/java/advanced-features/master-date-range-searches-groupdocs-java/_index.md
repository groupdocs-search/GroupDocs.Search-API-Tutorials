---
date: '2026-03-04'
description: Tanulja meg, hogyan valósítható meg egyedi dátumformátumú Java-keresés
  a GroupDocs.Search segítségével, beleértve a dátumtartomány-kereséseket, egyedi
  mintákat és a teljesítményre vonatkozó tippeket.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: Egyéni dátumformátum Java | Dátumtartomány keresés a GroupDocs-szal
type: docs
url: /hu/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Egyedi dátumformátum Java | Dátumtartomány keresés a GroupDocs-szal

A dokumentumok dátum szerinti keresése gyakori igény—legyen szó archiváló rendszerről, pénzügyi jelentéskészítő eszközről vagy tartalomkezelő portálról. Ebben az útmutatóban **custom date format java** technikákat tanul meg a GroupDocs.Search használatával, beleértve a dátumtartomány lekérdezéseket, egyedi minták definiálását és tippeket a **optimize search performance** javításához. A végére képes lesz arra, hogy a felhasználók bármilyen dátumintervallumba eső rekordokat lekérjék, függetlenül a használt formátumtól.

## Gyors válaszok
- **Mi a fő osztály az indexeléshez?** `Index` a `com.groupdocs.search` csomagból.  
- **Hogyan definiálhatok egy egyedi dátummintát?** Használja a `DateFormat`-ot `DateFormatElement` objektumokkal és egy elválasztóval.  
- **Kereshetek szöveges lekérdezéssel?** Igen, a `daterange(start ~~ end)` szintaxis közvetlenül a lekérdezés karakterláncában működik.  
- **Mely Maven koordináták szükségesek?** `com.groupdocs:groupdocs-search:25.4` (vagy újabb).  
- **Szükségem van licencre fejlesztéshez?** Egy ingyenes próba vagy ideiglenes licenc elegendő a teszteléshez; a termeléshez kereskedelmi licenc szükséges.

## Mi az **custom date format java**?
A **custom date format java** megmondja a GroupDocs.Search-nek, hogyan értelmezze azokat a dátumkarakterláncokat, amelyek nem követik az alapértelmezett ISO mintát (YYYY‑MM‑DD). Saját minta definiálásával—például `MM/dd/yyyy` vagy `dd‑MM‑yyyy`—lehetővé teszi, hogy a motor felismerje a regionális vagy régi formátumú dokumentumokban található dátumokat.

## Miért használjuk a GroupDocs.Search-t dátumtartomány lekérdezésekhez?
- **Sebesség:** A beépített indexelés O(log n) kereséseket tesz lehetővé.  
- **Rugalmasság:** Támogatja a szöveges és objektumalapú lekérdezés létrehozását.  
- **Több formátum támogatása:** Kezeli a PDF-eket, Word, Excel, egyszerű szöveget és egyebeket extra kód nélkül.  

## Hogyan **search documents by date** a GroupDocs.Search-szel
Az alábbiakban egy lépésről‑lépésre útmutatót talál, amely végigvezeti a könyvtár beállításán, a fájlok indexelésén és egyszerű, valamint fejlett dátumtartomány keresések végrehajtásán.

### Prerequisites
- Java 8 vagy újabb telepítve.  
- Maven a függőségkezeléshez.  
- Hozzáférés egy GroupDocs.Search licenchez (próba vagy ideiglenes licenc fejlesztéshez).  

### Setting Up GroupDocs.Search for Java

#### Installation Using Maven
Adja hozzá a tárolót és a függőséget a `pom.xml`-hez:

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

#### Direct Download
Alternatívaként letöltheti a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

#### Basic Initialization and Setup
Hozzon létre egy `Index` példányt, és adja hozzá a dokumentumokat:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Feature 1: Creating Date Range Search Queries

### Using Text Form Query
A legegyszerűbb mód, ha a dátumtartományt közvetlenül a lekérdezés karakterláncába ágyazza:

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

**Magyarázat**: A `daterange` szintaxis `YYYY‑MM‑DD` formátumú dátumokat vár. Visszaadja az összes dokumentumot, amelynek indexelt dátuma az intervallumba esik.

### Using Query Object
Programozott vezérléshez és egyedi feldolgozáshoz építsen egy `SearchQuery` objektumot:

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

**Magyarázat**: A `createDateRangeQuery` lehetővé teszi `java.util.Date` objektumok megadását, teljes rugalmasságot biztosítva az időzónák és a helyspecifikus kezelések felett.

## Feature 2: Specifying **custom date format java** Patterns

### Setting Custom Date Formats
Definiáljon egy `DateFormat`-ot, amely megfelel a dokumentum dátumábrázolásának:

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

**Magyarázat**: Az alapértelmezett formátumok törlésével és egy `/` elválasztót használó `DateFormat` hozzáadásával a motor most már érti a `MM/dd/yyyy` formátumban írt dátumokat. Ez elengedhetetlen a **search documents by date** funkcióhoz olyan régiókban, ahol a hónap‑előtti jelölést részesítik előnyben.

## Tips to **optimize search performance**
- **Index Incrementally**: Új fájlok hozzáadása a meglévő indexhez ahelyett, hogy a semmiből újraépítené.  
- **Prune Stale Data**: Időnként távolítsa el a már nem szükséges dokumentumokat.  
- **Adjust Memory Settings**: Növelje a JVM heap méretét (`-Xmx`) nagy indexek esetén.  

## Common Issues and Solutions
- **Date Parsing Errors**: Ellenőrizze, hogy a dokumentum dátumkarakterláncai pontosan egyeznek-e a definiált egyedi mintával.  
- **Missing Results**: Győződjön meg róla, hogy az indexelt mezők tartalmazzák a dátum metaadatait; egyébként a motor nem tud dátum lekérdezéseket egyezni.  
- **Index Access Exceptions**: Ellenőrizze, hogy az `indexFolder` útvonal írható-e, és nincs-e más folyamat által zárolva.  

## Practical Applications
1. **Archival Systems** – Rekordok lekérdezése egy adott történelmi időszakból.  
2. **Content Management** – Regionális dátumformátumok támogatása, például `dd/MM/yyyy` az európai felhasználók számára.  
3. **Financial Software** – Tranzakciók gyors szűrése pénzügyi negyedév vagy év szerint.  

## Why This Matters
A **custom date format java** kezelés bevezetése megszünteti a különböző dátumábrázolások közti súrlódást a dokumentumokban. Lehetővé teszi, hogy egyetlen indexben több dátumformátumot kezeljen, biztosítva, hogy a végfelhasználók pontos eredményeket kapjanak, függetlenül attól, hogyan rögzítették a dátumokat eredetileg.

## Next Steps
- Fedezze fel a fejlettebb lekérdezés kombinációkat az `AND`, `OR` és `NOT` operátorokkal.  
- Kísérletezzen egyedi elemzőkkel, ha további időbeli metaadatokat kell indexelni.  
- Tekintse át a teljesítményhangolási útmutatót a hivatalos dokumentációban, hogy megoldását millió dokumentumra skálázza.

## Frequently Asked Questions

**Q: Mi a különbség a szöveges és az objektumalapú dátumlekérdezések között?**  
A: A szöveges forma gyors és egyszerű, de csak az alapértelmezett ISO formátumra korlátozódik; az objektumalapú lekérdezések lehetővé teszik `Date` objektumok és egyedi formátumok megadását a nagyobb rugalmasság érdekében.

**Q: Kereshetek több dátumtartományt egyetlen lekérdezésben?**  
Igen, kombinálja a `daterange` klauzulákat logikai operátorokkal, például `AND` vagy `OR`, összetett lekérdezések építéséhez.

**Q: Lassítják-e az egyedi dátumformátumok a keresést?**  
Van egy kisebb többletterhelés a további elemzés miatt, de a hatás elhanyagolható a tipikus munkaterhelések esetén, és felülmúlja a pontosságnövekedés előnye.

**Q: Alkalmas a GroupDocs.Search nagy‑léptékű telepítésekhez?**  
Abszolút. Megfelelő indexelési stratégiákkal és JVM hangolással millió dokumentumra is skálázható.

**Q: Hol találok további Java példákat?**  
Fedezze fel a [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) oldalt további minták és felhasználási esetek megtekintéséhez.

---

**Resources**

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support Forum**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-03-04  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs