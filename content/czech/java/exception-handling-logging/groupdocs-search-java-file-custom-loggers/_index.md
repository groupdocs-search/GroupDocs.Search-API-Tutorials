---
date: '2026-09-21'
description: Naučte se, jak vytvořit logger, nastavit maximální velikost logu a použít
  konzolový logger v GroupDocs.Search pro Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Naučte se, jak vytvořit logger, nastavit maximální velikost logu a
  použít konzolový logger v GroupDocs.Search pro Java. Postupujte podle krok‑za‑krokem
  instrukcí a tipů na nejlepší postupy.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Jak vytvořit logger a omezit velikost logu v GroupDocs.Search
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
title: Jak vytvořit logger a omezit velikost logu v GroupDocs.Search pro Java
type: docs
url: /cs/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Jak vytvořit logger a omezit velikost souboru protokolu v GroupDocs.Search pro Java

V tomto tutoriálu se dozvíte, **jak vytvořit logger** implementace pro GroupDocs.Search, nakonfigurovat maximální velikost souboru protokolu a přepínat mezi souborovým a konzolovým logováním. Správná správa protokolů zabraňuje zaplnění disků během rozsáhlých indexovacích úloh, zlepšuje odstraňování problémů a poskytuje okamžitou zpětnou vazbu při vývoji. Začneme nastavením Maven, projdeme konfigurací loggeru a skončíme jednoduchým vyhledávacím dotazem, který ukazuje logger v akci.

## Rychlé odpovědi
- **Co znamená „limit log file size“?** Omezuje maximální velikost souboru protokolu, čímž zabraňuje nekontrolovanému růstu na disku.  
- **Který logger umožňuje omezit velikost souboru protokolu?** Vestavěný `FileLogger` přijímá parametr maximální velikosti.  
- **Jak použít console logger java?** Vytvořte instanci `ConsoleLogger` a nastavte ji na `IndexSettings`.  
- **Potřebuji licenci pro GroupDocs.Search?** Zkušební verze funguje pro hodnocení; pro produkci je vyžadována komerční licence.  
- **Jaký je první krok?** Přidejte závislost GroupDocs.Search do svého Maven projektu.  

## Co je limit log file size?
Nastavení **limit log file size** říká loggeru, aby přestal zapisovat nové položky, jakmile soubor dosáhne definovaného prahu (například 4 MB). Když je limit dosažen, logger buď zahodí další zprávy, nebo přepne na nový soubor, čímž udržuje předvídatelné využití disku.

## Proč používat souborové a vlastní loggery s GroupDocs.Search?
Souborové a vlastní loggery vám poskytují auditovatelnost, přehled o ladění a flexibilitu. V produkčních prostředích poskytují souborové protokoly trvalý záznam každé operace indexování a vyhledávání, zatímco konzolové protokoly dodávají okamžitou zpětnou vazbu během vývoje. Tyto protokoly pomáhají týmům sledovat výkon, sledovat chyby a splňovat požadavky na soulad tím, že zachovávají podrobnou stopu činnosti.

## Požadavky
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 nebo novější, s IDE jako IntelliJ IDEA nebo Eclipse.  
- Základní znalost Maven a programování v Javě.  

## Nastavení GroupDocs.Search pro Java

Přidejte knihovnu do svého projektu pomocí jedné z níže uvedených metod.

**Nastavení Maven:**  

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

**Přímé stažení:**  
Download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Obtain a trial or purchase a license via the [licensing page](https://purchase.groupdocs.com/temporary-license/).

## Jak vytvořit vlastní logger pro GroupDocs.Search
Creating a custom logger is straightforward because GroupDocs.Search relies on the `ILogger` interface. By implementing this interface—or by extending the provided `FileLogger` or `ConsoleLogger`—you can inject additional behavior such as remote forwarding or log rotation. You can also add initialization logic, such as opening network connections, and ensure resources are closed in the logger’s shutdown method. This approach lets you integrate with monitoring platforms like ELK or Splunk.

### Definiční kotva
`ILogger` je hlavní smlouva pro logování v GroupDocs.Search; jakákoli třída, která implementuje její metodu `log(Level, String)`, může být loggerem.

### Příklad přístupu (bez kódu)
1. Vytvořte třídu, která implementuje `ILogger`.  
2. Přepište metodu `log`, aby zapisovala zprávy do vámi zvoleného cíle (soubor, databáze, HTTP endpoint).  
3. V konfiguraci indexu zavolejte `settings.setLogger(new YourCustomLogger())`.  

## Jak omezit velikost souboru protokolu pomocí File Logger
The `FileLogger` class writes log entries to a file on disk and accepts a maximum size argument. By specifying the size limit, the logger automatically stops adding new entries or creates a new file when the threshold is reached, preventing uncontrolled disk growth. This behavior ensures that logging does not interfere with indexing performance while keeping a concise record of events.

### Definiční kotva
`FileLogger` je vestavěný logger, který ukládá zprávy do textového souboru a podporuje konfigurovatelnou maximální velikost souboru.

### Průvodce krok za krokem
1️⃣ **Importujte potřebné balíčky**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Nastavte nastavení indexu s File Logger**  
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

3️⃣ **Vytvořte nebo načtěte index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Přidejte dokumenty do indexu**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Proveďte vyhledávací dotaz**  
```text
```java
SearchResult result = index.search(query);
```
```

**Klíčový bod:** Konstruktor `FileLogger` s druhým argumentem (`4.0`) definuje **set max log size** v megabajtech, čímž přímo řeší požadavek **limit log file size**.

## Jak použít console logger java
When you need instant visibility of log events, the `ConsoleLogger` writes each message to `System.out`. This logger is lightweight and thread‑safe, making it suitable for development and debugging sessions. It provides immediate feedback on indexing progress, search queries, and error conditions without requiring file I/O, which can speed up iterative testing.

### Definiční kotva
`ConsoleLogger` je lightweight logger that outputs log entries to the standard console stream, making it ideal for debugging sessions.

### Kroky konfigurace
1️⃣ **Importujte console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Nastavte nastavení indexu s Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Vytvořte nebo načtěte index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Přidejte dokumenty a proveďte vyhledávání**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Tip:** Console logger je ideální během vývoje, protože okamžitě vypisuje každý záznam, což vám pomáhá ověřit, že indexování a vyhledávání fungují podle očekávání.

## Praktické aplikace
1. **Systémy pro správu dokumentů:** Uchovávejte auditní stopy každého indexovaného dokumentu, čímž splňujete požadavky na soulad.  
2. **Enterprise vyhledávače:** Monitorujte výkon dotazů a míru chyb v reálném čase, což umožňuje rychlé kontroly souladu se SLA.  
3. **Právní a compliance software:** Zaznamenávejte vyhledávací termíny a časová razítka pro regulatorní reportování, přičemž protokoly jsou uchovávány po požadovanou dobu.  

## Úvahy o výkonu
- **Velikost logu:** Pomocí **set max log size** se vyhnete nadměrnému využití disku, které by jinak mohlo zpomalit garbage collector JVM.  
- **Asynchronní logování:** Pro scénáře s vysokým průtokem obalte svůj logger do asynchronní fronty, aby se oddělilo I/O od vlákna indexování (implementace mimo rozsah tohoto průvodce).  
- **Správa paměti:** Uvolněte velké objekty `Index` pomocí `index.close()`, když již nejsou potřeba, aby byl paměťový otisk JVM nízký.  

## Časté problémy a řešení
- **Cesta k logu není přístupná:** Ověřte, že adresář existuje a že aplikace má oprávnění k zápisu pro uživatelský účet, pod kterým běží JVM.  
- **Logger se nespouští:** Ujistěte se, že voláte `settings.setLogger(...)` *před* vytvořením objektu `Index`; jinak se použije výchozí logger.  
- **Chybí výstup do konzole:** Ověřte, že aplikaci spouštíte v terminálu, který zobrazuje `System.out`, a že žádný logging framework (např. SLF4J) neodchytává výstup.  

## Často kladené otázky

**Q: Co řídí druhý parametr `FileLogger`?**  
A: Nastavuje maximální velikost souboru protokolu v megabajtech, což vám umožňuje **set max log size** a zabránit nekontrolovanému růstu.

**Q: Mohu kombinovat souborové a konzolové loggery?**  
A: Ano. Vytvořte vlastní logger, který přeposílá každé volání `log` jak do `FileLogger`, tak do `ConsoleLogger`, a poté zaregistrujte tento kompozitní logger pomocí `IndexSettings`.

**Q: Jak přidám dokumenty do indexu po jeho počátečním vytvoření?**  
A: Zavolejte `index.add(pathToNewDocs)` kdykoli; nakonfigurovaný logger automaticky zaznamená přidání.

**Q: Je `ConsoleLogger` thread‑safe?**  
A: Zapíše přímo do `System.out`, což JVM interně synchronizuje, takže je bezpečný pro typické vícevláknové scénáře.

**Q: Ovlivní omezení velikosti souboru protokolu množství uložených informací?**  
A: Jakmile je limit velikosti dosažen, nové záznamy jsou buď zahazovány, nebo logger přepne na nový soubor, v závislosti na zvolené implementaci.

## Zdroje
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Poslední aktualizace:** 2026-09-21  
**Testováno s:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs  

---

## Související tutoriály

- [Jak implementovat logování - Tutoriály o zpracování výjimek a logování pro GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implementace asynchronního logování v Javě s GroupDocs.Search – Průvodce vlastním loggerem](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Vytvoření vyhledávacího indexu Java – Tutoriály GroupDocs.Search](/search/java/indexing/)