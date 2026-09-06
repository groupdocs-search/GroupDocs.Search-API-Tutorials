---
date: '2026-06-12'
description: Scopri come creare un indice di ricerca .NET e applicare la redazione
  a PDF usando GroupDocs.Search e GroupDocs.Redaction. Configurazione, distribuzione,
  indicizzazione e ricerca avanzata spiegate.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Creare un indice di ricerca .NET con GroupDocs Search e GroupDocs.Redaction
  – Guida completa
type: docs
url: /it/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Crea un indice di ricerca .NET con GroupDocs Search e Redaction – Guida completa

Nell'odierno panorama digitale, **creare un indice di ricerca .NET** è una soluzione che può sia individuare rapidamente le informazioni sia proteggere i dati sensibili, ed è una priorità assoluta per qualsiasi organizzazione. Questo tutorial ti guida nella configurazione di una rete scalabile GroupDocs.Search, nel deployment dei nodi, nell'indicizzazione dei documenti e nell'utilizzo di GroupDocs.Redaction per **applicare la redazione ai file PDF** — tutto all'interno di un ambiente .NET.

## Risposte rapide
- **Qual è il primo passo per creare un indice di ricerca .NET?** Definire un percorso base e una porta, quindi distribuire i nodi della rete.  
- **Come applico la redazione ai PDF con GroupDocs?** Inizializzare un'istanza di `Redactor`, caricare il PDF e chiamare `Redact` con i pattern desiderati.  
- **Posso eseguire la rete di ricerca su più macchine?** Sì — distribuisci i nodi su server separati e lascia che il nodo master coordini l'indicizzazione e le query.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza valida di GroupDocs per la produzione; è disponibile una licenza di prova temporanea per la valutazione.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.7.2+, .NET Core 3.1+ e .NET 5/6/7 sono pienamente supportati.

## Cos'è “creare un indice di ricerca .net”?
*Creare un indice di ricerca .NET* si riferisce alla costruzione di un repository ricercabile di metadati e contenuti dei documenti usando librerie .NET, che estrae il testo, tokenizza i termini e li memorizza in una struttura di indice ottimizzata. Questo consente risposte istantanee alle query su nodi distribuiti, supportando vari formati di file e permettendo il recupero di documenti scalabile e ad alte prestazioni nelle applicazioni aziendali.

## Perché usare GroupDocs Search e Redaction insieme?
GroupDocs.Search supporta **oltre 50 formati di file** — inclusi DOCX, PDF, PPTX e HTML — e può indicizzare documenti di centinaia di pagine senza caricare l'intero file in memoria. Combinato con GroupDocs.Redaction, che può **applicare la redazione ai PDF** in meno di 200 ms per pagina, ottieni una pipeline di gestione documenti sicura e ad alte prestazioni.

## Prerequisiti

### Librerie e dipendenze richieste
Per seguire questo tutorial, installa i seguenti pacchetti:
- **GroupDocs.Search** per .NET
- **GroupDocs.Redaction** per .NET  

Puoi utilizzare uno qualsiasi di questi metodi per installare le librerie necessarie:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Cerca "GroupDocs.Search" e "GroupDocs.Redaction" e installa l'ultima versione.

### Requisiti di configurazione dell'ambiente
- .NET Framework 4.7.2 o superiore (o .NET Core 3.1+)
- IDE Visual Studio (Community, Professional o Enterprise)

### Prerequisiti di conoscenza
- Programmazione C# di base
- Concetti di programmazione orientata agli oggetti
- Familiarità con le configurazioni di rete e i sistemi di gestione documentale

## Configurazione di GroupDocs.Redaction per .NET

### Informazioni sull'installazione
Per integrare le funzionalità di redazione nella tua applicazione, inizia aggiungendo la libreria GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Cerca "GroupDocs.Redaction" e installala.

### Acquisizione della licenza
Per iniziare con una prova gratuita o una licenza temporanea, segui questi passaggi:
- Visita il [sito web di GroupDocs](https://purchase.groupdocs.com/temporary-license/) per richiedere una licenza temporanea.  
- Per le opzioni di acquisto, vai alla loro [pagina dei prezzi](https://groupdocs.com/pricing).

Una volta ottenuto il file di licenza, applicalo nella configurazione della tua applicazione:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Inizializzazione di base
Per inizializzare GroupDocs.Redaction per operazioni di base, utilizza il seguente frammento di codice:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Guida all'implementazione

### Configurazione

#### Panoramica
Questa funzionalità configura la tua rete di ricerca usando un percorso base e un numero di porta, formando la base del tuo sistema di gestione documenti.

#### Ancoraggio della definizione
`SearchNetworkDeployment` è la classe che orchestra il deployment dei nodi di ricerca nella rete.

#### Step 1: Define Base Path and Port  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Step 2: Configure the Network  
Usa il metodo `Configure` per impostare la rete di ricerca con il percorso e la porta specificati:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Distribuzione dei nodi di rete

#### Panoramica
Distribuisci i nodi all'interno della rete di ricerca configurata per la ricerca di documenti distribuita.

#### Ancoraggio della definizione
`SearchNetworkNode` rappresenta un nodo ricercabile individuale che comunica con il nodo master.

#### Step 1: Initialize Deployment  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Sottoscrizione agli eventi per il nodo master

#### Panoramica
Sottoscrivi gli eventi sul nodo master per monitorare e gestire le operazioni della rete in modo efficace.

#### Ancoraggio della definizione
`SearchNetworkNodeEvents` fornisce callback per l'indicizzazione, l'esecuzione delle query e la gestione degli errori.

#### Step 1: Identify the Master Node  
Seleziona il primo nodo come master:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Step 2: Subscribe to Events  
Sottoscrivi gli eventi usando:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Indicizzazione dei documenti

#### Panoramica
Indicizza i documenti per operazioni di ricerca efficienti. Questo passo è cruciale per garantire che la tua rete possa recuperare rapidamente i dati necessari.

#### Ancoraggio della definizione
`SearchIndex` è l'oggetto principale che memorizza token ricercabili e metadati per ogni file indicizzato.

#### Step 1: Add Directories to Index  
Specifica le directory contenenti i tuoi documenti:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Funzionalità di ricerca – Uso base

#### Panoramica
Esegui operazioni di ricerca di base sui nodi della rete.

#### Risposta diretta
Chiama `SearchNetwork.Query("your term")` sul nodo master per recuperare istantaneamente i documenti corrispondenti. Il metodo restituisce una collezione di oggetti `SearchResult` che includono i percorsi dei file e i punteggi di rilevanza.  
`SearchNetwork.Query` è un metodo che esegue una query di ricerca su tutta la rete e restituisce i risultati corrispondenti.

#### Step 1: Define Search Parameters  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Funzionalità di ricerca avanzata

#### Panoramica
Utilizza tecniche di ricerca avanzata con parametri personalizzabili per risultati più precisi.

#### Risposta diretta
Implementa un metodo che crea un oggetto `SearchOptions`, imposta le proprietà `UseFuzzySearch`, `Highlight` e `PageSize`, quindi lo passa a `SearchNetwork.QueryAdvanced`. Questo restituisce risultati paginati e evidenziati con corrispondenza fuzzy abilitata.  
`SearchNetwork.QueryAdvanced` è un metodo che esegue una query con opzioni avanzate come la corrispondenza fuzzy e la paginazione.

#### Step 1: Implement the Advanced Search Method  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Applicazione della redazione ai file PDF

#### Panoramica
Proteggi le informazioni sensibili redigendo il contenuto PDF prima che venga memorizzato o condiviso.

#### Risposta diretta
Crea un'istanza `Redactor`, carica il PDF di destinazione, definisci un `RedactionPattern` (ad esempio, regex SSN), chiama `redactor.Apply(pattern)` e infine salva il documento redatto. Questo processo garantisce che i dati personali siano rimossi in modo permanente.

#### Ancoraggio della definizione
`Redactor` è la classe principale in GroupDocs.Redaction che elabora i documenti e applica le regole di redazione.

#### Example Workflow (no new code block)  
1. Inizializza `Redactor` con la tua licenza.  
2. Carica il PDF usando `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` rappresenta una regola che specifica il testo o il pattern da redigere. Definisci pattern come `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Esegui `redactor.Apply(pattern)`.  
5. Salva l'output con `redactor.Save("sample_redacted.pdf")`.

### Applicazioni pratiche

#### Casi d'uso reali
1. **Gestione dei documenti legali** – Ricerca efficiente dei contratti e redazione automatica degli identificatori dei clienti.  
2. **Cartelle cliniche** – Individua le note dei pazienti garantendo la redazione conforme a HIPAA dei dati sanitari (PHI).  
3. **Conformità aziendale** – Scansiona le comunicazioni interne per termini proibiti e redigili prima dell'archiviazione.

## Conclusione 
Questa guida fornisce un percorso completo per **creare un indice di ricerca .NET** che scala, indicizza rapidamente e protegge i dati tramite redazione. Configurando i nodi, indicizzando i documenti, sfruttando le funzionalità di ricerca avanzata e applicando la redazione, gli sviluppatori possono migliorare notevolmente i flussi di lavoro di gestione dei documenti mantenendo standard di sicurezza rigorosi.

## Domande frequenti

**D: Come configuro una rete di ricerca distribuita in .NET con GroupDocs?**  
R: Definisci un percorso base e una porta, quindi chiama `SearchNetworkDeployment.Deploy()` per avviare i nodi master e worker su più macchine.

**D: Posso eseguire ricerche avanzate con più parametri in GroupDocs?**  
R: Sì — usa `SearchOptions` per combinare la corrispondenza fuzzy, il supporto ai wildcard e l'evidenziazione dei risultati in una singola query.

**D: È possibile monitorare l'attività della rete sul nodo master?**  
R: Assolutamente — sottoscrivi `SearchNetworkNodeEvents` come `IndexingCompleted` e `QueryExecuted` per informazioni in tempo reale.

**D: Come applico la redazione ai file PDF usando GroupDocs?**  
R: Inizializza un `Redactor`, carica il PDF, definisci oggetti `RedactionPattern` (regex o stringhe letterali), chiama `Apply` e salva il documento sanificato.

**D: Qual è il modo più semplice per migliorare le prestazioni di ricerca in un ambiente di rete?**  
R: Indicizza completamente il tuo set di documenti prima delle query, distribuisci i nodi per utilizzare l'elaborazione parallela e ottimizza `SearchOptions` per caching e paginazione.

---

**Ultimo aggiornamento:** 2026-06-12  
**Testato con:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Master .NET Document Indexing with GroupDocs.Search&#58; Guida completa](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Master Document Indexing and Advanced Search Queries with GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Mastering GroupDocs Search and Redaction in .NET&#58; Gestione avanzata dei documenti](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)