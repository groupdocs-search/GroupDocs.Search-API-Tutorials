---
date: '2026-09-02'
description: Ismerje meg, hogyan hozhat létre search index java-t és engedélyezheti
  a helyesírási javítást a GroupDocs.Search használatával. Kövesse a lépésről‑lépésre
  útmutatót a dokumentumok hozzáadásához, a max mistake count konfigurálásához, és
  a keresési pontosság javításához.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Ismerje meg, hogyan hozhat létre search index java-t és engedélyezheti
  a helyesírási javítást a GroupDocs.Search használatával. Kövesse a lépésről‑lépésre
  útmutatót a dokumentumok hozzáadásához, a max mistake count konfigurálásához, és
  a keresési pontosság javításához.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Hogyan hozhatunk létre search index java-t és engedélyezhetjük a helyesírási
  javítást
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Hogyan hozhatunk létre search index java-t és engedélyezhetjük a helyesírási
  javítást
type: docs
url: /hu/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Hogyan hozzunk létre keresési indexet Java-ban és engedélyezzük a helyesírást

A modern Java alkalmazásokban a pontos keresési eredmények biztosítása alapvető funkció. Ez a bemutató megmutatja, **hogyan hozzunk létre keresési indexet Java-ban** és hogyan kapcsoljuk be a helyesírási javítást a GroupDocs.Search segítségével, így a felhasználók releváns találatokat kapnak még akkor is, ha elgépelik a lekérdezéseket. Megmutatjuk, hogyan állítsuk be a könyvtárat, adjunk dokumentumokat, konfiguráljuk a maximális hibaszámot, és hajtsunk végre egy hibákat toleráló keresést – mindezt anélkül, hogy egyetlen extra konfigurációs kódsort is írnánk.

## Gyors válaszok
- **Mi a “enable spelling” funkció?** Aktiválja a beépített helyesírás-ellenőrzőt, amely a keresés során a helytelenül írt kifejezéseket a legközelebbi helyes formájukra cseréli.  
- **Melyik könyvtár biztosítja ezt a funkciót?** GroupDocs.Search for Java.  
- **Szükségem van licencre?** Egy ingyenes próba a kiértékeléshez megfelelő; a termelésben való használathoz teljes licenc szükséges.  
- **Mérhető-e a tolerancia?** Igen – használja a `setMaxMistakeCount` metódust, hogy meghatározza, hány elütés engedélyezett lekérdezésenként.  
- **Alkalmas nagy indexekre?** Teljesen – a motor millió rekordot tartalmazó indexeket is kezel, miközben a lekérdezési késleltetés tipikus szerverkörnyezetben 100 ms alatt marad.

## Mi a GroupDocs.Search?
A GroupDocs.Search egy Java könyvtár, amely gyors teljes szöveges indexelést és fejlett keresési funkciókat biztosít, beleértve a beépített helyesírási javítást is. Több mint 50 bemeneti formátumot támogat, és több száz oldalas dokumentumokat képes feldolgozni anélkül, hogy az egész fájlt a memóriába töltené.

## Miért engedélyezzük a helyesírási javítást Java alkalmazásokban?
- **Növeli a felhasználói elégedettséget** – a látogatók helyes eredményeket kapnak még hibás írás esetén is.  
- **Csökkenti a visszafordulási arányt** – a pontos találatok hosszabb ideig lekötik a felhasználókat.  
- **Minden területen működik** – a könyvtári katalógusoktól az e‑kereskedelmi termékkeresésekig, a helyesírási javítás mindenhol növeli a relevanciát.

## Előfeltételek
- Java Development Kit (JDK) telepítve.  
- Alapvető Java és Maven ismeretek.  
- Az indexelés koncepciójának megértése.  
- GroupDocs.Search próba vagy licenc kulcs.

### A GroupDocs.Search beállítása Java-hoz
Integrálja a könyvtárat Maven projektjébe.

**Maven beállítás**  
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

**Közvetlen letöltés**  
Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
Szerezzen be egy ingyenes próba licencet a kiértékeléshez. Termelési használathoz vásároljon teljes licencet, vagy kérjen ideiglenes kulcsot a hivatalos oldalról.

## Hogyan hozhatok létre keresési indexet Java-ban?
`SearchIndex` az elsődleges osztály, amely a lemezen tárolt kereshető indexet képviseli.  
Hozzon létre egy `SearchIndex` példányt, amely egy lemez mappára mutat, majd adjon hozzá dokumentumokat egy forráskönyvtárból. A motor egy fordított indexet épít, amely a gyors kereséseket teszi lehetővé. Hívhatja a `index.add()` metódust minden fájlhoz; a könyvtár automatikusan kinyeri a szöveget a fájltípus alapján.

## Hogyan engedélyezhetem a helyesírási javítást?
`getSpellingOptions()` visszaadja az index helyesírási konfigurációs objektumát, lehetővé téve a helyesírás-ellenőrzés funkcióinak engedélyezését vagy finomhangolását.  
A helyesírás engedélyezéséhez hívja a `index.getSpellingOptions().setEnabled(true)` metódust. Ez azt mondja a motornak, hogy elemezze a lekérdezési kifejezéseket, és javasoljon javított alternatívákat, ha eltéréseket észlel. A funkció azonnal működik minden olyan nyelvre, amelyet a könyvtár támogat.

## Mi a maximális hibaszám beállítás?
`setMaxMistakeCount` beállítja a karaktermódosítások maximális számát, amelyet a helyesírás-ellenőrző egy kifejezésre tolerál.  
`setMaxMistakeCount(int)` meghatározza a karaktermódosítások (beszúrások, törlések, helyettesítések) maximális számát, amelyet a helyesírás-ellenőrző egy kifejezésre tolerál. **2**‑re állítva a motor képes a gyakori két karakteres elütéseket javítani, miközben elkerüli a túl agresszív javításokat, amelyek irreleváns eredményeket hozhatnak.

## Hogyan hajtsunk végre helyesírási javítással ellátott keresést
`search()` végrehajt egy lekérdezést az indexen, és visszaad egy `SearchResult` objektumot, amely tartalmazza a találatokat és az esetleges javított kifejezéseket.  
Futtasson egy keresési lekérdezést a `search()` metódussal. Ha a lekérdezés hibásan írt szavakat tartalmaz, a motor egy `SearchResult` objektumot ad vissza, amely tartalmazza a javított kifejezéseket és a legrelevánsabb dokumentumok listáját. Megjelenítheti a felhasználónak mind az eredeti lekérdezést, mind a javított változatot az átláthatóság érdekében.  
A `SearchResult` tartalmazza a megfelelő dokumentumok listáját és információkat a lekérdezés javításairól.

## Gyakorlati alkalmazások
1. **Könyvtári rendszerek** – automatikusan javítja a helytelenül írt könyvcímeket vagy szerzőneveket.  
2. **E‑kereskedelmi platformok** – javítja a terméknevek elütéseit a konverziós arány növelése érdekében.  
3. **Tartalomkezelés** – segíti a szerkesztői csapatot a cikkek megtalálásában még hiányos kulcsszavak esetén is.

## Teljesítmény szempontok
- **Tartsa az indexet naprakészen** – rendszeresen újraindexelje az új vagy módosított fájlokat.  
- **Finomhangolja a JVM memória beállításait** – biztosítson elegendő heap memóriát nagy indexekhez (pl. `-Xmx4g`).  
- **Figyelje az erőforrás-használatot** – állítsa be a garbage collector zászlókat, ha nagy mennyiségű indexelés során szüneteket észlel.

## Gyakori problémák és hibaelhárítás
| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| Nincsenek eredmények a helyesírás engedélyezése után | Az index mappájának útvonala hibás vagy üres | Ellenőrizze, hogy az `indexFolder` egy érvényes indexre mutat, és hogy a `index.add()` sikeres volt |
| A helyesírás-ellenőrző nem javítja a nyilvánvaló elütéseket | `setMaxMistakeCount` túl alacsonyra van állítva | Növelje a számot 2‑re vagy 3‑ra a toleránsabb javítás érdekében |
| Az alkalmazás összeomlik nagy dokumentumkészletek esetén | Nem elegendő JVM heap | Növelje a `-Xmx` opciót (pl. `-Xmx4g`) |

## Gyakran feltett kérdések

**Q: Mi a GroupDocs.Search?**  
A: A GroupDocs.Search egy Java könyvtár, amely gyors indexelést, fejlett lekérdezési képességeket és beépített helyesírási javítást biztosít bármely Java alkalmazáshoz.

**Q: Hogyan szerezhetek licencet a GroupDocs.Search-hez?**  
A: Látogassa meg a hivatalos weboldalt, hogy letöltsön egy ingyenes próbát vagy megvásároljon egy teljes licencet; ideiglenes kulcs is elérhető rövid távú teszteléshez.

**Q: Integrálhatom a GroupDocs.Search-t más Java keretrendszerekkel?**  
A: Igen, zökkenőmentesen működik a Spring, a Jakarta EE és bármely standard Java alkalmazással.

**Q: Milyen gyakori problémák merülnek fel az index beállításakor?**  
A: Helytelen mappa útvonalak, hiányzó fájlengedélyek vagy hiányzó Maven függőségek a tipikus okok.

**Q: Hogyan javítja a helyesírási javítás a keresési eredményeket?**  
A: Automatikusan átírja a helytelenül írt lekérdezéseket a legközelebbi helyes kifejezésekre, így relevánsabb találatokat ad és csökkenti a felhasználói frusztrációt.

## További források
- [Dokumentáció](https://docs.groupdocs.com/search/java/)
- [API Referencia](https://reference.groupdocs.com/search/java)
- [Letöltés](https://releases.groupdocs.com/search/java/)
- [GitHub tároló](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Ingyenes támogatási fórum](https://forum.groupdocs.com/c/search/10)
- [Ideiglenes licenc](https://purchase.groupdocs.com/temporary-license/)

---

**Utoljára frissítve:** 2026-09-02  
**Tesztelve a következővel:** GroupDocs.Search 25.4  
**Szerző:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Kapcsolódó oktatóanyagok

- [Hogyan hozzunk létre dokumentum indexet és adjunk hozzá dokumentumokat a GroupDocs.Search API Java-hoz](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Nyelvfeldolgozás Java – Szinonima szótár létrehozása a GroupDocs.Search segítségével](/search/java/dictionaries-language-processing/)
- [Stop szavak a keresésben: Dokumentumok hozzáadása az indexhez a GroupDocs.Search Java-val](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)