---
date: '2026-01-11'
description: Lär dig hur du skapar ett anpassat sökindex med GroupDocs.Search för
  Java, konfigurerar vanliga och blandade tecken för avancerad OCR och bildsökning.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Skapa anpassat sökindex med teckenigenkänning – GroupDocs.Search Java
type: docs
url: /sv/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Skapa anpassat sökindex med teckenigenkänning med GroupDocs.Search för Java

I moderna dokumenttunga applikationer är **att skapa ett anpassat sökindex** som förstår nyanserna i din text—såsom bindestreck, understreck eller språk‑specifika symboler—avgörande för snabb och exakt återhämtning. Denna handledning guidar dig genom att konfigurera teckenigenkänning i **GroupDocs.Search för Java**, och täcker både vanliga tecken (bokstäver, siffror, understreck) och blandade tecken (t.ex. bindestreck). I slutet kommer du kunna skräddarsy ett index som passar exakt dina OCR‑ eller bildsök‑scenarier.

## Snabba svar
- **Vad betyder “skapa anpassat sökindex”?** Det innebär att konfigurera ett index så att specifika symboler behandlas som bokstäver eller blandade tecken, snarare än att ignoreras.  
- **Vilket bibliotek används?** GroupDocs.Search för Java (v25.4 vid skrivtillfället).  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en betald licens krävs för produktion.  
- **Kan jag indexera både PDF‑filer och bilder?** Ja—GroupDocs.Search stödjer OCR på bilder och PDF‑filer när det är korrekt konfigurerat.  
- **Krävs Maven?** Maven är det rekommenderade sättet att hantera beroenden, men du kan också använda Gradle eller manuella JAR‑filer.

## Vad är ett anpassat sökindex?
Ett anpassat sökindex låter dig definiera hur sökmotorn tolkar tecken. Som standard ignoreras många symboler, vilket kan leda till missade träffar för exempelvis ärendenummer (`ABC-123`) eller kodsnuttar (`my_variable`). Genom att justera alfabet‑ordlistan får du full kontroll över vad motorn betraktar som sökbar text.

## Varför konfigurera vanliga och blandade tecken?
- **Vanliga tecken** (bokstäver, siffror, understreck) behandlas som fristående token, vilket förbättrar exakt‑match‑sökningar.  
- **Blandade tecken** (bindestreck, snedstreck) förenar ord; att konfigurera dem förhindrar oönskad token‑uppdelning, vilket är kritiskt för juridiska referenser, produktkoder eller källkod‑indexering.

## Förutsättningar
- **JDK 8** eller senare installerad.  
- **Maven** för beroendehantering.  
- Tillgång till **GroupDocs.Search för Java**‑biblioteket (nedladdat via Maven eller den officiella webbplatsen).  

### Nödvändiga bibliotek och beroenden
Lägg till repository‑ och beroende‑poster i din `pom.xml` (som visas nedan). XML‑blocket får inte ändras.

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

Du kan också ladda ner de senaste JAR‑filerna från [GroupDocs.Search för Java‑releaser](https://releases.groupdocs.com/search/java/).

### Licensanskaffning
- **Gratis prov** – perfekt för tidig experimentering.  
- **Tillfällig licens** – användbar för längre utvecklingscykler.  
- **Produktionslicens** – krävs för kommersiell driftsättning.  

Skaffa en licens via den officiella portalen: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Grundläggande initialisering
Kodsnutten nedan visar den minsta koden som behövs för att starta ett tomt index. Behåll den oförändrad; vi bygger vidare på den senare.

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

## Installera GroupDocs.Search för Java

### Installation via Maven
Maven‑konfigurationen från avsnittet *Förutsättningar* är allt du behöver. Efter att du lagt till den kör du `mvn clean install` för att hämta binärerna.

### Miljöinställningar
- Säkerställ att **indexmappen** och **dokumentmappen** finns på disken.  
- Använd absoluta sökvägar eller konfigurera din IDE så att relativa sökvägar löses korrekt.  

## Implementeringsguide

Nedan går vi igenom två separata funktioner: **vanliga tecken** och **blandade tecken**. Varje funktion följer samma mönster—definiera sökvägar, skapa indexet, sätt teckensnitt‑ordlistan och indexera slutligen dina dokument.

### Funktion 1 – Vanliga tecken

#### Översikt
Vanliga tecken behandlas som oberoende token. Detta är idealiskt när du vill att siffror, bokstäver och understreck ska vara sökbara exakt som de visas.

#### Steg‑för‑steg‑implementering

**1️⃣ Ange sökvägar**  
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
Blandade tecken (som bindestreck) förenar ofta två ord. Att markera dem som *blandade* talar om för motorn att hålla de omgivande token‑erna ihop under indexeringen.

#### Steg‑för‑steg‑implementering

**1️⃣ Ange sökvägar**  

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
Juridiska filer innehåller ofta ärendenummer som `2023-AB-456`. Genom att konfigurera understreck och bindestreck returnerar sökningar exakta träffar utan att dela upp identifieraren.

### Användningsfall 2 – Källkodsförråd
Utvecklare behöver söka i kodsnuttar där understreck (`my_variable`) och bindestreck (`my-function`) är meningsfulla. Anpassad teckenigenkänning säkerställer att sökmotorn respekterar dessa symboler.

### Användningsfall 3 – Flerspråkiga dataset
När du arbetar med språk som använder ytterligare alfabet kan du utöka den vanliga teckenmängden för att inkludera dessa Unicode‑intervall, vilket garanterar korrekta korsspråkliga sökresultat.

## Prestanda‑överväganden

- **Resurshantering** – Håll koll på heap‑användning; stora index drar nytta av inkrementella commit‑s.  
- **Garbage Collection** – Frigör `Index`‑objekt när de är klara så att JVM kan återvinna minnet.  
- **Indexoptimering** – Anropa periodiskt `index.optimize()` (om tillgängligt) för att komprimera indexet och förbättra frågehastigheten.  

## Slutsats

Du vet nu hur du **skapar ett anpassat sökindex** som skiljer mellan vanliga och blandade tecken med GroupDocs.Search för Java. Denna fin‑granulerade kontroll ger dig möjlighet att bygga OCR‑medvetna, högpresterande söklösningar skräddarsydda för juridiska, utvecklings‑ eller flerspråkiga miljöer.

**Nästa steg**  
- Experimentera med ytterligare Unicode‑intervall för icke‑latinska alfabet.  
- Kombinera teckenkonfiguration med andra GroupDocs.Search‑funktioner som stemming eller synonymer.  
- Integrera indexet i ett REST‑API för att exponera sökfunktionalitet till front‑end‑applikationer.

## Vanliga frågor

**Q:** *Vad är syftet med `CharacterType.Letter`?*  
**A:** Det talar om för indexet att behandla de angivna tecknen som vanliga bokstäver, så att de tokeniseras separat under indexeringen.

**Q:** *Kan jag blanda vanliga och blandade tecken i samma index?*  
**A:** Ja—anropa helt enkelt `setRange` för varje typ; ordlistan hanterar båda konfigurationerna samtidigt.

**Q:** *Behöver jag bygga om indexet efter att ha ändrat alfabetet?*  
**A:** Absolut. Ändringar i teckenordlistan påverkar tokeniseringen, så du måste åter‑indexera dokumenten för att tillämpa de nya reglerna.

**Q:** *Finns det en gräns för hur många anpassade tecken jag kan definiera?*  
**A:** Biblioteket stödjer hela Unicode‑området; prestandan kan försämras om du lägger till en extremt stor mängd, så begränsa dig till de tecken du faktiskt behöver.

**Q:** *Hur påverkar detta OCR‑noggrannheten?*  
**A:** Genom att anpassa indexets teckenmängd till OCR‑motorns utdata minskar du falska negativa och förbättrar den övergripande sökrelevansen.

---

**Senast uppdaterad:** 2026-01-11  
**Testat med:** GroupDocs.Search 25.4 för Java  
**Författare:** GroupDocs  

---