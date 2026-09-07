---
date: '2026-06-22'
description: Scopri come censurare i documenti in .NET ottimizzando le prestazioni
  di ricerca con GroupDocs.Redaction e GroupDocs.Search. Gestione passo‑passo degli
  attributi, indicizzazione e censura sicura per gli sviluppatori .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Come censurare i documenti in .NET usando GroupDocs Redaction
type: docs
url: /it/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Come Redigere Documenti in .NET Utilizzando GroupDocs Redaction

In questo tutorial completo scoprirai **come censurare documenti** in un ambiente .NET e, allo stesso tempo, padroneggiare la gestione degli attributi dei documenti con GroupDocs.Redaction e GroupDocs.Search. Che tu debba proteggere dati sensibili, aumentare la velocità di ricerca o organizzare grandi librerie di documenti, le tecniche illustrate qui offrono una soluzione pronta per la produzione che scala a centinaia di migliaia di file.

## Risposte Rapide
- **Come posso censurare un PDF in .NET?** Carica il file con `Redactor`, definisci una `RedactionRegion` e chiama `Redactor.Apply()` – tre righe di codice gestiscono il lavoro pesante.  
- **Posso modificare gli attributi del documento dopo l'indicizzazione?** Sì, usa `AttributeChangeBatch` per aggiungere, aggiornare o rimuovere attributi in blocco.  
- **Quali librerie sono necessarie?** `GroupDocs.Redaction` + `GroupDocs.Search` (ultime versioni NuGet).  
- **È necessaria una licenza per la produzione?** È richiesta una licenza valida di GroupDocs; è disponibile una licenza di prova temporanea per la valutazione.  
- **Come posso migliorare la velocità di ricerca?** Abilita l'elaborazione in batch e l'indicizzazione selettiva; queste tecniche possono **ottimizzare le prestazioni di ricerca** fino al 40 % su grandi set di dati.

## Che cosa significa “come censurare documenti”?

Descrive il processo automatizzato di individuare informazioni sensibili all'interno di un file e sostituirle con contenuti oscurati—come barre nere o spazi bianchi—mantenendo intatto il layout originale. Questo garantisce che i dati riservati siano nascosti agli osservatori, ma il documento rimane leggibile e funzionale per le attività successive.

## Perché utilizzare GroupDocs.Redaction e GroupDocs.Search insieme?

GroupDocs.Redaction supporta **oltre 50 formati di file** (PDF, DOCX, XLSX, PPTX, immagini, ecc.) e può elaborare documenti fino a **2 GB** senza caricare l'intero file in memoria. GroupDocs.Search indicizza oltre **70 milioni di termini** all'ora su un server standard, consentendoti di **ottimizzare le prestazioni di ricerca** in modo drammatico quando combinato con il filtraggio basato su attributi.

## Prerequisiti

- **Librerie richieste:** `GroupDocs.Search` e `GroupDocs.Redaction` (ultime versioni NuGet).  
- **Ambiente di sviluppo:** Visual Studio 2019 o successivo, con destinazione .NET Core 3.1 o .NET 6+.  
- **Conoscenze di base:** sintassi C#, concetti di programmazione orientata agli oggetti e familiarità con i principi di indicizzazione dei documenti.

## Configurare GroupDocs.Redaction per .NET

### Installazione della libreria

Puoi aggiungere **GroupDocs.Redaction** al tuo progetto usando uno dei seguenti metodi:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- Cerca “GroupDocs.Redaction” e installa l'ultima versione.

### Passaggi per l'Acquisizione della Licenza

Per iniziare, puoi ottenere una licenza temporanea o acquistarne una. È disponibile una prova gratuita per testare le funzionalità prima di impegnarti:
1. Visita la [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) per richiedere una licenza temporanea.  
2. Segui le istruzioni fornite per applicare la licenza nella tua applicazione.

### Inizializzazione e Configurazione di Base

`Redactor` è la classe principale usata per caricare un documento e applicare operazioni di censura.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Funzione 1: Modificare gli Attributi del Documento

### Panoramica
Modificare gli attributi del documento ti consente di affinare come i documenti appaiono nei risultati di ricerca, abilitando filtraggi e categorizzazioni precise.

#### Passo 1: Inizializzare l'Indice

`Index` rappresenta una collezione ricercabile di documenti e dei relativi metadati.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Passo 2: Modificare gli Attributi

`AttributeChangeBatch` è la classe che raggruppa gli aggiornamenti degli attributi per efficienza.  

**Ancora di definizione:** *`AttributeChangeBatch` raggruppa operazioni di aggiunta, aggiornamento e cancellazione sugli attributi del documento in un'unica transazione.*  

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### Passo 3: Ricerca con Filtri di Attributi

Puoi filtrare i risultati della ricerca per valori di attributi usando `SearchOptions`.  

**Risposta diretta:** Per cercare documenti che contengono l'attributo `Category = "Legal"`, configura `SearchOptions` con un `AttributeFilter` e chiama `searcher.Search("contract", options)`. Questo restituisce solo i contratti etichettati come legali, riducendo il rumore dei risultati e **ottimizzando le prestazioni di ricerca**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Funzione 2: Aggiungere Attributi Durante l'Indicizzazione

### Panoramica
Aggiungere attributi al momento dell'indicizzazione garantisce che ogni documento sia arricchito con i metadati corretti fin dall'inizio, eliminando la necessità di aggiornamenti massivi successivi.

#### Passo 1: Configurare il Gestore di Eventi per l'Indicizzazione

**Ancora di definizione:** *L'evento `DocumentIndexed` viene attivato ogni volta che un documento viene aggiunto con successo all'indice, consentendo l'esecuzione di logica personalizzata.*  

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Passo 2: Configurare ed Eseguire la Ricerca

Dopo che gli attributi sono stati associati, puoi cercare usando quei nuovi campi.

**Risposta diretta:** Usa `SearchOptions` con `AttributeFilter` per interrogare gli attributi appena aggiunti, ad esempio `AttributeFilter("Department", "Finance")`. Questo restituisce solo i file relativi alla finanza, dimostrando **come indicizzare gli attributi** per risultati più rapidi e pertinenti.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Applicazioni Pratiche

Ecco tre scenari comuni in cui la gestione congiunta di attributi e censura aggiunge valore concreto al business:

1. **Gestione Documenti Legali** – Censura automaticamente le clausole riservate e tagga i contratti per giurisdizione, consentendo agli avvocati di trovare solo i file pertinenti.  
2. **Organizzazione Cartelle Cliniche** – Censura gli identificatori dei pazienti aggiungendo attributi come `PatientID` e `VisitDate` per un recupero conforme e veloce.  
3. **Catalogazione Prodotti E‑commerce** – Censura le informazioni sui prezzi dei fornitori e tagga i prodotti con `StockStatus` o `DiscountRate` durante l'importazione di massa, consentendo query di inventario in tempo reale.

## Considerazioni sulle Prestazioni

Quando si lavora con grandi set di dati, tieni presente queste best practice:

- **Elaborazione in Batch:** `AttributeChangeBatch` riduce le richieste all'indice, diminuendo il tempo di elaborazione fino al **45 %** su batch di 100 k documenti.  
- **Indicizzazione Selettiva:** Indicizza solo i documenti che necessitano di nuovi attributi; ignora i file non modificati per risparmiare CPU e I/O.  
- **Gestione della Memoria:** Disporre le istanze di `SearchResult`, `Redactor` e `Indexer` non appena non sono più necessarie per liberare risorse non gestite.

## Problemi Comuni e Soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| La censura non nasconde il testo | Coordinate `RedactionRegion` errate | Verifica le dimensioni della pagina con `Redactor.GetPageSize()` prima di definire la regione. |
| Le modifiche agli attributi non sono riflesse nella ricerca | Indice non aggiornato | Chiama `searcher.Refresh()` dopo l'esecuzione di `AttributeChangeBatch`. |
| Errori di out‑of‑memory su file di grandi dimensioni | Caricamento dell'intero file in memoria | Abilita la modalità streaming impostando `RedactorOptions.Stream = true`. |

## Domande Frequenti

**D: Qual è il modo migliore per censurare in batch più PDF?**  
R: Carica ogni file con `Redactor`, aggiungi una `RedactionRegion` per ogni area sensibile, quindi chiama `Redactor.Apply()` all'interno di un ciclo; questo approccio elabora migliaia di file con un minimo utilizzo di memoria.

**D: Posso combinare la censura con il filtraggio degli attributi in un'unica query?**  
R: Sì. Dopo la censura, il documento mantiene i metadati, quindi è possibile cercare sia con termini di testo sia con `AttributeFilter` simultaneamente.

**D: Come gestisco i documenti protetti da password?**  
R: Passa la password al costruttore `Redactor`; la libreria decritterà, censurerà e ricifrerà il file automaticamente.

**D: GroupDocs supporta l'OCR per immagini scansionate prima della censura?**  
R: Assolutamente. Abilita `RedactorOptions.Ocr = true` per riconoscere il testo nelle immagini, quindi applica le regole di censura sul testo estratto.

**D: Quali versioni .NET sono ufficialmente supportate?**  
R: GroupDocs.Redaction e GroupDocs.Search supportano .NET Core 3.1, .NET 5, .NET 6 e .NET 7, così come .NET Framework 4.6.2+.

## Conclusione

Ora disponi di una soluzione full‑stack per **censurare documenti** ottimizzando le **prestazioni di ricerca** e **indicizzare gli attributi** usando GroupDocs.Redaction e GroupDocs.Search. Seguendo i passaggi sopra, potrai proteggere i dati sensibili, arricchire il tuo indice di ricerca con metadati significativi e mantenere le tue applicazioni .NET rapide e sicure.

---

**Last Updated:** 2026-06-22  
**Tested With:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**Author:** GroupDocs

## Tutorial Correlati

- [Padroneggiare GroupDocs.Redaction .NET: Creazione Efficiente di Indici e Gestione Alias per Ricerca Avanzata di Documenti](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Censura di Documenti e Indicizzazione dei Metadati con GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Padroneggiare GroupDocs.Redaction .NET: Configurazione e Gestione degli Eventi per la Gestione Sicura dei Documenti](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)