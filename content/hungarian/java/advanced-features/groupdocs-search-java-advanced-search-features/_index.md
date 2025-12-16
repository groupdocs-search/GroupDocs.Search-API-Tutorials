---
date: '2025-12-16'
description: Tanulja meg, hogyan végezzen dátumtartomány-keresést és más fejlett keresési
  funkciókat, például facettált keresést Java-ban a GroupDocs.Search for Java használatával,
  beleértve a hibakezelést és a teljesítményoptimalizálást.
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: 'GroupDocs.Search Java: Dátumtartomány keresés és fejlett funkciók'
type: docs
url: /hu/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

# A GroupDocs.Search Java elsajátítása: Dátumtartomány keresés és haladó funkciók

A mai adat‑központú alkalmazásokban a **date range search** alapvető képesség, amely lehetővé teszi a dokumentumok időszakok szerinti szűrését, jelentősen javítva a relevanciát és a sebességet. Akár megfelelőségi portált, e‑commerce katalógust vagy tartalomkezelő rendszert építesz, a date range search és más erőteljes lekérdezéstípusok elsajátítása rugalmas és robusztus megoldást eredményez. Ez az útmutató végigvezet a hibakezelésen, a lekérdezéstípusok teljes skáláján és a teljesítmény tippeken, mind valós Java kóddal, amelyet egyszerűen másolhatsz‑beilleszthetsz.

## Quick Answers
- **Mi a date range search?** Olyan dokumentumok szűrése, amelyek dátumai egy megadott kezdő‑vég intervallumban vannak.  
- **Melyik könyvtár biztosítja?** GroupDocs.Search for Java.  
- **Szükségem van licencre?** A fejlesztéshez egy ingyenes próba elegendő; a kereskedelmi használathoz terméklicenc szükséges.  
- **Kombinálhatom más lekérdezésekkel?** Igen — keverheted a date range search‑t boolean, faceted vagy regex lekérdezésekkel.  
- **Gyors-e nagy adathalmazok esetén?** Ha megfelelően indexelt, a keresések almásodperces idő alatt futnak még millió rekord esetén is.

## What is date range search?
A date range search lehetővé teszi, hogy olyan dokumentumokat találj, amelyek dátumai két határ között vannak, például „2023‑01‑01 ~~ 2023‑12‑31”. Elengedhetetlen jelentésekhez, audit naplókhoz és minden olyan esetben, ahol az időalapú szűrés fontos.

## Why use GroupDocs.Search for Java?
A GroupDocs.Search egységes API‑t biztosít számos lekérdezéstípushoz — simple, wildcard, faceted, numeric, date range, regex, boolean és phrase — így több könyvtár egyidejű kezelése nélkül építhetsz kifinomult keresési élményt. Az esemény‑alapú hibakezelés pedig ellenállóvá teszi az indexelési folyamatot.

## Prerequisites
- **GroupDocs.Search Java library** (v25.4 vagy újabb).  
- **Java Development Kit (JDK)** kompatibilis a projekteddel.  
- Maven a függőségkezeléshez (vagy manuális letöltés).  

### Required Libraries and Environment Setup
Add hozzá a GroupDocs tárolót és függőséget a `pom.xml` fájlodhoz:

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

### Alternative Setup
Közvetlen letöltéshez látogasd meg a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalt.

### Licensing and Initial Setup
Kezdd egy ingyenes próba vagy egy ideiglenes licenc használatával:

- Látogasd meg a [GroupDocs License Options](https://purchase.groupdocs.com/temporary-license/) oldalt a részletekért.

Most hozzuk létre az index mappát, amely a kereshető adatokat tárolja.

## Setting Up GroupDocs.Search for Java

### Basic Initialization
Először hozd létre az `Index` objektumot, amely egy lemezen lévő mappára mutat:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

Most már van egy átjáród minden keresési művelethez.

## Implementation Guide

### Feature 1: Error Handling in Indexing
#### How to capture indexing errors (Java)

```java
import com.groupdocs.search.events.*;

index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
    @Override
    public void invoke(Object sender, IndexErrorEventArgs args) {
        System.out.println(args.getMessage()); // Output the error message
    }
});

// Add documents to the index
index.add("YOUR_DOCUMENT_DIRECTORY");
```

*Miért fontos*: Az `ErrorOccurred` esemény figyelésével naplózhatod a problémákat, újrapróbálhatod a hibás fájlokat, vagy felhívhatod a felhasználók figyelmét anélkül, hogy az egész folyamat összeomlana.

### Feature 2: Simple Search Query
#### What is a simple search?

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*Eredmény*: Visszaad minden dokumentumot, amely tartalmazza a **volutpat** kifejezést.

### Feature 3: Wildcard Search Query
#### How does wildcard search work?

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*Eredmény*: Mind a **affect**, mind a **effect** kifejezést megtalálja, bemutatva a `?` helyettesítő karakter erejét.

### Feature 4: Faceted Search Query
#### How to perform faceted search Java

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*Eredmény*: Korlátozza a keresést a **Content** mezőre, ami ideális a metaadatok, például kategória vagy szerző szerinti szűréshez.

### Feature 5: Numeric Range Search Query
#### How to search numeric ranges

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*Eredmény*: Olyan dokumentumokat ad vissza, ahol a numerikus értékek 2000 és 3000 között vannak.

### Feature 6: Date Range Search Query
#### How to execute date range search

```java
import com.groupdocs.search.options.*;
import java.util.*;

String query = "daterange(2000-01-01 ~~ 2001-06-15)";
SearchOptions options = new SearchOptions();

options.getDateFormats().clear();
DateFormatElement[] elements = {
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

SearchResult result = index.search(query, options);
```

*Magyarázat*: A `SearchOptions` testreszabásával megmondod a motornak, hogy ismerje fel a **MM/DD/YYYY** formátumú dátumokat, majd lekérdezi az összes rekordot 2000. január 1. és 2001. június 15. között.

### Feature 7: Regular Expression Search Query
#### How to run regex search Java

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*Eredmény*: Megtalálja három vagy több azonos karakterből álló sorozatokat (pl. „aaa”, „111”).

### Feature 8: Boolean Search Query
#### How to combine conditions with boolean search Java

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*Eredmény*: Visszaadja azokat a dokumentumokat, amelyek tartalmazzák a **justo** szót, de kizárja azokat, amelyekben **3456** is szerepel.

### Feature 9: Complex Boolean Search Query
#### How to craft advanced boolean queries

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*Eredmény*: Olyan fájlneveket keres, amelyek hasonlóak az „English” kifejezéshez (1‑3 karakteres eltérésekkel), **vagy** olyan tartalmat, amely mind a **3456**, mind a **consequat** szavakat tartalmazza.

### Feature 10: Phrase Search Query
#### How to search exact phrases

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*Eredmény*: Csak azokat a dokumentumokat adja vissza, amelyek pontosan a **ipsum dolor sit amet** kifejezést tartalmazzák.

## Practical Applications
1. **E‑commerce platformok** – Használd a faceted search Java‑t a termékek méret, szín és márka szerinti szűréséhez.  
2. **Tartalomkezelő rendszerek** – Kombináld a boolean search Java‑t a phrase search‑el, hogy fejlett szerkesztői eszközöket biztosíts.  
3. **Adat-elemző eszközök** – Használd a date range search‑t időalapú jelentések és műszerfalak készítéséhez.

## Common Issues & Solutions
- **Nincs eredmény a date range search‑hez** – Ellenőrizd, hogy a dokumentumaidban szereplő dátumformátum megegyezik a hozzáadott egyéni `DateFormat`‑tal.  
- **A regex lekérdezések túl sok találatot adnak** – Finomítsd a mintát vagy korlátozd a keresési tartományt további mezőfeltételekkel.  
- **Az indexelési hibák nem kerülnek rögzítésre** – Győződj meg róla, hogy az eseménykezelő **az `index.add(...)` hívás előtt** van csatolva.

## Frequently Asked Questions

**Q: Keverhetem a date range search‑t más lekérdezéstípusokkal?**  
A: Természetesen. Egy date range klauzulát kombinálhatsz boolean operátorokkal, faceted szűrőkkel vagy regex mintákkal egyetlen lekérdezésstringben.

**Q: Újra kell építeni az indexet a dátumformátumok módosítása után?**  
A: Igen. Az index tokenizált kifejezéseket tárol; csak a `SearchOptions` frissítése nem tokenizálja újra a meglévő adatokat. A formátumok módosítása után indexeld újra a dokumentumokat.

**Q: Hogyan kezeli a GroupDocs.Search a nagy indexeket?**  
A: Inkrementális indexelést és lemezen tárolást használ, ami lehetővé teszi, hogy milliók számú dokumentumot is kezelj, miközben alacsony a memóriahasználat.

**Q: Van korlát a helyettesítő karakterek (wildcard) számában?**  
A: A wildcard‑ok hatékonyan feldolgozhatók, de sok vezető wildcard (pl. `*term`) a teljesítményt rontja. Inkább használj előtag vagy utótag wildcard‑ot.

**Q: Melyik licencmodell ajánlott termeléshez?**  
A: A GroupDocs által kínált örökös vagy előfizetéses licenc biztosítja a frissítéseket, a támogatást és a korlátozás nélküli telepítést.

## Conclusion
A **date range search** és a GroupDocs.Search for Java által kínált fejlett lekérdezéstípusok teljes skálájának elsajátításával rendkívül gyors és funkciógazdag keresési élményeket építhetsz. Valósíts meg robusztus hibakezelést, finomhangold az indexet, és kombináld a lekérdezéseket, hogy szinte bármilyen visszakeresési helyzetet kielégíts. Kezdj el ma kísérletezni, és emeld alkalmazásod adat‑hozzáférési képességeit.

---

**Utolsó frissítés:** 2025-12-16  
**Tesztelve ezzel:** GroupDocs.Search 25.4 (Java)  
**Szerző:** GroupDocs