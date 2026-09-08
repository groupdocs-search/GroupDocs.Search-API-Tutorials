---
date: '2026-07-21'
description: Tutoriál Vytvořte Boolean dotaz v Javě ukazuje, jak implementovat boolean
  AND, OR, NOT vyhledávání pomocí GroupDocs.Search for Java, přidat dokumenty do indexu
  a boost document retrieval.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Tutoriál Vytvořte Boolean dotaz v Javě vysvětluje krok za krokem,
  jak vytvořit AND, OR, NOT dotazy s GroupDocs.Search for Java, přidat dokumenty do
  indexu a zlepšit retrieval performance.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Vytvořte Boolean dotaz v Javě – Ovládněte Boolean vyhledávání s GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Vytvořte Boolean dotaz v Javě: Ovládněte Boolean vyhledávání s GroupDocs.Search
  for Java'
type: docs
url: /cs/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Vytvořte Boolean dotaz v Javě: Ovládněte Boolean vyhledávání s GroupDocs.Search pro Javu

Prohledávání obrovských kolekcí dokumentů může připomínat hledání jehly v kupce sena. **Vytvořte Boolean dotaz v Javě** vám umožňuje přesně říct enginu, co potřebujete — dokumenty, které obsahují *obě* termíny, *kterýkoli* termín, nebo *vyloučit* nechtěná slova. V tomto průvodci vás provedeme nastavením **GroupDocs.Search for Java**, přidáváním dokumentů do indexu a vytvářením výkonných boolean dotazů, které zlepší vaše **document retrieval java** workflowy. Na konci budete schopni napsat čistý, udržovatelný kód, který vytváří boolean dotazy v Javě pomocí jen několika řádků.

## Rychlé odpovědi
- **Co je boolean AND dotaz?** Vrací pouze dokumenty, které obsahují *vše* zadané termíny.  
- **Jak se OR liší od AND?** OR odpovídá dokumentům s *kterýmkoli* z termínů, čímž rozšiřuje množinu výsledků.  
- **Kdy mám použít NOT?** Použijte NOT k odfiltrování dokumentů obsahujících nechtěná slova.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro testování; pro produkci je vyžadována komerční licence.  
- **Jaká verze Javy je požadována?** Java 8+ je podporována; JDK 11+ se doporučuje.

## Co je **vytvořit boolean dotaz v Javě**?
`create boolean query java` odkazuje na vytváření vyhledávacího dotazu v Javě, který kombinuje logické operátory jako AND, OR a NOT pomocí API GroupDocs.Search. Sestavením těchto operátorů můžete přesně řídit, které dokumenty odpovídají, což umožňuje pokročilé filtrování, ladění relevance a složité vyhledávací scénáře.

## Proč používat GroupDocs.Search pro Javu?
- **Vysoký výkon** na velkých sadách dokumentů — dokáže indexovat a prohledávat 500 GB textu za méně než minutu na standardním serveru.  
- **Bohaté API**, které podporuje jak textové, tak objektové dotazy, což vám umožní vybrat styl, který odpovídá vaší architektuře.  
- **Vestavěná podpora jazyků** pro stemming, stop‑slova a fuzzy vyhledávání ve více než 30 jazycích.  
- **Jednoduchá integrace** s Mavenem nebo přímým stažením JAR, vyžadující jen několik řádků kódu pro zahájení.

## Předpoklady
- **GroupDocs.Search for Java** (v25.4 nebo novější) — viz odkaz ke stažení níže.  
- JDK 8+ nainstalováno a nakonfigurováno ve vašem IDE (IntelliJ IDEA, Eclipse atd.).  
- Základní znalost Javy a Maven pro správu závislostí.  

## Nastavení GroupDocs.Search pro Javu

### Nastavení Maven
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

### Přímé stažení
Alternativně stáhněte nejnovější JAR z oficiální stránky: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Začněte s bezplatnou zkušební licencí pro vyzkoušení všech funkcí. Pro produkční použití zakupte komerční licenci, která odemkne plnou funkčnost.

### Základní inicializace a nastavení
Create an index folder and instantiate the `Index` object:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Jak vytvořit boolean dotaz v Javě?
Třída `Index` představuje prohledávatelnou kolekci dokumentů uložených na disku. `BooleanQuery` kombinuje více pod‑dotazů pomocí logických operátorů. `createAndQuery`, `createOrQuery` a `createNotQuery` vytvářejí pod‑dotazy AND, OR a NOT. Načtěte nebo vytvořte instanci `Index`, přidejte dokumenty a poté vytvořte objekt `BooleanQuery` pomocí `createAndQuery`, `createOrQuery` nebo `createNotQuery`. Zavolejte `index.search(query)`, abyste získali odpovídající dokumenty. Tento vzor funguje jak pro jednoduché, tak pro složité scénáře a vyžaduje pouze tři logické kroky: inicializaci indexu, přidání dokumentů a provedení dotazu.

## Boolean AND vyhledávání

### Přehled
AND dotaz zužuje výsledky, zlepšuje relevanci, když potřebujete dokumenty, které splňují více kritérií.

### Kroky implementace
1. **Inicializace Indexu** — toto také ukazuje **přidání dokumentů do indexu** pro scénář AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Indexování dokumentů**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Provést vyhledávání textovým dotazem** — pomocí jednoduché řetězcové syntaxe.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Provést vyhledávání objektovým dotazem** — užitečné při programovém sestavování dotazů (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Boolean OR vyhledávání

### Přehled
OR dotaz je ideální pro průzkumná vyhledávání, kde chcete zachytit dokumenty obsahující alespoň jedno z několika klíčových slov (**search with or java**).

### Kroky implementace
1. **Inicializace Indexu**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Indexování dokumentů**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Provést vyhledávání textovým dotazem**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Provést vyhledávání objektovým dotazem**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Boolean NOT vyhledávání

### Přehled
NOT dotaz vám pomáhá odstranit irelevantní dokumenty, například filtrováním názvu značky konkurenta (**boolean search examples java**).

### Kroky implementace
1. **Inicializace Indexu**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Indexování dokumentů**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Provést vyhledávání textovým dotazem**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Provést vyhledávání objektovým dotazem**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Složité Boolean dotazy

### Přehled
Složité dotazy vám umožňují modelovat reálné vyhledávací scénáře, například „najít sportovní články, které jsou pozitivní, ale vyloučit jakékoli zmínky o konkrétních sportovcích“.

### Kroky implementace
1. **Inicializace Indexu**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Indexování dokumentů**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Provést vyhledávání textovým dotazem**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Provést vyhledávání objektovým dotazem**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Praktické aplikace **java boolean and or** dotazů
- **Systémy pro správu dokumentů** — najděte smlouvy, které obsahují jak „confidential“, **AND** „renewal“.  
- **Právní výzkum** — filtrujte judikaturu pomocí **AND**/**OR**, přičemž vylučujete zastaralé zákony pomocí **NOT**.  
- **Zákaznická podpora** — načtěte tickety, které zmiňují „login“ **AND** „error“, ale ne „resolved“.  
- **Kurátorství obsahu** — shromážděte blogové příspěvky o „cloud“ **OR** „serverless“ pro newsletter.

## Časté úskalí a řešení problémů
- **Chybějící obnovení indexu** — po přidání nových dokumentů zavolejte `index.update()`, aby byly prohledávatelné.  
- **Nesprávné mezery u operátorů** — GroupDocs.Search očekává mezery kolem operátorů (`AND`, `OR`, `NOT`).  
- **Rozlišování velkých a malých písmen** — dotazy jsou ve výchozím nastavení necitlivé na velikost písmen, ale vlastní analyzátory to mohou ovlivnit.  
- **Velké množiny výsledků** — použijte stránkování (`search(query, 0, 100)`) k zabránění přetížení paměti.  

## Často kladené otázky

**Q: Můžu kombinovat více než dva termíny v AND dotazu?**  
A: Rozhodně. Můžete řetězit více objektů `createWordQuery` pomocí `createAndQuery`, nebo jednoduše napsat `"term1 AND term2 AND term3"` v textovém dotazu.

**Q: Podporuje GroupDocs.Search vyhledávání s maskou nebo fuzzy?**  
A: Ano. Přidejte `*` pro masku (např. `promot*`) nebo použijte `~` pro fuzzy shodu (např. `comfort~`).

**Q: Jak omezím vyhledávání na konkrétní typy souborů?**  
`FileTypeQuery` omezuje výsledky vyhledávání na určité formáty souborů, jako PDF nebo DOCX.  
A: Použijte třídu `FileTypeQuery` k omezení výsledků na PDF, DOCX atd., a kombinujte ji s vaším boolean dotazem.

**Q: Jaký je nejlepší způsob, jak sledovat výkon indexování?**  
A: Aktivujte vestavěný logger (`index.getLogger().setLevel(Level.INFO)`) a přezkoumejte časové metriky po každé operaci `add`.

**Q: Existuje způsob, jak zvýšit relevanci určitých termínů?**  
`BoostQuery` zvyšuje relevanční skóre specifikovaných termínů ve vyhledávacím dotazu.  
A: Ano. Obalte důležitá slova pomocí `BoostQuery`, aby se zvýšila jejich váha v algoritmu hodnocení.

---

**Poslední aktualizace:** 2026-07-21  
**Testováno s:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs

## Související tutoriály

- [Boolean operátory Java – Vytvoření vyhledávacího indexu a faceted vyhledávání](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Mistrovství GroupDocs.Search Java: Efektivní vyhledávání dokumentů a správa indexu](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java – Ovládání GroupDocs.Search Java – Vytvoření a správa vyhledávacího indexu](/search/java/indexing/groupdocs-search-java-create-index-guide/)