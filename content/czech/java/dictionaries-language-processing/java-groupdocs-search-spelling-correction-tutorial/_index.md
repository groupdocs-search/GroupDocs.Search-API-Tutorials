---
date: '2026-09-02'
description: Naučte se, jak vytvořit search index java a povolit spelling correction
  pomocí GroupDocs.Search. Postupujte podle step‑by‑step instrukcí pro přidání documents,
  nastavení max mistake count a zlepšení search accuracy.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Naučte se, jak vytvořit search index java a povolit spelling correction
  pomocí GroupDocs.Search. Postupujte podle step‑by‑step instrukcí pro přidání documents,
  nastavení max mistake count a zlepšení search accuracy.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Jak vytvořit search index java a povolit spelling
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Jak vytvořit search index java a povolit spelling
type: docs
url: /cs/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Jak vytvořit vyhledávací index java a povolit pravopis

V moderních Java aplikacích je poskytování přesných výsledků vyhledávání nezbytnou funkcí. Tento tutoriál ukazuje **jak vytvořit vyhledávací index java** a zapnout opravu pravopisu pomocí GroupDocs.Search, takže uživatelé získají relevantní výsledky i při překlepování dotazů. Uvidíte, jak nastavit knihovnu, přidat dokumenty, nakonfigurovat maximální počet chyb a spustit tolerantní vyhledávání na překlepy — vše bez psaní jediného řádku dalšího konfiguračního kódu.

## Rychlé odpovědi
- **Co dělá „enable spelling“?** Aktivuje vestavěný kontrolor pravopisu, který během vyhledávání přepisuje chybně napsané výrazy na jejich nejbližší správné tvary.  
- **Která knihovna tuto funkci poskytuje?** GroupDocs.Search pro Java.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkční použití je vyžadována plná licence.  
- **Mohu řídit toleranci?** Ano – použijte `setMaxMistakeCount` k definování, kolik překlepů je povoleno na dotaz.  
- **Je vhodný pro velké indexy?** Rozhodně – engine zvládá indexy s miliony záznamů a udržuje latenci dotazu pod 100 ms na typickém serverovém hardware.

## Co je GroupDocs.Search?
GroupDocs.Search je Java knihovna, která poskytuje rychlé full‑textové indexování a pokročilé vyhledávací funkce, včetně vestavěné opravy pravopisu. Podporuje více než 50 vstupních formátů a dokáže zpracovat dokumenty o stovkách stránek, aniž by načítala celý soubor do paměti.

## Proč povolit opravu pravopisu v Java aplikacích?
- **Zvyšuje spokojenost uživatelů** – návštěvníci získají správné výsledky i při nedokonalém psaní.  
- **Snižuje míru odchodů** – přesné výsledky udržují uživatele déle zapojené.  
- **Funguje napříč doménami** – od knihovních katalogů po vyhledávání produktů v e‑commerce, oprava pravopisu zlepšuje relevanci všude.

## Předpoklady
- Java Development Kit (JDK) nainstalován.  
- Základní znalost Javy a Maven.  
- Porozumění konceptům indexování.  
- Zkušební verze nebo licenční klíč GroupDocs.Search.

### Nastavení GroupDocs.Search pro Java
Integrovat knihovnu do vašeho Maven projektu.

**Nastavení Maven**  
Přidejte repozitář a závislost do souboru `pom.xml`:

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

**Přímé stažení**  
Alternativně stáhněte nejnovější verzi z [vydání GroupDocs.Search pro Java](https://releases.groupdocs.com/search/java/).

### Získání licence
Získejte bezplatnou zkušební licenci pro hodnocení. Pro produkční použití zakupte plnou licenci nebo požádejte o dočasný klíč na oficiální stránce.

## Jak vytvořit vyhledávací index v Javě?
`SearchIndex` je hlavní třída, která představuje vyhledávatelný index uložený na disku.  
Vytvořte instanci `SearchIndex`, která ukazuje na složku na disku, a poté přidejte dokumenty ze zdrojového adresáře. Engine vytváří invertovaný index, který umožňuje rychlé vyhledávání. Můžete volat `index.add()` pro každý soubor; knihovna automaticky extrahuje text podle typu souboru.

## Jak mohu povolit opravu pravopisu?
`getSpellingOptions()` vrací objekt konfigurace pravopisu pro index, který vám umožní povolit nebo upravit funkce kontroly pravopisu.  
Povolit pravopis voláním `index.getSpellingOptions().setEnabled(true)`. Tím řeknete engine, aby analyzoval výrazy dotazu a navrhl opravené alternativy, když jsou zjištěny nesrovnalosti. Funkce funguje ihned pro všechny indexované jazyky podporované knihovnou.

## Co je nastavení maximálního počtu chyb?
`setMaxMistakeCount` konfiguruje maximální počet úprav znaků, které kontrolor pravopisu toleruje na termín.  
`setMaxMistakeCount(int)` definuje maximální počet úprav znaků (vkládání, mazání, nahrazování), které kontrolor pravopisu toleruje na termín. Nastavením na **2** umožní engine opravit běžné dvouznakové překlepy a zároveň se vyhnout příliš agresivním opravám, které by mohly vrátit nesouvisející výsledky.

## Jak provést vyhledávání s opravou pravopisu
`search()` provádí dotaz proti indexu a vrací objekt `SearchResult` obsahující shody a případné opravené výrazy.  
Spusťte vyhledávací dotaz pomocí metody `search()`. Pokud dotaz obsahuje chybně napsaná slova, engine vrátí `SearchResult`, který zahrnuje opravené výrazy a seznam nejrelevantnějších dokumentů. Můžete uživateli zobrazit jak původní dotaz, tak opravenou verzi pro transparentnost.  
`SearchResult` obsahuje seznam odpovídajících dokumentů a informace o opravách dotazu.

## Praktické aplikace
1. **Knihovní systémy** – automaticky opravovat chybně napsané názvy knih nebo jména autorů.  
2. **E‑commerce platformy** – opravovat překlepy v názvech produktů pro zvýšení konverzního poměru.  
3. **Správa obsahu** – pomoci redakčnímu týmu najít články i při nedokonalých klíčových slovech.

## Úvahy o výkonu
- **Udržujte index aktuální** – pravidelně reindexujte nové nebo změněné soubory.  
- **Ladit nastavení paměti JVM** – přidělte dostatečnou haldu pro velké indexy (např. `-Xmx4g`).  
- **Monitorovat využití zdrojů** – upravte příznaky garbage‑collectoru, pokud zaznamenáte pauzy během hromadného indexování.

## Běžné problémy a řešení
| Příznak | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| Žádné výsledky po povolení pravopisu | Cesta k složce indexu je špatná nebo je prázdná | Ověřte, že `indexFolder` ukazuje na platný index a že `index.add()` byl úspěšný |
| Kontrolor pravopisu neopravu evidentních překlepů | `setMaxMistakeCount` je nastaven příliš nízko | Zvyšte počet na 2 nebo 3 pro tolerantnější opravu |
| Aplikace spadne při velkých sadách dokumentů | Nedostatečná halda JVM | Zvyšte volbu `-Xmx` (např. `-Xmx4g`) |

## Často kladené otázky

**Q: Co je GroupDocs.Search?**  
A: GroupDocs.Search je Java knihovna, která poskytuje rychlé indexování, pokročilé možnosti dotazování a vestavěnou opravu pravopisu pro jakoukoli Java aplikaci.

**Q: Jak získám licenci pro GroupDocs.Search?**  
A: Navštivte oficiální stránku a stáhněte si bezplatnou zkušební verzi nebo zakupte plnou licenci; dočasný klíč je také k dispozici pro krátkodobé testování.

**Q: Mohu integrovat GroupDocs.Search s jinými Java frameworky?**  
A: Ano, funguje bez problémů se Spring, Jakarta EE a jakoukoli standardní Java aplikací.

**Q: Jaké jsou běžné problémy při nastavování indexu?**  
A: Nesprávné cesty ke složkám, chybějící oprávnění k souborům nebo chybějící Maven závislosti jsou typické příčiny.

**Q: Jak oprava pravopisu zlepšuje výsledky vyhledávání?**  
A: Automaticky přepisuje chybně napsané dotazy na jejich nejbližší správné výrazy, vrací relevantnější výsledky a snižuje frustraci uživatelů.

## Další zdroje
- [Dokumentace](https://docs.groupdocs.com/search/java/)
- [Reference API](https://reference.groupdocs.com/search/java)
- [Stáhnout](https://releases.groupdocs.com/search/java/)
- [GitHub repozitář](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/search/10)
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-09-02  
**Testováno s:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Související tutoriály

- [Jak vytvořit index dokumentů a přidat dokumenty pomocí GroupDocs.Search API pro Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Zpracování jazyka v Javě – Vytvořit slovník synonym s GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Stop slova ve vyhledávání: Přidat dokumenty do indexu s GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)