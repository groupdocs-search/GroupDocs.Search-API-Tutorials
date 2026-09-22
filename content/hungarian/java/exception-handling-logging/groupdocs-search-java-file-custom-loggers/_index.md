---
date: '2026-09-21'
description: Ismerje meg, hogyan hozhat létre logger-t, állíthatja be a maximális
  napló méretét, és használhatja a konzol logger-t a GroupDocs.Search for Java-ban.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Ismerje meg, hogyan hozhat létre logger-t, állíthatja be a maximális
  napló méretét, és használhatja a konzol logger-t a GroupDocs.Search for Java-ban.
  Kövesse a lépésről‑lépésre útmutatót és a legjobb gyakorlatok tippeit.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Hogyan hozhatunk létre logger-t és korlátozhatjuk a napló méretét a GroupDocs.Search-ben
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Hogyan hozhatunk létre logger-t és korlátozhatjuk a napló méretét a GroupDocs.Search
  for Java-ban
type: docs
url: /hu/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Hogyan hozhatunk létre naplózót és korlátozhatjuk a naplófájl méretét a GroupDocs.Search Java-hoz

Ebben az útmutatóban megtanulja, hogyan hozhat létre naplózó implementációkat a GroupDocs.Search számára, hogyan konfigurálhatja a naplófájl maximális méretét, és hogyan válthat a fájl‑alapú és a konzol naplózás között. A megfelelő naplókezelés megakadályozza, hogy a lemezek nagy indexelési feladatok során megteljenek, javítja a hibaelhárítást, és azonnali visszajelzést ad a fejlesztés során. A Maven beállítással kezdünk, végigvezetjük a naplózási konfiguráción, és egy egyszerű keresési lekérdezéssel zárjuk, amely bemutatja a naplózó működését.

## Gyors válaszok
- **Mit jelent a „logfájl méretének korlátozása”?** A naplófájl maximális méretét korlátozza, megakadályozva a lemezen a szabálytalan növekedést.  
- **Melyik naplózó teszi lehetővé a logfájl méretének korlátozását?** A beépített `FileLogger` egy max‑méret paramétert fogad.  
- **Hogyan használhatom a konzol naplózót Java-ban?** Hozzon létre egy `ConsoleLogger` példányt, és állítsa be az `IndexSettings`‑ben.  
- **Szükségem van licencre a GroupDocs.Search-hez?** A próbaverzió elegendő értékeléshez; a termeléshez kereskedelmi licenc szükséges.  
- **Mi az első lépés?** Adja hozzá a GroupDocs.Search függőséget a Maven projektjéhez.  

## Mi a logfájl méretének korlátozása?
A **logfájl méretének korlátozása** beállítás azt mondja a naplózónak, hogy hagyja abba az új bejegyzések írását, amint a fájl eléri a meghatározott küszöböt (például 4 MB). Amikor a korlátot eléri, a naplózó vagy eldobja a további üzeneteket, vagy új fájlba vált, így a lemezhasználat előre látható marad.

## Miért használjunk fájl és egyedi naplózókat a GroupDocs.Search‑ben?
A fájl és egyedi naplózók auditálhatóságot, hibakeresési betekintést és rugalmasságot biztosítanak. Termelési környezetben a fájl naplók állandó feljegyzést nyújtanak minden indexelési és keresési műveletről, míg a konzol naplók azonnali visszajelzést adnak a fejlesztés során. Ezek a naplók segítik a csapatokat a teljesítmény monitorozásában, a hibák nyomon követésében és a megfelelőségi követelmények teljesítésében a részletes tevékenységi nyomvonal megőrzésével.

## Előfeltételek
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 vagy újabb, IDE‑val, például IntelliJ IDEA vagy Eclipse.  
- Alapvető ismeretek a Maven‑ról és a Java programozásról.  

## A GroupDocs.Search Java beállítása

Adja hozzá a könyvtárat a projekthez az alábbi módszerek egyikével.

**Maven beállítás:**  

```text
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
```

**Közvetlen letöltés:**  
Töltse le a legújabb JAR‑t a hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
Szerezzen próbaverziót vagy vásároljon licencet a [licencoldal](https://purchase.groupdocs.com/temporary-license/) segítségével.

## Egyedi naplózó létrehozása a GroupDocs.Search‑hez
A GroupDocs.Search a `ILogger` interfészre támaszkodik, ezért az egyedi naplózó létrehozása egyszerű. Az interfész implementálásával vagy a biztosított `FileLogger` vagy `ConsoleLogger` kiterjesztésével további viselkedést adhat hozzá, például távoli továbbítást vagy naplórotációt. Inicializációs logikát is beépíthet, például hálózati kapcsolatok nyitását, és biztosíthatja az erőforrások lezárását a naplózó leállítási metódusában. Ez a megközelítés lehetővé teszi integrációt felügyeleti platformokkal, mint az ELK vagy a Splunk.

### Definíció horgony
`ILogger` a GroupDocs.Search alapvető naplózási szerződése; bármely osztály, amely megvalósítja a `log(Level, String)` metódust, naplózóvá válhat.

### Példa megközelítés (kódblokk nélkül)
1. Hozzon létre egy osztályt, amely implementálja az `ILogger`‑t.  
2. Írja felül a `log` metódust, hogy az üzeneteket a választott célhelyre (fájl, adatbázis, HTTP végpont) írja.  
3. Az index konfigurációjában hívja meg a `settings.setLogger(new YourCustomLogger())`‑t.  

## A naplófájl méretének korlátozása a File Logger‑rel
A `FileLogger` osztály naplóbejegyzéseket ír lemezre, és elfogad egy maximális méret argumentumot. A méretkorlát megadásával a naplózó automatikusan leállítja az új bejegyzések hozzáadását vagy új fájlt hoz létre, amikor a küszöböt eléri, megakadályozva a szabálytalan lemeznövekedést. Ez a viselkedés biztosítja, hogy a naplózás ne befolyásolja az indexelés teljesítményét, miközben tömör eseménynaplót tart.

### Definíció horgony
`FileLogger` egy beépített naplózó, amely üzeneteket szöveges fájlba ment, és támogatja a konfigurálható maximális fájlméretet.

### Lépésről‑lépésre útmutató
1️⃣ **Szükséges csomagok importálása**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Index beállítások konfigurálása File Logger‑rel**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Az index létrehozása vagy betöltése**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Dokumentumok hozzáadása az indexhez**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Keresési lekérdezés végrehajtása**  
```text
```java
SearchResult result = index.search(query);
```
```

**Kulcsfontosságú pont:** A `FileLogger` konstruktorának második argumentuma (`4.0`) meghatározza a **maximális naplóméret beállítását** megabájtban, közvetlenül a **logfájl méretének korlátozása** követelménynek megfelelően.

## A console logger Java használata
Amikor azonnali láthatóságra van szükség a naplóeseményekhez, a `ConsoleLogger` minden üzenetet a `System.out`‑ba ír. Ez a naplózó könnyű és szálbiztos, így alkalmas fejlesztési és hibakeresési ülésekhez. Azonnali visszajelzést ad az indexelés előrehaladásáról, a keresési lekérdezésekről és a hibaállapotokról anélkül, hogy fájl‑I/O‑ra lenne szükség, ami felgyorsíthatja az iteratív tesztelést.

### Definíció horgony
`ConsoleLogger` egy könnyű naplózó, amely a standard konzolfolyamra írja a naplóbejegyzéseket, így ideális hibakeresési ülésekhez.

### Konfigurációs lépések
1️⃣ **A console logger importálása**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Index beállítások konfigurálása Console Logger‑rel**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Az index létrehozása vagy betöltése**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Dokumentumok hozzáadása és keresés végrehajtása**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Tipp:** A console logger fejlesztés közben ideális, mivel azonnal kiírja minden naplóbejegyzést, segítve annak ellenőrzését, hogy az indexelés és a keresés a várt módon működik.

## Gyakorlati alkalmazások
1. **Dokumentumkezelő rendszerek:** Minden indexelt dokumentum audit nyomvonalát nyújtja, megfelelve a megfelelőségi követelményeknek.  
2. **Vállalati keresőmotorok:** Valós időben figyeli a lekérdezések teljesítményét és hibaarányát, lehetővé téve a gyors SLA megfelelőség ellenőrzést.  
3. **Jogi és megfelelőségi szoftverek:** Rögzíti a keresési kifejezéseket és időbélyegeket a szabályozói jelentéshez, a naplókat a kötelező megőrzési időszakig megőrizve.  

## Teljesítménybeli megfontolások
- **Naplóméret:** A **maximális naplóméret beállításával** elkerülhető a túlzott lemezhasználat, amely egyébként lelassíthatná a JVM szemétgyűjtőjét.  
- **Aszinkron naplózás:** Nagy áteresztőképességű esetekben csomagolja a naplózót egy aszinkron sorba, hogy leválassza az I/O‑t az indexelési szálról (a megvalósítás kívül esik ebben az útmutatóban).  
- **Memóriakezelés:** Szabadítsa fel a nagy `Index` objektumokat a `index.close()` hívással, amikor már nincs rájuk szükség, hogy alacsony JVM lábnyomot tartson.  

## Gyakori problémák és megoldások
- **A napló útvonal nem érhető el:** Ellenőrizze, hogy a könyvtár létezik, és hogy az alkalmazásnak írási jogosultsága van a JVM‑et futtató felhasználói fiók számára.  
- **A naplózó nem aktiválódik:** Győződjön meg róla, hogy a `settings.setLogger(...)` hívást a `Index` objektum létrehozása *előtt* végzi; ellenkező esetben az alapértelmezett naplózó lesz használva.  
- **A konzol kimenet hiányzik:** Ellenőrizze, hogy a programot olyan terminálban futtatja, amely megjeleníti a `System.out`‑ot, és hogy semmilyen naplózási keretrendszer (pl. SLF4J) nem szakítja meg a kimenetet.  

## Gyakran ismételt kérdések

**K: Mit szabályoz a `FileLogger` második paramétere?**  
V: A naplófájl maximális méretét megabájtban állítja be, lehetővé téve a **maximális naplóméret beállítását** és a szabálytalan növekedés megakadályozását.

**K: Kombinálhatom a fájl és a konzol naplózókat?**  
V: Igen. Hozzon létre egy egyedi naplózót, amely minden `log` hívást továbbít mind a `FileLogger`, mind a `ConsoleLogger` felé, majd regisztrálja ezt a kompozit naplózót az `IndexSettings`‑ben.

**K: Hogyan adhatok dokumentumokat az indexhez a kezdeti létrehozás után?**  
V: Bármikor meghívhatja a `index.add(pathToNewDocs)`‑t; a konfigurált naplózó automatikusan rögzíti a hozzáadást.

**K: A `ConsoleLogger` szálbiztos?**  
V: Közvetlenül a `System.out`‑ba ír, amelyet a JVM belsőleg szinkronizál, így biztonságos a tipikus több szálas használati esetekben.

**K: A naplófájl méretének korlátozása befolyásolja a tárolt információ mennyiségét?**  
V: Amikor a méretkorlátot eléri, az új bejegyzéseket vagy eldobja, vagy a naplózó új fájlra vált, a választott megvalósítástól függően.

## Erőforrások
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Last Updated:** 2026-09-21  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

---

## Kapcsolódó útmutatók

- [How to Implement Logging - Exception Handling and Logging Tutorials for GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implement Asynchronous Logging in Java with GroupDocs.Search – Custom Logger Guide](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Create Search Index Java – GroupDocs.Search Tutorials](/search/java/indexing/)