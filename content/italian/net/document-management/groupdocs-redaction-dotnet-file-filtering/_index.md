---
date: '2026-04-21'
description: Impara come filtrare i file usando GroupDocs.Redaction per .NET, inclusi
  il filtro per data di creazione, dimensione del file, data di modifica e come applicare
  filtri NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Come filtrare i file con GroupDocs.Redaction per .NET
type: docs
url: /it/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Come filtrare i file con GroupDocs.Redaction per .NET

Nell'odierno ambiente digitale in rapida evoluzione, **come filtrare i file** in modo efficiente può fare la differenza nella tua produttività. Che tu debba isolare i documenti per estensione, data di creazione, dimensione o data di modifica, una solida strategia di filtraggio fa risparmiare tempo, riduce i costi di archiviazione e mantiene pulito l'indice di ricerca. In questo tutorial vedremo esempi pratici usando GroupDocs.Redaction per .NET, mostrandoti esattamente come filtrare i file per soddisfare le comuni esigenze aziendali.

## Risposte rapide
- **Quale libreria è necessaria?** GroupDocs.Redaction per .NET (installare via NuGet).  
- **Posso filtrare per data di creazione?** Sì – usa `CreateCreationTimeRange`.  
- **Come escludere determinati tipi?** Applica un filtro NOT con `DocumentFilter.CreateNot`.  
- **Il filtraggio per dimensione del file è supportato?** Assolutamente, tramite `CreateFileLengthRange` o limiti superiori/inferiori.  
- **È necessaria una licenza?** È richiesta una licenza di prova o completa per l'uso in produzione.

## Cos'è il filtraggio dei file con GroupDocs.Redaction?
Il filtraggio dei file consente di indicare al motore di indicizzazione quali documenti includere o ignorare in base a metadati come estensione, date, pattern di percorso o dimensione. Definendo regole precise di `DocumentFilter`, mantieni l'indice snello e le ricerche veloci.

## Perché usare GroupDocs.Redaction per .NET?
- **Helper di filtro integrati** – non è necessario scrivere codice personalizzato per il file system.  
- **Operatori logici** – combina più criteri con AND, OR e NOT.  
- **Ottimizzato per le prestazioni** – i filtri vengono applicati durante l'indicizzazione, non dopo.  
- **Cross‑platform** – funziona con .NET Framework, .NET Core e .NET 5/6+.

## Prerequisiti
- .NET Framework 4.6+ o .NET Core 3.1+ installato.  
- Visual Studio o il tuo IDE C# preferito.  
- Conoscenze di base di C#.

### Librerie richieste e configurazione
Installa il pacchetto NuGet usando il metodo che preferisci:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Suggerimento:** Dopo l'installazione, aggiungi il file di licenza nella radice del progetto e chiama `License.SetLicense("license-file-path")` prima di creare qualsiasi oggetto Redactor o Index.

## Configurare GroupDocs.Redaction per .NET

Per prima cosa, crea un'istanza di `Redactor` che punti al documento con cui vuoi lavorare:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Perché è importante:** Inizializzare il Redactor garantisce che la libreria sia pronta ad applicare filtri e regole di redazione più avanti nel flusso di lavoro.

## Come filtrare i file per estensione

Filtrare per estensione del file è il modo più comune per restringere un insieme di documenti. Di seguito manteniamo solo i file FB2, EPUB e TXT.

### Filtra per estensione del file

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Come applicare un filtro NOT per escludere tipi indesiderati

Se hai bisogno di **applicare la logica del filtro NOT** — ad esempio, escludere file HTML e PDF — usa `CreateNot`.

### Escludi file HTM, HTML e PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Come filtrare i file per data di creazione

Quando è necessario **filtrare per data di creazione**, specifica un `DateTime` di inizio e fine.

### Filtra per intervallo di data di creazione

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Come filtrare i file per data di modifica

Simile alle date di creazione, puoi limitare i risultati ai file modificati prima di un certo momento.

### Filtra per data di modifica

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Come filtrare i file per percorso usando espressioni regolari

Se la struttura delle cartelle segue convenzioni di denominazione, una regex può mirare a percorsi specifici.

### Filtra per pattern di percorso del file

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Come filtrare i file per dimensione

Controllare la dimensione dei documenti è essenziale quando si gestiscono limiti di larghezza di banda o di archiviazione.

### Filtra per dimensione del file (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Come combinare più condizioni con AND

Quando è necessario **filtrare i file** usando più criteri contemporaneamente, combinateli con `CreateAnd`.

### Esempio di AND logico

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Come combinare più condizioni con OR

Usa `CreateOr` quando una qualsiasi delle diverse regole deve essere soddisfatta.

### Esempio di OR logico

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Problemi comuni e soluzioni
- **Filtro non applicato:** Assicurati di assegnare `settings.DocumentFilter` **prima** di creare l'istanza `Index`.  
- **Appaiono file inattesi:** Verifica che le estensioni dei file includano il punto iniziale (`.txt`).  
- **Rallentamento delle prestazioni:** Combina i filtri con AND per ridurre il numero di file scansionati nelle prime fasi della pipeline di indicizzazione.  
- **Errori di regex:** Escapa i caratteri speciali nel pattern di percorso o usa `RegexOptions.IgnoreCase` per corrispondenze senza distinzione tra maiuscole e minuscole.

## Domande frequenti

**Q: Posso combinare un filtro NOT con un filtro AND?**  
A: Sì. Costruisci prima il filtro NOT (`DocumentFilter.CreateNot`) e poi includilo come uno degli argomenti di `DocumentFilter.CreateAnd`.

**Q: Come filtro i file più grandi di 10 MB?**  
A: Usa `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` per includere solo i file che superano quella dimensione.

**Q: È possibile filtrare sia per data di creazione sia per data di modifica simultaneamente?**  
A: Assolutamente. Crea ogni filtro separatamente e combinateli con `CreateAnd`.

**Q: Questi filtri funzionano con percorsi di archiviazione cloud?**  
A: I filtri operano sul file system locale. Per le fonti cloud, scarica i file in una cartella temporanea prima, quindi applica gli stessi filtri.

**Q: Modificare il filtro richiederà una re‑indicizzazione?**  
A: Sì. I filtri vengono valutati quando chiami `index.Add`. Cambiare un filtro significa che devi ricostruire l'indice per riflettere i nuovi criteri.

## Conclusione

Padroneggiando **come filtrare i file** con GroupDocs.Redaction per .NET — sia per estensione, data di creazione, data di modifica, dimensione del file o usando la logica NOT — puoi ottimizzare la gestione dei documenti, mantenere gli indici performanti e concentrarti sul contenuto che conta davvero. Sperimenta con gli operatori logici per adattare il filtraggio alle tue regole aziendali precise, e vedrai guadagni immediati in velocità ed efficienza di archiviazione.

---

**Ultimo aggiornamento:** 2026-04-21  
**Testato con:** GroupDocs.Redaction 24.11 for .NET  
**Autore:** GroupDocs  

---