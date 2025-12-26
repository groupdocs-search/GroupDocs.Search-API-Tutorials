---
date: '2025-12-26'
description: Naučte se vyhledávat a zvýrazňovat text v dokumentech pomocí GroupDocs.Search
  pro Javu. Prozkoumejte techniky zvýrazňování celých dokumentů i fragmentů.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Vyhledávejte a zvýrazňujte text pomocí GroupDocs.Search pro Javu
type: docs
url: /cs/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Vyhledávání a zvýrazňování textu v dokumentech pomocí GroupDocs.Search pro Java

V dnešní digitální éře je **vyhledávání a zvýrazňování textu** v rozsáhlých kolekcích dokumentů běžnou potřebou. Ať už vytváříte nástroj pro právní revizi, akademický výzkumný portál nebo dashboard zákaznické podpory, schopnost okamžitě najít a zdůraznit klíčové termíny výrazně zlepšuje použitelnost. V tomto komplexním průvodci se dozvíte, jak implementovat **vyhledávání a zvýrazňování textu** pomocí GroupDocs.Search pro Java — včetně zvýrazňování celých dokumentů i zvýrazňování na úrovni fragmentů pro zaměřený kontext.

## Rychlé odpovědi
- **Co znamená „vyhledávání a zvýrazňování textu“?** Jedná se o vyhledání dotazových termínů v dokumentu a jejich vizuální zvýraznění (např. pomocí barvy pozadí).  
- **Která knihovna tuto funkci poskytuje?** GroupDocs.Search pro Java.  
- **Potřebuji licenci?** Bezplatná zkušební verze stačí pro hodnocení; pro produkční nasazení je vyžadována plná licence.  
- **Mohu přizpůsobit barvy zvýraznění?** Ano — libovolná RGB barva může být nastavena pomocí `HighlightOptions`.  
- **Je podporováno zvýrazňování fragmentů?** Rozhodně; můžete definovat termíny před a po shodě pro vytvoření stručných úryvků.

## Co je vyhledávání a zvýrazňování textu?
Vyhledávání a zvýrazňování textu je proces prohledávání indexu dokumentů podle zadaného dotazu, získání odpovídajících dokumentů a následné označení každého výskytu dotazového termínu v výstupu dokumentu (HTML, PDF atd.). Tento vizuální prvek pomáhá koncovým uživatelům okamžitě najít relevantní informace.

## Proč použít GroupDocs.Search pro Java?
- **Vysoce výkonná indexace** s konfigurovatelnou kompresí.  
- **Bohaté API pro zvýrazňování** funguje na celých dokumentech i na vlastních fragmentech.  
- **Podpora napříč formáty** (DOCX, PDF, PPTX, TXT a další).  
- **Jednoduchá integrace s Maven** a přehledné Java‑centrické API.

## Předpoklady
- Java Development Kit (JDK) 8 nebo novější.  
- Maven pro správu závislostí.  
- IDE, například IntelliJ IDEA nebo Eclipse.  
- Základní znalost syntaxe jazyka Java.

## Nastavení GroupDocs.Search pro Java

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

Můžete také stáhnout nejnovější JAR přímo z oficiálního webu: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Začněte s bezplatnou zkušební verzí nebo si pořiďte dočasnou licenci pro hodnocení. Pro produkční nasazení zakupte plnou licenci, která odemkne všechny funkce.

## Průvodce implementací

Implementace je rozdělena do dvou praktických částí: **zvýrazňování v celých dokumentech** a **zvýrazňování ve fragmentech**. Obě sekce obsahují nezbytné kroky pro **to, jak zvýraznit Java** dokumenty pomocí GroupDocs.Search.

### Konfigurace nastavení indexu
Před indexací nakonfigurujte úložiště tak, aby používalo vysokou kompresi — tím se sníží využití disku při zachování rychlosti vyhledávání.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Zvýrazňování v celých dokumentech

#### Krok 1: Vytvořit a naplnit index
Vytvořte složku indexu a přidejte všechny zdrojové soubory, které chcete prohledávat.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Krok 2: Proveďte vyhledávání a aplikujte zvýraznění
Vyhledejte termín (např. `ipsum`) a vygenerujte HTML soubor se zvýrazněnými shodami.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Klíčové možnosti vysvětleny**
- **Compression** – vysoká komprese šetří úložiště.  
- **HighlightColor** – nastavte libovolnou RGB hodnotu, aby odpovídala vaší UI paletě.  
- **UseInlineStyles** – `false` generuje čisté HTML, které lze stylovat globálně pomocí CSS.

### Zvýrazňování ve fragmentech

#### Krok 1: Indexace a vyhledávání (stejné jako výše)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Krok 2: Definujte kontext fragmentu a zvýrazněte
Určete, kolik termínů před a po shodě se má objevit v každém fragmentu.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Krok 3: Získejte a zapište zvýrazněné fragmenty
Shromážděte vygenerované fragmenty a zapište je do HTML souboru.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Praktické aplikace
1. **Legal Document Review** – okamžitě zvýrazněte zákony, klauzule nebo odkazy na případy.  
2. **Academic Research** – zobrazte klíčovou terminologii napříč desítkami PDF a Word souborů.  
3. **Customer Support** – identifikujte čísla objednávek nebo chybové kódy v historii tiketů.

## Úvahy o výkonu
- **Index Size** – vysoká komprese (`Compression.High`) snižuje velikost na disku.  
- **Fragment Context** – větší hodnoty `termsBefore/After` zvyšují přesnost, ale mohou ovlivnit rychlost.  
- **Memory Management** – monitorujte haldu JVM při indexaci velkých korpusů; zvažte inkrementální indexaci pro velmi velké sady.

## Časté problémy a řešení
- **Indexing Errors** – ověřte cesty k souborům a zajistěte, aby aplikace měla oprávnění ke čtení/zápisu.  
- **No Highlights Appear** – potvrďte, že `UseInlineStyles` odpovídá vašemu výstupnímu formátu (HTML vs. PDF).  
- **Color Not Applied** – ujistěte se, že RGB hodnoty jsou v rozmezí 0‑255 a že HTML prohlížeč podporuje daný styl.

## Často kladené otázky

**Q: Jaké jsou výhody používání GroupDocs.Search pro Java?**  
A: Nabízí rychlou, škálovatelnou indexaci, přizpůsobitelné zvýrazňování a podporu mnoha formátů dokumentů.

**Q: Jak mohu integrovat GroupDocs.Search s REST API?**  
A: Zveřejněte metody vyhledávání a zvýrazňování prostřednictvím Spring Boot kontrolerů, které vrací HTML nebo JSON payloady.

**Q: Zvládá knihovna soubory chráněné heslem?**  
A: Ano — poskytněte heslo při přidávání dokumentu do indexu.

**Q: Mohu přizpůsobit značkování zvýraznění mimo barvu?**  
A: Rozhodně; můžete vložit CSS třídy pomocí `HighlightOptions` nebo upravit HTML po vygenerování.

**Q: Jaká verze byla testována pro tento průvodce?**  
A: Kód byl ověřen proti GroupDocs.Search 25.4.

---

**Poslední aktualizace:** 2025-12-26  
**Testováno s:** GroupDocs.Search 25.4  
**Autor:** GroupDocs