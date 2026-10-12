---
date: '2026-10-12'
description: Scopri come aggiornare l'indice Java per la ricerca full-text Java usando
  GroupDocs.Search. Include l'aggiunta di documenti, l'aggiornamento delle versioni
  dell'indice, la configurazione di Maven e consigli sulle prestazioni.
keywords:
- java full text search
- update index java
- add documents to index
- upgrade search index
lastmod: '2026-10-12'
og_description: Scopri come aggiornare l'indice Java per la ricerca full-text Java
  con GroupDocs.Search. Guida passo-passo che include la configurazione di Maven,
  l'aggiunta di documenti e l'aggiornamento della versione dell'indice.
og_image_alt: Guide to updating Java full text search index using GroupDocs.Search
og_title: Come aggiornare l'indice Java per la ricerca full-text Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: Learn how to update index java for java full text search using GroupDocs.Search.
    Covers adding documents, upgrading index versions, Maven setup, and performance
    tips.
  headline: How to update index java for java full text search
  type: TechArticle
- description: Learn how to update index java for java full text search using GroupDocs.Search.
    Covers adding documents, upgrading index versions, Maven setup, and performance
    tips.
  name: How to update index java for java full text search
  steps:
  - name: '**Maven setup** – Add the repository and dependency to your `pom.xml` as
      shown above.'
    text: '**Maven setup** – Add the repository and dependency to your `pom.xml` as
      shown above.'
  - name: '**Direct download** – If you prefer not to use Maven, grab the JAR from
      the [GroupDocs downloads page](https://releases.groupdocs.com/search/java/).'
    text: '**Direct download** – If you prefer not to use Maven, grab the JAR from
      the [GroupDocs downloads page](https://releases.groupdocs.com/search/java/).'
  - name: '**Content management systems** – Keep search indexes fresh as articles,
      PDFs, and images are added or edited.'
    text: '**Content management systems** – Keep search indexes fresh as articles,
      PDFs, and images are added or edited.'
  - name: '**Legal document repositories** – Automatically reflect amendments to contracts,
      statutes, and case files.'
    text: '**Legal document repositories** – Automatically reflect amendments to contracts,
      statutes, and case files.'
  - name: '**Enterprise data warehousing** – Regularly refresh indexed data for accurate
      analytics and reporting.'
    text: '**Enterprise data warehousing** – Regularly refresh indexed data for accurate
      analytics and reporting.'
  type: HowTo
- questions:
  - answer: Yes, as long as the old index is still readable by the library; the `canUpdateVersion`
      method will confirm compatibility.
    question: Can I upgrade an index created with a very old version of GroupDocs.Search?
  - answer: Not necessarily. Updating the index version is sufficient in most cases,
      saving time and resources.
    question: Do I need to recreate the index after every library update?
  - answer: Start with 2‑4 threads and monitor CPU usage; increase only if the system
      has spare cores and memory.
    question: How many threads should I use for large indexes?
  - answer: The trial license removes feature limits, making it ideal for development
      and QA environments.
    question: Is a trial license enough for production testing?
  - answer: The index structure is migrated, but the searchable content remains unchanged,
      so results stay consistent.
    question: What happens to existing search results after an index version update?
  type: FAQPage
tags:
- java full text search
- GroupDocs.Search
- document indexing
title: Come aggiornare l'indice Java per la ricerca full-text Java
type: docs
url: /it/java/document-management/guide-updating-index-versions-groupdocs-search-java/
weight: 1
---

# Come aggiornare l'indice java per la ricerca full text java

Mantenere aggiornato un indice **java full text search** è essenziale per qualsiasi applicazione Java ad alte prestazioni. In questa guida imparerai come aggiornare l'indice java con GroupDocs.Search, dall'aggiunta di nuovi documenti all'aggiornamento della versione dell'indice, e otterrai anche consigli di ottimizzazione delle prestazioni che funzionano per CMS, repository legali e grandi data warehouse.

## Risposte rapide
- **Cosa significa “update index java”?** È il processo di aggiornamento dell'indice su disco in modo che rifletta le ultime modifiche ai documenti e la versione della libreria.  
- **Quale artefatto Maven è necessario?** Aggiungi la dipendenza `groupdocs-search` al tuo `pom.xml`.  
- **È necessaria una licenza per provarlo?** Sì – è disponibile una licenza di prova gratuita per la valutazione.  
- **Posso aggiornare gli indici in parallelo?** Assolutamente – configura `UpdateOptions` con più thread.  
- **Questo approccio è efficiente in termini di memoria?** Impostazioni corrette dei thread e pulizie regolari mantengono basso l'utilizzo dell'heap Java.

## Cos'è “update index java”

Aggiornare un indice in Java sincronizza la struttura dell'indice su disco con l'insieme corrente di documenti sorgente e la versione della libreria GroupDocs.Search in uso. Quando la libreria evolve, potresti anche dover **upgrade search index** per mantenere la compatibilità.

## Perché usare GroupDocs.Search per Java?

GroupDocs.Search fornisce una ricerca full‑text robusta su **50+ formati di documento** (PDF, DOCX, XLSX, PPTX, HTML, XML e molti tipi di immagine). Supporta l'indicizzazione multi‑thread che può elaborare **centinaia di megabyte al secondo** su un server tipico, e offre una gestione delle versioni integrata così i tuoi indici rimangono utilizzabili dopo gli aggiornamenti della libreria.

## Prerequisiti
- Java Development Kit (JDK) 8 o superiore.  
- Un IDE come IntelliJ IDEA o Eclipse.  
- Conoscenze di base di Java e Maven.  

## Dipendenza Maven groupdocs

Per lavorare con GroupDocs.Search, è necessario utilizzare le coordinate Maven corrette. Aggiungi il repository e la dipendenza mostrati di seguito al tuo file `pom.xml`.

**Configurazione Maven:**  
```xml
<repositories>
    <repository>
        <id>repository.groupdocs.com</id>
        <name>GroupDocs Repository</name>
        <url>https://releases.groupdocs.com/search/java/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-search</artifactId>
        <version>25.4</version>
    </dependency>
</dependencies>
```  
In alternativa, puoi [scaricare l'ultima versione direttamente](https://releases.groupdocs.com/search/java/).

## Configurare GroupDocs.Search per Java

### Istruzioni di installazione
1. **Configurazione Maven** – Aggiungi il repository e la dipendenza al tuo `pom.xml` come mostrato sopra.  
2. **Download diretto** – Se preferisci non usare Maven, scarica il JAR dalla [pagina di download di GroupDocs](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
GroupDocs offre una licenza di prova gratuita che ti consente di esplorare tutte le funzionalità senza restrizioni. Ottieni una licenza temporanea dal [portale di acquisto](https://purchase.groupdocs.com/temporary-license/). Per la produzione, acquista una licenza completa.

### Inizializzazione e configurazione di base
```java
import com.groupdocs.search.Index;

// Define the index directory path
String indexFolder = "YOUR_OUTPUT_DIRECTORY/UpdateIndexedDocuments/Index";

// Create an Index instance
Index index = new Index(indexFolder);
```

## Guida all'implementazione

### Aggiornare i documenti indicizzati – **add documents to index**

Mantenere il tuo indice sincronizzato con i file sorgente è una parte fondamentale di **update index java**.

#### Implementazione passo‑passo
**1. Definire i percorsi delle directory**  
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/UpdateIndexedDocuments/Index";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY/Documents";
```  

**2. Preparare i dati**  
```java
Utils.cleanDirectory(documentFolder);
Utils.copyFiles(Utils.DocumentsPath, documentFolder);
```  

**3. Creare un indice**  
```java
Index index = new Index(indexFolder);
```  

**4. Aggiungere documenti all'indice**  
```java
index.add(documentFolder);
```  

**5. Eseguire la ricerca iniziale**  
```java
String query = "son";
SearchResult searchResult = index.search(query);
```  

**6. Simulare modifiche ai documenti**  
```java
Utils.copyFiles(Utils.DocumentsPath4, documentFolder);
```  

**7. Impostare le opzioni di aggiornamento**  
`UpdateOptions` definisce come si comporta l'indicizzatore durante un aggiornamento, ad esempio il numero di thread, la dimensione del batch e se eliminare i file mancanti.  
```java
UpdateOptions options = new UpdateOptions();
options.setThreads(2); // Using two threads for faster indexing
```  

**8. Aggiornare l'indice**  
```java
index.update(options);
```  

**9. Verificare gli aggiornamenti con un'altra ricerca**  
```java
SearchResult searchResult2 = index.search(query);
```  

**Suggerimenti per la risoluzione dei problemi**
- Verifica che tutti i percorsi dei file siano corretti e accessibili.  
- Assicurati che il processo abbia permessi di lettura/scrittura sulla cartella dell'indice.  
- Monitora l'utilizzo di CPU e memoria quando aumenti il numero di thread.

### Aggiornare la versione dell'indice – **upgrade search index**

Quando aggiorni GroupDocs.Search, potresti dover **upgrade search index** per mantenere gli indici esistenti utilizzabili.

#### Implementazione passo‑passo
**1. Definire i percorsi delle directory**  
```java
String oldIndexFolder = Utils.OldIndexPath;
String sourceIndexFolder = "YOUR_DOCUMENT_DIRECTORY/SourceIndex";
String targetIndexFolder = "YOUR_OUTPUT_DIRECTORY/TargetIndex";
```  

**2. Preparare i dati**  
```java
Utils.cleanDirectory(sourceIndexFolder);
Utils.cleanDirectory(targetIndexFolder);
Utils.copyFiles(oldIndexFolder, sourceIndexFolder);
```  

**3. Creare un aggiornatore di indice**  
La classe `IndexUpdater` gestisce la migrazione di un indice esistente alla versione corrente della libreria.  
```java
IndexUpdater updater = new IndexUpdater();
```  

**4. Verificare e aggiornare la versione**  
```java
if (updater.canUpdateVersion(sourceIndexFolder)) {
    VersionUpdateResult result = updater.updateVersion(sourceIndexFolder, targetIndexFolder);
}
```  

**Suggerimenti per la risoluzione dei problemi**
- Conferma che l'indice di origine sia stato creato con una versione più vecchia supportata.  
- Assicurati di avere spazio su disco sufficiente per la cartella dell'indice di destinazione.  
- Aggiorna tutte le dipendenze Maven alla stessa versione per evitare problemi di compatibilità.

## Applicazioni pratiche
1. **Sistemi di gestione dei contenuti** – Mantieni gli indici di ricerca aggiornati man mano che articoli, PDF e immagini vengono aggiunti o modificati.  
2. **Repository di documenti legali** – Riflette automaticamente le modifiche a contratti, leggi e fascicoli.  
3. **Data warehousing aziendale** – Aggiorna regolarmente i dati indicizzati per analisi e report accurati.

## Considerazioni sulle prestazioni
- **Gestione dei thread** – Usa il multi‑threading con saggezza; troppi thread possono causare pressione sul GC.  
- **Monitoraggio della memoria** – Chiama periodicamente `System.gc()` o utilizza strumenti di profiling per osservare l'uso dell'heap.  
- **Ottimizzazione delle query** – Scrivi stringhe di ricerca concise e sfrutta i filtri per ridurre la dimensione del set di risultati.

## Problemi comuni e soluzioni
| Sintomo | Causa probabile | Soluzione |
|---------|-----------------|-----------|
| `Index not found` error | Percorso della cartella errato | Verifica nuovamente `indexFolder` e assicurati che la directory esista. |
| Out‑of‑memory durante l'aggiornamento | Numero eccessivo di thread | Riduci `options.setThreads()` o aumenta l'heap (`-Xmx`). |
| Nessun risultato dopo l'aggiornamento della versione | Indice vecchio incompatibile | Verifica che `updater.canUpdateVersion()` restituisca `true` prima di procedere. |
| Eccezione di licenza | Licenza di prova scaduta | Richiedi una nuova licenza di prova o applica una chiave di licenza acquistata. |

## Domande frequenti

**Q: Posso aggiornare un indice creato con una versione molto vecchia di GroupDocs.Search?**  
**A:** Sì, purché l'indice vecchio sia ancora leggibile dalla libreria; il metodo `canUpdateVersion` confermerà la compatibilità.

**Q: Devo ricreare l'indice dopo ogni aggiornamento della libreria?**  
**A:** Non necessariamente. Aggiornare la versione dell'indice è sufficiente nella maggior parte dei casi, risparmiando tempo e risorse.

**Q: Quanti thread dovrei usare per indici di grandi dimensioni?**  
**A:** Inizia con 2‑4 thread e monitora l'utilizzo della CPU; aumenta solo se il sistema ha core e memoria disponibili.

**Q: Una licenza di prova è sufficiente per i test di produzione?**  
**A:** La licenza di prova rimuove i limiti delle funzionalità, rendendola ideale per ambienti di sviluppo e QA.

**Q: Cosa succede ai risultati di ricerca esistenti dopo l'aggiornamento della versione dell'indice?**  
**A:** La struttura dell'indice viene migrata, ma il contenuto ricercabile rimane invariato, quindi i risultati rimangono coerenti.

## Conclusione
Seguendo i passaggi sopra, ora hai una solida comprensione di come **update index java** per **java full text search** con GroupDocs.Search. Aggiornare sia il contenuto dei documenti sia le versioni dell'indice garantisce che la tua esperienza di ricerca rimanga veloce, accurata e compatibile con le future versioni della libreria.

### Prossimi passi
- Sperimenta con diverse configurazioni di `UpdateOptions` per trovare il punto ottimale per il tuo carico di lavoro.  
- Esplora funzionalità avanzate di query come il facetting e l'evidenziazione offerte da GroupDocs.Search.  
- Integra il flusso di lavoro di indicizzazione nel tuo pipeline CI/CD per aggiornamenti automatizzati.

---

**Ultimo aggiornamento:** 2026-10-12  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Come implementare la ricerca full text java: creare la directory dell'indice con GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Libreria Java Full Text Search – Ottimizzare l'indice con GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Ricerca fuzzy Java: aggiungere documenti all'indice con GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)