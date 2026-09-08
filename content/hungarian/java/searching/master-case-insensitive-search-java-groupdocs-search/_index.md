---
date: '2026-07-31'
description: Ismerje meg, hogyan valósítható meg a case insensitive search Java a
  dokumentumok indexhez adásával a GroupDocs.Search segítségével, karaktercserével
  a szöveg normalizálásához az indexelés során.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: A case insensitive search Java lehetővé teszi, hogy dokumentumokat
  adjunk hozzá egy indexhez, és lekérdezzük őket a betűkészlet mérete nélkül. Ez az
  útmutató bemutatja, hogyan normalizálja a szöveget a GroupDocs.Search az indexelés
  során a gyors és megbízható eredményekért.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Case Insensitive Search Java – Dokumentumok indexelése a GroupDocs segítségével
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Dokumentumok hozzáadása az indexhez a Case‑Insensitive Search-hez Java-ban
type: docs
url: /hu/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Dokumentumok hozzáadása az indexhez a kis- és nagybetűket figyelmen kívül hagyó kereséshez Java-ban

Amikor **case insensitive search java**-ra van szükség, amely megbízhatóan megtalálja az információkat, függetlenül attól, hogyan gépelik be a felhasználók, a kulcs az, hogy a dokumentumokat egy indexhez adjuk hozzá, miközben normalizáljuk a szöveget. Ebben az útmutatóban bemutatjuk a GroupDocs.Search for Java konfigurálását, hogy minden indexelt dokumentum automatikusan kisbetűssé (vagy egyéb módon átalakítottá) legyen az indexelés során, ezáltal biztosítva a kis- és nagybetűket figyelmen kívül hagyó eredményeket extra lekérdezési logika nélkül.

## Gyors válaszok
- **Mi jelent a „add documents to index”?** Ez azt jelenti, hogy a forrásfájlokat betöltjük egy kereshető adatstruktúrába, hogy később lekérdezhetők legyenek.  
- **Miért használunk karaktercserét?** Ez normalizálja minden karaktert — általában kisbetűre — így a keresések automatikusan figyelmen kívül hagyják a kis- és nagybetű különbségeket.  
- **Szükségem van licencre?** Egy ingyenes próba működik fejlesztéshez; egy teljes licenc szükséges a termelési környezethez.  
- **Melyik Java verzió szükséges?** Java 8 vagy újabb; a könyvtár a Java 11+ célja a legjobb teljesítmény érdekében.  
- **Átkapcsolhatok-e szükség esetén kis‑ és nagybetű érzékeny keresésre?** Igen — a keresési beállítások lehetővé teszik a case‑sensitivity kapcsolását lekérdezésenként.

## Mi az a „add documents to index” a GroupDocs.Search-ben?
Töltsd fel a forrásfájljaidat (PDF, DOCX, TXT, stb.) egy kereshető indexbe, hogy a motor gyorsan vissza tudja őket találni. A dokumentumok indexhez adása minden fájlt feldolgoz, kinyeri a egyszerű szöveget, és egy optimalizált adatstruktúrában tárolja, amely gyors keresést tesz lehetővé.

## Miért engedélyezzük a karaktercserét az indexelés során?
A karaktercsere minden karaktert egy előre meghatározott ekvivalensre alakít — leggyakrabban kisbetűre — az index felépítése közben. Ez biztosítja, hogy a nagybetűk, diakritikus jelek vagy a helyi specifikus szimbólumok változásai ne befolyásolják a keresési eredményeket. A szöveg indexelés közbeni normalizálásával a motor egységes tokenkészlethez tudja illeszteni a lekérdezéseket, gyors, megbízható kis- és nagybetűket figyelmen kívül hagyó viselkedést biztosítva anélkül, hogy minden keresésnél további feldolgozásra lenne szükség.

## Előfeltételek
- **GroupDocs.Search for Java** verzió 25.4 vagy újabb (a könyvtár több mint 30 fájlformátumot támogat, és több száz oldalas dokumentumokat indexelhet anélkül, hogy az egész fájlt memóriába töltené).
- **Java Development Kit (JDK)** 8 vagy újabb telepítve.
- Alapvető ismeretek a **Maven**-ról (vagy a JAR-ok kézi hozzáadásának képessége).

## A GroupDocs.Search for Java beállítása

### Maven beállítás
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

### Közvetlen letöltés
Ha nem szeretnél Maven-t használni, töltsd le a legújabb JAR-t a hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc megszerzése
- **Free Trial** – tölts le egy próba licencet a kísérletezéshez.  
- **Temporary License** – kérj egy kibővített teszt licencet a GroupDocs portálról.  
- **Full License** – vásárolj termelési licencet, amikor készen állsz az éles üzemre.

### Alap inicializálás (Az index létrehozása)
Az alábbi kódrészlet létrehoz egy index mappát és engedélyezi a karaktercseréket:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Implementációs útmutató

### Karaktercsere engedélyezése az index beállításaiban
Ennek a funkciónak az aktiválása azt mondja a motornak, hogy cserélje a karaktereket az indexelés során, ami a kis- és nagybetűket figyelmen kívül hagyó viselkedés alaplépése.

#### 1. lépés: `IndexSettings` konfigurálása
`IndexSettings` a konfigurációs objektum, amely szabályozza, hogyan tárolja és dolgozza fel a szöveget az index. A `useCharacterReplacements` **true** értékre állításával bekapcsolod az automatikus kisbetűssé alakítást (vagy bármilyen egyéni leképezést, amit megadsz).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Karaktercserék konfigurálása
Térképezd le minden karaktert a megfelelő kisbetűs megfelelőjére (vagy bármilyen egyéni leképezésre, amire szükséged van).

#### 2. lépés: Helyettesítő párok definiálása és hozzáadása
A helyettesítő szótár párokat tartalmaz, mint például `'A' → 'a'`, `'É' → 'e'` stb. Ezeknek a pároknak az indexelés előtt történő hozzáadása biztosítja, hogy minden token normalizálva legyen.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Dokumentumok indexelése
Most, hogy az index készen áll, **add documents to index**-et használhatsz bármely mappából.

#### 3. lépés: Dokumentumok hozzáadása az indexeléshez
A GroupDocs.Search beolvassa a célkönyvtárat, kinyeri a szöveget minden támogatott fájltípusból, alkalmazza a helyettesítő térképet, és a tokeneket az index tárolóba írja.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Kis‑ és nagybetű érzékeny keresés végrehajtása (opcionális)

#### 4. lépés: Kis‑ és nagybetű érzékeny keresések végrehajtása
`SearchOptions` konfigurálja a lekérdezés viselkedését, például a case sensitivity kapcsolását, lehetővé téve a keresések finomhangolását.  
`SearchOptions.setUseCaseSensitiveSearch(true)` arra kényszeríti a motort, hogy egy adott lekérdezés során a nagy- és kisbetű karaktereket különbözőnek tekintse, felülbírálva az alapértelmezett kis‑ és nagybetűket figyelmen kívül hagyó viselkedést.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Gyakorlati alkalmazások
1. **Marketing kampányok** – Normalizáld a termékneveket, hogy az értékesítési csapatok az eszközöket a betűkészlet figyelembevétele nélkül találhassák meg.  
2. **Ügyfélszolgálat** – Segítsd a help‑desk keresőmezőket, hogy a megfelelő cikket adja vissza, függetlenül attól, hogy a felhasználó “login” vagy “Login”‑t ír be.  
3. **E‑commerce katalógusok** – Biztosítsd, hogy a vásárlók megtalálják a termékeket, függetlenül attól, hogyan írják be a termékcímeket, ezáltal növelve a konverziós arányt.

## Teljesítmény szempontok
- **Forrásfájlok szervezése** – Egy rendezett mappaszerkezet csökkenti a **add documents to index** lépés során a beolvasásra fordított időt.  
- **Memória figyelése** – Nagy korpuszok indexelése jelentős RAM-ot fogyaszthat; a fájlok 500 – 1 000 elemes kötegekben történő feldolgozása a heap használatot kontroll alatt tartja.  
- **Aszinkron indexelés** – Ha támogatott, futtasd az indexelést háttérszálon, hogy a felhasználói felület reagáló maradjon, és elkerüld a felhasználói műveletek blokkolását.

## Gyakori problémák és hibaelhárítás
| Tünet | Valószínű ok | Javítás |
|---------|--------------|-----|
| Nincs eredmény egy ismert kifejezésre | A karaktercserék nincsenek engedélyezve | Ellenőrizd, hogy `settings.setUseCharacterReplacements(true)` be van-e állítva, és hogy a helyettesítő térkép tartalmazza-e a szükséges karaktereket. |
| Memóriahiány hiba az indexelés során | Túl sok nagy fájl egyidejű indexelése | Indexelj kisebb kötegekben, vagy növeld a JVM heap méretét (`-Xmx4g`). |
| A keresés váratlanul kis‑ és nagybetű érzékeny eredményeket ad | `SearchOptions.setUseCaseSensitiveSearch(true)` be lett állítva | Távolítsd el vagy állítsd `false`‑ra az alapértelmezett kis‑ és nagybetűket figyelmen kívül hagyó viselkedéshez. |
| Az index betöltési ideje meghaladja a várakozást | Hatékonytalan mappaszerkezet vagy SSD hiánya | Rendezd át a fájlokat, távolítsd el a nem használt dokumentumokat, és tárold az indexet egy gyors SSD-n. |
| A speciális karakterek figyelmen kívül maradnak | A helyettesítő térkép hiányzik Unicode bejegyzésekkel | Adj hozzá leképezéseket olyan karakterekhez, mint “é”, “ß”, “ø”, a kívánt ekvivalensekhez. |

## Gyakran ismételt kérdések

**Q: Hogyan kezeljem a speciális karaktereket (pl. “é”, “ß”) az indexelés során?**  
A: Vedd fel ezeket a karaktereket a helyettesítő térképbe, és térképezd őket ASCII ekvivalenseikre, vagy tartsd őket változatlanul a keresési követelmények alapján.

**Q: Korlátozhatom a karaktercserét egy adott nyelvre?**  
A: Igen. Készíts egy egyedi helyettesítő tömböt, amely csak a célnyelv karaktereit tartalmazza, mielőtt hozzáadnád a szótárhoz.

**Q: Mit tegyek, ha az index betöltése sokáig tart?**  
A: Optimalizáld a mappaszerkezetet, távolítsd el a felesleges fájlokat, és tárold az indexet egy nagy sebességű SSD-n. Az inkrementális indexelés is csökkenti a betöltési terhet.

**Q: Lehet visszavonni a karaktercseréket az indexelés után?**  
A: Nem. A cserék az indexelt adatokba vannak beágyazva; az új beállításokkal újra kell építeni az indexet a módosításhoz.

**Q: Hol találok részletesebb API dokumentációt?**  
A: A hivatalos dokumentáció és API referencia kimerítő részleteket nyújt (lásd az alábbi forrásokat).

## Források
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/) 

---

**Utolsó frissítés:** 2026-07-31  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs  

---

## Kapcsolódó oktatóanyagok

- [Karaktercsere a GroupDocs.Search Java-ban: Átfogó útmutató a szöveges keresés és indexelés fejlesztéséhez](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Dokumentumok hozzáadása az indexhez: kis‑ és nagybetű érzékeny Java keresés a GroupDocs-szal](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Hogyan adjunk dokumentumokat az indexhez a GroupDocs.Search for Java használatával](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)