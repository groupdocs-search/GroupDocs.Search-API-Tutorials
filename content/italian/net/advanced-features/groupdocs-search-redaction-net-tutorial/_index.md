---
date: '2026-04-04'
description: Scopri come cercare documenti legali e gestire gli indici utilizzando
  GroupDocs.Search e integrare la redazione per i record medici con GroupDocs.Redaction
  in .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Cerca documenti legali con GroupDocs Search & Redaction per .NET
type: docs
url: /it/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Cerca documenti legali con GroupDocs Search & Redaction in .NET

Nell’attuale ambiente guidato dai dati, **cercare documenti legali** rapidamente e in modo sicuro è un requisito critico per qualsiasi organizzazione. Che tu stia gestendo contratti, depositi giudiziari o rapporti di conformità, GroupDocs.Search ti offre un indice veloce e scalabile, mentre GroupDocs.Redaction garantisce che le informazioni sensibili rimangano nascoste. Questo tutorial ti guida nella creazione di un indice ricercabile, nell’aggiunta di documenti da più cartelle e nella configurazione della redazione così da poter cercare in sicurezza cartelle cliniche e altri file riservati.

## Risposte rapide
- **Che cosa fa GroupDocs.Search?** Crea un indice full‑text ricercabile per un’ampia gamma di formati di documento.  
- **Posso redigere le informazioni prima della ricerca?** Sì – usa GroupDocs.Redaction per mascherare o rimuovere i dati sensibili.  
- **Come aggiungo documenti all’indice?** Chiama `index.Add("folderPath")` per ogni cartella che desideri includere.  
- **Quali tipi di file sono supportati?** PDF, DOCX, PPTX, TXT e molti altri.  
- **È necessaria una licenza per la produzione?** È disponibile una prova temporanea; è richiesta una licenza permanente per l’uso commerciale.

## Prerequisiti
Per seguire questo tutorial, assicurati di avere:
- .NET Core SDK (3.1 o successivo) installato.
- Visual Studio Code, Visual Studio o un altro IDE che supporta .NET.
- Familiarità di base con la programmazione C#.

### Acquisizione della licenza
Puoi iniziare con una prova gratuita di entrambe le librerie. Per un utilizzo prolungato, considera di acquisire una licenza temporanea o di acquistarne una dal [sito web di GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Installazione dei pacchetti richiesti

**Installazione di GroupDocs.Search:**  
Usando **.NET CLI**, esegui:
```bash
dotnet add package GroupDocs.Search
```
In alternativa, usa la console Package Manager in Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**Installazione di GroupDocs.Redaction:**  
- Usa .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Oppure, tramite Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Visita l'interfaccia UI di NuGet Package Manager e cerca "GroupDocs.Redaction" per installarla se preferisci un'interfaccia grafica.

## Configura le impostazioni del Redattore
Prima di iniziare a redigere, potresti voler modificare il comportamento del redattore (ad esempio, impostare il colore della redazione o definire pattern personalizzati). Il frammento seguente mostra l'inizializzazione di base:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Consiglio professionale:** Regola `redactorSettings` per adeguarlo alle politiche di conformità della tua organizzazione (ad esempio, sostituire il testo con caselle nere, applicare OCR prima della redazione, ecc.).

## Guida all'implementazione

### Come cercare documenti legali?
Creare un indice ricercabile è la base per il recupero rapido di documenti legali. GroupDocs.Search ti consente di puntare a qualsiasi cartella, costruire un indice e poi eseguire query complesse su migliaia di file.

### Come aggiungere documenti all’indice
Aggiungere documenti è semplice: basta puntare la libreria alle directory che contengono i tuoi file. Puoi aggiungere più cartelle, il che è utile quando il tuo corpus legale è distribuito in diverse posizioni.

#### Creazione e gestione di un indice
**Panoramica:**  
Creare un indice è il primo passo verso operazioni di ricerca documentale efficienti. GroupDocs.Search permette di creare un indice ricercabile in qualsiasi directory di tua scelta, consentendo un rapido recupero dei documenti.

##### Passo 1: Crea l'indice
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Spiegazione:* `Index` inizializza un indice di ricerca nella directory specificata. Assicurati che il percorso rifletta la struttura delle cartelle del tuo progetto.

##### Passo 2: Aggiungere documenti a un indice
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Spiegazione:* Il metodo `Add` analizza la cartella fornita e include ogni documento supportato nell'indice. Usa questo per **aggiungere documenti all’indice** da più fonti, come contratti, fascicoli di casi o cartelle cliniche.

### Recupero e visualizzazione dei report di indicizzazione
**Panoramica:**  
I report di indicizzazione ti forniscono informazioni su quanti documenti sono stati processati, il conteggio totale dei termini e la dimensione di archiviazione—metriche essenziali per l’ottimizzazione delle prestazioni.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Spiegazione:* `GetIndexingReports` restituisce un array di report che dettagliano il processo di indicizzazione, aiutandoti a monitorare e ottimizzare le prestazioni.

## Applicazioni pratiche
1. **Gestione dei documenti legali:** Automatizza l'indicizzazione dei fascicoli per il recupero istantaneo di statuti, memorie e sentenze.  
2. **Sistema di cartelle cliniche:** Cerca i record dei pazienti preservando la privacy usando GroupDocs.Redaction per mascherare le informazioni sanitarie protette (PHI).  
3. **Portale HR aziendale:** Combina file dei dipendenti ricercabili con la redazione per proteggere i dati personali.

## Considerazioni sulle prestazioni
- **Ottimizzazione delle dimensioni dell'indice:** Elimina periodicamente le voci obsolete e ricostruisci l'indice per mantenerlo snello.  
- **Gestione della memoria:** Sfrutta il garbage collector di .NET; elimina gli oggetti `Index` quando non sono più necessari.  
- **Best practice per la scalabilità:** Conserva l'indice su storage SSD veloce e considera lo sharding di grandi corpora su più indici.

## Domande frequenti

**Q: Quali sono gli usi principali di GroupDocs.Search?**  
A: È ideale per creare indici ricercabili da grandi collezioni di documenti, consentendo un rapido recupero di file legali e medici.

**Q: Come garantisce GroupDocs.Redaction la privacy dei dati?**  
A: Ti permette di definire pattern di redazione che rimuovono o mascherano permanentemente le informazioni sensibili prima che il documento venga indicizzato o condiviso.

**Q: Posso usare queste librerie in un ambiente cloud?**  
A: Sì—entrambe le librerie funzionano su Azure, AWS o qualsiasi distribuzione .NET containerizzata con licenza adeguata.

**Q: Quali formati di file sono supportati da GroupDocs.Search?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML e molti altri formati aziendali.

**Q: Come risolvo gli errori di indicizzazione?**  
A: Verifica i percorsi delle cartelle, controlla i permessi dei file e rivedi l'output della console da `IndexingReport` per codici di errore specifici.

## Risorse
- **Documentazione:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **Riferimento API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Supporto gratuito:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licenza temporanea:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Ultimo aggiornamento:** 2026-04-04  
**Testato con:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Autore:** GroupDocs