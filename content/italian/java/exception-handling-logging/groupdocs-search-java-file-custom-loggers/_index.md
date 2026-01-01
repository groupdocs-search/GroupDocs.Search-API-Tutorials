---
date: '2025-12-24'
description: Scopri come limitare la dimensione del file di log e utilizzare il logger
  console Java con GroupDocs.Search per Java. Questa guida copre le configurazioni
  di logging, i suggerimenti per la risoluzione dei problemi e l'ottimizzazione delle
  prestazioni.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Limita la dimensione del file di log con i logger Java di GroupDocs.Search
type: docs
url: /it/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Limita la dimensione del file di log con i logger di GroupDocs.Search per Java

Il logging efficiente è essenziale quando si gestiscono grandi collezioni di documenti, soprattutto quando è necessario **limitare la dimensione del file di log** per mantenere sotto controllo lo spazio di archiviazione. **GroupDocs.Search for Java** offre soluzioni robuste per la gestione dei log grazie alle sue potenti capacità di ricerca. Questo tutorial ti guida nell'implementazione di logger su file e personalizzati usando GroupDocs.Search, migliorando la capacità della tua applicazione di tracciare eventi e debug.

## Risposte rapide
- **Cosa significa “limitare la dimensione del file di log”?** Limita la dimensione massima di un file di log, impedendo una crescita incontrollata sul disco.  
- **Quale logger consente di limitare la dimensione del file di log?** Il `FileLogger` integrato accetta un parametro di dimensione massima.  
- **Come utilizzo il console logger in Java?** Istanzia `ConsoleLogger` e impostalo su `IndexSettings`.  
- **È necessaria una licenza per GroupDocs.Search?** Una versione di prova è sufficiente per la valutazione; è richiesta una licenza commerciale per la produzione.  
- **Qual è il primo passo?** Aggiungi la dipendenza di GroupDocs.Search al tuo progetto Maven.

## Cos'è il limite della dimensione del file di log?
Limitare la dimensione del file di log significa configurare il logger in modo che, una volta raggiunta una soglia predefinita (ad esempio 4 MB), il file smetta di crescere o venga ruotato. Questo mantiene prevedibile l'impronta di archiviazione della tua applicazione ed evita il degrado delle prestazioni.

## Perché utilizzare logger su file e personalizzati con GroupDocs.Search?
- **Auditabilità:** Mantieni un registro permanente degli eventi di indicizzazione e ricerca.  
- **Debugging:** Individua rapidamente i problemi esaminando log concisi.  
- **Flessibilità:** Scegli tra log su file persistenti e output immediato sulla console (`use console logger java`).  

## Prerequisiti
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 o versioni successive, IDE (IntelliJ IDEA, Eclipse, ecc.).  
- Conoscenze di base di Java e Maven.  

## Configurazione di GroupDocs.Search per Java

Aggiungi la libreria al tuo progetto usando uno dei metodi seguenti.

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

### Ottenimento della licenza
Ottieni una versione di prova o acquista una licenza tramite la [pagina di licenza](https://purchase.groupdocs.com/temporary-license/).

## Come limitare la dimensione del file di log con File Logger
Di seguito trovi una guida passo‑passo che mostra come configurare `FileLogger` affinché il file di log non superi mai la dimensione specificata.

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

**Punto chiave:** Il secondo argomento del costruttore `FileLogger` (`4.0`) definisce la dimensione massima del file di log in megabyte, rispondendo direttamente al requisito di **limitare la dimensione del file di log**.

## Come utilizzare console logger in Java
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
1. **Sistemi di gestione documentale:** Mantieni tracce di audit di ogni documento indicizzato.  
2. **Motori di ricerca aziendali:** Monitora le prestazioni delle query e i tassi di errore in tempo reale.  
3. **Software legale e di conformità:** Registra i termini di ricerca per la segnalazione normativa.

## Considerazioni sulle prestazioni
- **Dimensione del log:** Limitando la dimensione del file di log, eviti un utilizzo eccessivo del disco che potrebbe rallentare la tua applicazione.  
- **Logging asincrono:** Se hai bisogno di maggiore throughput, considera di avvolgere il logger in una coda asincrona (fuori dal campo di questa guida).  
- **Gestione della memoria:** Rilascia gli oggetti `Index` di grandi dimensioni quando non sono più necessari per mantenere ridotta l'impronta della JVM.

## Problemi comuni e soluzioni
- **Percorso del log non accessibile:** Verifica che la directory esista e che l'applicazione abbia i permessi di scrittura.  
- **Logger non attivo:** Assicurati di chiamare `settings.setLogger(...)` *prima* di creare l'oggetto `Index`.  
- **Output della console mancante:** Conferma di eseguire l'applicazione in un terminale che visualizza `System.out`.

## Domande frequenti

**D: Cosa controlla il secondo parametro di `FileLogger`?**  
R: Imposta la dimensione massima del file di log in megabyte, consentendoti di limitare la dimensione del file di log.

**D: Posso combinare file logger e console logger?**  
R: Sì, creando un logger personalizzato che inoltra i messaggi a entrambe le destinazioni.

**D: Come aggiungo documenti all'indice dopo la creazione iniziale?**  
R: Chiama `index.add(pathToNewDocs)` in qualsiasi momento il logger registrerà l'operazione.

**D: `ConsoleLogger` è thread‑safe?**  
R: Scrive direttamente su `System.out`, che è sincronizzato dalla JVM, rendendolo sicuro per la maggior parte dei casi d'uso.

**D: Limitare la dimensione del file di log influirà sulla quantità di informazioni memorizzate?**  
R: Una volta raggiunto il limite di dimensione, le nuove voci possono essere scartate o il file può essere ruotato, a seconda dell'implementazione del logger.

## Risorse
- [Documentazione](https://docs.groupdocs.com/search/java/)
- [Riferimento API](https://reference.groupdocs.com/search/java/)

---

**Last Updated:** 2025-12-24  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs