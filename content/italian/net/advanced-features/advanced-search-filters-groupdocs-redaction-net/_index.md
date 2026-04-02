---
date: '2026-04-02'
description: Scopri come filtrare per estensione di file e cercare solo i file txt
  con GroupDocs.Redaction per .NET—migliora l'efficienza della gestione dei documenti.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtra per estensione del file in .NET usando GroupDocs.Redaction
type: docs
url: /it/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filtra per estensione file in .NET usando GroupDocs.Redaction

Ricercare in una collezione enorme di file può risultare opprimente, soprattutto quando ti servono risultati solo da tipi di file specifici. In questo tutorial scoprirai **come filtrare per estensione file** con GroupDocs.Redaction per .NET, permettendoti di cercare solo file txt o qualsiasi altra estensione tu scelga. Ti guideremo nella configurazione sia di filtri basati sul tipo di file sia di filtri basati sul percorso, così potrai individuare rapidamente i documenti esatti di cui hai bisogno.

## Risposte rapide
- **Che cosa fa “filter by file extension”?** Limita una ricerca ai documenti che corrispondono a una determinata estensione file (ad es., *.txt).  
- **Perché usare GroupDocs.Redaction per questo?** Fornisce API di filtraggio integrate che sono veloci e facili da integrare.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per i test; è necessaria una licenza a pagamento per la produzione.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Posso combinare filtri per tipo di file e per percorso?** Sì—applica più filtri per ricerche altamente precise.

## Cosa imparerai
- Come **filtrare per estensione file** in modo che vengano cercati solo i file di testo.  
- Come configurare **filtri per percorso file** per restringere i risultati a cartelle specifiche o a schemi di denominazione.  
- Suggerimenti per mantenere il tuo indice veloce ed efficiente in termini di memoria.

## Prerequisiti

Prima di approfondire, assicurati di avere:

- **GroupDocs.Redaction Library** installata e compatibile con il tuo progetto .NET.  
- Un ambiente di sviluppo come Visual Studio o VS Code.  
- Conoscenze di base di C# e familiarità con la struttura di un progetto .NET.

## Configurazione di GroupDocs.Redaction per .NET

Per prima cosa, aggiungi la libreria al tuo progetto.

**Utilizzando .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Utilizzando Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Oppure individua “GroupDocs.Redaction” nell'interfaccia di NuGet Package Manager e installa l'ultima versione.

### Acquisizione della licenza

Puoi iniziare con una prova gratuita o richiedere una licenza temporanea. Per progetti a lungo termine, acquista una licenza dal sito ufficiale.

### Inizializzazione di base

Dopo aver installato il pacchetto, crea un indice che conterrà i riferimenti ai tuoi documenti:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Guida all'implementazione

### Funzione 1: Impostare un filtro per documenti di testo (.txt)

#### Come filtrare per estensione file per documenti di testo

1. **Definisci l'indice e le cartelle dei documenti**  
   Imposta i percorsi dove risiedono i tuoi file sorgente:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Crea un indice**  
   Carica tutti i file dalla cartella sorgente nell'indice:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Configura le opzioni di ricerca con un filtro per estensione file**  
   Indica al motore di considerare solo i file *.txt:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Esegui la ricerca**  
   Esegui una query; il filtro assicura che i file non di testo vengano ignorati:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Spiegazione*: Il metodo `Search` restituisce le corrispondenze che soddisfano il filtro, riducendo drasticamente il rumore e migliorando le prestazioni.

### Funzione 2: Filtri per percorso file

#### Perché usare filtri per percorso file?

A volte è necessario limitare le ricerche a una cartella di un dipartimento specifico o a un insieme di file che condividono una convenzione di denominazione. I filtri per percorso ti permettono di fare esattamente questo.

1. **Definisci l'indice e le cartelle dei documenti**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Crea un indice**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Configura le opzioni di ricerca con un'espressione regolare basata sul percorso**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Questa espressione regolare corrisponde a qualsiasi file il cui percorso completo contiene la parola “Lorem”, permettendoti di mirare a sottocartelle specifiche.

4. **Esegui la ricerca basata sul percorso**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Applicazioni pratiche
- **Gestione documenti legali** – Individua rapidamente i contratti pertinenti archiviati come file di testo semplice.  
- **Ricerca accademica** – Estrai solo le note di ricerca *.txt che appartengono a una cartella di progetto specifica.  
- **Report aziendali** – Filtra i report interni per percorso dipartimento (ad es., `/Finance/2025/`).  

## Considerazioni sulle prestazioni
- Indicizza solo i tipi di documento di cui hai realmente bisogno; i file non necessari aumentano la dimensione dell'indice e il tempo di ricerca.  
- Mantieni il tuo indice aggiornato con un job programmato che chiama `index.Add()` per file nuovi o modificati.  
- Usa espressioni regolari semplici; pattern eccessivamente complessi possono rallentare il motore di ricerca.  
- Dispone degli oggetti `Index` quando non sono più necessari per liberare memoria.

## Conclusione
Ora sai come **filtrare per estensione file** e applicare **filtri per percorso file** usando GroupDocs.Redaction per .NET. Queste tecniche ti offrono un controllo granulare sulle grandi collezioni di documenti, rendendo le ricerche più veloci e pertinenti. Successivamente, sperimenta combinando più filtri o integrando la ricerca in un flusso di lavoro di un'applicazione più ampia.

## Sezione FAQ

**Q1: Posso filtrare documenti diversi dai file di testo?**  
A1: Sì, GroupDocs.Redaction supporta molti formati. Cambia l'argomento in `CreateFileExtension` con l'estensione desiderata (ad es., ".pdf").

**Q2: Come aggiorno regolarmente il mio indice di ricerca?**  
A2: Pianifica un servizio in background o un cron job che esegue `index.Add()` sulle directory che vuoi mantenere aggiornate.

**Q3: C'è un impatto sulle prestazioni quando si filtra per percorso file?**  
A3: Le espressioni regolari ottimizzate correttamente hanno un impatto minimo, ma esegui sempre benchmark con il tuo set di dati.

**Q4: Posso combinare più filtri per ricerche più raffinate?**  
A4: Assolutamente. Puoi concatenare filtri o creare filtri compositi per mirare sia al tipo di file sia al percorso simultaneamente.

**Q5: Dove posso trovare più risorse su GroupDocs.Redaction?**  
A5: Visita la documentazione ufficiale su [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) per guide dettagliate e riferimenti API.

## Domande frequenti

**Q: Il `SearchDocumentFilter` funziona con file crittografati?**  
A: Il filtro stesso opera sui metadati del file, quindi i file crittografati vengono comunque indicizzati se fornisci le credenziali di decrittazione necessarie durante l'indicizzazione.

**Q: Posso usare i caratteri jolly invece di un'espressione regolare per il filtraggio del percorso?**  
A: L'API attualmente richiede un'espressione regolare, ma puoi simulare semplici jolly (ad es., `.*` per qualsiasi carattere).

**Q: Quanto può diventare grande l'indice prima di dover considerare lo sharding?**  
A: Indici di diverse centinaia di gigabyte possono trarre beneficio dallo splitting in più indici logici; testa le prestazioni man mano che la tua collezione cresce.

**Q: Esistono metodi integrati per rimuovere documenti dall'indice?**  
A: Sì—chiama `index.Delete(documentId)` o `index.DeleteAll()` per gestire le voci obsolete.

**Q: C'è un modo per visualizzare in anteprima i risultati della ricerca prima di caricare il documento completo?**  
A: L'oggetto `SearchResult` include informazioni di snippet che puoi mostrare nell'interfaccia senza aprire l'intero file.

## Risorse
- **Documentazione**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)  
- **Riferimento API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)  
- **Supporto gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licenza temporanea**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)  

---

**Ultimo aggiornamento:** 2026-04-02  
**Testato con:** GroupDocs.Redaction 23.12 for .NET  
**Autore:** GroupDocs