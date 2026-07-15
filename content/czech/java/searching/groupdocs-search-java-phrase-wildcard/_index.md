---
date: '2026-05-28'
description: Naučte se, jak vyhledávat frázi s vzory obsahujícími divoké znaky pomocí
  GroupDocs.Search pro Java. Zahrnuje vytvoření vyhledávacího indexu, přidání dokumentů
  a provádění dotazů na přesnou frázi i s divokými znaky.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Jak vyhledat frázi s divokými znaky v GroupDocs.Search pro Java
type: docs
url: /cs/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Jak vyhledávat frázi s divokými znaky v GroupDocs.Search pro Java

V moderních aplikacích zaměřených na dokumenty je **vyhledávání fráze** rychle a přesně klíčovým faktorem pro uživatelský zážitek. Ať už budujete znalostní bázi, e‑commerce katalog nebo úložiště řízené shodou, schopnost najít přesnou frázi – nebo její flexibilní variaci – udržuje uživatele produktivní a snižuje zátěž podpory. Tento tutoriál vás provede instalací **GroupDocs.Search for Java**, vytvořením vyhledávacího indexu, načtením dokumentů a spuštěním jak přesných frází, tak dotazů rozšířených o divoké znaky, vše s jasnými, připravenými k produkci ukázkami kódu.

## Rychlé odpovědi
- **Jaký je hlavní přínos vyhledávání frází?** Přesná shoda pořadí slov a blízkosti, zaručující, že jsou vráceny pouze dokumenty obsahující přesnou sekvenci.  
- **Lze v rámci fráze použít divoké znaky?** Ano – divoké znaky vám umožní přeskočit nebo nahradit slova při zachování celkového pořadí.  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro testování; plná licence je vyžadována pro nasazení do produkce.  
- **Kterou verzi Maven použít?** Nejnovější vydání GroupDocs.Search for Java (např. 25.4 v době psaní).  
- **Je tento přístup vhodný pro velké sady dokumentů?** Rozhodně – GroupDocs.Search dokáže zpracovat stovky tisíc dokumentů s podsekundovou latencí dotazů, pokud je index optimalizován.

## Co je „vyhledávání fráze“?
**Vyhledávání fráze znamená hledání konkrétní posloupnosti slov v dokumentu.**  
Když spustíte dotaz na frázi, engine kontroluje, že slova se objevují ve přesném pořadí a v definované blízkosti, čímž eliminuje nerelevantní výsledky, které obsahují stejná slova v jiném kontextu. To činí vyhledávání frází ideálním pro vyhledávání právních klauzulí, kódů produktů nebo jakéhokoli textu, kde je důležité pořadí.

## Proč použít GroupDocs.Search pro dotazy na fráze a divoké znaky?
GroupDocs.Search poskytuje **vysokorychlostní indexování až 1 milionu dokumentů při zachování podsekundových odezvových časů dotazů** na typickém serverovém hardware. Jeho dotazovací jazyk podporuje přesné fráze, jednoduché `*` a `?` divoké znaky a pokročilé vzory jako číselné rozsahy (`*2~5`). Knihovna se integruje s jakoukoliv Java aplikací přes Maven nebo přímé stažení JAR, a běží na Java 8+ bez externích služeb.

## Požadavky
- Java 8 nebo novější (doporučeno Java 11 LTS).  
- Maven 3 nebo novější (pokud dáváte přednost správě závislostí).  
- Základní znalost struktury Java projektu a objektově orientovaných konceptů.  

## Nastavení GroupDocs.Search pro Java

### Použití Maven
Přidejte oficiální repozitář a závislost GroupDocs.Search do vašeho `pom.xml`:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Přímé stažení
Alternativně stáhněte nejnovější JAR z oficiální stránky vydání: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Bezplatná zkušební verze:** Ideální pro rychlé experimenty; omezeno na 100 MB indexovaných dat.  
- **Dočasná licence:** Požádejte o 30‑denní evaluační klíč z portálu GroupDocs.  
- **Plná licence:** Vyžadována pro produkční použití a neomezenou kapacitu indexování.

## Základní inicializace a nastavení
Vytvořte složku, která bude obsahovat soubory indexu, a vytvořte instanci objektu `Index`. Třída `Index` představuje vyhledávatelný index uložený na disku a poskytuje metody pro přidávání, aktualizaci a dotazování dokumentů.

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

Přidejte dokumenty, které chcete zpřístupnit pro vyhledávání:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Jak vyhledávat frázi s divokými znaky v GroupDocs.Search
Tato sekce demonstruje tři úrovně vyhledávání frází – přesná shoda, jednoduchý divoký znak a pokročilé vzory divokých znaků – ukazující, jak vytvořit index, přidat dokumenty a spustit každý typ dotazu pomocí stručného Java kódu. Příklady ilustrují jak textové dotazy, tak konstrukci dotazů na základě objektů, což vývojářům umožňuje integrovat flexibilní vyhledávací schopnosti do svých aplikací.

### Jednoduché vyhledávání fráze

#### Přehled
Použijte tento přístup, když potřebujete **přesnou shodu** posloupnosti slov, například právní klauzuli nebo modelové číslo produktu.

#### Přímá odpověď
Načtěte index, zavolejte `search` s uvozovkovou frází (např. `"quick brown fox"`), a engine vrátí pouze dokumenty obsahující tuto přesnou sekvenci, zachovávající pořadí slov a mezery. Dotaz se provádí v milisekundách, i na indexech obsahujících stovky tisíc souborů.

#### Krok 1: Vytvořit index
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Krok 2: Přidat dokumenty do indexu
```java
Index index = new Index(indexFolder);
```

#### Krok 3: Vyhledat konkrétní frázi (textová forma)
```java
index.add(documentsFolder);
```

#### Krok 4: Dotazy na základě objektu (vyhledat přesnou frázi)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Vyhledávání fráze s divokými znaky

#### Přehled
Zástupné znaky (`*` pro libovolný počet znaků, `?` pro jeden znak) vám umožní **přeskočit proměnlivá slova** při zachování okolního pořadí.

#### Přímá odpověď
Vložte zástupný znak (`*`) uvnitř uvozovkové fráze – např. `"quick * fox"` – pro shodu s libovolným slovem (slovy) mezi *quick* a *fox*. Engine rozšíří divoký znak v čase dotazu, prohledává pouze indexované termíny, které splňují vzor, což udržuje výkon srovnatelný s jednoduchým dotazem na frázi.

#### Krok 1: Vytvořit index
*(Stejné jako u jednoduchého vyhledávání fráze.)*

#### Krok 2: Přidat dokumenty do indexu
*(Stejné jako výše.)*

#### Krok 3: Textové vyhledávání s divokými znaky
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Krok 4: Dotazy na základě objektu s divokými znaky (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Pokročilé vyhledávání divokých znaků

#### Přehled
Kombinujte číselné rozsahy, volitelné znaky a vlastní vzory podobné regexu pro **sofistikované shody**, jako jsou čísla verzí nebo kódy produktů.

#### Přímá odpověď
Použijte rozšířenou syntaxi divokých znaků `*min~max` pro definování rozsahu povolených vzdáleností slov, nebo `?` pro shodu s jedním znakem. Například `"error *2~5 code"` najde slovo *error* následované libovolnými dvěma až pěti slovy a poté *code*. Tato přesnost snižuje falešně pozitivní výsledky a zároveň poskytuje flexibilitu.

#### Krok 1: Vytvořit index
*(Opakováno pro přehlednost.)*

#### Krok 2: Přidat dokumenty do indexu
*(Opakováno.)*

#### Krok 3: Textové vyhledávání s komplexními vzory divokých znaků
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Krok 4: Dotazy na základě objektu s pokročilými divokými znaky
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Praktické aplikace
- **Systémy pro správu obsahu:** Editoři mohou najít přesné klauzule nebo flexibilní úryvky bez ručního procházení stovek stránek.  
- **E‑commerce katalogy:** Nakupující najdou produkty i když vynechají popis nebo použijí synonyma, díky toleranci divokých znaků.  
- **Právo a shoda:** Rychle izolovat smluvní jazyk, který se může v různých dohodách objevit s drobnými odchylkami.  

## Úvahy o výkonu
- **Vytvořit vyhledávací index** jen jednou pro stabilní sadu dokumentů; znovu použijte stejnou instanci `Index` pro všechny dotazy.  
- **Přidávat dokumenty inkrementálně** při příchodu nových souborů – vyhněte se přestavování celého indexu, aby byl nízký odběr CPU.  
- **Navrhněte přesné vzory divokých znaků**; širší vzory (`*`) zvyšují počet rozšíření termínů a mohou zatížit CPU.  
- **Volat `index.optimize()`** periodicky (pokud je podporováno) pro kompaktní index a udržení spotřeby paměti pod kontrolou.  

## Časté problémy a řešení
| Problém | Řešení |
|-------|----------|
| Žádné výsledky pro dotaz s divokým znakem | Ověřte syntaxi divokého znaku (`*min~max`) a ujistěte se, že cílová slova existují v definované vzdálenosti. |
| Index se zastará po aktualizaci souborů | Použijte `index.add(updatedFolder)` nebo API pro inkrementální aktualizaci k obnovení pouze změněných souborů. |
| Vysoká spotřeba paměti u velkých datových sad | Zvyšte JVM haldu (`-Xmx4g` nebo vyšší) a zvažte rozdělení indexu do více shardů pro paralelní zpracování. |

## Často kladené otázky

**Q: Jaký je rozdíl mezi divokým znakem a vyhledáváním fráze?**  
A: Vyhledávání fráze vyžaduje přesné pořadí slov a mezery, zatímco divoký znak vám umožní nahradit nebo přeskočit slova v rámci tohoto pořadí, což poskytuje flexibilní shodu.

**Q: Mohu v dotazech použít divoké znaky s číselnými daty?**  
A: Ano – parametry rozsahu divokých znaků (`*min~max`) fungují i s čísly i se slovy, což umožňuje dotazy jako `"version *1~3"`.

**Q: Jak mám zacházet s velmi velkými kolekcemi dokumentů?**  
A: Udržujte index optimalizovaný, provádějte inkrementální aktualizace a vytvářejte specifické vzory divokých znaků pro omezení rozšíření termínů. GroupDocs.Search může indexovat 1 milion dokumentů při latenci dotazu pod 200 ms na standardním hardware.

**Q: Je GroupDocs.Search vhodný pro scénáře vyhledávání v reálném čase?**  
A: Rozhodně — po vytvoření indexu se dotazy provádějí v milisekundách, což je ideální pro interaktivní vyhledávací pole a funkce automatického doplňování.

**Q: Mohu tuto knihovnu integrovat do existujícího Java projektu?**  
A: Ano. Přidejte Maven závislost nebo JAR, vytvořte instanci `Index` podle ukázky a můžete dotazovat bez úpravy existujícího kódu.

---

**Poslední aktualizace:** 2026-05-28  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

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

## Související tutoriály

- [Vytvořit vyhledávací index Java – GroupDocs.Search tutoriály](/search/java/)
- [Přidat dokumenty do indexu – GroupDocs.Search Java tutoriály](/search/java/document-management/)
- [Vytvořit vyhledávací index - GroupDocs.Search Java tutoriály](/search/java/advanced-features/)