---
date: '2025-12-19'
description: Scopri come aggiungere documenti all'indice e abilitare la ricerca basata
  su chunk in Java usando GroupDocs.Search, migliorando le prestazioni per grandi
  insiemi di documenti.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Aggiungi documenti all'indice con ricerca basata su blocchi in Java
type: docs
url: /it/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Aggiungere documenti all'indice con ricerca basata su chunk in Java

Nel mondo odierno guidato dai dati, la capacità di **aggiungere documenti all'indice** rapidamente e poi eseguire ricerche basate su chunk è essenziale per qualsiasi applicazione che gestisce grandi collezioni di file. Che tu stia lavorando con contratti legali, archivi di supporto clienti o enormi biblioteche di ricerca, questo tutorial ti mostra esattamente come configurare GroupDocs.Search per Java in modo da indicizzare i documenti in modo efficiente e recuperare informazioni rilevanti in piccoli pezzi.

## Cosa Imparerai
- Come creare un indice di ricerca in una cartella specificata.  
- Passaggi per **aggiungere documenti all'indice** da più posizioni.  
- Configurare le opzioni di ricerca per abilitare la ricerca basata su chunk.  
- Eseguire ricerche basate su chunk iniziali e successive.  
- Scenari reali in cui la ricerca basata su chunk brilla.

## Risposte Rapide
- **Qual è il primo passo?** Creare una cartella per l'indice di ricerca.  
- **Come includo molti file?** Usa `index.add()` per ogni cartella di documenti.  
- **Quale opzione abilita la ricerca a chunk?** `options.setChunkSearch(true)`.  
- **Posso continuare a cercare dopo il primo chunk?** Sì, chiama `index.searchNext()` con il token.  
- **È necessaria una licenza?** Una prova gratuita o una licenza temporanea funziona per lo sviluppo; è richiesta una licenza completa per la produzione.

## Prerequisiti
Per seguire questa guida, assicurati di avere:

- **Librerie Richieste**: GroupDocs.Search per Java 25.4 o versioni successive.  
- **Configurazione dell'Ambiente**: Un Java Development Kit (JDK) compatibile installato.  
- **Prerequisiti di Conoscenza**: Programmazione Java di base e familiarità con Maven.

## Configurare GroupDocs.Search per Java
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

In alternativa, scarica l'ultima versione da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della Licenza
Per provare GroupDocs.Search:

- **Prova Gratuita** – testa le funzionalità principali senza impegno.  
- **Licenza Temporanea** – accesso esteso per lo sviluppo.  
- **Acquisto** – licenza completa per l'uso in produzione.

### Inizializzazione e Configurazione di Base
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
Ora che l'indice esiste, il passo logico successivo è **aggiungere documenti all'indice** dalle posizioni in cui i tuoi file sono archiviati.

### 1. Creare un Indice
**Panoramica**: Configura una directory per l'indice di ricerca.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Aggiungere Documenti all'Indice
**Panoramica**: Importa file da diverse cartelle sorgente.

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

### 3. Configurare le Opzioni di Ricerca per la Ricerca a Chunk
Abilita la ricerca basata su chunk modificando l'oggetto delle opzioni.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Eseguire la Ricerca Iniziale Basata su Chunk
Esegui la prima query usando le opzioni abilitate per i chunk.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuare la Ricerca Basata su Chunk
Itera attraverso i chunk rimanenti finché la ricerca non è completa.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Perché usare la ricerca basata su chunk?
La ricerca basata su chunk suddivide enormi collezioni di documenti in pezzi gestibili, riducendo la pressione sulla memoria e accelerando i tempi di risposta. È particolarmente vantaggiosa quando:

1. **I team legali** devono individuare clausole specifiche tra migliaia di contratti.  
2. **I portali di supporto clienti** devono mostrare istantaneamente articoli pertinenti della knowledge‑base.  
3. **I ricercatori** setacciano grandi set di dati senza caricare interi file in memoria.

## Considerazioni sulle Prestazioni
- **Gestione della Memoria** – Assegna spazio heap sufficiente (`-Xmx`) per indici di grandi dimensioni.  
- **Monitoraggio delle Risorse** – Tieni d'occhio l'utilizzo della CPU durante le operazioni di indicizzazione e ricerca.  
- **Manutenzione dell'Indice** – Ricostruisci o pulisci periodicamente l'indice per eliminare dati obsoleti.

## Problemi Comuni & Risoluzione dei Problemi
| Problema | Perché Accade | Soluzione |
|----------|----------------|-----------|
| `OutOfMemoryError` durante l'indicizzazione | Heap troppo piccolo | Aumenta l'heap JVM (`-Xmx2g` o superiore) |
| Nessun risultato restituito | Token del chunk non elaborato | Assicurati che il ciclo `while` continui fino a quando `getNextChunkSearchToken()` è `null` |
| Prestazioni di ricerca lente | Indice non ottimizzato | Esegui `index.optimize()` dopo aggiunte massive |

## Domande Frequenti

**D: Cos'è la ricerca basata su chunk?**  
R: La ricerca basata su chunk divide il dataset in pezzi più piccoli, consentendo query efficienti su grandi volumi di dati senza caricare interi documenti in memoria.

**D: Come aggiorno il mio indice con nuovi file?**  
R: Basta chiamare `index.add()` con il percorso dei nuovi documenti; l'indice li incorporerà automaticamente.

**D: GroupDocs.Search può gestire diversi formati di file?**  
R: Sì, supporta PDF, DOCX, XLSX, PPTX e molti altri formati comuni.

**D: Quali sono i tipici colli di bottiglia delle prestazioni?**  
R: Vincoli di memoria e indici non ottimizzati sono i più comuni; assegna heap sufficiente e ottimizza regolarmente l'indice.

**D: Dove posso trovare documentazione più dettagliata?**  
R: Visita la documentazione ufficiale [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) per guide approfondite e riferimenti API.

## Risorse
- **Documentazione**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Riferimento API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Supporto Gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licenza Temporanea**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ultimo Aggiornamento:** 2025-12-19  
**Testato Con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs  

---