---
date: '2025-12-18'
description: Tanulja meg, hogyan valósíthat meg egyedi dátumformátumú Java-kereséseket
  a GroupDocs.Search segítségével, beleértve a dátumtartomány-kereséseket, egyedi
  mintákat és a teljesítményre vonatkozó tippeket.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'Egyéni dátumformátum Java: Dátumtartomány keresés a GroupDocs-szal'
type: docs
url: /hu/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Egyedi dátumformátum Java: Dátumtartomány keresés a GroupDocs-szal

A dokumentumok dátum szerinti keresése gyakori követelmény—legyen szó archiválási rendszerről, pénzügyi jelentéskészítő eszközről vagy tartalomkezelő portálról. Ebben az útmutatóban a **custom date format java** technikákat tanulod meg a GroupDocs.Search használatával, beleértve a dátumtartomány lekérdezéseket, egyedi mintadefiníciókat és tippeket a **search performance** optimalizálásához. A végére képes leszel arra, hogy a felhasználók bármilyen dátumintervallumba eső rekordokat lekérjék, függetlenül a használt formátumtól.

## Gyors válaszok
- **Mi a fő osztály az indexeléshez?** `Index` from the `com.groupdocs.search` package.  
- **Hogyan definiálhat egy egyedi dátummintát?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Kereshetek szöveges lekérdezéssel?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Mely Maven koordináták szükségesek?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Szükségem van licencre a fejlesztéshez?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## Mi az a **custom date format java**?
A **custom date format java** megmondja a GroupDocs.Search-nek, hogyan értelmezze a dátumkarakterláncokat, amelyek nem követik az alapértelmezett ISO mintát (YYYY‑MM‑DD). Saját minta definiálásával—például `MM/dd/yyyy` vagy `dd‑MM‑yyyy`—lehetővé teszi a motor számára, hogy felismerje a dokumentumokban beágyazott dátumokat, amelyek regionális vagy régi formátumokat használnak.

## Miért használja a GroupDocs.Search-t dátumtartomány lekérdezésekhez?
- **Sebesség:** A beépített indexelés O(log n) kereséseket tesz lehetővé.  
- **Rugalmasság:** Támogatja a szöveges és objektumalapú lekérdezéskészítést is.  
- **Többformátumú támogatás:** Kezeli a PDF-eket, Word, Excel, egyszerű szöveget és egyebeket extra kód nélkül.

## Hogyan **keressen dokumentumokat dátum szerint** a GroupDocs.Search-szel
Az alábbiakban egy lépésről‑lépésre útmutatót találsz, amely végigvezet a könyvtár beállításán, a fájlok indexelésén és az egyszerű és fejlett dátumtartomány keresések végrehajtásán.

### Előkövetelmények
- Java 8 vagy újabb telepítve.  
- Maven a függőségkezeléshez.  
- Hozzáférés egy GroupDocs.Search licenchez (próba vagy ideiglenes licenc a fejlesztéshez megfelelő).

### A GroupDocs.Search beállítása Java-hoz

#### Telepítés Maven használatával
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

#### Közvetlen letöltés
Alternatívaként letöltheti a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

#### Alap inicializálás és beállítás
Hozzon létre egy `Index` példányt, és adja hozzá a dokumentumait:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## 1. funkció: Dátumtartomány keresési lekérdezések létrehozása

### Szöveges forma lekérdezés használata
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

**Magyarázat**: A `daterange` szintaxis a dátumokat `YYYY‑MM‑DD` formátumban várja. Az összes olyan dokumentumot visszaadja, amelynek indexelt dátuma az intervallumba esik.

### Lekérdezés objektum használata
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

**Magyarázat**: A `createDateRangeQuery` lehetővé teszi, hogy `java.util.Date` objektumokat adjon meg, teljes rugalmasságot biztosítva az időzónák és a helyspecifikus kezelés tekintetében.

## 2. funkció: **custom date format java** minták megadása

### Egyedi dátumformátumok beállítása
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

**Magyarázat**: Az alapértelmezett formátumok törlésével és egy `/` elválasztót használó `DateFormat` hozzáadásával a motor most már érti a `MM/dd/yyyy` formátumú dátumokat. Ez elengedhetetlen a **search documents by date** funkcióhoz olyan régiókban, ahol a hónap‑első jelölés a preferált.

## Tippek a **search performance** optimalizálásához
- **Indexelés fokozatosan**: Új fájlokat adjon a meglévő indexhez ahelyett, hogy a semmiből újraépítené.  
- **Elavult adatok tisztítása**: Időnként távolítsa el a már nem szükséges dokumentumokat.  
- **Memória beállítások módosítása**: Növelje a JVM heap méretét (`-Xmx`), ha nagy indexekkel dolgozik.

## Gyakori problémák és megoldások
- **Dátumfeldolgozási hibák**: Ellenőrizze, hogy a dokumentum dátumkarakterláncai pontosan egyeznek-e a definiált egyedi mintával.  
- **Hiányzó eredmények**: Győződjön meg arról, hogy az indexelt mezők tartalmazzák a dátum metaadatokat; ellenkező esetben a motor nem tudja egyeztetni a dátum lekérdezéseket.  
- **Index hozzáférési kivételek**: Ellenőrizze, hogy az `indexFolder` útvonal írható-e, és nincs-e más folyamat által zárolva.

## Gyakorlati alkalmazások
1. **Archiválási rendszerek** – Rekordok lekérdezése egy adott történelmi időszakból.  
2. **Tartalomkezelés** – Regionális dátumformátumok támogatása, például `dd/MM/yyyy` az európai felhasználók számára.  
3. **Pénzügyi szoftver** – Tranzakciók gyors szűrése pénzügyi negyedév vagy év szerint.

## Következtetés
Most már rendelkezik egy teljes **custom date format java** eszköztárral a hatékony dátumtartomány keresések felépítéséhez a GroupDocs.Search segítségével. Alkalmazza ezeket a mintákat, finomhangolja a teljesítményt, és alkalmazása gyors, pontos eredményeket fog nyújtani bármely időbeli lekérdezéshez.

## Gyakran Ismételt Kérdések

**Q: Mi a különbség a szöveges forma és az objektumalapú dátum lekérdezések között?**  
A: A szöveges forma gyors és egyszerű, de csak az alapértelmezett ISO formátumra korlátozódik; az objektumalapú lekérdezések lehetővé teszik `Date` objektumok és egyedi formátumok megadását a nagyobb rugalmasság érdekében.

**Q: Kereshetek több dátumtartományt egyetlen lekérdezésben?**  
A: Igen, kombinálja a `daterange` feltételeket logikai operátorokkal, például `AND` vagy `OR`, hogy összetett lekérdezéseket építsen.

**Q: Lassítják-e az egyedi dátumformátumok a keresést?**  
A: Van egy kisebb többletterhelés a további feldolgozás miatt, de a hatás elhanyagolható a tipikus munkaterhelések esetén, és felülmúlja a pontosság növekedése.

**Q: Alkalmas a GroupDocs.Search nagy léptékű telepítésekhez?**  
A: Teljes mértékben. Megfelelő indexelési stratégiákkal és JVM hangolással több millió dokumentumra is skálázható.

**Q: Hol találhatok további Java példákat?**  
A: Tekintse meg a [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) oldalt további minták és felhasználási esetek megvalósításaiért.

---

**Erőforrások**

- **Dokumentáció**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API referencia**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Letöltés**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub tároló**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ingyenes támogatási fórum**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Ideiglenes licenc**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Utolsó frissítés:** 2025-12-18  
**Tesztelve a következővel:** GroupDocs.Search Java 25.4  
**Szerző:** GroupDocs