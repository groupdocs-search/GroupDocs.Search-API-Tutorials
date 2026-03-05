---
date: '2026-02-03'
description: Scopri come aggiungere documenti all'indice ed eseguire ricerche efficienti
  senza distinzione tra maiuscole e minuscole in Java con GroupDocs.Search, utilizzando
  la sostituzione dei caratteri durante l'indicizzazione.
keywords:
- case-insensitive search in Java
- character replacement during indexing
- GroupDocs.Search setup
title: Aggiungi documenti all'indice per la ricerca senza distinzione tra maiuscole
  e minuscole in Java
type: docs
url: /it/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Aggiungere Documenti all'Indice percolo in Java

Quando è necessario **aggiungere documenti all'indice** e garantire che gli utenti possano trovare ciò che cercano indipendentemente dal caso delle lettere, una ricerca non sensibile al mai è essenziale. In questa guida vedremo comeizzato affidabili e non sensibili al caso ogni volta.

 “aggiungere documenti all'indice”?** Significa inserire i tuoi file sorgente in un indice ricercabile affinché possano essere interrogati in seguito.  
- **Perché utilizzare la sostituzione dei caratteri?** Normalizza il testo (ad esempio forzando tutto in minuscolo) così le ricerche ignorano le differenze di caso.  
- **È necessaria una licenza?** Una prova gratuita è sufficiente per lo sviluppo; è richiesta una licenza completa per la produzione.  
- **Quale versione di Java è richiesta?** Java 8 o superiore; la libreria è ottimizzata per Java 11+ per la massima compatibilità.  
- **Posso eseguire ricerche sensibili al caso se necessario?** Sì—le opzioni di ricerca consentono di attivare il comportamento sensibile al caso per ogni query.

## Che cosa significa “aggiungere documenti all'indice” in GroupDocs.Search?
Aggiungere documenti a un indice significa caricare file (PDF, documenti Word, testo semplice, ecc.) in una struttura dati che GroupDocs.Search può interrogare. La libreria analizza ogni file, estrae il testo ricercabile e lo memorizza in modo da rendere le ricerche rapide ed efficienti.

## Perché abilitare la sostituzione dei caratteri durante l'indicizzazione?
La sostituzione dei caratteri trasforma ogni carattere in un equivalente predefinito—di solito minuscolo—mentre l'indice viene costruito. Questo garantisce che una query come **“Promotion”** corrisponda a **“promotion”**, **“PROMOTION”** o a qualsiasi variante mista senza ulteriori sforzi da parte dell'utente.

## Prerequisiti
- **GroupDocs.Search per Java** versione 25.4 o più recente.  
- **Java Development Kit (JDK)** 8 o successivo installato.  
- Familiarità di base con **Maven** (o capacità di aggiungere manualmente i JAR).  

## Configurazione di GroupDocs.Search per Java

### Configurazione Maven
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

### Download Diretto
Se preferisci non usare Maven, scarica l'ultimo JAR dal sito ufficiale: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisizione della Licenza
- **Prova Gratuita** – scarica una licenza di prova per iniziare a sperimentare.  
- **Licenza Temporanea** – richiedi una licenza di test estesa dal portale GroupDocs.  
- **Licenza Completa** – acquista una licenza di produzione quando sei pronto per il rilascio.

### Inizializzazione di Base (Creare l'indice)
Il frammento seguente crea una cartella per l'indice e abilita le sostituzioni dei caratteri:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Guida all'Implementazione

### Abilitare la Sostituzione dei Caratteri nelle Impostazioni dell'Indice
Attivare questa funzionalità indica al motore di sostituire i caratteri durante l'indicizzazione, passo fondamentale per il comportamento non sensibile al caso.

#### Passo 1: Configurare `IndexSettings`
```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Configurare le Sostituzioni dei Caratteri
Mappa ogni carattere al suo equivalente minuscolo (o a qualsiasi mappatura personalizzata necessaria).

#### Passo 2: Definire e Aggiungere le Coppie di Sostituzione
```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Indicizzare i Documenti
Ora che l'indice è pronto, puoi **aggiungere documenti all'indice** da qualsiasi cartella.

#### Passo 3: Aggiungere Documenti per l'Indicizzazione
```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Eseguire Ricer caso, puoi attivare questa opzione per richiesta.

#### Passo 4: Eseguire Ricerche Sensibili al Caso
```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Applicazioni Pratiche
1. **Campagne di Marketing** – Normalizza i nomi dei prodotti affinché i team di vendita possano trovare le risorse senza preoccuparsi del caso.  
2. **Assistenza Clienti** – Alimenta le caselle di ricerca del help‑desk che restituiscono l'articolo corretto sia che l'utente digiti “login” o “Login”.  
3. **Cataloghi E‑commerce** – Garantenti trovino gli articoli indipazioni sulle Prestazioni
- **Organizzare i File Sorgente** – Una gerarchia di cartelle ordinata velocizza il passo **aggiungere documenti all'indice**.  
- **Monitorare la Memoria** – Corpora di grandi dimensioni possono consumare molta RAM; considera l'indicizzazione incrementale o il processamento a batch.  
- **Indicizzazione Asincrona** – Se la tua versione di GroupDocs.Search lo supporta, esegui l'indicizzazione in un thread di background per mantenere l'interfaccia reattiva.

## Problemi Comuni e Risoluzione
| Sintomo | Causa Probabile | Soluzione |
|---------|-----------------|-----------|
| Nessun risultato restituito per un termine noto | Sostituzioni dei caratteri non abilitate | Verifica `settings.setUseCharacterReplacements(true)` e che le sostituzioni siano state aggiunte. |
| Errore di out‑of‑memory durante l'indicizzazione | Indicizzazione di troppi file di grandi dimensioni contemporaneamente | Indicizza in batch più piccoli o aumenta l'heap JVM (`-Xmx`). |
| La ricerca restituisce risultati sensibili al caso in modo inatteso | È stato impostato `SearchOptions.setUseCaseSensitiveSearch(true)` | Rimuovi o imposta a `false` per il comportamento predefinito non sensibile al caso. |

## Domande Frequenti

**D: Come gestisco i caratteri speciali (ad es. “é”, “ß”) durante l'indicizzazione?**  
R: Includi quei caratteri nella tua mappa di sostituzione. Puoi mappare a equivalenti ASCII o mantenerli invariati, a seconda dei requisiti di ricerca.

**D: Posso limitare la sostituzione dei caratteri a una lingua specifica?**  
R: Sì. Crea un array di sostituzione personalizzato che contenga solo i caratteri della lingua target prima di aggiungerlo al dizionario.

**D: Cosa fare se l'indice impiega molto tempo a caricarsi?**  
R: Ottimizza la struttura delle cartelle, rimuovi i file non necessari e considera di persistere l'indice su un SSD veloce.

**D: È possibile annullare le sostituzioni dei caratteri dopo l'indicizzazione?**  
R: No. Le sostituzioni sono incorporate nei dati indicizzati; è necessario ricostruire l'indice con nuove impostazioni per modificarle.

**D: Dove posso trovare una documentazione API più dettagliata?**  
R: La documentazione ufficiale e il riferimento API forniscono dettagli esaustivi (vedi Risorse sotto).

## Risorse
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/) 

---

**Ultimo Aggiornamento:** 2026-02-03  
**Testato Con:** GroupDocs.Search 25.4 per Java  
**Autore:** GroupDocs