---
date: '2026-06-07'
description: Scopri come aggiornare l'indice in modo efficiente con GroupDocs.Search
  e Redaction per .NET, migliorando il tuo sistema di gestione dei documenti.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Come aggiornare l'indice con GroupDocs.Search e Redaction (.NET)
type: docs
url: /it/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Come aggiornare l'indice con GroupDocs.Search & Redaction (.NET)

In moderne imprese guidate dai dati, **how to update index** in modo rapido e affidabile può fare la differenza nell'esperienza di ricerca. Che tu stia gestendo migliaia di contratti o un vasto knowledge base, mantenere l'indice di ricerca sincronizzato con le ultime modifiche ai documenti è essenziale per risultati veloci e accurati. Questo tutorial ti guida nell'uso di GroupDocs.Search per .NET insieme a GroupDocs.Redaction per **update index** file, gestire indici versionati e proteggere contenuti sensibili—tutto all'interno di un progetto .NET pulito.

## Risposte rapide
- **What does “how to update index” mean?** È il processo di modifica di un indice di ricerca esistente affinché i documenti nuovi o modificati diventino ricercabili senza ricostruire da zero.  
- **Which libraries are required?** GroupDocs.Search e GroupDocs.Redaction per .NET (entrambi disponibili via NuGet).  
- **Do I need a license?** Una prova gratuita funziona per i test; una licenza di produzione sblocca tutte le funzionalità.  
- **Can I run this on .NET Core?** Sì, le librerie supportano .NET Framework 4.5+, .NET Core 3.1+, e .NET 5/6+.  
- **What performance can I expect?** Aggiornare un indice da 1 GB con 2 thread termina in meno di un minuto su un tipico server a 4 core.

## Cos'è “how to update index”?
**How to update index** si riferisce alla tecnica di applicare modifiche incrementali a un indice di ricerca esistente anziché ricrearlo completamente. Questo approccio riduce i tempi di inattività, risparmia cicli CPU e mantiene i risultati di ricerca aggiornati man mano che i documenti vengono aggiunti, modificati o rimossi.

## Perché usare GroupDocs.Search e Redaction per gli aggiornamenti dell'indice?
GroupDocs.Search supporta **50+ formati di file** (PDF, DOCX, XLSX, PPTX, HTML, immagini, ecc.) e può elaborare documenti di centinaia di pagine senza caricare l'intero file in memoria. Combinato con GroupDocs.Redaction, è possibile rimuovere o mascherare automaticamente dati sensibili prima dell'indicizzazione, garantendo la conformità mantenendo la rilevanza della ricerca.

## Prerequisiti

- **GroupDocs.Search** – installa via NuGet.  
- **GroupDocs.Redaction for .NET** – necessario per le funzionalità di redazione.  
- Visual Studio (o qualsiasi IDE .NET) con .NET 6+ installato.  
- Conoscenza di base di C# e familiarità con i concetti di indicizzazione.

### Librerie richieste e versioni
- **GroupDocs.Search** – ultima versione stabile disponibile su NuGet.  
- **GroupDocs.Redaction for .NET** – ultima versione stabile disponibile su NuGet.

### Requisiti di configurazione dell'ambiente
- Una macchina Windows o Linux con .NET SDK installato.  
- Accesso a una cartella dove verranno memorizzati i file dell'indice.

### Prerequisiti di conoscenza
- Comprensione dei fondamenti di indicizzazione dei documenti e della ricerca.  
- Consapevolezza della gestione del ciclo di vita dei documenti nei sistemi aziendali.

## Configurazione di GroupDocs.Redaction per .NET

### Installa i pacchetti

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Cerca “GroupDocs.Redaction” e installa l'ultima versione.

### Passaggi per l'acquisizione della licenza
1. **Free Trial** – inizia con una prova per esplorare tutte le funzionalità.  
2. **Temporary License** – richiedi una chiave temporanea per test più estesi.  
3. **Purchase** – ottieni una licenza completa per le distribuzioni in produzione.

### Inizializzazione e configurazione di base
`Redactor` è la classe principale che applica le regole di redazione ai documenti.  
Per iniziare, importa lo spazio dei nomi Redaction e crea un'istanza di `Redactor`:

```csharp
using GroupDocs.Redaction;
```

Questo ti prepara ad applicare le regole di redazione prima di inserire i documenti nell'indice di ricerca.

## Guida all'implementazione

Tratteremo due funzionalità principali: aggiornare i documenti indicizzati e mantenere il controllo della versione dell'indice.

### Come aggiornare l'indice usando GroupDocs.Search?

`Index` rappresenta la collezione ricercabile memorizzata su disco.  
`UpdateOptions` configura come vengono eseguiti gli aggiornamenti incrementali (ad es. numero di thread).  
`UpdateDocument` applica le modifiche a un singolo documento, e `Commit` finalizza tutti gli aggiornamenti in sospeso.

**Direct answer (40‑70 words):**  
Crea un oggetto `Index` puntando alla cartella del tuo indice, usa `UpdateOptions` per specificare il numero di thread, chiama `UpdateDocument` per ogni file modificato e infine invoca `Commit` per persistere le modifiche. Questo approccio incrementale aggiorna solo le parti modificate, mantenendo l'indice corrente senza una ricostruzione completa.

#### Funzione 1: Aggiornare i documenti indicizzati

##### Panoramica
Aggiornare i documenti indicizzati garantisce che i risultati di ricerca riflettano il contenuto più recente, anche quando i documenti vengono modificati o sostituiti.

##### Passo 1: Creare un indice  
La classe `Index` è l'oggetto di livello superiore che rappresenta una collezione ricercabile su disco.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Passo 2: Aggiungere documenti all'indice  
Aggiungi file da una directory; la libreria estrae automaticamente il testo ricercabile.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Passo 3: Ricerca e aggiornamento  
Esegui una query, modifica il file sorgente, quindi chiama `UpdateDocument` con le stesse `UpdateOptions` usate durante l'indicizzazione.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Why This Works:** Impostando `Threads = 2`, l'aggiornamento sfrutta due core CPU, riducendo il tempo di elaborazione di circa la metà su una macchina quad‑core.

### Come mantenere il controllo della versione dell'indice?

`IndexUpdater` è una classe di utilità che aggiorna formati di indice più vecchi alla versione più recente supportata dalla libreria.  

**Direct answer (40‑70 words):**  
Istanzia `IndexUpdater` con il percorso del tuo indice esistente, chiama `CanUpdateVersion()` per verificare la compatibilità, quindi esegui `UpdateVersion()` se necessario. Dopo l'aggiornamento, ricarica l'indice con il nuovo formato ed esegui una ricerca per confermare che tutto funzioni. Questo garantisce una migrazione senza interruzioni tra le versioni della libreria.

#### Funzione 2: Mantenere il controllo della versione dell'indice

##### Panoramica
Il controllo della versione assicura che gli indici più vecchi rimangano ricercabili dopo un aggiornamento della libreria.

##### Passo 1: Verificare la compatibilità  
`IndexUpdater` controlla se l'indice corrente può essere aggiornato al formato più recente.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Passo 2: Caricare e cercare  
Dopo l'aggiornamento, carica l'indice aggiornato ed esegui una query per verificare l'integrità.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Why This Works:** La guardia `CanUpdateVersion` previene eccezioni a runtime causate da schemi di indice non corrispondenti, offrendo un percorso di aggiornamento sicuro.

## Applicazioni pratiche

Scenari reali in cui **how to update index** è fondamentale:

1. **Gestione documenti legali** – Reindicizza rapidamente i contratti dopo le modifiche, redigendo le clausole riservate.  
2. **Archivi aziendali** – Mantieni i record storici ricercabili senza dover riprocessare milioni di file.  
3. **Sistemi di gestione dei contenuti (CMS)** – Invia aggiornamenti incrementali all'indice di ricerca man mano che gli autori pubblicano nuovi articoli.

## Considerazioni sulle prestazioni

- **Threading Options:** Regola `UpdateOptions.Threads` in base ai core CPU; più thread migliorano il throughput ma aumentano l'uso di memoria.  
- **Resource Usage:** Monitora la RAM; la libreria streamma i file, quindi i picchi di memoria sono minimi anche per PDF di 500 pagine.  
- **Best Practices:** Pianifica aggiornamenti incrementali regolari e rimuovi versioni di indice obsolete per mantenere prestazioni ottimali.

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Index not found** | Percorso della cartella errato | Verifica che il costruttore `Index` punti alla directory corretta. |
| **Version mismatch error** | Uso di un indice più vecchio con una libreria più recente | Esegui il flusso `IndexUpdater` prima dell'indicizzazione normale. |
| **Redaction not applied** | Regole di redazione caricate dopo l'indicizzazione | Applica la redazione **prima** di aggiungere i documenti all'indice. |

## Domande frequenti

**Q: Qual è la differenza tra `UpdateDocument` e `Rebuild`?**  
A: `UpdateDocument` modifica solo i file cambiati, mentre `Rebuild` ricrea l'intero indice da zero, consumando più tempo e risorse.

**Q: Posso aggiornare più documenti in parallelo?**  
A: Sì, imposta `UpdateOptions.Threads` al numero di core che desideri utilizzare; la libreria gestisce il processamento parallelo internamente.

**Q: GroupDocs.Search supporta PDF criptati?**  
A: Assolutamente. Fornisci la password tramite `SearchOptions.Password` quando carichi il documento.

**Q: Come verifico che la redazione sia avvenuta con successo prima dell'indicizzazione?**  
A: Chiama `Redactor.Apply()` e controlla la dimensione del file di output; una dimensione ridotta indica spesso una redazione efficace.

**Q: Quali versioni .NET sono ufficialmente supportate?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 e .NET 6+.

## Conclusione

Ora disponi di una guida completa e pronta per la produzione su **how to update index** usando GroupDocs.Search e su come mantenere quegli indici compatibili con le versioni di GroupDocs.Redaction per .NET. Seguendo i passaggi sopra, potrai garantire che il tuo livello di ricerca rimanga veloce, accurato e conforme alle normative sulla privacy dei dati.

**Passaggi successivi:**  
- Sperimenta con impostazioni `Threads` diverse per trovare il punto ottimale per il tuo hardware.  
- Esplora pattern di redazione avanzati (ad es. rimozione SSN basata su regex) prima dell'indicizzazione.  
- Integra la routine di aggiornamento dell'indice nel tuo pipeline CI/CD per una gestione dei documenti completamente automatizzata.

---

**Ultimo aggiornamento:** 2026-06-07  
**Testato con:** GroupDocs.Search 23.10 per .NET, GroupDocs.Redaction 23.10 per .NET  
**Autore:** GroupDocs  

## Risorse
- [Documentazione](https://docs.groupdocs.com/search/net/)
- [Riferimento API](https://reference.groupdocs.com/redaction/net)
- [Scarica GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/search/10)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

## Tutorial correlati

- [Mastering GroupDocs.Redaction .NET: Efficient Index Creation and Alias Management for Advanced Document Search](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implement Synonym Search with GroupDocs.Redaction .NET for Enhanced Document Management](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Mastering GroupDocs Search and Redaction in .NET: Advanced Document Management](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)