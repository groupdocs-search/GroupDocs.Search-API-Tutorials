---
date: '2026-02-24'
description: Naučte se, jak vytvořit vlastní logger, nastavit maximální velikost logu
  a nakonfigurovat konzolový nebo souborový logger v GroupDocs.Search pro Javu.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Jak vytvořit vlastní logger a omezit velikost souboru s logy pomocí GroupDocs.Search
  Java
type: docs
url: /cs/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Omezte velikost souboru protokolu pomocí loggerů GroupDocs.Search pro Java

V tomto průvodci **vytvoříte vlastní implementace loggeru** a naučíte se, jak **omezit velikost souboru protokolu** při používání GroupDocs.Search pro Java. Řízení růstu logu je klíčové pro rozsáhlé indexování dokumentů a vestavěné loggery vám umožňují **nastavit maximální velikost logu**, **převrátit soubor protokolu** nebo přepnout na **use console logger** pro okamžitou zpětnou vazbu. Projdeme kompletní nastavení, od konfigurace Maven až po spuštění dotazu vyhledávání, a ukážeme si, jak **přidat dokumenty do indexu** s nastaveným loggerem.

## Rychlé odpovědi
- **Co znamená „omezit velikost souboru protokolu“?** Nastaví maximální velikost souboru protokolu, čímž zabrání nekontrolovanému růstu na disku.  
- **Který logger umožňuje omezit velikost souboru protokolu?** Vestavěný `FileLogger` přijímá parametr max‑size.  
- **Jak použít console logger java?** Vytvořte instanci `ConsoleLogger` a nastavte ji v `IndexSettings`.  
- **Potřebuji licenci pro GroupDocs.Search?** Zkušební verze stačí pro hodnocení; pro produkční nasazení je vyžadována komerční licence.  
- **Jaký je první krok?** Přidejte závislost GroupDocs.Search do svého Maven projektu.  

## Co je omezení velikosti souboru protokolu?
Omezení velikosti souboru protokolu znamená nakonfigurovat logger tak, aby po dosažení předdefinovaného prahu (např. 4 MB) přestal růst nebo se převrátil. Tím zajistíte předvídatelnou velikost úložiště aplikace a vyhnete se degradaci výkonu.

## Proč používat souborové a vlastní loggery s GroupDocs.Search?
- **Auditovatelnost:** Uchovávejte trvalý záznam o událostech indexování a vyhledávání.  
- **Ladění:** Rychle identifikujte problémy pomocí stručných logů.  
- **Flexibilita:** Vyberte si mezi trvalými souborovými logy a okamžitým výstupem do konzole (`use console logger`).  

## Předpoklady
- **GroupDocs.Search pro Java** ≥ 25.4.  
- JDK 8 nebo novější, IDE (IntelliJ IDEA, Eclipse apod.).  
- Základní znalosti Javy a Maven.  

## Nastavení GroupDocs.Search pro Java

Přidejte knihovnu do svého projektu pomocí jedné z metod níže.

**Maven Setup:**

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

**Přímé stažení:**  
Stáhněte nejnovější JAR z oficiálního webu: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Získejte zkušební verzi nebo zakupte licenci na [licensing page](https://purchase.groupdocs.com/temporary-license/).

## Jak vytvořit vlastní logger pro GroupDocs.Search
GroupDocs.Search umožňuje připojit libovolnou implementaci rozhraní `ILogger`. Rozšířením `FileLogger` nebo `ConsoleLogger` můžete přidat další chování — například převrácení souboru protokolu nebo přeposílání zpráv do vzdálené monitorovací služby. Tato flexibilita je důvodem, proč mnoho týmů **vytváří vlastní logger** řešení, která odpovídají jejich provozním potřebám.

## Jak omezit velikost souboru protokolu pomocí File Logger
Níže je krok‑za‑krokem návod, který ukazuje, jak **nakonfigurovat file logger**, aby soubor protokolu nikdy nepřekročil zadanou velikost.

### 1️⃣ Import potřebných balíčků
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Nastavení Index Settings s File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Vytvoření nebo načtení indexu
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Přidání dokumentů do indexu
```java
index.add(documentsFolder);
```

### 5️⃣ Provedení dotazu vyhledávání
```java
SearchResult result = index.search(query);
```

**Klíčový bod:** Druhý argument konstruktoru `FileLogger` (`4.0`) definuje **set max log size** v megabajtech, čímž přímo řeší požadavek **limit log file size**.

## Jak použít console logger java
Pokud dáváte přednost okamžité zpětné vazbě v terminálu, vyměňte file logger za console logger.

### 1️⃣ Import Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Nastavení Index Settings s Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Vytvoření nebo načtení indexu
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Přidání dokumentů a provedení vyhledávání
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** Console logger je ideální během vývoje, protože okamžitě vypisuje každý záznam protokolu, což vám pomůže ověřit, že indexování a vyhledávání fungují podle očekávání.

## Praktické aplikace
1. **Systémy správy dokumentů:** Uchovávejte auditní stopy každého indexovaného dokumentu.  
2. **Podnikové vyhledávače:** Monitorujte výkon dotazů a míru chyb v reálném čase.  
3. **Právní a compliance software:** Zaznamenávejte vyhledávací termíny pro regulatorní reportování.

## Úvahy o výkonu
- **Velikost logu:** Pomocí **set max log size** zabráníte nadměrnému využití disku, které by mohlo zpomalit vaši aplikaci.  
- **Asynchronní logování:** Pokud potřebujete vyšší propustnost, zvažte obalení loggeru do asynchronní fronty (mimo rozsah tohoto průvodce).  
- **Správa paměti:** Uvolňujte velké objekty `Index`, když již nejsou potřeba, aby byl JVM úsporný.

## Časté problémy a řešení
- **Cesta k logu není přístupná:** Ověřte, že adresář existuje a aplikace má oprávnění k zápisu.  
- **Logger se nespouští:** Ujistěte se, že voláte `settings.setLogger(...)` *před* vytvořením objektu `Index`.  
- **Chybí výstup do konzole:** Zkontrolujte, že aplikaci spouštíte v terminálu, který zobrazuje `System.out`.

## Často kladené otázky

**Q: Co řídí druhý parametr `FileLogger`?**  
A: Nastavuje maximální velikost souboru protokolu v megabajtech, což vám umožní **set max log size**.

**Q: Mohu kombinovat file a console loggery?**  
A: Ano, vytvořením vlastního loggeru, který přeposílá zprávy do obou destinací.

**Q: Jak přidám dokumenty do indexu po jeho počáteční tvorbě?**  
A: Zavolejte `index.add(pathToNewDocs)` kdykoli; logger zaznamená operaci.

**Q: Je `ConsoleLogger` thread‑safe?**  
A: Píše přímo do `System.out`, který je JVM‑em synchronizován, takže je bezpečný pro většinu případů použití.

**Q: Ovlivní omezení velikosti souboru protokolu množství uložených informací?**  
A: Po dosažení limitu mohou být nové záznamy zahazovány nebo může dojít k **roll over log file**, podle implementace loggeru.

## Zdroje
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Poslední aktualizace:** 2026-02-24  
**Testováno s:** GroupDocs.Search pro Java 25.4  
**Autor:** GroupDocs  

---