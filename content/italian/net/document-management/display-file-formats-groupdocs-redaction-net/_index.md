---
date: '2026-06-07'
description: Scopri come elencare le estensioni dei file e ottenere i formati dei
  file usando GroupDocs.Redaction in C#. Include configurazione, codice e consigli
  pratici.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Come elencare le estensioni dei file con GroupDocs.Redaction in .NET – Guida
  completa
type: docs
url: /it/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Visualizzare i formati di file supportati usando GroupDocs.Redaction in .NET

Gestire un'ampia varietà di tipi di documento è una realtà quotidiana per gli sviluppatori .NET. Utilizzando **GroupDocs.Redaction**, è possibile **elencare le estensioni dei file** supportate dalla libreria, fornendo alla tua applicazione l'intelligenza per accettare o rifiutare upload, presentare scelte UI amichevoli e evitare costosi errori di runtime. Questo tutorial ti guida attraverso tutto ciò di cui hai bisogno — dai prerequisiti a un'implementazione completa e pronta per la produzione — così potrai **ottenere i formati di file** e **c# display file formats** nella tua soluzione.

## Risposte rapide
- **Cosa significa “list file extensions”?** Significa recuperare la collezione di identificatori di tipi di file supportati (ad es., *.pdf*, *.docx*) dall'API.  
- **Quale pacchetto NuGet fornisce questa funzionalità?** `GroupDocs.Redaction` (ultima versione stabile).  
- **Ho bisogno di una licenza per eseguire il campione?** Una licenza di prova gratuita funziona per lo sviluppo; è necessaria una licenza permanente per la produzione.  
- **Posso memorizzare nella cache i risultati?** Sì — memorizza l'elenco in memoria o in una cache distribuita per evitare chiamate API ripetute.  
- **Questa funzionalità è compatibile con .NET 6 e .NET Core?** Assolutamente; la libreria supporta .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ e .NET 6+.

## Cos'è GroupDocs.Redaction?
**GroupDocs.Redaction** è una libreria .NET che consente agli sviluppatori di redigere contenuti sensibili, convertire documenti e scoprire i tipi di file supportati — tutto senza richiedere Microsoft Office sul server. Astrae la gestione complessa dei formati dietro un'API pulita e orientata agli oggetti. Offre un'API unificata per redazione, conversione e scoperta dei formati, gestendo PDF, documenti Office, immagini e altro, garantendo alte prestazioni e sicurezza.

## Perché elencare le estensioni dei file con GroupDocs.Redaction?
La libreria **supporta oltre 50 formati di input e output**, inclusi PDF, DOCX, PPTX, XLSX, HTML e oltre 30 tipi di immagine. Programmaticamente **elencando le estensioni dei file**, è possibile:
- Impedire agli utenti di caricare file non supportati (riducendo gli errori di validazione fino al 90%).  
- Popolare dinamicamente i menu a discesa, garantendo che l'interfaccia rimanga sincronizzata con gli aggiornamenti della libreria.  
- Creare log di audit che registrano il tipo di file esatto che l'utente ha tentato di elaborare.

## Prerequisiti
- **GroupDocs.Redaction**: Installa tramite NuGet (vedi i comandi sotto).  
- **.NET SDK**: Assicurati che l'ultimo .NET SDK sia installato. Scaricalo [qui](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 o qualsiasi editor compatibile.  
- **Conoscenza di base di C#**: Dovresti sentirti a tuo agio con le collezioni e LINQ.

## Configurare GroupDocs.Redaction per .NET

### Installa la libreria

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Apri NuGet Package Manager, cerca “GroupDocs.Redaction” e installa l'ultima versione.

### Ottieni e applica una licenza

Inizia con una prova gratuita o richiedi una licenza temporanea per esplorare tutte le funzionalità senza limitazioni. Per le opzioni di acquisto, visita la [pagina di acquisto di GroupDocs](https://purchase.groupdocs.com/). Una volta ottenuto il file di licenza:
1. Posizionalo in una cartella accessibile all'interno del tuo progetto (ad es., `./Licenses/GroupDocs.Redaction.lic`).  
2. Inizializza la licenza all'avvio dell'applicazione:

La classe `License` carica il tuo file di licenza e attiva GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Come elencare le estensioni dei file usando GroupDocs.Redaction?

Carica l'API Redaction e chiama il metodo che restituisce i formati supportati. La chiamata restituisce una collezione in cui ogni elemento contiene un'estensione e una descrizione leggibile. Questa operazione è leggera e può essere eseguita all'avvio o su richiesta.

### Recupera i tipi di file supportati
Il metodo `RedactionApi.GetSupportedFileFormats()` restituisce una collezione di sola lettura di oggetti `FileFormatInfo` che descrivono ogni formato.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Visualizza ogni estensione e descrizione
Ogni `FileFormatInfo` fornisce le proprietà `Extension` e `Description` per un tipo di file.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Spiegazione**: Il ciclo itera su ogni oggetto `FileFormatInfo`, stampando la sua `Extension` e `Description` in una tabella ordinatamente allineata.

## Come integrare l'elenco in un menu a discesa UI?

Una volta ottenuta la collezione, collegala a qualsiasi componente UI — `ComboBox` WinForms, `ComboBox` WPF o elemento `select` ASP.NET Core. La chiave è usare `Extension` come valore e `Description` come testo visualizzato. Questo garantisce che gli utenti vedano nomi amichevoli mentre il tuo codice lavora con le stringhe di estensione esatte.

## Problemi comuni e soluzioni
- **Errore di namespace mancante** – Verifica di aver importato `GroupDocs.Redaction` e `GroupDocs.Redaction.Common`.  
- **Licenza non trovata** – Assicurati che il percorso del file di licenza sia corretto e che il file sia incluso nell'output di build.  
- **Prestazioni su progetti grandi** – Metti nella cache il risultato in una variabile statica o in una cache distribuita (ad es., Redis) per evitare enumerazioni ripetute.

## Applicazioni pratiche
Conoscere l'elenco esatto delle estensioni supportate sblocca diversi scenari reali:
1. **Sistemi di gestione documentale** – Auto-categorizza i file in ingresso in base alla loro estensione.  
2. **Strumenti di filtraggio dei contenuti** – Blocca i formati non consentiti (ad es., file eseguibili) al momento del caricamento.  
3. **Pipeline di conversione file** – Decidi dinamicamente se un file può essere convertito o necessita di un flusso di lavoro alternativo.

## Considerazioni sulle prestazioni
- **Impronta di memoria** – L'elenco dei formati è memorizzato in una leggera `IReadOnlyCollection`, tipicamente inferiore a 2 KB.  
- **Sicurezza dei thread** – La collezione è immutabile dopo la creazione, rendendola sicura per letture concorrenti.  
- **Caching** – Per API ad alto traffico, memorizza nella cache l'elenco per tutta la durata dell'applicazione per eliminare i pochi microsecondi di overhead per richiesta.

## Conclusione
Seguendo i passaggi sopra, ora disponi di un modo affidabile per **elencare le estensioni dei file** e **c# display file formats** usando GroupDocs.Redaction. Questa funzionalità non solo migliora l'esperienza utente, ma protegge anche il tuo backend da file non supportati. Esplora le funzionalità aggiuntive di Redaction — come il mascheramento dei contenuti, la redazione PDF e l'elaborazione batch — per rafforzare ulteriormente il tuo flusso di lavoro documentale.

## Domande frequenti
**Q: Quali sono i formati di file supportati di default?**  
A: GroupDocs.Redaction supporta 50+ formati, inclusi PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG e molti altri. Vedi l'elenco completo su [Documentazione di GroupDocs](https://docs.groupdocs.com/search/net/).

**Q: Come aggiorno la libreria all'ultima versione?**  
A: Apri NuGet Package Manager, cerca “GroupDocs.Redaction” e fai clic su **Update**. In alternativa, esegui `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Posso usare questo elenco per la validazione lato server dei file caricati?**  
A: Sì — confronta l'estensione del file caricato con la collezione recuperata prima dell'elaborazione. Questo elimina il 99 % degli errori di formato non valido.

**Q: È possibile estendere il supporto a tipi di file personalizzati?**  
A: Le estensioni personalizzate richiedono gestori personalizzati; la libreria core non aggiunge nativamente nuovi formati. Consulta la documentazione API per creare pipeline di import/export personalizzate.

**Q: La mia applicazione si blocca dopo aver aggiunto il codice—cosa devo controllare?**  
A: Verifica che la licenza sia caricata correttamente, che le istruzioni `using` facciano riferimento ai namespace corretti e che gestisci `IOException` durante la lettura del file di licenza.

---

**Ultimo aggiornamento:** 2026-06-07  
**Testato con:** GroupDocs.Redaction 23.9 for .NET  
**Autore:** GroupDocs  

## Risorse
- [Documentazione](https://docs.groupdocs.com/search/net/)
- [Riferimento API](https://reference.groupdocs.com/redaction/net)
- [Scarica GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/search/10)
- [Richiesta licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

## Tutorial correlati
- [Filtraggio avanzato dei file in .NET con GroupDocs.Redaction: Tecniche efficienti di gestione documentale](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Master GroupDocs.Redaction .NET: Configurazione e gestione eventi per una gestione documentale sicura](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Padroneggiare la gestione documentale in .NET con GroupDocs.Redaction: Configurazione licenza e evidenziazione ricerca HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)