---
date: '2026-02-21'
description: Lär dig hur du genererar singular‑ och pluralformer i Java med GroupDocs.Search
  API. Skapa en anpassad leverantör av ordformer för exakt sökning och textanalys.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Generera singular‑pluralformer i Java med GroupDocs.Search
type: docs
url: /sv/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Generera singular‑pluralformer i Java med GroupDocs.Search

Om du behöver **generera singular‑pluralformer i Java**, är en anpassad word‑forms‑provider nyckeln till att få din sök‑ eller textanalys‑motor att förstå varje variation av ett begrepp. I den här handledningen går vi igenom hur du bygger en sådan provider med GroupDocs.Search Java‑API, så att din applikation automatiskt kan matcha “cat”, “cats”, “city” och “citis” utan extra ansträngning.

## Snabba svar
- **Vad gör en word forms provider?** Den genererar alternativa former (singular, plural osv.) av ett givet ord så att sökningar kan matcha alla varianter.  
- **Vilket bibliotek krävs?** GroupDocs.Search for Java (version 25.4 or newer).  
- **Behöver jag en licens?** En gratis provperiod fungerar för utvärdering; en permanent licens krävs för produktion.  
- **Vilken Java‑version stöds?** JDK 8 or higher.  
- **Hur många kodrader behövs?** Ungefär 30 lines for a simple provider implementation.

## Vad är en “Create Word Forms Provider”-funktion?
En **create word forms provider**‑komponent är en anpassad klass som implementerar `IWordFormsProvider`. Den tar emot ett ord och returnerar en array av möjliga former — singular, plural eller andra språkliga variationer — baserat på regler du definierar. Detta gör att sökindexet behandlar “cat” och “cats” som ekvivalenta, vilket förbättrar återkallning utan att offra precision.

## Varför använda GroupDocs.Search för word‑form‑generering?
- **Inbyggd extensibilitet:** Anslut din egen provider direkt i indexerings‑pipeline.  
- **Prestandaoptimerad:** Hanterar stora index effektivt, och du kan cache‑lagra resultat för extra hastighet.  
- **Stöd för flera språk:** Koncepten gäller även för .NET och andra plattformar.

## Förutsättningar
Innan du implementerar **create word forms provider**, se till att du har:

- **Maven** installerat och en JDK 8 eller nyare konfigurerad på din maskin.  
- Grundläggande kunskap om Java‑utveckling och Maven‑konfigurationen `pom.xml`.  
- Tillgång till GroupDocs.Search Java‑biblioteket (version 25.4 eller senare).  

## Konfigurera GroupDocs.Search för Java

### Maven‑konfiguration
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

### Direktnedladdning
Alternativt, ladda ner den senaste JAR‑filen från den officiella releases‑sidan: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Steg för att skaffa licens
1. **Free Trial:** Registrera dig för en provperiod för att utforska huvudfunktionerna.  
2. **Temporary License:** Begär en tillfällig nyckel för utökad testning.  
3. **Purchase:** Skaffa en kommersiell licens för obegränsad produktionsanvändning.

### Grundläggande initiering och konfiguration
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

## Implementationsguide
Nedan går vi igenom stegen för att **create word forms provider** som hanterar enkla singular‑till‑plural och plural‑till‑singular‑omvandlingar.

### Implementering av SimpleWordFormsProvider
#### Översikt
Our custom provider will:

- Ta bort avslutande “es” eller “s” för att gissa en singularform.  
- Ändra ett avslutande “y” till “is” för att skapa en pluralform (t.ex. “city” → “citis”).  
- Lägg till “s” och “es” för att generera grundläggande plural‑kandidater.

#### Steg 1 – Skapa klass‑skelettet
Start by defining a class that implements `IWordFormsProvider`. Keep the import statements unchanged:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Steg 2 – Implementera `getWordForms`
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

#### Förklaring av logiken
- **Singularisering:** Upptäcker vanliga plural‑suffix (`es`, `s`) och tar bort dem för att approximera grundordet.  
- **Pluralisering:** Hanterar substantiv som slutar på `y` genom att byta ut det mot `is`, en enkel regel som fungerar för många engelska ord.  
- **Suffix‑tillägg:** Lägger till `s` och `es` för att täcka vanliga pluralformer som kanske inte fångas av de tidigare kontrollerna.

#### Felsökningstips
- **Skiftlägeskänslighet:** Metoden använder `toLowerCase()` för jämförelse, vilket säkerställer att “Cats” och “cats” beter sig likadant.  
- **Edge Cases:** Ord kortare än suffixets längd ignoreras för att undvika att returnera tomma strängar.  
- **Prestanda:** För stora vokabulärer, överväg att cache‑lagra resultat i en `ConcurrentHashMap`.

## Praktiska tillämpningar
Att implementera en **create word forms provider** kan förbättra flera verkliga scenarier:

1. **Sökmotorer:** Användare som skriver “mouse” bör också hitta dokument som innehåller “mice”. En provider kan generera sådana oregelbundna former.  
2. **Textanalysverktyg:** Sentiment‑ eller entitetsutvinning blir mer pålitlig när alla ordvarianter känns igen.  
3. **Content Management Systems:** Automatisk tag‑generering kan inkludera plural‑synonymer, vilket förbättrar SEO och intern länkning.

## Prestandaöverväganden
När du integrerar providern i ett produktionssystem, ha dessa tips i åtanke:

- **Cachea ofta använda former:** Lagra resultat i minnet för att undvika att beräkna samma ord upprepade gånger.  
- **Övervaka JVM‑heap:** Stora index kan öka minnesbelastningen; justera `-Xmx` därefter.  
- **Använd effektiva samlingar:** `ArrayList` fungerar för små mängder, men för tusentals former överväg `HashSet` för att snabbt eliminera dubbletter.

**Bästa praxis**
- Håll biblioteket uppdaterat för att dra nytta av prestandaförbättringar.  
- Profilera providern med realistiska frågelaster för att tidigt identifiera flaskhalsar.

## Slutsats
Du har nu lärt dig hur du **genererar singular‑pluralformer i Java** med en anpassad `SimpleWordFormsProvider` i GroupDocs.Search. Denna lätta komponent kan avsevärt förbättra relevansen i sökresultat och noggrannheten i språkanalys i många applikationer.

**Nästa steg:**  
- Experimentera med mer avancerade språkliga regler (oregelbundna pluralformer, stemming).  
- Integrera providern i en indexerings‑pipeline och mät förbättringar i återkallning.  
- Utforska andra GroupDocs.Search‑funktioner som synonym‑ordböcker och anpassade analysverktyg.

**Uppmaning:** Prova att lägga till `SimpleWordFormsProvider` i ditt eget projekt idag och se hur det berikar din sökupplevelse!

## FAQ‑avsnitt

**1. Vad är GroupDocs.Search för Java?**  
Det är ett kraftfullt bibliotek som erbjuder fulltextsökning, indexering och språkliga funktioner — inklusive möjligheten att ansluta anpassade word‑form‑providers.

**2. Hur fungerar SimpleWordFormsProvider?**  
Den genererar alternativa former genom att tillämpa enkla suffix‑baserade regler (ta bort “s/es”, konvertera “y” till “is” och lägga till “s/es”).

**3. Kan jag anpassa reglerna för word‑form‑generering?**  
Absolut. Modifiera `getWordForms`‑metoden för att inkludera oregelbundna former, lokalspecifika regler eller integration med externa ordböcker.

**4. Vilka är vanliga tillämpningar för denna funktion?**  
Sökmotorer, textanalys‑pipelines och CMS‑plattformar drar nytta av att känna igen singular‑/plural‑varianter.

**5. Behöver jag en kommersiell licens för produktionsanvändning?**  
Ja — även om en provperiod låter dig utforska API‑et, tar en köpt licens bort användningsgränser och ger support.

---

**Senast uppdaterad:** 2026-02-21  
**Testat med:** GroupDocs.Search 25.4 (Java)  
**Författare:** GroupDocs