---
date: '2026-02-21'
description: Scopri come aggiungere documenti all'indice e aumentare le prestazioni
  di ricerca con la ricerca basata su chunk in Java usando GroupDocs.Search, ottimizzando
  la memoria dell'indice di ricerca Java per grandi insiemi di documenti.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Aggiungi documenti all'indice con ricerca basata su chunk in Java
type: docs
url: /it/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

Now produce final translated content.# Aggiungere documenti all'indice con ricerca basata su chunk in Java

Nelle applicazioni moderne che necessitano di **add documents to index** rapidamente e poi eseguire query veloci basate su chunk, vorrai una soluzione che scala senza consumare troppa memoria. Questo tutorial ti guida nella configurazione di GroupDocs.Search per Java, nell'aggiunta di più cartelle di documenti e nella configurazione del motore per **increase search performance** mantenendo sotto controllo l'utilizzo della **java search index memory**. Che tu stia indicizzando contratti legali, ticket di supporto o articoli di ricerca, i passaggi seguenti ti forniranno un'implementazione pronta per la produzione.

## Risposte rapide
- **Qual è il primo passo?** Crea una cartella per l'indice di ricerca.  
- **Come includere molti file?** Usa `index.add()` per ogni cartella di documenti.  
- **Quale opzione abilita la ricerca a chunk?** `options.setChunkSearch(true)`.  
- **Posso continuare la ricerca dopo il primo chunk?** Sì, chiama `index.searchNext()` con il token.  
- **Ho bisogno di una licenza?** Una prova gratuita o una licenza temporanea funziona per lo sviluppo; è necessaria una licenza completa per la produzione.  

## Cosa imparerai
- Come creare un indice di ricerca in una cartella specificata.  
- Passaggi per **add documents to index** da più posizioni.  
- Configurare le opzioni di ricerca per abilitare la ricerca basata su chunk.  
- Eseguire ricerche iniziali e successive basate su chunk.  
- Scenari reali in cui la ricerca di documenti basata su chunk si distingue.  

## Prerequisiti
Per seguire questa guida, assicurati di avere:

- **Librerie richieste**: GroupDocs.Search for Java 25.4 or later.  
- **Configurazione dell'ambiente**: Un Java Development Kit (JDK) compatibile installato.  
- **Prerequisiti di conoscenza**: Programmazione Java di base e familiarità con Maven.  

## Configurazione di GroupDocs.Search per Java
Per iniziare, integra GroupDocs.Search nel tuo progetto usando Maven:

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

Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
Per provare GroupDocs.Search:

- **Free Trial** – testa le funzionalità principali senza impegno.  
- **Temporary License** – accesso esteso per lo sviluppo.  
- **Purchase** – licenza completa per l'uso in produzione.  

### Inizializzazione e configurazione di base
Crea un indice nella cartella dove desideri che i dati ricercabili risiedano:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Come aggiungere documenti all'indice
Ora che l'indice esiste, il passo logico successivo è **add documents to index** dalle posizioni in cui sono archiviati i tuoi file.

### 1. Creazione di un indice
**Panoramica**: Configura una directory per l'indice di ricerca.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Aggiunta di documenti all'indice
**Panoramica**: Importa file da diverse cartelle di origine.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Configurazione delle opzioni di ricerca per la ricerca a chunk
Abilita la ricerca basata su chunk modificando l'oggetto delle opzioni.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Esecuzione della ricerca iniziale basata su chunk
Esegui la prima query usando le opzioni con chunk abilitato.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuare la ricerca basata su chunk
Itera attraverso i chunk rimanenti fino al completamento della ricerca.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Perché usare la ricerca basata su chunk?
La ricerca basata su chunk suddivide collezioni di documenti massivi in pezzi gestibili, riducendo la pressione sulla memoria e accelerando i tempi di risposta. È particolarmente vantaggiosa quando:

1. **Legal teams** hanno bisogno di individuare clausole specifiche tra migliaia di contratti.  
2. **Customer support portals** devono mostrare articoli pertinenti della knowledge‑base istantaneamente.  
3. **Researchers** setacciano dataset estesi senza caricare interi file in memoria.  

## Come questo approccio **increase search performance**
Cercando chunk più piccoli anziché file interi, il motore può:

- Saltare sezioni irrilevanti in anticipo, riducendo i cicli CPU.  
- Tenere in memoria solo il chunk attivo, il che riduce direttamente il consumo di **java search index memory**.  
- Parallelizzare l'elaborazione dei chunk su macchine multi‑core per risultati più rapidi.  

## Gestione di **java search index memory**
Sebbene la ricerca basata su chunk riduca già l'impronta di memoria, puoi ulteriormente ottimizzare la JVM:

- Assegna un heap sufficiente (`-Xmx2g` o superiore) in base alle dimensioni dell'indice.  
- Usa `index.optimize()` dopo aggiunte massive per comprimere la struttura dell'indice.  
- Monitora le pause del GC con strumenti come VisualVM per evitare picchi di latenza.  

## Considerazioni sulle prestazioni
- **Memory Management** – Assegna spazio heap sufficiente (`-Xmx`) per indici di grandi dimensioni.  
- **Resource Monitoring** – Tieni d'occhio l'utilizzo della CPU durante le operazioni di indicizzazione e ricerca.  
- **Index Maintenance** – Ricostruisci o pulisci periodicamente l'indice per eliminare dati obsoleti.  

## Problemi comuni e risoluzione
| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| `OutOfMemoryError` durante l'indicizzazione | Dimensione heap troppo piccola | Aumentare l'heap JVM (`-Xmx2g` o superiore) |
| Nessun risultato restituito | Token di chunk non elaborato | Assicurarsi che il ciclo `while` continui fino a quando `getNextChunkSearchToken()` è `null` |
| Prestazioni di ricerca lente | Indice non ottimizzato | Eseguire `index.optimize()` dopo aggiunte massive |

## Domande frequenti

**Q: Cos'è la ricerca basata su chunk?**  
A: La ricerca basata su chunk divide il dataset in pezzi più piccoli, consentendo query efficienti su grandi volumi di dati senza caricare interi documenti in memoria.

**Q: Come aggiorno il mio indice con nuovi file?**  
A: Basta chiamare `index.add()` con il percorso dei nuovi documenti; l'indice li incorporerà automaticamente.

**Q: GroupDocs.Search può gestire diversi formati di file?**  
A: Sì, supporta PDF, DOCX, XLSX, PPTX e molti altri formati comuni.

**Q: Quali sono i tipici colli di bottiglia delle prestazioni?**  
A: Le limitazioni di memoria e gli indici non ottimizzati sono i più comuni; assegna un heap sufficiente e ottimizza regolarmente l'indice.

**Q: Dove posso trovare una documentazione più dettagliata?**  
A: Visita la documentazione ufficiale [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) per guide approfondite e riferimenti API.

**Q: La ricerca basata su chunk funziona con PDF crittografati?**  
A: Sì, purché fornisca la password tramite il sovraccarico API appropriato.

**Q: Come posso monitorare l'avanzamento dell'indicizzazione?**  
A: Usa il sovraccarico `Index.add()` che restituisce un oggetto `Progress` o collega i callback di logging.

## Risorse
- **Documentazione**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Riferimento API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Supporto gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licenza temporanea**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ultimo aggiornamento:** 2026-02-21  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs