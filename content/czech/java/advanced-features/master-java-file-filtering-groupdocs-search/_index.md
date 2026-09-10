---
date: '2026-09-06'
description: Naučte se, jak filtrovat přípony souborů java pomocí GroupDocs.Search
  pro Java, zahrnující logické operátory AND, OR, NOT, filtry časového rozmezí a filtry
  cesty.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Filtrovat přípony souborů java pomocí GroupDocs.Search. Naučte se
  kombinovat filtr přípony, filtr časového rozmezí a filtr cesty s logickými operátory
  v Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Filtrovat přípony souborů java pomocí GroupDocs.Search – Kompletní průvodce
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Jak filtrovat přípony souborů java pomocí GroupDocs.Search
type: docs
url: /cs/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filtrace přípon souborů java pomocí GroupDocs.Search

V tomto komplexním tutoriálu se naučíte, jak **filtraci přípon souborů java** provádět při indexaci dokumentů pomocí GroupDocs.Search. Na konci průvodce budete schopni zahrnout pouze potřebné typy souborů, vyloučit nežádoucí formáty a kombinovat tato pravidla s filtry časového rozmezí a cesty pomocí logických operátorů AND, OR a NOT. Tento přístup udržuje index úsporný, zrychluje vyhledávání a pomáhá dodržovat zásady zacházení s daty.

## Rychlé odpovědi
- **Co je filtr přípon souborů java?** Jedná se o pravidlo, které říká GroupDocs.Search, které přípony souborů zahrnout nebo vyloučit během indexace.  
- **Která knihovna poskytuje tuto funkci?** GroupDocs.Search for Java.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; plná licence je vyžadována pro produkci.  
- **Mohu kombinovat filtry?** Ano – můžete řetězit filtry přípon, data, velikosti a cesty pomocí logiky AND, OR, NOT.  
- **Je kompatibilní s Maven?** Naprosto – přidejte závislost GroupDocs.Search do svého `pom.xml`.

## Co je filtr přípon souborů java?
**Filtr přípon souborů java** je sada pravidel, která vyhodnocuje příponu každého souboru před jeho odesláním do indexovacího enginu. Zadáním přípon jako `.txt`, `.pdf` nebo `.epub` můžete **zahrnout soubory podle přípony** nebo **vyloučit soubory podle přípony**, aby byl váš index zaměřený a výsledky vyhledávání relevantní.

## Proč používat filtraci přípon souborů s GroupDocs.Search?
Filtrace přípon souborů zvyšuje efektivitu indexace tím, že vylučuje irelevantní formáty, snižuje požadavky na úložiště a pomáhá splňovat pravidla souladu tím, že zabraňuje vstupu nežádoucího obsahu do indexu. Také umožňuje rychlejší odezvy na dotazy, protože vyhledávač zpracovává menší, relevantnější datovou sadu.

- **Výkon:** Přeskakování nežádoucích souborů snižuje I/O a zrychluje indexaci až o 40 % u velkých úložišť.  
- **Úspora úložiště:** Do indexu jsou uloženy jen relevantní dokumenty, což snižuje využití disku v průměru o 30 %.  
- **Soulad:** Zabraňuje neúmyslné indexaci důvěrných nebo nepodporovaných typů souborů.  
- **Flexibilita:** Kombinujte s **filtry časového rozmezí java** pro cílení souborů vytvořených nebo upravených v konkrétních obdobích.

## Předpoklady

Než začneme, ujistěte se, že máte následující:

### Požadované knihovny a závislosti
- **GroupDocs.Search for Java** – verze 25.4 nebo novější (podporuje více než 60 vstupních formátů).  
- **Java Development Kit (JDK)** – libovolná kompatibilní verze (8 nebo novější).

### Nastavení prostředí
- Integrované vývojové prostředí (IDE): IntelliJ IDEA, Eclipse nebo jakékoli Maven‑kompatibilní IDE.

### Předpoklady znalostí
- Základní programování v Javě.  
- Znalost souborového I/O v Javě.  
- Porozumění regulárním výrazům a práci s datum‑časem.

## Nastavení GroupDocs.Search pro Java
Abyste mohli začít používat GroupDocs.Search, musíte jej zahrnout jako závislost do svého projektu.

### Maven konfigurace
Přidejte následující repozitář a konfiguraci závislosti do souboru `pom.xml`:

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
Alternativně si stáhněte nejnovější verzi přímo z [vydání GroupDocs.Search pro Java](https://releases.groupdocs.com/search/java/).

#### Získání licence
1. **Bezplatná zkušební verze** – prozkoumejte funkce zdarma.  
2. **Dočasná licence** – získáte plnou funkčnost na omezenou dobu.  
3. **Nákup** – získáte trvalou licenci pro produkční použití.

### Základní inicializace a nastavení
Jakmile je knihovna přidána, inicializujte své indexovací prostředí. Třída `IndexSettings` obsahuje všechna konfigurační nastavení, včetně filtrů.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Průvodce implementací
Níže se ponoříme do jednotlivých typů filtrů, vysvětlíme **proč jsou důležité** a poskytneme krok‑za‑krokem instrukce, které můžete zkopírovat do svého projektu.

### Filtrace přípon souborů
Filtrujte soubory podle jejich přípon během indexace. To je ideální, když chcete zpracovávat jen e‑knihy (`.fb2`, `.epub`) a čisté textové soubory (`.txt`).

#### Přehled
`DocumentFilter.createFileExtension` vytváří whitelist přípon.

#### Kroky implementace
1. **Vytvořit filtr** – definujte přípony, které chcete ponechat.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Inicializovat index a přidat dokumenty** – aplikujte filtr při vytváření `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logický NOT filtr
Vylučte konkrétní přípony, například webové stránky a PDF, pokud nejsou potřeba pro váš vyhledávací scénář.

#### Kroky implementace
1. **Vytvořit vylučovací filtr** – uveďte přípony, které chcete odmítnout.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Aplikovat na nastavení indexu** – kombinujte NOT filtr s dalšími pravidly.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Přidat dokumenty** – indexovány budou jen soubory, které projdou kombinovaným filtrem.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logický AND filtr
Kombinujte několik podmínek — datum vytvoření, příponu a velikost souboru — tak, aby **pouze soubory splňující všechna kritéria** byly indexovány.

#### Přehled
`DocumentFilter.createAnd` spojuje více filtrů do jedné pravidla.

#### Kroky implementace
1. **Definovat filtry** – vytvořte samostatné filtry pro každou podmínku.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Kombinovat filtry** – použijte operátor AND, aby byly vyžadovány všechny podmínky.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Indexovat dokumenty** – předávejte kombinovaný filtr do indexovacího pipeline.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logický OR filtr
Zahrňte soubory, které splňují **kterékoli** z uvedených podmínek — užitečné, když chcete zachytit jak malé textové soubory, tak větší netextové soubory.

#### Kroky implementace
1. **Definovat filtry** – vytvořte samostatné filtry pro každou alternativní podmínku.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Kombinovat filtry s logickými podmínkami** – použijte operátor OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Dokončit OR filtr** – připojte kombinovaný filtr k nastavení indexu.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry času vytvoření
Cíleně indexujte soubory vytvořené v konkrétním období — klasický **filtr časového rozmezí java** scénář.

#### Kroky implementace
1. **Definovat filtr časového rozmezí** – uveďte počáteční a koncové datum.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Indexovat dokumenty** – budou indexovány jen soubory, jejichž časové razítko vytvoření spadá do zadaného rozmezí.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtry času úpravy
Vylučte soubory, které byly upraveny po určitém datu ohraničení.

#### Kroky implementace
1. **Definovat filtr** – nastavte maximální časové razítko úpravy.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Indexovat dokumenty** – soubory novější než ohraničení jsou ignorovány.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filtrování cesty souboru
Omezte indexaci na soubory umístěné ve specifických složkách nebo odpovídající vzoru — ideální pro **zahrnutí souborů podle přípony** v konkrétní hierarchii adresářů.

#### Kroky implementace
1. **Definovat filtr cesty souboru** – použijte glob nebo regex vzory pro shodu adresářů.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Inicializovat index a přidat dokumenty** – aplikujte filtr cesty spolu s ostatními pravidly.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Časté úskalí a tipy

- **Nikdy neprovádějte smíchání absolutních a relativních cest** ve stejné konfiguraci filtru – může to vést k neočekávaným vyloučením.  
- **Resetujte `IndexSettings`** při přepínání sad filtrů; jinak mohou přetrvávat předchozí filtry.  
- **Kombinujte horní limit délky s filtrem přípon** pro velké kolekce, aby se snížila spotřeba paměti.  
- LoggingOptions řídí konfiguraci logování pro GroupDocs.Search.  
- **Povolte logování** (`LoggingOptions.setEnabled(true)`) pro zjištění, proč byl soubor odmítnut.  

## Často kladené otázky

**Q: Mohu změnit kritéria filtru po vytvoření indexu?**  
A: Ano. Přestavte index s novým `DocumentFilter` nebo použijte inkrementální indexaci s aktualizovanými nastaveními.

**Q: Funguje filtr přípon souborů java na komprimované archivy (např. ZIP)?**  
A: GroupDocs.Search může indexovat podporované formáty archivů, ale filtr přípon se vztahuje na samotný archiv, nikoli na vnitřní soubory. Pro hlubší kontrolu použijte vnořené filtry.

**Q: Jak debugovat, proč byl konkrétní soubor vyloučen?**  
A: Povolte logování knihovny (`LoggingOptions.setEnabled(true)`) a prohlédněte si log — zpráva uvádí, který filtr odmítl daný soubor.

**Q: Je možné kombinovat filtr přípon souborů java s vlastním regex filtrem?**  
A: Rozhodně. Zabalte regex filtr do `DocumentFilter.createAnd()` vedle filtru přípon.

**Q: Jaký dopad na výkon má přidání mnoha filtrů?**  
A: Každý filtr přidává během indexace mírnou režii, ale snížení objemu indexovaných dat obvykle převáží náklady. Otestujte na reprezentativním vzorku, abyste našli optimální rovnováhu.

---

**Last Updated:** 2026-09-06  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Související tutoriály

- [Vlastní formát data Java | Vyhledávání v časovém rozmezí s GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Mistrovské booleanové vyhledávání s GroupDocs.Search pro Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Optimalizace výkonu vyhledávání pomocí pokročilých technik indexování v GroupDocs.Search pro Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

