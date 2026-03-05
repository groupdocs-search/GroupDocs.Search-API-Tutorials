---
date: '2026-02-21'
description: Naučte se, jak implementovat filtr přípon souborů v Javě pomocí GroupDocs.Search
  pro Javu, zahrnující logické operátory, data vytvoření/úpravy a filtry cest.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: Filtr přípon souborů v Javě s GroupDocs.Search – Průvodce
type: docs
url: /cs/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Mistrovství filtru rozšíření souboru java s GroupDocs.Search

Správa rostoucího úložiště dokumentů může rychle přerůst v přetížení, zejména když potřebujete indexovat jen určité typy souborů. **The java file extension filter** vám umožní říci GroupDocs.Search přesně, které rozšíření zahrnout nebo vyloučit, a poskytuje vám přesnou kontrolu nad vaším indexovacím procesem. V tomto průvodci vás provedeme nastavením GroupDocs.Search pro Java a ukážeme, jak kombinovat filtrování rozšíření souborů s logickými operátory AND, OR a NOT, stejně jako s filtry pro časové rozmezí a cesty.

## Rychlé odpovědi
- **What is the java file extension filter?** Konfigurace, která říká GroupDocs.Search, které rozšíření souborů zahrnout nebo vyloučit během indexování.  
- **Which library provides this feature?** GroupDocs.Search for Java.  
- **Do I need a license?** Bezplatná zkušební verze funguje pro hodnocení; plná licence je vyžadována pro produkci.  
- **Can I combine filters?** Ano – můžete řetězit filtry rozšíření, data, velikosti a cesty s logikou AND, OR, NOT.  
- **Is it Maven‑compatible?** Naprosto – přidejte závislost GroupDocs.Search do vašeho `pom.xml`.

## Co je java file extension filter?
A **java file extension filter** je sada pravidel, která vyhodnocuje rozšíření každého souboru před jeho odesláním do indexovacího enginu. Zadáním rozšíření jako `.txt`, `.pdf` nebo `.epub` můžete **include files by extension** nebo **exclude files by extension**, aby byl váš index zaměřený a výsledky vyhledávání relevantní.

## Proč používat filtrování rozšíření souborů s GroupDocs.Search?
- **Performance:** Přeskakování nechtěných souborů snižuje I/O a zrychluje indexování.  
- **Storage savings:** Do indexu jsou uloženy jen relevantní dokumenty, což snižuje využití disku.  
- **Compliance:** Zabraňuje neúmyslnému indexování důvěrných nebo nepodporovaných typů souborů.  
- **Flexibility:** Kombinujte s funkcemi **date range filter java** pro cílení souborů vytvořených nebo upravených v konkrétních obdobích.

## Předpoklady

Než začneme, ujistěte se, že máte následující:

### Požadované knihovny a závislosti
- **GroupDocs.Search for Java**: Verze 25.4 nebo novější  
- **Java Development Kit (JDK)**: Nainstalovaná kompatibilní verze  

### Nastavení prostředí
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse nebo jakékoli Maven‑compatible IDE.

### Předpoklady znalostí
- Základní programování v Javě  
- Znalost souborového I/O v Javě  
- Porozumění regulárním výrazům a zpracování data‑času  

## Nastavení GroupDocs.Search pro Java
Pro zahájení používání GroupDocs.Search musíte zahrnout tuto knihovnu jako závislost ve vašem projektu.

### Maven konfigurace
Přidejte následující konfiguraci repozitáře a závislosti do souboru `pom.xml`:

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

### Přímé stažení
Alternativně stáhněte nejnovější verzi přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Získání licence
1. **Free Trial** – prozkoumejte funkce bez nákladů.  
2. **Temporary License** – získáte plnou funkčnost na omezené období.  
3. **Purchase** – získáte trvalou licenci pro produkční použití.  

### Základní inicializace a nastavení
Jakmile je knihovna přidána, inicializujte své indexovací prostředí:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Průvodce implementací
Níže se ponoříme do každého typu filtru, vysvětlíme **proč je důležitý** a poskytneme krok‑za‑krokem kód, který můžete zkopírovat do svého projektu.

### Filtrování rozšíření souborů
Filtrujte soubory podle jejich rozšíření během indexování. To je ideální, když chcete zpracovávat jen e‑knihy (`.fb2`, `.epub`) a prosté textové soubory (`.txt`).

#### Přehled
Použijte `DocumentFilter.createFileExtension` k vytvoření whitelistu rozšíření.

#### Kroky implementace
1. **Create Filter**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logický NOT filtr
Vyloučte konkrétní rozšíření, jako jsou webové stránky a PDF, pokud nejsou ve vašem vyhledávacím scénáři potřeba.

#### Kroky implementace
1. **Create Exclusion Filter**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to Index Settings**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add Documents**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logický AND filtr
Kombinujte několik podmínek—datum vytvoření, rozšíření a velikost souboru—tak, aby **only files that meet all criteria** byly indexovány.

#### Přehled
`DocumentFilter.createAnd` spojuje více filtrů do jedné pravidla.

#### Kroky implementace
1. **Define Filters**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine Filters**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index Documents**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logický OR filtr
Zahrňte soubory, které splňují **any** z uvedených podmínek—užitečné, když chcete zachytit jak malé textové soubory, tak větší netextové soubory.

#### Kroky implementace
1. **Define Filters**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine Filters with Logical Conditions**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR Filter**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry času vytvoření
Cílové soubory vytvořené v konkrétním období—klasický scénář **date range filter java**.

#### Kroky implementace
1. **Define Date Range Filter**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index Documents**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry času úpravy
Vyloučte soubory, které byly upraveny po určitém datu ořezu.

#### Kroky implementace
1. **Define Filter**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index Documents**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtrování cesty souboru
Omezte indexování na soubory umístěné ve specifických složkách nebo odpovídající vzoru—ideální pro **include files by extension** v rámci konkrétní hierarchie adresářů.

#### Kroky implementace
1. **Define File Path Filter**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Běžné úskalí a tipy

- **Never mix absolute and relative paths** ve stejné konfiguraci filtru – může to vést k neočekávaným vyloučením.  
- **Reset the `IndexSettings`** při přepínání sad filtrů; jinak mohou přetrvávat předchozí filtry.  
- **Combine a length upper bound with an extension filter** pro velké kolekce, aby se udržovala nízká spotřeba paměti.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) pro zjištění, proč byl soubor odmítnut.  

## Často kladené otázky

**Q: Can I change the filter criteria after the index is created?**  
A: Ano. Přestavte index s novým `DocumentFilter` nebo použijte inkrementální indexování s aktualizovanými nastaveními.

**Q: Does the java file extension filter work on compressed archives (e.g., ZIP)?**  
A: GroupDocs.Search může indexovat podporované formáty archivů, ale filtr rozšíření se vztahuje na samotný archiv, ne na vnitřní soubory. Použijte vnořené filtry pro podrobnější kontrolu.

**Q: How do I debug why a particular file was excluded?**  
A: Aktivujte logování knihovny (`LoggingOptions.setEnabled(true)`) a prohlédněte si log – uvádí, který filtr odmítl každý soubor.

**Q: Is it possible to combine the java file extension filter with custom regex filters?**  
A: Naprosto. Zabalte regex filtr do `DocumentFilter.createAnd()` spolu s filtrem rozšíření.

**Q: What performance impact does adding many filters have?**  
A: Každý filtr přidává během indexování mírnou zátěž, ale snížení množství indexovaných dat obvykle převáží náklady. Otestujte na reprezentativním vzorku, abyste našli optimální rovnováhu.

---

**Poslední aktualizace:** 2026-02-21  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs