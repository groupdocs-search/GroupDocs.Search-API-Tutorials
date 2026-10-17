---
date: '2026-10-17'
description: Μάθετε πώς να εκτελέσετε ένα full text search java query, να προσθέσετε
  έγγραφα στο index και να δημιουργήσετε μια αξιόπιστη λύση αναζήτησης με GroupDocs.Search
  for Java, συμπεριλαμβανομένου του πώς να προσθέσετε folder στο index.
keywords:
- full text search java
- add folder to index
- add documents to index
- GroupDocs.Search Java
- search index Java
lastmod: '2026-10-17'
og_description: Full text search java με GroupDocs.Search for Java σας επιτρέπει να
  προσθέσετε folder στο index και να προσθέσετε έγγραφα στο index αποδοτικά. Μάθετε
  βήμα‑βήμα το setup, το indexing και το querying.
og_image_alt: Diagram showing Java code indexing documents and performing full text
  search using GroupDocs.Search
og_title: Full text search java με GroupDocs.Search – δημιουργία και διαχείριση ενός
  search index
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to execute a full text search java query, add documents to
    index, and build a robust search solution with GroupDocs.Search for Java, including
    how to add folder to index.
  headline: How to implement full text search java with GroupDocs.Search – create
    and manage a search index
  type: TechArticle
- description: Learn how to execute a full text search java query, add documents to
    index, and build a robust search solution with GroupDocs.Search for Java, including
    how to add folder to index.
  name: How to implement full text search java with GroupDocs.Search – create and
    manage a search index
  steps:
  - name: '**Java Development Kit (JDK) 8+** – the runtime for compiling and running
      the code.'
    text: '**Java Development Kit (JDK) 8+** – the runtime for compiling and running
      the code.'
  - name: '**Maven** – for dependency management (you can also use Gradle, but Maven
      examples are provided).'
    text: '**Maven** – for dependency management (you can also use Gradle, but Maven
      examples are provided).'
  - name: Basic familiarity with Java classes, methods, and the command line.
    text: Basic familiarity with Java classes, methods, and the command line.
  - name: '**Internal document management systems** – instant retrieval of policies,
      contracts, and manuals.'
    text: '**Internal document management systems** – instant retrieval of policies,
      contracts, and manuals.'
  - name: '**E‑commerce platforms** – fast product search across catalogs with thousands
      of items.'
    text: '**E‑commerce platforms** – fast product search across catalogs with thousands
      of items.'
  - name: '**Content management systems (CMS)** – enable editors and visitors to locate
      articles, media, and PDFs quickly.'
    text: '**Content management systems (CMS)** – enable editors and visitors to locate
      articles, media, and PDFs quickly.'
  type: HowTo
- questions:
  - answer: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, and many more common office
      formats – in total **30+** supported types.
    question: What file formats can GroupDocs.Search index?
  - answer: Yes. Build the index on the server and expose a REST endpoint that forwards
      the query to the Java service.
    question: Can I run a full text search java on a remote server?
  - answer: Use `index.update("path/to/changed/file")` to replace the old entry without
      rebuilding the whole index.
    question: How do I update the index when a document changes?
  - answer: After obtaining `SearchResult`, filter `result.getDocuments()` by their
      original path.
    question: Is there a way to limit search results to a specific folder?
  - answer: The library includes built‑in support for fuzzy matching (`~`) and wildcard
      (`*`) operators in query strings.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs.Search
- Java indexing
- search indexing
title: Πώς να υλοποιήσετε full text search java με GroupDocs.Search – δημιουργία και
  διαχείριση ενός search index
type: docs
url: /el/java/indexing/groupdocs-search-java-create-index-guide/
weight: 1
---

# Πλήρης αναζήτηση κειμένου java – εξειδίκευση GroupDocs.Search Java – δημιουργία και διαχείριση ευρετηρίου αναζήτησης

Στις σημερινές εφαρμογές που βασίζονται στα δεδομένα, η εκτέλεση μιας αποδοτικής **full text search java** σε μεγάλες συλλογές εγγράφων είναι απαραίτητη δυνατότητα. Είτε δημιουργείτε μια εσωτερική πύλη εγγράφων, έναν κατάλογο e‑commerce, είτε ένα CMS με πολλά περιεχόμενα, ένα καλά δομημένο ευρετήριο αναζήτησης παρέχει γρήγορα, ακριβή αποτελέσματα. Αυτό το εκπαιδευτικό υλικό σας καθοδηγεί στη ρύθμιση του GroupDocs.Search για Java, στη δημιουργία ενός ευρετηρίου αναζήτησης, **adding documents to index**, και στην εκτέλεση ενός ερωτήματος **full text search java** — όλα εξηγημένα με φιλικό, βήμα‑βήμα στυλ.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “full text search java”;** Εκτέλεση αναζήτησης με βάση το κείμενο σε ένα ευρετήριο που έχει δημιουργηθεί με το GroupDocs.Search σε μια εφαρμογή Java.  
- **Ποια βιβλιοθήκη διαχειρίζεται την ευρετηρίαση;** GroupDocs.Search for Java (latest stable release).  
- **Χρειάζομαι άδεια για να το δοκιμάσω;** Δωρεάν δοκιμή διατίθεται· απαιτείται προσωρινή ή πλήρης άδεια για παραγωγή.  
- **Μπορώ να ευρετηριάσω ολόκληρο φάκελο ταυτόχρονα;** Ναι – χρησιμοποιήστε `index.add("folderPath")` για **add folder to index** σε μία κλήση.  
- **Η αναζήτηση είναι ανεξάρτητη από πεζά/κεφαλαία;** Από προεπιλογή, το GroupDocs.Search εκτελεί ανεξάρτητες από πεζά/κεφαλαία full‑text αναζητήσεις.

## Τι είναι η full text search java;
Μια λειτουργία **full text search java** σας επιτρέπει να εντοπίζετε έγγραφα που περιέχουν ένα συγκεκριμένο μοτίβο κειμένου. Περνάτε μια συμβολοσειρά ερωτήματος στη μέθοδο `search()` ενός αντικειμένου GroupDocs.Search `Index`, και η βιβλιοθήκη αναλύει το ερώτημα, σαρώει τους ευρετηριασμένους όρους και επιστρέφει άμεσα τα ταιριαστά έγγραφα. Αυτό επιτρέπει γρήγορη ανάκτηση σχετικού περιεχομένου σε χιλιάδες αρχεία χωρίς χειροκίνητη σάρωση.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
Το GroupDocs.Search για Java παρέχει μια υψηλής απόδοσης, έτοιμη λύση για ευρετηρίαση και αναζήτηση. Μπορεί να ευρετηριάσει **30+** μορφές εγγράφων — συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, TXT, HTML, και πολλών τύπων εικόνων — και επεξεργάζεται αρχεία πολλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Οι ενσωματωμένοι αλγόριθμοι παρέχουν χρόνους απόκρισης σε επίπεδο **χιλιοστών του δευτερολέπτου** ακόμη και όταν το ευρετήριο περιέχει **εκατομμύρια έγγραφα**, καθιστώντας το κατάλληλο τόσο για μικρά εργαλεία όσο και για μεγάλες επιχειρησιακές υλοποιήσεις.

## Προαπαιτούμενα
1. **Java Development Kit (JDK) 8+** – το περιβάλλον εκτέλεσης για τη μεταγλώττιση και εκτέλεση του κώδικα.  
2. **Maven** – για διαχείριση εξαρτήσεων (μπορείτε επίσης να χρησιμοποιήσετε Gradle, αλλά παραδείγματα Maven παρέχονται).  
3. Βασική εξοικείωση με κλάσεις Java, μεθόδους και τη γραμμή εντολών.

## Ρύθμιση του GroupDocs.Search για Java

### Ρύθμιση Maven
Προσθέστε το αποθετήριο GroupDocs και την εξάρτηση στο `pom.xml`. Αυτή είναι η μόνη αλλαγή που χρειάζεται να κάνετε στη διαμόρφωση του έργου σας.

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

### Άμεση λήψη (προαιρετικό)
Εάν προτιμάτε να μην χρησιμοποιήσετε Maven, κατεβάστε το τελευταίο JAR από τη σελίδα επίσημων εκδόσεων: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Απόκτηση άδειας
- **Free trial:** Ιδανικό για αξιολόγηση λειτουργιών.  
- **Temporary license:** Χρησιμοποιήστε για εκτεταμένη δοκιμή χωρίς δέσμευση.  
- **Full license:** Συνιστάται για παραγωγικές υλοποιήσεις.

### Βασική αρχικοποίηση
Το παρακάτω απόσπασμα δημιουργεί έναν κενό φάκελο ευρετηρίου. Είναι η βάση για κάθε **full text search java** που θα εκτελέσετε αργότερα.

`Index` είναι η βασική κλάση που αντιπροσωπεύει ένα ευρετήριο αναζήτησης αποθηκευμένο στο δίσκο.

```java
import com.groupdocs.search.Index;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/HelloWorld";
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Πώς να δημιουργήσετε ένα ευρετήριο αναζήτησης

### Άμεση απάντηση
Δημιουργήστε ένα αντικείμενο `Index` που δείχνει σε φάκελο στο δίσκο, έπειτα καλέστε `index.add()` για να εισάγετε αρχεία. Αυτή η μοναδική λειτουργία δημιουργεί τη δομή αναζήτησης που τροφοδοτεί όλα τα επόμενα ερωτήματα full‑text. Αρχικοποιώντας το ευρετήριο μία φορά και προσθέτοντας έγγραφα μαζικά, εξασφαλίζετε βέλτιστη απόδοση και αποφεύγετε την επαναλαμβανόμενη επανευρετηρίαση.

`Index` είναι η κεντρική κλάση που διαχειρίζεται τη δομή δεδομένων αναζήτησης.

```java
import com.groupdocs.search.Index;

public class CreateIndexExample {
    public static void main(String[] args) {
        // Define the path for the output index directory
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/HelloWorld";
        
        // Creating an index in the specified folder.
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

### Προσθήκη φακέλου στο ευρετήριο
Τώρα που υπάρχει το ευρετήριο, πρέπει να **add documents to index** ώστε να γίνουν αναζητήσιμα. Το GroupDocs.Search μπορεί να εισάγει ολόκληρο φάκελο με μία κλήση.

Η μέθοδος `add` σαρώει τον καθορισμένο κατάλογο αναδρομικά, εξάγει κείμενο από κάθε υποστηριζόμενο αρχείο και αποθηκεύει τους όρους στο ευρετήριο.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexExample {
    public static void main(String[] args) {
        // Define the path for the output index directory and documents folder
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/HelloWorld";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Create an index in the specified folder.
        Index index = new Index(indexFolder);
        
        // Adding documents from the specified folder to the index.
        index.add(documentsFolder);
        System.out.println("Documents added to index.");
    }
}
```

### Εκτέλεση full text search java
Με τα έγγραφά σας ευρετηριασμένα, η εκτέλεση ενός **full text search java** είναι απλή.

Η μέθοδος `search` λαμβάνει μια συμβολοσειρά ερωτήματος, την επεξεργάζεται χρησιμοποιώντας τον ρυθμισμένο αναλυτή και επιστρέφει ένα `SearchResult` που περιέχει τα ταιριαστά έγγραφα.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchIndexExample {
    public static void main(String[] args) {
        // Define the path for the output index directory
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/HelloWorld";
        
        // Create an index in the specified folder.
        Index index = new Index(indexFolder);
        
        // Performing a search query on the indexed documents.
        SearchResult result = index.search("Lorem");
        
        System.out.println("Search completed. Number of results: " + result.getDocumentCount());
    }
}
```

## Πρακτικές εφαρμογές
Το GroupDocs.Search για Java διαπρέπει σε πολλές πραγματικές περιπτώσεις:

- **Internal document management systems** – άμεση ανάκτηση πολιτικών, συμβάσεων και εγχειριδίων.  
- **E‑commerce platforms** – γρήγορη αναζήτηση προϊόντων σε καταλόγους με χιλιάδες αντικείμενα.  
- **Content management systems (CMS)** – επιτρέπει σε επεξεργαστές και επισκέπτες να εντοπίζουν άρθρα, πολυμέσα και PDF γρήγορα.  

## Σκέψεις απόδοσης
Για να διατηρήσετε το **full text search java** αστραπιαία γρήγορο:

- **Optimize indexing:** Επαναευρετηριάστε μόνο τα τροποποιημένα αρχεία και καθαρίστε τα παλιά στοιχεία τακτικά.  
- **Manage resources:** Παρακολουθήστε τη χρήση heap της JVM· εξετάστε την επαυξητική ευρετηρίαση για τεράστιες συλλογές δεδομένων.  
- **Follow best practices:** Χρησιμοποιήστε κλήσεις batch `add()` αντί για προσθήκη αρχείων ένα‑ένα όταν είναι δυνατόν.  

## Συχνά προβλήματα & λύσεις

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| Δεν επιστράφηκαν αποτελέσματα | Το ευρετήριο δεν έχει δημιουργηθεί ή τα έγγραφα δεν έχουν προστεθεί | Επαληθεύστε ότι το `index.add()` εκτελέστηκε επιτυχώς· ελέγξτε τη διαδρομή του φακέλου. |
| Σφάλματα έλλειψης μνήμης | Πολύ μεγάλα αρχεία φορτώνονται όλα μαζί | Ενεργοποιήστε επαυξητική ευρετηρίαση ή αυξήστε το heap της JVM (`-Xmx`). |
| Η αναζήτηση παραλείπει όρους | Ο αναλυτής δεν είναι ρυθμισμένος για τη γλώσσα | Χρησιμοποιήστε τα κατάλληλα `IndexSettings` για να ορίσετε αναλυτές ειδικούς για τη γλώσσα. |

## Συχνές ερωτήσεις

**Q: Ποιοι τύποι αρχείων μπορεί να ευρετηριάσει το GroupDocs.Search;**  
A: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, και πολλοί άλλοι κοινοί τύποι γραφείου – συνολικά **30+** υποστηριζόμενοι τύποι.

**Q: Μπορώ να εκτελέσω ένα full text search java σε απομακρυσμένο διακομιστή;**  
A: Ναι. Δημιουργήστε το ευρετήριο στον διακομιστή και εκθέστε ένα REST endpoint που προωθεί το ερώτημα στην υπηρεσία Java.

**Q: Πώς ενημερώνω το ευρετήριο όταν αλλάζει ένα έγγραφο;**  
A: Χρησιμοποιήστε `index.update("path/to/changed/file")` για να αντικαταστήσετε την παλιά καταχώρηση χωρίς να ξαναδημιουργήσετε ολόκληρο το ευρετήριο.

**Q: Υπάρχει τρόπος να περιορίσω τα αποτελέσματα αναζήτησης σε συγκεκριμένο φάκελο;**  
A: Αφού λάβετε το `SearchResult`, φιλτράρετε το `result.getDocuments()` με βάση την αρχική διαδρομή τους.

**Q: Υποστηρίζει το GroupDocs.Search ασαφείς ή μπαλαντέρ αναζητήσεις;**  
A: Η βιβλιοθήκη περιλαμβάνει ενσωματωμένη υποστήριξη για ασαφή αντιστοίχιση (`~`) και τελεστές μπαλαντέρ (`*`) σε συμβολοσειρές ερωτημάτων.

**Q: Πώς μπορώ να βελτιώσω την κατάταξη συνάφειας για το full text search java μου;**  
A: Ρυθμίστε το `IndexSettings` όπως η βαρύτητα όρων, ενισχύστε συγκεκριμένα πεδία ή ενεργοποιήστε συνώνυμα για να βελτιώσετε τη συνάφεια.

**Q: Είναι δυνατόν να διαγράψετε έγγραφα από το ευρετήριο;**  
A: Ναι. Καλέστε `index.delete("path/to/file")` για να αφαιρέσετε μια καταχώρηση εγγράφου.

**Q: Τι κάνει πραγματικά το “add folder to index” στο παρασκήνιο;**  
A: Το GroupDocs.Search σαρώει τον φάκελο αναδρομικά, εξάγει κείμενο από κάθε υποστηριζόμενο αρχείο, δημιουργεί διακριτικά (tokens) όρων και τα αποθηκεύει στη δομή του ευρετηρίου για γρήγορη αναζήτηση.

---

**Τελευταία ενημέρωση:** 2026-10-17  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με ευρετηρίαση μεταδεδομένων σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Υλοποίηση Full Text Search Java Groupdocs Search](/search/java/searching/implement-full-text-search-java-groupdocs-search/)
- [Βιβλιοθήκη Java Full Text Search – Βελτιστοποίηση ευρετηρίου με το GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)