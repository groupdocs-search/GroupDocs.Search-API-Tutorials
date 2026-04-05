---
date: '2026-04-05'
description: Leer hoe je een zoekindex in .NET maakt, documenten aan de index toevoegt
  en speciale tekens in een query escapt met GroupDocs.Search en GroupDocs.Redaction.
keywords:
- create search index .net
- add documents to index
- escape special characters query
title: Maak zoekindex .NET met GroupDocs Redaction & Search
type: docs
url: /nl/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/
weight: 1
---

# Beheersen van GroupDocs Redaction en Search in .NET: Efficiënt Documentbeheer en Veilige Zoeken

Het beheren van grote collecties documenten kan snel overweldigend worden, vooral wanneer je **create search index .NET** oplossingen moet maken die ook gevoelige informatie beschermen. Of je nu een juridisch archief, een medisch dossiersysteem of een e‑commercecatalogus bouwt, de combinatie van **GroupDocs.Redaction** en **GroupDocs.Search for .NET** biedt je de tools om inhoud veilig en efficiënt te indexeren, doorzoeken en te redigeren.

## Snelle Antwoorden
- **What does “create search index .NET” mean?** Het betekent het bouwen van een doorzoekbare datastructuur op schijf die je .NET-app in staat stelt documenten snel te vinden.  
- **Which library handles redaction?** GroupDocs.Redaction verwijdert of maskeert gevoelige gegevens uit documenten.  
- **How do I add documents to index?** Gebruik `index.Add(yourFolderPath)` om bestanden automatisch in te lezen.  
- **Do I need to escape special characters in queries?** Ja—escape karakters zoals `&`, `|`, `(`, `)` om parse‑fouten te voorkomen.  
- **Is this approach suitable for large datasets?** Absoluut; de index kan schalen en incrementeel worden bijgewerkt.

## Wat is “create search index .NET”?
Het maken van een zoekindex in .NET betekent het construeren van een persistente structuur die termen koppelt aan de documenten waarin ze voorkomen. Deze index maakt snelle full‑text zoekopdrachten mogelijk zonder elke keer alle bestanden te scannen wanneer een query wordt uitgevoerd.

## Waarom GroupDocs.Search combineren met GroupDocs.Redaction?
- **Security first:** Redigeer persoonlijke gegevens voordat zoekresultaten worden getoond.  
- **Performance:** Zoekindexen zijn geoptimaliseerd voor snelheid, terwijl redactie alleen op de originele bestanden wordt uitgevoerd wanneer nodig.  
- **Flexibility:** Beide bibliotheken ondersteunen veel bestandsformaten (PDF, DOCX, afbeeldingen, enz.) direct uit de doos.

## Vereisten
- **GroupDocs.Search** version 21.8+  
- **GroupDocs.Redaction** for .NET (compatible version)  
- .NET Core SDK 3.1 of later  
- Een map met de documenten die je wilt indexeren  

## GroupDocs.Redaction voor .NET instellen
### Installatie
```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

### Licentie‑acquisitie
1. **Free Trial** – test de kernfuncties.  
2. **Temporary License** – breid de proeflimieten uit.  
3. **Full License** – ontgrendel productie‑klare mogelijkheden.

### Basisinitialisatie
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the file path of the document
Redactor redactor = new Redactor("path/to/document.pdf");
```

## Hoe create search index .NET te maken
Hieronder vind je een stapsgewijze walkthrough die precies laat zien hoe je **create search index .NET** projecten maakt, speciale‑tekenverwerking configureert en queries voorbereidt.

### Stap 1: Index maken
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchForSpecialCharacters";

// Create an index at the specified path. The second parameter 'true' allows overwriting existing indexes.
Index index = new Index(indexFolder, true);
```
*Deze regel maakt de fysieke indexmap aan en bereidt deze voor op het inlezen van documenten.*

### Stap 2: Teken­typen configureren
```csharp
// Configure character types for '&' as a letter and '-' as a separator within the alphabet dictionary of the index.
index.Dictionaries.Alphabet.SetRange(new char[] { '&' }, CharacterType.Letter);
index.Dictionaries.Alphabet.SetRange(new char[] { '-' }, CharacterType.Separator);
```
*Het aanpassen van de tekenverwerking zorgt ervoor dat queries zoals “rock&roll‑music” correct worden geïnterpreteerd.*

### Stap 3: Documenten aan index toevoegen
```csharp
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index.
index.Add(documentsFolder);
```
*Hier **voegen we documenten toe aan de index** in bulk, waardoor elk ondersteund bestand doorzoekbaar wordt.*

### Stap 4: Speciale tekens definiëren en escapen in query
```csharp
using System.Text;

string word = "rock&roll-music";
StringBuilder result = new StringBuilder();

// Replace separators with space characters in the query string.
for (int i = 0; i < word.Length; i++)
{
    char character = word[i];
    CharacterType characterType = index.Dictionaries.Alphabet.GetCharacterType(character);
    if (characterType == CharacterType.Separator)
    {
        result.Append(' ');
    }
    else
    {
        result.Append(character);
    }
}

// Escape special characters.
const string specialCharacters = "():\"&|!^~*?\\";
for (int i = result.Length - 1; i >= 0; i--)
{
    char c = result[i];
    if (specialCharacters.Contains(c.ToString()))
    {
        result.Insert(i, '\\');
    }
}

string query = result.ToString();
if (query.Contains(" "))
{
    query = "\"" + query + "\"";
}
```
*Dit blok **escape special characters query** logica garandeert dat de zoekmachine de invoer correct parseert.*

### Stap 5: De zoekquery uitvoeren
```csharp
// Perform the search using the prepared query string.
SearchResult searchResult = index.Search(query);
```
*Het `SearchResult`‑object bevat nu alle overeenkomende documenten, klaar voor verdere verwerking of weergave.*

## Praktische Toepassingen
1. **Legal Document Management** – vind clausules in duizenden contracten terwijl persoonlijke gegevens worden geredigeerd.  
2. **Medical Records Search** – vind patiëntnotities snel, en redacteer vervolgens PHI voordat ze worden gedeeld.  
3. **E‑commerce Catalogs** – maak robuuste productzoekopdrachten mogelijk met aangepaste tokenisatie voor SKU‑codes en merknamen.

## Prestatie‑overwegingen
- **Index Refresh:** Voer `index.Add()` opnieuw uit of gebruik incrementele updates wanneer bestanden wijzigen.  
- **Memory Management:** Vernietig `Index`‑objecten wanneer ze niet meer nodig zijn, vooral in services met hoge belasting.  
- **Async Operations:** Wikkel zoekaanroepen in `Task.Run` voor niet‑blokkende UI‑ of API‑reacties.

## Veelvoorkomende Problemen en Oplossingen
| Probleem | Oplossing |
|----------|-----------|
| Queries geven geen resultaten voor termen met `&` of `-` | Zorg ervoor dat teken‑typen zijn geconfigureerd zoals weergegeven in **Step 2**. |
| Grote PDF's veroorzaken hoog geheugenverbruik | Schakel streaming‑modus in (`index.Options.UseStreaming = true`) en verwerk resultaten in batches. |
| Redaction wordt niet toegepast op doorzochte fragmenten | Redigeer eerst het originele bestand, bouw daarna de index opnieuw om de opgeschoonde inhoud weer te geven. |

## Veelgestelde Vragen

**Q: Hoe kan ik de tekenverwerking in mijn zoekindex aanpassen?**  
A: Gebruik `index.Dictionaries.Alphabet.SetRange()` om tekens te markeren als letters, scheidingstekens of interpunctie.

**Q: Kan ik meerdere documentformaten indexeren?**  
A: Ja—GroupDocs.Search ondersteunt PDF's, Word, Excel, PowerPoint, afbeeldingen en nog veel meer.

**Q: Hoe moet ik speciale tekens in zoekqueries behandelen?**  
A: Volg de stap **Define and Escape Special Characters in Query** om scheidingstekens te vervangen door spaties en een backslash (`\`) voor gereserveerde symbolen te plaatsen.

**Q: Wordt redaction automatisch uitgevoerd tijdens een zoekopdracht?**  
A: Redaction is een aparte stap; je kunt documenten eerst redigeren en daarna de index opnieuw opbouwen, of resultaten na het ophalen redigeren.

**Q: Hoe vaak moet ik mijn index opnieuw opbouwen of bijwerken?**  
A: Werk de index bij telkens wanneer bronbestanden wijzigen; een nachtelijke incrementele heropbouw werkt goed voor de meeste omgevingen.

## Conclusie
Je hebt nu een complete, productie‑klare gids voor **create search index .NET** projecten die krachtige redactiemogelijkheden integreren. Door de tekenverwerking te configureren, query‑strings veilig te escapen en je index regelmatig bij te werken, lever je snelle, veilige zoekervaringen voor elke document‑intensieve applicatie.

---

**Laatst bijgewerkt:** 2026-04-05  
**Getest met:** GroupDocs.Search 21.8+, GroupDocs.Redaction latest release  
**Auteur:** GroupDocs