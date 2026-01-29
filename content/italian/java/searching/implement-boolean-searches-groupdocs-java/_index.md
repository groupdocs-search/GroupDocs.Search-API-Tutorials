---
date: '2026-01-29'
description: Impara come implementare query booleane AND/OR in Java utilizzando GroupDocs.Search
  per Java, aggiungi documenti all'indice e migliora il recupero dei documenti.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean AND OR: padroneggia le ricerche booleane con GroupDocs.Search
  per Java'
type: docs
url: /it/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Padroneggia le ricerche booleane con GroupDocs.Search per Java

Cercare tra enormi collezioni di documenti può sembrare come trovare un ago in un pagliaio. Con le query **java boolean and or** puoi indicare al motore esattamente ciò di cui hai bisogno—documenti che contengono *entrambi* i termini, *uno* dei termini, o *escludere* parole indesiderate. In questa guida ti mostreremo come configurare **GroupDocs.Search for Java**, aggiungere documenti a un indice e creare potenti query booleane che migliorano i tuoi flussi di lavoro di **document retrieval java**.

## Risposte rapide
- **Cos'è una query boolean AND?** Restituisce solo i documenti che contengono *tutti* i termini specificati.  
- **In che modo OR differisce da AND?** OR corrisponde ai documenti con *qualsiasi* dei termini, ampliando il set di risultati.  
- **Quando dovrei usare NOT?** Usa NOT per filtrare i documenti che contengono parole indesiderate.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per i test; è necessaria una licenza commerciale per la produzione.  
- **Quale versione di Java è richiesta?** Java 8+ è supportata; JDK 11+ è consigliato.

## Cos'è **java boolean and or**?
Una query **java boolean and or** combina operatori logici (AND, OR, NOT) per affinare i risultati di ricerca. Strutturando le query, indichi a GroupDocs.Search esattamente come i termini si relazionano tra loro, fornendoti un controllo preciso sul processo di recupero.

## Perché usare GroupDocs.Search per Java?
- **Alte prestazioni** su grandi insiemi di documenti.  
- **API ricca** che supporta query basate su testo e su oggetti.  
- **Supporto linguistico integrato** per stemming, stop‑words e fuzzy matching.  
- **Integrazione facile** con Maven o download diretto del JAR.

## Prerequisiti
Prima di iniziare, assicurati di avere:

- **GroupDocs.Search for Java** (v25.4 o successivo) – vedi il link per il download qui sotto.  
- JDK 8+ installato e configurato nel tuo IDE (IntelliJ IDEA, Eclipse, ecc.).  
- Conoscenze di base di Java e Maven per la gestione delle dipendenze.  

## Configurare GroupDocs.Search per Java

### Configurazione Maven
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
Alternatively, download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della licenza
Inizia con una licenza di prova gratuita per esplorare tutte le funzionalità. Per l'uso in produzione, acquista una licenza commerciale per sbloccare tutte le funzionalità.

### Inizializzazione e configurazione di base
Crea una cartella per l'indice e istanzia l'oggetto `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or: Implementare ricerche booleane

Di seguito tratteremo le query **AND**, **OR**, **NOT** e **complex**. Ogni sezione mostra sia una query in testo semplice sia la query equivalente basata su oggetti, così potrai scegliere lo stile più adatto al tuo codice.

### Ricerca Boolean AND
Combina i termini con **AND** per recuperare solo i documenti che contengono *tutte* le parole chiave.

#### Panoramica
Una query AND restringe i risultati, migliorando la pertinenza quando hai bisogno di documenti che soddisfano più criteri.

#### Passaggi di implementazione

1. **Inizializza l'indice** – dimostra anche **add documents to index** per lo scenario AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Indicizza i documenti**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Esegui la ricerca con query di testo** – usando la sintassi di stringa semplice.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Esegui la ricerca con query oggetto** – utile quando si costruiscono query programmaticamente (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Ricerca Boolean OR
Usa **OR** per ampliare i risultati, corrispondendo a qualsiasi dei termini forniti.

#### Panoramica
Una query OR è ideale per ricerche esplorative dove vuoi catturare documenti contenenti almeno una di diverse parole chiave (**search with or java**).

#### Passaggi di implementazione

1. **Inizializza l'indice**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Indicizza i documenti**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Esegui la ricerca con query di testo**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Esegui la ricerca con query oggetto**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Ricerca Boolean NOT
Escludi termini indesiderati con **NOT** per filtrare il rumore dai risultati.

#### Panoramica
Una query NOT ti aiuta a eliminare documenti irrilevanti, ad esempio filtrando il nome di un marchio concorrente (**boolean search examples java**).

#### Passaggi di implementazione

1. **Inizializza l'indice**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Indicizza i documenti**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Esegui la ricerca con query di testo**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Esegui la ricerca con query oggetto**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Query Boolean complesse
Combina **AND**, **OR** e **NOT** per creare logiche di ricerca complesse per esigenze di recupero altamente specifiche.

#### Panoramica
Le query complesse ti permettono di modellare scenari di ricerca reali, come “trova articoli sportivi favorevoli ma escludi qualsiasi menzione di atleti specifici”.

#### Passaggi di implementazione

1. **Inizializza l'indice**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Indicizza i documenti**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Esegui la ricerca con query di testo**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Esegui la ricerca con query oggetto**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Applicazioni pratiche delle query java boolean and or
- **Document Management Systems** – individua i contratti che contengono sia “confidential” **AND** “renewal”.  
- **Legal Research** – filtra la giurisprudenza con **AND**/ **OR** escludendo leggi obsolete usando **NOT**.  
- **Customer Support** – recupera i ticket che menzionano “login” **AND** “error” ma non “resolved”.  
- **Content Curation** – raccogli i post del blog su “cloud” **OR** “serverless” per una newsletter.

## Problemi comuni e risoluzione dei problemi
- **Missing Index Refresh** – dopo aver aggiunto nuovi documenti, chiama `index.update()` per assicurarti che siano ricercabili.  
- **Incorrect Operator Spacing** – GroupDocs.Search si aspetta spazi attorno agli operatori (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – le query sono insensibili al maiuscolo/minuscolo per impostazione predefinita, ma gli analizzatori personalizzati possono influire.  
- **Large Result Sets** – usa la paginazione (`search(query, 0, 100)`) per evitare sovraccarico di memoria.

## Domande frequenti

**Q: Posso combinare più di due termini in una query AND?**  
A: Assolutamente. Puoi concatenare più oggetti `createWordQuery` con `createAndQuery`, oppure scrivere semplicemente `"term1 AND term2 AND term3"` nella query di testo.

**Q: GroupDocs.Search supporta ricerche wildcard o fuzzy?**  
A: Sì. Aggiungi `*` per il wildcard (es., `promot*`) o usa `~` per il fuzzy matching (es., `comfort~`).

**Q: Come posso limitare la ricerca a tipi di file specifici?**  
A: Usa la classe `FileTypeQuery` per restringere i risultati a PDF, DOCX, ecc., e combinala con la tua query booleana.

**Q: Qual è il modo migliore per monitorare le prestazioni dell'indicizzazione?**  
A: Abilita il logger integrato (`index.getLogger().setLevel(Level.INFO)`) e controlla le metriche di tempo dopo ogni operazione `add`.

**Q: Esiste un modo per aumentare la rilevanza di alcuni termini?**  
A: Sì. Avvolgi le parole importanti con `BoostQuery` per aumentare il loro peso nell'algoritmo di punteggio.

---

**Ultimo aggiornamento:** 2026-01-29  
**Testato con:** GroupDocs.Search 25.4 (Java)  
**Autore:** GroupDocs