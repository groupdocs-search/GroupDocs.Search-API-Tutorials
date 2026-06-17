---
date: '2026-02-24'
description: Scopri come creare un logger personalizzato, impostare la dimensione
  massima del log e configurare il logger console o file in GroupDocs.Search per Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Come creare un logger personalizzato e limitare la dimensione del file di log
  con GroupDocs.Search Java
type: docs
url: /it/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

 exactly.

Check for any missing placeholders: CODE_BLOCK_0-9 present.

Check for any shortcodes: none.

Check for any markdown links: we have them.

Check for any images: none.

Now produce final output with translated content only.# Limita la dimensione del file di log con i logger Java di GroupDocs.Search

In questa guida **creerai implementazioni di logger personalizzati** e imparerai come **limitare la dimensione del file di log** utilizzando GroupDocs.Search per Java. Controllare la crescita dei log è fondamentale per l'indicizzazione di documenti su larga scala, e i logger integrati ti consentono di **impostare la dimensione massima del log**, **ruotare il file di log**, o passare a un **use console logger** per un feedback immediato. Esploriamo l'intera configurazione, dalla configurazione Maven all'esecuzione di una query di ricerca, e vediamo come **add documents index** con il logger attivo.

## Risposte rapide
- **Cosa significa “limit log file size”?** Limita la dimensione massima di un file di log, evitando una crescita incontrollata sul disco.  
- **Quale logger consente di limitare la dimensione del file di log?** Il `FileLogger` integrato accetta un parametro max‑size.  
- **Come si usa console logger java?** Istanzia `ConsoleLogger` e impostalo su `IndexSettings`.  
- **Ho bisogno di una licenza per GroupDocs.Search?** Una versione di prova è sufficiente per la valutazione; è necessaria una licenza commerciale per la produzione.  
- **Qual è il primo passo?** Aggiungi la dipendenza GroupDocs.Search al tuo progetto Maven.  

## Che cosa significa limitare la dimensione del file di log?
Limitare la dimensione del file di log significa configurare il logger in modo che, una volta che il file raggiunge una soglia predefinita (ad esempio 4 MB), smetta di crescere o venga ruotato. Questo mantiene l'impronta di archiviazione dell'applicazione prevedibile ed evita il degrado delle prestazioni.

## Perché usare logger file e personalizzati con GroupDocs.Search?
- **Auditability:** Conserva un registro permanente degli eventi di indicizzazione e ricerca.  
- **Debugging:** Identifica rapidamente i problemi esaminando log concisi.  
- **Flexibility:** Scegli tra log file persistenti e output console istantaneo (`use console logger`).  

## Prerequisiti
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 o superiore, IDE (IntelliJ IDEA, Eclipse, ecc.).  
- Conoscenze di base di Java e Maven.  

## Configurazione di GroupDocs.Search per Java

Aggiungi la libreria al tuo progetto utilizzando uno dei metodi seguenti.

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

**Download diretto:**  
Scarica l'ultimo JAR dal sito ufficiale: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
Ottieni una versione di prova o acquista una licenza tramite la [pagina di licenza](https://purchase.groupdocs.com/temporary-license/).

## Come creare un logger personalizzato per GroupDocs.Search
GroupDocs.Search consente di collegare qualsiasi implementazione dell'interfaccia `ILogger`. Estendendo `FileLogger` o `ConsoleLogger`, è possibile aggiungere comportamenti extra—come ruotare il file di log o inoltrare messaggi a un servizio di monitoraggio remoto. Questa flessibilità è il motivo per cui molti team **creano logger personalizzati** soluzioni che si adattano alle loro esigenze operative.

## Come limitare la dimensione del file di log con File Logger
Di seguito trovi una guida passo‑passo che mostra come **configurare il file logger** affinché il file di log non superi mai la dimensione specificata.

### 1️⃣ Importa i pacchetti necessari
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Configura Index Settings con File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Crea o carica l'indice
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Aggiungi documenti all'indice
```java
index.add(documentsFolder);
```

### 5️⃣ Esegui una query di ricerca
```java
SearchResult result = index.search(query);
```

**Punto chiave:** Il secondo argomento del costruttore `FileLogger` (`4.0`) definisce il **set max log size** in megabyte, rispondendo direttamente al requisito di **limitare la dimensione del file di log**.

## Come usare console logger java
Se preferisci un feedback immediato nel terminale, sostituisci il file logger con un console logger.

### 1️⃣ Importa il Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Configura Index Settings con Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Crea o carica l'indice
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Aggiungi documenti ed esegui una ricerca
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Suggerimento:** Il console logger è ideale durante lo sviluppo perché stampa ogni voce di log istantaneamente, aiutandoti a verificare che l'indicizzazione e la ricerca si comportino come previsto.

## Applicazioni pratiche
1. **Document Management Systems:** Conserva le tracce di audit di ogni documento indicizzato.  
2. **Enterprise Search Engines:** Monitora le prestazioni delle query e i tassi di errore in tempo reale.  
3. **Legal & Compliance Software:** Registra i termini di ricerca per la segnalazione normativa.

## Considerazioni sulle prestazioni
- **Log Size:** Con **set max log size**, eviti un utilizzo eccessivo del disco che potrebbe rallentare l'applicazione.  
- **Asynchronous Logging:** Se hai bisogno di maggiore throughput, considera di avvolgere il logger in una coda asincrona (fuori dallo scopo di questa guida).  
- **Memory Management:** Rilascia gli oggetti `Index` di grandi dimensioni quando non sono più necessari per mantenere ridotto l'ingombro della JVM.

## Problemi comuni e soluzioni
- **Log path not accessible:** Verifica che la directory esista e che l'applicazione abbia i permessi di scrittura.  
- **Logger not firing:** Assicurati di chiamare `settings.setLogger(...)` *prima* di creare l'oggetto `Index`.  
- **Console output missing:** Conferma di eseguire l'applicazione in un terminale che visualizza `System.out`.

## Domande frequenti

**D: Cosa controlla il secondo parametro di `FileLogger`?**  
A: Imposta la dimensione massima del file di log in megabyte, consentendo di **set max log size**.

**D: Posso combinare file logger e console logger?**  
A: Sì, creando un logger personalizzato che inoltra i messaggi a entrambe le destinazioni.

**D: Come aggiungere documenti all'indice dopo la creazione iniziale?**  
A: Chiama `index.add(pathToNewDocs)` in qualsiasi momento; il logger registrerà l'operazione.

**D: `ConsoleLogger` è thread‑safe?**  
A: Scrive direttamente su `System.out`, che è sincronizzato dalla JVM, rendendolo sicuro per la maggior parte dei casi d'uso.

**D: Limitare la dimensione del file di log influirà sulla quantità di informazioni memorizzate?**  
A: Una volta raggiunto il limite di dimensione, le nuove voci possono essere scartate o il file può **roll over log file**, a seconda dell'implementazione del logger.

## Risorse
- [Documentazione](https://docs.groupdocs.com/search/java/)
- [Riferimento API](https://reference.groupdocs.com/search/java/)

---

**Ultimo aggiornamento:** 2026-02-24  
**Testato con:** GroupDocs.Search for Java 25.4  
**Autore:** GroupDocs