---
date: '2026-06-07'
description: Scopri come implementare l'alta compressione .NET per l'archiviazione
  di testo e redigere dati riservati utilizzando GroupDocs.Search e GroupDocs.Redaction
  nelle applicazioni .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Implementare l''alta compressione .NET con GroupDocs: Guida a Testo e Redazione'
type: docs
url: /it/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementare l'alta compressione .NET con GroupDocs: Guida a Testo e Redazione

Nelle soluzioni .NET moderne, **implement high compression .net** è essenziale quando è necessario archiviare collezioni di testo massive senza aumentare eccessivamente l'uso del disco. Allo stesso tempo, proteggere le informazioni sensibili — come identificatori personali o dati finanziari — richiede una redazione affidabile. Questo tutorial mostra, passo‑a‑passo, come configurare l'archiviazione di testo ad alta compressione con **GroupDocs.Search** e come redigere in modo sicuro i dati riservati usando **GroupDocs.Redaction**. Alla fine, sarai in grado di comprimere il testo indicizzato fino al 90 % e rimuovere contenuti privati da PDF, file Word e molti altri formati.

## Risposte Rapide
- **Quale libreria fornisce indicizzazione ad alta compressione?** GroupDocs.Search for .NET.  
- **Quale strumento redige i dati sensibili?** GroupDocs.Redaction for .NET.  
- **Posso aggiungere documenti all'indice automaticamente?** Yes—use the `AddDocument` API inside a folder‑scan loop.  
- **La compressione è senza perdita per la ricerca?** Yes, the text remains fully searchable after compression.  
- **È necessaria una licenza per la produzione?** A permanent GroupDocs license is required for commercial use.

## Che cos'è “implement high compression .net”?
Implementare l'alta compressione .net significa configurare il motore di indicizzazione GroupDocs.Search per memorizzare il contenuto testuale estratto in forma compressa. Questo riduce drasticamente le dimensioni dell'indice su disco mantenendo il testo completamente ricercabile. La compressione è senza perdita, quindi la rilevanza delle query e l'estrazione dei frammenti funzionano esattamente come con un indice non compresso.

## Perché usare GroupDocs per compressione e redazione?
GroupDocs.Search supporta più di cinquanta formati di input e può comprimere il testo indicizzato fino al novanta percento, consentendo a grandi collezioni di documenti di occupare solo una frazione delle loro dimensioni originali. GroupDocs.Redaction completa questo cancellando o mascherando permanentemente le informazioni sensibili in oltre trenta tipi di file, aiutandoti a rispettare normative di conformità rigorose come GDPR e HIPAA senza strumenti aggiuntivi.

## Prerequisiti
- **Ambiente di sviluppo:** Visual Studio 2022 or later, .NET 6+ (or .NET Framework 4.7.2).  
- **Librerie:** `GroupDocs.Search` and `GroupDocs.Redaction` NuGet packages.  
- **Permessi:** Read/write access to the folders that contain source documents and the index output location.  
- **Conoscenze di base:** C# syntax, file I/O, and familiarity with .NET project structure.

## Come implementare l'alta compressione .NET con GroupDocs?
Per implementare l'alta compressione .NET con GroupDocs, crea prima un'istanza di `TextStorageSettings` e imposta il suo `CompressionLevel` su `High`. Quindi istanzia un oggetto `Index`, passando le impostazioni e la cartella dove verrà memorizzato l'indice. Dopo che l'indice è pronto, aggiungi i documenti usando `AddDocument` e infine esegui le ricerche con il metodo `Search`, il tutto mentre il motore gestisce in modo trasparente la compressione e la decompressione.

### Passo 1: Installa i pacchetti NuGet richiesti
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Search for “GroupDocs.Search” and click **Install**.  

### Passo 2: Installa GroupDocs.Redaction (per la redazione dei dati)
- Open the **NuGet Package Manager**.  
- Search for **GroupDocs.Redaction** and install the latest stable version.  

### Passo 3: Ottieni e applica una licenza
- **Prova gratuita:** Register on the GroupDocs portal for a 30‑day trial key.  
- **Licenza temporanea:** Request a temporary key for development environments.  
- **Licenza permanente:** Purchase a production license to remove evaluation limitations.

### Passo 4: Inizializzazione di base di entrambe le librerie
Il motore `Search` e `Redaction` condividono un modello di licenza comune. Inizializzali all'avvio dell'applicazione:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Funzionalità 1: Impostazioni di archiviazione del testo ad alta compressione

### Configurazione dell'indicizzazione
`TextStorageSettings` è la classe che indica a GroupDocs.Search come conservare il testo estratto. Abilitare l'alta compressione riduce le dimensioni dell'indice fino a **10×** senza influire sulla velocità di ricerca.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Spiegazione:**  
- `CompressionLevel.High` attiva un algoritmo basato su ZSTD che comprime i blocchi di testo in modo efficiente.  
- `UseMemoryCache = false` costringe il motore a trasmettere i dati dal disco, ideale per distribuzioni su larga scala.

### Creazione e gestione dell'indice
L'oggetto `Index` rappresenta il repository ricercabile su disco. Specifici la cartella dove verranno memorizzati i file dell'indice e passi le impostazioni di compressione definite sopra.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Spiegazione:**  
- `indexFolder` determina dove risiedono i file dell'indice compresso.  
- `settings` inietta la configurazione ad alta compressione, garantendo che ogni documento aggiunto ne benefici.

## Funzionalità 2: Aggiungere documenti all'indice

### Aggiungi documenti al tuo indice
`AddDocument` aggiunge un singolo file all'indice, estraendo il suo testo, comprimendolo secondo le impostazioni configurate e memorizzando il risultato. GroupDocs.Search può ingerire file da un albero di directory. Il ciclo seguente attraversa `documentsFolder`, aggiunge ogni file e registra i progressi.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Spiegazione:**  
- `AddDocument` analizza il file, estrae il testo ricercabile, lo comprime secondo `TextStorageSettings` e lo memorizza nell'indice.  
- Questo approccio funziona per **PDF, DOCX, TXT, HTML** e più di **30** altri formati.

## Funzionalità 3: Eseguire una query di ricerca

### Esegui una ricerca
`Search` esegue una query sull'indice compresso e restituisce una collezione di oggetti `DocumentResult` corrispondenti con punteggi di rilevanza e frammenti evidenziati. Una volta che l'indice è popolato, puoi eseguire query rapide. Il metodo `Search` restituisce una collezione di oggetti `DocumentResult` che includono percorsi dei file e frammenti evidenziati.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Spiegazione:**  
- Il motore di ricerca analizza direttamente il testo compresso, quindi la latenza delle query rimane bassa anche per indici che contengono **milioni di pagine**.  
- `Score` indica la rilevanza; valori più alti indicano una corrispondenza migliore.

## Come redigere dati riservati con GroupDocs.Redaction?
Redigere dati riservati con GroupDocs.Redaction inizia creando un'istanza `Redactor` per il file di destinazione. Definisci uno o più oggetti `SearchPattern` che descrivono il testo da rimuovere, come espressioni regolari per i numeri di previdenza sociale. Applica ogni pattern usando `Redact`, specificando un `RedactionType` come `BlackOut`, e salva il risultato come un nuovo documento, garantendo che l'originale rimanga intatto.

`Redactor` è la classe principale in GroupDocs.Redaction usata per caricare un documento ed eseguire operazioni di redazione.  
`SearchPattern` definisce un'espressione regolare che identifica il testo da redigere.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Spiegazione:**  
- `SearchPattern` utilizza un'espressione regolare per individuare i numeri di previdenza sociale.  
- `RedactionType.BlackOut` sostituisce il testo corrispondente con un rettangolo nero solido, garantendo che i dati non possano essere recuperati.

## Applicazioni pratiche
1. **Gestione documenti legali:** Comprimi automaticamente file di casi massivi e redigi gli identificatori dei clienti prima dell'archiviazione.  
2. **Cartelle cliniche:** Archivia anni di note dei pazienti in un indice compresso e rimuovi le PHI (Informazioni Sanitarie Protette) prima di condividerle con partner di ricerca.  
3. **Report finanziari:** Metti al sicuro i report trimestrali redigendo i numeri di conto mantenendo il testo ricercabile per le query di audit.

## Considerazioni sulle prestazioni
- **Impatto della compressione:** High compression reduces index size by up to **90 %**, which lowers SSD wear and speeds up backup operations.  
- **Utilizzo della memoria:** Disable in‑memory caching for very large indexes to keep the process footprint under **500 MB**.  
- **Ottimizzazione I/O:** Batch document addition in groups of 100 to minimize disk thrashing.  
- **Elaborazione asincrona:** Wrap `AddDocument` calls in `Task.Run` to keep UI threads responsive in desktop apps.

## Problemi comuni e risoluzione dei problemi
- **Percorsi file errati:** Verify that `documentsFolder` and `indexFolder` are absolute paths and that the application has read/write permissions.  
- **Errori di licenza:** Ensure the `.lic` files are deployed alongside the executable or embedded as resources.  
- **La ricerca non restituisce risultati:** Check that the `TextStorageSettings` compression level matches the one used during indexing; mismatched settings can cause deserialization failures.  

## Domande frequenti

**Q: Posso aggiungere documenti all'indice dopo la costruzione iniziale?**  
A: Sì—basta chiamare `index.AddDocument` per i nuovi file; il motore aggiorna l'indice compresso in modo incrementale.

**Q: La redazione altera il file originale?**  
A: No—il file originale rimane intatto; la versione redatta viene salvata come un nuovo file, preservando l'integrità del documento.

**Q: Quali formati supporta GroupDocs.Redaction?**  
A: Oltre **30** formati, tra cui PDF, DOCX, PPTX, XLSX, immagini (PNG, JPEG) e testo semplice.

**Q: Come influisce l'alta compressione sulla rilevanza della ricerca?**  
A: Non influisce. La compressione è senza perdita per il testo, quindi i punteggi di rilevanza sono identici a quelli di un indice non compresso.

**Q: Esiste un limite alla dimensione dei documenti che posso indicizzare?**  
A: GroupDocs.Search può gestire file multi‑gigabyte trasmettendo il contenuto in streaming; tuttavia, assicurati di avere spazio su disco sufficiente per l'indice compresso (circa il 10 % della dimensione originale).

## Risorse
- [Documentazione](https://docs.groupdocs.com/search/net/)
- [Riferimento API](https://reference.groupdocs.com/redaction/net)
- [Scarica GroupDocs.Redaction per .NET](https://releases.groupdocs.com/search/net/)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/search/10)
- [Acquisizione licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-06-07  
**Testato con:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Implementare GroupDocs.Search e Redaction in .NET per la gestione dei documenti](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Come ottimizzare GroupDocs.Redaction per .NET: Guida alla gestione efficiente di indice e ortografia](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Padroneggiare GroupDocs Redaction e Search in .NET: Gestione efficiente dei documenti e ricerca sicura](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)