---
date: '2026-08-10'
description: Scopri come creare searchable index java e abilitare la ricerca case‑sensitive
  con GroupDocs.Search, migliorando la precisione per le applicazioni Java.
keywords:
- create searchable index java
- case sensitive search java
- groupdocs search java tutorial
- java text query search
lastmod: '2026-08-10'
og_description: Scopri come creare searchable index java e abilitare la ricerca case‑sensitive
  con GroupDocs.Search. Guida passo‑passo per gli sviluppatori Java.
og_image_alt: Guide to creating a searchable index in Java using GroupDocs with case‑sensitive
  search
og_title: 'Crea searchable index java: aggiungi ricerca case‑sensitive nei documenti'
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  headline: 'Create searchable index java: add docs case‑sensitive search'
  type: TechArticle
- description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  name: 'Create searchable index java: add docs case‑sensitive search'
  steps:
  - name: create an index and add your documents
    text: The `Index` class represents a searchable storage area on disk where documents
      are indexed. > **Pro tip:** You can call `index.add()` multiple times to **search
      across multiple directories** in a single index.
  - name: enable case‑sensitive search
    text: '`SearchOptions` configures how queries are processed, including case sensitivity
      and other search behaviors.'
  - name: execute a case‑sensitive text query
    text: '`SearchQuery` builds the query object that the engine evaluates against
      the index. The loop prints the full path of each document that contains the
      exact case‑matched term.'
  - name: initialize a second index (optional)
    text: A second `Index` instance can be created to isolate object‑based searches
      from plain‑text searches.
  - name: re‑use the case‑sensitive option
    text: '`SearchOptions` can be reused across different query types to maintain
      consistent case handling.'
  - name: build and run an object query
    text: '`WordQuery` represents a word‑level search that can be combined with other
      query types for complex searches. Using `createWordQuery` lets you later combine
      it with phrase, wildcard, or Boolean queries for more complex scenarios.'
  type: HowTo
- questions:
  - answer: Add documents to an index with `index.add(...)`.
    question: What is the primary step to start searching?
  - answer: Set `options.setUseCaseSensitiveSearch(true)`.
    question: How do you enable case‑sensitive search?
  - answer: Yes – call `index.add()` for each folder you want to include.
    question: Can you search across multiple directories?
  - answer: Use `SearchQuery.createWordQuery(...)`.
    question: Which method lets you search with objects?
  - answer: A temporary license is available for trial purposes.
    question: Do you need a license for testing?
  type: FAQPage
tags:
- create searchable index
- case-sensitive search
- groupdocs search
- java document processing
title: 'Crea searchable index java: aggiungi ricerca case‑sensitive nei documenti'
type: docs
url: /it/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Crea indice ricercabile java: aggiungi documenti ricerca sensibile al maiuscolo/minuscolo

## Risposte rapide
- **Qual è il passaggio principale per iniziare a cercare?** Aggiungi documenti a un indice con `index.add(...)`.  
- **Come abiliti la ricerca sensibile al maiuscolo/minuscolo?** Imposta `options.setUseCaseSensitiveSearch(true)`.  
- **Puoi cercare in più directory?** Sì – chiama `index.add()` per ogni cartella che desideri includere.  
- **Quale metodo consente di cercare con oggetti?** Usa `SearchQuery.createWordQuery(...)`.  
- **Hai bisogno di una licenza per i test?** È disponibile una licenza temporanea per scopi di prova.

## Cosa significa “aggiungere documenti all'indice”?
Aggiungere documenti a un indice significa fornire i tuoi file di origine (PDF, documenti Word, testo semplice, ecc.) a GroupDocs.Search affinché possa costruire una struttura dati ricercabile. L'indice memorizza termini tokenizzati, posizioni e metadati, consentendo al motore di eseguire query rapide, incluse quelle sensibili al maiuscolo/minuscolo, e di classificare i risultati in modo efficiente.

## Perché abilitare la ricerca sensibile al maiuscolo/minuscolo in Java?
Abilitare la ricerca sensibile al maiuscolo/minuscolo garantisce che il motore distingua tra termini che differiscono solo per la capitalizzazione, il che è fondamentale per i settori in cui le maiuscole hanno significato. Consente il matching esatto dei termini, supporta i requisiti di conformità normativa e migliora la pertinenza restituendo risultati che corrispondono esattamente al caso della query dell'utente.

- **Matching esatto dei termini** – ad es., “Apple” (azienda) vs. “apple” (frutto).  
- **Conformità normativa** – molte industrie richiedono un matching preciso delle frasi.  
- **Rilevanza migliorata** – gli utenti tecnici e legali spesso si aspettano risultati specifici per il caso.

## Prerequisiti
- JDK 17 o successivo (consigliato)  
- Maven per la gestione delle dipendenze  
- Un IDE come IntelliJ IDEA o Eclipse  
- Familiarità di base con la programmazione Java  

## Configurare GroupDocs.Search per Java
Il seguente snippet Maven aggiunge il repository GroupDocs.Search e la dipendenza necessaria al tuo progetto.

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

In alternativa, puoi scaricare l'ultima versione direttamente da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenza
Per iniziare con una prova, visita GroupDocs per ottenere una licenza temporanea. Questo ti permetterà di testare tutte le funzionalità senza alcuna limitazione.

## Come creare indice ricercabile java – ricerca con query di testo

### Passo 1: crea un indice e aggiungi i tuoi documenti
La classe `Index` rappresenta un'area di archiviazione ricercabile su disco dove i documenti vengono indicizzati.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Suggerimento:** Puoi chiamare `index.add()` più volte per **cercare in più directory** in un unico indice.

### Passo 2: abilita la ricerca sensibile al maiuscolo/minuscolo
`SearchOptions` configura come le query vengono elaborate, includendo la sensibilità al caso e altri comportamenti di ricerca.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Passo 3: esegui una query di testo sensibile al maiuscolo/minuscolo
`SearchQuery` costruisce l'oggetto query che il motore valuta contro l'indice.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Il ciclo stampa il percorso completo di ogni documento che contiene il termine con corrispondenza esatta del caso.

## Come creare indice ricercabile java – ricerca con query di oggetto

### Passo 1: inizializza un secondo indice (opzionale)
Una seconda istanza `Index` può essere creata per isolare le ricerche basate su oggetti da quelle di testo semplice.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Passo 2: riutilizza l'opzione sensibile al maiuscolo/minuscolo
`SearchOptions` può essere riutilizzato tra diversi tipi di query per mantenere una gestione coerente del caso.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Passo 3: costruisci ed esegui una query di oggetto
`WordQuery` rappresenta una ricerca a livello di parola che può essere combinata con altri tipi di query per ricerche complesse.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Usare `createWordQuery` ti permette di combinarlo in seguito con query di frase, wildcard o Boolean per scenari più complessi.

## Applicazioni pratiche
- **Gestione documenti legali:** Recupera normative specifiche al caso dove la capitalizzazione è importante.  
- **Piattaforme e‑commerce:** Distinguere SKU di prodotto come “PRO‑X” vs. “pro‑x”.  
- **Sistemi di gestione dei contenuti (CMS):** Garantire che gli autori trovino intestazioni o tag esatti.

## Considerazioni sulle prestazioni
- **Mantieni l'indice aggiornato** – reindicizza quando vengono aggiunti nuovi file o quelli esistenti cambiano.  
- **Monitora l'uso della memoria** – grandi corpora beneficiano dell'indicizzazione incrementale e di una corretta dimensione dell'heap JVM.  
- **Sfrutta il garbage collector di Java** – rilascia gli oggetti `Index` quando non sono più necessari.

## Problemi comuni e soluzioni
| Problema | Soluzione |
|----------|-----------|
| `useCaseSensitiveSearch` sembra ignorato | Verifica di utilizzare l'ultima versione di GroupDocs.Search e che l'indice sia stato ricostruito dopo aver modificato l'opzione. |
| Nessun risultato restituito per un termine noto | Assicurati che il caso del termine corrisponda esattamente e che il documento sia stato aggiunto correttamente all'indice. |
| La ricerca in molte cartelle rallenta | Aggiungi ogni cartella individualmente con `index.add()` e considera di suddividere l'indice in shard per dataset molto grandi. |

## Domande frequenti

**D:** Come gestisco grandi dataset con GroupDocs.Search?  
**R:** Utilizza il partizionamento dell'indice, ottimizza le impostazioni di memoria della JVM e compatta periodicamente l'indice per mantenere le prestazioni ottimali.

**D:** Posso cercare simultaneamente in più directory?  
**R:** Sì – chiama `index.add()` per ogni directory che desideri includere, poi esegui una singola query sull'indice combinato.

**D:** Quali sono gli errori comuni quando si configurano ricerche sensibili al maiuscolo/minuscolo?  
**R:** Dimenticare di ricostruire l'indice dopo aver abilitato `useCaseSensitiveSearch`, o usare il caso sbagliato nella stringa di query.

**D:** Come posso risolvere gli errori di ricerca?  
**R:** Controlla i file di log generati da GroupDocs.Search per gli stack trace e conferma che tutte le dipendenze Maven siano risolte correttamente.

**D:** GroupDocs.Search è adatto per applicazioni in tempo reale?  
**R:** Con strategie di indicizzazione appropriate (aggiornamenti incrementali e caching in memoria), può fornire risultati di ricerca quasi in tempo reale.

## Risorse
- **Documentazione:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **Riferimento API:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **Repository GitHub:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum di supporto:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Licenza temporanea:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-08-10  
**Testato con:** GroupDocs.Search 25.4  
**Autore:** GroupDocs  

---

## Tutorial correlati

- [Create Search Index Java – GroupDocs.Search Tutorials](/search/java/indexing/)
- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)