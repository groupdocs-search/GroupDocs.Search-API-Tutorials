---
date: '2025-12-18'
description: Scopri come implementare ricerche Java con formato data personalizzato
  usando GroupDocs.Search, includendo query di intervallo di date, pattern personalizzati
  e consigli sulle prestazioni.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'Formato data personalizzato Java: ricerca per intervallo di date con GroupDocs'
type: docs
url: /it/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Formato data personalizzato Java: Ricerca intervallo di date con GroupDocs

La ricerca di documenti per data è una necessità frequente—che tu stia costruendo un sistema di archiviazione, uno strumento di reportistica finanziaria o un portale di gestione dei contenuti. In questo tutorial imparerai le tecniche di **custom date format java** usando GroupDocs.Search, coprendo le query di intervallo di date, le definizioni di pattern personalizzati e consigli per **ottimizzare le prestazioni della ricerca**. Alla fine, sarai in grado di consentire agli utenti di recuperare i record che rientrano in qualsiasi intervallo di date, indipendentemente dal formato utilizzato.

## Risposte rapide
- **Qual è la classe principale per l'indicizzazione?** `Index` dal pacchetto `com.groupdocs.search`.  
- **Come si definisce un pattern di data personalizzato?** Usa `DateFormat` con oggetti `DateFormatElement` e un separatore.  
- **Posso cercare con una query testuale?** Sì, la sintassi `daterange(start ~~ end)` funziona direttamente nella stringa di query.  
- **Quali coordinate Maven sono necessarie?** `com.groupdocs:groupdocs-search:25.4` (o più recenti).  
- **È necessaria una licenza per lo sviluppo?** Una prova gratuita o una licenza temporanea è sufficiente per i test; è richiesta una licenza commerciale per la produzione.

## Cos'è **custom date format java**?
Un **custom date format java** indica a GroupDocs.Search come interpretare le stringhe di data che non seguono il pattern ISO predefinito (YYYY‑MM‑DD). Definendo il tuo pattern—come `MM/dd/yyyy` o `dd‑MM‑yyyy`—consenti al motore di riconoscere le date incorporate nei documenti che usano formati regionali o legacy.

## Perché usare GroupDocs.Search per le query di intervallo di date?
- **Velocità:** L'indicizzazione integrata rende le ricerche O(log n).  
- **Flessibilità:** Supporta sia la creazione di query basate su testo sia su oggetti.  
- **Supporto multi‑formato:** Gestisce PDF, Word, Excel, testo semplice e altro senza codice aggiuntivo.  

## Come **search documents by date** con GroupDocs.Search
Di seguito trovi una guida passo‑paso che ti accompagna nella configurazione della libreria, indicizzazione dei file ed esecuzione di ricerche di intervallo di date sia semplici che avanzate.

### Prerequisiti
- Java 8 o versioni successive installate.  
- Maven per la gestione delle dipendenze.  
- Accesso a una licenza GroupDocs.Search (la versione di prova o temporanea funziona per lo sviluppo).  

### Configurazione di GroupDocs.Search per Java

#### Installazione con Maven
Aggiungi il repository e la dipendenza al tuo `pom.xml`:

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
Crea un'istanza `Index` e aggiungi i tuoi documenti:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Funzionalità 1: Creazione di query di ricerca per intervallo di date

### Uso della query in forma testuale
Il modo più semplice è incorporare l'intervallo di date direttamente nella stringa di query:

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

**Spiegazione**: La sintassi `daterange` si aspetta date nel formato `YYYY‑MM‑DD`. Restituisce tutti i documenti le cui date indicizzate rientrano nell'intervallo.

### Uso dell'oggetto Query
Per un controllo programmatico e parsing personalizzato, costruisci un oggetto `SearchQuery`:

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

**Spiegazione**: `createDateRangeQuery` consente di fornire oggetti `java.util.Date`, offrendo piena flessibilità su fusi orari e gestione specifica per locale.

## Funzionalità 2: Specificare i pattern **custom date format java**
### Impostazione dei formati data personalizzati
Definisci un `DateFormat` che corrisponda alla rappresentazione della data nel tuo documento:

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

**Spiegazione**: Cancellando i formati predefiniti e aggiungendo un `DateFormat` che utilizza `/` come separatore, il motore ora comprende le date scritte come `MM/dd/yyyy`. Questo è essenziale per **search documents by date** nelle regioni che preferiscono la notazione mese‑primo.

## Consigli per **optimize search performance**
- **Indicizza incrementalmente**: Aggiungi nuovi file all'indice esistente invece di ricostruirlo da zero.  
- **Rimuovi dati obsoleti**: Rimuovi periodicamente i documenti non più necessari.  
- **Regola le impostazioni di memoria**: Aumenta l'heap JVM (`-Xmx`) quando lavori con indici di grandi dimensioni.  

## Problemi comuni e soluzioni
- **Errori di parsing della data**: Verifica che le stringhe di data del documento corrispondano esattamente al pattern personalizzato definito.  
- **Risultati mancanti**: Assicurati che i campi indicizzati contengano metadati di data; altrimenti, il motore non può corrispondere alle query di data.  
- **Eccezioni di accesso all'indice**: Conferma che il percorso `indexFolder` sia scrivibile e non bloccato da un altro processo.

## Applicazioni pratiche
1. **Sistemi di archiviazione** – Recupera record da un periodo storico specifico.  
2. **Gestione dei contenuti** – Supporta formati data regionali come `dd/MM/yyyy` per il pubblico europeo.  
3. **Software finanziario** – Filtra le transazioni per trimestre fiscale o anno rapidamente.

## Conclusione
Ora disponi di un toolbox completo **custom date format java** per costruire ricerche potenti di intervallo di date con GroupDocs.Search. Implementa questi pattern, ottimizza le prestazioni e la tua applicazione fornirà risultati rapidi e accurati per qualsiasi query temporale.

## Domande frequenti

**Q: Qual è la differenza tra le query di data in forma testuale e quelle basate su oggetti?**  
A: La forma testuale è rapida e semplice ma limitata al formato ISO predefinito; le query basate su oggetti consentono di fornire oggetti `Date` e formati personalizzati per maggiore flessibilità.

**Q: Posso cercare più intervalli di date in una singola query?**  
A: Sì, combina le clausole `daterange` con operatori logici come `AND` o `OR` per costruire query complesse.

**Q: I formati data personalizzati rallenteranno la ricerca?**  
A: C'è un leggero overhead per il parsing aggiuntivo, ma l'impatto è trascurabile per i carichi di lavoro tipici ed è compensato dai guadagni in precisione.

**Q: GroupDocs.Search è adatto per distribuzioni su larga scala?**  
A: Assolutamente. Con strategie di indicizzazione appropriate e ottimizzazione della JVM, scala a milioni di documenti.

**Q: Dove posso trovare altri esempi Java?**  
A: Esplora il [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) per ulteriori esempi e implementazioni di casi d'uso.

**Risorse**
- **Documentazione**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Riferimento API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **Repository GitHub**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum di supporto gratuito**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Licenza temporanea**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

**Ultimo aggiornamento:** 2025-12-18  
**Testato con:** GroupDocs.Search Java 25.4  
**Autore:** GroupDocs