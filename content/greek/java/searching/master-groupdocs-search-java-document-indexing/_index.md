---
date: '2026-09-11'
description: Μάθετε πώς να επισημαίνετε τα αποτελέσματα αναζήτησης Java και να ευρετηριάζετε
  έγγραφα Java χρησιμοποιώντας το GroupDocs.Search for Java με τόσο synchronous όσο
  και asynchronous ευρετηρίαση.
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: Επισήμανση αποτελεσμάτων αναζήτησης Java με το GroupDocs.Search. Μάθετε
  για synchronous και asynchronous ευρετηρίαση, real‑time ενημερώσεις, και επισήμανση
  αποτελεσμάτων σε εφαρμογές Java.
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: Επισήμανση αποτελεσμάτων αναζήτησης Java – Γρήγορη synchronous & async ευρετηρίαση
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: Επισήμανση αποτελεσμάτων αναζήτησης Java – Συγχρονισμένη & ασύγχρονη ευρετηρίαση
type: docs
url: /el/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Επισήμανση αποτελεσμάτων αναζήτησης Java – Συγχρονισμένη & ασύγχρονη ευρετηρίαση

Σε αυτόν τον οδηγό θα ανακαλύψετε πώς να **highlight search results Java** χρησιμοποιώντας τη βιβλιοθήκη GroupDocs.Search, και θα δείτε βήμα‑βήμα πώς να ευρετηριάσετε έγγραφα Java τόσο συγχρονισμένα όσο και ασύγχρονα. Είτε δημιουργείτε ένα μικρό εργαλείο επιφάνειας εργασίας είτε μια μεγάλης κλίμακας υπηρεσία αναζήτησης για επιχειρήσεις, αυτές οι τεχνικές σας επιτρέπουν να παρέχετε άμεσες, οπτικά σαφείς αντιστοιχίες χωρίς να μπλοκάρετε τα νήματα της εφαρμογής σας.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “highlight search results Java”;** Σημαίνει την περιτύλιξη κάθε ταιριασμένου όρου στα επιστρεφόμενα αποσπάσματα με σήμανση (π.χ., `<mark>`) ώστε οι χρήστες να βλέπουν άμεσα το πλαίσιο του αποτελέσματος.  
- **Πότε πρέπει να χρησιμοποιήσω συγχρονισμένη ευρετηρίαση;** Χρησιμοποιήστε την για μικρές‑μέτριες συλλογές όπου χρειάζεται το έγγραφο να είναι αναζητήσιμο τη στιγμή που προστίθεται.  
- **Πότε είναι προτιμότερη η ασύγχρονη ευρετηρίαση;** Επιλέξτε την για μεγάλες παρτίδες ή όταν το νήμα UI πρέπει να παραμένει ανταποκρινόμενο ενώ το ευρετήριο δημιουργείται στο παρασκήνιο.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· μια πλήρης άδεια αφαιρεί τους περιορισμούς και ξεκλειδώνει προηγμένα χαρακτηριστικά.  
- **Ποια έκδοση της Java υποστηρίζεται;** Java 8 ή νεότερη.

## Τι είναι η “επισήμανση αποτελεσμάτων αναζήτησης Java”;
`highlight search results java` είναι η διαδικασία λήψης ακατέργαστων δεδομένων αντιστοίχισης από το GroupDocs.Search και εισαγωγής οπτικών ενδείξεων—συνήθως ετικετών HTML `<mark>`—γύρω από κάθε ευρεθέν όρο. Αυτό κάνει τα αποσπάσματα αποτελεσμάτων άμεσα αναγνώσιμα σε μια ιστοσελίδα ή στοιχείο Swing, βελτιώνοντας την εμπειρία χρήστη δείχνοντας ακριβώς πού εμφανίζεται το ερώτημα.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
Το GroupDocs.Search παρέχει μια υψηλής απόδοσης, γλώσσα‑ανεξάρτητη μηχανή που μπορεί **να επεξεργάζεται έως 5 000 έγγραφα ανά δευτερόλεπτο**, **να υποστηρίζει 30+ μορφές αρχείων**, και **να ευρετηριάζει συλλογές 10 εκατομμυρίων εγγράφων** χωρίς να φορτώνει ολόκληρο το σώμα στη μνήμη. Η ενσωματωμένη επισήμανση, η ευρετηρίαση σε πραγματικό χρόνο, και οι πολυγλωσσικοί αναλυτές την καθιστούν ιδανική για συστήματα διαχείρισης περιεχομένου, καταλόγους e‑commerce, και εταιρικά αποθετήρια εγγράφων.

## Προαπαιτούμενα
- **Java Development Kit** (JDK 8 ή νεότερο) εγκατεστημένο και το `JAVA_HOME` σωστά ορισμένο.  
- Ένα IDE όπως το **IntelliJ IDEA** ή το **Eclipse**.  
- Ένας φάκελος (π.χ., `documents/`) που περιέχει τα αρχεία που θέλετε να ευρετηριάσετε—απλό κείμενο, PDF, DOCX, κ.λπ.  
- Maven για διαχείριση εξαρτήσεων (ή μπορείτε να προσθέσετε το JAR χειροκίνητα).

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις
Προσθέστε το GroupDocs.Search στο Maven `pom.xml` σας:

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

Για άμεσες λήψεις, αποκτήστε την πιο πρόσφατη έκδοση από [GroupDocs.Search για Java εκδόσεις](https://releases.groupdocs.com/search/java/).

### Ρύθμιση περιβάλλοντος
- Επαληθεύστε ότι το `JAVA_HOME` δείχνει σε συμβατό JDK.  
- Δημιουργήστε ένα νέο Maven project και επικολλήστε το παραπάνω απόσπασμα στην ενότητα `<dependencies>`.  
- Τοποθετήστε δείγμα αρχεία σε κατάλογο όπως `src/main/resources/documents/`.

## Πώς να ρυθμίσετε το GroupDocs.Search για Java
`Index` είναι η κεντρική κλάση που αντιπροσωπεύει μια αναζητήσιμη συλλογή αποθηκευμένη στο δίσκο.

Δημιουργήστε μια παρουσία `Index` που δείχνει σε φάκελο στο δίσκο, εφαρμόστε άδεια εάν έχετε μία, και προαιρετικά ρυθμίστε έναν αναλυτή για γλωσσο‑συγκεκριμένη τοκενοποίηση. Αυτό το βήμα προετοιμασίας διασφαλίζει ότι η μηχανή μπορεί να διαβάσει, να γράψει και να αναζητήσει το ευρετήριο αποδοτικά.

Η κλάση `Index` είναι το βασικό στοιχείο που αντιπροσωπεύει μια αναζητήσιμη συλλογή στο δίσκο. Αφού τη δημιουργήσετε, όλες οι λειτουργίες ευρετηρίασης και ερωτημάτων περνούν μέσω αυτού του αντικειμένου.

1. **Εγκατάσταση της βιβλιοθήκης** – Χρησιμοποιήστε το Maven απόσπασμα παραπάνω ή κατεβάστε το JAR από [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Απόκτηση άδειας** – Ξεκινήστε με άδεια δοκιμής· αντικαταστήστε την με κλειδί παραγωγής πριν την ανάπτυξη.  
3. **Αρχικοποίηση του ευρετηρίου** – Το παρακάτω απόσπασμα δείχνει πώς να δημιουργήσετε (ή ανοίξετε) έναν φάκελο ευρετηρίου:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Πώς να επισήμανση αποτελεσμάτων αναζήτησης Java – συγχρονισμένη ευρετηρίαση
`DocumentHighlighter` είναι μια βοηθητική κλάση που δημιουργεί επισημασμένα αποσπάσματα από τα αποτελέσματα αναζήτησης.

Φορτώστε το ευρετήριο, προσθέστε έγγραφα με `index.add(documentPath)`, εκτελέστε ένα ερώτημα, και στη συνέχεια καλέστε το `DocumentHighlighter` για να τυλίξετε τις αντιστοιχίες με ετικέτες `<mark>`. Η όλη διαδικασία εκτελείται στο νήμα που την καλεί, έτσι το έγγραφο γίνεται αναζητήσιμο αμέσως μετά την επιστροφή του `add` για τους τελικούς χρήστες.

### Βήμα 1: δημιουργία του ευρετηρίου και προσθήκη διαχείρισης σφαλμάτων
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Βήμα 2: προσθήκη εγγράφων και εκτέλεση αναζήτησης
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Βήμα 3: επεξεργασία αποτελεσμάτων και επισήμανση αποτελεσμάτων αναζήτησης Java
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## Πώς να επισήμανση αποτελεσμάτων αναζήτησης Java – ασύγχρονη ευρετηρίαση
`IndexingOptions` ρυθμίζει πώς εκτελείται η διαδικασία ευρετηρίασης, συμπεριλαμβανομένης της συγχρονισμένης ή ασύγχρονης λειτουργίας.

Ρυθμίστε το `IndexingOptions` για εκτέλεση σε λειτουργία παρασκηνίου, εγγραφείτε σε συμβάντα `StatusChanged`, και αφήστε τη μηχανή να ευρετηριάζει αρχεία ενώ το UI σας συνεχίζει να εξυπηρετεί άλλα αιτήματα. Μόλις η κατάσταση αλλάξει σε `Ready`, μπορείτε να εκτελέσετε αναζητήσεις και να λάβετε επισημασμένα αποσπάσματα όπως στη συγχρονισμένη λειτουργία.

Ο `AsyncIndexingListener` λαμβάνει ενημερώσεις προόδου, επιτρέποντάς σας να εμφανίσετε μπάρα προόδου ή να καταγράψετε την κατάσταση χωρίς να μπλοκάρετε το κύριο νήμα.

### Βήμα 1: ρύθμιση του ευρετηρίου με ακροατές συμβάντων
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Βήμα 2: ενεργοποίηση ασύγχρονης λειτουργίας και έναρξη ευρετηρίασης
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## Πώς να ευρετηριάσετε έγγραφα Java – πρακτικές συμβουλές
`index.update(path)` ενημερώνει ένα υπάρχον έγγραφο στο ευρετήριο με το αρχείο στο καθορισμένο μονοπάτι.

Διαιρέστε μεγάλες συλλογές σε παρτίδες των 1 000–5 000 αρχείων, φιλτράρετε κατά επέκταση για να αποφύγετε περιττή ανάλυση, και χρησιμοποιήστε το `index.update(path)` για αλλαγμένα αρχεία αντί να ξαναδημιουργήσετε ολόκληρο το ευρετήριο. Αυτές οι πρακτικές διατηρούν τη χρήση μνήμης χαμηλή και τον χρόνο ευρετηρίασης προβλέψιμο για διατήρηση συνέπειας.

- **Μέγεθος παρτίδας**: Για τεράστιες συλλογές, χωρίστε το φάκελο σε μικρότερες παρτίδες για να αποφύγετε αιχμές μνήμης.  
- **Φίλτρα αρχείων**: Χρησιμοποιήστε `IndexingOptions.setFileExtensions` για να συμπεριλάβετε μόνο τις μορφές που χρειάζεστε (π.χ., `.pdf`, `.docx`).  
- **Επαναευρετηρίαση**: Όταν ένα έγγραφο αλλάζει, καλέστε `index.update(documentPath)` αντί να δημιουργήσετε ξανά το ευρετήριο από την αρχή.

## Εξετάσεις απόδοσης
- **Μνήμη**: Παρακολουθήστε τη χρήση heap· αυξήστε το `-Xmx` εάν επεξεργάζεστε πολλά μεγάλα αρχεία ταυτόχρονα.  
- **CPU**: Η ασύγχρονη ευρετηρίαση διανέμει το φορτίο σε νήματα αλλά εξακολουθεί να καταναλώνει CPU—παρακολουθήστε τη χρήση με το JVisualVM.  
- **Επισήμανση αποτελεσμάτων**: Η επισήμανση προσθέτει ένα μικρό κόστος (≈ 2–5 ms ανά αποτέλεσμα). Αποθηκεύστε στην cache το παραγόμενο HTML εάν χρειάζεται να εμφανίζετε τα ίδια αποσπάσματα επανειλημμένα.

## Συχνές ερωτήσεις

**Ε: Μπορώ να συνδυάσω συγχρονισμένη και ασύγχρονη ευρετηρίαση στην ίδια εφαρμογή;**  
Α: Ναι. Χρησιμοποιήστε συγχρονισμένη ευρετηρίαση για μικρά, συχνά ενημερωμένα σύνολα και ασύγχρονη ευρετηρίαση για μαζικές εισαγωγές ή εργασίες παρασκηνίου.

**Ε: Πώς προσαρμόζω το στυλ της επισήμανσης;**  
Α: Παρέχετε μια προσαρμοσμένη υλοποίηση `DocumentHighlighter` που γράφει το επιθυμητό HTML, CSS ή XML γύρω από τους ταιριαστούς όρους.

**Ε: Ποιους τύπους αρχείων υποστηρίζει το GroupDocs.Search εξ'ορισμού;**  
Α: Κείμενο, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, και πολλά άλλα μέσω ενσωματωμένων αναλυτών—πάνω από 30 μορφές συνολικά.

**Ε: Είναι δυνατόν να αναζητήσετε σε πολλές γλώσσες ταυτόχρονα;**  
Α: Απόλυτα. Το GroupDocs.Search περιλαμβάνει πολυγλωσσικούς αναλυτές· απλώς ρυθμίστε τον κατάλληλο `Analyzer` κατά τη δημιουργία του ευρετηρίου.

**Ε: Πώς ασφαλίζω το φάκελο του ευρετηρίου;**  
Α: Αποθηκεύστε το ευρετήριο σε προστατευμένο κατάλογο, ορίστε αυστηρά δικαιώματα συστήματος αρχείων, και προαιρετικά κρυπτογραφήστε το ευρετήριο χρησιμοποιώντας τις λειτουργίες ασφαλείας της βιβλιοθήκης.

---

**Τελευταία ενημέρωση:** 2026-09-11  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να δημιουργήσετε ευρετήριο εγγράφων και να προσθέσετε έγγραφα χρησιμοποιώντας το GroupDocs.Search API για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Πώς να δημιουργήσετε αποθετήριο ευρετηρίου java με το GroupDocs.Search: Αποτελεσματική ευρετηρίαση & αναζήτηση εγγράφων](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [Αποτελεσματική ευρετηρίαση εγγράφων Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)