---
date: '2026-03-06'
description: Scopri come aggiungere più alias, aggiungere documenti all'indice e gestire
  gli indici ricercabili in modo efficiente con GroupDocs.Search per Java.
keywords:
- GroupDocs.Search Java
- index management
- alias dictionary
title: Come aggiungere più alias e aggiungere documenti all’indice in GroupDocs.Search
  per Java
type: docs
url: /it/java/indexing/groupdocs-search-java-efficient-index-alias-management/
weight: 1
---

# Aggiungere più alias e aggiungere documenti all'indice in GroupDocs.Search Java: Guida completa

Nel mondo odierno guidato dai dati, la possibilità di **aggiungere più alias** mentre **aggiungi documenti all'indice** offre alla tua soluzione di ricerca un chiaro vantaggio di prestazioni. Che tu stia indicizzando migliaia di contratti, cataloghi di prodotti o articoli di ricerca, GroupDocs.Search per Java ti consente di **creare strutture di indice ricercabili** e di perfezionare le query con dizionari di alias—tutto mantenendo l'implementazione semplice e veloce.

## Risposte rapide
- **Qual è il primo passo per iniziare a usare GroupDocs.Search?** Aggiungi la dipendenza Maven e inizializza un oggetto `Index`.  
- **Come aggiungo documenti all'indice?** Chiama `index.add("<folder_path>")` con la cartella che contiene i tuoi file.  
- **Posso creare alias per query complesse?** Sì—usa il dizionario di alias per mappare token brevi a espressioni di query complete, e puoi anche **aggiungere più alias** in blocco.  
- **È possibile esportare e importare i dizionari di alias?** Assolutamente—usa i metodi `exportDictionary` e `importDictionary`.  
- **Quale versione di GroupDocs.Search è necessaria?** Versione 25.4 o successiva (il tutorial utilizza la 25.4).  

## Cos'è “add documents to index”?
Aggiungere documenti a un indice significa fornire file grezzi (PDF, DOCX, TXT, ecc.) a GroupDocs.Search affinché la libreria possa analizzarne il contenuto e costruire un **indice ricercabile**. Una volta indicizzati, è possibile eseguire query rapide e full‑text su tutti quei documenti.

## Perché gestire gli alias?
Gli alias ti consentono di sostituire frammenti di query lunghi e ripetitivi con token brevi e memorabili (ad esempio, `@t` → `(gravida OR promotion)`). Questo non solo accorcia le stringhe di ricerca, ma migliora anche la leggibilità, la manutenibilità e **ottimizza le prestazioni di ricerca**, soprattutto quando le query diventano complesse.

## Come aggiungere più alias?
GroupDocs.Search fornisce un comodo metodo `addRange` che consente di inserire molte coppie alias‑sostituzione in una sola volta. Questa operazione in blocco riduce l'overhead rispetto all'aggiunta di ogni alias singolarmente.

## Prerequisiti

- **GroupDocs.Search for Java** ≥ 25.4.  
- **JDK** (qualsiasi versione recente, ad es., 11+).  
- Un IDE come **IntelliJ IDEA** o **Eclipse**.  
- Conoscenze di base di Java e Maven.  

## Configurazione di GroupDocs.Search per Java

### Utilizzo di Maven
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

### Download diretto
In alternativa, scarica l'ultimo JAR dal sito ufficiale:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Passaggi per l'acquisizione della licenza
1. **Free Trial** – esplora tutte le funzionalità senza impegno.  
2. **Temporary License** – richiedi una chiave a breve termine per la valutazione.  
3. **Full Purchase** – ottieni una licenza permanente per l'uso in produzione.  

### Inizializzazione e configurazione di base

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        // Specify the directory to store indices
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
        
        // Create or open an index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## Guida all'implementazione

Di seguito è presente una panoramica completa di ogni funzionalità. Leggi prima le spiegazioni, poi copia il blocco di codice corrispondente.

### Creazione o apertura di un indice

**Come aggiungere documenti all'indice – prima è necessario un'istanza Index attiva.**

#### Passo 1: Importa la classe Index
```java
import com.groupdocs.search.Index;
```

#### Passo 2: Definisci dove verranno salvati i file dell'indice
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
```

#### Passo 3: Crea un nuovo indice o aprine uno esistente
```java
Index index = new Index(indexFolder);
```

### Aggiungere documenti a un indice

Ora che l'indice esiste, aggiungiamo **documenti all'indice**.

#### Passo 1: Indica la cartella di origine
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/Documents";
```

#### Passo 2: Aggiungi tutti i file supportati da quella cartella
```java
index.add(documentsFolder);
```

> **Consiglio:** Esegui questo passo ogni volta che arrivano nuovi file. GroupDocs.Search indicizzerà solo il nuovo contenuto, lasciando intatti gli elementi esistenti. Questa è l'essenza dell'**indicizzazione incrementale java**.

### Gestione del dizionario di alias

Gli alias ti consentono di mappare token brevi a stringhe di query complesse. Tratteremo la cancellazione delle voci vecchie, l'aggiunta di alias singoli e **l'aggiunta di più alias** in blocco.

#### Cancellazione degli alias esistenti
```java
if (index.getDictionaries().getAliasDictionary().getCount() > 0) {
    index.getDictionaries().getAliasDictionary().clear();
}
```

#### Aggiunta di alias singoli
```java
index.getDictionaries().getAliasDictionary().add("t", "(gravida OR promotion)");
index.getDictionaries().getAliasDictionary().add("e", "(viverra OR farther)");
```

#### Aggiunta di più alias
```java
AliasReplacementPair[] pairs = new AliasReplacementPair[] {
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};
index.getDictionaries().getAliasDictionary().addRange(pairs);
```

### Interrogazione delle sostituzioni di alias

Puoi recuperare il testo completo per qualsiasi alias definito:

```java
if (index.getDictionaries().getAliasDictionary().contains("e")) {
    String replacement = index.getDictionaries().getAliasDictionary().getText("e");
}
```

### Esportazione e importazione del dizionario di alias

L'esportazione è utile per backup o condivisione tra ambienti.

#### Esporta alias
```java
String fileName = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.getDictionaries().getAliasDictionary().exportDictionary(fileName);
```

#### Importa alias
```java
index.getDictionaries().getAliasDictionary().importDictionary(fileName);
```

### Ricerca usando query con alias

Con gli alias in posizione, le tue stringhe di ricerca diventano molto più pulite:

```java
String query = "@t OR @e";
SearchResult result = index.search(query);
```

Il simbolo `@` indica a GroupDocs.Search di sostituire il token con la sua espressione completa prima di eseguire la ricerca.

## Applicazioni pratiche

| Scenario | Come gli alias aiutano |
|----------|------------------------|
| **Gestione documenti legali** | Mappa i numeri di caso (`@case123`) a clausole Boolean complesse, accelerando il recupero. |
| **Ricerca prodotti e‑commerce** | Sostituisci combinazioni di attributi comuni (`@sale`) con `(discounted OR clearance)`. |
| **Basi di dati di ricerca** | Usa `@year2020` per espandere a un filtro di intervallo di date su molti articoli. |

## Considerazioni sulle prestazioni

- **Indicizzazione incrementale:** Aggiungi solo file nuovi o modificati; evita una re‑indicizzazione completa.  
- **Ottimizzazione JVM:** Assegna sufficiente memoria heap (`-Xmx4g` per corpora grandi).  
- **Aggiornamenti batch di alias:** Usa `addRange` per inserire molti alias in una volta, riducendo l'overhead.  
- **Ottimizza le prestazioni di ricerca:** Mantieni il dizionario di alias snello e riutilizza i token in modo intelligente per minimizzare il tempo di parsing delle query.

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| I nuovi file non sono ricercabili | Esegui nuovamente `index.add(newFolder)`; GroupDocs.Search indicizza solo i file non visti. |
| L'alias restituisce un risultato vuoto | Verifica che la chiave dell'alias (`@`) sia correttamente prefissata e che il dizionario contenga il token. |
| Elevato utilizzo di memoria durante l'indicizzazione in blocco | Aumenta la heap JVM (`-Xmx`) e considera l'indicizzazione in batch più piccoli. |

## Domande frequenti

**Q: Qual è il beneficio principale dell'utilizzo di GroupDocs.Search per Java?**  
A: Fornisce potenti capacità di indicizzazione e ricerca full‑text pronte all'uso, consentendo di **add documents to index** rapidamente e di interrogarli con alte prestazioni.

**Q: Posso usare GroupDocs.Search con i database?**  
A: Sì—estrai dati da qualsiasi fonte (SQL, NoSQL, CSV) e alimentali all'indice usando gli stessi metodi `add`.

**Q: Come gli alias migliorano l'efficienza della ricerca?**  
A: Gli alias ti permettono di memorizzare una logica di query complessa una sola volta e riutilizzarla con token brevi, riducendo il tempo di parsing della query e minimizzando gli errori umani quando **search with aliases**.

**Q: È possibile aggiornare un alias esistente senza ricostruire l'intero dizionario?**  
A: Assolutamente—basta chiamare `add` con la stessa chiave; la libreria sovrascriverà il valore precedente.

**Q: Cosa devo fare se la mia ricerca restituisce risultati inattesi?**  
A: Verifica che le definizioni degli alias siano corrette, re‑indicizza eventuali nuovi documenti e controlla le impostazioni dell'analyzer per problemi di tokenizzazione.

---

**Ultimo aggiornamento:** 2026-03-06  
**Testato con:** GroupDocs.Search 25.4 for Java  
**Autore:** GroupDocs