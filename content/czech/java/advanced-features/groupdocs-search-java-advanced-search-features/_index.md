---
date: '2025-12-16'
description: Naučte se, jak provádět vyhledávání v rozmezí dat a další pokročilé funkce
  vyhledávání, jako je faceted vyhledávání v Javě, pomocí GroupDocs.Search pro Javu,
  včetně zpracování chyb a optimalizace výkonu.
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: 'GroupDocs.Search Java: Vyhledávání v rozmezí dat a pokročilé funkce'
type: docs
url: /cs/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

# Ovládání GroupDocs.Search Java: Vyhledávání v časovém rozmezí a Pokročilé funkce

V dnešních aplikacích řízených daty je **date range search** základní schopností, která vám umožňuje filtrovat dokumenty podle časových období, což výrazně zvyšuje relevance a rychlost. Ať už vytváříte portál pro soulad, e‑commerce katalog nebo systém pro správu obsahu, ovládání date range search spolu s dalšími výkonnými typy dotazů učiní vaše řešení flexibilním a robustním. Tento průvodce vás provede zpracováním chyb, kompletní sadou typů dotazů a tipy na výkon, vše s reálným Java kódem, který můžete zkopírovat a vložit.

## Rychlé odpovědi
- **What is date range search?** Filtrování dokumentů, které obsahují data v určeném intervalu od začátku do konce.  
- **Which library provides it?** GroupDocs.Search for Java.  
- **Do I need a license?** Bezplatná zkušební verze funguje pro vývoj; pro komerční použití je vyžadována produkční licence.  
- **Can I combine it with other queries?** Ano — kombinujte date range search s boolean, faceted nebo regex dotazy.  
- **Is it fast for large datasets?** Ano, pokud je indexováno správně, vyhledávání probíhá v podsekundovém čase i u milionů záznamů.

## Co je date range search?
Date range search vám umožňuje najít dokumenty, které obsahují data spadající mezi dvěma hranicemi, například „2023‑01‑01 ~~ 2023‑12‑31“. Je nezbytný pro zprávy, auditní logy a jakýkoli scénář, kde je důležité časové filtrování.

## Proč používat GroupDocs.Search pro Java?
GroupDocs.Search poskytuje jednotné API pro mnoho typů dotazů — simple, wildcard, faceted, numeric, date range, regex, boolean a phrase — takže můžete vytvářet sofistikované vyhledávací zážitky bez nutnosti používat více knihoven. Jeho událostmi řízené zpracování chyb také udržuje váš indexovací pipeline odolný.

## Předpoklady
- **GroupDocs.Search Java library** (v25.4 nebo novější).  
- **Java Development Kit (JDK)** kompatibilní s vaším projektem.  
- Maven pro správu závislostí (nebo ruční stažení).  

### Požadované knihovny a nastavení prostředí
Přidejte repository GroupDocs a závislost do vašeho `pom.xml`:

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

### Alternativní nastavení
Pro přímé stažení navštivte [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licencování a počáteční nastavení
Začněte s bezplatnou zkušební verzí nebo dočasnou licencí:

- Navštivte [GroupDocs License Options](https://purchase.groupdocs.com/temporary-license/) pro podrobnosti.

Nyní vytvořme složku indexu, která bude obsahovat vaše prohledávatelná data.

## Nastavení GroupDocs.Search pro Java

### Základní inicializace
Nejprve vytvořte objekt `Index`, který ukazuje na složku na disku:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

Nyní máte bránu ke všem vyhledávacím operacím.

## Průvodce implementací

### Funkce 1: Zpracování chyb při indexování
#### Jak zachytit chyby při indexování (Java)

```java
import com.groupdocs.search.events.*;

index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
    @Override
    public void invoke(Object sender, IndexErrorEventArgs args) {
        System.out.println(args.getMessage()); // Output the error message
    }
});

// Add documents to the index
index.add("YOUR_DOCUMENT_DIRECTORY");
```

*Proč je to důležité*: Posloucháním události `ErrorOccurred` můžete zaznamenávat problémy, znovu zkusit neúspěšné soubory nebo upozornit uživatele, aniž by došlo k pádu celého procesu.

### Funkce 2: Jednoduchý vyhledávací dotaz
#### Co je jednoduché vyhledávání?

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*Výsledek*: Vrátí každý dokument obsahující termín **volutpat**.

### Funkce 3: Vyhledávání s divokou kartou
#### Jak funguje vyhledávání s divokou kartou?

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*Výsledek*: Odpovídá jak **affect**, tak **effect**, což ukazuje sílu zástupného znaku `?`.

### Funkce 4: Facetované vyhledávání
#### Jak provést faceted search v Java

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*Výsledek*: Omezuje vyhledávání na pole **Content**, ideální pro filtrování podle metadat, jako je kategorie nebo autor.

### Funkce 5: Vyhledávání číselného rozsahu
#### Jak vyhledávat číselné rozsahy

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*Výsledek*: Získá dokumenty, kde číselné hodnoty spadají mezi 2000 a 3000.

### Funkce 6: Vyhledávání v časovém rozmezí
#### Jak provést date range search

```java
import com.groupdocs.search.options.*;
import java.util.*;

String query = "daterange(2000-01-01 ~~ 2001-06-15)";
SearchOptions options = new SearchOptions();

options.getDateFormats().clear();
DateFormatElement[] elements = {
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

SearchResult result = index.search(query, options);
```

*Vysvětlení*: Přizpůsobením `SearchOptions` řeknete enginu, aby rozpoznával data ve formátu **MM/DD/YYYY**, a poté získá všechny záznamy mezi 1. lednem 2000 a 15. červnem 2001.

### Funkce 7: Vyhledávání regulárním výrazem
#### Jak spustit regex search v Java

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*Výsledek*: Najde sekvence tří nebo více stejných znaků (např. „aaa“, „111“).

### Funkce 8: Boolean vyhledávání
#### Jak kombinovat podmínky pomocí boolean search v Java

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*Výsledek*: Vrátí dokumenty obsahující **justo**, ale vyloučí všechny, které také obsahují **3456**.

### Funkce 9: Komplexní Boolean vyhledávání
#### Jak vytvořit pokročilé boolean dotazy

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*Výsledek*: Hledá názvy souborů podobné „English“ (s 1‑3 znakovými odchylkami) **nebo** obsah, který obsahuje jak **3456**, tak **consequat**.

### Funkce 10: Vyhledávání fráze
#### Jak vyhledávat přesné fráze

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*Výsledek*: Vrátí pouze dokumenty, které obsahují přesnou frázi **ipsum dolor sit amet**.

## Praktické aplikace
1. **E‑commerce Platforms** – Použijte faceted search v Java k filtrování produktů podle velikosti, barvy a značky.  
2. **Content Management Systems** – Kombinujte boolean search v Java s vyhledáváním frází pro pokročilé editační nástroje.  
3. **Data Analysis Tools** – Využijte date range search k tvorbě časově orientovaných zpráv a dashboardů.

## Časté problémy a řešení
- **No results for date range search** – Ověřte, že formát data ve vašich dokumentech odpovídá vlastnímu `DateFormat`, který jste přidali.  
- **Regex queries return too many hits** – Upřesněte vzor nebo omezte rozsah vyhledávání pomocí dalších specifikátorů pole.  
- **Indexing errors not captured** – Ujistěte se, že je obslužná rutina události připojena **před** voláním `index.add(...)`.

## Často kladené otázky

**Q: Mohu kombinovat date range search s jinými typy dotazů?**  
A: Ano. Můžete kombinovat klauzuli date range search s boolean operátory, faceted filtry nebo regex vzory v jednom dotazovém řetězci.

**Q: Musím přestavět index po změně formátů dat?**  
A: Ano. Index ukládá tokenizované termíny; pouhá aktualizace `SearchOptions` neprovádí re-tokenizaci existujících dat. Po změně formátů je nutné dokumenty znovu indexovat.

**Q: Jak GroupDocs.Search zachází s velkými indexy?**  
A: Používá inkrementální indexování a úložiště na disku, což vám umožní škálovat na miliony dokumentů při nízké spotřebě paměti.

**Q: Existuje limit na počet znaků wildcard?**  
A: Wildcardy jsou zpracovávány efektivně, ale použití mnoha úvodních wildcardů (např. `*term`) může snížit výkon. Upřednostněte prefixové nebo suffixové wildcardy.

**Q: Jaký licenční model se doporučuje pro produkci?**  
A: Perpetuální nebo předplatitelská licence od GroupDocs vám zajišťuje aktualizace, podporu a možnost nasazení bez omezení zkušební verze.

## Závěr
Ovládnutím **date range search** a celé sady pokročilých typů dotazů nabízených GroupDocs.Search pro Java můžete vytvořit vysoce responzivní, funkčně bohaté vyhledávací zážitky. Implementujte robustní zpracování chyb, dolaďte svůj index a kombinujte dotazy tak, aby vyhovovaly prakticky jakémukoli scénáři vyhledávání. Začněte dnes experimentovat a posuňte schopnosti přístupu k datům vaší aplikace na vyšší úroveň.

---

**Poslední aktualizace:** 2025-12-16  
**Testováno s:** GroupDocs.Search 25.4 (Java)  
**Autor:** GroupDocs