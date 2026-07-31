---
date: '2026-07-31'
description: Zjistěte, jak implementovat case insensitive search java přidáním dokumentů
  do indexu s GroupDocs.Search, pomocí nahrazování znaků k normalizaci textu během
  indexování.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Case insensitive search java vám umožní přidat dokumenty do indexu
  a dotazovat je bez starostí o velikost písmen. Tento průvodce ukazuje, jak GroupDocs.Search
  normalizuje text během indexování pro rychlé a spolehlivé výsledky.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Case Insensitive Search Java – Indexování dokumentů s GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Přidání dokumentů do indexu pro Case‑Insensitive Search v Java
type: docs
url: /cs/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Přidání dokumentů do indexu pro vyhledávání bez rozlišení velkých a malých písmen v Javě

Když potřebujete **vyhledávání bez rozlišení velkých a malých písmen v Javě**, které spolehlivě najde informace bez ohledu na to, jak je uživatelé zadávají, klíčové je přidat dokumenty do indexu při normalizaci textu. V tomto tutoriálu vás provedeme konfigurací GroupDocs.Search pro Java tak, aby každý dokument, který indexujete, byl během indexování automaticky převeden na malá písmena (nebo jinak transformován), což zaručuje výsledky bez rozlišení velikosti písmen bez další logiky během dotazu.

## Rychlé odpovědi
- **Co znamená „add documents to index“?** To znamená načtení zdrojových souborů do vyhledávatelné datové struktury, aby je bylo možné později dotazovat.  
- **Proč použít nahrazení znaků?** Normalizuje každý znak – obvykle na malá písmena – takže vyhledávání automaticky ignoruje rozdíly v velikosti písmen.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; plná licence je vyžadována pro nasazení do produkce.  
- **Jaká verze Javy je požadována?** Java 8 nebo novější; knihovna cílí na Java 11+ pro optimální výkon.  
- **Mohu přepnout na vyhledávání s rozlišením velkých a malých písmen, pokud je potřeba?** Ano – možnosti vyhledávání vám umožní přepínat rozlišení velikosti písmen pro jednotlivé dotazy.

## Co znamená „add documents to index“ v GroupDocs.Search?

Načtěte své zdrojové soubory (PDF, DOCX, TXT atd.) do vyhledávatelného indexu, aby je engine mohl rychle načíst. Přidání dokumentů do indexu parsuje každý soubor, extrahuje prostý text a uloží jej do optimalizované datové struktury, která umožňuje rychlé vyhledávání.

## Proč povolit nahrazení znaků během indexování?

Nahrazení znaků převádí každý znak na předdefinovaný ekvivalent – nejčastěji na malá písmena – během vytváření indexu. Tím se zajistí, že variace v kapitalizaci, diakritice nebo lokálně specifických symbolech neovlivní výsledky vyhledávání. Normalizací textu v čase indexování může engine porovnávat dotazy s konzistentním tokenovým souborem, což poskytuje rychlé, spolehlivé chování bez rozlišení velikosti písmen bez dalšího zpracování během každého vyhledávání.

## Požadavky
- **GroupDocs.Search for Java** verze 25.4 nebo novější (knihovna podporuje více než 30 formátů souborů a může indexovat dokumenty s několika stovkami stránek, aniž by načítala celý soubor do paměti).  
- **Java Development Kit (JDK)** 8 nebo novější nainstalovaný.  
- Základní znalost **Maven** (nebo schopnost přidat JAR soubory ručně).  

## Nastavení GroupDocs.Search pro Java

### Nastavení Maven
Přidejte repozitář GroupDocs a závislost do souboru `pom.xml`:

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
Pokud raději nepoužíváte Maven, stáhněte si nejnovější JAR z oficiální stránky: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Free Trial** – stáhněte si zkušební licenci a začněte experimentovat.  
- **Temporary License** – požádejte o prodlouženou testovací licenci prostřednictvím portálu GroupDocs.  
- **Full License** – zakupte produkční licenci, až budete připraveni spustit do provozu.

### Základní inicializace (vytvoření indexu)
Následující úryvek vytvoří složku indexu a povolí nahrazení znaků:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Průvodce implementací

### Povolení nahrazení znaků v nastavení indexu
Aktivace této funkce říká enginu, aby během indexování nahrazoval znaky, což je klíčový krok pro chování bez rozlišení velikosti písmen.

#### Krok 1: Konfigurace `IndexSettings`
`IndexSettings` je konfigurační objekt, který řídí, jak index ukládá a zpracovává text. Nastavením `useCharacterReplacements` na **true** zapnete automatické převádění na malá písmena (nebo jakékoli vlastní mapování, které poskytnete).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Konfigurace nahrazení znaků
Mapujte každý znak na jeho ekvivalent v malých písmenech (nebo jakékoli vlastní mapování, které potřebujete).

#### Krok 2: Definování a přidání párů nahrazení
Slovník nahrazení obsahuje páry jako `'A' → 'a'`, `'É' → 'e'` atd. Přidání těchto párů před indexováním zajistí, že každý token bude normalizován.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Indexování dokumentů
Nyní, když je index připraven, můžete **add documents to index** z libovolné složky.

#### Krok 3: Přidání dokumentů pro indexování
GroupDocs.Search prohledá cílový adresář, extrahuje text z každého podporovaného typu souboru, použije mapu nahrazení a zapíše tokeny do úložiště indexu.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Provedení vyhledávání s rozlišením velikosti písmen (volitelné)

#### Krok 4: Provedení vyhledávání s rozlišením velikosti písmen
`SearchOptions` konfiguruje chování dotazu, například přepínání rozlišení velikosti písmen, což umožňuje jemnou kontrolu nad tím, jak jsou vyhledávání prováděna.  
`SearchOptions.setUseCaseSensitiveSearch(true)` nutí engine považovat velká a malá písmena za odlišná během konkrétního dotazu, čímž přepíše výchozí chování bez rozlišení velikosti písmen.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Praktické aplikace
1. **Marketingové kampaně** – Normalizujte názvy produktů, aby prodejní týmy mohly najít materiály bez starostí o velikost písmen.  
2. **Zákaznická podpora** – Pohánějte vyhledávací pole helpdesku, které vrátí správný článek, ať už uživatel napíše „login“ nebo „Login“.  
3. **E‑commerce katalogy** – Zajistěte, aby zákazníci našli položky bez ohledu na to, jak zadávají názvy produktů, což zvyšuje konverzní poměr.

## Úvahy o výkonu
- **Organizujte zdrojové soubory** – Přehledná hierarchie složek snižuje čas potřebný k prohledávání během kroku **add documents to index**.  
- **Sledujte paměť** – Indexování velkých korpusů může spotřebovat značnou RAM; zpracování souborů v dávkách po 500 – 1 000 položkách udržuje využití haldy pod kontrolou.  
- **Asynchronní indexování** – Pokud je podporováno, spusťte indexování na pozadí, aby UI zůstalo responzivní a neblokovalo uživatelské operace.

## Časté problémy a řešení

| Problém | Předpokládaná příčina | Řešení |
|---------|-----------------------|--------|
| Nejsou vráceny žádné výsledky pro známý termín | Nahrazení znaků není povoleno | Ověřte, že `settings.setUseCharacterReplacements(true)` a že slovník nahrazení obsahuje potřebné znaky. |
| Chyba nedostatku paměti během indexování | Indexování příliš mnoha velkých souborů najednou | Indexujte v menších dávkách nebo zvýšte velikost haldy JVM (`-Xmx4g`). |
| Vyhledávání neočekávaně vrací výsledky s rozlišením velikosti písmen | Bylo nastaveno `SearchOptions.setUseCaseSensitiveSearch(true)` | Odstraňte nebo nastavte na `false` pro výchozí chování bez rozlišení velikosti písmen. |
| Doba načítání indexu překračuje očekávání | Neefektivní uspořádání složek nebo nepoužití SSD | Přesuďte soubory, odstraňte nepoužívané dokumenty a uložte index na rychlý SSD. |
| Speciální znaky jsou ignorovány | Ve slovníku nahrazení chybí položky Unicode | Přidejte mapování pro znaky jako “é”, “ß”, “ø” na požadované ekvivalenty. |

## Často kladené otázky

**Q: Jak mám během indexování zacházet se speciálními znaky (např. “é”, “ß”)?**  
**A:** Zařaďte tyto znaky do svého slovníku nahrazení, mapujte je na jejich ASCII ekvivalenty nebo je ponechte beze změny podle požadavků vyhledávání.

**Q: Mohu omezit nahrazení znaků na konkrétní jazyk?**  
**A:** Ano. Vytvořte vlastní pole nahrazení, které obsahuje pouze znaky pro cílový jazyk, a přidejte jej do slovníku.

**Q: Co mám dělat, pokud načítání indexu trvá dlouho?**  
**A:** Optimalizujte strukturu složek, odstraňte zbytečné soubory a uložte index na vysokorychlostní SSD. Inkrementální indexování také snižuje zátěž načítání.

**Q: Je možné po indexování vrátit zpět nahrazení znaků?**  
**A:** Ne. Nahrazení jsou zakódována v indexovaných datech; musíte index přestavět s novým nastavením, abyste je změnili.

**Q: Kde najdu podrobnější dokumentaci API?**  
**A:** Oficiální dokumentace a reference API poskytují podrobné informace (viz zdroje níže).

## Zdroje
- [Dokumentace](https://docs.groupdocs.com/search/java/)
- [Reference API](https://reference.groupdocs.com/search/java)
- [Stáhnout GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [Repozitář na GitHubu](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/search/10)
- [Informace o dočasné licenci](https://purchase.groupdocs.com/temporary-license/) 

---

**Poslední aktualizace:** 2026-07-31  
**Testováno s:** GroupDocs.Search 25.4 pro Java  
**Autor:** GroupDocs  

---

## Související tutoriály

- [Nahrazení znaků v GroupDocs.Search Java: Komplexní průvodce pro zlepšení vyhledávání textu a indexování](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Přidání dokumentů do indexu: vyhledávání s rozlišením velikosti písmen v Javě s GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Jak přidat dokumenty do indexu pomocí GroupDocs.Search pro Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)