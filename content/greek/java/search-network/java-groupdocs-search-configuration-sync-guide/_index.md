---
date: '2026-05-17'
description: Μάθετε πώς να προσθέσετε την εξάρτηση groupdocs Maven, να ρυθμίσετε ένα
  Java search network και να προσθέσετε directories στο index για γρήγορη, κλιμακώσιμη
  document retrieval.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Πώς να προσθέσετε την εξάρτηση GroupDocs Maven για το Search Network
type: docs
url: /el/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Πώς να Προσθέσετε την Εξάρτηση GroupDocs Maven για Δίκτυο Αναζήτησης

Σε αυτόν τον ολοκληρωμένο οδηγό θα ανακαλύψετε **πώς να προσθέσετε την εξάρτηση groupdocs Maven**, να διαμορφώσετε ένα ισχυρό δίκτυο αναζήτησης Java χρησιμοποιώντας το GroupDocs.Search, και να διατηρήσετε τα shards σας συγχρονισμένα. Είτε ευρετηριάζετε νομικές αναφορές, οικονομικές καταστάσεις ή ακαδημαϊκές εργασίες, τα παρακάτω βήματα θα σας βοηθήσουν να δημιουργήσετε ευρετήρια αναζήτησης, να διανείμετε το φορτίο ερωτημάτων σε κόμβους, και να διατηρήσετε τη συνοχή των δεδομένων με ελάχιστη προσπάθεια.

## Γρήγορες Απαντήσεις
- **Τι είναι η εξάρτηση GroupDocs Maven;** Ένα Maven artifact που περιλαμβάνει τη βιβλιοθήκη GroupDocs.Search για έργα Java.  
- **Γιατί να χρησιμοποιήσετε ένα δίκτυο αναζήτησης;** Διανέμει το φορτίο ευρετηρίασης και ερωτημάτων σε πολλαπλούς κόμβους, βελτιώνοντας την ταχύτητα και την αξιοπιστία.  
- **Πώς να προσθέσω καταλόγους για ευρετηρίαση;** Χρησιμοποιήστε `IndexingDocuments.addDirectories` στον κύριο κόμβο.  
- **Πώς να συγχρονίσετε τα shards;** Κλήστε `SynchronizeOptions` σε κάθε `Indexer` κόμβου.  
- **Χρειάζομαι άδεια;** Ναι, απαιτείται άδεια δοκιμής ή εμπορική άδεια για χρήση σε παραγωγή.

## Τι είναι η Εξάρτηση GroupDocs Maven;

Η `GroupDocs Maven dependency` είναι ένα Maven artifact που περιλαμβάνει τη βιβλιοθήκη GroupDocs.Search για έργα Java.  
Παρέχει όλες τις απαιτούμενες κλάσεις για τη δημιουργία ευρετηρίων αναζήτησης, τη διαχείριση κόμβων δικτύου και την εκτέλεση γρήγορων ερωτημάτων, ενώ το Maven επιλύει αυτόματα τις διαμεταβιβαστικές εξαρτήσεις, προσφέροντάς σας μια έτοιμη προς χρήση μηχανή αναζήτησης με λίγες μόνο γραμμές στο `pom.xml`.

## Πώς να Προσθέσετε την Εξάρτηση GroupDocs Maven

Προσθέστε τις καταχωρίσεις αποθετηρίου και εξάρτησης στο `pom.xml` σας, στη συνέχεια εκτελέστε `mvn clean install`; το Maven κατεβάζει το JAR `groupdocs-search` και τις απαιτούμενες βιβλιοθήκες του, καθιστώντας το API διαθέσιμο στο έργο σας. Μετά την επιτυχή κατασκευή μπορείτε να αρχίσετε να χρησιμοποιείτε αμέσως τις κλάσεις `com.groupdocs.search`.

### Διαμόρφωση Maven

Add the repository and dependency to your `pom.xml`:

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

> **Pro tip:** Διατηρήστε τον αριθμό έκδοσης ενημερωμένο ελέγχοντας τη σελίδα επίσημων εκδόσεων.

Μπορείτε επίσης να κατεβάσετε το JAR απευθείας από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Γιατί να Χρησιμοποιήσετε ένα Δίκτυο Αναζήτησης;

Ένα δίκτυο αναζήτησης επιτρέπει οριζόντια κλιμάκωση διαχωρίζοντας το ευρετήριο σε shards που βρίσκονται σε ξεχωριστούς κόμβους. Το GroupDocs.Search μπορεί να διαχειριστεί **πάνω από 50 μορφές εισόδου** και να επεξεργαστεί **έγγραφα πολλαπλών εκατοντάδων σελίδων** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, παρέχοντας απαντήσεις ερωτημάτων κάτω του δευτερολέπτου ακόμη και καθώς αυξάνεται ο όγκος των δεδομένων.

## Προαπαιτούμενα

- **JDK** (11 ή νεότερο) εγκατεστημένο.  
- Ένα IDE όπως το IntelliJ IDEA ή το Eclipse.  
- Βασικές γνώσεις Java, εξοικείωση με Maven, και κατανόηση των εννοιών κόμβων δικτύου.  
- Ένα έγκυρο άδεια GroupDocs.Search (δωρεάν δοκιμή ή εμπορική).

## Βασική Αρχικοποίηση και Ρύθμιση

Ξεκινήστε δημιουργώντας έναν κατάλογο ευρετηρίου:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

## Οδηγός Υλοποίησης

### Χαρακτηριστικό 1: Διαμόρφωση Δικτύου Αναζήτησης

#### Επισκόπηση

Η διαμόρφωση του δικτύου αναζήτησης ορίζει τις διαδρομές αρχείων και τις θύρες που θα χρησιμοποιούν οι κόμβοι για επικοινωνία.

##### Ρύθμιση Διαδρομών και Θυρών

Η Configuration είναι μια κλάση που περιέχει τις διαδρομές δικτύου, τις θύρες και άλλες ρυθμίσεις για το σύμπλεγμα αναζήτησης.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
Το αντικείμενο `configuration` τώρα περιέχει όλες τις απαραίτητες ρυθμίσεις για το δίκτυο αναζήτησης σας.

### Χαρακτηριστικό 2: Ανάπτυξη Κόμβων Δικτύου Αναζήτησης

#### Επισκόπηση

Αναπτύξτε κόμβους για να διανείμετε το φορτίο εργασίας στο δίκτυό σας. Ο κύριος κόμβος διαχειρίζεται τις λειτουργίες και τα γεγονότα.

##### Κώδικας Ανάπτυξης

Το SearchNetworkNode αντιπροσωπεύει έναν κόμβο στο δίκτυο αναζήτησης που μπορεί να λειτουργήσει ως κύριος ή εργαζόμενος.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Χαρακτηριστικό 3: Εγγραφή σε Γεγονότα Κόμβου Δικτύου Αναζήτησης

#### Επισκόπηση

Η ακρόαση των γεγονότων επιτρέπει δυναμική διαχείριση αλλαγών ή ενημερώσεων στο δίκτυό σας.

##### Υλοποίηση Εγγραφής

Το SearchNetworkNodeEvents παρέχει αγκίστρια γεγονότων για τον κύκλο ζωής του κόμβου και τις ενέργειες ευρετηρίασης.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Χαρακτηριστικό 4: Προσθήκη Καταλόγων στο Ευρετήριο

#### Επισκόπηση

Η προσθήκη καταλόγων είναι το βασικό βήμα που κάνει τα έγγραφά σας αναζητήσιμα.

##### Προσθήκη Εγγράφου

`IndexingDocuments.addDirectories` προσθέτει διαδρομές φακέλων στο ευρετήριο για επεξεργασία.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Χαρακτηριστικό 5: Συγχρονισμός Shards σε Κόμβο Δικτύου Αναζήτησης

#### Επισκόπηση

Ο συγχρονισμός εξασφαλίζει τη συνοχή των δεδομένων σε όλα τα shards.

##### Κώδικας Συγχρονισμού

`SynchronizeOptions` διαμορφώνει πώς τα shards συγχρονίζονται μεταξύ των κόμβων.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Χαρακτηριστικό 6: Κλείσιμο Κόμβων Δικτύου Αναζήτησης

#### Επισκόπηση

Το σωστό κλείσιμο των κόμβων απελευθερώνει πόρους και αποτρέπει διαρροές μνήμης.

##### Κλείσιμο Κόμβου

`close()` απελευθερώνει πόρους και τερματίζει τον κόμβο του δικτύου αναζήτησης.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Πρακτικές Εφαρμογές

1. **Legal Document Management** – Γρήγορη ανάκτηση φακέλων υποθέσεων και προτύπων.  
2. **Financial Record Keeping** – Πρόσβαση σε καταστάσεις και αρχεία ελέγχου σε δευτερόλεπτα.  
3. **Academic Research** – Αναζήτηση σε χιλιάδες εργασίες για εύρεση σχετικών παραπομπών.

## Σκέψεις για την Απόδοση

- **Optimize Queries** – Γράψτε σύντομες ερωτήσεις για μείωση του χρόνου απόκρισης.  
- **Memory Management** – Παρακολουθήστε τη χρήση heap της JVM· εξετάστε τη βελτιστοποίηση του GC για μεγάλα ευρετήρια.  
- **Scaling Strategy** – Προσθέστε κόμβους ανάλογα με τον όγκο των δεδομένων και το φορτίο ερωτημάτων.

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| Αποτυχία σύνδεσης κόμβων | Σύγκρουση θύρας | Αλλάξτε το `basePort` σε μια αχρησιμοποίητη τιμή |
| Το ευρετήριο δεν ενημερώνεται | Λείπει η εγγραφή σε γεγονότα | Βεβαιωθείτε ότι καλείται το `SearchNetworkNodeEvents.subscribe(masterNode)` |
| Υψηλή καθυστέρηση | Ανεπαρκή shards | Αυξήστε τον αριθμό των κόμβων και εξισορροπήστε τη διανομή των εγγράφων |

## Συχνές Ερωτήσεις

**Q: Ποιο είναι το κύριο όφελος από τη χρήση του GroupDocs.Search;**  
A: Παρέχει γρήγορες, κλιμακώσιμες δυνατότητες αναζήτησης σε μεγάλα σύνολα εγγράφων με ελάχιστη διαμόρφωση.

**Q: Μπορώ να προσαρμόσω τις ρυθμίσεις κόμβων σε ένα δίκτυο αναζήτησης;**  
A: Ναι, μπορείτε να ορίσετε προσαρμοσμένες διαδρομές, θύρες και άλλες επιλογές μέσω του αντικειμένου `Configuration`.

**Q: Πώς να προσθέσω καταλόγους στο ευρετήριο μετά την εκκίνηση του δικτύου;**  
A: Κλήστε το `IndexingDocuments.addDirectories(masterNode, "path")` όποτε χρειάζεται να ευρετηριάσετε νέους φακέλους.

**Q: Πώς να συγχρονίσετε τα shards όταν ένας νέος κόμβος ενταχθεί στο δίκτυο;**  
A: Χρησιμοποιήστε τη μέθοδο `synchronizeShards` που εμφανίζεται παραπάνω στον νέο κόμβο.

**Q: Χρειάζομαι άδεια για ανάπτυξη;**  
A: Μια άδεια δοκιμής είναι επαρκής για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.

## Συμπέρασμα

Ακολουθώντας αυτόν τον οδηγό, τώρα γνωρίζετε πώς να **προσθέσετε την εξάρτηση groupdocs Maven**, να διαμορφώσετε ένα πολυ‑κόμβο δίκτυο αναζήτησης, να ευρετηριάσετε καταλόγους και να διατηρήσετε τα shards συγχρονισμένα. Αυτά τα βήματα θέτουν τη βάση για μια λύση υψηλής απόδοσης αναζήτησης εγγράφων που μπορεί να αναπτυχθεί μαζί με τις ανάγκες του οργανισμού σας.

---

**Τελευταία Ενημέρωση:** 2026-05-17  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Μαθήματα και Παραδείγματα του GroupDocs.Search για Java](/search/net/)
- [Διαμόρφωση Δικτύου GroupDocs.Search σε .NET: Ένας Ολοκληρωμένος Οδηγός](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Πώς να Υλοποιήσετε ένα Δίκτυο Αναζήτησης με το GroupDocs.Search σε .NET για Συστήματα Διαχείρισης Εγγράφων](/search/net/search-network/implement-search-network-groupdocs-dotnet/)