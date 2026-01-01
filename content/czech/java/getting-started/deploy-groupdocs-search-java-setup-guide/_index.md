---
date: '2025-12-26'
description: Naučte se, jak vytvořit prohledávatelný index v Javě pomocí GroupDocs.Search
  pro Javu, přidávat soubory k vyhledávání a přidávat adresáře do uzlu.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Vytvořte prohledávatelný index v Javě – nasazení GroupDocs.Search pro Javu
type: docs
url: /cs/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Vytvoření prohledávatelného indexu Java – nasazení GroupDocs.Search pro Java

V dnešním daty řízeném světě aplikace **vytvářející prohledávatelný index java** potřebují efektivně zpracovávat obrovské kolekce dokumentů. Ať už budujete podnikové vyhledávací řešení nebo menší projekt, dobře nakonfigurovaná vyhledávací síť může výrazně zlepšit rychlost a relevanci vyhledávání. V tomto průvodci vás provedeme celým procesem nastavení **GroupDocs.Search pro Java**, od přidávání souborů do vyhledávání po přidávání adresářů do uzlu, abyste mohli okamžitě začít indexovat své dokumenty.

## Rychlé odpovědi
- **Jaký je hlavní účel GroupDocs.Search?** Poskytuje škálovatelný, na Javě postavený engine pro indexování a vyhledávání dokumentů napříč distribuovanou sítí.  
- **Kterou verzi mám použít?** Pro nové projekty se doporučuje nejnovější stabilní vydání (např. 25.4).  
- **Potřebuji licenci?** K dispozici je 30‑denní bezplatná zkušební verze; pro produkční použití je vyžadována trvalá licence.  
- **Mohu přidat jak soubory, tak celé adresáře?** Ano – použijte pomocníky `addFiles` a `addDirectories` k načtení obsahu.  
- **Jaká verze Javy je vyžadována?** Java 8 nebo vyšší, s Mavenem pro správu závislostí.

## Co je „vytvořit prohledávatelný index java“?
Vytvoření prohledávatelného indexu v Javě znamená vytvořit datovou strukturu, která mapuje termíny na dokumenty, které je obsahují, což umožňuje rychlé full‑textové dotazy. GroupDocs.Search abstrahuje těžkou práci, takže se můžete soustředit na načítání dokumentů a ladění chování vyhledávání.

## Proč použít GroupDocs.Search pro Java?
- **Škálovatelná síťová architektura** – nasazení více uzlů, které sdílejí zátěž indexování.  
- **Bohatá podpora formátů dokumentů** – PDF, Word, Excel, PowerPoint, obrázky a další.  
- **Událostmi řízené aktualizace** – přihlaste se k událostem uzlu, aby byl index v reálném čase aktuální.  
- **Jednoduchá integrace s Mavenem** – přidejte několik řádků do `pom.xml` a začněte indexovat.

## Požadavky
- **JDK 8+** nainstalováno na vašem vývojovém počítači.  
- IDE, jako je **IntelliJ IDEA** nebo **Eclipse**.  
- Základní znalost **Javy** a **Mavenu**.  
- Přístup ke knihovně **GroupDocs.Search pro Java** (stažení nebo Maven).

## Nastavení GroupDocs.Search pro Java

### Maven Dependency
Add the repository and dependency to your `pom.xml`:

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

> **Tip:** Udržujte číslo verze aktuální kontrolou oficiální stránky vydání.

Můžete také stáhnout JAR přímo z oficiálního webu: [vydání GroupDocs.Search pro Java](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Bezplatná zkušební verze:** 30‑denní hodnocení.  
- **Dočasná licence:** požádejte o prodloužené testování.  
- **Nákup:** vyžadováno pro produkční nasazení.

### Basic Initialization
Create a configuration object that points to a folder where index files will be stored and defines the base communication port:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## Jak vytvořit prohledávatelný index java s GroupDocs.Search?

Níže rozkládáme hlavní funkce, které budete potřebovat k **přidání souborů do vyhledávání** a **přidání adresářů do uzlu**, a zároveň nasadit škálovatelnou síť.

### Feature 1 – Configuration and Network Setup
Configuring the search network is the first step toward building a searchable index.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – adresář, kde budou data indexu uložena.  
- **`basePort`** – počáteční port; každý uzel bude inkrementovat od této hodnoty.

### Feature 2 – Deploying Search Network Nodes
Nasazení uzlů rozděluje zátěž indexování mezi více strojů nebo procesů.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Každý `SearchNetworkNode` běží se svým vlastním indexovacím servisem, což vám umožňuje **vytvořit prohledávatelný index java**, který se horizontálně škáluje.

### Feature 3 – Subscribing to Node Events
Událostmi řízené aktualizace
Aktualizace v reálném čase udržují index synchronizovaný se změnami souborového systému.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Poslechem událostí můžete automaticky spustit re‑indexaci, když přijdou nové soubory.

### Feature 4 – Adding Directories to Network Node
Funkce 4 – Přidání adresářů do uzlu sítě
Použijte tento pomocník k **přidání adresářů do uzlu**, rekurzivně sbírající všechny podporované dokumenty.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### Feature 5 – Adding Files to Network Node
Funkce 5 – Přidání souborů do uzlu sítě
Když potřebujete jemnozrnné řízení, **přidejte soubory do vyhledávání** jednotlivě:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Časté problémy a řešení
| Problém | Příčina | Řešení |
|-------|--------|-----|
| **Žádné dokumenty se neobjevují ve výsledcích vyhledávání** | Index nebyl potvrzen | Po přidání souborů zavolejte `node.getIndexer().commit()`. |
| **Chyba konfliktu portu** | Jiná služba používá `basePort` | Zvolte jiný `basePort` nebo ověřte volné porty. |
| **Nepodporovaný formát souboru** | Knihovna postrádá parser | Ujistěte se, že je přípona souboru podporována, nebo přidejte vlastní extraktor. |

## Často kladené otázky

**Q: Mohu použít GroupDocs.Search v cloudové Java aplikaci?**  
A: Ano. Knihovna funguje s libovolným Java runtime a můžete nastavit `basePath` na síťově připojený adresář nebo cloudové úložiště připojené lokálně.

**Q: Jak aktualizuji index, když se soubor změní?**  
A: Přihlaste se k událostem uzlu (viz Funkce 3) a znovu zavolejte `addFiles` nebo `addDirectories` pro upravené cesty.

**Q: Existuje limit na počet uzlů, které mohu nasadit?**  
A: Prakticky je limit dán vaším hardwarem a šířkou pásma sítě. API samo o sobě neklade žádný pevný limit.

**Q: Musím po přidání nových souborů restartovat uzly?**  
A: Ne. Přidání souborů automaticky spustí indexování; pouze pokud operaci odložíte, je potřeba provést commit.

**Q: Jaké formáty dokumentů jsou podporovány přímo z krabice?**  
A: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML a mnoho typů obrázků. Kompletní seznam najdete v oficiální dokumentaci.

**Poslední aktualizace:** 2025-12-26  
**Testováno s:** GroupDocs.Search pro Java 25.4  
**Autor:** GroupDocs