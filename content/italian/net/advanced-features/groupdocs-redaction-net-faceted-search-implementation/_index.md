---
date: '2026-04-02'
description: Scopri come creare un indice di ricerca GroupDocs e aggiungere documenti
  all'indice implementando la ricerca a faccette con GroupDocs.Search e GroupDocs.Redaction
  in .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Crea indice di ricerca GroupDocs con Redaction .NET e ricerca a faccette
type: docs
url: /it/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Crea indice di ricerca GroupDocs con Redaction .NET Faceted Search

Nelle applicazioni moderne, **creare un indice di ricerca con GroupDocs** è essenziale per un recupero rapido e preciso dei documenti. Che tu stia gestendo contratti legali, cataloghi di prodotti o grandi basi di conoscenza, un indice ben costruito ti consente di **aggiungere documenti all'indice** ed eseguire potenti ricerche faccettate in pochi secondi. Questo tutorial ti guida attraverso l'intero processo — dall'impostazione di GroupDocs.Redaction alla creazione di query faccettate semplici e complesse — così potrai offrire un'esperienza di ricerca reattiva nei tuoi progetti .NET.

## Risposte rapide
- **Qual è lo scopo principale?** Creare un indice di ricerca con GroupDocs e abilitare la ricerca faccettata.  
- **Quali librerie sono necessarie?** GroupDocs.Redaction e GroupDocs.Search per .NET.  
- **Come aggiungo documenti all'indice?** Usa `index.Add(documentsFolder)` dopo aver inizializzato l'indice.  
- **Posso eseguire query complesse?** Sì, combina query oggetto con operatori logici per filtraggio avanzato.  
- **È necessaria una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per la produzione.

## Cos'è la ricerca faccettata e perché usarla con GroupDocs?
La ricerca faccettata consente agli utenti di affinare i risultati applicando più filtri — come categoria, data o autore — simultaneamente. Quando combinata con **GroupDocs.Redaction**, ottieni contenuti sicuri e ricercabili che rispettano le regole di redazione, rendendola ideale per ambienti con elevati requisiti di conformità.

## Prerequisiti

### Librerie richieste, versioni e dipendenze
- **GroupDocs.Redaction .NET** – ultima versione stabile.  
- **GroupDocs.Search .NET** – funziona a stretto contatto con Redaction per l'indicizzazione.

### Requisiti di configurazione dell'ambiente
- **IDE**: Visual Studio 2019 o versioni successive.  
- **Framework**: .NET Core 3.1, .NET 5 o .NET 6.  
- **Compatibilità OS**: Windows, Linux, macOS.

### Prerequisiti di conoscenza
Competenze di base in C# e una comprensione di alto livello dei concetti di ricerca faccettata saranno utili, ma la guida passo‑passo è adatta anche ai principianti.

## Configurazione di GroupDocs.Redaction per .NET

### Informazioni sull'installazione
Puoi aggiungere il pacchetto GroupDocs.Redaction utilizzando uno dei seguenti metodi:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Cerca "GroupDocs.Redaction" e installa l'ultima versione.

### Passaggi per l'acquisizione della licenza
Per sbloccare tutte le funzionalità, inizia con una prova gratuita o ottieni una licenza permanente:

1. Visita [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) per esplorare le opzioni di licenza.  
2. Segui le istruzioni a schermo per ricevere il file di licenza di prova o acquistato.

### Inizializzazione e configurazione di base
Una volta installato il pacchetto, inizializza il Redactor nella tua applicazione:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Come creare un indice di ricerca groupdocs

Di seguito suddividiamo l'implementazione in due parti: **Simple Faceted Search** e **Complex Query**. Ogni parte mostra come **creare un indice di ricerca groupdocs**, aggiungere documenti ed eseguire query.

### Funzionalità 1: Ricerca faccettata semplice

**Panoramica**  
La ricerca faccettata consente agli utenti di restringere i risultati selezionando più criteri. Questa sezione dimostra un approccio semplice usando GroupDocs.Search.

#### Passo 1: Definisci le cartelle dell'indice e dei documenti
Imposta i percorsi delle cartelle dove risiederà l'indice e dove si trovano i documenti di origine.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Passo 2: Crea un indice
```csharp
Index index = new Index(indexFolder);
```

#### Passo 3: Aggiungi documenti all'indice
```csharp
index.Add(documentsFolder);
```

#### Passo 4: Esegui una ricerca di query testuale
Esegui una query testuale di base sul campo **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Passo 5: Esegui una ricerca di query oggetto
Utilizza query orientate agli oggetti per un controllo più preciso.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Funzionalità 2: Query complessa

**Panoramica**  
Quando è necessario combinare più filtri — come modelli di nome file e corrispondenze di frasi — è possibile costruire una query complessa usando operatori logici.

#### Passo 1: Definisci le cartelle dell'indice e dei documenti
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Passo 2: Crea un indice e aggiungi documenti
(Guarda i passi 2‑3 dell'esempio semplice; rimangono gli stessi.)

#### Passo 3: Esegui una ricerca di query testuale
Esegui una query testuale composta che combina criteri di nome file e contenuto.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Passo 4: Costruisci ed esegui query oggetto
Costruisci la stessa logica programmaticamente.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Continua a combinare frasi, intervalli e operatori booleani per soddisfare le tue regole di business esatte.

## Applicazioni pratiche

1. **Piattaforme E‑Commerce** – Filtra i prodotti per categoria, prezzo e valutazione.  
2. **Sistemi di gestione documentale** – Individua i contratti per autore, data o livello di riservatezza.  
3. **Portali di contenuti** – Consenti ai lettori di approfondire per tag, argomenti e date di pubblicazione.

## Considerazioni sulle prestazioni

- **Aggiornamento indice**: Reindicizza regolarmente file nuovi o aggiornati per mantenere la ricerca veloce.  
- **Gestione della memoria**: Disporre degli oggetti `Index` quando non più necessari, specialmente per grandi set di dati.  
- **Indicizzazione asincrona**: Usa `Task.Run` o servizi in background per evitare blocchi dell'interfaccia durante indicizzazioni pesanti.

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Index not found** | Verifica il percorso `indexFolder` e assicurati che la cartella abbia permessi di scrittura. |
| **No results returned** | Controlla che i campi su cui esegui la query (es. `Content`, `Filename`) siano indicizzati. |
| **Out‑of‑memory errors** | Elabora i documenti in batch e considera di aumentare la dimensione dell'heap GC di .NET. |

## Domande frequenti

**Q: Cos'è la ricerca faccettata?**  
A: La ricerca faccettata consente agli utenti di affinare i risultati utilizzando più filtri indipendenti come categoria, data o autore.

**Q: Come gestisco grandi set di dati con GroupDocs.Search?**  
A: Usa l'indicizzazione incrementale, l'elaborazione in batch e le operazioni asincrone per mantenere basso l'uso della memoria e alta la performance.

**Q: Posso integrare le funzionalità di GroupDocs in applicazioni .NET esistenti?**  
A: Sì, le librerie sono progettate per un'integrazione senza soluzione di continuità con qualsiasi progetto .NET.

**Q: Quali sono alcuni problemi comuni con la ricerca faccettata?**  
A: La sintassi di query complesse e la garanzia che tutti i campi rilevanti siano indicizzati sono sfide tipiche; test adeguati e la manutenzione dell'indice le mitigano.

**Q: Come posso ottenere una licenza temporanea per GroupDocs?**  
A: Visita la [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) per richiedere una licenza di prova che sblocca tutte le funzionalità durante la valutazione.

## Risorse
- **Documentazione**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Riferimento API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Ultimo aggiornamento:** 2026-04-02  
**Testato con:** GroupDocs.Redaction 23.12 per .NET, GroupDocs.Search 23.12 per .NET  
**Autore:** GroupDocs