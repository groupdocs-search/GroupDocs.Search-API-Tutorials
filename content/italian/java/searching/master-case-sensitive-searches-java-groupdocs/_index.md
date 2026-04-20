---
date: '2026-02-06'
description: Scopri come aggiungere documenti all'indice e abilitare la ricerca sensibile
  al maiuscolo/minuscolo in Java con GroupDocs.Search, migliorando l'accuratezza della
  tua applicazione.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Aggiungi documenti all''indice: ricerca Java sensibile a maiuscole/minuscole
  con GroupDocs'
type: docs
url: /it/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Aggiungere documenti all'indice: Padroneggiare le ricerche Case‑Sensitive in Java con GroupDocs

Recuperare la giusta informazione da una collezione enorme di documenti è un requisito fondamentale per le applicazioni moderne. In questa guida, imparerai **come aggiungere documenti all'indice** e eseguire **ricerche case‑sensitive** usando GroupDocs.Search per Java. Che tu stia costruendo un repository di documenti legali, un catalogo e‑commerce o un sistema di gestione dei contenuti, risultati di ricerca precisi mantengono gli utenti soddisfatti e i tuoi dati affidabili.

## Risposte rapide
- **Qual è il passo principale per iniziare a cercare?** Aggiungi documenti a un indice con `index.add(...)`.
- **Come abilitare la ricerca case sensitive?** Imposta `options.setUseCaseSensitiveSearch(true)`.
- **Posso cercare in più directory?** Sì – chiama `index.add()` per ogni cartella che desideri includere.
- **Quale metodo consente di cercare con oggetti?** Usa `SearchQuery.createWordQuery(...)`.
- **È necessaria una licenza per i test?** È disponibile una licenza temporanea per scopi di prova.

## Cosa significa “add documents to index”?
Aggiungere documenti a un indice significa fornire i tuoi file sorgente (PDF, documenti Word, testo semplice, ecc.) a GroupDocs.Search affinché possa costruire una struttura dati ricercabile. Una volta indicizzati, il motore può eseguire query rapide, incluse quelle case‑sensitive.

## Perché abilitare la ricerca case‑sensitive in Java?
- **Corrispondenza esatta del termine** – differenzia “Apple” (l'azienda) da “apple” (il frutto).  
- **Conformità normativa** – alcune industrie richiedono una corrispondenza esatta delle frasi.  
- **Rilevanza migliorata** – gli utenti spesso si aspettano risultati case‑specifici in contesti tecnici o legali.

## Prerequisiti
- JDK (Java 17 o successivo consigliato)  
- Maven per la gestione delle dipendenze  
- Un IDE come IntelliJ IDEA o Eclipse  
- Familiarità di base con la programmazione Java  

## Configurare GroupDocs.Search per Java
Per prima cosa, aggiungi il repository GroupDocs e la dipendenza al tuo `pom.xml`:

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

In alternativa, puoi scaricare l'ultima versione direttamente da [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenza
Per iniziare con una versione di prova, visita GroupDocs per ottenere una licenza temporanea. Questo ti permetterà di testare tutte le funzionalità senza alcuna limitazione.

## Come aggiungere documenti all'indice – Ricerca con query di testo

### Passo 1: Creare un indice e aggiungere i tuoi documenti
Crea una cartella dove saranno memorizzati i file dell'indice, quindi aggiungi la directory sorgente che contiene i documenti che desideri cercare.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Consiglio professionale:** Puoi chiamare `index.add()` più volte per **cercare in più directory** in un unico indice.

### Passo 2: Abilitare la ricerca case‑sensitive
Configura le opzioni di ricerca per rispettare la distinzione tra maiuscole e minuscole.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Passo 3: Eseguire una query di testo case‑sensitive
Esegui una query che differenzia “Advantages” da “advantages”.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Il ciclo stampa il percorso completo di ogni documento che contiene il termine con corrispondenza esatta di maiuscole/minuscole.

## Come aggiungere documenti all'indice – Ricerca con query di oggetto

Le query di oggetto ti offrono maggiore flessibilità, soprattutto quando devi combinare più criteri.

### Passo 1: Inizializzare un secondo indice (opzionale)
Se preferisci tenere separate le ricerche basate su oggetti, crea un'altra cartella per l'indice.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Passo 2: Riutilizzare l'opzione case‑sensitive
La stessa istanza di `SearchOptions` funziona per le query di oggetto.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Passo 3: Costruire ed eseguire una query di oggetto
Crea un oggetto query di parola e passalo al motore di ricerca.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Usare `createWordQuery` ti consente di combinarlo in seguito con query di frase, wildcard o Boolean per scenari più complessi.

## Applicazioni pratiche
- **Gestione documenti legali:** Recupera normative specifiche del caso dove la capitalizzazione è importante.  
- **Piattaforme e‑commerce:** Distinguere SKU di prodotto come “PRO‑X” vs. “pro‑x”.  
- **Sistemi di gestione dei contenuti (CMS):** Garantire che gli autori trovino intestazioni o tag esatti.

## Considerazioni sulle prestazioni
- **Mantenere l'indice aggiornato** – re‑indicizzare quando vengono aggiunti nuovi file o quelli esistenti cambiano.  
- **Monitorare l'uso della memoria** – grandi corpora beneficiano dell'indicizzazione incrementale e di una corretta dimensione dell'heap JVM.  
- **Sfruttare il garbage collector di Java** – rilascia gli oggetti `Index` quando non sono più necessari.

## Problemi comuni e soluzioni
| Problema | Soluzione |
|----------|-----------|
| `useCaseSensitiveSearch` appears ignored | Verifica di utilizzare l'ultima versione di GroupDocs.Search e che l'indice sia stato ricostruito dopo aver modificato l'opzione. |
| No results returned for a known term | Assicurati che la capitalizzazione del termine corrisponda esattamente e che il documento sia stato aggiunto correttamente all'indice. |
| Searching many folders slows down | Aggiungi ogni cartella singolarmente con `index.add()` e considera di suddividere l'indice in shard per dataset molto grandi. |

## Domande frequenti

**D:** Come gestisco grandi dataset con GroupDocs.Search?  
**R:** Utilizza il partizionamento dell'indice, ottimizza le impostazioni di memoria della JVM e compatta periodicamente l'indice per mantenere le prestazioni ottimali.

**D:** Posso cercare simultaneamente in più directory?  
**R:** Sì – chiama `index.add()` per ogni directory che desideri includere, quindi esegui una singola query sull'indice combinato.

**D:** Quali sono gli errori comuni nella configurazione delle ricerche case‑sensitive?  
**R:** Dimenticare di ricostruire l'indice dopo aver abilitato `useCaseSensitiveSearch`, o usare la capitalizzazione errata nella stringa di query.

**D:** Come posso risolvere gli errori di ricerca?  
**R:** Controlla i file di log generati da GroupDocs.Search per le tracce di stack e conferma che tutte le dipendenze Maven siano risolte correttamente.

**D:** GroupDocs.Search è adatto per applicazioni in tempo reale?  
**R:** Con strategie di indicizzazione adeguate (aggiornamenti incrementali e caching in‑memory), può fornire risultati di ricerca quasi in tempo reale.

## Risorse
- **Documentazione:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **Riferimento API:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **Repository GitHub:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum di supporto:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Licenza temporanea:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-02-06  
**Testato con:** GroupDocs.Search 25.4  
**Autore:** GroupDocs  

---