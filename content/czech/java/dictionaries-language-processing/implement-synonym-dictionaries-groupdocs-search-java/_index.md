---
date: '2026-10-17'
description: Naučte se, jak používat synonyma v Javě s GroupDocs.Search, import synonym
  dictionaries, manage synonym groups a optimalizovat váš search index pro lepší relevance.
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: Naučte se, jak používat synonyma v Javě s GroupDocs.Search, import
  synonym dictionaries, manage synonym groups a optimalizovat váš search index pro
  lepší relevance.
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: Jak používat synonyma v Javě s GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: Jak používat synonyma v Javě s GroupDocs.Search
type: docs
url: /cs/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat synonyma v Javě s GroupDocs.Search

Pokud chcete, aby vaši uživatelé našli správný obsah i když zadávají různá slova, **search with synonyms** je řešením. V tomto průvodci se naučíte, jak vytvořit slovník synonym, importovat nebo exportovat jej, spravovat skupiny synonym a spustit vyhledávání, které automaticky rozšiřuje dotazy pomocí těchto synonym. Ať už budujete CMS, katalog e‑commerce nebo úložiště právních dokumentů, přidání podpory synonym může výrazně zvýšit relevantnost a míru konverze.

## Rychlé odpovědi
- **Jaký je první krok k přidání synonym?** Vytvořte instanci `Index` a pracujte s API `SynonymDictionary`.  
- **Mohu importovat hotový slovník synonym?** Ano – zavolejte `importDictionary(path)` s umístěním souboru.  
- **Jak zapnu vyhledávání s podporou synonym?** Povolit `SearchOptions.setUseSynonymSearch(true)`.  
- **Je možné upravovat skupiny synonym za běhu?** Ano – můžete vymazat, přidat nebo načíst skupiny pomocí API slovníku.  
- **Co bych měl sledovat při škálování indexu?** Pravidelně odstraňujte nepoužívané položky a laděte haldu JVM pro velké soubory synonym.

## Co je search with synonyms?
**Search with synonyms** znamená, že engine považuje sadu slov nebo frází za zaměnitelné. Když uživatel napíše **“better”**, engine také hledá **“improve”**, **“enhance”** nebo jakýkoli jiný termín, který jste definovali ve stejné skupině synonym, a poskytuje tak bohatší výsledky, aniž by měnil uživatelův dotaz.

## Proč povolit podporu synonym v GroupDocs.Search?
Povolení podpory synonym umožňuje engine automaticky rozšířit dotazy tak, aby zahrnovaly ekvivalentní termíny, což zlepšuje relevanci výsledků, zvyšuje spokojenost uživatelů a může zvýšit míru konverze pro e‑commerce nebo obsahově orientované stránky. Také centralizuje správu terminologie, čímž snižuje nároky na údržbu napříč více aplikacemi.

## Předpoklady
- GroupDocs.Search for Java verze **25.4** nebo novější.  
- Java IDE (IntelliJ IDEA, Eclipse, atd.) s podporou Maven.  
- Základní znalost Javy a povědomí o struktuře Maven projektu.

### Požadované knihovny a verze
- GroupDocs.Search for Java **25.4** nebo vyšší.

### Nastavení prostředí
- IDE dle vašeho výběru (IntelliJ IDEA, Eclipse, atd.).  
- Maven pro správu závislostí.

### Požadované znalosti
- Objektově orientované programování v Javě.  
- Základní operace se soubory (I/O).

## Nastavení GroupDocs.Search pro Javu

### Informace o instalaci
Přidejte repozitář a závislost do vašeho `pom.xml`:

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

**Přímé stažení** – můžete také stáhnout nejnovější JAR z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Free trial:** Otestujte základní funkce bez licence.  
- **Temporary license:** Rozšiřte možnosti zkušební verze během hodnocení.  
- **Purchase:** Vyžadováno pro produkční použití a plnou sadu funkcí.

#### Základní inicializace a nastavení
Vytvořte instanci `Index` a poté přidejte dokumenty, které mají být prohledávatelné:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## Jak přidat synonyma do vašeho vyhledávacího indexu

### Funkce 1: vytváření a indexování indexu
Třída `Index` představuje prohledávatelnou kolekci dokumentů uložených na disku nebo v paměti.  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### Funkce 2: získání synonym pro slovo
`SynonymDictionary` spravuje skupiny synonym a poskytuje metody pro dotazování na synonyma pro daný termín.  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Funkce 3: získání skupin synonym
`SynonymDictionary.getGroups()` vrací seznam všech definovaných skupin synonym s jejich identifikátory.  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### Funkce 4: správa položek slovníku synonym
`add(word, synonym)` vloží nový vztah synonym do slovníku. `clear()` odstraní všechny položky a `remove(word)` smaže konkrétní termín ze slovníku.  

```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### Funkce 5: export synonym do souboru
`exportDictionary(path)` zapíše aktuální slovník synonym do binárního .dat souboru na určené místo.  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### Funkce 6: import synonym ze souboru
`importDictionary(path)` načte dříve exportovaný .dat soubor do slovníku synonym.  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### Funkce 7: provádění vyhledávání s podporou synonym
`SearchOptions` konfiguruje chování dotazu, včetně toho, zda je povoleno rozšíření synonym. `setUseSynonymSearch(true)` zapíná vyhledávání s podporou synonym pro nadcházející dotaz.  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## Jak vyhledávat se synonyma
Načtěte svůj `Index`, povolte vyhledávání se synonyma a spusťte dotaz. Engine automaticky rozšíří dotaz pomocí slovníku synonym, který jste vytvořili nebo importovali, a vrátí shody pro všechny související termíny.

## Jak importovat slovník synonym
Pokud již máte `.dat` soubor připravený v jiném prostředí, jednoduše zavolejte `importDictionary(path)`. To je ideální pro synchronizaci slovníků mezi vývojovými, testovacími a produkčními servery.

## Jak spravovat skupiny synonym
Skupiny synonym vám umožňují považovat sadu termínů za jedinečnou logickou entitu. Přidávání, mazání nebo načítání skupin se provádí pomocí API `SynonymDictionary`, jak je ukázáno v kódech výše.

## Jak optimalizovat vyhledávací index
- **Pravidelně odstraňujte nepoužívané položky:** Použijte `clear()` před hromadnými aktualizacemi.  
- **Upravte haldu JVM:** Velké slovníky mohou vyžadovat více paměti; odpovídajícím způsobem zvyšte parametr `-Xmx`.  
- **Udržujte knihovnu aktuální:** Nové verze obsahují vylepšení výkonu a opravy chyb.

## Praktické aplikace
1. **Content management systems (CMS):** Uživatelé najdou články i když používají alternativní terminologii.  
2. **E‑commerce platforms:** Vyhledávání produktů se stane tolerantním k synonymům jako “laptop” vs. “notebook”.  
3. **Document repositories:** Právní nebo medicínské archivy těží z doménově specifických skupin synonym, což zlepšuje vyhledatelnost pro profesionály.

## Úvahy o výkonu
- **Optimalizujte úložiště indexu:** Periodicky přestavujte index, aby se odstranila zastaralá data.  
- **Spravujte využití paměti:** Sledujte spotřebu haldy při načítání velkých souborů synonym; slovník o velikosti 500 MB typicky vyžaduje 2 GB haldu na 64‑bitovém JVM.  
- **Pravidelné aktualizace:** Používejte nejnovější verzi GroupDocs.Search pro opravy chyb a zrychlení.

## Časté problémy a řešení
| Problém | Pravděpodobná příčina | Řešení |
|-------|--------------|-----|
| Neobjevují se žádné shody synonym | `setUseSynonymSearch(true)` není nastaveno nebo slovník nebyl importován | Ověřte, že je volba povolena a soubor slovníku existuje. |
| Chyby nedostatku paměti během importu | Velmi velký `.dat` soubor překračuje haldu JVM | Zvyšte velikost haldy `-Xmx` nebo importujte po menších dávkách. |
| Duplicitní položky ve výsledcích | Stejný termín se objevuje ve více skupinách synonym | Konsolidujte překrývající se skupiny pomocí `clear()` a poté `addRange()`. |

## Často kladené otázky

**Q: Jaký je minimální systémový požadavek pro používání GroupDocs.Search?**  
**A:** Jakýkoli moderní operační systém s kompatibilní JDK (Java 8 nebo novější) je dostačující.

**Q: Jak často bych měl aktualizovat svůj slovník synonym?**  
**A:** Aktualizujte jej, kdykoli se objeví nová terminologie – použijte `clear()` následované `addRange()` pro čistou obnovu.

**Q: Mohu spouštět GroupDocs.Search bez zakoupení licence?**  
**A:** Free trial funguje pro hodnocení, ale licence je vyžadována pro produkční nasazení.

**Q: Jaké jsou osvědčené postupy pro indexování velkých datových sad?**  
**A:** Rozdělte data do logických dávek, sledujte využití haldy a naplánujte pravidelnou údržbu indexu.

**Q: Nevidím očekávané shody synonym – co bych měl zkontrolovat?**  
**A:** Ověřte, že je slovník správně importován, že `setUseSynonymSearch(true)` je aktivní, a že termíny jsou přítomny ve skupinách synonym.

**Zdroje**  
- [Dokumentace](https://docs.groupdocs.com/search/java/)  
- [Reference API](https://reference.groupdocs.com/search/java)  
- [Stáhnout GroupDocs.Search pro Javu](https://releases.groupdocs.com/search/java/)  
- [GitHub repozitář](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/search/10)  
- [Získání dočasné licence](https://purchase.groupdocs.com/temporary-license/) 

---

**Poslední aktualizace:** 2026-10-17  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Související tutoriály

- [Vytvořit a spravovat Groupdocs Search Java index](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Java Full Text Search Library – Optimalizace indexu pomocí GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Java Fuzzy Search: Přidání dokumentů do indexu pomocí GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}