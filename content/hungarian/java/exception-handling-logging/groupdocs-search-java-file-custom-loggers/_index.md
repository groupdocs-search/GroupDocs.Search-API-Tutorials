---
date: '2026-02-24'
description: Tanulja meg, hogyan hozhat létre egyedi naplózót, állíthatja be a maximális
  naplóméretet, és konfigurálhatja a konzol‑ vagy fájlnaplózót a GroupDocs.Search
  for Java‑ban.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Hogyan hozhatunk létre egyedi naplózót és korlátozhatjuk a naplófájl méretét
  a GroupDocs.Search Java-val
type: docs
url: /hu/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Logfájl méretének korlátozása a GroupDocs.Search Java naplózók segítségével

Ebben az útmutatóban **egyedi naplózó** megvalósításokat hozol létre, és megtanulod, hogyan **korlátozd a logfájl méretét** a GroupDocs.Search for Java használata közben. A napló növekedésének szabályozása kulcsfontosságú a nagyméretű dokumentumindexelésnél, és a beépített naplózók lehetővé teszik a **maximális naplóméret beállítását**, a **logfájl forgatását**, vagy egy **console logger használatát** az azonnali visszajelzéshez. Végigvezetünk a teljes beállításon, a Maven konfigurációtól a keresési lekérdezés futtatásáig, és megmutatjuk, hogyan **adjunk dokumentumokat az indexhez** a naplózó használatával.

## Gyors válaszok
- **Mit jelent a „logfájl méretének korlátozása”?** A logfájl maximális méretét korlátozza, megakadályozva a lemezterület kontrollálatlan növekedését.  
- **Melyik naplózó teszi lehetővé a logfájl méretének korlátozását?** A beépített `FileLogger` egy max‑méret paramétert fogad el.  
- **Hogyan használjam a console logger‑t Java‑ban?** Hozd létre a `ConsoleLogger` példányt, és állítsd be az `IndexSettings`‑ben.  
- **Szükség van licencre a GroupDocs.Search‑hez?** A próbaverzió elegendő értékeléshez; a kereskedelmi licenc a termeléshez kötelező.  
- **Mi az első lépés?** Add hozzá a GroupDocs.Search függőséget a Maven projektedhez.  

## Mi az a logfájl méretének korlátozása?
A logfájl méretének korlátozása azt jelenti, hogy a naplózót úgy konfigurálod, hogy a fájl elérve egy előre meghatározott küszöböt (pl. 4 MB), már ne növekedjen, vagy forgassa át. Ez előre láthatóvá teszi az alkalmazás tárolási lábnyomát, és elkerüli a teljesítményromlást.

## Miért használjunk fájl‑ és egyedi naplózókat a GroupDocs.Search‑el?
- **Auditálhatóság:** Állandó nyilvántartás a indexelési és keresési eseményekről.  
- **Hibakeresés:** Gyorsan azonosíthatók a problémák a tömör naplók áttekintésével.  
- **Rugalmasság:** Választhatsz a tartós fájlnaplók és az azonnali konzolkimenet (`use console logger`) között.  

## Előfeltételek
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 vagy újabb, IDE (IntelliJ IDEA, Eclipse, stb.).  
- Alapvető Java és Maven ismeretek.  

## A GroupDocs.Search for Java beállítása

Add hozzá a könyvtárat a projektedhez az alábbi módszerek egyikével.

**Maven beállítás:**

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

**Közvetlen letöltés:**  
Töltsd le a legújabb JAR‑t a hivatalos oldalról: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
Szerezz próbaverziót vagy vásárolj licencet a [licencoldal](https://purchase.groupdocs.com/temporary-license/) segítségével.

## Hogyan hozzunk létre egyedi naplózót a GroupDocs.Search‑hez
A GroupDocs.Search lehetővé teszi bármely `ILogger` interfész megvalósításának csatlakoztatását. A `FileLogger` vagy `ConsoleLogger` kiterjesztésével extra viselkedést adhatunk hozzá – például a logfájl forgatását vagy az üzenetek továbbítását egy távoli megfigyelőszolgáltatásnak. Ez a rugalmasság teszi lehetővé, hogy sok csapat **egyedi naplózót** hozzon létre, amely megfelel a működési igényeiknek.

## Hogyan korlátozzuk a logfájl méretét a File Logger‑rel
Az alábbi lépésről‑lépésre útmutató bemutatja, hogyan **konfiguráljuk a fájlnaplót**, hogy a logfájl soha ne lépje túl a megadott méretet.

### 1️⃣ Szükséges csomagok importálása
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Index beállítások konfigurálása File Logger‑rel
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Index létrehozása vagy betöltése
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Dokumentumok hozzáadása az indexhez
```java
index.add(documentsFolder);
```

### 5️⃣ Keresési lekérdezés végrehajtása
```java
SearchResult result = index.search(query);
```

**Kulcspont:** A `FileLogger` konstruktorának második argumentuma (`4.0`) határozza meg a **maximális naplóméret beállítását** megabájtban, közvetlenül a **logfájl méretének korlátozása** követelménynek megfelelően.

## Hogyan használjuk a console logger‑t Java‑ban
Ha azonnali visszajelzést szeretnél a terminálban, cseréld le a fájlnaplót console logger‑re.

### 1️⃣ A Console Logger importálása
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Index beállítások konfigurálása Console Logger‑rel
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Index létrehozása vagy betöltése
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Dokumentumok hozzáadása és keresés végrehajtása
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tipp:** A console logger fejlesztés közben ideális, mivel minden naplóbejegyzést azonnal kiír, segítve a indexelés és keresés helyes működésének ellenőrzését.

## Gyakorlati alkalmazások
1. **Dokumentumkezelő rendszerek:** Audit nyomvonalak vezetése minden **indexelt dokumentum** esetén.  
2. **Vállalati keresőmotorok:** Keresési teljesítmény és **hibaarány** valós idejű monitorozása.  
3. **Jogszabályi és megfelelőségi szoftverek:** **Keresési kifejezések** rögzítése **szabályozási** jelentésekhez.

## Teljesítménybeli megfontolások
- **Log méret:** A **maximális naplóméret beállításával** elkerülhető a túlzott **lemez**használat, ami lelassíthatná az alkalmazást.  
- **Aszinkron naplózás:** Ha nagyobb áteresztőképességre van szükség, fontold meg a naplózó egy aszinkron sorba csomagolását (az útmutató keretein kívül).  
- **Memóriakezelés:** Szabadítsd fel a nagy `Index` objektumokat, amikor már nincs rájuk szükség, hogy alacsonyan tartsd a JVM lábnyomát.

## Gyakori problémák és megoldások
- **A log útvonal nem érhető el:** Ellenőrizd, hogy a könyvtár létezik, és az alkalmazásnak van írási joga.  
- **A naplózó nem aktiválódik:** Győződj meg róla, hogy a `settings.setLogger(...)` hívást *az* `Index` objektum létrehozása **előtt** hajtod végre.  
- **A konzol kimenet hiányzik:** Ellenőrizd, hogy a programot olyan terminálban futtatod, amely megjeleníti a `System.out`‑t.

## Gyakran ismételt kérdések

**Q: Mit szabályoz a `FileLogger` második paramétere?**  
A: A logfájl maximális méretét megabájtban állítja be, lehetővé téve a **maximális naplóméret beállítását**.

**Q: Kombinálhatom a fájl‑ és console naplózókat?**  
A: Igen, egyedi naplózó létrehozásával, amely az üzeneteket mindkét célpontra továbbítja.

**Q: Hogyan adhatok dokumentumokat az indexhez az **elsődleges létrehozás** után?**  
A: Hívd meg a `index.add(pathToNewDocs)`‑t bármikor; a naplózó rögzíti a műveletet.

**Q: A `ConsoleLogger` szálbiztos?**  
A: Közvetlenül a `System.out`‑ra ír, amelyet a JVM szinkronizál, így a legtöbb esetben **biztonságos**.

**Q: Befolyásolja-e a logfájl méretének korlátozása a tárolt információ mennyiségét?**  
A: Amikor a méretkorlátot eléri, az új bejegyzések elvetésre kerülhetnek, vagy a fájl **logfájl forgatása** történik, a naplózó implementációjától függően.

## Források
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Utoljára frissítve:** 2026-02-24  
**Tesztelve a következővel:** GroupDocs.Search for Java 25.4  
**Szerző:** GroupDocs  

---