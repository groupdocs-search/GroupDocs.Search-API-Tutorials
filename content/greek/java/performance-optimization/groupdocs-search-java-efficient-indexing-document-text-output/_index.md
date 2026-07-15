---
date: '2026-06-27'
description: Οδηγός βήμα‑βήμα για το πώς να δημιουργήσετε ευρετήριο, να εξάγετε κείμενο
  από έγγραφα και να εξάγετε κείμενο σε αρχείο χρησιμοποιώντας το GroupDocs.Search
  for Java – τη γρήγορη βιβλιοθήκη αναζήτησης java.
keywords:
- how to create index
- extract text from documents
- output text to file
- add documents to index
- extract text to string
schemas:
- author: GroupDocs
  dateModified: '2026-06-27'
  description: Step‑by‑step guide on how to create index, extract text from documents
    and output text to file using GroupDocs.Search for Java – the fast java search
    library.
  headline: How to create index java with GroupDocs.Search for Java
  type: TechArticle
- questions:
  - answer: Yes, the library is pure Java and works seamlessly with any JVM language.
    question: Can I use GroupDocs.Search with other JVM languages like Kotlin or Scala?
  - answer: High compression reduces disk usage by up to 70 % and adds only a minimal
      CPU overhead during indexing; query latency remains under 100 ms for typical
      workloads.
    question: How does compression affect search speed?
  - answer: Absolutely. Use `index.add()` for new files and `index.remove()` to delete
      outdated ones, allowing incremental updates.
    question: Is it possible to update an existing index without rebuilding it?
  - answer: The `PlainText` result from the **structured text extraction** adapter
      provides clean, language‑agnostic content ideal for NLP tasks.
    question: Which output format is best for natural‑language‑processing pipelines?
  - answer: A free trial license suffices for development and evaluation; production
      deployments require a purchased license.
    question: Do I need a license for development and testing?
  type: FAQPage
title: Πώς να δημιουργήσετε ευρετήριο java με GroupDocs.Search for Java
type: docs
url: /el/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# Κατακτώντας την Αποτελεσματική Αναζήτηση Εγγράφων με το GroupDocs.Search για Java

Η εύρεση του σωστού αποσπάσματος μέσα σε χιλιάδες PDF, αρχεία Word ή λογιστικά φύλλα μπορεί να μοιάζει με την αναζήτηση μιας βελόνας σε άχυρο. **How to create index** γρήγορα και η ανάκτηση εκείνης της βελόνας είναι αυτό που κάνει μια λύση αναζήτησης εγγράφων πολύτιμη. Σε αυτό το tutorial θα μάθετε πώς να χρησιμοποιήσετε το **GroupDocs.Search for Java**, μια υψηλών επιδόσεων java search library, για **create index**, **add documents to index**, και **extract text from documents** σε πολλαπλές μορφές όπως αρχεία, ροές, συμβολοσειρές και δομημένα δεδομένα. Στο τέλος θα έχετε μια pipeline δημιουργίας ευρετηρίου έτοιμη για παραγωγή που κλιμακώνεται σε μεγάλες συλλογές εγγράφων ενώ διατηρεί τη χρήση μνήμης χαμηλή.

## Γρήγορες Απαντήσεις
- **Ποιος είναι ο κύριος σκοπός;** Για **how to create index** και άμεση ανάκτηση του περιεχομένου του εγγράφου.  
- **Ποια βιβλιοθήκη πρέπει να χρησιμοποιήσω;** The **GroupDocs.Search for Java** **java search library**.  
- **Μπορώ να εξάγω κείμενο σε αρχείο;** Ναι – η βιβλιοθήκη παρέχει **output text to file** adapters για HTML, plain text, και άλλα.  
- **Υποστηρίζεται η δομημένη εξαγωγή;** Απόλυτα – χρησιμοποιήστε τον **structured text extraction** adapter για να λάβετε δεδομένα επιπέδου πεδίου.  
- **Χρειάζομαι άδεια;** Μια δοκιμαστική άδεια λειτουργεί για ανάπτυξη· απαιτείται μόνιμη άδεια για παραγωγικές εγκαταστάσεις.

## Τι Θα Μάθετε
- Πώς να **how to create index** και **add documents to index** χρησιμοποιώντας το GroupDocs.Search for Java.  
- Τεχνικές για **output text to file**, streams, strings, και δομημένες μορφές.  
- Συμβουλές βελτιστοποίησης απόδοσης που διατηρούν το ευρετήριο γρήγορο και αποδοτικό σε μνήμη.  
- Πραγματικά σενάρια όπου αυτές οι δυνατότητες ξεχωρίζουν, όπως αποθετήρια νομικών συμβάσεων και αρχεία ακαδημαϊκών εργασιών.

## Γιατί να Χρησιμοποιήσετε το GroupDocs.Search για Java
Το GroupDocs.Search υποστηρίζει **50+ input and output formats** – συμπεριλαμβανομένων των DOCX, XLSX, PPTX, PDF, HTML και κοινών τύπων εικόνων – και μπορεί να ευρετηριάσει αρχεία πολλαπλών gigabyte χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Τα benchmarks δείχνουν ότι μια συλλογή εγγράφων 1 GB μπορεί να ευρετηριαστεί σε λιγότερο από 2 λεπτά σε έναν τυπικό διακομιστή 8‑πυρήνων, ενώ τα ερωτήματα αναζήτησης επιστρέφουν αποτελέσματα σε λιγότερο από 100 ms.

## Προαπαιτούμενα
- **Java Development Kit (JDK)** 8 ή νεότερο.  
- **GroupDocs.Search for Java** library (trial ή licensed).  
- **Maven** για διαχείριση εξαρτήσεων.  
- Βασικές γνώσεις Java I/O.

## Ρύθμιση του GroupDocs.Search για Java
Αρχικά, προσθέστε το αποθετήριο Maven του GroupDocs.Search και την εξάρτηση στο `pom.xml` του έργου σας. Αυτό το βήμα εξασφαλίζει ότι η βιβλιοθήκη είναι διαθέσιμη στο classpath.

**Maven Setup**  
Προσθέστε τις παρακάτω ρυθμίσεις αποθετηρίου και εξαρτήσεων στο αρχείο `pom.xml` σας:

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

Για όσους προτιμούν άμεση λήψη, μπορείτε να αποκτήσετε την τελευταία έκδοση από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License Acquisition**  
Για να χρησιμοποιήσετε το GroupDocs.Search σε παραγωγή, αποκτήστε δοκιμαστική ή μόνιμη άδεια από τον επίσημο ιστότοπο. Η δοκιμαστική άδεια δεν έχει περιορισμούς για ανάπτυξη και δοκιμές.

## Πώς να δημιουργήσετε ευρετήριο java με προσαρμοσμένες ρυθμίσεις
`Index` είναι η βασική κλάση που αντιπροσωπεύει μια συλλογή εγγράφων με δυνατότητα αναζήτησης.  
`IndexSettings` διαμορφώνει επιλογές όπως η συμπίεση για το ευρετήριο.  
`CompressionLevel` ορίζει το επίπεδο συμπίεσης που εφαρμόζεται στο αποθηκευμένο κείμενο.

Φορτώστε το αντικείμενο `Index` με ενεργοποιημένη τη συμπίεση, δείξτε το σε έναν φάκελο και προσθέστε όλα τα υποστηριζόμενα αρχεία. Αυτή η παράγραφος απάντησης σας λέει ακριβώς τι να κάνετε: δημιουργήστε ένα `Index` με `new Index("indexFolder", new IndexSettings().setCompressionLevel(CompressionLevel.High))`, στη συνέχεια καλέστε `index.add("documentsFolder", true)` για να ευρετηριάσετε αναδρομικά κάθε υποστηριζόμενο αρχείο. Η λειτουργία υψηλής συμπίεσης μειώνει το μέγεθος στο δίσκο έως και 70 % ενώ διατηρεί την ταχύτητα αναζήτησης υψηλή.

Η δημιουργία του ευρετηρίου είναι η βάση για οποιαδήποτε εφαρμογή που βασίζεται στην αναζήτηση. Το παρακάτω παράδειγμα σας καθοδηγεί στη διαδικασία, εξηγεί κάθε ρύθμιση και δείχνει πώς να επαληθεύσετε ότι το ευρετήριο δημιουργήθηκε επιτυχώς.

### Δημιουργία Ευρετηρίου και Ευρετηρίαση Εγγράφων

#### Επισκόπηση
Η κλάση `Index` είναι το βασικό συστατικό που αντιπροσωπεύει μια συλλογή εγγράφων με δυνατότητα αναζήτησης. Αποθηκεύει ανεστραμμένα ευρετήρια, λεξικά όρων και μεταδεδομένα που απαιτούνται για γρήγορες αναζητήσεις.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**Εξήγηση**  
- **Index Settings**: Ενεργοποιούμε **high compression** για την αποθήκευση κειμένου, βελτιστοποιώντας τη χρήση του χώρου στο δίσκο χωρίς να επηρεάζουμε την ταχύτητα ερωτημάτων.  
- **Adding Documents**: Η μέθοδος `index.add()` **adds documents to index**, σαρώνοντας τον φάκελο αναδρομικά και διαχειριζόμενη αυτόματα όλες τις υποστηριζόμενες μορφές.

## Πώς να εξάγετε κείμενο σε αρχείο, ροή, συμβολοσειρά και δομημένες μορφές
Μετά την ευρετηρίαση, συχνά χρειάζεται να εξάγετε το ακατέργαστο ή μορφοποιημένο κείμενο ενός εγγράφου. Το GroupDocs.Search προσφέρει τέσσερις adapters που σας επιτρέπουν να γράψετε το εξαγόμενο περιεχόμενο σε αρχείο, σε ροή μνήμης, σε Java `String`, ή σε δομημένο μοντέλο αντικειμένου.

### Εξαγωγή Κειμένου Εγγράφου σε Αρχείο

`FileOutputAdapter` γράφει το εξαγόμενο κείμενο του εγγράφου σε αρχείο στην επιλεγμένη μορφή.

#### Επισκόπηση
Το `FileOutputAdapter` γράφει το εξαγόμενο κείμενο στην επιλεγμένη μορφή (HTML, plain text κ.λπ.) απευθείας σε αρχείο στο δίσκο. Αυτό είναι χρήσιμο για τη δημιουργία αναφορών ευανάγνωστων από άνθρωπο ή για την τροφοδοσία επεξεργαστικών pipelines.

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**Εξήγηση**  
- **FileOutputAdapter**: Μετατρέπει το κείμενο του ευρετηριασμένου εγγράφου σε HTML και το γράφει στη συγκεκριμένη διαδρομή αρχείου, διατηρώντας βασική μορφοποίηση όπως επικεφαλίδες και πίνακες.

### Εξαγωγή Κειμένου Εγγράφου σε Ροή

`StreamOutputAdapter` ροή εξαγόμενου κειμένου εγγράφου σε `ByteArrayOutputStream` χωρίς δημιουργία προσωρινού αρχείου.

#### Επισκόπηση
Όταν χρειάζεστε το περιεχόμενο μόνο προσωρινά—π.χ., για αποστολή μέσω HTTP ή ενσωμάτωση σε απάντηση web—χρησιμοποιήστε το `StreamOutputAdapter`. Ροή το κείμενο σε `ByteArrayOutputStream`, αποφεύγοντας το κόστος δημιουργίας προσωρινού αρχείου.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**Εξήγηση**  
- **StreamOutputAdapter**: Ροή του κειμένου του εγγράφου σε `ByteArrayOutputStream`, επιτρέποντας ευέλικτη διαχείριση χωρίς επαφή με το σύστημα αρχείων.

### Εξαγωγή Κειμένου Εγγράφου σε Συμβολοσειρά

`StringOutputAdapter` καταγράφει ολόκληρο το κείμενο του εγγράφου σε ένα μοναδικό αντικείμενο `String`.

#### Επισκόπηση
Για γρήγορη καταγραφή, αποσφαλμάτωση ή εμφάνιση UI, το `StringOutputAdapter` καταγράφει ολόκληρο το κείμενο του εγγράφου σε ένα μοναδικό αντικείμενο `String`.

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**Εξήγηση**  
- **StringOutputAdapter**: Καταγράφει το κείμενο του εγγράφου σε `String`, καθιστώντας το εύκολο για ενσωμάτωση σε logs, έξοδο κονσόλας ή UI components.

### Εξαγωγή Κειμένου Εγγράφου σε Δομημένη Μορφή

`StructuredOutputAdapter` επιστρέφει ένα πλούσιο μοντέλο αντικειμένου που περιέχει παραγράφους, πίνακες και προσαρμοσμένα μεταδεδομένα.

#### Επισκόπηση
Το `StructuredOutputAdapter` επιστρέφει ένα πλούσιο μοντέλο αντικειμένου που περιέχει παραγράφους, πίνακες και προσαρμοσμένα μεταδεδομένα. Αυτή η μορφή είναι ιδανική για downstream natural‑language‑processing (NLP) ή ροές εργασίας εξαγωγής δεδομένων.

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**Εξήγηση**  
- **StructuredOutputAdapter**: Εξάγει το κείμενο του εγγράφου σε μορφή **structured text extraction**, επιτρέποντας λεπτομερή ανάλυση, εξαγωγή πεδίων και ενσωμάτωση σε pipelines μηχανικής μάθησης.

## Συνηθισμένα Προβλήματα και Λύσεις
| Issue | Cause | Fix |
|-------|-------|-----|
| **Δεν δημιουργήθηκε το ευρετήριο** | Λάθος διαδρομή φακέλου ή έλλειψη δικαιωμάτων εγγραφής | Επαληθεύστε ότι το `indexFolder` υπάρχει και η εφαρμογή έχει δικαίωμα εγγραφής |
| **Δεν επιστράφηκαν έγγραφα** | `index.add()` δεν κλήθηκε ή λανθασμένος φάκελος προέλευσης | Βεβαιωθείτε ότι το `documentsFolder` δείχνει στον σωστό κατάλογο και περιέχει υποστηριζόμενους τύπους αρχείων |
| **Το αρχείο εξόδου είναι κενό** | Μη έγκυρη διαδρομή adapter εξόδου ή λείπουν κατάλογοι | Δημιουργήστε τον προορισμό (`YOUR_OUTPUT_DIRECTORY`) πριν την εκτέλεση |
| **Αιχμές μνήμης με μεγάλα αρχεία** | Φόρτωση ολόκληρου αρχείου στη μνήμη | Χρησιμοποιήστε `StreamOutputAdapter` για επεξεργασία δεδομένων σταδιακά |

## Συχνές Ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs.Search με άλλες γλώσσες JVM όπως Kotlin ή Scala;**  
A: Ναι, η βιβλιοθήκη είναι καθαρή Java και λειτουργεί άψογα με οποιαδήποτε γλώσσα JVM.

**Q: Πώς η συμπίεση επηρεάζει την ταχύτητα αναζήτησης;**  
A: Η υψηλή συμπίεση μειώνει τη χρήση δίσκου έως και 70 % και προσθέτει μόνο ελάχιστο φόρτο CPU κατά την ευρετηρίαση· η καθυστέρηση ερωτημάτων παραμένει κάτω από 100 ms για τυπικά φορτία εργασίας.

**Q: Είναι δυνατόν να ενημερώσετε ένα υπάρχον ευρετήριο χωρίς επαναδημιουργία;**  
A: Απόλυτα. Χρησιμοποιήστε `index.add()` για νέα αρχεία και `index.remove()` για διαγραφή παλαιών, επιτρέποντας σταδιακές ενημερώσεις.

**Q: Ποια μορφή εξόδου είναι η καλύτερη για pipelines επεξεργασίας φυσικής γλώσσας (NLP);**  
A: Το αποτέλεσμα `PlainText` από τον **structured text extraction** adapter παρέχει καθαρό, γλωσσικά ανεξάρτητο περιεχόμενο ιδανικό για εργασίες NLP.

**Q: Χρειάζομαι άδεια για ανάπτυξη και δοκιμές;**  
A: Μια δωρεάν δοκιμαστική άδεια αρκεί για ανάπτυξη και αξιολόγηση· οι παραγωγικές εγκαταστάσεις απαιτούν αγορασμένη άδεια.

## Συμπέρασμα
Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή ροή εργασίας για **how to create index**, προσθήκη εγγράφων και εξαγωγή του κειμένου τους σε κάθε μορφή που μπορεί να χρειαστείτε. Ξεκινήστε διαμορφώνοντας το `Index` με συμπίεση, προσθέστε τη συλλογή εγγράφων σας και επιλέξτε τον κατάλληλο adapter εξόδου για το downstream σενάριό σας—είτε πρόκειται για δημιουργία αναφορών HTML, τροφοδοσία μοντέλου NLP, ή ροή περιεχομένου σε web client. Πειραματιστείτε με τα APIs σταδιακής ενημέρωσης για να διατηρείτε το ευρετήριο φρέσκο χωρίς δαπανηρές επαναδημιουργίες, και θα απολαμβάνετε γρήγορη, αξιόπιστη αναζήτηση σε οποιοδήποτε αποθετήριο εγγράφων.

---

**Τελευταία Ενημέρωση:** 2026-06-27  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Σχετικά Μαθήματα

- [Προσθήκη Εγγράφων στο Ευρετήριο – Οδηγός GroupDocs.Search Java](/search/java/advanced-features/)
- [Δημιουργία Ευρετηρίου Εγγράφου με το GroupDocs.Search για Java](/search/java/advanced-features/groupdocs-search-java-implementation-guide/)
- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με Metadata Indexing σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)