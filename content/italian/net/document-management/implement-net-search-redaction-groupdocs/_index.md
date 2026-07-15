---
date: '2026-06-12'
description: Scopri come cercare e redigere documenti in .NET con GroupDocs.Search
  e GroupDocs.Redaction, ottimizzando le prestazioni di ricerca e gestendo gli errori
  di indicizzazione.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Come cercare e redigere documenti in .NET usando GroupDocs.Search e GroupDocs.Redaction
type: docs
url: /it/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Cerca e Redigi Documenti in .NET con GroupDocs.Search & GroupDocs.Redaction

Negli ambienti aziendali moderni, le funzionalità di **search and redact** sono essenziali per proteggere le informazioni sensibili mantenendo i documenti facilmente rintracciabili. Questo tutorial ti guida nella creazione di una soluzione .NET robusta che combina GroupDocs.Search per una ricerca full‑text veloce con GroupDocs.Redaction per rimuovere in modo sicuro i dati riservati. Alla fine, saprai come configurare le librerie, creare un segmentatore di testo personalizzato, eseguire ricerche ad alte prestazioni e applicare le redazioni in modo sicuro.

## Risposte Rapide
- **Cosa significa “search and redact”?** Significa trovare il testo nei documenti e mascherarlo permanentemente.  
- **Quali librerie sono richieste?** GroupDocs.Search e GroupDocs.Redaction per .NET.  
- **Posso gestire contenuti multilingue?** Sì—usa un segmentatore di testo personalizzato per suddividere correttamente le parole.  
- **Come posso migliorare la velocità di ricerca?** Indicizza una volta, riutilizza l'indice e abilita le impostazioni `optimize search performance`.  
- **Cosa succede se l'indicizzazione fallisce?** Segui le linee guida “handle indexing errors” nella sezione di risoluzione dei problemi.

## Cos'è “search and redact”
Search and redact è il processo di individuare termini specifici all'interno di una collezione di documenti e poi oscurarli o rimuoverli permanentemente per proteggere la privacy o soddisfare i requisiti normativi. Combina la ricerca full‑text per trovare informazioni sensibili con strumenti di redazione che sostituiscono il contenuto mantenendo il layout originale del documento.

## Perché usare GroupDocs.Search e GroupDocs.Redaction insieme?
GroupDocs.Search supporta **oltre 50 formati di file** e può indicizzare **oltre 100.000 documenti** in meno di un minuto su hardware server tipico, mentre GroupDocs.Redaction può applicare redazioni a **PDF, DOCX, PPTX e altri** senza alterare il layout originale. Combinarli ti offre una soluzione a stack unico che **ottimizza le prestazioni di ricerca** e **gestisce gli errori di indicizzazione** in modo fluido.

## Prerequisiti
- Visual Studio 2022 o versioni successive con supporto .NET 6+.
- Pacchetti NuGet: **GroupDocs.Search** e **GroupDocs.Redaction** (ultime versioni stabili).
- Una licenza GroupDocs valida (trial o acquistata).

### Librerie Richieste
- **GroupDocs.Search** – Fornisce indicizzazione, interrogazione e segmentazione personalizzata.  
- **GroupDocs.Redaction** – Offre redazione di testo, immagini e metadati nei formati supportati.

### Requisiti per la Configurazione dell'Ambiente
Assicurati che la tua macchina di sviluppo abbia i permessi di scrittura sulla cartella in cui verrà memorizzato l'indice.

### Prerequisiti di Conoscenza
- Familiarità con C# e le strutture di progetto .NET.  
- Comprensione di base dei concetti di elaborazione dei documenti (facoltativa ma utile).

## Come installare GroupDocs.Redaction per .NET?
Puoi aggiungere il pacchetto Redaction al tuo progetto usando sia la .NET CLI sia il NuGet Package Manager. Il comando scarica l'ultima versione stabile e la registra nel file di progetto, rendendo l'API disponibile immediatamente.  

```bash
dotnet add package GroupDocs.Redaction
```  

## Come ottenere una licenza per GroupDocs?
GroupDocs offre tre opzioni di licenza: una prova gratuita per la valutazione, una licenza temporanea per test di sviluppo prolungati e una licenza commerciale completa per l'uso in produzione. La prova fornisce funzionalità limitate, mentre la chiave temporanea estende il periodo di valutazione, e la licenza acquistata sblocca tutte le funzionalità e il supporto prioritario.

## Come inizializzare GroupDocs.Redaction nella mia applicazione?
La classe `Redaction` è il punto di ingresso principale per applicare redazioni ai documenti supportati. Carica un file, prepara gli oggetti di redazione ed esegue il processo di redazione, restituendo un documento modificato mantenendo il layout originale. È inoltre possibile configurare le opzioni di redazione come colore, sovrapposizione e rimozione dei metadati per soddisfare requisiti di conformità specifici.  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Come configurare un indice usando GroupDocs.Search?
La classe `Index` rappresenta un repository ricercabile memorizzato su disco. Gestisce la creazione, l'aggiornamento e l'interrogazione dell'indice, consentendo di aggiungere documenti, ricostruire l'indice ed eseguire ricerche rapide su grandi collezioni. La cartella dell'indice può trovarsi su storage locale o di rete, e puoi configurare le impostazioni di compressione e crittografia per proteggere i dati indicizzati.  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Cos'è un Segmentatore di Testo Personalizzato e perché usarlo?
Un segmentatore di testo personalizzato determina come il testo grezzo viene suddiviso in token ricercabili. Personalizzando le regole di segmentazione per lingue o domini specifici, migliori l'accuratezza della tokenizzazione, ottenendo un richiamo e una pertinenza più elevati nei risultati di ricerca. Questo è particolarmente utile per lingue con confini di parola complessi, come il giapponese o l'arabo, dove i tokenizzatori predefiniti possono suddividere le parole in modo errato.  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Come eseguire una ricerca full‑text con il segmentatore personalizzato?
L'oggetto `SearchQuery` incapsula la query dell'utente e lavora con il segmentatore personalizzato per individuare le corrispondenze. Supporta il fuzzy matching, le query di frase e il weighting, restituendo un set di risultati con ID documento, posizioni dei risultati e punteggi di rilevanza. È inoltre possibile applicare filtri come tipo di file o intervallo di date per restringere i risultati e ottenere un targeting più preciso.  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Come applicare le redazioni dopo aver trovato il testo sensibile?
L'API `Redaction` ti consente di sostituire o rimuovere testo, immagini e metadati nei documenti supportati. Dopo aver identificato i termini sensibili, crei oggetti di redazione, li applichi e salvi il file redatto, garantendo che le informazioni riservate siano nascoste permanentemente. Le opzioni di redazione includono la sovrapposizione di riquadri neri, l'applicazione di colori personalizzati o la rimozione di interi oggetti mantenendo la struttura del documento.  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## Problemi comuni e come gestire gli errori di indicizzazione
- **Index Not Found:** Verifica che il percorso dell'indice esista e che l'applicazione abbia i permessi di lettura/scrittura.  
- **Search Returns No Results:** Riesegui il processo di indicizzazione e assicurati che il segmentatore personalizzato sia correttamente registrato.  
- **Redaction Fails on Certain Formats:** Conferma che il tipo di file sia supportato; per i PDF, utilizza l'ultima versione di Redaction per gestire le funzionalità PDF 2.0.

## Applicazioni pratiche
1. **Gestione dei Documenti Legali:** Cerca contratti per “non‑disclosure” e redigi automaticamente le clausole prima della condivisione esterna.  
2. **Ricerca Accademica:** Individua dati non pubblicati nei manoscritti e nascondili per i processi di revisione tra pari.  
3. **Contratti Aziendali:** Elabora in batch migliaia di accordi, redigendo gli identificatori personali mantenendo il linguaggio legale.

## Come ottimizzare le prestazioni di ricerca per grandi insiemi di documenti?
Per massimizzare le prestazioni, indicizza i documenti una volta e riutilizza lo stesso indice per le query successive. Abilita l'elaborazione parallela, configura la cache e ottimizza le impostazioni dell'indice per ridurre la latenza e migliorare il throughput su server multi‑core. Inoltre, imposta il flag `EnableMemoryMapping` per consentire che l'indice sia mappato in memoria, accelerando le operazioni di lettura per grandi set di dati.

## Come gestire la memoria .NET quando si lavora con file di grandi dimensioni?
Una gestione efficiente della memoria è fondamentale quando si gestiscono documenti di grandi dimensioni. Avvolgi gli oggetti `Index` e `Redaction` in istruzioni `using` per garantire una disposizione deterministica, ed elabora i file come stream anziché caricare interi documenti in memoria. Il monitoraggio dei contatori di prestazioni aiuta a rilevare picchi di memoria in anticipo, consentendoti di regolare le dimensioni dei batch o abilitare la sintonizzazione della garbage collection.

## Domande frequenti
**Q: Posso usare GroupDocs.Search con metadati non testuali?**  
A: Sì—i campi di metadati possono essere indicizzati insieme al contenuto del documento, consentendo ricerche come “author:JohnDoe”.

**Q: GroupDocs.Redaction supporta la redazione in tempo reale in una web API?**  
A: Sì; puoi invocare l'API Redaction in modo sincrono per file piccoli o mettere in coda lavori più grandi per l'elaborazione asincrona.

**Q: Cosa devo fare se l'indice diventa corrotto?**  
A: Elimina la cartella dell'indice corrotta e ricostruiscila usando la stessa routine di indicizzazione; la libreria registra messaggi di errore dettagliati per aiutarti a individuare la causa.

**Q: È possibile visualizzare in anteprima i documenti redatti prima di salvarli?**  
A: Assolutamente—chiama `redaction.Apply()` con il flag `preview` per generare una versione temporanea da revisionare.

**Q: Quali versioni .NET sono ufficialmente supportate?**  
A: GroupDocs.Search e GroupDocs.Redaction supportano .NET 6, .NET 5, .NET Core 3.1 e .NET Framework 4.6.2+.

## Risorse
- **Documentazione:** [Documentazione GroupDocs Redaction](https://docs.groupdocs.com/search/net/)
- **Riferimento API:** [Riferimento API GroupDocs](https://reference.groupdocs.com/redaction/net)
- **Download:** [Rilasci GroupDocs](https://releases.groupdocs.com/search/net/)
- **Supporto gratuito:** [Forum GroupDocs](https://forum.groupdocs.com/c/search/10)
- **Licenza temporanea:** [Licenza temporanea GroupDocs](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-12  
**Tested With:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Tutorial correlati
- [Padroneggiare GroupDocs Search e Redaction in .NET: Gestione avanzata dei documenti](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [Implementare GroupDocs.Search & Redaction: Aggiornare e gestire gli indici dei documenti in .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Ottimizzare l'indicizzazione dei documenti in .NET con GroupDocs.Redaction: Cancellazione, Async e Thread](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)