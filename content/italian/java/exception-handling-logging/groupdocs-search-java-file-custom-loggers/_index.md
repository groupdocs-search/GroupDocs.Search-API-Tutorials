---
date: '2026-09-21'
description: Scopri come creare il logger, impostare la dimensione massima del log
  e utilizzare il console logger in GroupDocs.Search for Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Scopri come creare il logger, impostare la dimensione massima del
  log e utilizzare il console logger in GroupDocs.Search for Java. Segui istruzioni
  passo‑passo e consigli sulle migliori pratiche.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Come creare il logger e limitare la dimensione del log in GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Come creare il logger e limitare la dimensione del log in GroupDocs.Search
  for Java
type: docs
url: /it/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Come creare un logger e limitare la dimensione del file di log in GroupDocs.Search per Java

In questo tutorial imparerai **come creare un logger** per GroupDocs.Search, configurare una dimensione massima del file di log e passare dal logging basato su file a quello su console. Una corretta gestione dei log impedisce che i dischi si riempiano durante grandi operazioni di indicizzazione, migliora il troubleshooting e fornisce feedback immediato durante lo sviluppo. Inizieremo con la configurazione di Maven, passeremo attraverso la configurazione del logger e concluderemo con una semplice query di ricerca che dimostra il logger in azione.

## Risposte rapide
- **Cosa significa “limit log file size”?** Limita la dimensione massima di un file di log, impedendo una crescita incontrollata sul disco.  
- **Quale logger consente di limitare la dimensione del file di log?** Il `FileLogger` integrato accetta un parametro di dimensione massima.  
- **Come utilizzo il console logger in Java?** Istanziare `ConsoleLogger` e impostarlo su `IndexSettings`.  
- **È necessaria una licenza per GroupDocs.Search?** Una versione di prova è sufficiente per la valutazione; è necessaria una licenza commerciale per la produzione.  
- **Qual è il primo passo?** Aggiungere la dipendenza GroupDocs.Search al progetto Maven.  

## Cos'è il limite della dimensione del file di log?
L'impostazione **limit log file size** indica al logger di smettere di scrivere nuove voci una volta che il file raggiunge una soglia definita (ad esempio, 4 MB). Quando il limite è raggiunto, il logger scarta i messaggi successivi o passa a un nuovo file, mantenendo prevedibile l'utilizzo del disco.

## Perché utilizzare logger su file e personalizzati con GroupDocs.Search?
I logger su file e personalizzati offrono auditabilità, approfondimenti di debug e flessibilità. Negli ambienti di produzione, i log su file forniscono una registrazione permanente di ogni operazione di indicizzazione e ricerca, mentre i log su console forniscono feedback immediato durante lo sviluppo. Questi log aiutano i team a monitorare le prestazioni, tracciare gli errori e soddisfare i requisiti di conformità preservando una traccia dettagliata delle attività.

## Prerequisiti
- GroupDocs.Search per Java ≥ 25.4.  
- JDK 8 o superiore, con un IDE come IntelliJ IDEA o Eclipse.  
- Familiarità di base con Maven e la programmazione Java.  

## Configurare GroupDocs.Search per Java

Aggiungi la libreria al tuo progetto usando uno dei metodi seguenti.

**Configurazione Maven:**  

```text
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
```

**Download diretto:**  
Scarica l'ultimo JAR dal sito ufficiale: [GroupDocs.Search per Java releases](https://releases.groupdocs.com/search/java/).

### Ottenimento della licenza
Ottieni una versione di prova o acquista una licenza tramite la [pagina di licenza](https://purchase.groupdocs.com/temporary-license/).

## Come creare un logger personalizzato per GroupDocs.Search
Creare un logger personalizzato è semplice perché GroupDocs.Search si basa sull'interfaccia `ILogger`. Implementando questa interfaccia — o estendendo i forniti `FileLogger` o `ConsoleLogger` — è possibile iniettare comportamenti aggiuntivi come il forwarding remoto o la rotazione dei log. È inoltre possibile aggiungere logica di inizializzazione, come l'apertura di connessioni di rete, e garantire che le risorse vengano chiuse nel metodo di spegnimento del logger. Questo approccio consente di integrarsi con piattaforme di monitoraggio come ELK o Splunk.

### Definizione
`ILogger` è il contratto di logging principale in GroupDocs.Search; qualsiasi classe che implementa il suo metodo `log(Level, String)` può diventare un logger.

### Approccio di esempio (senza blocco di codice)
1. Crea una classe che implementa `ILogger`.  
2. Sovrascrivi il metodo `log` per scrivere i messaggi nella destinazione scelta (file, database, endpoint HTTP).  
3. Nella configurazione dell'indice, chiama `settings.setLogger(new YourCustomLogger())`.  

## Come limitare la dimensione del file di log con File Logger
La classe `FileLogger` scrive le voci di log su un file su disco e accetta un argomento di dimensione massima. Specificando il limite di dimensione, il logger interrompe automaticamente l'aggiunta di nuove voci o crea un nuovo file quando la soglia è raggiunta, evitando una crescita incontrollata del disco. Questo comportamento garantisce che il logging non interferisca con le prestazioni di indicizzazione mantenendo al contempo un registro conciso degli eventi.

### Definizione
`FileLogger` è un logger integrato che persiste i messaggi in un file di testo e supporta una dimensione massima del file configurabile.

### Guida passo‑passo
1️⃣ **Importa i pacchetti necessari**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Configura le impostazioni dell'indice con File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Crea o carica l'indice**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Aggiungi documenti all'indice**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Esegui una query di ricerca**  
```text
```java
SearchResult result = index.search(query);
```
```

**Punto chiave:** Il secondo argomento del costruttore `FileLogger` (`4.0`) definisce il **set max log size** in megabyte, rispondendo direttamente al requisito di **limit log file size**.

## Come utilizzare console logger in Java
Quando hai bisogno di visibilità immediata degli eventi di log, il `ConsoleLogger` scrive ogni messaggio su `System.out`. Questo logger è leggero e thread‑safe, rendendolo adatto a sessioni di sviluppo e debug. Fornisce feedback immediato sul progresso dell'indicizzazione, sulle query di ricerca e sulle condizioni di errore senza richiedere I/O su file, il che può accelerare i test iterativi.

### Definizione
`ConsoleLogger` è un logger leggero che invia le voci di log allo stream della console standard, rendendolo ideale per le sessioni di debug.

### Passaggi di configurazione
1️⃣ **Importa il console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Configura le impostazioni dell'indice con Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Crea o carica l'indice**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Aggiungi documenti ed esegui una ricerca**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Suggerimento:** Il console logger è ideale durante lo sviluppo perché stampa ogni voce di log istantaneamente, aiutandoti a verificare che l'indicizzazione e la ricerca si comportino come previsto.

## Applicazioni pratiche
1. **Sistemi di gestione documentale:** Conserva le tracce di audit di ogni documento indicizzato, soddisfacendo i requisiti di conformità.  
2. **Motori di ricerca aziendali:** Monitora le prestazioni delle query e i tassi di errore in tempo reale, consentendo rapidi controlli di conformità SLA.  
3. **Software legale e di conformità:** Registra i termini di ricerca e i timestamp per la reportistica normativa, mantenendo i log per il periodo di conservazione obbligatorio.

## Considerazioni sulle prestazioni
- **Dimensione del log:** Con **set max log size**, eviti un utilizzo eccessivo del disco che potrebbe altrimenti rallentare il garbage collector della JVM.  
- **Logging asincrono:** Per scenari ad alto throughput, avvolgi il tuo logger in una coda asincrona per disaccoppiare I/O dal thread di indicizzazione (implementazione al di fuori dello scopo di questa guida).  
- **Gestione della memoria:** Rilascia gli oggetti `Index` di grandi dimensioni con `index.close()` quando non sono più necessari per mantenere basso l'impronta della JVM.

## Problemi comuni e soluzioni
- **Percorso del log non accessibile:** Verifica che la directory esista e che l'applicazione abbia i permessi di scrittura per l'account utente che esegue la JVM.  
- **Logger non attivo:** Assicurati di chiamare `settings.setLogger(...)` *prima* di creare l'oggetto `Index`; altrimenti viene usato il logger predefinito.  
- **Output della console mancante:** Conferma di eseguire l'applicazione in un terminale che visualizza `System.out` e che nessun framework di logging (ad es., SLF4J) stia intercettando l'output.

## Domande frequenti

**D: Cosa controlla il secondo parametro di `FileLogger`?**  
R: Imposta la dimensione massima del file di log in megabyte, consentendoti di **set max log size** e prevenire una crescita incontrollata.

**D: Posso combinare logger su file e console?**  
R: Sì. Crea un logger personalizzato che inoltra ogni chiamata `log` sia a un `FileLogger` sia a un `ConsoleLogger`, quindi registra quel logger composito con `IndexSettings`.

**D: Come aggiungo documenti all'indice dopo la creazione iniziale?**  
R: Chiama `index.add(pathToNewDocs)` in qualsiasi momento; il logger configurato registrerà automaticamente l'aggiunta.

**D: `ConsoleLogger` è thread‑safe?**  
R: Scrive direttamente su `System.out`, che la JVM sincronizza internamente, rendendolo sicuro per i tipici casi d'uso multi‑thread.

**D: Limitare la dimensione del file di log influenzerà la quantità di informazioni memorizzate?**  
R: Una volta raggiunto il limite di dimensione, le nuove voci vengono scartate o il logger passa a un nuovo file, a seconda dell'implementazione scelta.

## Risorse
- [Documentazione](https://docs.groupdocs.com/search/java/)
- [Riferimento API](https://reference.groupdocs.com/search/java/)

---

**Ultimo aggiornamento:** 2026-09-21  
**Testato con:** GroupDocs.Search per Java 25.4  
**Autore:** GroupDocs  

## Tutorial correlati

- [Come implementare il logging - Tutorial su gestione delle eccezioni e logging per GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implementare il logging asincrono in Java con GroupDocs.Search – Guida al logger personalizzato](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Creare indice di ricerca Java – Tutorial GroupDocs.Search](/search/java/indexing/)