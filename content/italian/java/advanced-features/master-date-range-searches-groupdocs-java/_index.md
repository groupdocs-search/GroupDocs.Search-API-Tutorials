---
date: '2026-03-04'
description: Scopri come implementare ricerche Java con formato data personalizzato
  usando GroupDocs.Search, coprendo le query di intervallo di date, i pattern personalizzati
  e i consigli sulle prestazioni.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: Formato Data Personalizzato Java | Ricerca Intervallo di Date con GroupDocs
type: docs
url: /it/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Formato data personalizzato Java | Ricerca intervallo di date con GroupDocs

La ricerca di documenti per data è una necessità frequente—che tu stia costruendo un sistema di archiviazione, uno strumento di reporting finanziario o un portale di gestione dei contenuti. In questo tutorial imparerai le tecniche di **custom date format java** usando GroupDocs.Search, coprendo le query di intervallo di date, le definizioni di pattern personalizzati e consigli per **ottimizzare le prestazioni della ricerca**. Alla fine, potrai consentire agli utenti di recuperare i record che rientrano in qualsiasi intervallo di date, indipendentemente dal formato utilizzato.

## Risposte rapide
- **Qual è la classe principale per l'indicizzazione?** `Index` dal pacchetto `com.groupdocs.search`.  
- **Come si definisce un pattern di data personalizzato?** Usa `DateFormat` con oggetti `DateFormatElement` e un separatore.  
- **Posso cercare con una query testuale?** Sì, la sintassi `daterange(start ~~ end)` funziona direttamente nella stringa di query.  
- **Quali coordinate Maven sono necessarie?** `com.groupdocs:groupdocs-search:25.4` (o versioni più recenti).  
- **È necessaria una licenza per lo sviluppo?** Una prova gratuita o una licenza temporanea è sufficiente per i test; è necessaria una licenza commerciale per la produzione.

## Cos'è **custom date format java**?
Un **custom date format java** indica a GroupDocs.Search come interpretare le stringhe di data che non seguono il pattern ISO predefinito (YYYY‑MM‑DD). Definendo il tuo pattern—ad esempio `MM/dd/yyyy` o `dd‑MM‑yyyy`—consenti al motore di riconoscere le date incorporate nei documenti che utilizzano formati regionali o legacy.

## Perché usare GroupDocs.Search per le query di intervallo di date?
- **Velocità:** L'indicizzazione integrata rende le ricerche O(log n).  
- **Flessibilità:** Supporta sia la creazione di query basate su testo che su oggetti.  
- **Supporto multi‑formato:** Gestisce PDF, Word, Excel, testo semplice e altro senza codice aggiuntivo.  

## Come **cercare documenti per data** con GroupDocs.Search
Di seguito trovi una guida passo‑passo che ti accompagna nella configurazione della libreria, indicizzazione dei file e nell'esecuzione di ricerche di intervallo di date sia semplici che avanzate.

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

## Funzionalità 1: Creazione di query di ricerca intervallo di date

### Utilizzo della query in forma testuale
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

**Spiegazione**: La sintassi `daterange` si aspetta date nel formato `YYYY‑MM‑DD`. Restituisce tutti i documenti le cui date indicizzate ricadono nell'intervallo.

### Utilizzo dell'oggetto Query
For programmatic control and custom parsing, build a `SearchQuery` object:

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

**Spiegazione**: `createDateRangeQuery` consente di fornire oggetti `java.util.Date`, offrendo piena flessibilità su fusi orari e gestione specifica della locale.

## Funzionalità 2: Specificare i pattern **custom date format java**
### Impostazione dei formati data personalizzati
Define a `DateFormat` that matches your document’s date representation:

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

**Spiegazione**: Cancellando i formati predefiniti e aggiungendo un `DateFormat` che utilizza `/` come separatore, il motore ora comprende le date scritte come `MM/dd/yyyy`. Questo è essenziale per **cercare documenti per data** nelle regioni che preferiscono la notazione mese‑primo.

## Consigli per **ottimizzare le prestazioni della ricerca**
- **Indicizzare incrementalmente**: Aggiungi nuovi file all'indice esistente invece di ricostruirlo da zero.  
- **Eliminare dati obsoleti**: Rimuovi periodicamente i documenti non più necessari.  
- **Regolare le impostazioni di memoria**: Aumenta l'heap JVM (`-Xmx`) quando lavori con indici di grandi dimensioni.  

## Problemi comuni e soluzioni
- **Errori di parsing della data**: Verifica che le stringhe di data del documento corrispondano esattamente al pattern personalizzato definito.  
- **Risultati mancanti**: Assicurati che i campi indicizzati contengano metadati di data; altrimenti il motore non può corrispondere alle query di data.  
- **Eccezioni di accesso all'indice**: Conferma che il percorso `indexFolder` sia scrivibile e non bloccato da un altro processo.  

## Applicazioni pratiche
1. **Sistemi di archiviazione** – Recupera record da un periodo storico specifico.  
2. **Gestione dei contenuti** – Supporta formati data regionali come `dd/MM/yyyy` per il pubblico europeo.  
3. **Software finanziario** – Filtra le transazioni per trimestre fiscale o anno rapidamente.  

## Perché è importante
Implementare la gestione di **custom date format java** elimina le difficoltà legate a rappresentazioni di data incoerenti nei documenti. Consente di **gestire più formati di data** in un unico indice, garantendo che gli utenti finali ottengano risultati accurati indipendentemente da come le date sono state originariamente registrate.

## Prossimi passi
- Esplora combinazioni di query più avanzate usando gli operatori `AND`, `OR` e `NOT`.  
- Sperimenta con analyzer personalizzati se devi indicizzare metadati temporali aggiuntivi.  
- Rivedi la guida di ottimizzazione delle prestazioni nella documentazione ufficiale per scalare la tua soluzione a milioni di documenti.  

## Domande frequenti

**D: Qual è la differenza tra le query di data in forma testuale e quelle basate su oggetti?**  
R: La forma testuale è rapida e semplice ma limitata al formato ISO predefinito; le query basate su oggetti consentono di fornire oggetti `Date` e formati personalizzati per una maggiore flessibilità.

**D: Posso cercare più intervalli di date in una singola query?**  
R: Sì, combina le clausole `daterange` con operatori logici come `AND` o `OR` per costruire query complesse.

**D: I formati di data personalizzati rallenteranno la ricerca?**  
R: C'è un leggero overhead per il parsing aggiuntivo, ma l'impatto è trascurabile per i carichi di lavoro tipici ed è compensato dai guadagni in precisione.

**D: GroupDocs.Search è adatto per implementazioni su larga scala?**  
R: Assolutamente. Con strategie di indicizzazione adeguate e ottimizzazione della JVM, scala a milioni di documenti.

**D: Dove posso trovare più esempi Java?**  
R: Esplora il [repository GitHub di GroupDocs](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) per ulteriori esempi e implementazioni di casi d'uso.

---

**Risorse**

- **Documentazione**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Riferimento API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Ottieni l'ultima versione qui](https://releases.groupdocs.com/search/java/)
- **Repository GitHub**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum di supporto gratuito**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Licenza temporanea**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-03-04  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs  

---