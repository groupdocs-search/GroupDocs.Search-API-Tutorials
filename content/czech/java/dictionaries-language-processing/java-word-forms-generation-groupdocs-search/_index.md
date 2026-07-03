---
date: '2026-02-21'
description: Naučte se, jak v Javě generovat jednotné a množné tvary pomocí GroupDocs.Search
  API. Vytvořte vlastní poskytovatele tvarů slov pro přesné vyhledávání a analýzu
  textu.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Generujte jednotné a množné tvary v Javě s GroupDocs.Search
type: docs
url: /cs/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

 added Czech description. That's fine.

Check headings: keep same number of #.

Now produce final answer.# Generování singulárních a plurálních tvarů v Javě s GroupDocs.Search

Pokud potřebujete **generovat singulární a plurální tvary v Javě**, je klíčovým prvkem vlastní poskytovatel tvarů slov, který umožní vašemu vyhledávacímu nebo textovému analytickému enginu pochopit každou variantu termínu. V tomto tutoriálu vás provedeme tvorbou takového poskytovatele pomocí GroupDocs.Search Java API, aby vaše aplikace mohla automaticky najít „cat“, „cats“, „city“ a „citis“ bez dalšího úsilí.

## Quick Answers
- **Co dělá poskytovatel tvarů slov?** Generuje alternativní tvary (singulární, plurální atd.) daného slova, aby vyhledávání mohlo odpovídat všem variantám.  
- **Která knihovna je vyžadována?** GroupDocs.Search pro Javu (verze 25.4 nebo novější).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkční nasazení je vyžadována trvalá licence.  
- **Jaká verze Javy je podporována?** JDK 8 nebo vyšší.  
- **Kolik řádků kódu je potřeba?** Přibližně 30 řádků pro jednoduchou implementaci poskytovatele.

## Co je funkce „Create Word Forms Provider“?
Komponenta **create word forms provider** je vlastní třída implementující `IWordFormsProvider`. Přijímá slovo a vrací pole možných tvarů – singulární, plurální nebo jiné jazykové varianty – na základě pravidel, která definujete. To umožňuje indexu vyhledávání považovat „cat“ a „cats“ za ekvivalentní, čímž se zvyšuje úplnost (recall) bez ztráty přesnosti.

## Proč použít GroupDocs.Search pro generování tvarů slov?
- **Vestavěná rozšiřitelnost:** Připojte svůj vlastní poskytovatel přímo do pipeline indexování.  
- **Optimalizováno pro výkon:** Efektivně zpracovává velké indexy a můžete kešovat výsledky pro vyšší rychlost.  
- **Podpora napříč jazyky:** Koncepty platí i pro .NET a další platformy.

## Požadavky
Před implementací **create word forms provider** se ujistěte, že máte:

- **Maven** nainstalovaný a JDK 8 nebo novější nastavený na vašem počítači.  
- Základní znalost vývoje v Javě a konfigurace `pom.xml` v Maven.  
- Přístup ke knihovně GroupDocs.Search pro Javu (verze 25.4 nebo novější).

## Nastavení GroupDocs.Search pro Javu

### Maven konfigurace

Přidejte repozitář a závislost do souboru `pom.xml` přesně tak, jak je uvedeno níže:

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

Alternativně stáhněte nejnovější JAR z oficiální stránky vydání: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Kroky získání licence
1. **Free Trial:** Zaregistrujte se k vyzkoušení, abyste prozkoumali základní funkce.  
2. **Temporary License:** Požádejte o dočasný klíč pro rozšířené testování.  
3. **Purchase:** Získejte komerční licenci pro neomezené používání v produkci.

### Základní inicializace a nastavení

Následující úryvek ukazuje, jak vytvořit index – váš výchozí bod pro přidávání dokumentů a logiky tvarů slov:

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

Níže projdeme kroky k **create word forms provider**, který zpracovává jednoduché transformace singulár‑na‑plurál a plurál‑na‑singulár.

### Implementace SimpleWordFormsProvider

#### Přehled
Náš vlastní poskytovatel bude:

- Odstraní koncové „es“ nebo „s“ pro odhad singulárního tvaru.  
- Změní koncové „y“ na „is“ pro vytvoření plurálního tvaru (např. „city“ → „citis“).  
- Přidá „s“ a „es“ pro generování základních plurálních kandidátů.

#### Krok 1 – Vytvoření kostry třídy

Začněte definováním třídy, která implementuje `IWordFormsProvider`. Importy ponechte beze změny:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Krok 2 – Implementace `getWordForms`

Přidejte metodu, která sestaví seznam možných tvarů. Tento blok obsahuje hlavní logiku; později ji můžete rozšířit o složitější pravidla.

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
- **Singularizace:** Detekuje běžné plurální přípony (`es`, `s`) a odstraňuje je pro aproximaci základního slova.  
- **Pluralizace:** Zpracovává podstatná jména končící na `y` tím, že je nahradí `is`, jednoduché pravidlo fungující pro mnoho anglických slov.  
- **Přidávání přípon:** Přidává `s` a `es` pro pokrytí pravidelných plurálních tvarů, které nemusí být zachyceny předchozími kontrolami.

#### Tipy pro odstraňování problémů
- **Rozlišování velkých a malých písmen:** Metoda používá `toLowerCase()` pro porovnání, což zajišťuje, že „Cats“ a „cats“ se chovají stejně.  
- **Hraniční případy:** Slova kratší než délka přípony jsou ignorována, aby se předešlo vrácení prázdných řetězců.  
- **Výkon:** Pro velké slovníky zvažte kešování výsledků v `ConcurrentHashMap`.

## Praktické aplikace

Implementace **create word forms provider** může podpořit několik reálných scénářů:

1. **Vyhledávače:** Uživatelé zadávající „mouse“ by měli také najít dokumenty obsahující „mice“. Poskytovatel může generovat takové nepravidelné tvary.  
2. **Nástroje pro analýzu textu:** Analýza sentimentu nebo extrakce entit se stává spolehlivější, když jsou rozpoznány všechny varianty slov.  
3. **Systémy pro správu obsahu (CMS):** Automatické generování štítků může zahrnovat plurální synonyma, což zlepšuje SEO a interní prolinkování.

## Úvahy o výkonu

Když vložíte poskytovatele do produkčního systému, mějte na paměti tyto tipy:

- **Kešujte často používané tvary:** Ukládejte výsledky do paměti, abyste se vyhnuli opakovanému přepočítávání stejných slov.  
- **Sledujte haldu JVM:** Velké indexy mohou zvyšovat zatížení paměti; podle toho upravte `-Xmx`.  
- **Používejte efektivní kolekce:** `ArrayList` funguje pro malé sady, ale pro tisíce tvarů zvažte `HashSet` pro rychlé odstranění duplicit.

**Nejlepší postupy**
- Udržujte knihovnu aktuální, abyste získali výkonnostní opravy.  
- Profilujte poskytovatele s realistickým zatížením dotazů, abyste včas odhalili úzká místa.

## Závěr

Nyní jste se naučili, jak **generovat singulární a plurální tvary v Javě** pomocí vlastního `SimpleWordFormsProvider` s GroupDocs.Search. Tato lehká komponenta může výrazně zlepšit relevantnost výsledků vyhledávání a přesnost jazykové analýzy v mnoha aplikacích.

**Další kroky:**  
- Experimentujte s pokročilejšími jazykovými pravidly (nepravidelné plurály, stemming).  
- Integrovat poskytovatele do pipeline indexování a změřit zlepšení recall.  
- Prozkoumejte další funkce GroupDocs.Search, jako jsou slovníky synonym a vlastní analyzátory.

**Výzva k akci:** Vyzkoušejte přidat `SimpleWordFormsProvider` do svého projektu ještě dnes a uvidíte, jak obohacuje vaše vyhledávací zkušenosti!

## Často kladené otázky

**1. Co je GroupDocs.Search pro Javu?**  
Jedná se o výkonnou knihovnu, která nabízí full‑textové vyhledávání, indexování a jazykové funkce – včetně možnosti připojit vlastní poskytovatele tvarů slov.

**2. Jak funguje SimpleWordFormsProvider?**  
Generuje alternativní tvary aplikací jednoduchých pravidel založených na příponách (odstraňuje „s/es“, převádí „y“ na „is“ a přidává „s/es“).

**3. Mohu přizpůsobit pravidla generování tvarů slov?**  
Ano. Upravte metodu `getWordForms`, aby zahrnovala nepravidelné tvary, pravidla specifická pro locale nebo integraci s externími slovníky.

**4. Jaké jsou běžné aplikace této funkce?**  
Vyhledávače, pipeline pro analýzu textu a CMS platformy těží z rozpoznávání singulárních/plurálních variant.

**5. Potřebuji komerční licenci pro produkční použití?**  
Ano – zatímco zkušební verze vám umožní prozkoumat API, zakoupená licence odstraňuje omezení používání a poskytuje podporu.

---

**Poslední aktualizace:** 2026-02-21  
**Testováno s:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs