---
date: '2026-05-22'
description: Μάθετε πώς να προσθέτετε έγγραφα στο ευρετήριο και να δημιουργείτε κλιμακώσιμο
  δίκτυο αναζήτησης χρησιμοποιώντας το GroupDocs.Search for Java. Υποστηρίζει αναζήτηση
  σε πολλούς διακομιστές.
keywords:
- build scalable search network
- add documents to index
- search across multiple servers
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  headline: Build Scalable Search Network – Index Docs with GroupDocs Java
  type: TechArticle
- description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  name: Build Scalable Search Network – Index Docs with GroupDocs Java
  steps:
  - name: Define Base Path and Port
    text: The `SearchNetworkNode` class represents a single node that participates
      in the distributed index.
  - name: Configure the Network
    text: '`NetworkConfiguration` holds the common settings (base path, ports, replication
      factor) that every node reads at startup.'
  - name: Deploy Nodes Using Configuration
    text: '`SearchNetworkNode` instances are started with the same configuration file,
      allowing them to discover each other via the defined base port range.'
  - name: Define Subscription Method
    text: '`NodeEventListener` is an interface you implement to receive callbacks
      for indexing progress, errors, and node health changes.'
  - name: Use Subscription Method
    text: Register your listener with each node so that you get real‑time feedback
      during large batch operations.
  type: HowTo
- questions:
  - answer: Change the `basePort` variable in your configuration code to an available
      port.
    question: How do I handle port conflicts when deploying nodes?
  - answer: Yes, it supports real‑time indexing with appropriate configurations.
    question: Can GroupDocs.Search be used for real‑time indexing?
  - answer: Network connectivity and incorrect path settings are frequent culprits.
      Ensure all paths and ports are correctly configured.
    question: What are some common issues during node deployment?
  - answer: Absolutely. You can call `index.add(...)` on any node, and the network
      will distribute the new workload automatically.
    question: Is it possible to add documents to index after the network is running?
  - answer: A temporary trial license is sufficient for testing; a commercial license
      is required for production use.
    question: Do I need a license for development testing?
  type: FAQPage
title: Δημιουργία Κλιμακώσιμου Δικτύου Αναζήτησης – Ευρετηρίαση Εγγράφων με GroupDocs
  Java
type: docs
url: /el/java/search-network/scalable-search-groupdocs-java/
weight: 1
---

# Δημιουργία Κλιμακώσιμου Δικτύου Αναζήτησης – Καταχώρηση Εγγράφων με GroupDocs.Java

Σε αυτό το σεμινάριο θα μάθετε **πώς να προσθέτετε έγγραφα στο ευρετήριο** και **να δημιουργήσετε ένα κλιμακώσιμο δίκτυο αναζήτησης** με το GroupDocs.Search για Java. Θα περάσουμε από τη διαμόρφωση ενός δικτύου αναζήτησης, την ανάπτυξη κόμβων και τη διαχείριση συμβάντων ώστε η εφαρμογή σας να μπορεί να επεξεργάζεται αποδοτικά μεγάλες συλλογές εγγράφων σε πολλαπλούς διακομιστές.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “προσθήκη εγγράφων στο ευρετήριο”;** Σημαίνει την εισαγωγή αρχείων σε ένα ευρετήσιμο ευρετήριο ώστε να μπορούν να ερωτηθούν γρήγορα.  
- **Ποια βιβλιοθήκη παρέχει αυτή τη δυνατότητα;** GroupDocs.Search for Java.  
- **Χρειάζομαι άδεια;** Διατίθεται προσωρινή δοκιμαστική άδεια· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να κλιμακώσω οριζόντια;** Ναι—αναπτύσσοντας πολλαπλά στιγμιότυπα SearchNetworkNode.  
- **Ποια έκδοση Java απαιτείται;** JDK 8 ή νεότερη.

## Τι είναι η προσθήκη εγγράφων στο ευρετήριο;
Φορτώστε τα πηγαία αρχεία σας (PDF, DOCX, PPTX κ.λπ.) στη μηχανή GroupDocs.Search, η οποία εξάγει κείμενο, δημιουργεί πίνακες συχνότητας όρων και τα αποθηκεύει σε ένα αρχείο ευρετηρίου. Το προκύπτον ευρετήριο επιτρέπει ερωτήματα λέξεων-κλειδιών κάτω του δευτερολέπτου ακόμη και σε συλλογές με εκατοντάδες σελίδες.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java σε δικτυακό περιβάλλον;
Διανείμετε το φορτίο ευρετηρίου και αναζήτησης σε πολλούς κόμβους, μειώστε την καθυστέρηση ερωτημάτων επεξεργάζοντας κοντά στην πηγή των δεδομένων, και προσθέστε ή αφαιρέστε κόμβους χωρίς χρόνο διακοπής. Αυτή η αρχιτεκτονική σας επιτρέπει να **αναζητήσετε σε πολλαπλούς διακομιστές** διατηρώντας τη σταθερότητα της απόδοσης.

## Προαπαιτούμενα
- **Java Development Kit (JDK) 8+** εγκατεστημένο.  
- **Maven** για διαχείριση εξαρτήσεων.  
- Βασική εξοικείωση με τη Java και τη δομή έργου Maven.  

### Απαιτούμενες Βιβλιοθήκες, Εκδόσεις και Εξαρτήσεις
Για να υλοποιήσετε το GroupDocs.Search για Java, συμπεριλάβετε τα παρακάτω στο Maven έργο σας:

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

Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση από το [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/). Μπορείτε επίσης να βρείτε τις εκδόσεις στο [GroupDocs Search Java releases](https://releases.groupdocs.com/search/java/).

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
- JDK 8 ή νεότερο εγκατεστημένο στο σύστημά σας.  
- Maven εγκατεστημένο και ρυθμισμένο εάν χρησιμοποιείτε Maven έργο.

### Προαπαιτούμενες Γνώσεις
- Βασική κατανόηση του προγραμματισμού Java.  
- Εξοικείωση με τη διαχείριση εξαρτήσεων στο Maven.

## Ρύθμιση του GroupDocs.Search για Java

1. **Maven Setup**: Προσθέστε το αποθετήριο και την εξάρτηση όπως φαίνεται παραπάνω στο αρχείο `pom.xml`.  
2. **Direct Download**: Εναλλακτικά, κατεβάστε τη βιβλιοθήκη από το [GroupDocs Search Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας
- Αποκτήστε δωρεάν δοκιμαστική ή προσωρινή άδεια επισκεπτόμενοι το [GroupDocs website](https://purchase.groupdocs.com/temporary-license).  
- Για πλήρη πρόσβαση και υποστήριξη, σκεφτείτε την αγορά εμπορικής άδειας.

### Βασική Αρχικοποίηση

Αρχικοποιήστε το GroupDocs.Search στην Java εφαρμογή σας:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index/directory");

        // Add documents to the index
        index.add("path/to/documents");
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## Πώς να προσθέσετε έγγραφα στο ευρετήριο σε Δίκτυο Αναζήτησης;
Φορτώστε τα έγγραφά σας μέσω οποιουδήποτε κόμβου στο δίκτυο· το πλαίσιο διανέμει αυτόματα το φορτίο ευρετηρίου, εξισορροπεί το φορτίο και ενημερώνει το κοινό ευρετήριο σε πραγματικό χρόνο. Κάθε κόμβος επεξεργάζεται τα ανατεθειμένα αρχεία, εξάγει κείμενο και γράφει σταδιακές αλλαγές στο κεντρικό ευρετήριο, διασφαλίζοντας ότι το νέο περιεχόμενο γίνεται αναζητήσιμο σε όλους τους κόμβους σχεδόν αμέσως.

### Χαρακτηριστικό 1: Διαμόρφωση Δικτύου Αναζήτησης

#### Επισκόπηση
Η διαμόρφωση ενός δικτύου αναζήτησης περιλαμβάνει τη ρύθμιση κόμβων για τη διαχείριση και κατανομή εργασιών αναζήτησης αποδοτικά.

##### Βήμα 1: Ορισμός Βασικής Διαδρομής και Θύρας
Η κλάση `SearchNetworkNode` αντιπροσωπεύει έναν μοναδικό κόμβο που συμμετέχει στο κατανεμημένο ευρετήριο.  
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SearchNetworkNodeEvents/";
int basePort = 49140; // Change if necessary due to busy port issues
```

##### Βήμα 2: Διαμόρφωση του Δικτύου
`NetworkConfiguration` περιέχει τις κοινές ρυθμίσεις (βασική διαδρομή, θύρες, παράγοντας αντιγραφής) που διαβάζει κάθε κόμβος κατά την εκκίνηση.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.scaling.configuring.*;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

### Χαρακτηριστικό 2: Ανάπτυξη Κόμβων Δικτύου Αναζήτησης

#### Επισκόπηση
Αναπτύξτε κόμβους για τη διανομή και διαχείριση λειτουργιών αναζήτησης στο δίκτυό σας.

##### Βήμα 1: Ανάπτυξη Κόμβων Χρησιμοποιώντας Διαμόρφωση
Οι στιγμιότυπα `SearchNetworkNode` ξεκινούν με το ίδιο αρχείο διαμόρφωσης, επιτρέποντάς τους να ανακαλύπτουν ο ένας τον άλλο μέσω του καθορισμένου εύρους βασικής θύρας.  
```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
```

### Χαρακτηριστικό 3: Εγγραφή σε Συμβάντα Κόμβου

#### Επισκόπηση
Η εγγραφή σε συμβάντα κόμβου σας επιτρέπει να παρακολουθείτε και να αντιδράτε σε διάφορες ενέργειες εντός του δικτύου αναζήτησης.

##### Βήμα 1: Ορισμός Μεθόδου Εγγραφής
`NodeEventListener` είναι μια διεπαφή που υλοποιείτε για να λαμβάνετε κλήσεις επιστροφής σχετικά με την πρόοδο ευρετηρίου, σφάλματα και αλλαγές στην υγεία του κόμβου.  
```java
import com.groupdocs.search.events.*;
import com.groupdocs.search.scaling.events.*;

public static void subscribe(SearchNetworkNode node) {
    // Subscribe to IndexingCompleted event
    node.getEvents().IndexingCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            System.out.println("Indexing completed.");
        }
    });

    // Additional events can be subscribed similarly...
}
```

##### Βήμα 2: Χρήση Μεθόδου Εγγραφής
Καταχωρίστε τον ακροατή σας σε κάθε κόμβο ώστε να λαμβάνετε ανατροφοδότηση σε πραγματικό χρόνο κατά τις μεγάλες παρτίδες λειτουργιών.  
```java
SearchNetworkNode masterNode = nodes[0];
subscribe(masterNode);
```

### Κλείσιμο Κόμβων
Πάντα κλείστε τους κόμβους με χάρη ώστε να εκκαθαρίσετε τις εκκρεμείς εγγραφές και να απελευθερώσετε τις δικτυακές υποδοχές.  
```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Πρακτικές Εφαρμογές
1. **Enterprise Search Solutions** – Υλοποιήστε ένα δίκτυο αναζήτησης για τη διαχείριση μεγάλων αναζητήσεων εγγράφων σε πολλαπλούς διακομιστές.  
2. **E‑commerce Platforms** – Βελτιώστε τις δυνατότητες αναζήτησης προϊόντων διανέμοντας εργασίες ευρετηρίου σε πολλούς κόμβους.  
3. **Content Management Systems (CMS)** – Βελτιώστε την απόδοση ανάκτησης και ενημέρωσης περιεχομένου σε περιβάλλοντα CMS.  

## Σκέψεις Απόδοσης
- Βελτιστοποιήστε την ανάπτυξη κόμβων βάσει των πόρων του συστήματός σας.  
- Παρακολουθείτε τακτικά τη χρήση μνήμης για να αποτρέψετε διαρροές, ειδικά όταν διαχειρίζεστε μεγάλα σύνολα δεδομένων.  
- Χρησιμοποιήστε τις ρυθμίσεις διαμόρφωσης για να βελτιώσετε την ευρετηρίαση και τις λειτουργίες αναζήτησης για καλύτερη αποδοτικότητα.  

## Συχνά Προβλήματα και Λύσεις
| Πρόβλημα | Τυπική Αιτία | Λύση |
|----------|--------------|------|
| Συγκρούσεις θύρας | `basePort` ήδη σε χρήση | Αλλάξτε το `basePort` σε διαθέσιμο αριθμό |
| Ο κόμβος δεν είναι προσβάσιμος | Τείχος προστασίας ή κανόνες δικτύου | Ανοίξτε τις απαιτούμενες θύρες και επαληθεύστε τη συνδεσιμότητα |
| Το ευρετήριο δεν ενημερώνεται | Λανθασμένη διαδρομή εγγράφου | Επαληθεύστε ότι το `basePath` δείχνει στον σωστό φάκελο |
| Υψηλή χρήση μνήμης | Ευρετηρίαση μεγάλων παρτίδων | Ευρετηριάστε έγγραφα σε μικρότερες παρτίδες ή αυξήστε το μέγεθος heap |

## Συχνές Ερωτήσεις
**Q: Πώς να αντιμετωπίσω συγκρούσεις θύρας κατά την ανάπτυξη κόμβων;**  
A: Αλλάξτε τη μεταβλητή `basePort` στον κώδικα διαμόρφωσης σε διαθέσιμη θύρα.

**Q: Μπορεί το GroupDocs.Search να χρησιμοποιηθεί για ευρετηρίαση σε πραγματικό χρόνο;**  
A: Ναι, υποστηρίζει ευρετηρίαση σε πραγματικό χρόνο με τις κατάλληλες ρυθμίσεις.

**Q: Ποια είναι μερικά κοινά προβλήματα κατά την ανάπτυξη κόμβου;**  
A: Η συνδεσιμότητα δικτύου και οι λανθασμένες ρυθμίσεις διαδρομών είναι συχνά αιτίες. Βεβαιωθείτε ότι όλες οι διαδρομές και οι θύρες είναι σωστά διαμορφωμένες.

**Q: Είναι δυνατόν να προσθέσετε έγγραφα στο ευρετήριο μετά την εκκίνηση του δικτύου;**  
A: Απόλυτα. Μπορείτε να καλέσετε `index.add(...)` σε οποιονδήποτε κόμβο, και το δίκτυο θα διανείμει αυτόματα το νέο φορτίο.

**Q: Χρειάζομαι άδεια για δοκιμές ανάπτυξης;**  
A: Μια προσωρινή δοκιμαστική άδεια είναι επαρκής για δοκιμές· απαιτείται εμπορική άδεια για παραγωγική χρήση.

## Πόροι
- **Documentation**: [GroupDocs Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [Latest Release](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

Ακολουθώντας αυτόν τον οδηγό, μπορείτε αποτελεσματικά να **προσθέσετε έγγραφα στο ευρετήριο** και να διαχειριστείτε ένα ισχυρό, **να δημιουργήσετε κλιμακώσιμο δίκτυο αναζήτησης** χρησιμοποιώντας το GroupDocs.Search για Java. Καλή προγραμματιστική!

---

**Τελευταία Ενημέρωση:** 2026-05-22  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα
- [Μαθήματα Δικτύου Αναζήτησης για GroupDocs.Search .NET](/search/net/search-network/)
- [Πώς να Διαμορφώσετε ένα .NET Δίκτυο Αναζήτησης Χρησιμοποιώντας το GroupDocs.Search και Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Ανάπτυξη Κόμβου Δικτύου Αναζήτησης σε .NET χρησιμοποιώντας το GroupDocs για Αποτελεσματική Ευρετηρίαση και Ανάκτηση Εγγράφων](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)