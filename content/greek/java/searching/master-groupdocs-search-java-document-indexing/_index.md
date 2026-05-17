---
date: '2026-02-08'
description: Μάθετε πώς να επισημαίνετε τα αποτελέσματα αναζήτησης Java και πώς να
  ευρετηριάτε έγγραφα Java χρησιμοποιώντας το GroupDocs.Search for Java με συγχρονισμένη
  και ασύγχρονη ευρετηρίαση.
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: Επισήμανση Αποτελεσμάτων Αναζήτησης Java – Συγχρονιστική & Ασύγχρονη Δεικτοδότηση
type: docs
url: /el/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Επισήμανση Αποτελεσμάτων Αναζήτησης Java – Συγχρονιστική & Ασύγχρονη Δεικτοδότηση

Boost your Java applications by **highlighting search results Java** with the powerful GroupDocs.Search library. Whether you’re dealing with a few files or a massive repository, mastering both synchronous and asynchronous indexing lets you deliver fast, accurate results without blocking your application threads.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “highlight search results Java”;** Αναφέρεται στην απόδοση των ταιριασμένων όρων στα αποτελέσματα αναζήτησης με οπτικές ενδείξεις (π.χ., ετικέτες HTML `<mark>`) ώστε οι χρήστες να βλέπουν πού εμφανίζεται το ερώτημα σε κάθε έγγραφο.  
- **Πότε πρέπει να χρησιμοποιήσω συγχρονιστική δεικτοδότηση;** Για μικρά έως μεσαία σύνολα δεδομένων όπου απαιτείται άμεση διαθεσιμότητα των νεοπροστέθειων εγγράφων.  
- **Πότε είναι προτιμότερη η ασύγχρονη δεικτοδότηση;** Όταν επεξεργάζεστε μεγάλες συλλογές εγγράφων ή εκτελείτε σε νήμα UI όπου πρέπει να διατηρείται η ανταπόκριση της εφαρμογής.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· μια πλήρης άδεια ξεκλειδώνει προηγμένες λειτουργίες και αφαιρεί τους περιορισμούς χρήσης.  
- **Ποια έκδοση της Java υποστηρίζεται;** Java 8 ή νεότερη.

## Τι είναι το “highlight search results Java”;
Η επισήμανση αποτελεσμάτων αναζήτησης σε Java σημαίνει ότι λαμβάνονται οι ακατέργαστες αντιστοιχίες που επιστρέφει το GroupDocs.Search και τυλίγονται οι ταιριασμένοι όροι σε HTML (ή άλλη σήμανση) ώστε να ξεχωρίζουν όταν εμφανίζονται σε UI ή ιστοσελίδα. Αυτό βελτιώνει την εμπειρία του χρήστη εμφανίζοντας άμεσα το πλαίσιο κάθε αποτελέσματος.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
GroupDocs.Search provides a high‑performance, language‑agnostic engine that supports:
- Δεικτοδότηση και αναζήτηση σε πραγματικό χρόνο
- Ασύγχρονη επεξεργασία για μεγάλα φορτία εργασίας
- Ενσωματωμένη επισήμανση αποτελεσμάτων
- Υποστήριξη πολυγλωσσικών και προσαρμοσμένων αναλυτών  

These capabilities make it ideal for content management systems, e‑commerce catalogs, and enterprise document repositories.

## Προαπαιτούμενα
Before you start, make sure you have:

- **Java Development Kit** (JDK 8 ή νεότερο) installed.
- Ένα IDE όπως το **IntelliJ IDEA** ή το **Eclipse**.
- Έναν φάκελο που περιέχει τα έγγραφα που θέλετε να δεικτοδοτήσετε.
- Maven για διαχείριση εξαρτήσεων (ή μπορείτε να κατεβάσετε το JAR χειροκίνητα).

### Απαιτούμενες Βιβλιοθήκες και Εξαρτήσεις
Add GroupDocs.Search to your Maven project:

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

For direct downloads, get the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Ρύθμιση Περιβάλλοντος
- Επαληθεύστε ότι το **JAVA_HOME** σας δείχνει σε συμβατό JDK.
- Δημιουργήστε ένα project στο IDE σας και προσθέστε τη Maven διαμόρφωση παραπάνω.
- Προετοιμάστε έναν κατάλογο (π.χ., `documents/`) με δείγμα κειμένου, PDF ή αρχεία Word.

## Πώς να ρυθμίσετε το GroupDocs.Search για Java
1. **Εγκατάσταση της Βιβλιοθήκης** – Χρησιμοποιήστε το Maven snippet παραπάνω ή κατεβάστε το JAR από [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Απόκτηση Άδειας** – Ξεκινήστε με δοκιμαστική άδεια, στη συνέχεια αναβαθμίστε όταν μεταβείτε στην παραγωγή.  
3. **Αρχικοποίηση του Δείκτη** – Το παρακάτω snippet δείχνει πώς να δημιουργήσετε (ή να ανοίξετε) έναν φάκελο δείκτη:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Πώς να επισήμανση αποτελεσμάτων αναζήτησης Java – Συγχρονιστική Δεικτοδότηση
Synchronous indexing processes documents immediately, making newly added files searchable right away.

### Βήμα 1: Δημιουργία του δείκτη και προσθήκη διαχείρισης σφαλμάτων
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

### Βήμα 2: Προσθήκη εγγράφων και εκτέλεση αναζήτησης
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Βήμα 3: Επεξεργασία αποτελεσμάτων και **highlight search results Java**
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

The `DocumentHighlighter` automatically wraps matched terms with `<mark>` tags (or any format you configure), giving you **highlighted search results** ready for display.

## Πώς να επισήμανση αποτελεσμάτων αναζήτησης Java – Ασύγχρονη Δεικτοδότηση
When dealing with thousands of files, blocking the main thread is undesirable. Asynchronous indexing lets the engine work in the background.

### Βήμα 1: Ρύθμιση του δείκτη με ακροατές συμβάντων
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

### Βήμα 2: Ενεργοποίηση ασύγχρονης λειτουργίας και έναρξη δεικτοδότησης
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

While the index is being built, your application can continue to serve other requests. Once the `StatusChanged` event reports `Ready`, you can safely run searches and obtain **highlighted search results Java**.

## Πώς να **index documents java** – Πρακτικές Συμβουλές
- **Batch size**: Για τεράστιες συλλογές, χωρίστε το φάκελο σε μικρότερα batch ώστε να αποφύγετε ξαφνικές αυξήσεις μνήμης.  
- **File filters**: Χρησιμοποιήστε `IndexingOptions.setFileExtensions` για να συμπεριλάβετε μόνο τις μορφές που χρειάζεστε (π.χ., `.pdf`, `.docx`).  
- **Re‑indexing**: Όταν τα έγγραφα αλλάζουν, καλέστε `index.update(documentPath)` αντί να ξαναχτίσετε ολόκληρο τον δείκτη.

## Σκέψεις Απόδοσης
- **Memory**: Παρακολουθείτε τη χρήση heap· αυξήστε το `-Xmx` αν επεξεργάζεστε πολλά μεγάλα αρχεία.  
- **CPU**: Η ασύγχρονη δεικτοδότηση διανέμει το φορτίο, αλλά εξακολουθεί να καταναλώνει CPU—παρακολουθήστε με το JVisualVM.  
- **Result Highlighting**: Η επισήμανση προσθέτει μικρό κόστος επεξεργασίας· αποθηκεύστε στην cache το παραγόμενο HTML αν χρειάζεται να εμφανίζετε τα αποτελέσματα επανειλημμένα.

## Συχνές Ερωτήσεις

**Q: Μπορώ να συνδυάσω συγχρονιστική και ασύγχρονη δεικτοδότηση στην ίδια εφαρμογή;**  
A: Ναι. Χρησιμοποιήστε συγχρονιστική δεικτοδότηση για μικρά, συχνά ενημερωμένα σύνολα και ασύγχρονη δεικτοδότηση για μαζικές εισαγωγές ή εργασίες παρασκηνίου.

**Q: Πώς προσαρμόζω το στυλ της επισήμανσης;**  
A: Παρέχετε μια προσαρμοσμένη υλοποίηση `DocumentHighlighter` που γράφει τις επιθυμητές ετικέτες HTML, CSS ή XML γύρω από τους ταιριασμένους όρους.

**Q: Ποιοι τύποι αρχείων υποστηρίζει το GroupDocs.Search εξ' αρχής;**  
A: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, και πολλά άλλα μέσω των ενσωματωμένων αναλυτών του.

**Q: Είναι δυνατόν να αναζητήσω σε πολλαπλές γλώσσες ταυτόχρονα;**  
A: Απόλυτα. Το GroupDocs.Search περιλαμβάνει πολυγλωσσικούς αναλυτές· απλώς ρυθμίστε τον κατάλληλο `Analyzer` κατά τη δημιουργία του δείκτη.

**Q: Πώς ασφαλίζω το φάκελο του δείκτη;**  
A: Αποθηκεύστε το δείκτη σε προστατευμένο κατάλογο, ορίστε σωστές άδειες συστήματος αρχείων και σκεφτείτε την κρυπτογράφηση του δείκτη με τις λειτουργίες ασφαλείας της βιβλιοθήκης.

---

**Τελευταία Ενημέρωση:** 2026-02-08  
**Δοκιμή Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs