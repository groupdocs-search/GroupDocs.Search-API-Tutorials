---
date: '2026-10-22'
description: Μάθετε πώς να εκτελείτε αναζήτηση metadata με το GroupDocs σε Java, να
  ρυθμίζετε τις ρυθμίσεις index settings, να προσθέτετε documents και να κάνετε query
  στα metadata fields αποδοτικά.
keywords:
- metadata search with groupdocs
- metadata indexing java
- groupdocs search java
lastmod: '2026-10-22'
og_description: Μάθετε πώς να εκτελείτε αναζήτηση metadata με το GroupDocs σε Java,
  να ρυθμίζετε τις ρυθμίσεις index settings, να προσθέτετε documents και να κάνετε
  query στα metadata fields αποδοτικά.
og_image_alt: Guide showing Java code for metadata indexing using GroupDocs.Search
og_title: Πώς να κάνετε αναζήτηση metadata με το GroupDocs σε Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-22'
  description: Learn how to perform metadata search with GroupDocs in Java, configure
    index settings, add documents, and query by metadata fields efficiently.
  headline: How to do metadata search with GroupDocs in Java
  type: TechArticle
- description: Learn how to perform metadata search with GroupDocs in Java, configure
    index settings, add documents, and query by metadata fields efficiently.
  name: How to do metadata search with GroupDocs in Java
  steps:
  - name: Visit the GroupDocs website and go to the **Purchase** section.
    text: Visit the GroupDocs website and go to the **Purchase** section.
  - name: Choose a **temporary license** plan that matches your evaluation needs.
    text: Choose a **temporary license** plan that matches your evaluation needs.
  - name: '**Enterprise document management:** Retrieve contracts by contract date
      or signatory name.'
    text: '**Enterprise document management:** Retrieve contracts by contract date
      or signatory name.'
  - name: '**Digital library catalogs:** Let users browse books by genre, publication
      year, or author.'
    text: '**Digital library catalogs:** Let users browse books by genre, publication
      year, or author.'
  - name: '**CRM systems:** Quickly locate client files using custom metadata like
      customer ID or region.'
    text: '**CRM systems:** Quickly locate client files using custom metadata like
      customer ID or region.'
  type: HowTo
- questions:
  - answer: Metadata indexing stores document attributes (author, title, custom tags)
      in a searchable structure, enabling fast look‑ups without scanning full text.
    question: What is metadata indexing?
  - answer: Visit the GroupDocs purchase page and follow the steps to acquire a trial
      license.
    question: How do I obtain a temporary license?
  - answer: Yes, GroupDocs.Search supports PDF, DOCX, PPT, and many other formats.
    question: Can I index PDFs with this setup?
  - answer: Verify correct file paths and ensure the application has read permissions
      for the directories.
    question: What are common issues when adding documents?
  - answer: Regularly update your index, use incremental adds, and tune JVM memory
      settings.
    question: How do I optimize search performance?
  type: FAQPage
tags:
- metadata search
- GroupDocs
- Java indexing
title: Πώς να κάνετε αναζήτηση metadata με το GroupDocs σε Java
type: docs
url: /el/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Πώς να κάνετε αναζήτηση μεταδεδομένων με το GroupDocs σε Java

Η γρήγορη και αξιόπιστη προσθήκη εγγράφων σε ένα ευρετήριο αποτελεί τη ραχοκοκαλιά κάθε σύγχρονης εφαρμογής που βασίζεται στην αναζήτηση. Είτε δημιουργείτε ένα νομικό αποθετήριο, μια βάση γνώσεων για την εξυπηρέτηση πελατών ή μια εσωτερική πύλη εγγράφων, **metadata search with GroupDocs** σας επιτρέπει να εντοπίζετε αρχεία με βάση τον συγγραφέα, τον τίτλο ή οποιαδήποτε προσαρμοσμένη ετικέτα χωρίς να σαρώσετε το πλήρες κείμενο. Σε αυτό το tutorial θα μάθετε πώς να διαμορφώσετε τις ρυθμίσεις του ευρετηρίου, να δημιουργήσετε ένα ευρετήριο προσανατολισμένο στα μεταδεδομένα, να προσθέσετε τα αρχεία σας και να εκτελέσετε ακριβείς αναζητήσεις — όλα με το GroupDocs.Search for Java.

## Γρήγορες απαντήσεις
- **Ποιος είναι ο κύριος σκοπός της ευρετηρίασης μεταδεδομένων;** Επιτρέπει γρήγορες αναζητήσεις βασισμένες στις ιδιότητες του εγγράφου αντί στο πλήρες κείμενο.  
- **Ποια μέθοδος προσθέτει αρχεία στο ευρετήριο;** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Μπορώ να κάνω αναζήτηση με προσαρμοσμένα πεδία μεταδεδομένων;** Ναι, μόλις τα πεδία ευρετηριαστούν μπορείτε να τα ερωτήσετε απευθείας.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια προσωρινή δοκιμαστική άδεια είναι επαρκής για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγή.  
- **Ποια έκδοση Java απαιτείται;** Συνιστάται JDK 8 ή νεότερο.  

## Τι είναι η ευρετηρίαση μεταδεδομένων στο GroupDocs.Search;
Η ευρετηρίαση μεταδεδομένων εξάγει και αποθηκεύει τα χαρακτηριστικά του εγγράφου (π.χ., συγγραφέας, ημερομηνία δημιουργίας, προσαρμοσμένες ετικέτες) σε μια δομή αναζήτησης. Όταν **προσθέτετε έγγραφα στο ευρετήριο**, η μηχανή καταγράφει αυτά τα χαρακτηριστικά, επιτρέποντάς σας να εκτελείτε ακριβείς ερωτήματα όπως “βρείτε όλα τα PDF που έχουν δημιουργηθεί από *John Doe*” ή “search pdf by author”.  

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για ευρετηρίαση μεταδεδομένων;
Η αναζήτηση μεταδεδομένων με το GroupDocs παρέχει ελαφριά, υποδευτερόλεπτη απόκριση ακόμη και όταν το ευρετήριο περιέχει εκατομμύρια εγγραφές. Υποστηρίζει **πάνω από 30 μορφές εισόδου και εξόδου** — συμπεριλαμβανομένων PDF, DOCX, PPTX, HTML και αρχείων εικόνας — και καταναλώνει λιγότερο από 200 MB μνήμης heap για ένα ευρετήριο 100 000 εγγράφων σε έναν τυπικό διακομιστή.  

## Προαπαιτούμενα
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 ή νεότερο εγκατεστημένο και διαμορφωμένο.  
- Βασική εξοικείωση με Java και Maven.  

## Ρύθμιση του GroupDocs.Search για Java

### Οδηγίες εγκατάστασης
Προσθέστε το αποθετήριο GroupDocs και την εξάρτηση στο `pom.xml` σας:

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

Μπορείτε επίσης να κατεβάσετε τα πιο πρόσφατα binaries απευθείας από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση άδειας
Για να αποκτήσετε μια προσωρινή άδεια για δοκιμή:

1. Επισκεφθείτε την ιστοσελίδα GroupDocs και μεταβείτε στην ενότητα **Purchase**.  
2. Επιλέξτε ένα πρόγραμμα **temporary license** που ταιριάζει στις ανάγκες αξιολόγησής σας.  

## Πώς να διαμορφώσετε τις ρυθμίσεις ευρετηρίου για μεταδεδομένα;
Η διαμόρφωση των ρυθμίσεων ευρετηρίου ενημερώνει τη μηχανή ποια πληροφορία να εξάγει και να αποθηκεύσει. Ορίζοντας τον τύπο ευρετηρίου σε `MetadataIndex`, υποδεικνύετε στο GroupDocs.Search να εστιάσει στα πεδία μεταδεδομένων αντί στο πλήρες κείμενο, μειώνοντας το μέγεθος του ευρετηρίου και επιταχύνοντας τα ερωτήματα. Αυτή η διαμόρφωση εφαρμόζεται μέσω του αντικειμένου `IndexSettings`, όπου μπορείτε επίσης να καθορίσετε προσαρμοσμένα πεδία μεταδεδομένων προς ευρετηρίαση.

```text
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);
```

## Χαρακτηριστικό 1: διαμόρφωση ρυθμίσεων ευρετηρίου
Η κλήση `setIndexType(IndexType.MetadataIndex)` ενημερώνει τη μηχανή να εστιάσει στα μεταδεδομένα αντί στο πλήρες κείμενο. **`IndexType.MetadataIndex`** είναι μια τιμή απαρίθμησης που επιλέγει τη λειτουργία ευρετηρίασης μόνο μεταδεδομένων.

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

## Χαρακτηριστικό 2: δημιουργία ευρετηρίου σε καθορισμένο φάκελο
Δημιουργήστε έναν φυσικό κατάλογο ευρετηρίου όπου θα αποθηκευτούν όλα τα μεταδεδομένα:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Αντικαταστήστε το `YOUR_DOCUMENT_DIRECTORY` με τη διαδρομή που ταιριάζει στη διάταξη του έργου σας.

## Χαρακτηριστικό 3: Πώς να προσθέσετε έγγραφα στο ευρετήριο
Η μέθοδος `index.add` προσθέτει αρχεία από έναν φάκελο στο ευρετήριο και εξάγει τα μεταδεδομένα τους. **`index.add`** σαρώει κάθε έγγραφο, διαβάζει τα υποστηριζόμενα πεδία μεταδεδομένων και τα αποθηκεύει στο ευρετήριο για γρήγορη ανάκτηση.

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Συμβουλές:**  
- Επαληθεύστε ότι η διαδρομή του φακέλου είναι σωστή και ότι η εφαρμογή έχει δικαιώματα ανάγνωσης.  
- Το GroupDocs.Search εξάγει αυτόματα τα υποστηριζόμενα μεταδεδομένα από κάθε αρχείο.

## Χαρακτηριστικό 4: Αναζήτηση εγγράφων με βάση τα μεταδεδομένα
Εκτελέστε ένα ερώτημα που στοχεύει στα πεδία μεταδεδομένων, για παράδειγμα αναζητώντας έγγραφα όπου η γλώσσα είναι Αγγλικά:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

Η μέθοδος `search(query)` εξετάζει τα ευρετηριασμένα μεταδεδομένα και επιστρέφει τα ταιριαστά έγγραφα. Μπορείτε επίσης να **search pdf by author** χρησιμοποιώντας το όνομα του συγγραφέα ως συμβολοσειρά ερωτήματος.

## Πρακτικές εφαρμογές
1. **Enterprise document management:** Ανάκτηση συμβάσεων με βάση την ημερομηνία σύμβασης ή το όνομα του υπογράφοντα.  
2. **Digital library catalogs:** Επιτρέψτε στους χρήστες να περιηγούνται σε βιβλία κατά είδος, έτος έκδοσης ή συγγραφέα.  
3. **CRM systems:** Εντοπίστε γρήγορα αρχεία πελατών χρησιμοποιώντας προσαρμοσμένα μεταδεδομένα όπως αναγνωριστικό πελάτη ή περιοχή.  

## Συμβουλές και βέλτιστες πρακτικές
- **Incremental updates:** Χρησιμοποιήστε `index.addOrUpdate()` για νέα ή τροποποιημένα αρχεία αντί για επαναδημιουργία ολόκληρου του ευρετηρίου.  
- **Batch processing:** Όταν διαχειρίζεστε χιλιάδες αρχεία, προσθέστε τα σε μικρότερες παρτίδες για να διατηρήσετε τη χρήση μνήμης χαμηλή.  
- **Metadata validation:** Βεβαιωθείτε ότι τα έγγραφα προέλευσης περιέχουν πραγματικά τα μεταδεδομένα που σκοπεύετε να ερωτήσετε (π.χ., πεδία συγγραφέα σε PDF).  

## Σκέψεις απόδοσης
- **Memory tuning:** Ρυθμίστε το μέγεθος heap της JVM (`-Xmx`) βάσει του όγκου των ευρετηριασμένων μεταδεδομένων.  
- **Optimized storage:** Καλέστε περιοδικά το `index.optimize()` για να συμπιέσετε το ευρετήριο και να βελτιώσετε την ταχύτητα των ερωτημάτων.  

## Συχνά προβλήματα και λύσεις
| Πρόβλημα | Λύση |
|----------|------|
| **Δεν επιστρέφονται αποτελέσματα** | Επιβεβαιώστε ότι τα πεδία μεταδεδομένων που αναμένετε είναι πραγματικά παρόντα στα αρχεία προέλευσης. |
| **Σφάλματα δικαιωμάτων** | Βεβαιωθείτε ότι η διαδικασία Java έχει πρόσβαση ανάγνωσης τόσο στον φάκελο εγγράφων όσο και στον κατάλογο ευρετηρίου. |
| **Σφάλματα έλλειψης μνήμης** | Αυξήστε το μέγεθος heap της JVM ή εκτελέστε την λειτουργία `add` σε παρτίδες για να επεξεργαστείτε τα αρχεία σε μικρότερες ομάδες. |

## Συχνές ερωτήσεις

**Ε: Τι είναι η ευρετηρίαση μεταδεδομένων;**  
Α: Η ευρετηρίαση μεταδεδομένων αποθηκεύει τα χαρακτηριστικά του εγγράφου (συγγραφέας, τίτλος, προσαρμοσμένες ετικέτες) σε μια δομή αναζήτησης, επιτρέποντας γρήγορη ανάκτηση χωρίς σάρωση του πλήρους κειμένου.

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια;**  
Α: Επισκεφθείτε τη σελίδα αγοράς του GroupDocs και ακολουθήστε τα βήματα για να αποκτήσετε δοκιμαστική άδεια.

**Ε: Μπορώ να ευρετηριάσω PDF με αυτή τη ρύθμιση;**  
Α: Ναι, το GroupDocs.Search υποστηρίζει PDF, DOCX, PPT και πολλές άλλες μορφές.

**Ε: Ποια είναι τα κοινά προβλήματα κατά την προσθήκη εγγράφων;**  
Α: Επαληθεύστε τις σωστές διαδρομές αρχείων και βεβαιωθείτε ότι η εφαρμογή έχει δικαιώματα ανάγνωσης για τους καταλόγους.

**Ε: Πώς βελτιστοποιώ την απόδοση της αναζήτησης;**  
Α: Ενημερώνετε τακτικά το ευρετήριό σας, χρησιμοποιείτε προσθήκες incremental και ρυθμίζετε τις ρυθμίσεις μνήμης της JVM.

## Πόροι

- **Τεκμηρίωση:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **Αναφορά API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Λήψη:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **Αποθετήριο GitHub:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Δωρεάν φόρουμ υποστήριξης:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Προσωρινή άδεια:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία ενημέρωση:** 2026-10-22  
**Δοκιμή με:** GroupDocs.Search Java 25.4  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με ευρετηρίαση μεταδεδομένων σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Πώς να δημιουργήσετε ευρετήριο εγγράφων και να προσθέσετε έγγραφα χρησιμοποιώντας το GroupDocs.Search API για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Κατακτώντας τον Οδηγό Διαχείρισης Ευρετηρίου Groupdocs Search Java](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)