---
date: '2026-02-08'
description: Scopri come evidenziare i risultati di ricerca in Java e come indicizzare
  i documenti Java usando GroupDocs.Search per Java con indicizzazione sincrona e
  asincrona.
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: Evidenzia i risultati di ricerca Java – Indicizzazione sincrona e asincrona
type: docs
url: /it/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Evidenzia i risultati di ricerca Java – Indicizzazione sincrona e asincrona

Migliora le tue applicazioni Java **evidenziando i risultati di ricerca Java** con la potente libreria GroupDocs.Search. Che tu stia gestendo pochi file o un repository massiccio, padroneggiare sia l'indicizzazione sincrona che quella asincrona ti permette di fornire risultati rapidi e precisi senza bloccare i thread della tua applicazione.

## Risposte rapide
- **Cosa significa “highlight search results Java”?** Si riferisce al rendering dei termini corrispondenti nei risultati di ricerca con indicazioni visive (ad es., tag HTML `<mark>`) in modo che gli utenti possano vedere dove la query appare in ciascun documento.  
- **Quando dovrei usare l'indicizzazione sincrona?** Per set di dati piccoli o medi dove è necessaria la disponibilità immediata dei documenti appena aggiunti.  
- **Quando è preferibile l'indicizzazione asincrona?** Quando si elaborano grandi collezioni di documenti o si esegue su un thread UI dove è necessario mantenere l'applicazione reattiva.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per lo sviluppo; una licenza completa sblocca funzionalità avanzate e rimuove i limiti di utilizzo.  
- **Quale versione di Java è supportata?** Java 8 o successiva.

## Cos'è “highlight search results Java”?
Evidenziare i risultati di ricerca in Java significa prendere le corrispondenze grezze restituite da GroupDocs.Search e avvolgere i termini corrispondenti in HTML (o un altro markup) in modo che risaltino quando visualizzati in un'interfaccia utente o in una pagina web. Questo migliora l'esperienza dell'utente mostrando istantaneamente il contesto di ogni risultato.

## Perché usare GroupDocs.Search per Java?
GroupDocs.Search fornisce un motore ad alte prestazioni, indipendente dalla lingua, che supporta:
- Indicizzazione e ricerca in tempo reale
- Elaborazione asincrona per carichi di lavoro elevati
- Evidenziazione dei risultati integrata
- Supporto multilingua e analizzatori personalizzati  

Queste capacità lo rendono ideale per sistemi di gestione dei contenuti, cataloghi e‑commerce e repository di documenti aziendali.

## Prerequisiti
Prima di iniziare, assicurati di avere:

- **Java Development Kit** (JDK 8 o più recente) installato.
- Un IDE come **IntelliJ IDEA** o **Eclipse**.
- Una cartella contenente i documenti che desideri indicizzare.
- Maven per la gestione delle dipendenze (oppure puoi scaricare manualmente il JAR).

### Librerie e dipendenze richieste
Aggiungi GroupDocs.Search al tuo progetto Maven:

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

Per download diretti, ottieni l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Configurazione dell'ambiente
- Verifica che il tuo **JAVA_HOME** punti a un JDK compatibile.
- Crea un progetto nel tuo IDE e aggiungi la configurazione Maven sopra.
- Prepara una directory (ad es., `documents/`) con file di testo, PDF o Word di esempio.

## Come configurare GroupDocs.Search per Java
1. **Installa la libreria** – Usa lo snippet Maven sopra o scarica il JAR da [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Ottieni una licenza** – Inizia con una licenza di prova, poi effettua l'upgrade quando passi alla produzione.  
3. **Inizializza l'indice** – Il frammento seguente mostra come creare (o aprire) una cartella indice:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Come evidenziare i risultati di ricerca Java – Indicizzazione sincrona
L'indicizzazione sincrona elabora i documenti immediatamente, rendendo i file appena aggiunti ricercabili subito.

### Passo 1: Crea l'indice e aggiungi la gestione degli errori
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Passo 2: Aggiungi i documenti ed esegui una ricerca
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Passo 3: Elabora i risultati e **evidenzia i risultati di ricerca Java**
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

`DocumentHighlighter` avvolge automaticamente i termini corrispondenti con i tag `<mark>` (o qualsiasi formato tu configuri), fornendoti **risultati di ricerca evidenziati** pronti per la visualizzazione.

## Come evidenziare i risultati di ricerca Java – Indicizzazione asincrona
Quando si gestiscono migliaia di file, bloccare il thread principale è indesiderabile. L'indicizzazione asincrona consente al motore di lavorare in background.

### Passo 1: Configura l'indice con i listener di eventi
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Passo 2: Abilita la modalità asincrona e avvia l'indicizzazione
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

Mentre l'indice viene costruito, la tua applicazione può continuare a gestire altre richieste. Una volta che l'evento `StatusChanged` segnala `Ready`, puoi eseguire ricerche in sicurezza e ottenere **risultati di ricerca evidenziati Java**.

## Come **indicizzare documenti java** – Consigli pratici
- **Dimensione batch**: Per collezioni enormi, suddividi la cartella in batch più piccoli per evitare picchi di memoria.  
- **Filtri file**: Usa `IndexingOptions.setFileExtensions` per includere solo i formati necessari (ad es., `.pdf`, `.docx`).  
- **Re‑indicizzazione**: Quando i documenti cambiano, chiama `index.update(documentPath)` invece di ricostruire l'intero indice.

## Considerazioni sulle prestazioni
- **Memoria**: Tieni sotto controllo l'uso dell'heap; aumenta `-Xmx` se elabori molti file di grandi dimensioni.  
- **CPU**: L'indicizzazione asincrona distribuisce il carico di lavoro, ma consuma comunque CPU—monitorala con JVisualVM.  
- **Evidenziazione dei risultati**: L'evidenziazione aggiunge un piccolo overhead di elaborazione; memorizza nella cache l'HTML generato se devi visualizzare i risultati più volte.

## Domande frequenti

**Q: Posso combinare indicizzazione sincrona e asincrona nella stessa applicazione?**  
A: Sì. Usa l'indicizzazione sincrona per set piccoli e frequentemente aggiornati e l'indicizzazione asincrona per importazioni massive o lavori in background.

**Q: Come personalizzo lo stile di evidenziazione?**  
A: Fornisci un'implementazione personalizzata di `DocumentHighlighter` che scriva i tag HTML, CSS o XML desiderati attorno ai termini corrispondenti.

**Q: Quali tipi di file supporta GroupDocs.Search nativamente?**  
A: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML e molti altri tramite i suoi parser integrati.

**Q: È possibile cercare in più lingue simultaneamente?**  
A: Assolutamente. GroupDocs.Search include analizzatori multilingua; basta configurare l'`Analyzer` appropriato quando crei l'indice.

**Q: Come proteggere la cartella indice?**  
A: Conserva l'indice in una directory protetta, imposta i permessi corretti del file system e considera la crittografia dell'indice con le funzionalità di sicurezza della libreria.

---

**Ultimo aggiornamento:** 2026-02-08  
**Testato con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs