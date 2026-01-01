---
date: '2025-12-29'
description: Scopri come ottimizzare le prestazioni di ricerca utilizzando le funzionalità
  avanzate di indicizzazione di GroupDocs.Search per Java, inclusi annullamento, operazioni
  asincrone, multithreading e personalizzazione dei metadati.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: Ottimizza le prestazioni di ricerca con tecniche di indicizzazione avanzate
  in GroupDocs.Search per Java
type: docs
url: /it/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Ottimizzare le prestazioni di ricerca con tecniche di indicizzazione avanzate in GroupDocs.Search per Java

Nell'attuale ambiente digitale frenetico, **ottimizzare le prestazioni di ricerca** è fondamentale per fornire risultati istantanei agli utenti. Che tu stia costruendo un motore di ricerca personalizzato o migliorando un sistema di gestione documenti esistente, la giusta strategia di indicizzazione può ridurre drasticamente latenza e consumo di risorse. In questo tutorial esamineremo le funzionalità più potenti di GroupDocs.Search per Java — cancellazione, indicizzazione asincrona, multithreading e personalizzazione dei metadati — così potrai **add documents index** più rapidamente ed efficientemente.

**Cosa imparerai**

- Come annullare un'operazione di indicizzazione dopo un tempo specificato  
- Eseguire operazioni di indicizzazione asincrone e gestire i cambiamenti di stato  
- Configurare il multithreading per un'indicizzazione più veloce  
- Personalizzare le opzioni di indicizzazione dei metadati  

Assicuriamoci di avere tutto il necessario prima di immergerci nel codice.

## Prerequisiti

- **GroupDocs.Search Library** – versione 25.4 o successiva.  
- **Java Development Environment** – JDK 8 o superiore è consigliato.  
- Familiarità di base con Java e il concetto di indicizzazione.  

### Configurazione di GroupDocs.Search per Java

#### Installazione con Maven

Add the repository and dependency to your `pom.xml` file:

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

In alternativa, scarica l'ultimo JAR da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Acquisizione della licenza** – Inizia con una prova gratuita o richiedi una licenza temporanea per sbloccare l'intero set di funzionalità.

### Inizializzazione e configurazione di base

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Risposte rapide

- **Cosa fa la cancellazione?** Interrompe l'indicizzazione dopo un tempo impostato per liberare risorse.  
- **Posso indicizzare i documenti in modo asincrono?** Sì – imposta `options.setAsync(true)`.  
- **Quanti thread posso usare?** Qualsiasi intero positivo; valori tipici sono 2‑4 per la maggior parte dei server.  
- **L'indicizzazione dei metadati è opzionale?** Assolutamente – puoi abilitarla o regolarla per campo.  
- **È necessaria una licenza per queste funzionalità?** Una prova funziona per i test; è necessaria una licenza completa per la produzione.  

## Cosa significa “Ottimizzare le prestazioni di ricerca” in questo contesto?

Ottimizzare le prestazioni di ricerca significa configurare il processo di indicizzazione in modo che consumi la giusta quantità di CPU, memoria e tempo, fornendo al contempo i risultati più pertinenti istantaneamente. Controllando la cancellazione, l'esecuzione asincrona, il threading e la gestione dei metadati, influenzi direttamente la rapidità con cui il motore può **add documents index** e rispondere alle query.

## Perché utilizzare le funzionalità avanzate di indicizzazione?

- **Latenza ridotta** – L'indicizzazione asincrona e multithread mantiene la tua applicazione reattiva.  
- **Migliore gestione delle risorse** – La cancellazione previene processi incontrollati.  
- **Rilevanza di ricerca personalizzata** – Le opzioni dei metadati ti permettono di evidenziare le informazioni più importanti.  

## Guida all'implementazione

### Proprietà di cancellazione

**Panoramica** – Annulla l'indicizzazione dopo una durata specificata per evitare un consumo eccessivo di risorse.

#### Passo 1: Configurare l'ambiente

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: Creare le opzioni di indicizzazione con cancellazione

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Punti chiave**

- `setCancellation()` attiva la funzionalità.  
- `cancelAfter(int milliseconds)` definisce il timeout (3 secondi in questo esempio).  

### Proprietà asincrona

**Panoramica** – Esegui l'indicizzazione su un thread in background e ascolta i cambiamenti di stato.

#### Passo 1: Configurare l'ambiente

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: Sottoscrivere l'evento StatusChanged

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Passo 3: Configurare le opzioni asincrone

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Proprietà dei thread

**Panoramica** – Accelerare l'indicizzazione sfruttando più core CPU.

#### Passo 1: Configurare l'ambiente

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: Configurare il multithreading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Proprietà delle opzioni di indicizzazione dei metadati

**Panoramica** – Regola finemente quali metadati del documento vengono indicizzati e come vengono memorizzati.

#### Passo 1: Configurare l'ambiente

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Passo 2: Configurare le opzioni dei metadati

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Applicazioni pratiche

1. **Sistemi di gestione documenti** – Usa l'indicizzazione asincrona per mantenere l'interfaccia utente reattiva mentre grandi lotti vengono elaborati in background.  
2. **Motori di ricerca di contenuti** – Applica la cancellazione per impedire che lavori di lunga durata monopolizzino le risorse del server durante i picchi di traffico.  
3. **Pipeline di ingestione su larga scala** – Sfrutta il multithreading per **add documents index** su larga scala, riducendo drasticamente il tempo di elaborazione.  

## Considerazioni sulle prestazioni

- **Gestione dei thread** – Monitora l'uso della CPU; troppi thread possono causare overhead di cambio contesto.  
- **Impronta di memoria** – I limiti dei metadati (ad es., `setMaxBytesToIndexField`) aiutano a mantenere prevedibile l'uso della memoria.  
- **Garbage Collection** – Usa i flag JVM appropriati (`-Xmx`, `-XX:+UseG1GC`) durante l'indicizzazione di corpora massivi.  

## Problemi comuni e soluzioni

| Sintomo | Probabile causa | Risoluzione |
|---------|-----------------|-------------|
| L'indicizzazione non termina mai | Cancellazione impostata troppo bassa | Aumenta il valore di `cancelAfter` o rimuovi la cancellazione per lavori lunghi |
| Nessun aggiornamento di stato in modalità asincrona | Gestore eventi non collegato correttamente | Assicurati che `index.getEvents().StatusChanged.add(...)` sia chiamato prima di `index.add` |
| Errori di out‑of‑memory | Troppi thread o limiti di metadati troppo alti | Riduci `options.setThreads` e abbassa i limiti dei campi dei metadati |
| Metadati mancanti nei risultati | Indicizzazione dei metadati disabilitata | Verifica che `options.getMetadataIndexingOptions()` sia configurato e non impostato per ignorare i campi |

## Domande frequenti

**D: Come posso ottenere una licenza temporanea per GroupDocs.Search?**  
R: Visita la [pagina della licenza temporanea di GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**D: Posso annullare un'operazione di indicizzazione a metà?**  
R: Sì – usa la proprietà di cancellazione con `cancelAfter()` o chiama `Cancellation.cancel()` programmaticamente.

**D: Quali sono alcuni casi d'uso per l'indicizzazione asincrona?**  
R: Recupero di documenti in tempo reale, elaborazione batch in background e applicazioni con interfaccia utente reattiva beneficiano dell'indicizzazione asincrona.

**D: È sicuro aumentare il numero di thread su un server condiviso?**  
R: Incrementa gradualmente e monitora il carico CPU; in ambienti molto condivisi, mantieni il numero di thread moderato (2‑4).

**D: Come influisce l'indicizzazione dei metadati sulla rilevanza della ricerca?**  
R: I metadati indicizzati correttamente (autore, data di creazione, tag) possono avere un peso maggiore nelle query, migliorando l'accuratezza dei risultati.

## Conclusione

Adottando queste funzionalità avanzate di GroupDocs.Search per Java, **ottimizzerai le prestazioni di ricerca** in una varietà di scenari — dall'ingestione rapida di documenti al controllo fine dei metadati. Sperimenta con diverse configurazioni, monitora l'uso delle risorse e adatta le impostazioni al tuo carico di lavoro specifico per ottenere i migliori risultati.

---

**Ultimo aggiornamento:** 2025-12-29  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs