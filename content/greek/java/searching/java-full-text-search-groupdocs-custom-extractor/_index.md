---
date: '2026-08-05'
description: Μάθετε πώς να δημιουργήσετε έναν log file extractor για full-text search
  σε Java χρησιμοποιώντας το GroupDocs.Search. Προσθέστε έγγραφα στο index, βελτιστοποιήστε
  την απόδοση της αναζήτησης και διαχειριστείτε large log files αποδοτικά.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Το Full text search java tutorial δείχνει πώς να δημιουργήσετε έναν
  custom log file extractor χρησιμοποιώντας το GroupDocs.Search, να προσθέσετε έγγραφα
  στο index και να optimise την απόδοση της αναζήτησης για massive log archives.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Αναζήτηση πλήρους κειμένου java: log file extractor με GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Αναζήτηση πλήρους κειμένου java: log file extractor με GroupDocs'
type: docs
url: /el/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Αναζήτηση πλήρους κειμένου java: εξαγωγέας αρχείων καταγραφής με GroupDocs

Η αναζήτηση πλήρους κειμένου java είναι θεμέλιο για κάθε σύστημα που πρέπει να εντοπίζει γρήγορα πληροφορίες μέσα σε τεράστιες συλλογές εγγράφων. Σε αυτό το σεμινάριο θα μάθετε πώς να διαμορφώσετε το GroupDocs.Search, να δημιουργήσετε έναν προσαρμοσμένο εξαγωγέα αρχείων καταγραφής, να προσθέσετε έγγραφα στο ευρετήριο και να βελτιστοποιήσετε την απόδοση της αναζήτησης όταν εργάζεστε με γιγαμπάιτ δεδομένα καταγραφής.

## Τι θα μάθετε
- Ρυθμίστε και διαμορφώστε το GroupDocs.Search για Java.  
- Υλοποιήστε έναν **εξαγωγέα αρχείων καταγραφής** που αναλύει αρχεία κειμένου όπως χρειάζεστε.  
- **Προσθέστε έγγραφα στο ευρετήριο** μαζί με PDFs, DOCX και άλλες μορφές.  
- Πραγματικά σενάρια όπου ένας **εξαγωγέας αρχείων καταγραφής** προσθέτει μετρήσιμη αξία.  
- Αποδεδειγμένες συμβουλές για **βελτιστοποίηση της απόδοσης αναζήτησης** για αρχεία καταγραφής πολλαπλών γιγαμπάιτ.

## Γρήγορες απαντήσεις
- **Τι είναι ένας εξαγωγέας αρχείων καταγραφής;** Ένα προσαρμοσμένο στοιχείο που λέει στο GroupDocs.Search πώς να διαβάζει και να ευρετηριάζει αρχεία κειμένου καταγραφής.  
- **Γιατί να χρησιμοποιήσετε το GroupDocs.Search;** Υποστηρίζει την ευρετηρίαση πάνω από 50 μορφών, παρέχει αυτόματη επανευρετηρίαση και διαχειρίζεται ευρετήρια έως 10 GB με λιγότερο από 2 GB RAM.  
- **Χρειάζομαι άδεια;** Ναι – απαιτείται δοκιμαστική ή πλήρης άδεια για την ενεργοποίηση της βιβλιοθήκης.  
- **Μπορώ να ευρετηριάσω άλλους τύπους αρχείων ταυτόχρονα;** Απόλυτα· μπορείτε να συνδυάσετε PDFs, DOCX και προσαρμοσμένα αρχεία καταγραφής στο ίδιο ευρετήριο.  
- **Πώς να βελτιώσετε την απόδοση;** Χρησιμοποιήστε σταδιακή ευρετηρίαση, ρυθμίστε το `IndexSettings` και ενεργοποιήστε τη σημαία `autoReindex`.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε τα εξής:

### Απαιτούμενες βιβλιοθήκες
Προσθέστε την εξάρτηση GroupDocs.Search Maven στο `pom.xml` σας. Χρησιμοποιήστε την πιο πρόσφατη έκδοση που ταιριάζει με το επίπεδο Java του έργου σας.

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

### Ρύθμιση περιβάλλοντος
- JDK 8 ή νεότερο.  
- Εξοικείωση με τον προγραμματισμό Java και βασικές έννοιες διαχείρισης αρχείων.

### Απόκτηση άδειας
Ξεκινήστε κατεβάζοντας μια δωρεάν δοκιμαστική άδεια για να εξερευνήσετε τις δυνατότητες του GroupDocs.Search. Για παραγωγική χρήση, αγοράστε πλήρη άδεια ή ζητήστε προσωρινή μέσω [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## Ρύθμιση του GroupDocs.Search για Java

Για να ξεκινήσετε, αρχικοποιήστε τη βιβλιοθήκη και εφαρμόστε το αρχείο άδειας σας:

1. **Ρύθμιση Maven** – επιβεβαιώστε ότι η εξάρτηση από το προηγούμενο βήμα υπάρχει.  
2. **Αρχικοποίηση άδειας** – φορτώστε το αρχείο άδειας πριν από οποιαδήποτε άλλη κλήση API.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

Με το περιβάλλον έτοιμο, μπορείτε να προχωρήσετε στην κατασκευή του προσαρμοσμένου **εξαγωγέα αρχείων καταγραφής**.

## Τι είναι ένας εξαγωγέας αρχείων καταγραφής;

Ένας εξαγωγέας αρχείων καταγραφής είναι ένα κομμάτι κώδικα που λέει στο GroupDocs.Search πώς να διαβάζει ακατέργαστα αρχεία καταγραφής (συνήθως `.log`) και να μετατρέπει το περιεχόμενό τους σε κείμενο αναζητήσιμο. Παρέχοντας τον δικό σας εξαγωγέα αποκτάτε πλήρη έλεγχο των κανόνων ανάλυσης, του φιλτραρίσματος του θορύβου και της εξαγωγής μόνο των πληροφοριών που έχουν σημασία για την περίπτωση χρήσης της αναζήτησής σας.

## Δημιουργία εξαγωγέα αρχείων καταγραφής

Το GroupDocs.Search σας επιτρέπει να ενσωματώσετε προσαρμοσμένους εξαγωγείς κειμένου για οποιονδήποτε τύπο αρχείου. Ακολουθήστε αυτά τα βήματα για να δημιουργήσετε έναν για αρχεία καταγραφής.

### Βήμα 1: ορισμός του προσαρμοσμένου εξαγωγέα
`TextExtractorBase` είναι η αφηρημένη βασική κλάση που επεκτείνετε για να δημιουργήσετε έναν προσαρμοσμένο εξαγωγέα. Καθορίζει ποιες επεκτάσεις αρχείων υποστηρίζει ο εξαγωγέας και περιέχει τη βασική λογική εξαγωγής.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Βασικά σημεία**  
- `getFileExtensions()` καταχωρεί τον εξαγωγέα για αρχεία `.log`.  
- `extractText` είναι το σημείο όπου μπορείτε να αφαιρέσετε χρονικές σήμανση, να φιλτράρετε γραμμές εντοπισμού σφαλμάτων ή να εφαρμόσετε οποιαδήποτε προεπεξεργασία απαιτείται για **αναζήτηση μεγάλων αρχείων καταγραφής**.

### Βήμα 2: ρύθμιση των ρυθμίσεων ευρετηρίου με τον εξαγωγέα
Προσθέστε τον εξαγωγέα σας στο `IndexSettings` και ενεργοποιήστε το `autoReindex` ώστε τα νέα αρχεία καταγραφής να ευρετηριάζονται αυτόματα χωρίς χειροκίνητη παρέμβαση.

`IndexSettings` διαμορφώνει τη συμπεριφορά του ευρετηρίου όπως όρια μνήμης και προσαρμοσμένους εξαγωγείς.  
`autoReindex` ενημερώνει αυτόματα το ευρετήριο όταν τα πηγαία αρχεία αλλάζουν.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### Βήμα 3: προσθήκη εγγράφων στο ευρετήριο
Τώρα που το ευρετήριο αναγνωρίζει αρχεία καταγραφής, μπορείτε να **προσθέσετε έγγραφα στο ευρετήριο** όπως και με οποιαδήποτε άλλη υποστηριζόμενη μορφή.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### Βήμα 4: αναζήτηση στο ευρετήριο
Εκτελέστε ερωτήματα απλού κειμένου. Ο προσαρμοσμένος εξαγωγέας εγγυάται ότι κάθε καταχώρηση καταγραφής είναι αναζητήσιμη.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Συμβουλές για βελτιστοποίηση της απόδοσης αναζήτησης

- **Σταδιακή ευρετηρίαση** – προσθέστε μόνο νέα ή τροποποιημένα αρχεία καταγραφής αντί να ξαναχτίζετε ολόκληρο το ευρετήριο.  
- **Διαχείριση μνήμης** – η σημαία `autoReindex` διατηρεί τη χρήση RAM χαμηλή εκκενώνοντας ενδιάμενα δεδομένα στο δίσκο.  
- **Ρυθμίσεις ευρετηρίου** – προσαρμόστε το `setMaxMemoryUsage` ανάλογα με τη χωρητικότητα του διακομιστή σας· μια τυπική ρύθμιση είναι 1 GB για ευρετήριο 10 GB.  
- **Βελτιστοποίηση ερωτημάτων** – χρησιμοποιήστε ερωτήματα φράσεων, μπαλαντέρ ή φίλτρα για να περιορίσετε τα αποτελέσματα όταν αναζητάτε τεράστια αρχεία καταγραφής.

## Πρακτικές εφαρμογές

Το GroupDocs.Search μπορεί να εφαρμοστεί σε πολλές πραγματικές περιπτώσεις, όπως:

- **Διαχείριση καταγραφών** – εντοπίστε μηνύματα σφάλματος, ενέργειες χρηστών ή συγκεκριμένες χρονικές σήμανση σε γιγαμπάιτ δεδομένων καταγραφής σε δευτερόλεπτα.  
- **Συστήματα ανάκτησης εγγράφων** – διατηρήστε ένα ενιαίο αναζητήσιμο αποθετήριο που περιλαμβάνει PDFs, έγγραφα Word, λογιστικά φύλλα και προσαρμοσμένα αρχεία καταγραφής.  
- **Ανάλυση περιεχομένου** – εκτελέστε αναφορές συχνότητας λέξεων-κλειδιών ή εντοπίστε ανωμαλίες σε ροές δεδομένων καταγραφής.

## Σκέψεις για την απόδοση

Κατά την ανάπτυξη του GroupDocs.Search σε μεγάλη κλίμακα, κρατήστε αυτές τις βέλτιστες πρακτικές στο μυαλό:

- Αποθηκεύστε τα ευρετήρια σε γρήγορα SSD για ελαχιστοποίηση του λανθάνοντος χρόνου ανάγνωσης/εγγραφής.  
- Παρακολουθείτε τη χρήση heap της JVM· σκεφτείτε την εκφόρτωση μεγάλων ευρετηρίων σε ξεχωριστή διεργασία αν η μνήμη γίνει περιοριστικός παράγοντας.  
- Ενεργοποιήστε το `autoReindex` (όπως φαίνεται) για να διατηρείτε το ευρετήριο ενημερωμένο χωρίς χειροκίνητη επαναδημιουργία.

## Συμπέρασμα

Μέχρι τώρα έχετε δημιουργήσει έναν **εξαγωγέα αρχείων καταγραφής**, έχετε μάθει πώς να **προσθέτετε έγγραφα στο ευρετήριο** και έχετε ανακαλύψει τρόπους **βελτιστοποίησης της απόδοσης αναζήτησης** για μεγάλα αρχεία καταγραφής. Αυτός ο συνδυασμός επιτρέπει στις εφαρμογές Java σας να παρέχουν γρήγορη, ακριβή αναζήτηση πλήρους κειμένου σε οποιονδήποτε τύπο εγγράφου.

Για πιο βαθιά εξερεύνηση, δείτε την επίσημη [GroupDocs documentation](https://docs.groupdocs.com/search/java/) ή πειραματιστείτε με διαφορετικές υλοποιήσεις εξαγωγέων για να ταιριάζουν στην μοναδική σας περίπτωση χρήσης.

## Ενότητα Συχνών Ερωτήσεων
1. **Ποιοι τύποι αρχείων μπορώ να ευρετηριάσω χρησιμοποιώντας το GroupDocs.Search;**  
   - Μπορείτε να ευρετηριάσετε PDFs, έγγραφα Word, λογιστικά φύλλα και πολλές άλλες μορφές, καθώς και προσαρμοσμένα αρχεία καταγραφής μέσω εξαγωγέων κειμένου.  
2. **Πώς να διαχειριστώ μεγάλες συλλογές εγγράφων αποδοτικά;**  
   - Χρησιμοποιήστε σταδιακές ενημερώσεις, κατατμήστε τα ευρετήρια και ρυθμίστε το `IndexSettings` για αποτελεσματική διαχείριση πόρων.  
3. **Μπορεί το GroupDocs.Search να ενσωματωθεί με άλλα συστήματα;**  
   - Ναι, προσφέρει ένα καθαρό Java API που μπορεί να ενσωματωθεί σε υπάρχουσες υπηρεσίες, μικρο‑υπηρεσίες ή web εφαρμογές.  
4. **Τι είναι μια προσωρινή άδεια και πώς μπορώ να αποκτήσω μία;**  
   - Μια προσωρινή άδεια παρέχει πλήρη λειτουργικότητα για αξιολόγηση χωρίς χρονικούς περιορισμούς. Αιτηθείτε μέσω [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## Συχνές ερωτήσεις

**Q: Πώς διαφέρει ένας εξαγωγέας αρχείων καταγραφής από τον προεπιλεγμένο εξαγωγέα;**  
A: Ο προεπιλεγμένος εξαγωγέας διαχειρίζεται κοινές μορφές (PDF, DOCX κλπ.). Ένας προσαρμοσμένος εξαγωγέας αρχείων καταγραφής σας επιτρέπει να ορίσετε ακριβώς πώς θα αναλύονται και θα ευρετηριάζονται οι καταχωρήσεις κειμένου καταγραφής.

**Q: Μπορώ να ευρετηριάσω συμπιεσμένα αρχεία καταγραφής (π.χ., .zip);**  
A: Ναι, προσθέτοντας ένα βήμα προεπεξεργασίας που εξάγει τα αρχεία από το συμπιεσμένο αρχείο πριν τα περάσετε στο ευρετήριο.

**Q: Ποιος είναι ο καλύτερος τρόπος να διατηρείται το ευρετήριο ενημερωμένο με συνεχώς δημιουργούμενες καταγραφές;**  
A: Ενεργοποιήστε το `autoReindex` και προγραμματίστε έναν παρακολουθητή στο παρασκήνιο που καλεί `index.add(newLogFile)` κάθε φορά που εμφανίζεται νέο αρχείο.

**Q: Υπάρχει όριο στο μέγεθος ενός μεμονωμένου αρχείου καταγραφής που μπορεί να ευρετηριαστεί;**  
A: Στην πράξη, το όριο εξαρτάται από τη διαθέσιμη μνήμη. Συνιστάται η διαίρεση πολύ μεγάλων αρχείων καταγραφής σε μικρότερα τμήματα πριν την ευρετηρίαση.

**Q: Υποστηρίζει το GroupDocs.Search αναζητήσεις fuzzy ή με μπαλαντέρ;**  
A: Ναι, το API αναζήτησης περιλαμβάνει fuzzy matching, μπαλαντέρ και ερωτήματα εγγύτητας για βελτίωση της σχετικότητας των αποτελεσμάτων.

---

**Τελευταία ενημέρωση:** 2026-08-05  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Αναζήτηση πλήρους κειμένου Java: Δημιουργία ευρετηρίου με GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με GroupDocs.Search για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Βελτίωση απόδοσης ερωτημάτων με GroupDocs.Search Java: Βελτιστοποίηση ευρετηρίου & αναζήτησης](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)