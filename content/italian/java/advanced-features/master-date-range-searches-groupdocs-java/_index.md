---
date: '2026-10-07'
description: Scopri come implementare ricerche con custom date format java con GroupDocs,
  coprendo date range queries, custom patterns e performance tips.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: Il tutorial su Custom date format java mostra come configurare GroupDocs.Search
  per Java, eseguire date range queries e migliorare le prestazioni. Segui esempi
  passo‑passo.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Custom date format java – guida alla ricerca per intervallo di date con
  GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Formato data personalizzato java | ricerca per intervallo di date con GroupDocs
type: docs
url: /it/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Formato data personalizzato java | ricerca intervallo date con GroupDocs

Cercare documenti per data è una necessità frequente—che tu stia costruendo un sistema di archiviazione, uno strumento di reporting finanziario o un portale di gestione dei contenuti. In questo tutorial imparerai le tecniche **custom date format java** usando GroupDocs.Search, coprendo le query di intervallo di date, le definizioni di pattern personalizzati e consigli per **optimize search performance**. Alla fine, sarai in grado di consentire agli utenti di recuperare i record che rientrano in qualsiasi intervallo di date, indipendentemente dal formato utilizzato.

## Risposte rapide
- **Qual è la classe principale per l'indicizzazione?** `Index` dal pacchetto `com.groupdocs.search`.  
- **Come si definisce un pattern di data personalizzato?** Usa `DateFormat` con oggetti `DateFormatElement` e un separatore.  
- **Posso cercare con una query di testo?** Sì, la sintassi `daterange(start ~~ end)` funziona direttamente nella stringa di query.  
- **Quali coordinate Maven sono richieste?** `com.groupdocs:groupdocs-search:25.4` (o più recenti).  
- **È necessaria una licenza per lo sviluppo?** Una prova gratuita o una licenza temporanea è sufficiente per i test; è necessaria una licenza commerciale per la produzione.

## Cos'è custom date format java?
Custom date format java indica a GroupDocs.Search come interpretare le stringhe di data che non seguono il pattern ISO predefinito (YYYY‑MM‑DD). Definendo il tuo pattern—come `MM/dd/yyyy` o `dd‑MM‑yyyy`—consenti al motore di riconoscere le date incorporate nei documenti che usano formati regionali o legacy. Questa capacità ti permette di indicizzare e interrogare le date in modo coerente su fonti eterogenee, migliorando sia il richiamo sia la precisione per le ricerche incentrate sulle date.

## Perché usare GroupDocs.Search per le query di intervallo di date?
GroupDocs.Search combina indicizzazione ad alta velocità con una costruzione di query flessibile, rendendolo ideale per scenari di intervallo di date. Il motore può individuare rapidamente i documenti che contengono date entro un intervallo specificato, anche quando tali date appaiono in testo libero o nei campi di metadati. Il suo supporto integrato per più formati di file e parser di data personalizzabili significa che puoi gestire collezioni di documenti diverse senza scrivere codice specifico per il formato, mantenendo tempi di risposta inferiori al secondo su indici di grandi dimensioni.

## Come cercare documenti per data con GroupDocs.Search
Imposterai la libreria, indicizzerai una cartella di esempio e poi eseguirai sia query di testo semplici sia query basate su oggetti più ricche. Il processo inizia creando un'istanza `Index`, configurando eventuali formati di data personalizzati necessari, e poi invocando l'API di ricerca con una stringa semplice o un `SearchQuery` strutturato. Questo approccio ti consente di scegliere il livello di controllo che corrisponde ai requisiti della tua applicazione.

### Prerequisiti
- Java 8 o versioni successive installate.  
- Maven per la gestione delle dipendenze.  
- Accesso a una licenza GroupDocs.Search (la versione di prova o temporanea funziona per lo sviluppo).  

### Configurazione di GroupDocs.Search per Java

#### Installazione con Maven
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

#### Download diretto
In alternativa, puoi scaricare l'ultima versione direttamente da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Inizializzazione e configurazione di base
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** La classe `Index` è il contenitore principale che memorizza i metadati ricercabili per ogni file aggiunto, consentendo ricerche rapide su grandi collezioni.

## Funzione 1: creare query di ricerca per intervallo di date

### Utilizzo della query in forma di testo
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** Carica il tuo indice, quindi chiama `search("daterange(2022-01-01 ~~ 2022-12-31)")` per recuperare ogni documento la cui data indicizzata cade tra il 1 gennaio 2022 e il 31 dicembre 2022. Questa query a una riga funziona subito e restituisce i risultati ordinati per rilevanza.

**Explanation:** La sintassi `daterange` si aspetta date nel formato `YYYY‑MM‑DD`. Restituisce tutti i documenti le cui date indicizzate ricadono nell'intervallo.

### Utilizzo dell'oggetto query
Per un controllo programmatico e un parsing personalizzato, costruisci un oggetto `SearchQuery`. La classe `SearchQuery` rappresenta una query strutturata che può combinare più criteri come parole chiave, filtri e intervalli di date.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** Costruisci un `SearchQuery` con `createDateRangeQuery(startDate, endDate)` dove `startDate` e `endDate` sono istanze `java.util.Date`; quindi passa la query a `index.search(query)` per ottenere risultati precisi che rispettano gli offset del fuso orario e i calendari specifici per locale.

**Definition anchor:** La classe `SearchQuery` incapsula tutti i criteri di ricerca, consentendoti di combinare intervalli di date con filtri di parole chiave, operatori booleani e regole di boosting.

**Explanation:** `createDateRangeQuery` ti consente di fornire oggetti `java.util.Date`, offrendoti piena flessibilità su fusi orari e gestione specifica per locale.

## Funzione 2: specificare pattern custom date format java

### Impostazione dei formati di data personalizzati
La classe `DateFormat` indica al motore come suddividere e interpretare una stringa di data in base all'ordine degli elementi e ai caratteri separatori. Definisci un `DateFormat` che corrisponda alla rappresentazione della data nel tuo documento:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** Cancella i formati predefiniti con `dateFormat.clear()`, quindi aggiungi un nuovo `DateFormat` costruito da oggetti `DateFormatElement` (mese, giorno, anno) e imposta il separatore su `/`. Dopo ciò, il motore interpreterà correttamente le date scritte come `MM/dd/yyyy` durante l'indicizzazione e la query.

**Definition anchor:** `DateFormat` è un oggetto di configurazione che indica a GroupDocs.Search come suddividere e interpretare una stringa di data in base all'ordine degli elementi e ai caratteri separatori.

**Explanation:** Cancellando i formati predefiniti e aggiungendo un `DateFormat` che usa `/` come separatore, il motore ora comprende le date scritte come `MM/dd/yyyy`. Questo è essenziale per **search documents by date** nelle regioni che preferiscono la notazione mese‑primo.

## Suggerimenti per ottimizzare le prestazioni di ricerca
- **Indicizzare in modo incrementale:** Aggiungi nuovi file all'indice esistente invece di ricostruirlo da zero; ciò riduce l'uso della CPU fino al 70 % per gli aggiornamenti giornalieri.  
- **Eliminare dati obsoleti:** Rimuovi periodicamente i documenti non più necessari; un indice snello migliora i tassi di hit della cache e riduce la latenza delle query.  
- **Regolare le impostazioni di memoria:** Aumenta l'heap JVM (`-Xmx4g` o superiore) quando lavori con indici più grandi di 5 GB per evitare errori di out‑of‑memory.  
- **Abilitare l'indicizzazione multithread:** Usa `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` per parallelizzare l'elaborazione dei documenti e ridurre il tempo di indicizzazione di circa il numero di core CPU.

## Problemi comuni e soluzioni
- **Errori di parsing della data:** Verifica che le stringhe di data del documento corrispondano esattamente al pattern personalizzato definito; separatori non corrispondenti o zeri iniziali mancanti causano errori.  
- **Risultati mancanti:** Assicurati che i campi indicizzati contengano metadati di data; se un documento ha solo date in paragrafi di testo libero, abilita l'opzione `ExtractDateMetadata` durante l'indicizzazione.  
- **Eccezioni di accesso all'indice:** Conferma che il percorso `indexFolder` sia scrivibile e non bloccato da un altro processo; usa una cartella dedicata per ogni ambiente (dev, test, prod) per evitare conflitti.

## Applicazioni pratiche
1. **Sistemi di archiviazione** – Recupera record da un periodo storico specifico senza normalizzare manualmente le date.  
2. **Gestione dei contenuti** – Supporta formati di data regionali come `dd/MM/yyyy` per il pubblico europeo, migliorando la soddisfazione degli utenti.  
3. **Software finanziario** – Filtra le transazioni per trimestre fiscale o anno rapidamente, consentendo dashboard di reporting in tempo reale.

## Perché è importante
Implementare la gestione **custom date format java** elimina le difficoltà legate a rappresentazioni di data incoerenti nei documenti. Ti consente di **handle multiple date formats** in un unico indice, garantendo che gli utenti finali ottengano risultati accurati indipendentemente da come le date sono state originariamente registrate. Questa flessibilità migliora la rilevanza della ricerca, riduce lo sforzo di pre‑elaborazione e accorcia il time‑to‑value per le applicazioni incentrate sulle date.

## Prossimi passi
- Esplora combinazioni di query più avanzate usando gli operatori `AND`, `OR` e `NOT`.  
- Sperimenta con analyzer personalizzati se devi indicizzare metadati temporali aggiuntivi come timestamp incorporati in tag XML.  
- Consulta la guida di ottimizzazione delle prestazioni nella documentazione ufficiale per scalare la tua soluzione a milioni di documenti e ambienti multi‑tenant.

## Domande frequenti

**Q: Qual è la differenza tra le query in forma di testo e quelle basate su oggetti per le date?**  
A: La forma di testo è rapida e semplice ma limitata al formato ISO predefinito; le query basate su oggetti ti consentono di fornire oggetti `Date` e formati personalizzati per maggiore flessibilità.

**Q: Posso cercare più intervalli di date in una singola query?**  
A: Sì, combina clausole `daterange` con operatori logici come `AND` o `OR` per costruire query complesse.

**Q: I formati di data personalizzati rallenteranno la ricerca?**  
A: C'è un piccolo overhead per il parsing aggiuntivo, ma l'impatto è trascurabile per i carichi di lavoro tipici ed è compensato dai guadagni in precisione.

**Q: GroupDocs.Search è adatto per distribuzioni su larga scala?**  
A: Assolutamente. Con strategie di indicizzazione adeguate e ottimizzazione della JVM, scala a milioni di documenti mantenendo tempi di risposta alle query inferiori al secondo.

**Q: Dove posso trovare più esempi Java?**  
A: Esplora il [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) per ulteriori esempi e implementazioni di casi d'uso.

---

**Risorse**
- **Documentazione:** [Documentazione GroupDocs Search](https://docs.groupdocs.com/search/java/)
- **Riferimento API:** [Riferimento API GroupDocs](https://reference.groupdocs.com/search/java)
- **Download:** [Scarica l'ultima versione qui](https://releases.groupdocs.com/search/java/)
- **Repository GitHub:** [Repository GitHub GroupDocs](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Visualizza su GitHub:** [Visualizza su GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum di supporto gratuito:** [Partecipa alla discussione](https://forum.groupdocs.com/c/search/10)
- **Licenza temporanea:** [Ottieni una licenza temporanea qui](https://purchase.groupdocs.com/temporary-license/)

**Ultimo aggiornamento:** 2026-10-07  
**Testato con:** GroupDocs.Search Java 25.4  
**Autore:** GroupDocs  

## Tutorial correlati

- [Funzionalità avanzate di ricerca Java di Groupdocs Search](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Libreria Java di ricerca full-text – Ottimizza l'indice con GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Come aggiungere documenti all'indice con indicizzazione dei metadati in Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)