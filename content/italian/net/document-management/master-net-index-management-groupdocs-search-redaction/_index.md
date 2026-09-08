---
date: '2026-07-26'
description: Scopri come creare un indice in .NET utilizzando GroupDocs.Search e integrare
  la redazione con GroupDocs.Redaction, consentendo una ricerca rapida dei documenti
  e una gestione efficiente dei dati.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: Scopri come creare un indice in .NET utilizzando GroupDocs.Search
  e integrare la redazione con GroupDocs.Redaction, consentendo una ricerca rapida
  dei documenti e una gestione efficiente dei dati.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: Come creare un indice in .NET con l'API GroupDocs Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: Come creare un indice in .NET con l'API GroupDocs Search
type: docs
url: /it/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# Come creare indice in .NET con GroupDocs Search API

In questo tutorial scoprirai **come creare indice** per le tue applicazioni .NET usando GroupDocs.Search e poi proteggere i contenuti sensibili con GroupDocs.Redaction. Alla fine della guida sarai in grado di costruire, aggiornare e potare un indice ricercabile, e comprenderai perché combinare ricerca e redazione è una best‑practice per la gestione sicura dei documenti.

## Risposte rapide
- **Cosa significa “come creare indice”?** Significa costruire una struttura dati ricercabile che mappa il contenuto dei documenti a chiavi di ricerca rapide.  
- **Quali librerie sono necessarie?** GroupDocs.Search e GroupDocs.Redaction per .NET (pacchetti NuGet).  
- **Posso indicizzare PDF, Word e immagini?** Sì—oltre 150 formati sono supportati nativamente.  
- **Come elimino un documento dall'indice?** Chiama il metodo `Delete` con il percorso o l'ID del documento.  
- **La redazione avviene prima o dopo l'indicizzazione?** La redazione dovrebbe avvenire per prima, così i dati protetti non entrano mai nell'indice.

## Cos'è “come creare indice”?
La frase **come creare indice** si riferisce al processo di generazione di una struttura dati ricercabile che memorizza le mappature termine‑documento per un recupero rapido. In GroupDocs, questa struttura risiede su disco e può essere aggiornata in modo incrementale senza ricostruire l'intera collezione.

## Perché usare GroupDocs.Search e GroupDocs.Redaction insieme?
GroupDocs.Search supporta l'indicizzazione di **oltre 150 formati di file** e può gestire indici più grandi di **10 GB** mantenendo l'uso di memoria sotto i 200 MB perché trasmette i file in streaming anziché caricarli interamente. Aggiungere GroupDocs.Redaction garantisce che qualsiasi testo, immagine o metadato confidenziale venga rimosso prima che il contenuto raggiunga l'indice, garantendo la conformità a GDPR, HIPAA e altre normative.

## Prerequisiti
- **Librerie e versioni** – Installa gli ultimi pacchetti NuGet **GroupDocs.Search** e **GroupDocs.Redaction** compatibili con .NET 6 o versioni successive.  
- **IDE** – Visual Studio 2022 (o qualsiasi IDE che supporti .NET 6).  
- **Conoscenze** – Competenze di base in C#, familiarità con I/O di file e comprensione dei concetti di indicizzazione.

## Configurazione di GroupDocs.Redaction per .NET

### Installazione

**Utilizzando .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Utilizzando la console del Package Manager in Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Puoi anche trovare “GroupDocs.Redaction” nell'interfaccia del NuGet Package Manager e installare l'ultima versione stabile.

### Acquisizione della licenza

Puoi ottenere una prova gratuita o richiedere una licenza temporanea per esplorare tutte le funzionalità senza limitazioni. Visita [Pagina di acquisto di GroupDocs](https://purchase.groupdocs.com/temporary-license/) per ulteriori dettagli su come ottenere una licenza.

### Inizializzazione di base

Redactor è la classe principale che esegue le operazioni di redazione su un documento.  
Il frammento seguente mostra il codice minimo necessario per iniziare a usare GroupDocs.Redaction:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

Questa semplice configurazione è tutto ciò di cui hai bisogno per iniziare a usare GroupDocs.Redaction.

## Guida all'implementazione

### Come creare indice?

`Index` rappresenta il contenitore ricercabile che contiene i dizionari dei termini e i metadati dei documenti.  
Carica o crea un oggetto `Index`, puntalo a una cartella dove verranno archiviati i file dell'indice e chiama `Create`. L'operazione scrive i file di metadati necessari e prepara il motore per l'ingestione dei documenti.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### Passo 1: Creare l'indice
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### Come aggiungere documenti all'indice?

`Add` inserisce un singolo documento nell'indice, mentre `AddFolder` elabora tutti i file in una directory.  
Aggiungi file chiamando `Add` o `AddFolder`. Il motore legge ogni file supportato, estrae il testo e aggiorna il dizionario dei termini.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### Passo 2: Aggiungere cartelle di documenti
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### Come recuperare i percorsi indicizzati?

`GetIndexedPaths` restituisce una collezione di tutti i percorsi dei documenti memorizzati nell'indice.  
Recuperare l'elenco dei percorsi dei file indicizzati ti permette di verificare quali documenti sono attualmente ricercabili.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### Passo 3: Visualizzare i percorsi indicizzati
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### Come eliminare un documento dall'indice?

`Delete` rimuove un documento dall'indice tramite il suo percorso o identificatore.  
Quando un file viene rimosso o diventa obsoleto, dovresti eliminare la sua voce per mantenere accurati i risultati di ricerca.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### Passo 4: Eliminare percorsi specifici
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### Come verificare i percorsi indicizzati rimanenti dopo l'eliminazione?

Dopo la rimozione, puoi rieseguire il metodo di recupero per assicurarti che l'indice rifletta lo stato attuale.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### Passo 5: Verificare i percorsi rimanenti
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## Applicazioni pratiche

1. **Sistemi di gestione documentale** – Trova rapidamente contratti, fatture o manuali tra milioni di file.  
2. **Revisione di documenti legali** – Redigi le informazioni privilegiate prima dell'indicizzazione per evitare esposizioni accidentali.  
3. **Soluzioni di archiviazione** – Conserva metadati ricercabili per documenti storici senza caricare interi archivi in memoria.  
4. **Piattaforme di gestione dei contenuti** – Alimenta la ricerca a livello di sito per blog, basi di conoscenza e librerie multimediali.  
5. **Audit di conformità dei dati** – Garantisce che solo contenuti sanitizzati siano ricercabili, soddisfacendo i requisiti normativi.

## Considerazioni sulle prestazioni

- **Ottimizzare l'indicizzazione** – Pianifica l'indicizzazione incrementale notturna; usa `AddFolder` con una dimensione batch di 100 file per ridurre i picchi di I/O.  
- **Gestione delle risorse** – Monitora CPU e RAM; GroupDocs.Search elabora i file in streaming, mantenendo la memoria di picco sotto i 200 MB anche per indici da 10 GB.  
- **Best practice** – Conserva l'indice su SSD per risposte alle query inferiori a un secondo, e abilita la compressione (`index.Compression = true`) per dimezzare l'uso del disco.

## Domande frequenti

**D: Posso indicizzare file non testuali con GroupDocs?**  
R: Sì, GroupDocs.Search può indicizzare oltre 150 formati—incluse PDF, DOCX, PPTX, XLSX e tipi di immagine—estrapolando il testo incorporato tramite OCR quando necessario.

**D: Come gestisco grandi volumi di documenti?**  
R: Usa `AddFolder` con una dimensione batch configurabile, esegui l'indicizzazione in un servizio in background e chiama periodicamente `Optimize()` per unire piccoli segmenti dell'indice.

**D: Quali sono i vantaggi di usare la redazione con l'indicizzazione?**  
R: La redazione rimuove le informazioni personalmente identificabili prima che raggiungano l'indice, garantendo che i risultati di ricerca non espongano mai dati protetti.

**D: È possibile personalizzare gli algoritmi di ricerca?**  
R: GroupDocs.Search fornisce dizionari di sinonimi, tokenizzatori personalizzati e filtri di espressioni regolari, consentendo di affinare il punteggio di rilevanza.

**D: Come risolvo i problemi comuni di indicizzazione?**  
R: Verifica i permessi delle cartelle, assicurati che il runtime .NET corrisponda al target della libreria e controlla il file di log generato nella cartella dell'indice per messaggi di errore dettagliati.

## Risorse

- **Documentazione**: [Documentazione GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **Riferimento API**: [API GroupDocs Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Download**: [Ultime versioni GroupDocs](https://releases.groupdocs.com/search/net/)  
- **Supporto gratuito**: [Forum GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Licenza temporanea**: [Richiedi una licenza temporanea](https://purchase.groupdocs.com/temporary-license/)  

Esplora queste risorse per approfondire la tua comprensione e migliorare l'implementazione di GroupDocs.Search e Redaction in .NET. Buon coding!

---

**Ultimo aggiornamento:** 2026-07-26  
**Testato con:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 per .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Creazione e fusione di indice master con GroupDocs.Redaction .NET per una gestione documentale efficiente](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Padroneggiare GroupDocs.Redaction .NET: Creazione efficiente di indice e gestione alias per ricerca avanzata di documenti](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Master GroupDocs Search e Redaction in .NET: Guida completa per la gestione dei documenti](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)