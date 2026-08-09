---
date: '2026-07-07'
description: Scopri come disabilitare le parole di stop Java e aggiungere documenti
  all'indice utilizzando GroupDocs.Search per Java, migliorando l'accuratezza e le
  prestazioni della ricerca.
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: Disabilita le parole di stop Java e aggiungi documenti all'indice
  con GroupDocs.Search per Java. Segui questa guida passo‑passo per migliorare l'accuratezza
  e le prestazioni delle query.
og_title: Disabilita le parole di stop Java – Aggiungi documenti all'indice con GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: Disabilita le parole di stop Java – Aggiungi documenti all'indice con GroupDocs
type: docs
url: /it/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Disabilitare le parole stop Java – Aggiungere documenti all'indice con GroupDocs

In questo tutorial scoprirai come **disable stop words java** mentre aggiungi i tuoi file a un indice ricercabile con GroupDocs.Search per Java. Disattivando il filtro integrato delle parole stop, ogni token—incluse parole comuni come “on”, “by” o “the”—diventa ricercabile, migliorando drasticamente la pertinenza dei risultati per domini specializzati come contratti legali, cataloghi e‑commerce o manuali tecnici.

## Risposte rapide
- **What does “add documents to index” mean?** Significa caricare i file di origine in un indice ricercabile in modo che possano essere interrogati in modo efficiente.  
- **Why would I disable stop words?** Per includere parole comuni (es. “on”, “the”) nelle ricerche quando tali termini sono significativi per il tuo dominio.  
- **Which library version is required?** GroupDocs.Search per Java 25.4 o successiva.  
- **Do I need a license?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza permanente per la produzione.  
- **Can I use this in a Maven project?** Sì – basta aggiungere il repository e la dipendenza mostrati di seguito.

## Cosa sono le parole stop nella ricerca e perché potresti volerle disabilitare?

Le parole stop sono termini ad alta frequenza che molti motori di ricerca filtrano automaticamente per velocizzare l'elaborazione delle query. Disabilitarle garantisce che **ogni parola**—incluse quelle tradizionalmente ignorate—contribuisca all'indice di ricerca, il che è essenziale quando queste parole hanno un significato specifico del dominio. Ad esempio, in un contratto legale la parola “by” può distinguere le parti, e in un catalogo di prodotti “on” può far parte del nome di un modello.

## Come funziona l'aggiunta di documenti all'indice in GroupDocs.Search?

Quando aggiungi documenti, GroupDocs.Search legge ogni file, tokenizza il contenuto e memorizza i token in un indice invertito ottimizzato. Questa struttura consente il recupero in meno di un secondo anche per collezioni contenenti **centinaia di migliaia di file**. La libreria supporta anche aggiornamenti incrementali, così puoi mantenere l'indice aggiornato senza ricostruirlo da zero.

## Prerequisiti

- **Required Libraries**: GroupDocs.Search per Java 25.4 (o più recente).  
- **Development Environment**: IntelliJ IDEA, Eclipse o qualsiasi IDE Java tu preferisca.  
- **Basic Knowledge**: Familiarità con la sintassi Java e il concetto di indicizzazione.

## Configurazione di GroupDocs.Search per Java

### Installazione con Maven

Se utilizzi Maven, includi quanto segue nel tuo `pom.xml`:

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

### Download diretto

In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Passaggi per l'acquisizione della licenza
- **Free Trial** – inizia a testare subito.  
- **Temporary License** – ottieni una chiave a tempo limitato per la funzionalità completa.  
- **Purchase** – assicurati una licenza permanente per l'uso in produzione.

## Inizializzazione e configurazione di base

IndexSettings è una classe di configurazione che definisce come l'indice è costruito, ricercato e quali funzionalità sono abilitate.

Crea un'istanza di `IndexSettings` per controllare il comportamento dell'indice:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Come disabilitare le parole stop nella ricerca (Java)?

IndexSettings è l'oggetto di configurazione che controlla il comportamento dell'indice di ricerca. Per impostazione predefinita abilita un filtro integrato per le parole stop. Per disattivare questo filtro, chiama il metodo `setUseStopWords(false)` sull'istanza `IndexSettings`. Questa singola chiamata disabilita la rimozione delle parole stop, garantendo che ogni token—incluse parole comuni come “on” o “the”—venga indicizzato e possa essere interrogato.

## Come aggiungere documenti all'indice

L'aggiunta di documenti all'indice avviene creando un oggetto `Index` con le `IndexSettings` desiderate e poi invocando il suo metodo `add` per ogni file o cartella. La libreria legge ogni documento, tokenizza il contenuto e memorizza i termini risultanti nell'indice invertito, rendendoli ricercabili immediatamente. Puoi indirizzare l'indice a una directory di output specifica e specificare la cartella sorgente contenente i file da indicizzare.

### Definizione della directory di output

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### Specifica della directory dei documenti

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## Esecuzione di una query di ricerca

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Poiché `disable stop words java` è attivo, una query contenente il termine "on" verrà valutata, restituendo corrispondenze che altrimenti verrebbero ignorate dal filtro predefinito.

## Applicazioni pratiche

1. **Enterprise Document Search** – Conserva la terminologia critica che verrebbe rimossa dalle liste di parole stop predefinite.  
2. **E‑commerce Platforms** – Aumenta la scoperta dei prodotti indicizzando ogni parola nelle descrizioni, nei numeri di modello e nelle specifiche.  
3. **Legal Research Tools** – Cattura ogni termine legale, anche quelli comunemente trattati come parole stop, per evitare di perdere clausole cruciali.

## Considerazioni sulle prestazioni

- **Optimization Tips**: Aggiorna e pota regolarmente il tuo indice per mantenere alta la velocità di ricerca. GroupDocs.Search può gestire **fino a 1 milione di documenti** mantenendo tempi di query inferiori al secondo.  
- **Resource Usage**: Monitora la dimensione dell'heap JVM; indici grandi possono richiedere un heap massimo (`-Xmx`) di 4 GB o più.  
- **Java Memory Management**: Usa opzioni di archiviazione off‑heap per corpora molto grandi per mantenere l'impronta on‑heap sotto i 2 GB.

## Problemi comuni e soluzioni

| Sintomo | Causa probabile | Soluzione |
|---|---|---|
| Nessun risultato per parole comuni | `setUseStopWords(true)` (predefinito) | Chiama `setUseStopWords(false)` come mostrato sopra. |
| Errori out‑of‑memory durante l'indicizzazione | Indicizzazione di troppi file di grandi dimensioni contemporaneamente | Indicizza i file in batch; aumenta l'opzione JVM `-Xmx`. |
| La ricerca restituisce dati obsoleti | Indice non aggiornato dopo l'aggiunta di nuovi file | Chiama `index.update()` o ri‑aggiungi i documenti modificati. |

## Domande frequenti

**Q: What are stop words?**  
A: Le parole stop sono termini comuni (es. “the”, “is”, “on”) che molti motori di ricerca ignorano per velocizzare le query. Disabilitarle ti consente di trattare ogni token come ricercabile.

**Q: Why disable stop words in search indexes?**  
A: Quando è necessario il matching di frasi esatte—come in documenti legali o tecnici—ogni parola ha un significato, quindi è necessario includere le parole stop.

**Q: How does GroupDocs.Search handle large datasets?**  
A: La libreria utilizza strutture dati ottimizzate e indicizzazione incrementale per mantenere basso l'uso della memoria, anche con **milioni di documenti**.

**Q: Can I integrate GroupDocs.Search with other Java applications?**  
A: Sì, l'API è progettata per un facile inserimento in qualsiasi sistema basato su Java, dai servizi web alle applicazioni desktop.

**Q: What should I do if my search results are not accurate?**  
A: Verifica che l'indice includa tutti i file necessari (`add documents to index`), assicurati che il filtro delle parole stop sia disabilitato quando necessario, e considera di ricostruire l'indice dopo modifiche importanti.

## Risorse aggiuntive

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Seguendo questa guida, ora sai come **add documents to index** e **disable stop words java** per fornire risultati di ricerca più accurati nelle tue applicazioni Java.

---

**Ultimo aggiornamento:** 2026-07-07  
**Testato con:** GroupDocs.Search for Java 25.4  
**Autore:** GroupDocs  

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## Tutorial correlati

- [Elaborazione del linguaggio Java – Creare dizionario dei sinonimi con GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Come aggiungere documenti all'indice con indicizzazione dei metadati in Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Come aggiungere documenti all'indice con GroupDocs.Search per Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)