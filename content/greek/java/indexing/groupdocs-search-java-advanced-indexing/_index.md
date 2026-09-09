---
date: '2026-08-15'
description: Μάθετε πώς να βελτιώσετε το search latency χρησιμοποιώντας τις δυνατότητες
  advanced indexing του GroupDocs.Search for Java, συμπεριλαμβανομένων των cancellation,
  async operations, multithreading και metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Βελτιώστε το search latency με το GroupDocs.Search for Java χρησιμοποιώντας
  cancellation, asynchronous indexing, multithreading και metadata customization.
  Boost performance και reduce resource use.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Βελτιώστε το search latency με advanced indexing στο GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Βελτιώστε το search latency με advanced indexing στο GroupDocs
type: docs
url: /el/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Βελτιώστε το χρόνο απόκρισης της αναζήτησης με προχωρημένη ευρετηρίαση στο GroupDocs

Στο σημερινό γρήγορα εξελισσόμενο ψηφιακό περιβάλλον, η **βελτίωση του χρόνου απόκρισης της αναζήτησης** είναι απαραίτητη για την παροχή άμεσων αποτελεσμάτων στους χρήστες. Είτε δημιουργείτε μια προσαρμοσμένη μηχανή αναζήτησης είτε βελτιώνετε ένα υπάρχον σύστημα διαχείρισης εγγράφων, η σωστή στρατηγική ευρετηρίασης μπορεί να μειώσει δραστικά τον χρόνο απόκρισης, να μειώσει την κατανάλωση πόρων και να **βελτιώσει το χρόνο απόκρισης της αναζήτησης** συνολικά. Σε αυτό το σεμινάριο θα εξετάσουμε τις πιο ισχυρές δυνατότητες του GroupDocs.Search για Java — ακύρωση, ασύγχρονη ευρετηρίαση, πολυνηματική επεξεργασία και προσαρμογή μεταδεδομένων — ώστε να μπορείτε να **προσθέτετε έγγραφα στο ευρετήριο** πιο γρήγορα και αποδοτικά.

**Τι θα μάθετε**

- Πώς να ακυρώσετε μια λειτουργία ευρετηρίασης μετά από καθορισμένο χρόνο  
- Εκτέλεση ασύγχρονων λειτουργιών ευρετηρίασης και διαχείριση αλλαγών κατάστασης  
- Διαμόρφωση πολυνηματικότητας για ταχύτερη ευρετηρίαση  
- Προσαρμογή επιλογών ευρετηρίασης μεταδεδομένων για **προσαρμογή μεταδεδομένων αναζήτησης**  

Ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε πριν βουτήξουμε στον κώδικα.

## Γρήγορες απαντήσεις
- **Τι κάνει η ακύρωση;** Σταματά την ευρετηρίαση μετά από ένα καθορισμένο χρονικό όριο, ελευθερώνοντας CPU και μνήμη για άλλες εργασίες.  
- **Μπορώ να ευρετηριάσω έγγραφα ασύγχρονα;** Ναι – ενεργοποιήστε το με `options.setAsync(true)`.  
- **Πόσα νήματα μπορώ να χρησιμοποιήσω;** Οποιοσδήποτε θετικός ακέραιος· 2‑4 νήματα είναι τυπικά για τους περισσότερους διακομιστές.  
- **Είναι η ευρετηρίαση μεταδεδομένων προαιρετική;** Απόλυτα – μπορείτε να την ενεργοποιήσετε ή να την ρυθμίσετε λεπτομερώς ανά πεδίο.  
- **Χρειάζομαι άδεια για αυτές τις λειτουργίες;** Μια δοκιμαστική άδεια λειτουργεί για δοκιμές· απαιτείται πλήρης άδεια για παραγωγή.

## Προαπαιτούμενα

- **GroupDocs.Search library** – έκδοση 25.4 ή νεότερη.  
- **Java Development Environment** – συνιστάται JDK 8 ή νεότερο.  
- Βασική εξοικείωση με τη Java και την έννοια της ευρετηρίασης.

### Ρύθμιση του GroupDocs.Search για Java

#### Εγκατάσταση Maven

Προσθέστε το αποθετήριο και την εξάρτηση στο αρχείο `pom.xml` σας:

`pom.xml` configuration tells Maven which GroupDocs.Search artifacts to download and include in your project.

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

#### Άμεση λήψη

Εναλλακτικά, κατεβάστε το πιο πρόσφατο JAR από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Απόκτηση άδειας** – Ξεκινήστε με μια δωρεάν δοκιμή ή ζητήστε προσωρινή άδεια για να ξεκλειδώσετε το πλήρες σύνολο λειτουργιών.

### Βασική αρχικοποίηση και ρύθμιση

Η κλάση `SearchIndex` είναι το σημείο εισόδου που αντιπροσωπεύει ένα ευρετήσιμο ευρετήριο αποθηκευμένο στο δίσκο ή στη μνήμη.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Τι σημαίνει «βελτιστοποίηση της απόδοσης αναζήτησης» σε αυτό το πλαίσιο;

Η βελτιστοποίηση της απόδοσης αναζήτησης σημαίνει τη διαμόρφωση της διαδικασίας ευρετηρίασης ώστε να καταναλώνει την κατάλληλη ποσότητα CPU, μνήμης και χρόνου, παρέχοντας τα πιο σχετικές αποτελέσματα άμεσα. Ελέγχοντας την ακύρωση, την ασύγχρονη εκτέλεση, το νήμα και τη διαχείριση μεταδεδομένων, επηρεάζετε άμεσα το πόσο γρήγορα η μηχανή μπορεί να **προσθέσει έγγραφα στο ευρετήριο** και να απαντήσει σε ερωτήματα.

## Γιατί να χρησιμοποιήσετε προχωρημένες λειτουργίες ευρετηρίασης;

Η ασύγχρονη και πολυνηματική ευρετηρίαση διατηρεί την εφαρμογή σας ανταποκρινόμενη, ενώ η ακύρωση αποτρέπει ατέρμονες διεργασίες. Οι λεπτομερώς ρυθμισμένες επιλογές μεταδεδομένων σας επιτρέπουν να προβάλλετε τις πιο σημαντικές πληροφορίες, κάτι που **βελτιώνει το χρόνο απόκρισης της αναζήτησης** για τους τελικούς χρήστες. Επιπλέον, αυτές οι λειτουργίες μειώνουν τις αιχμές CPU, μειώνουν την πίεση μνήμης και επιτρέπουν ομαλότερη κλιμάκωση όταν διαχειρίζεστε μεγάλους όγκους εγγράφων.

## Πώς να βελτιώσετε το χρόνο απόκρισης της αναζήτησης με προχωρημένη ευρετηρίαση;

Φορτώστε το αντικείμενο `SearchIndex`, διαμορφώστε το `IndexingOptions` με ρυθμίσεις ακύρωσης, ασύγχρονης λειτουργίας και αριθμού νημάτων, και στη συνέχεια καλέστε `index.add(document)` — αυτός ο συνδυασμός μειώνει το συνολικό χρόνο ευρετηρίασης έως και 60 % σε τυπικά φορτία εργασίας και εγγυάται ότι οι μακροχρόνιες εργασίες δεν θα μπλοκάρουν άλλες λειτουργίες. Μπορείτε επίσης να προσαρμόσετε τα όρια ευρετηρίασης μεταδεδομένων και να παρακολουθείτε την πρόοδο μέσω των γεγονότων αλλαγής κατάστασης για να διασφαλίσετε ότι η διαδικασία παραμένει εντός των προϋπολογισμών απόδοσης.

## Οδηγός υλοποίησης

### Ιδιότητα ακύρωσης

**Επισκόπηση** – Ακυρώστε την ευρετηρίαση μετά από καθορισμένη διάρκεια για να αποφύγετε την υπερβολική κατανάλωση πόρων.

#### Βήμα 1: ρύθμιση του περιβάλλοντος

Δημιουργήστε ένα αντικείμενο `SearchIndex` που δείχνει στο φάκελο του ευρετηρίου σας.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Βήμα 2: δημιουργία επιλογών ευρετηρίασης με ακύρωση

`IndexingOptions` σας επιτρέπει να καθορίσετε πώς συμπεριφέρεται η μηχανή ευρετηρίασης.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Κύρια σημεία**

- `setCancellation()` ενεργοποιεί τη λειτουργία.  
- `cancelAfter(int milliseconds)` ορίζει το χρονικό όριο (3 δευτερόλεπτα σε αυτό το παράδειγμα).

### Ιδιότητα ασύγχρονης λειτουργίας

**Επισκόπηση** – Εκτελέστε την ευρετηρίαση σε ένα νήμα παρασκηνίου και ακούστε τις αλλαγές κατάστασης.

#### Βήμα 1: ρύθμιση του περιβάλλοντος

Δημιουργήστε το ευρετήριο και προετοιμάστε τη συλλογή εγγράφων.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Βήμα 2: εγγραφή στο γεγονός αλλαγής κατάστασης

Το γεγονός `StatusChanged` σας ενημερώνει όταν η εργασία ευρετηρίασης μεταβαίνει μεταξύ καταστάσεων.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Βήμα 3: διαμόρφωση ασύγχρονων επιλογών

Ενεργοποιήστε τη λειτουργία async ώστε η κλήση να επιστρέφει αμέσως και η επεξεργασία να συνεχίζεται στο παρασκήνιο.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Ιδιότητα νημάτων

**Επισκόπηση** – Επιταχύνετε την ευρετηρίαση αξιοποιώντας πολλαπλούς πυρήνες CPU.

#### Βήμα 1: ρύθμιση του περιβάλλοντος

Προετοιμάστε το ευρετήριο και βεβαιωθείτε ότι η JVM διαθέτει αρκετή μνήμη heap.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Βήμα 2: διαμόρφωση πολυνηματικότητας

Ορίστε τον αριθμό των εργατικών νημάτων· κάθε νήμα επεξεργάζεται ένα υποσύνολο εγγράφων.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Ιδιότητα επιλογών ευρετηρίασης μεταδεδομένων

**Επισκόπηση** – Ρυθμίστε λεπτομερώς ποια μεταδεδομένα εγγράφων ευρετηριάζονται και πώς αποθηκεύονται.

#### Βήμα 1: ρύθμιση του περιβάλλοντος

Φορτώστε ένα έγγραφο που περιέχει πεδία μεταδεδομένων όπως συγγραφέας, τίτλος και προσαρμοσμένες ετικέτες.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Βήμα 2: διαμόρφωση επιλογών μεταδεδομένων

`MetadataIndexingOptions` σας επιτρέπει να ενεργοποιήσετε ή να απενεργοποιήσετε μεμονωμένα πεδία μεταδεδομένων και να ορίσετε όρια μεγέθους.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Πρακτικές εφαρμογές

1. **Συστήματα διαχείρισης εγγράφων** – Χρησιμοποιήστε ασύγχρονη ευρετηρίαση για να διατηρήσετε το UI ανταποκρινόμενο ενώ μεγάλες παρτίδες επεξεργάζονται στο παρασκήνιο.  
2. **Μηχανές αναζήτησης περιεχομένου** – Εφαρμόστε ακύρωση για να αποτρέψετε τις μακροχρόνιες εργασίες από το να καταναλώνουν πόρους του διακομιστή κατά τις ώρες αιχμής.  
3. **Συστήματα εισαγωγής μεγάλης κλίμακας** – Εκμεταλλευτείτε την πολυνηματική επεξεργασία για να **προσθέσετε έγγραφα στο ευρετήριο** σε μεγάλη κλίμακα, μειώνοντας δραστικά το χρόνο επεξεργασίας.

## Σκέψεις για την απόδοση

- **Διαχείριση νημάτων** – Παρακολουθήστε τη χρήση CPU· πολλά νήματα μπορούν να προκαλέσουν υπερβολικό κόστος εναλλαγής περιεχομένου.  
- **Αποτύπωμα μνήμης** – Τα όρια μεταδεδομένων (π.χ., `setMaxBytesToIndexField`) διατηρούν τη χρήση μνήμης προβλέψιμη.  
- **Καθαρισμός μνήμης (Garbage collection)** – Χρησιμοποιήστε κατάλληλες σημαίες JVM (`-Xmx`, `-XX:+UseG1GC`) όταν ευρετηριάζετε τεράστιες συλλογές.

## Συχνά προβλήματα και λύσεις

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| Η ευρετηρίαση δεν ολοκληρώνεται ποτέ | Η ακύρωση έχει οριστεί πολύ χαμηλά | Αυξήστε την τιμή `cancelAfter` ή αφαιρέστε την ακύρωση για μακροχρόνιες εργασίες |
| Δεν υπάρχουν ενημερώσεις κατάστασης σε ασύγχρονη λειτουργία | Ο διαχειριστής γεγονότων δεν έχει συνδεθεί σωστά | Βεβαιωθείτε ότι το `index.getEvents().StatusChanged.add(...)` καλείται πριν από το `index.add` |
| Σφάλματα έλλειψης μνήμης | Πάρα πολλά νήματα ή υψηλά όρια μεταδεδομένων | Μειώστε το `options.setThreads` και τα όρια πεδίων μεταδεδομένων |
| Απουσία μεταδεδομένων στα αποτελέσματα | Η ευρετηρίαση μεταδεδομένων είναι απενεργοποιημένη | Επαληθεύστε ότι το `options.getMetadataIndexingOptions()` είναι διαμορφωμένο και δεν είναι ρυθμισμένο να αγνοεί πεδία |

## Συχνές ερωτήσεις

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το GroupDocs.Search;**  
Α: Επισκεφθείτε τη [σελίδα προσωρινής άδειας του GroupDocs](https://purchase.groupdocs.com/temporary-license/) και ακολουθήστε τις οδηγίες στην οθόνη.

**Ε: Μπορώ να ακυρώσω μια λειτουργία ευρετηρίασης στη μέση;**  
Α: Ναι – χρησιμοποιήστε την ιδιότητα ακύρωσης με `cancelAfter()` ή καλέστε προγραμματιστικά το `Cancellation.cancel()`.

**Ε: Ποια είναι μερικά παραδείγματα χρήσης για ασύγχρονη ευρετηρίαση;**  
Α: Η ανάκτηση εγγράφων σε πραγματικό χρόνο, η επεξεργασία παρτίδων στο παρασκήνιο και οι εφαρμογές με ανταποκρινόμενο UI ωφελούνται από την ασύγχρονη ευρετηρίαση.

**Ε: Είναι ασφαλές να αυξήσω τον αριθμό των νημάτων σε κοινόχρηστο διακομιστή;**  
Α: Αυξήστε σταδιακά και παρακολουθήστε το φορτίο CPU· σε περιβάλλοντα με έντονη κοινή χρήση, διατηρήστε τον αριθμό των νημάτων μέτριο (2‑4).

**Ε: Πώς η ευρετηρίαση μεταδεδομένων επηρεάζει τη σχετικότητα της αναζήτησης;**  
Α: Τα σωστά ευρετηριασμένα μεταδεδομένα (συγγραφέας, ημερομηνία δημιουργίας, ετικέτες) μπορούν να έχουν μεγαλύτερο βάρος στα ερωτήματα, βελτιώνοντας την ακρίβεια των αποτελεσμάτων.

## Συμπέρασμα

Αποδεχόμενοι αυτές τις προχωρημένες δυνατότητες του GroupDocs.Search για Java, θα **βελτιώσετε το χρόνο απόκρισης της αναζήτησης** σε διάφορα σενάρια—από γρήγορη εισαγωγή εγγράφων έως λεπτομερή έλεγχο μεταδεδομένων. Πειραματιστείτε με διαφορετικές ρυθμίσεις, παρακολουθήστε τη χρήση πόρων και προσαρμόστε τις ρυθμίσεις στο συγκεκριμένο φορτίο εργασίας σας για να πετύχετε τα καλύτερα αποτελέσματα.

---

**Τελευταία ενημέρωση:** 2026-08-15  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά σεμινάρια

- [Βελτιώστε την απόδοση ερωτημάτων με GroupDocs.Search Java: Βελτιστοποίηση Ευρετηρίου & Αναζήτησης](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με ευρετηρίαση μεταδεδομένων σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Πώς να προσθέσετε πολλαπλά ψευδώνυμα και να προσθέσετε έγγραφα στο ευρετήριο στο GroupDocs.Search για Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)