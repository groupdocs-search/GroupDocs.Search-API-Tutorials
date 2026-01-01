---
date: '2025-12-29'
description: Naučte se, jak vyčistit adresář v Javě, automatizovat správu dokumentů
  a přejmenovávat soubory pomocí GroupDocs.Search pro Javu. Zvyšte efektivitu ve svých
  aplikacích.
keywords:
- Java document indexing
- GroupDocs.Search for Java
- automate document management
title: Čistý adresář Java – Automatizujte indexování a přejmenování
type: docs
url: /cs/java/indexing/automate-document-indexing-groupdocs-search-java/
weight: 1
---

# Clean Directory Java – Automatizujte indexování dokumentů a přejmenování pomocí GroupDocs.Search

## Quick Answers
- **Co znamená “clean directory java”?** Odstraňování všech souborů/složek uvnitř cílového adresáře pomocí Java kódu.  
- **Která knihovna vytváří prohledávatelný index?** GroupDocs.Search for Java.  
- **Jak přejmenuji dokument a udržuji index aktuální?** Použijte `File.renameTo()` a poté informujte index pomocí `Notification.createRenameNotification`.  
- **Mohu po vyčištění složky kopírovat soubory?** Ano – Java Streams mohou soubory kopírovat při zachování indexu.  
- **Je pro produkci vyžadována licence?** Pro komerční použití je potřeba platná licence GroupDocs.Search.

## What is “clean directory java”?
Vyčištění adresáře v Javě znamená programově odstranit každý soubor a podadresář uvnitř určené složky. Často to slouží jako předběžný krok před kopírováním nových souborů nebo přestavbou indexu, aby zastaralá data neovlivňovala výsledky vyhledávání.

## Why automate document indexing and renaming?
- **Automatizace správy dokumentů** snižuje ruční úsilí a eliminuje lidské chyby.  
- **Krok vytvoření prohledávatelného indexu** vám umožní okamžitě najít jakýkoli dokument podle obsahu.  
- **Přejmenování souborů bez aktualizace indexu** by narušilo přesnost vyhledávání; automatizace udržuje vše konzistentní.  

## Prerequisites

- **GroupDocs.Search for Java** (verze 25.4 nebo novější)  
- JDK 8 + a IDE jako IntelliJ IDEA nebo Eclipse  
- Základní znalost Javy, zejména práce se soubory (I/O)  

## Setting Up GroupDocs.Search for Java

### Maven Dependency
Přidejte repozitář a závislost do svého `pom.xml`:

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

### Direct Download
Alternativně stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License
Získejte bezplatnou zkušební verzi, dočasnou evaluační licenci nebo zakupte plnou licenci pro produkční použití.

### Basic Initialization
Vytvořte instanci `Index`, která bude obsahovat prohledávatelná data:

```java
import com.groupdocs.search.Index;

public class Main {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/DocumentIndexingAndRenaming/Index";
        Index index = new Index(indexFolder);
    }
}
```

## Implementation Guide

### 1. Add Documents to Index (create searchable index)

```java
import com.groupdocs.search.Index;

public class DocumentIndexingAndRenaming {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/DocumentIndexingAndRenaming/Index";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/";

        // Create an Index
        Index index = new Index(indexFolder);

        // Add documents to the index
        index.add(documentFolder);
    }
}
```

*Vysvětlení*:  
- `indexFolder` – kde jsou uloženy soubory indexu.  
- `documentFolder` – zdrojová složka, která obsahuje soubory, jež chcete učinit prohledávatelnými.  

### 2. Rename a Document and Notify the Index

```java
import com.groupdocs.search.Notification;

public class DocumentIndexingAndRenaming {
    public static void main(String[] args) {
        // Define paths for renaming
        String oldDocumentPath = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/Lorem ipsum.txt";
        String newDocumentPath = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/Lorem ipsum renamed.txt";

        java.io.File fileToRename = new java.io.File(oldDocumentPath);
        boolean renameSuccessful = fileToRename.renameTo(new java.io.File(newDocumentPath));

        if (renameSuccessful) {
            // Notify the index about the renaming
            Notification notification = Notification.createRenameNotification(oldDocumentPath, newDocumentPath);
            index.notifyIndex(notification);

            // Update the index to reflect changes
            index.update();
        }
    }
}
```

*Vysvětlení*:  
- `File.renameTo()` v Javě provádí fyzické přejmenování.  
- `Notification.createRenameNotification()` informuje GroupDocs.Search, že se název souboru změnil, čímž udržuje index přesný.  

## Clean Directory Java – Directory Cleaning and File Copying

Udržení složky v pořádku před hromadným kopírováním zabraňuje duplicitním nebo osiřelým souborům. Níže jsou dva znovupoužitelné úryvky.

### Step 1: Delete Folder Contents (delete folder contents)

```java
import java.io.File;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class DirectoryCleaningAndFileCopying {
    public static void main(String[] args) throws IOException {
        String targetDirectory = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/";

        Files.walk(Paths.get(targetDirectory))
             .map(Path::toFile)
             .sorted((o1, o2) -> -o1.compareTo(o2))
             .forEach(File::delete);
    }
}
```

*Vysvětlení*:  
- `Files.walk()` prochází každý soubor a podadresář.  
- Řazení v opačném pořadí zajišťuje, že soubory jsou odstraněny před jejich nadřazenými adresáři, čímž efektivně **odstraní obsah složky**.

### Step 2: Copy Files (copy files java)

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.Stream;

public class DirectoryCleaningAndFileCopying {
    public static void main(String[] args) throws IOException {
        String sourceDirectory = "YOUR_SOURCE_DIRECTORY/ExampleFiles/";
        String targetDirectory = "YOUR_DOCUMENT_DIRECTORY/DocumentIndexingAndRenaming/Documents/";

        try (Stream<Path> paths = Files.walk(Paths.get(sourceDirectory))) {
            paths.filter(Files::isRegularFile)
                 .forEach(sourcePath -> {
                     Path destPath = Paths.get(targetDirectory + sourcePath.getFileName().toString());
                     try {
                         Files.copy(sourcePath, destPath, java.nio.file.StandardCopyOption.REPLACE_EXISTING);
                     } catch (IOException e) {
                         e.printStackTrace();
                     }
                 });
        }
    }
}
```

*Vysvětlení*:  
- Proud filtruje pouze běžné soubory a poté je kopíruje do cílové složky, přepisuje existující soubory podle potřeby.  

## Practical Applications

- **Enterprise Document Management** – Automatizujte indexování tisíců smluv a udržujte názvy souborů synchronizované.  
- **Legal Firms** – Rychle přejmenujte spisové soubory při zachování prohledávatelného obsahu.  
- **Content Management Systems** – Použijte vzor clean‑directory k obnovení mediálních složek bez ručního úklidu.  

## Performance Considerations

- **Velikost indexu** – Pravidelně index kompaktně zmenšujte, pokud narůstá.  
- **Využití paměti** – Zpracovávejte soubory po dávkách, aby nedošlo k `OutOfMemoryError`.  
- **Současnost (Concurrency)** – Pro hromadné operace zvažte `ExecutorService` v Javě k paralelizaci čištění a kopírování.  

## Common Issues & Tips

| Problém | Příčina | Řešení |
|-------|-------|-----|
| Přejmenování selže | Soubor je uzamčen nebo cesta neplatná | Ujistěte se, že soubor není otevřen jinde; použijte `Files.move` pro spolehlivější přejmenování. |
| Index se neaktualizuje | Notifikace nebyla odeslána | Vždy zavolejte `index.notifyIndex(notification)` a poté `index.update()`. |
| Zastaralé výsledky vyhledávání po kopírování | Index stále odkazuje na staré soubory | Znovu přidejte cílovou složku do indexu nebo po kopírování zavolejte `index.update()`. |

## Frequently Asked Questions

**Q: Mohu vyčistit adresář, který obsahuje podadresáře?**  
A: Ano. Přístup pomocí `Files.walk()` rekurzivně odstraní všechny vnořené soubory a složky.

**Q: Musím po každém přejmenování přestavět celý index?**  
A: Ne. Stačí odeslat notifikaci o přejmenování a zavolat `index.update()`.

**Q: Jak velký adresář mohu vyčistit, než narazím na limity výkonu?**  
A: Záleží na paměti JVM; zpracování v menších dávkách nebo pomocí streamů pomáhá spravovat velké datové sady.

**Q: Je GroupDocs.Search zdarma pro vývoj?**  
A: K dispozici je bezplatná zkušební verze, ale pro produkční použití je vyžadována placená licence.

**Q: Mohu tento přístup použít i pro jiné typy souborů (např. PDF, DOCX)?**  
A: Rozhodně. GroupDocs.Search podporuje mnoho formátů; stačí přidat složku obsahující tyto soubory do indexu.

## Conclusion

Máte nyní kompletní, připravené řešení pro **clean directory java**, které přidává dokumenty do prohledávatelného indexu, přejmenovává soubory a udržuje vše synchronizované s GroupDocs.Search. Použijte tyto vzory k automatizaci pracovního postupu správy dokumentů a užívejte si rychlejší a spolehlivější vyhledávání.

---

**Poslední aktualizace:** 2025-12-29  
**Testováno s:** GroupDocs.Search 25.4  
**Autor:** GroupDocs