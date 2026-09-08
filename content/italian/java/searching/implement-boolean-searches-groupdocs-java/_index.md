---
date: '2026-07-21'
description: Il tutorial Create Boolean Query Java mostra come implementare ricerche
  boolean AND, OR, NOT usando GroupDocs.Search for Java, add documents to an index
  e boost document retrieval.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Il tutorial Create Boolean Query Java spiega passo‑a‑passo come costruire
  query AND, OR, NOT con GroupDocs.Search for Java, add documents to an index e improve
  retrieval performance.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – Padroneggia le ricerche Boolean con GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Crea query Boolean Java: padroneggia le ricerche Boolean con GroupDocs.Search
  for Java'
type: docs
url: /it/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Crea query booleane Java: padroneggia le ricerche booleane con GroupDocs.Search per Java

Cercare tra collezioni massive di documenti può sembrare trovare un ago in un pagliaio. **Create Boolean Query Java** ti consente di dire al motore esattamente ciò di cui hai bisogno — documenti che contengono *entrambi* i termini, *uno* dei termini, o *escludere* parole indesiderate. In questa guida ti mostreremo come configurare **GroupDocs.Search for Java**, aggiungere documenti a un indice e creare potenti query booleane che migliorano i tuoi flussi di lavoro di **document retrieval java**. Alla fine sarai in grado di scrivere codice pulito e manutenibile che crea query booleane in Java con poche righe.

## Risposte rapide
- **Cos'è una query boolean AND?** Restituisce solo i documenti che contengono *tutti* i termini specificati.  
- **In che modo OR differisce da AND?** OR corrisponde ai documenti con *qualsiasi* dei termini, ampliando il set di risultati.  
- **Quando dovrei usare NOT?** Usa NOT per filtrare i documenti che contengono parole indesiderate.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per i test; è necessaria una licenza commerciale per la produzione.  
- **Quale versione di Java è richiesta?** Java 8+ è supportata; JDK 11+ è consigliata.

## Cos'è **create boolean query java**?
`create boolean query java` si riferisce alla costruzione di una query di ricerca in Java che combina operatori logici come AND, OR e NOT utilizzando l'API GroupDocs.Search. Assemblando questi operatori è possibile controllare con precisione quali documenti corrispondono, abilitando filtri avanzati, ottimizzazione della rilevanza e scenari di ricerca complessi.

## Perché usare GroupDocs.Search per Java?
- **High performance** su grandi insiemi di documenti – può indicizzare e cercare 500 GB di testo in meno di un minuto su un server standard.  
- **Rich API** che supporta query basate su testo e su oggetti, permettendoti di scegliere lo stile che si adatta alla tua architettura.  
- **Built‑in language support** per stemming, stop‑words e fuzzy matching su oltre 30 lingue.  
- **Easy integration** con Maven o download diretto del JAR, richiedendo solo poche righe di codice per iniziare.

## Prerequisiti
Before diving in, make sure you have:

- **GroupDocs.Search for Java** (v25.4 o successivo) – vedi il link per il download qui sotto.  
- JDK 8+ installato e configurato nel tuo IDE (IntelliJ IDEA, Eclipse, ecc.).  
- Conoscenze di base di Java e Maven per la gestione delle dipendenze.  

## Configurazione di GroupDocs.Search per Java

### Configurazione Maven
Add the repository and dependency to your `pom.xml`:

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
Alternatively, download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
Inizia con una licenza di prova gratuita per esplorare tutte le funzionalità. Per l'uso in produzione, acquista una licenza commerciale per sbloccare tutte le funzionalità.

### Inizializzazione e configurazione di base
Create an index folder and instantiate the `Index` object:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Come creare boolean query java?
La classe `Index` rappresenta una collezione ricercabile di documenti memorizzati su disco. Un `BooleanQuery` combina più sotto‑query con operatori logici. `createAndQuery`, `createOrQuery` e `createNotQuery` costruiscono rispettivamente sotto‑query AND, OR e NOT. Carica o crea un'istanza di `Index`, aggiungi i documenti, quindi costruisci un oggetto `BooleanQuery` usando `createAndQuery`, `createOrQuery` o `createNotQuery`. Chiama `index.search(query)` per recuperare i documenti corrispondenti. Questo modello funziona sia per scenari semplici che complessi e richiede solo tre passaggi logici: inizializzazione dell'indice, aggiunta dei documenti e esecuzione della query.

## Ricerca Boolean AND

### Panoramica
Una query AND restringe i risultati, migliorando la rilevanza quando hai bisogno di documenti che soddisfano più criteri.

### Passaggi di implementazione

1. **Initialize Index** – questo dimostra anche **add documents to index** per lo scenario AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – usando la sintassi di stringa semplice.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – utile quando si costruiscono query programmaticamente (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Ricerca Boolean OR

### Panoramica
Una query OR è ideale per ricerche esplorative in cui vuoi catturare documenti contenenti almeno una di diverse parole chiave (**search with or java**).

### Passaggi di implementazione

1. **Initialize Index** – questo dimostra anche **add documents to index** per lo scenario OR.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Ricerca Boolean NOT

### Panoramica
Una query NOT ti aiuta a eliminare documenti irrilevanti, ad esempio filtrando il nome di un marchio concorrente (**boolean search examples java**).

### Passaggi di implementazione

1. **Initialize Index** – questo dimostra anche **add documents to index** per lo scenario NOT.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Query Boolean complesse

### Panoramica
Le query complesse ti permettono di modellare scenari di ricerca reali, come “trovare articoli sportivi favorevoli ma escludere qualsiasi menzione di atleti specifici”.

### Passaggi di implementazione

1. **Initialize Index** – questo dimostra anche **add documents to index** per lo scenario complesso.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Applicazioni pratiche delle query **java boolean and or**
- **Document Management Systems** – individua contratti che contengono sia “confidential” **AND** “renewal”.  
- **Legal Research** – filtra la giurisprudenza con **AND**/ **OR** escludendo leggi obsolete usando **NOT**.  
- **Customer Support** – recupera ticket che menzionano “login” **AND** “error” ma non “resolved”.  
- **Content Curation** – raccogli post di blog su “cloud” **OR** “serverless” per una newsletter.

## Problemi comuni e risoluzione
- **Missing Index Refresh** – dopo aver aggiunto nuovi documenti, chiama `index.update()` per garantire che siano ricercabili.  
- **Incorrect Operator Spacing** – GroupDocs.Search si aspetta spazi attorno agli operatori (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – le query sono insensibili al maiuscolo/minuscolo per impostazione predefinita, ma gli analizzatori personalizzati possono influire su questo.  
- **Large Result Sets** – usa la paginazione (`search(query, 0, 100)`) per evitare sovraccarichi di memoria.  

## Domande frequenti

**Q: Posso combinare più di due termini in una query AND?**  
A: Assolutamente. Puoi concatenare più oggetti `createWordQuery` con `createAndQuery`, oppure scrivere semplicemente `"term1 AND term2 AND term3"` nella query di testo.

**Q: GroupDocs.Search supporta ricerche wildcard o fuzzy?**  
A: Sì. Aggiungi `*` per il wildcard (es., `promot*`) o usa `~` per il fuzzy matching (es., `comfort~`).

**Q: Come limito la ricerca a tipi di file specifici?**  
`FileTypeQuery` limita i risultati della ricerca a formati di file particolari come PDF o DOCX.  
A: Usa la classe `FileTypeQuery` per restringere i risultati a PDF, DOCX, ecc., e combinala con la tua query booleana.

**Q: Qual è il modo migliore per monitorare le prestazioni dell'indicizzazione?**  
A: Abilita il logger integrato (`index.getLogger().setLevel(Level.INFO)`) e controlla le metriche di tempo dopo ogni operazione `add`.

**Q: Esiste un modo per aumentare la rilevanza di alcuni termini?**  
`BoostQuery` aumenta il punteggio di rilevanza dei termini specificati in una query di ricerca.  
A: Sì. Avvolgi le parole importanti con `BoostQuery` per aumentare il loro peso nell'algoritmo di punteggio.

---

**Ultimo aggiornamento:** 2026-07-21  
**Testato con:** GroupDocs.Search 25.4 (Java)  
**Autore:** GroupDocs

## Tutorial correlati

- [Operatori Booleani Java – Crea indice di ricerca e ricerca sfaccettata](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java: Ricerca efficiente di documenti e gestione dell'indice](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Padroneggiare GroupDocs.Search Java – Creare e gestire un indice di ricerca](/search/java/indexing/groupdocs-search-java-create-index-guide/)