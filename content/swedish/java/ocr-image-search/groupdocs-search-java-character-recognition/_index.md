---
date: '2026-03-17'
description: Lär dig hur du skapar ett index med GroupDocs.Search för Java, konfigurerar
  vanliga och blandade tecken och optimerar sökningen för juridiska ärendenummer och
  OCR‑bilder.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Hur man skapar ett index med teckenigenkänning i Java
type: docs
url: /sv/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

at med:** GroupDocs.Search 25.4 för Java"

"**Author:** GroupDocs" -> "**Författare:** GroupDocs"

Then "---"

We must ensure we keep all markdown formatting, code block placeholders unchanged.

Check for any other shortcodes: none.

Now produce final translated content.# Så skapar du index med teckenigenkänning med GroupDocs.Search för Java

I moderna dokumenttunga applikationer är **hur man skapar index** som respekterar nyanserna i din text—såsom bindestreck, understreck eller språk‑specifika symboler—viktigt för snabb, exakt återvinning. I den här handledningen går vi igenom hur man konfigurerar teckenigenkänning i **GroupDocs.Search för Java**, och täcker både vanliga tecken (bokstäver, siffror, understreck) och blandade tecken (t.ex. bindestreck). I slutet kommer du att kunna skräddarsy ett index som passar exakt dina OCR‑ eller bildsök‑scenarier, oavsett om du indexerar juridiska ärendenummer, källkods‑arkiv eller flerspråkiga PDF‑filer.

## Snabba svar
- **Vad betyder “create custom search index”?** Det betyder att konfigurera ett index för att behandla specifika symboler som bokstäver eller blandade tecken, snarare än att ignorera dem.  
- **Vilket bibliotek används?** GroupDocs.Search för Java (v25.4 vid skrivtillfället).  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en betald licens krävs för produktion.  
- **Kan jag indexera både PDF‑filer och bilder?** Ja—GroupDocs.Search stödjer OCR på bilder och PDF‑filer när det är korrekt konfigurerat.  
- **Krävs Maven?** Maven är det rekommenderade sättet att hantera beroenden, men du kan också använda Gradle eller manuella JAR‑filer.

## Vad är ett anpassat sök‑index?
Ett anpassat sök‑index låter dig definiera hur sökmotorn tolkar tecken. Som standard ignoreras många symboler, vilket kan leda till missade träffar för exempelvis ärendenummer (`2023-AB-456`) eller kodsnuttar (`my_variable`). Genom att justera alfabet‑ordlistan får du full kontroll över vad motorn behandlar som sökbar text.

## Varför konfigurera vanliga och blandade tecken för juridiska ärendenummer?
- **Vanliga tecken** (bokstäver, siffror, understreck) tokeniseras separat, vilket möjliggör exakt‑matchning sökningar för identifierare.  
- **Blandade tecken** (bindestreck, snedstreck) håller relaterade token ihop, vilket förhindrar oönskad splittring av ärendenummer, produktkoder eller filsökvägar.  
- Denna konfiguration **optimerar sök‑index**‑prestanda genom att minska token‑fragmentering och förbättra relevans för OCR‑genererat innehåll.

## Förutsättningar
- **JDK 8** eller senare installerat.  
- **Maven** för beroendehantering.  
- Tillgång till **GroupDocs.Search för Java**‑biblioteket (nedladdat via Maven eller den officiella webbplatsen).  

### Nödvändiga bibliotek och beroenden
Lägg till repository‑ och beroende‑poster i din `pom.xml` (som visas nedan). XML‑blocket måste förbli oförändrat.

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

Du kan också ladda ner de senaste JAR‑filerna från [GroupDocs.Search för Java‑utgåvor](https://releases.groupdocs.com/search/java/).

### Licensförvärv
- **Free Trial** – perfekt för tidig experimentering.  
- **Temporary License** – användbar för längre utvecklingscykler.  
- **Production License** – krävs för kommersiell distribution.  

Skaffa en licens från den officiella portalen: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Grundläggande initiering
Kodsnutten nedan visar den minsta koden som behövs för att starta ett tomt index. Behåll den som den är; vi kommer att bygga vidare på den senare.

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

## Konfigurera GroupDocs.Search för Java

### Installation via Maven
Maven‑konfigurationen från *Förutsättningar*-avsnittet är allt du behöver. Efter att du lagt till den, kör `mvn clean install` för att hämta binärerna.

### Krav för miljöinställning
- Se till att **index‑mappen** och **dokument‑mappen** finns på disken.  
- Använd absoluta sökvägar eller konfigurera din IDE för att lösa relativa sökvägar korrekt.  

## Implementeringsguide

Nedan går vi igenom två distinkta funktioner: **vanliga tecken** och **blandade tecken**. Varje funktion följer samma mönster—definiera sökvägar, skapa indexet, ange teckensnitt‑ordlistan och slutligen indexera dina dokument.

### Funktion 1 – Vanliga tecken

#### Översikt
Vanliga tecken behandlas som oberoende token. Detta är idealiskt när du vill att siffror, bokstäver och understreck ska vara sökbara exakt som de visas.

#### Steg‑för‑steg‑implementering

**1️⃣ Definiera sökvägar**  
Definiera var indexet ska lagras och var dina källdokument finns.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Skapa och konfigurera index**  
Instansiera indexet och rensa eventuell befintlig alfabet‑konfiguration.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definiera vanliga tecken**  
Bygg en teckenarray som inkluderar siffror, latinska bokstäver och understreck.

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

**4️⃣ Indexera dokument**  
Lägg till alla filer från källmappen till det nykonfigurerade indexet.

```java
index.add(documentFolder);
```

### Funktion 2 – Blandade tecken

#### Översikt
Blandade tecken (som bindestreck) kopplar ofta två ord. Att markera dem som *blandade* instruerar motorn att hålla de omgivande tokenen ihop under indexering.

#### Steg‑för‑steg‑implementering

**1️⃣ Definiera sökvägar**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Skapa och konfigurera index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definiera blandade tecken**  
Här talar vi om för ordlistan att bindestrecket ska behandlas som ett blandat tecken.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexera dokument**  

```java
index.add(documentFolder);
```

## Praktiska tillämpningar

### Användningsfall 1 – Juridisk dokumenthantering
Juridiska filer innehåller ofta ärendenummer som `2023-AB-456`. Genom att konfigurera understreck och bindestreck returnerar sökningar exakta träffar utan att dela identifieraren, vilket hjälper dig att **söka juridiska ärendenummer** effektivt.

### Användningsfall 2 – Källkods‑arkiv
Utvecklare behöver söka kodsnuttar där understreck (`my_variable`) och bindestreck (`my-function`) är betydelsefulla. Anpassad teckenigenkänning säkerställer att sökmotorn respekterar dessa symboler.

### Användningsfall 3 – Flerspråkiga dataset
När du arbetar med språk som använder ytterligare alfabet kan du **utöka Unicode‑teckenuppsättningen** för att inkludera dessa intervall, vilket garanterar korrekta sökresultat över språk.

### Användningsfall 4 – Indexera PDF‑bilder
Om du indexerar skannade PDF‑filer eller bildfiler innehåller OCR‑utdata ofta blandade tecken. Genom att korrekt konfigurera vanliga och blandade tecken **optimeras sök‑index**‑prestanda för bildbaserat innehåll.

## Prestandaöverväganden

- **Resurshantering** – Håll koll på heap‑användning; stora index drar nytta av inkrementella commit.  
- **Soppsamling** – Frigör `Index`‑objekt när de är klara så att JVM kan återta minnet.  
- **Indexoptimering** – Anropa periodiskt `index.optimize()` (om tillgängligt) för att komprimera indexet och förbättra frågehastigheten.  

## Slutsats

Du vet nu **hur man skapar index** som skiljer mellan vanliga och blandade tecken med GroupDocs.Search för Java. Denna finmaskiga kontroll gör det möjligt att bygga OCR‑medvetna, högpresterande söklösningar anpassade för juridiska, utvecklings‑ eller flerspråkiga miljöer.

### Nästa steg
- Experimentera med ytterligare Unicode‑intervall för icke‑latinska alfabet.  
- Kombinera teckenkonfiguration med andra GroupDocs.Search‑funktioner som stemming eller synonymer.  
- Integrera indexet i ett REST‑API för att exponera sökfunktioner till front‑end‑applikationer.

## Vanliga frågor

**Q:** *Vad är syftet med `CharacterType.Letter`?*  
**A:** Det talar om för indexet att behandla de angivna tecknen som vanliga bokstäver, så de tokeniseras separat under indexering.

**Q:** *Kan jag blanda vanliga och blandade tecken i samma index?*  
**A:** Ja—anropa helt enkelt `setRange` för varje typ; ordlistan hanterar båda konfigurationerna samtidigt.

**Q:** *Behöver jag bygga om indexet efter att ha ändrat alfabetet?*  
**A:** Absolut. Ändringar i teckenordlistan påverkar tokenisering, så du måste åter‑indexera dokumenten för att tillämpa de nya reglerna.

**Q:** *Finns det en gräns för hur många anpassade tecken jag kan definiera?*  
**A:** Biblioteket stödjer hela Unicode‑intervallet; prestanda kan försämras om du lägger till en extremt stor mängd, så begränsa det till de tecken du faktiskt behöver.

**Q:** *Hur påverkar detta OCR‑noggrannheten?*  
**A:** Genom att anpassa indexets teckenuppsättning till OCR‑motorns utdata minskar du falska negativa och förbättrar den övergripande sökrelevansen.

---

**Senast uppdaterad:** 2026-03-17  
**Testat med:** GroupDocs.Search 25.4 för Java  
**Författare:** GroupDocs  

---