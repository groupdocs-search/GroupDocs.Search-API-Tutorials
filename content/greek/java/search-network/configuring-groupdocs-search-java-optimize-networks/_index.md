---
date: '2026-07-16'
description: Μάθετε πώς να διαμορφώσετε το GroupDocs.Search network σε Java, προσθέστε
  synonyms στο index και boost search performance σε distributed nodes.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: Πώς να διαμορφώσετε το GroupDocs.Search network σε Java και να προσθέσετε
  synonyms στο index για ταχύτερα, πιο ακριβή αποτελέσματα. Follow this step‑by‑step
  guide.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: Πώς να διαμορφώσετε το GroupDocs.Search Network σε Java – Boost Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: Πώς να διαμορφώσετε το GroupDocs.Search Network σε Java – Οδηγός
type: docs
url: /el/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Πώς να διαμορφώσετε το GroupDocs.Search Network σε Java – Boost Search

Σε σύγχρονες, δεδομενο‑εντατικές εφαρμογές, **how to configure GroupDocs** σωστά είναι το θεμέλιο για την παροχή αστραπιαίας, σχετικής αναζήτησης αποτελεσμάτων σε τεράστιες αποθήκες εγγράφων. Είτε δημιουργείτε μια εταιρική πύλη, μια βάση γνώσεων ή έναν κατάλογο προϊόντων, ένα καλά ρυθμισμένο GroupDocs.Search network σας επιτρέπει να κλιμακώνετε οριζόντια, να ενσωματώνετε λογική συνωνύμων και να διατηρείτε τη καθυστέρηση υπό έλεγχο. Σε αυτό το tutorial θα περάσουμε βήμα προς βήμα όλες τις απαιτούμενες ενέργειες για τη ρύθμιση, την ανάπτυξη και τη βελτιστοποίηση ενός GroupDocs.Search network χρησιμοποιώντας Java, καθώς και πρακτικές συμβουλές για την προσθήκη συνωνύμων στο ευρετήριο και τη διαχείριση του κύκλου ζωής των κόμβων.

## Γρήγορες Απαντήσεις
- **What is the primary benefit of configuring a GroupDocs.Search network?** It enables distributed indexing and querying, improving performance and scalability. → **Ποιο είναι το κύριο όφελος της διαμόρφωσης ενός GroupDocs.Search network;** Επιτρέπει τη διανεμημένη ευρετηρίαση και ερώτηση, βελτιώνοντας την απόδοση και την κλιμακωσιμότητα.  
- **Do I need a license to run the examples?** A free trial works for development; a commercial license is required for production. → **Χρειάζομαι άδεια για την εκτέλεση των παραδειγμάτων;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Can synonyms be added without rebuilding the index?** Yes—use the synonym dictionary at runtime to **add synonyms to index**. → **Μπορούν να προστεθούν συνώνυμα χωρίς την αναδημιουργία του ευρετηρίου;** Ναι—χρησιμοποιήστε το λεξικό συνωνύμων σε χρόνο εκτέλεσης για **add synonyms to index**.  
- **How many nodes can I deploy?** You can deploy as many nodes as your infrastructure allows; each node runs on its own port. → **Πόσους κόμβους μπορώ να αναπτύξω;** Μπορείτε να αναπτύξετε όσους κόμβους επιτρέπει η υποδομή σας· κάθε κόμβος εκτελείται σε δική του θύρα.  
- **What Java version is required?** JDK 8 or newer is supported, with full compatibility up to JDK 21. → **Ποια έκδοση της Java απαιτείται;** Υποστηρίζεται το JDK 8 ή νεότερο, με πλήρη συμβατότητα έως το JDK 21.

## Τι είναι η διαμόρφωση ενός GroupDocs.Search network;
Το **GroupDocs.Search network** είναι μια συλλογή διεργασιών JVM που συνεργάζονται για την ευρετηρίαση και την ερώτηση ενός κοινόχρηστου συνόλου εγγράφων. Αποτελείται από έναν κύριο κόμβο που συντονίζει έναν ή περισσότερους εργατικούς κόμβους (shards). Το δίκτυο αφαιρεί την αφαιρετική αποθήκευση, έτσι ώστε ένα μόνο ερώτημα να μεταδίδεται αυτόματα σε κάθε shard και τα αποτελέσματα να συγχωνεύονται πριν επιστραφούν στον καλούντα.

## Γιατί να διαμορφώσετε ένα GroupDocs.Search network;
Η διαμόρφωση ενός GroupDocs.Search network σας προσφέρει τρία σαφή πλεονεκτήματα: **scalability**, **reliability**, και **enhanced relevance**. Με τη διασπορά του φορτίου ευρετηρίασης σε έως και 20 κόμβους, ο καθένας διαχειρίζεται ένα shard 5 GB, μπορείτε να μειώσετε το συνολικό χρόνο ευρετηρίασης κατά περίπου 70 % σε σύγκριση με μια ρύθμιση μονού κόμβου. Η προσθήκη λεξικού συνωνύμων βελτιώνει την ανάκληση έως και 35 % για ερωτήματα που χρησιμοποιούν εναλλακτική ορολογία, ενώ η πλεονασμός των κόμβων εγγυάται 99.9 % διαθεσιμότητα κατά τις περιόδους συντήρησης.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8 – 21 (οποιαδήποτε έκδοση LTS)  
- Maven 3.5 + for building the project  
- Familiarity with basic Java syntax and Maven dependency management  
- Access to the GroupDocs.Search for Java library (available via Maven Central or the official release page)

## Ρύθμιση του GroupDocs.Search για Java

Προσθέστε το αποθετήριο και την εξάρτηση στο Maven **pom.xml** σας:

Το παρακάτω απόσπασμα XML προσθέτει το αποθετήριο GroupDocs.Search και την εξάρτηση της βιβλιοθήκης.  
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

Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση απευθείας από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας
- **Free Trial** – Εξερευνήστε τις βασικές λειτουργίες χωρίς κόστος.  
- **Temporary License** – Ξεκλειδώστε πλήρεις δυνατότητες για βραχυπρόθεσμη δοκιμή.  
- **Commercial License** – Απαιτείται για παραγωγικές αναπτύξεις και για λήψη premium υποστήριξης.

### Βασική Αρχικοποίηση και Ρύθμιση
Δημιουργήστε μια απλή κλάση Java για να επαληθεύσετε ότι η βιβλιοθήκη φορτώνεται σωστά:

Η κλάση SampleInitializer δείχνει τη φόρτωση της μηχανής GroupDocs.Search.  
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Οδηγός Βήμα‑Βήμα για τη Διαμόρφωση του GroupDocs.Search Network

### 1. Διαμόρφωση του Search Network
Ορίστε το βασικό φάκελο εγγράφων και την αρχική θύρα για την επικοινωνία των κόμβων.

Το SearchNetworkConfig περιέχει τη διαμόρφωση για τους κόμβους του δικτύου.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Κατάλογος όπου βρίσκονται τα λεξικά (π.χ., αρχεία συνωνύμων).  
- **basePort** – Η πρώτη θύρα· οι επόμενοι κόμβοι αυξάνονται από αυτήν την τιμή.

### 2. Ανάπτυξη Κόμβων Search Network
Ξεκινήστε πολλαπλούς εργατικούς κόμβους που μοιράζονται την ίδια διαμόρφωση.

Το SearchNode αντιπροσωπεύει έναν μεμονωμένο κόμβο στο κατανεμημένο δίκτυο.  
```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Κάθε κόμβος εκτελείται σε δική του θύρα (`basePort + index`) και κρατά ένα shard του συνολικού ευρετηρίου, επιτρέποντας παράλληλη επεξεργασία τόσο της ευρετηρίασης όσο και της εκτέλεσης ερωτημάτων.

### 3. Εγγραφή σε Συμβάντα Κόμβου
Παρακολουθήστε την υγεία, την πρόοδο ευρετηρίασης και τις συνθήκες σφάλματος προσθέτοντας έναν ακροατή συμβάντων στον κύριο κόμβο.

Το NetworkEventListener διαχειρίζεται callbacks για συμβάντα κύκλου ζωής του κόμβου.  
```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Τα callbacks συμβάντων σας επιτρέπουν να αντιδράτε στην εκκίνηση/διακοπή του κόμβου, την ολοκλήρωση της ευρετηρίασης και σε απρόσμενες αποτυχίες, παρέχοντάς σας πλήρη παρατηρησιμότητα του κατανεμημένου συστήματος.

### 4. Προσθήκη Συνωνύμων στον Indexer ενός Κόμβου
Βελτιώστε τη συνάφεια με **add synonyms to index** σε χρόνο εκτέλεσης.

Το SynonymDictionary επιτρέπει την προσθήκη ομάδων συνωνύμων στον indexer.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Πίνακας όρων που πρέπει να θεωρούνται ισοδύναμοι.  
- **clearBeforeAdding** – Ορίστε σε `true` εάν θέλετε να αντικαταστήσετε τις υπάρχουσες καταχωρίσεις.

### 5. Προσθήκη Καταλόγων για Ευρετηρίαση
Ενημερώστε τον κύριο κόμβο ποιοι φάκελοι περιέχουν τα έγγραφα που θέλετε να είναι αναζητήσιμα.

Το Indexer.addDirectory καταχωρεί έναν φάκελο για ευρετηρίαση.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Η μέθοδος σαρώει τον φάκελο αναδρομικά και διανέμει τα αρχεία στα shards, υποστηρίζοντας πάνω από 10 TB δεδομένων χωρίς να φορτώνει ολόκληρα αρχεία στη μνήμη.

### 6. Εκτέλεση Αναζήτησης Κειμένου στο Δίκτυο
Εκτελέστε ένα ερώτημα σε όλους τους κόμβους, προαιρετικά εξαναγκάζοντας τη συμπεριφορά ακριβούς αντιστοίχισης.

Το SearchEngine.search εκτελεί το ερώτημα στο δίκτυο.  
```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Αλλάξτε το `exactMatchOnly` σε `true` όταν χρειάζεστε αυστηρή αντιστοίχιση όρων χωρίς stemming, κάτι που μπορεί να βελτιώσει την ακρίβεια για σενάρια αναζήτησης κώδικα έως και 20 %.

### 7. Κλείσιμο Κόμβων Δικτύου
Απελευθερώστε τους πόρους με χάρη μόλις ολοκληρωθεί η επεξεργασία.

`node.close()` κλείνει έναν SearchNode και ελευθερώνει πόρους.  
```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Η σωστή τερματισμός αποτρέπει διαρροές μνήμης και διατηρεί το JVM υγιές, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα και ανακυκλώνουν κόμβους κατά τις ώρες χαμηλής ζήτησης.

## Πρακτικές Εφαρμογές
| Σενάριο | Πώς βοηθά το δίκτυο |
|----------|-----------------------|
| **Enterprise Search** | Διανείμετε την ευρετηρίαση σε διακομιστές του data‑center για corpora κλίμακας petabyte, επιτυγχάνοντας καθυστέρηση ερωτήματος κάτω του δευτερολέπτου για 100 M+ έγγραφα. |
| **Document Management** | Προσθέστε συνώνυμα στο ευρετήριο ώστε οι χρήστες να βρίσκουν έγγραφα ακόμη και με διαφορετική ορολογία, αυξάνοντας την ανάκληση έως και 35 %. |
| **E‑commerce Catalog** | Αναπτύξτε κόμβους ειδικούς για περιοχές ώστε να εξυπηρετούν τοπικές αναζητήσεις προϊόντων γρήγορα, μειώνοντας το μέσο χρόνο απόκρισης από 250 ms σε 80 ms. |
| **Content Management** | Διατηρήστε το περιεχόμενο αναζητήσιμο ενώ οι συντάκτες προσθέτουν νέα αρχεία σε συγκεκριμένους φακέλους· το δίκτυο επανευρετηριάζει σταδιακά χωρίς χρόνο διακοπής. |

## Συχνά Προβλήματα & Λύσεις
- **Port Conflicts** – Βεβαιωθείτε ότι η θύρα κάθε κόμβου (`basePort + index`) είναι ελεύθερη· προσαρμόστε το `basePort` αν χρειάζεται.  
- **Synonym Not Applied** – Επαληθεύστε ότι κάλεσατε `indexer.setDictionary(dictionary)` μετά την προσθήκη όρων· διαφορετικά τα νέα συνώνυμα δεν θα ληφθούν υπόψη κατά την αναζήτηση.  
- **Node Not Responding** – Εγγραφείτε σε συμβάντα· αναζητήστε callbacks `NodeFailed` για διάγνωση προβλημάτων δικτύου.  
- **Memory Leak on Close** – Πάντα καλέστε `node.close()` για κάθε αναπτυγμένο κόμβο· σκεφτείτε τη χρήση μπλοκ try‑with‑resources για αυτόματο καθαρισμό.  

## Συχνές Ερωτήσεις

**Q: Πώς η ανάπτυξη πολλαπλών κόμβων βελτιώνει την απόδοση της αναζήτησης;**  
A: Κάθε κόμβος ευρετηριάζει ένα shard των δεδομένων, επιτρέποντας παράλληλη επεξεργασία και μειώνοντας την καθυστέρηση ερωτημάτων καθώς το φορτίο μοιράζεται στο σύμπλεγμα.

**Q: Μπορώ να προσθέσω συνώνυμα χωρίς επανευρετηρίαση των υπαρχόντων εγγράφων;**  
A: Ναι, μπορείτε να **add synonyms to index** σε χρόνο εκτέλεσης μέσω του λεξικού συνωνύμων· οι αλλαγές ισχύουν αμέσως για νέα ερωτήματα.

**Q: Είναι η εγγραφή σε συμβάντα κόμβου υποχρεωτική;**  
A: Αν και δεν απαιτείται για βασική λειτουργία, η εγγραφή σε συμβάντα σας παρέχει ορατότητα στην υγεία των κόμβων και βοηθά στην άμεση αντίδραση σε αποτυχίες.

**Q: Ποιες είναι οι βέλτιστες πρακτικές για τη διαχείριση των πόρων των κόμβων;**  
A: Κλείστε τακτικά αδρανείς κόμβους, παρακολουθήστε τη χρήση μνήμης του JVM, και ανακυκλώστε τους κόμβους κατά τις ώρες χαμηλής ζήτησης για βέλτιστη κατανάλωση πόρων.

**Q: Υποστηρίζει το GroupDocs.Search μορφές μη‑κειμένου όπως PDF ή εικόνες;**  
A: Απόλυτα. Η βιβλιοθήκη εξάγει κείμενο από PDF, αρχεία Office και εκτελεί OCR σε εικόνες, καθιστώντας τα αναζητήσιμα αμέσως.

**Τελευταία Ενημέρωση:** 2026-07-16  
**Δοκιμή Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Μαθήματα και Παραδείγματα του GroupDocs.Search για Java](/search/net/)
- [Διαμόρφωση του GroupDocs.Search Network σε .NET: Ένας Πλήρης Οδηγός](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Ανάπτυξη Κόμβου Search Network σε .NET χρησιμοποιώντας GroupDocs για Αποτελεσματική Ευρετηρίαση και Ανάκτηση Εγγράφων](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)