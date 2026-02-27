---
date: '2026-02-27'
description: Impara come evidenziare il testo in Java usando GroupDocs.Search per
  Java, coprendo la ricerca di documenti Java, l'indicizzazione di documenti Java
  e l'evidenziazione dei frammenti.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Evidenzia il testo Java con GroupDocs.Search
type: docs
url: /it/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Evidenziare Testo Java con GroupDocs.Search

Nell'attuale ambiente digitale frenetico, la capacità di **evidenziare testo Java** su grandi collezioni di file è una funzionalità indispensabile. Che tu stia costruendo una piattaforma di revisione legale, un motore di ricerca accademica o una console di supporto clienti, individuare istantaneamente i termini ricercati dagli utenti rende l'esperienza molto più efficiente. Questo tutorial ti guida nell'utilizzo di **GroupDocs.Search for Java** per **cercare documenti Java**, **indicizzare documenti Java** e applicare un'evidenziazione avanzata—sia per documenti interi sia per frammenti mirati.

## Risposte Rapide
- **Cosa significa “search and highlight text”?** Si riferisce al trovare i termini di ricerca in un documento e a enfatizzarli visivamente (ad es., con colore di sfondo).  
- **Quale libreria fornisce questa funzionalità?** GroupDocs.Search for Java.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza completa per la produzione.  
- **Posso personalizzare i colori di evidenziazione?** Sì—qualsiasi colore RGB può essere impostato tramite `HighlightOptions`.  
- **Il supporto per l'evidenziazione di frammenti è disponibile?** Assolutamente; è possibile definire termini prima/dopo la corrispondenza per creare snippet concisi.

## Come Evidenziare Testo Java nei Documenti
Evidenziare testo Java comporta tre passaggi fondamentali:

1. **Indicizzare i file sorgente** in modo che possano essere cercati rapidamente.  
2. **Eseguire una query** sull'indice per trovare i documenti corrispondenti.  
3. **Renderizzare i risultati con indicazioni visive** utilizzando l'API di evidenziazione.  

Di seguito esploriamo ogni passaggio in dettaglio, prima per l'output dell'intero documento e poi per gli snippet a livello di frammento.

## Che Cos'è la Ricerca e l'Evidenziazione del Testo?
La ricerca e l'evidenziazione del testo è il processo di scansione di un indice di documenti per una determinata query, recuperando i documenti corrispondenti e quindi segnando ogni occorrenza del termine di ricerca nell'output del documento (HTML, PDF, ecc.). Questo indicatore visivo aiuta gli utenti finali a individuare immediatamente le informazioni rilevanti.

## Perché Usare GroupDocs.Search per Java?
- **Indicizzazione ad alte prestazioni** con compressione configurabile (`index documents java`).  
- **API di evidenziazione avanzata** che funziona su documenti interi e su frammenti personalizzati (`highlight search terms java`).  
- **Supporto multi‑formato** (DOCX, PDF, PPTX, TXT e altri).  
- **Integrazione Maven semplice** e un design pulito incentrato su Java.

## Prerequisiti
- Java Development Kit (JDK) 8 o versioni successive.  
- Maven per la gestione delle dipendenze.  
- Un IDE come IntelliJ IDEA o Eclipse.  
- Familiarità di base con la sintassi Java.

## Configurare GroupDocs.Search per Java

Aggiungi il repository GroupDocs e la dipendenza al tuo `pom.xml`:

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

Puoi anche scaricare l'ultimo JAR direttamente dal sito ufficiale: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione Licenza
Inizia con una prova gratuita o ottieni una licenza temporanea per la valutazione. Per le distribuzioni in produzione, acquista una licenza completa per sbloccare tutte le funzionalità.

## Guida all'Implementazione

L'implementazione è suddivisa in due sezioni pratiche: **evidenziazione in documenti interi** e **evidenziazione in frammenti**. Entrambe le sezioni includono i passaggi essenziali per **come evidenziare documenti Java** usando GroupDocs.Search.

### Configurazione delle Impostazioni dell'Indice
Prima dell'indicizzazione, configura lo storage per utilizzare alta compressione—ciò riduce l'uso del disco mantenendo la velocità di ricerca.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Evidenziazione in Documenti Interi

#### Passo 1: Creare e Popolare l'Indice
Crea una cartella per l'indice e aggiungi tutti i file sorgente che desideri indicizzare.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Passo 2: Eseguire la Ricerca e Applicare l'Evidenziazione
Cerca il termine (ad esempio `ipsum`) e genera un file HTML con le corrispondenze evidenziate.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Opzioni chiave spiegate**  
- **Compression** – l'alta compressione salva spazio di archiviazione.  
- **HighlightColor** – imposta qualsiasi valore RGB per corrispondere alla palette UI.  
- **UseInlineStyles** – `false` genera HTML pulito che può essere stilizzato globalmente con CSS.  

### Evidenziazione in Frammenti

#### Passo 1: Indicizzare e Ricercare (come sopra)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Passo 2: Definire il Contesto del Frammento e Evidenziare
Specifica quanti termini prima e dopo la corrispondenza devono apparire in ogni frammento.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Passo 3: Recuperare e Scrivere i Frammenti Evidenziati
Raccogli i frammenti generati e scrivili in un file HTML.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Applicazioni Pratiche
1. **Revisione di Documenti Legali** – evidenzia istantaneamente statuti, clausole o riferimenti a casi.  
2. **Ricerca Accademica** – individua la terminologia chiave tra decine di PDF e file Word.  
3. **Supporto Clienti** – individua numeri d'ordine o codici di errore all'interno della cronologia dei ticket.

## Considerazioni sulle Prestazioni
- **Dimensione dell'Indice** – alta compressione (`Compression.High`) riduce l'occupazione su disco.  
- **Contesto del Frammento** – valori più grandi di `termsBefore/After` aumentano l'accuratezza ma possono influire sulla velocità.  
- **Gestione della Memoria** – monitora l'heap JVM durante l'indicizzazione di grandi corpora; considera l'indicizzazione incrementale per insiemi molto grandi.

## Problemi Comuni e Soluzioni
- **Errori di Indicizzazione** – verifica i percorsi dei file e assicurati che l'applicazione abbia permessi di lettura/scrittura.  
- **Nessuna Evidenziazione Visualizzata** – conferma che `UseInlineStyles` corrisponda al tuo formato di output (HTML vs. PDF).  
- **Colore Non Applicato** – assicurati che i valori RGB siano compresi tra 0‑255 e che il visualizzatore HTML supporti lo stile.

## Domande Frequenti

**D: Quali sono i vantaggi dell'utilizzare GroupDocs.Search per Java?**  
R: Offre indicizzazione veloce e scalabile, evidenziazione personalizzabile e supporto per molti formati di documento.

**D: Come posso integrare GroupDocs.Search con un'API REST?**  
R: Esporre i metodi di ricerca e evidenziazione tramite controller Spring Boot, restituendo payload HTML o JSON.

**D: La libreria gestisce file protetti da password?**  
R: Sì—fornisci la password quando aggiungi il documento all'indice.

**D: Posso personalizzare il markup di evidenziazione oltre al colore?**  
R: Assolutamente; puoi iniettare classi CSS tramite `HighlightOptions` o modificare l'HTML dopo la generazione.

**D: Quale versione è stata testata per questa guida?**  
R: Il codice è stato validato con GroupDocs.Search 25.4.

**D: Come faccio a impostare le highlight options java per usare una classe CSS invece di stili inline?**  
R: Imposta `options.setUseInlineStyles(false)` e aggiungi una regola CSS per la classe che assegni tramite `options.setCssClass("myHighlight")`.

**D: Esiste un modo per evidenziare termini pdf java direttamente quando la sorgente è un PDF?**  
R: Sì—GroupDocs.Search funziona con input PDF, e l'evidenziatore produrrà HTML che puoi incorporare in un visualizzatore PDF o convertire nuovamente in PDF usando GroupDocs.Conversion.

---

**Ultimo Aggiornamento:** 2026-02-27  
**Testato Con:** GroupDocs.Search 25.4  
**Autore:** GroupDocs