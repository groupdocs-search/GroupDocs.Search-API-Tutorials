---
date: '2026-01-26'
description: Naučte se, jak vyhledávat fráze pomocí vzorů s divokými znaky v GroupDocs.Search
  pro Javu. Tento průvodce pokrývá vytvoření vyhledávacího indexu, přidání dokumentů
  do indexu a provádění vyhledávání s divokými znaky v Javě.
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: Jak vyhledat frázi se zástupnými znaky v GroupDocs.Search Java
type: docs
url: /cs/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Jak vyhledávat frázi s divokými znaky v GroupDocs.Search pro Java

V dnešním rychle se vyvíjejícím světě správy dokumentů může **jak vyhledávat frázi** efektivně rozhodnout o použitelnosti aplikace. Ať už vytváříte systém pro správu obsahu, katalog e‑commerce nebo úložiště právních dokumentů, schopnost najít přesné fráze – nebo jejich flexibilní varianty – je důležitá. V tomto tutoriálu vás provedeme nastavením **GroupDocs.Search pro Java**, vytvořením vyhledávacího indexu, přidáním dokumentů do indexu a ovládnutím jak jednoduchých vyhledávání frází, tak výkonných technik vyhledávání s divokými znaky v Javě.

## Rychlé odpovědi
- **Jaký je hlavní přínos vyhledávání frází?** Přesná shoda pořadí slov a jejich blízkosti.  
- **Lze v rámci fráze použít divoké znaky?** Ano, můžete kombinovat divoké znaky s přesnými slovy pro flexibilní shodu.  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze stačí pro testování; pro produkci je vyžadována plná licence.  
- **Kterou verzi Maven mám použít?** Nejnovější vydání GroupDocs.Search pro Java (např. 25.4 v době psaní).  
- **Je tento přístup vhodný pro velké sady dokumentů?** Rozhodně – stačí udržovat index optimalizovaný a používat cílené vzory divokých znaků.

## Co je “jak vyhledávat frázi”?
Vyhledávání fráze znamená hledání konkrétního pořadí slov v dokumentu. Přidáním divokých znaků umožníte vyhledávači přeskočit nebo nahradit slova, čímž získáte flexibilitu pro shodu variant bez ztráty relevance.

## Proč používat GroupDocs.Search pro dotazy na fráze a divoké znaky?
- **Vysoký výkon** u velkých kolekcí díky optimalizovanému invertovanému indexu.  
- **Bohatý dotazovací jazyk**, který podporuje přesné fráze, jednoduché divoké znaky a pokročilé vzory.  
- **Snadná integrace** s jakoukoliv aplikací založenou na Javě pomocí Maven nebo přímého stažení.  

## Předpoklady
- Nainstalována Java 8 nebo novější.  
- Maven 3 nebo novější (pokud dáváte přednost správě závislostí přes Maven).  
- Základní znalost syntaxe Javy a struktury projektu.  

## Nastavení GroupDocs.Search pro Java

### Použití Maven
Add the repository and dependency to your `pom.xml` file:

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
Alternativně stáhněte nejnovější JAR z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Bezplatná zkušební verze:** Ideální pro rychlé experimenty.  
- **Dočasná licence:** Požádejte přes portál GroupDocs o prodloužené testování.  
- **Plná licence:** Doporučeno pro produkční nasazení.

### Základní inicializace a nastavení
Create a folder for the index and initialize it:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

Add the documents you want to make searchable:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## Jak vyhledávat frázi s divokými znaky v GroupDocs.Search
Níže rozdělujeme tři postupné scénáře: vyhledávání přesné fráze, jednoduché použití divokých znaků a pokročilé vzory divokých znaků.

### Jednoduché vyhledávání fráze

#### Přehled
Použijte, když potřebujete přesnou shodu posloupnosti slov.

##### Krok 1: Vytvoření indexu
```java
Index index = new Index(indexFolder);
```

##### Krok 2: Přidání dokumentů do indexu
```java
index.add(documentsFolder);
```

##### Krok 3: Vyhledání konkrétní fráze (textová forma)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Krok 4: Objektově‑založené dotazy (vyhledání přesné fráze)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Vyhledávání fráze s divokými znaky

#### Přehled
Zástupné znaky vám umožňují přeskočit proměnný počet slov mezi přesnými termíny.

##### Krok 1: Vytvoření indexu
*(Stejné jako kroky v Jednoduchém vyhledávání fráze.)*

##### Krok 2: Přidání dokumentů do indexu
*(Stejné jako výše.)*

##### Krok 3: Textová forma vyhledávání s divokými znaky
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Krok 4: Objektově‑založené dotazy s divokými znaky (Wildcard Search Java)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Pokročilé vyhledávání s divokými znaky

#### Přehled
Kombinujte číselné rozsahy, volitelné znaky a vlastní vzory pro sofistikovanou shodu.

##### Krok 1: Vytvoření indexu
*(Opakováno pro přehlednost.)*

##### Krok 2: Přidání dokumentů do indexu
*(Opakováno.)*

##### Krok 3: Textová forma vyhledávání s komplexními vzory divokých znaků
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### Krok 4: Objektově‑založené dotazy s pokročilými divokými znaky
```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Praktické aplikace
- **Systémy pro správu obsahu:** Umožňují editorům najít přesné klauzule nebo flexibilní úryvky.  
- **Katalogy e‑commerce:** Umožňují zákazníkům najít produkty i při chybějícím slově nebo použití synonym.  
- **Právní a compliance:** Rychle izoluje smluvní jazyk, který se může objevit s drobnými odchylkami.

## Úvahy o výkonu
- **Vytvořte vyhledávací index** jen jednou pro sadu dokumentů a poté jej znovu použijte.  
- **Přidávejte dokumenty do indexu** inkrementálně, když přicházejí nové soubory – nebudujte celý index znovu při každé změně.  
- Používejte **přesné vzory divokých znaků**, aby se předešlo zbytečnému skenování; širší vzory zvyšují zatížení CPU.  
- Periodicky zavolejte `index.optimize()` (pokud je k dispozici), aby se udržovala nízká spotřeba paměti.

## Časté problémy a řešení
| Problém | Řešení |
|-------|----------|
| Žádné výsledky pro dotaz s divokým znakem | Ověřte syntaxi divokého znaku (`*min~~max`) a ujistěte se, že slova existují v určené vzdálenosti. |
| Index se po aktualizaci souborů zastará | Znovu spusťte `index.add(updatedFolder)` nebo použijte API pro inkrementální aktualizaci. |
| Vysoká spotřeba paměti u velkých datových sad | Zvyšte velikost haldy JVM a zvažte rozdělení indexu do více shardů. |

## Často kladené otázky

**Q: Jaký je rozdíl mezi divokým znakem a vyhledáváním fráze?**  
A: Vyhledávání fráze hledá přesné pořadí slov, zatímco divoký znak vám umožňuje nahradit nebo přeskočit slova v tomto pořadí.

**Q: Mohu v dotazech používat divoké znaky s číselnými daty?**  
A: Ano, parametry rozsahu divokých znaků fungují jak s čísly, tak se slovy.

**Q: Jak mám zacházet s velmi velkými kolekcemi dokumentů?**  
A: Udržujte index optimalizovaný, používejte inkrementální aktualizace a navrhujte vzory divokých znaků co nejkonkrétněji.

**Q: Je GroupDocs.Search vhodný pro scénáře vyhledávání v reálném čase?**  
A: Rozhodně – jakmile je index vytvořen, dotazy se provádějí v milisekundách, což jej činí vhodným pro interaktivní aplikace.

**Q: Můžu tuto knihovnu integrovat do existujícího Java projektu?**  
A: Ano. Přidejte Maven závislost nebo JAR, inicializujte index podle ukázky a můžete začít.

---

**Poslední aktualizace:** 2026-01-26  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs