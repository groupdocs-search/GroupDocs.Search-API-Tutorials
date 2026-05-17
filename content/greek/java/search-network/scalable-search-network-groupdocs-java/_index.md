---
date: '2026-05-17'
description: Μάθετε πώς να διαμορφώσετε base port groupdocs για ένα κλιμακώσιμο GroupDocs.Search
  Java δίκτυο, βελτιώστε την ταχύτητα ανάκτησης, και ρυθμίστε συστήματα πολλαπλών
  κόμβων.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: Διαμορφώστε base port groupdocs στο Java Search Network
type: docs
url: /el/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Διαμόρφωση βασικής θύρας groupdocs σε δίκτυο αναζήτησης Java

Σε σύγχρονες, δεδομενοβόρες εφαρμογές, **configure base port groupdocs** είναι το πρώτο βήμα για την κατασκευή μιας γρήγορης, αξιόπιστης υποδομής αναζήτησης. Είτε κάνετε ευρετηρίαση χιλιάδων PDF είτε επεκτείνετε σε πολλούς διακομιστές, η ανάθεση μοναδικών θυρών και καταλόγων αποτρέπει συγκρούσεις μεταξύ κόμβων και διατηρεί το σύμπλεγμα υγιές. Αυτό το εκπαιδευτικό υλικό σας καθοδηγεί μέσω των προαπαιτήσεων, της εγκατάστασης και μιας πλήρους πολυ‑κόμβου διαμόρφωσης χρησιμοποιώντας το GroupDocs.Search για Java, ώστε να μπορείτε να ξεκινήσετε ένα πραγματικά κλιμακώσιμο δίκτυο αναζήτησης σήμερα.

## Γρήγορες Απαντήσεις
- **Ποιος είναι ο κύριος σκοπός;** Να ανατεθούν μοναδικές θύρες και βασικοί φάκελοι για κάθε κόμβο αναζήτησης, εξαλείφοντας τις συγκρούσεις.  
- **Χρειάζομαι άδεια;** Ναι – απαιτείται δοκιμαστική ή πλήρης άδεια για παραγωγικές εγκαταστάσεις.  
- **Ποια έκδοση της Java υποστηρίζεται;** Java 8 ή νεότερη (συνιστάται Java 11+).  
- **Μπορώ να το τρέξω σε διακομιστές cloud;** Απολύτως – απλώς ανοίξτε τις επιλεγμένες θύρες στις ομάδες ασφαλείας του cloud σας.  
- **Πόσους κόμβους μπορώ να προσθέσω;** Δεν υπάρχει σκληρό όριο· περιορίζεστε μόνο από το υλικό και τη χωρητικότητα του δικτύου.

## Τι είναι το “configure base port groupdocs”;

**Configure base port groupdocs** είναι η διαδικασία ανάθεσης μιας αρχικής θύρας TCP που θα χρησιμοποιεί κάθε κόμβος αναζήτησης και αυξάνει για τους επόμενους κόμβους. Αυτό το απλό βήμα εξαλείφει τα ενοχλητικά σφάλματα “port already in use” και θέτει τα θεμέλια για ένα καθαρό, οριζόντια κλιμακώσιμο σύμπλεγμα αναζήτησης, διασφαλίζοντας ότι κάθε κόμβος επικοινωνεί μέσω ενός ξεχωριστού σημείου λήψης.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για ένα κλιμακώσιμο δίκτυο;

Το GroupDocs.Search προσφέρει **υψηλής απόδοσης ευρετηρίαση** (έως 50 GB/λεπτό σε έναν τυπικό διακομιστή 8‑πυρήνων) και υποστηρίζει **πάνω από 50 μορφές αρχείων** συμπεριλαμβανομένων PDF, DOCX, PPTX και HTML. Η αρθρωτή αρχιτεκτονική του σας επιτρέπει να συνδυάσετε ευρετηριαστές, αναζητητές, shards και εξαγωγείς μεταξύ κόμβων, παρέχοντας γραμμική κλιμάκωση καθώς προσθέτετε υλικό. Η βιβλιοθήκη προσφέρει επίσης ενσωματωμένες επιλογές συμπίεσης που μειώνουν τη χρήση δίσκου έως και 70 % διατηρώντας την καθυστέρηση ερωτήματος κάτω από 200 ms για τυπικά φορτία εργασίας.

## Προαπαιτούμενα
- **Java Development Kit (JDK)** 8 ή νεότερο (συνιστάται Java 11+ για καλύτερη διαχείριση μνήμης).  
- **IDE** όπως IntelliJ IDEA ή Eclipse.  
- **GroupDocs.Search for Java** βιβλιοθήκη (έκδοση 25.4 ή νεότερη) εγκατεστημένη μέσω Maven ή χειροκίνητου λήψης.  
- Βασικές γνώσεις δικτύωσης (θύρες TCP, localhost vs. απομακρυσμένοι κεντρικοί υπολογιστές).  
- Ένα έγκυρο **GroupDocs.Search** άδεια (δοκιμαστική ή πλήρης).

## Ρύθμιση GroupDocs.Search για Java

### Οδηγίες Εγκατάστασης

**Maven Setup:**

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

**Άμεση Λήψη:**

Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας

- **Free Trial** – ξεκινήστε τη δοκιμή αμέσως.  
- **Temporary License** – αποκτήστε εκτεταμένη δοκιμή στο [Temporary License](https://purchase.groupdocs.com/temporary-license).  
- **Full Purchase** – απαιτείται για παραγωγικές εγκαταστάσεις.

### Βασική Αρχικοποίηση και Ρύθμιση

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Οδηγός Υλοποίησης

### Πώς να διαμορφώσετε τη βασική θύρα groupdocs;

Για να διαμορφώσετε τη βασική θύρα, επεξεργαστείτε το αρχείο ρυθμίσεων δικτύου ή προγραμματιστικά ορίστε την ιδιότητα `basePort` σε μια υψηλή, αχρησιμοποίητη τιμή όπως 49100. Για κάθε επόμενο κόμβο αυξήστε τον αριθμό θύρας κατά ένα (ή με σταθερό βήμα) ώστε κάθε κόμβος να δεσμεύεται σε δικό του ξεχωριστό σημείο TCP, εξαλείφοντας σφάλματα σύγκρουσης θυρών και απλοποιώντας τους κανόνες του τείχους προστασίας.

#### Ρύθμιση Βασικών Διαδρομών

Πριν γράψετε κώδικα, αποφασίστε για μια συνεπή δομή φακέλων. Για παράδειγμα, δημιουργήστε ξεχωριστούς καταλόγους για ευρετηριαστές (`Indexer0`), αναζητητές (`Searcher0`) και εξαγωγείς (`Extractor0`). Αυτή η δομή επιτρέπει σε κάθε κόμβο να εντοπίζει τα αρχεία του γρήγορα.

- **Γιατί**: Μια προβλέψιμη ιεραρχία καταλόγων αποτρέπει σφάλματα “file not found” όταν οι κόμβοι ξεκινούν σε διαφορετικές μηχανές.

#### Διαμόρφωση Βασικής Θύρας

Επιλέξτε μια υψηλή αρχική θύρα για να αποφύγετε συγκρούσεις με κοινές υπηρεσίες (HTTP 80, SSH 22, κ.λπ.). Αυξήστε τον αριθμό θύρας για κάθε νέο κόμβο που προσθέτετε.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Γιατί**: Η εκκίνηση από μια υψηλή θύρα (π.χ., 49100) μειώνει την πιθανότητα σύγκρουσης με υπάρχουσες υπηρεσίες και απλοποιεί τη δημιουργία κανόνων τείχους προστασίας.

#### Ορισμός Διεύθυνσης Φιλοξενίας

Κατά την ανάπτυξη, το `localhost` λειτουργεί καλά. Για παραγωγή, αντικαταστήστε το με τη διεύθυνση IP του διακομιστή ή το όνομα DNS ώστε οι απομακρυσμένοι κόμβοι να μπορούν να επικοινωνούν μεταξύ τους.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Γιατί**: Η χρήση πραγματικής διεύθυνσης φιλοξενίας επιτρέπει επικοινωνία μεταξύ μηχανών, κάτι που είναι απαραίτητο για clusters σε cloud ή on‑premise.

#### Δημιουργία Ρυθμίσεων Δικτύου

Η κλάση `NetworkConfig` συγκεντρώνει όλες τις επιλογές δικτύωσης—βασική θύρα, φιλοξενία και προαιρετικές ρυθμίσεις SSL—σε ένα ενιαίο αντικείμενο που καταναλώνει η μηχανή αναζήτησης.

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Γιατί**: Η κεντρική διαχείριση αυτών των επιλογών κάνει τη διαμόρφωση επαναχρησιμοποιήσιμη και πιο εύκολη στη συντήρηση σε πολλούς κόμβους.

#### Προσθήκη Κόμβων

`SearchNode` αντιπροσωπεύει έναν μεμονωμένο κόμβο στο σύμπλεγμα GroupDocs.Search που εκτελεί συγκεκριμένη λειτουργία όπως ευρετηρίαση ή αναζήτηση. Δημιουργήστε ένα `SearchNode` για κάθε ρόλο (indexer, searcher, extractor) και καταχωρήστε το στο `SearchEngine`. Η κατανομή των ευθυνών μεταξύ κόμβων βελτιώνει τον παραλληλισμό και την ανθεκτικότητα σε σφάλματα.

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Γιατί**: Η κατανομή εργασίας σε αφιερωμένους κόμβους μειώνει τον ανταγωνισμό και επιτρέπει σε κάθε μηχανή να ειδικεύεται σε μία εργασία, αυξάνοντας τη συνολική απόδοση.

#### Ολοκλήρωση Διαμόρφωσης

Αφού προσθέσετε όλους τους κόμβους, καλέστε `engine.start()` για να ενεργοποιήσετε το δίκτυο. Η μηχανή θα δεσμεύσει αυτόματα κάθε κόμβο στην εκχωρημένη του θύρα και θα επαληθεύσει τη συνδεσιμότητα.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Κοινά Προβλήματα & Λύσεις

- **Συγκρούσεις Θυρών** – Πάντα αυξάνετε το `basePort` για κάθε νέο κόμβο. Επαληθεύστε τις ανοιχτές θύρες με `netstat` ή το εργαλείο παρακολούθησης δικτύου του λειτουργικού σας συστήματος.  
- **Αγνοούμενοι Κατάλογοι** – Βεβαιωθείτε ότι κάθε φάκελος (`Indexer0`, `Searcher0`, κ.λπ.) υπάρχει και η διαδικασία Java έχει δικαιώματα ανάγνωσης/εγγραφής.  
- **Διαθεσιμότητα Δικτύου** – Κατά τη μετάβαση σε περιβάλλον πολλαπλών μηχανών, αντικαταστήστε το `127.0.0.1` με την πραγματική IP του κεντρικού υπολογιστή και ανοίξτε τις επιλεγμένες θύρες στα τείχη προστασίας.

## Πρακτικές Εφαρμογές

| Σενάριο | Όφελος της διαμόρφωσης της βασικής θύρας groupdocs |
|----------|--------------------------------------------|
| Διαχείριση Εγγράφων Επιχειρήσεων | Απρόσκοπτη κλιμάκωση μεταξύ τμημάτων χωρίς διακοπές |
| Μεγάλες Πλατφόρμες CMS | Ταχύτερη ανάκτηση περιεχομένου καθώς το ευρετήριο είναι διανεμημένο |
| Διαχείριση Νομικών Υποθέσεων | Παράλληλη εξαγωγή PDF μειώνει την καθυστέρηση αναζήτησης |

## Παρατηρήσεις Απόδοσης

- **Παρακολούθηση CPU/Μνήμης** – Χρησιμοποιήστε το JMX της Java ή ένα εργαλείο profiling για να παρακολουθείτε τη χρήση νημάτων.  
- **Ρύθμιση Συμπίεσης** – `Compression.High` εξοικονομεί χώρο δίσκου αλλά μπορεί να προσθέσει φόρτο CPU· δοκιμάστε τόσο `High` όσο και `Normal` για να βρείτε το βέλτιστο.  
- **Τακτικές Ενημερώσεις** – Οι νέες εκδόσεις του GroupDocs.Search συχνά περιλαμβάνουν διορθώσεις απόδοσης· διατηρήστε τη βιβλιοθήκη ενημερωμένη.

## Συμπέρασμα

Τώρα έχετε μάθει πώς να **configure base port groupdocs** και να ρυθμίσετε ένα πολυ‑κόμβο δίκτυο αναζήτησης χρησιμοποιώντας το GroupDocs.Search για Java. Πειραματιστείτε με επιπλέον κόμβους, βελτιστοποιήστε τις ρυθμίσεις του ευρετηρίου και ενσωματώστε το δίκτυο στις υπάρχουσες εφαρμογές σας για μια πραγματικά κλιμακώσιμη λύση αναζήτησης.

## Συχνές Ερωτήσεις

**Ε: Ποιος είναι ο σκοπός της απενεργοποίησης των stop words στην ευρετηρίαση;**  
Α: Η απενεργοποίηση των stop words μπορεί να βελτιώσει την ακρίβεια της αναζήτησης διατηρώντας κοινές λέξεις που μπορεί να είναι κρίσιμες σε εξειδικευμένους τομείς.

**Ε: Πώς να αντιμετωπίσω συγκρούσεις θυρών όταν προσθέτω πολλαπλούς κόμβους;**  
Α: Ξεκινήστε με μια υψηλή `basePort` (π.χ., 49100) και αυξήστε την για κάθε επόμενο κόμβο, διασφαλίζοντας ότι κάθε κόμβος έχει μοναδικό σημείο TCP.

**Ε: Μπορώ να χρησιμοποιήσω αυτή τη ρύθμιση για εφαρμογές cloud;**  
Α: Ναι—απλώς βεβαιωθείτε ότι οι επιλεγμένες θύρες είναι ανοιχτές στις ομάδες ασφαλείας του cloud σας και αντικαταστήστε το `127.0.0.1` με τη σωστή δημόσια ή ιδιωτική IP.

**Ε: Ποια είναι η διαφορά μεταξύ NormalIndex και άλλων τύπων ευρετηρίου;**  
Α: `NormalIndex` προσφέρει μια ισορροπημένη ανταλλαγή μεταξύ ταχύτητας και χρήσης μνήμης, ενώ εξειδικευμένα ευρετήρια (π.χ., `FastIndex`) στοχεύουν σε εξειδικευμένα σενάρια απόδοσης.

**Ε: Υπάρχει όριο στον αριθμό των κόμβων που μπορώ να προσθέσω;**  
Α: Τεχνικά όχι· το όριο καθορίζεται από τους πόρους του υλικού σας και το εύρος ζώνης του δικτύου.

---

**Τελευταία Ενημέρωση:** 2026-05-17  
**Δοκιμή Με:** GroupDocs.Search Java 25.4  
**Συγγραφέας:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## Σχετικά Μαθήματα

- [Πώς να Διαμορφώσετε ένα Δίκτυο Αναζήτησης .NET Χρησιμοποιώντας το GroupDocs.Search και Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Πώς να Υλοποιήσετε ένα Δίκτυο Αναζήτησης με το GroupDocs.Search σε .NET για Συστήματα Διαχείρισης Εγγράφων](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Ανάπτυξη Κόμβου Δικτύου Αναζήτησης σε .NET χρησιμοποιώντας το GroupDocs για Αποτελεσματική Ευρετηρίαση και Ανάκτηση Εγγράφων](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)