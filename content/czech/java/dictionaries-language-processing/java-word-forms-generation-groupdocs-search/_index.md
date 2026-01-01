---
date: '2025-12-20'
description: Naučte se, jak vytvořit poskytovatele tvarů slov v Javě s GroupDocs.Search.
  Generujte jednotné a množné tvary pro vyhledávání, analýzu textu a další.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Vytvořte poskytovatele tvarů slov v Javě pomocí GroupDocs.Search API
type: docs
url: /cs/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Vytvoření poskytovatele tvarů slov v Javě pomocí GroupDocs.Search API

Převod slov z jednotného čísla na množné — nebo naopak — je častou překážkou při tvorbě aplikací citlivých na jazyk. V tomto průvodci **vytvoříte poskytovatele tvarů slov** pomocí GroupDocs.Search Java API, což vašemu vyhledávači nebo nástroji pro analýzu textu umožní automaticky rozpoznávat a porovnávat různé varianty slov.

Ať už vyvíjíte vyhledávač, systém pro správu obsahu nebo jakoukoli Java aplikaci, která zpracovává přirozený jazyk, zvládnutí generování tvarů slov učiní vaše výsledky přesnějšími a uživatele spokojenějšími. Pojďme si prozkoumat předpoklady potřebné před zahájením.

## Rychlé odpovědi
- **Co dělá poskytovatel tvarů slov?** Vytváří alternativní tvary (jednotné, množné atd.) daného slova, aby vyhledávání mohlo odpovídat všem variantám.  
- **Která knihovna je vyžadována?** GroupDocs.Search pro Java (verze 25.4 nebo novější).  
- **Potřebuji licenci?** Bezplatná zkušební verze stačí pro hodnocení; pro produkční nasazení je vyžadována trvalá licence.  
- **Jaká verze Javy je podporována?** JDK 8 nebo vyšší.  
- **Kolik řádků kódu je potřeba?** Přibližně 30 řádků pro jednoduchou implementaci poskytovatele.

## Co je funkce „Vytvořit poskytovatele tvarů slov“?
Komponenta **vytvořit poskytovatele tvarů slov** je vlastní třída implementující `IWordFormsProvider`. Přijímá slovo a vrací pole možných tvarů — jednotné, množné nebo jiné jazykové varianty — na základě pravidel, která definujete. To umožňuje indexu vyhledávání považovat „cat“ a „cats“ za ekvivalentní, čímž se zvyšuje úplnost bez ztráty přesnosti.

## Proč použít GroupDocs.Search pro generování tvarů slov?
- **Vestavěná rozšiřitelnost:** Můžete přímo zapojit svůj vlastní poskytovatel do pipeline indexování.  
- **Optimalizovaný výkon:** Knihovna efektivně pracuje s velkými indexy a můžete ke zvýšení rychlosti kešovat výsledky.  
- **Podpora více jazyků:** I když se tento tutoriál zaměřuje na Javu, stejné koncepty platí pro .NET a další platformy.

## Předpoklady
Před implementací **vytvořit poskytovatele tvarů slov** se ujistěte, že máte:

- **Maven** nainstalovaný a JDK 8 nebo novější nastavené na vašem počítači.  
- Základní znalost vývoje v Javě a konfigurace `pom.xml` v Maven.  
- Přístup ke knihovně GroupDocs.Search pro Java (verze 25.4 nebo novější).  

## Nastavení GroupDocs.Search pro Javu

### Maven konfigurace
Add the repository and dependency to your `pom.xml` file exactly as shown below:

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
Alternatively, download the latest JAR from the official releases page: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Kroky získání licence
To use GroupDocs.Search without limitations:

1. **Free Trial:** Zaregistrujte se na zkušební verzi a vyzkoušejte hlavní funkce.  
2. **Temporary License:** Požádejte o dočasný klíč pro rozšířené testování.  
3. **Purchase:** Získejte komerční licenci pro neomezené používání v produkci.

### Základní inicializace a nastavení
The following snippet demonstrates how to create an index—your starting point for adding documents and word‑form logic:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Průvodce implementací

Below we walk through the steps to **create word forms provider** that handles simple singular‑to‑plural and plural‑to‑singular transformations.

### Implementace SimpleWordFormsProvider

#### Přehled
Our custom provider will:

- Odstraní koncové „es“ nebo „s“ pro odhad jednotného tvaru.  
- Změní koncové „y“ na „is“ pro vytvoření množného tvaru (např. „city“ → „citis“).  
- Přidá „s“ a „es“ pro vytvoření základních množných kandidátů.

#### Krok 1 – Vytvoření kostry třídy
Start by defining a class that implements `IWordFormsProvider`. Keep the import statements unchanged:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Krok 2 – Implementace `getWordForms`
Add the method that builds the list of possible forms. This block contains the core logic; you can extend it later to cover more complex rules.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Vysvětlení logiky
- **Singularizace:** Detekuje běžné množné koncovky (`es`, `s`) a odstraňuje je pro odhad základního slova.  
- **Pluralizace:** Zpracovává podstatná jména končící na `y` výměnou za `is`, jednoduché pravidlo fungující pro mnoho anglických slov.  
- **Přidávání koncovek:** Přidává `s` a `es` pro pokrytí pravidelných množných tvarů, které nemusí být zachyceny předchozími kontrolami.

#### Tipy pro odstraňování problémů
- **Rozlišování velikosti písmen:** Metoda používá `toLowerCase()` pro porovnání, což zajišťuje, že „Cats“ i „cats“ se chovají stejně.  
- **Hraniční případy:** Slova kratší než délka koncovky jsou ignorována, aby se předešlo vrácení prázdných řetězců.  
- **Výkon:** Pro velké slovníky zvažte kešování výsledků v `ConcurrentHashMap`.

## Praktické aplikace
Implementing a **create word forms provider** can boost several real‑world scenarios:

1. **Vyhledávače:** Uživatelé zadávající „mouse“ by měli také najít dokumenty obsahující „mice“. Poskytovatel může generovat takové nepravidelné tvary.  
2. **Nástroje pro analýzu textu:** Analýza sentimentu nebo extrakce entit je spolehlivější, když jsou rozpoznány všechny varianty slov.  
3. **Systémy pro správu obsahu:** Automatické generování štítků může zahrnovat množné synonyma, což zlepšuje SEO a interní propojení.

## Úvahy o výkonu
When you embed the provider into a production system, keep these tips in mind:

- **Kešovat často používané tvary:** Ukládejte výsledky do paměti, abyste se vyhnuli opakovanému přepočítávání stejných slov.  
- **Sledovat haldu JVM:** Velké indexy mohou zvyšovat zatížení paměti; podle toho upravte `-Xmx`.  
- **Používat efektivní kolekce:** `ArrayList` funguje pro malé sady, ale pro tisíce tvarů zvažte `HashSet` pro rychlé odstranění duplicit.

**Nejlepší postupy**
- Udržujte knihovnu aktuální, abyste získali výkonnostní opravy.  
- Profilujte poskytovatele s realistickým zatížením dotazů, abyste včas odhalili úzká místa.

## Závěr
You’ve now learned how to **create word forms provider** using GroupDocs.Search for Java. This lightweight component can dramatically improve the relevance of search results and the accuracy of linguistic analysis across many applications.

**Next steps:**  
- Experimentujte s pokročilejšími jazykovými pravidly (nepravidelné množné, stemming).  
- Integrovat poskytovatele do pipeline indexování a změřit zlepšení úplnosti.  
- Prozkoumat další funkce GroupDocs.Search, jako jsou slovníky synonym a vlastní analyzátory.

**Call to Action:** Try adding the `SimpleWordFormsProvider` to your own project today and see how it enriches your search experience!

## Často kladené otázky

**1. Co je GroupDocs.Search pro Java?**  
Jedná se o výkonnou knihovnu, která poskytuje full‑textové vyhledávání, indexování a jazykové funkce — včetně možnosti zapojit vlastní poskytovatele tvarů slov.

**2. Jak funguje SimpleWordFormsProvider?**  
Generuje alternativní tvary aplikací jednoduchých pravidel založených na koncovkách (odstraňuje „s/es“, převádí „y“ na „is“ a přidává „s/es“).

**3. Mohu přizpůsobit pravidla generování tvarů slov?**  
Ano. Upravit metodu `getWordForms` tak, aby zahrnovala nepravidelné tvary, pravidla specifická pro locale nebo integraci s externími slovníky.

**4. Jaké jsou běžné aplikace této funkce?**  
Vyhledávače, pipeline pro analýzu textu a CMS platformy těží z rozpoznávání jednotných/množných variant.

**5. Potřebuji komerční licenci pro produkční použití?**  
Ano — zatímco zkušební verze vám umožní prozkoumat API, zakoupená licence odstraňuje omezení používání a poskytuje podporu.

---

**Poslední aktualizace:** 2025-12-20  
**Testováno s:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs