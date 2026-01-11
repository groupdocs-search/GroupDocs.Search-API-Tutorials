---
date: '2026-01-11'
description: Naučte se, jak vytvořit vlastní vyhledávací index pomocí GroupDocs.Search
  pro Javu, konfigurací běžných a kombinovaných znaků pro pokročilé OCR a vyhledávání
  obrázků.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Vytvořte vlastní vyhledávací index s rozpoznáváním znaků – GroupDocs.Search
  Java
type: docs
url: /cs/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Vytvoření vlastního vyhledávacího indexu s rozpoznáváním znaků pomocí GroupDocs.Search pro Java

V moderních aplikacích pracujících s velkým množstvím dokumentů je **vytvoření vlastního vyhledávacího indexu**, který rozumí nuancím vašeho textu – například spojovníkům, podtržítkům nebo jazykově specifickým symbolům – nezbytné pro rychlé a přesné vyhledávání. Tento tutoriál vás provede nastavením rozpoznávání znaků v **GroupDocs.Search pro Java**, pokrývající jak běžné znaky (písmena, číslice, podtržítka), tak i spojené znaky (ř. spojovníky). Na konci budete schopni přizpůsobit index tak, aby přesně vyhovoval vašim potřebám OCR nebo vyhledávání obrázků.

## Rychlé odpovědi
- **Co znamená „vytvořit vlastní vyhledávací index“?** Znamená to nakonfigurovat index tak, aby určité symboly považoval za písmena nebo spojené znaky, místo aby je ignoroval.  
- **Která knihovna se používá?** GroupDocs.Search pro Java (v25.4 v době psaní).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována placená licence.  
- **Mohu indexovat jak PDF, tak i obrázky?** Ano – GroupDocs.Search podporuje OCR na obrázcích i PDF, pokud je správně nakonfigurován.  
- **Je Maven povinný?** Maven je doporučený způsob správy závislostí, ale můžete také použít Gradle nebo ruční JAR soubory.

## Co je vlastní vyhledávací index?
Vlastní vyhledávací index vám umožňuje definovat, jak vyhledávací engine interpretuje znaky. Ve výchozím nastavení jsou mnohé symboly ignorovány, což může vést k neúspěšným shodám u např. čísel spisů (`ABC-123`) nebo úryvků kódu (`my_variable`). Úprava slovníku abecedy vám dává plnou kontrolu nad tím, co engine považuje za prohledávatelný text.

## Proč konfigurovat běžné a spojené znaky?
- **Běžné znaky** (písmena, číslice, podtržítka) jsou považovány za samostatné tokeny, což zlepšuje vyhledávání přesných shod.  
- **Spojené znaky** (spojovníky, lomítka) spojují slova; jejich konfigurace zabraňuje nechtěnému rozdělení tokenů, což je klíčové pro právní odkazy, kódy produktů nebo indexování zdrojového kódu.

## Předpoklady
- **JDK 8** nebo novější nainstalováno.  
- **Maven** pro správu závislostí.  
- Přístup ke knihovně **GroupDocs.Search pro Java** (stažené přes Maven nebo oficiální web).  

### Požadované knihovny a závislosti
Přidejte záznamy repozitáře a závislosti do vašeho `pom.xml` (jak je ukázáno níže). XML blok musí zůstat nezměněn.

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

Můžete také stáhnout nejnovější JAR soubory z [vydání GroupDocs.Search pro Java](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Bezplatná zkušební verze** – ideální pro první experimenty.  
- **Dočasná licence** – užitečná pro delší vývojové cykly.  
- **Produkční licence** – vyžadována pro komerční nasazení.  

Získejte licenci z oficiálního portálu: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Základní inicializace
Níže uvedený úryvek ukazuje minimální kód potřebný k vytvoření prázdného indexu. Nechte jej beze změny; později na něj navážeme.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Nastavení GroupDocs.Search pro Java

### Instalace pomocí Maven
Maven konfigurace ze sekce *Předpoklady* je vše, co potřebujete. Po jejím přidání spusťte `mvn clean install` pro stažení binárek.

### Požadavky na nastavení prostředí
- Ujistěte se, že **složka indexu** a **složka dokumentů** existují na disku.  
- Používejte absolutní cesty nebo nakonfigurujte své IDE tak, aby správně řešilo relativní cesty.

## Průvodce implementací

Níže projdeme dvě odlišné funkce: **běžné znaky** a **spojené znaky**. Každá funkce následuje stejný vzor – definujte cesty, vytvořte index, nastavte slovník znaků a nakonec indexujte své dokumenty.

### Funkce 1 – Běžné znaky

#### Přehled
Běžné znaky jsou považovány za nezávislé tokeny. To je ideální, když chcete, aby číslice, písmena a podtržítka byly prohledávatelné přesně tak, jak se objeví.

#### Implementace krok za krokem

**1️⃣ Nastavení cest**  
Definujte, kde bude index uložen a kde se nacházejí vaše zdrojové dokumenty.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Vytvoření a konfigurace indexu**  
Vytvořte instanci indexu a vymažte jakoukoli předchozí konfiguraci abecedy.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definice běžných znaků**  
Sestavte pole znaků, které zahrnuje číslice, latinská písmena a podtržítko.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Indexování dokumentů**  
Přidejte všechny soubory ze zdrojové složky do nově nakonfigurovaného indexu.

```java
index.add(documentFolder);
```

### Funkce 2 – Spojené znaky

#### Přehled
Spojené znaky (např. spojovníky) často spojují dvě slova. Označení je jako *spojené* říká engine, aby během indexování udržel okolní tokeny pohromadě.

#### Implementace krok za krokem

**1️⃣ Nastavení cest**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Vytvoření a konfigurace indexu**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definice spojených znaků**  
Zde říkáme slovníku, že spojovník by měl být považován za spojený znak.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexování dokumentů**  

```java
index.add(documentFolder);
```

## Praktické aplikace

### Případ použití 1 – Správa právních dokumentů
Právní soubory často obsahují čísla spisů jako `2023-AB-456`. Konfigurací podtržítek a spojovníků vyhledávání vrací přesné shody, aniž by identifikátor rozdělovalo.

### Případ použití 2 – Repozitáře zdrojového kódu
Vývojáři potřebují vyhledávat úryvky kódu, kde jsou podtržítka (`my_variable`) a spojovníky (`my-function`) významné. Vlastní rozpoznávání znaků zajišťuje, že vyhledávací engine respektuje tyto symboly.

### Případ použití 3 – Vícejazyčné datové sady
Při práci s jazyky, které používají další abecedy, můžete rozšířit sadu běžných znaků o tyto Unicode rozsahy, což zaručuje přesné výsledky vyhledávání napříč jazyky.

## Úvahy o výkonu

- **Správa zdrojů** – Sledujte využití haldy; velké indexy těží z inkrementálních commitů.  
- **Garbage Collection** – Uvolněte objekty `Index`, když jsou hotové, aby JVM mohl uvolnit paměť.  
- **Optimalizace indexu** – Periodicky zavolejte `index.optimize()` (pokud je k dispozici) pro kompakci indexu a zrychlení dotazů.  

## Závěr

Nyní víte, jak **vytvořit vlastní vyhledávací index**, který rozlišuje mezi běžnými a spojenými znaky pomocí GroupDocs.Search pro Java. Tato jemná kontrola vám umožní vytvářet OCR‑vědomá, výkonná vyhledávací řešení přizpůsobená právnímu, vývojářskému nebo vícejazyčnému prostředí.

**Další kroky**  
- Experimentujte s dalšími Unicode rozsahy pro ne‑latinské abecedy.  
- Kombinujte konfiguraci znaků s dalšími funkcemi GroupDocs.Search, jako je stemming nebo synonymum.  
- Integrovat index do REST API pro zpřístupnění vyhledávacích možností front‑end aplikacím.

## Často kladené otázky

**Q:** *Jaký je účel `CharacterType.Letter`?*  
**A:** Říká indexu, aby považoval dodané znaky za běžná písmena, takže jsou během indexování tokenizovány samostatně.

**Q:** *Mohu v jednom indexu kombinovat běžné i spojené znaky?*  
**A:** Ano – stačí zavolat `setRange` pro každý typ; slovník bude obě konfigurace zpracovávat současně.

**Q:** *Musím po změně abecedy znovu vytvořit index?*  
**A:** Rozhodně. Změny ve slovníku znaků ovlivňují tokenizaci, takže musíte dokumenty znovu indexovat, aby se nová pravidla uplatnila.

**Q:** *Existuje limit na počet vlastních znaků, které mohu definovat?*  
**A:** Knihovna podporuje celý Unicode rozsah; výkon může klesat, pokud přidáte extrémně velkou sadu, proto omezte na znaky, které skutečně potřebujete.

**Q:** *Jak to ovlivňuje přesnost OCR?*  
**A:** Přizpůsobením znakové sady indexu výstupu OCR motoru snižujete počet falešných negativ a zlepšujete celkovou relevanci vyhledávání.

---

**Last Updated:** 2026-01-11  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---