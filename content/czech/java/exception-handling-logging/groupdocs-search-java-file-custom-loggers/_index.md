---
date: '2025-12-24'
description: Naučte se omezit velikost souboru protokolu a používat konzolový logger
  v Javě s GroupDocs.Search pro Javu. Tento průvodce zahrnuje konfigurace protokolování,
  tipy pro řešení problémů a optimalizaci výkonu.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Omezte velikost log souboru pomocí loggerů GroupDocs.Search Java
type: docs
url: /cs/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Omezení velikosti souboru protokolu pomocí GroupDocs.Search Java Loggers

Efektivní protokolování je nezbytné při správě velkých kolekcí dokumentů, zejména když potřebujete **omezit velikost souboru protokolu**, aby byl úložný prostor pod kontrolou. **GroupDocs.Search for Java** nabízí robustní řešení pro práci s protokoly díky svým výkonným vyhledávacím schopnostem. Tento tutoriál vás provede implementací souborových a vlastních loggerů pomocí GroupDocs.Search, čímž zlepší schopnost vaší aplikace sledovat události a ladit problémy.

## Rychlé odpovědi
- **Co znamená “limit log file size”?** Omezuje maximální velikost souboru protokolu, čímž zabraňuje nekontrolovanému růstu na disku.  
- **Který logger vám umožňuje omezit velikost souboru protokolu?** Vestavěný `FileLogger` přijímá parametr max‑size.  
- **Jak použít console logger java?** Vytvořte instanci `ConsoleLogger` a nastavte ji na `IndexSettings`.  
- **Potřebuji licenci pro GroupDocs.Search?** Zkušební verze funguje pro hodnocení; pro produkci je vyžadována komerční licence.  
- **Jaký je první krok?** Přidejte závislost GroupDocs.Search do svého Maven projektu.

## Co je limit velikosti souboru protokolu?
Omezení velikosti souboru protokolu znamená nastavení loggeru tak, aby po dosažení předdefinovaného prahu (např. 4 MB) soubor přestal růst nebo se přepnul. To udržuje předvídatelnou velikost úložiště vaší aplikace a zabraňuje degradaci výkonu.

## Proč používat souborové a vlastní loggery s GroupDocs.Search?
- **Auditovatelnost:** Uchovávejte trvalý záznam o událostech indexování a vyhledávání.  
- **Ladění:** Rychle identifikujte problémy prohlížením stručných protokolů.  
- **Flexibilita:** Vyberte mezi trvalými souborovými protokoly a okamžitým výstupem do konzole (`use console logger java`).  

## Předpoklady
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 nebo novější, IDE (IntelliJ IDEA, Eclipse, atd.).  
- Základní znalosti Javy a Maven.  

## Nastavení GroupDocs.Search pro Java

Přidejte knihovnu do svého projektu pomocí jedné z níže uvedených metod.

**Nastavení Maven  

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
Získejte zkušební verzi nebo zakupte licenci prostřednictvím [licenční stránky](https://purchase.groupdocs.com/temporary-license/).

## Jak omezit velikost souboru protokolu pomocí File Logger
Níže je krok‑za‑krokem průvodce, který ukazuje, jak nakonfigurovat `FileLogger`, aby soubor protokolu nikdy nepřekročil zadanou velikost.

### 1️⃣ Import potřebných balíčků
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Nastavte Index Settings s File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Vytvořte nebo načtěte Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Přidejte dokumenty do Indexu
```java
index.add(documentsFolder);
```

### 5️⃣ Proveďte vyhledávací dotaz
```java
SearchResult result = index.search(query);
```

**Klíčový bod:** Druhý argument konstruktoru `FileLogger` (`4.0`) určuje maximální velikost souboru protokolu v megabajtech, čímž přímo řeší požadavek na **limit log file size**.

## Jak použít console logger java
Pokud dáváte přednost okamžitému zpětnému vazbě v terminálu, vyměňte souborový logger za logger konzole.

### 1️⃣ Importujte Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Nastavte Index Settings s Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Vytvořte nebo načtěte Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Přidejte dokumenty a proveďte vyhledávání
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** Console logger je ideální během vývoje, protože okamžitě vypisuje každý záznam protokolu, což vám pomáhá ověřit, že indexování a vyhledávání fungují podle očekávání.

## Praktické aplikace
1. **Systémy pro správu dokumentů:** Uchovávejte auditní stopy každého indexovaného dokumentu.  
2. **Podnikové vyhledávače:** Monitorujte výkon dotazů a míru chyb v reálném čase.  
3. **Právní a compliance software:** Zaznamenávejte vyhledávané termíny pro regulatorické reportování.

## Úvahy o výkonu
- **Velikost protokolu:** Omezením velikosti souboru protokolu se vyhnete nadměrnému využití disku, které by mohlo zpomalit vaši aplikaci.  
- **Asynchronní protokolování:** Pokud potřebujete vyšší propustnost, zvažte zabalení loggeru do asynchronní fronty (mimo rozsah tohoto návodu).  
- **Správa paměti:** Uvolněte velké objekty `Index`, když již nejsou potřeba, aby byl paměťový otisk JVM nízký.

## Časté problémy a řešení
- **Cesta k protokolu není přístupná:** Ověřte, že adresář existuje a aplikace má oprávnění k zápisu.  
- **Logger neaktivuje:** Ujistěte se, že voláte `settings.setLogger(...)` *před* vytvořením objektu `Index`.  
- **Chybí výstup do konzole:** Ověřte, že aplikaci spouštíte v terminálu, který zobrazuje `System.out`.

## Často kladené otázky

**Q: Co řídí druhý parametr `FileLogger`?**  
A: Nastavuje maximální velikost souboru protokolu v megabajtech, což vám umožňuje omezit velikost souboru protokolu.

**Q: Mohu kombinovat souborové a konzolové loggery?**  
A: Ano, vytvořením vlastního loggeru, který přeposílá zprávy na oba cíle.

**Q: Jak přidám dokumenty do indexu po jeho počátečním vytvoření?**  
A: V libovolném okamžiku zavolejte `index.add(pathToNewDocs)`; logger zaznamená operaci.

**Q: Je `ConsoleLogger` thread‑safe?**  
A: Zapíše přímo do `System.out`, který je synchronizován JVM, takže je bezpečný pro většinu případů použití.

**Q: Ovlivní omezení velikosti souboru protokolu množství uložených informací?**  
A: Jakmile je dosaženo limitu velikosti, nové záznamy mohou být zahazovány nebo se soubor může přepnout, v závislosti na implementaci loggeru.

## Zdroje
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Poslední aktualizace:** 2025-12-24  
**Testováno s:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs