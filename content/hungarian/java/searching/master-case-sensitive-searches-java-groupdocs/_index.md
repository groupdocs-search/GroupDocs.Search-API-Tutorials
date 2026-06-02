---
date: '2026-02-06'
description: Tanulja meg, hogyan adhat dokumentumokat az indexhez, és hogyan engedélyezhet
  esetérzékeny keresést Java-ban a GroupDocs.Search segítségével, ezáltal növelve
  alkalmazása pontosságát.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Dokumentumok hozzáadása az indexhez: kis‑ és nagybetűkre érzékeny Java‑keresés
  a GroupDocs‑szal'
type: docs
url: /hu/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Add documents to index: Mastering Case‑Sensitive Searches in Java with GroupDocs

A megfelelő információ megtalálása egy hatalmas dokumentumgyűjteményben alapvető követelmény a modern alkalmazások számára. Ebben az útmutatóban megtanulja, **hogyan adjon dokumentumokat az indexhez** és végezzen **kis‑ és nagybetűérzékeny kereséseket** a GroupDocs.Search for Java segítségével. Legyen szó jogi dokumentumtár, e‑kereskedelmi katalógus vagy tartalomkezelő rendszer építéséről, a pontos keresési eredmények boldoggá teszik a felhasználókat és megbízhatóvá teszik az adatokat.

## Quick Answers
- **Mi a legfontosabb lépés a keresés megkezdéséhez?** Dokumentumok hozzáadása egy indexhez a `index.add(...)` segítségével.
- **Hogyan engedélyezhető a kis‑ és nagybetűérzékeny keresés?** Állítsa be a `options.setUseCaseSensitiveSearch(true)` értéket.
- **Kereshetek több könyvtárban egyszerre?** Igen – hívja meg az `index.add()`‑t minden egyes mappához, amelyet fel szeretne venni.
- **Melyik metódus teszi lehetővé a keresést objektumokkal?** Használja a `SearchQuery.createWordQuery(...)`‑t.
- **Szükség van licencre a teszteléshez?** Ideiglenes licenc áll rendelkezésre próbaverzióhoz.

## What does “add documents to index” mean?
A dokumentumok indexhez adása azt jelenti, hogy a forrásfájlokat (PDF‑ek, Word‑dokumentumok, egyszerű szöveg stb.) betáplálja a GroupDocs.Search‑be, hogy az felépíthesse a kereshető adatstruktúrát. Az indexelés után a motor gyors lekérdezéseket tud végrehajtani, beleértve a kis‑ és nagybetűérzékeny kereséseket is.

## Why enable case‑sensitive search in Java?
- **Pontos kifejezésillesztés** – megkülönbözteti a „Apple” (a cég) és az „apple” (a gyümölcs) kifejezéseket.  
- **Szabályozási megfelelés** – egyes iparágak pontos kifejezésillesztést követelnek meg.  
- **Javított relevancia** – a felhasználók gyakran kis‑ és nagybetűspecifikus eredményeket várnak technikai vagy jogi környezetben.

## Prerequisites
- JDK (ajánlott a Java 17 vagy újabb)  
- Maven a függőségkezeléshez  
- IDE, például IntelliJ IDEA vagy Eclipse  
- Alapvető Java programozási ismeretek  

## Setting Up GroupDocs.Search for Java
Először adja hozzá a GroupDocs tárolót és a függőséget a `pom.xml`‑hez:

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

Alternatívaként letöltheti a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licensing
A próbaverzióhoz látogasson el a GroupDocs oldalára, és szerezzen be egy ideiglenes licencet. Ez lehetővé teszi, hogy minden funkciót korlátozás nélkül teszteljen.

## How to add documents to index – Text Query Search

### Step 1: Create an Index and add your documents
Hozzon létre egy mappát, ahol az indexfájlok tárolódnak, majd adja meg a forráskönyvtárat, amely a keresni kívánt dokumentumokat tartalmazza.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Pro tip:** Többször is meghívhatja az `index.add()`‑t, hogy **több könyvtárban is keresést végezzen** egyetlen indexben.

### Step 2: Enable case‑sensitive search
Állítsa be a keresési opciókat úgy, hogy figyelembe vegyék a betűk nagyságát.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Step 3: Execute a case‑sensitive text query
Futtasson egy lekérdezést, amely megkülönbözteti a „Advantages” és a „advantages” kifejezéseket.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

A ciklus kiírja minden olyan dokumentum teljes elérési útját, amely a pontos, betűérzékeny kifejezést tartalmazza.

## How to add documents to index – Object Query Search

Az objektumalapú lekérdezések nagyobb rugalmasságot biztosítanak, különösen, ha több kritériumot kell kombinálni.

### Step 1: Initialize a second index (optional)
Ha külön szeretné tartani az objektumalapú kereséseket, hozzon létre egy másik indexmappát.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Step 2: Re‑use the case‑sensitive option
Ugyanaz a `SearchOptions` példány használható objektumlekérdezésekhez is.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Step 3: Build and run an object query
Hozzon létre egy szólekérdezés‑objektumot, és adja át a keresőmotornak.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

A `createWordQuery` használatával később kombinálhatja azt kifejezés‑, helyettesítő‑ vagy logikai lekérdezésekkel összetettebb forgatókönyvekhez.

## Practical Applications
- **Jogi dokumentumkezelés:** Olyan eset‑specifikus törvények visszakeresése, ahol a nagybetűk számítanak.  
- **E‑commerce platformok:** Termékkódok megkülönböztetése, például „PRO‑X” vs. „pro‑x”.  
- **Tartalomkezelő rendszerek (CMS):** Biztosítja, hogy a szerzők pontos címeket vagy címkéket találjanak.

## Performance Considerations
- **Az index naprakészen tartása** – új fájlok hozzáadásakor vagy meglévők módosításakor újra kell indexelni.  
- **Memóriahasználat figyelése** – nagy korpuszok esetén előnyös az inkrementális indexelés és a megfelelő JVM heap méret beállítása.  
- **A Java szemétgyűjtőjének kihasználása** – szabadítsa fel az `Index` objektumokat, ha már nincs rájuk szükség.

## Common Issues and Solutions
| Issue | Solution |
|-------|----------|
| `useCaseSensitiveSearch` figyelmen kívül marad | Ellenőrizze, hogy a legújabb GroupDocs.Search verziót használja, és hogy az opció módosítása után újraépítette-e az indexet. |
| Nem érkezik eredmény egy ismert kifejezésre | Győződjön meg róla, hogy a kifejezés pontosan megegyezik a betűmérettel, és hogy a dokumentum sikeresen hozzá lett adva az indexhez. |
| Sok mappa keresése lelassul | Adja hozzá egyesével minden mappát az `index.add()`‑vel, és fontolja meg az index szétbontását shard‑okra nagyon nagy adathalmazok esetén. |

## Frequently Asked Questions

**Q:** Hogyan kezeljem a nagy adatállományokat a GroupDocs.Search‑szal?  
**A:** Használjon indexpartícionálást, finomhangolja a JVM memória beállításait, és időnként tömörítse az indexet a teljesítmény optimalizálása érdekében.

**Q:** Kereshetek egyszerre több könyvtárban?  
**A:** Igen – hívja meg az `index.add()`‑t minden egyes könyvtárhoz, majd egyetlen lekérdezést futtasson a kombinált indexen.

**Q:** Mik a gyakori buktatók a kis‑ és nagybetűérzékeny keresések beállításakor?  
**A:** Az `useCaseSensitiveSearch` engedélyezése után elfelejtik újraépíteni az indexet, vagy a lekérdezésben rossz betűméretet használnak.

**Q:** Hogyan tudom hibakeresni a keresési hibákat?  
**A:** Ellenőrizze a GroupDocs.Search által generált naplófájlokat a stack trace‑ekért, és győződjön meg róla, hogy minden Maven függőség helyesen fel van oldva.

**Q:** Alkalmas a GroupDocs.Search valós‑idő alkalmazásokhoz?  
**A:** Megfelelő indexelési stratégiákkal (inkrementális frissítések és memóriában tárolt gyorsítótár) közel valós‑idő keresési eredményeket tud biztosítani.

## Resources
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API Reference:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub Repository:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Support Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Temporary License:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-02-06  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs