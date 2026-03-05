---
date: '2026-01-29'
description: Naučte se, jak pomocí GroupDocs.Search pro Javu implementovat booleanové
  dotazy AND a OR, přidávat dokumenty do indexu a zlepšovat vyhledávání dokumentů.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'Java Boolean AND OR: Mistrovské Boolean vyhledávání s GroupDocs.Search pro
  Javu'
type: docs
url: /cs/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Ovládněte Boolean vyhledávání s GroupDocs.Search pro Java

Prohledávání obrovských kolekcí dokumentů může připomínat hledání jehly v kupce sena. S dotazy **java boolean and or** můžete motoru přesně říct, co potřebujete — dokumenty, které obsahují *obě* termíny, *kterýkoliv* termín, nebo *vyloučit* nežádoucí slova. V tomto průvodci vás provedeme nastavením **GroupDocs.Search for Java**, přidáváním dokumentů do indexu a vytvářením výkonných boolean dotazů, které posílí vaše **document retrieval java** workflowy.

## Rychlé odpovědi
- **Co je boolean AND dotaz?** Vrací pouze dokumenty, které obsahují *vše* zadané termíny.  
- **Jak se OR liší od AND?** OR vyhledává dokumenty s *kterýmkoliv* z termínů, čímž rozšiřuje množinu výsledků.  
- **Kdy použít NOT?** Použijte NOT k filtrování dokumentů obsahujících nežádoucí slova.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro testování; pro produkci je vyžadována komerční licence.  
- **Jaká verze Javy je vyžadována?** Java 8+ je podporována; doporučuje se JDK 11+.

## Co je **java boolean and or**?
Dotaz **java boolean and or** kombinuje logické operátory (AND, OR, NOT) pro upřesnění výsledků vyhledávání. Strukturou dotazů řeknete GroupDocs.Search přesně, jak se termíny navzájem vztahují, což vám poskytuje přesnou kontrolu nad procesem získávání.

## Proč používat GroupDocs.Search pro Java?
- **High performance** při práci s velkými sadami dokumentů.  
- **Rich API** podporující jak textové, tak objektové dotazy.  
- **Built‑in language support** pro stemming, stop‑words a fuzzy matching.  
- **Easy integration** s Maven nebo přímým stažením JAR.

## Předpoklady
Předtím, než se ponoříte, ujistěte se, že máte:
- **GroupDocs.Search for Java** (v25.4 nebo novější) – viz odkaz ke stažení níže.  
- JDK 8+ nainstalovaný a nakonfigurovaný ve vašem IDE (IntelliJ IDEA, Eclipse, atd.).  
- Základní znalost Javy a Maven pro správu závislostí.  

## Nastavení GroupDocs.Search pro Java

### Maven nastavení
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

### Přímé stažení
Alternatively, download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Začněte s bezplatnou zkušební licencí pro vyzkoušení všech funkcí. Pro produkční použití zakupte komerční licenci, která odemkne plnou funkcionalitu.

### Základní inicializace a nastavení
Vytvořte složku indexu a vytvořte instanci objektu `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or: Implementace Boolean vyhledávání

Níže pokryjeme dotazy **AND**, **OR**, **NOT** a **complex**. Každá sekce ukazuje jak plain‑text dotaz, tak ekvivalentní objektový dotaz, takže si můžete vybrat styl, který vyhovuje vašemu kódu.

### Boolean AND vyhledávání
Kombinujte termíny pomocí **AND** pro získání pouze dokumentů, které obsahují *vše* klíčová slova.

#### Přehled
AND dotaz zužuje výsledky, zlepšuje relevanci, když potřebujete dokumenty splňující více kritérií.

#### Kroky implementace

1. **Initialize Index** – toto také ukazuje **add documents to index** pro scénář AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – pomocí syntaxe prostého řetězce.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – užitečné při programovém vytváření dotazů (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Boolean OR vyhledávání
Použijte **OR** pro rozšíření výsledků, které odpovídají libovolnému zadanému termínu.

#### Přehled
OR dotaz je ideální pro průzkumná vyhledávání, kde chcete zachytit dokumenty obsahující alespoň jedno z několika klíčových slov (**search with or java**).

#### Kroky implementace

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Boolean NOT vyhledávání
Vyloučte nežádoucí termíny pomocí **NOT**, abyste odfiltrovali šum z výsledků.

#### Přehled
NOT dotaz vám pomůže odstranit irelevantní dokumenty, například filtrováním značky konkurenta (**boolean search examples java**).

#### Kroky implementace

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Komplexní Boolean dotazy
Kombinujte **AND**, **OR** a **NOT** pro vytvoření složité logiky vyhledávání pro vysoce specifické potřeby.

#### Přehled
Komplexní dotazy vám umožní modelovat reálné scénáře vyhledávání, například „najít sportovní články, které jsou pozitivní, ale vyloučit jakékoli zmínky o konkrétních sportovcích“.

#### Kroky implementace

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

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

## Praktické aplikace java boolean and or dotazů
- **Document Management Systems** – najděte smlouvy, které obsahují jak „confidential“, tak **AND** „renewal“.  
- **Legal Research** – filtrujte judikaturu pomocí **AND**/ **OR**, přičemž vylučujete zastaralé zákony pomocí **NOT**.  
- **Customer Support** – načtěte tickety, které zmiňují „login“ **AND** „error“, ale ne „resolved“.  
- **Content Curation** – shromážděte blogové příspěvky o „cloud“ **OR** „serverless“ pro newsletter.

## Časté chyby a řešení problémů
- **Missing Index Refresh** – po přidání nových dokumentů zavolejte `index.update()`, aby byly prohledávatelné.  
- **Incorrect Operator Spacing** – GroupDocs.Search očekává mezery kolem operátorů (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – dotazy jsou ve výchozím nastavení necitlivé na velikost písmen, ale vlastní analyzátory to mohou ovlivnit.  
- **Large Result Sets** – použijte stránkování (`search(query, 0, 100)`) k zabránění přetížení paměti.

## Často kladené otázky

**Q: Můžu kombinovat více než dva termíny v AND dotazu?**  
A: Rozhodně. Můžete řetězit více objektů `createWordQuery` pomocí `createAndQuery`, nebo jednoduše napsat `"term1 AND term2 AND term3"` v textovém dotazu.

**Q: Podporuje GroupDocs.Search vyhledávání s divokými znaky nebo fuzzy vyhledávání?**  
A: Ano. Přidejte `*` pro wildcard (např. `promot*`) nebo použijte `~` pro fuzzy shodu (např. `comfort~`).

**Q: Jak omezím vyhledávání na konkrétní typy souborů?**  
A: Použijte třídu `FileTypeQuery` k omezení výsledků na PDF, DOCX atd., a kombinujte ji s vaším boolean dotazem.

**Q: Jaký je nejlepší způsob, jak sledovat výkon indexování?**  
A: Aktivujte vestavěný logger (`index.getLogger().setLevel(Level.INFO)`) a prohlédněte si časové metriky po každé operaci `add`.

**Q: Existuje způsob, jak zvýšit relevanci určitých termínů?**  
A: Ano. Obalte důležitá slova pomocí `BoostQuery`, aby se zvýšila jejich váha v algoritmu hodnocení.

---

**Poslední aktualizace:** 2026-01-29  
**Testováno s:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs