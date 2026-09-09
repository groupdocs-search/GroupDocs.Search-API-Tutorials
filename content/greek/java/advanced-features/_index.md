---
date: 2026-08-26
description: Μάθετε πώς να προσθέτετε έγγραφα σε ένα ευρετήριο για faceted search
  java χρησιμοποιώντας GroupDocs.Search, με υποστήριξη file extension filtering java
  και document filtering java.
keywords:
- faceted search java
- file extension filtering java
- document filtering java
lastmod: 2026-08-26
og_description: Μάθετε πώς να προσθέτετε έγγραφα σε ένα ευρετήριο για faceted search
  java χρησιμοποιώντας GroupDocs.Search, με υποστήριξη file extension filtering java
  και document filtering java.
og_image_alt: Guide showing how to add documents to an index for faceted search java
  using GroupDocs.Search
og_title: Προσθήκη εγγράφων στο ευρετήριο για faceted search java με GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how to add documents to an index for faceted search java using
    GroupDocs.Search, with file extension filtering java and document filtering java
    support.
  headline: Add documents to index for faceted search java with GroupDocs
  type: TechArticle
- description: Learn how to add documents to an index for faceted search java using
    GroupDocs.Search, with file extension filtering java and document filtering java
    support.
  name: Add documents to index for faceted search java with GroupDocs
  steps:
  - name: initialise the index folder
    text: Create a folder on disk that will hold the index files. Reusing the same
      folder across runs lets you append new documents without rebuilding the whole
      index.
  - name: configure optional index settings
    text: You can enable metadata extraction, set language options, or define custom
      analyzers. These settings affect tokenisation and how faceted search java interprets
      field values.
  - name: add documents to the index
    text: '`Index.add` adds one or more documents to the index, updating the inverted
      lists and storing any provided metadata. Pass a list of file paths (or streams)
      to `Index.add`. The library automatically detects the file type, extracts text,
      and updates the index. At this stage you can also apply **documen'
  - name: commit changes
    text: Calling `Index.commit()` flushes all pending updates to disk, guaranteeing
      that the newly added documents become searchable immediately.
  - name: verify the index
    text: Run a simple wildcard query such as `*` to confirm that the recently added
      documents appear in the results. This quick sanity check helps you catch indexing
      errors early.
  type: HowTo
- questions:
  - answer: Yes. GroupDocs.Search supports incremental indexing; simply call the add
      method with new files and commit the changes.
    question: Can I add documents to an existing index without rebuilding it?
  - answer: You can supply a whitelist or blacklist of extensions (e.g., `.pdf`, `.docx`).
      The engine will include only matching files when you add documents to the index.
    question: How does file extension filtering java work during indexing?
  - answer: Absolutely. Store the document’s creation or modification date as metadata,
      then use a date‑range query to retrieve matching items.
    question: Is it possible to filter search results by date range after indexing?
  - answer: The library throws a `DocumentProcessingException`. Wrap the add call
      in a try‑catch block and log the file path for later review.
    question: What happens if I try to add a corrupted file?
  - answer: Yes. Analyzer changes affect tokenisation, so a full re‑index ensures
      consistency across all documents.
    question: Do I need to re‑index when changing the analyzer settings?
  type: FAQPage
tags:
- faceted search
- GroupDocs.Search
- Java indexing
- document filtering java
- file extension filtering java
title: Προσθήκη εγγράφων στο ευρετήριο για faceted search java με GroupDocs
type: docs
url: /el/java/advanced-features/
weight: 8
---

# Προσθήκη εγγράφων στο ευρετήριο για faceted search java με GroupDocs

Σε αυτόν τον οδηγό θα μάθετε πώς να προσθέτετε έγγραφα σε ένα ευρετήριο ώστε να υποστηρίζετε εμπειρίες τύπου **faceted search java** με το GroupDocs.Search. Ένα καλά δομημένο ευρετήριο δεν επιταχύνει μόνο τις αναζητήσεις, αλλά επιτρέπει επίσης προηγμένα φίλτρα όπως document filtering java, file extension filtering java και ακριβείς ερωτήσεις εύρους ημερομηνιών. Στο τέλος του οδηγού θα είστε έτοιμοι να δημιουργήσετε γρήγορες, κλιμακώσιμες λύσεις αναζήτησης για μεγάλες συλλογές εγγράφων βασισμένες σε Java.

## Γρήγορες απαντήσεις
- **Τι σημαίνει το “add documents to index”;** Σημαίνει την εισαγωγή ενός ή περισσότερων αρχείων σε μια δομή δεδομένων αναζήτησης που δημιουργεί το GroupDocs.Search.  
- **Ποια έκδοση της Java απαιτείται;** Η Java 8 ή νεότερη υποστηρίζεται πλήρως.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια προσωρινή άδεια λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να φιλτράρω κατά τύπο αρχείου κατά την ευρετηρίαση;** Ναι – χρησιμοποιήστε το file extension filtering java για να συμπεριλάβετε ή να εξαιρέσετε συγκεκριμένες μορφές.  
- **Είναι δυνατή η αναζήτηση εύρους ημερομηνιών μετά την ευρετηρίαση;** Απολύτως, μπορείτε να εφαρμόσετε ερωτήματα εύρους ημερομηνιών στα μεταδεδομένα του ευρετηρίου.

## Τι είναι το “add documents to index” στο GroupDocs.Search;

Η φόρτωση ενός αρχείου στο ευρετήριο δημιουργεί άμεσα αναζητήσιμες καταχωρήσεις. Όταν προσθέτετε έγγραφα, το GroupDocs.Search εξάγει το ακατέργαστο κείμενο, δημιουργεί ένα ανεστραμμένο ευρετήριο και αποθηκεύει τυχόν παρεχόμενα μεταδεδομένα ώστε μελλοντικά ερωτήματα—όπως το faceted search java—να μπορούν να ανακτούν αποτελέσματα σε χιλιοστά του δευτερολέπτου. Αυτή η λειτουργία αποτελεί τη βάση για οποιοδήποτε επόμενο φιλτράρισμα ή faceted navigation.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για ευρετηρίαση Java;

Το GroupDocs.Search επεξεργάζεται έως και 5 εκατομμύρια έγγραφα με αποτύπωση μνήμης κάτω από 200 MB, κατάλληλο για επιχειρησιακά φορτία εργασίας. Υποστηρίζει πάνω από 50 μορφές εισόδου και εξόδου, σας επιτρέπει να προσθέτετε προσαρμοσμένα μεταδεδομένα (συγγραφέας, ημερομηνία δημιουργίας, ετικέτες) και περιλαμβάνει ενσωματωμένα document filtering java και file extension filtering java για να εξαιρούνται ανεπιθύμητα αρχεία κατά την ευρετηρίαση. Η μηχανή λειτουργεί on‑premises ή στο cloud, παρέχοντας συνεπή απόδοση.

## Προαπαιτούμενα
- Java 8 ή νεότερη εγκατεστημένη.  
- Η βιβλιοθήκη GroupDocs.Search for Java προστέθηκε στο έργο σας (Maven/Gradle).  
- Ένα προσωρινό ή πλήρες κλειδί άδειας (δείτε το **Additional Resources** παρακάτω).  

## Πώς να προσθέσετε έγγραφα στο ευρετήριο με το GroupDocs.Search Java;

Η κλάση `Index` διαχειρίζεται τη συλλογή αναζήτησης, αποθηκεύοντας το ανεστραμμένο ευρετήριο και τα συναφή μεταδεδομένα. Φορτώστε τα αρχεία σας, προαιρετικά προσθέστε μεταδεδομένα όπως συγγραφέας ή ημερομηνία δημιουργίας, διαμορφώστε τυχόν φίλτρα και, στη συνέχεια, δεσμεύστε τις αλλαγές—όλα σε λίγα απλά βήματα που εξασφαλίζουν ότι τα νέα έγγραφα γίνονται άμεσα αναζητήσιμα.

### Βήμα 1: αρχικοποίηση του φακέλου ευρετηρίου
Δημιουργήστε έναν φάκελο στο δίσκο που θα περιέχει τα αρχεία του ευρετηρίου. Η επαναχρήση του ίδιου φακέλου σε πολλαπλές εκτελέσεις σας επιτρέπει να προσθέτετε νέα έγγραφα χωρίς να ξαναχτίζετε ολόκληρο το ευρετήριο.

### Βήμα 2: διαμόρφωση προαιρετικών ρυθμίσεων ευρετηρίου
Μπορείτε να ενεργοποιήσετε την εξαγωγή μεταδεδομένων, να ορίσετε επιλογές γλώσσας ή να ορίσετε προσαρμοσμένους αναλυτές. Αυτές οι ρυθμίσεις επηρεάζουν την τοκενικοποίηση και το πώς το faceted search java ερμηνεύει τις τιμές πεδίων.

### Βήμα 3: προσθήκη εγγράφων στο ευρετήριο
`Index.add` προσθέτει ένα ή περισσότερα έγγραφα στο ευρετήριο, ενημερώνοντας τις ανεστραμμένες λίστες και αποθηκεύοντας τυχόν παρεχόμενα μεταδεδομένα. Περάστε μια λίστα διαδρομών αρχείων (ή ροών) στο `Index.add`. Η βιβλιοθήκη ανιχνεύει αυτόματα τον τύπο του αρχείου, εξάγει το κείμενο και ενημερώνει το ευρετήριο. Σε αυτό το στάδιο μπορείτε επίσης να εφαρμόσετε κανόνες **document filtering java** για να παραλείψετε αρχεία που δεν ταιριάζουν με τα επιχειρηματικά σας κριτήρια.

### Βήμα 4: δέσμευση αλλαγών
Η κλήση του `Index.commit()` αποθηκεύει όλες τις εκκρεμείς ενημερώσεις στο δίσκο, εξασφαλίζοντας ότι τα νεοπροστέθηκαν έγγραφα γίνονται άμεσα αναζητήσιμα.

### Βήμα 5: επαλήθευση του ευρετηρίου
Εκτελέστε ένα απλό ερώτημα μπαλαντέρ όπως `*` για να επιβεβαιώσετε ότι τα πρόσφατα προστιθέντα έγγραφα εμφανίζονται στα αποτελέσματα. Αυτός ο γρήγορος έλεγχος βοηθά στον εντοπισμό σφαλμάτων ευρετηρίου νωρίς.

## Γιατί είναι σημαντικό αυτό
Η υλοποίηση του faceted search java πάνω σε ένα σταθερό ευρετήριο επιτρέπει στους τελικούς χρήστες να εμβαθύνουν ανά κατηγορίες, ημερομηνίες ή προσαρμοσμένες ετικέτες με ένα κλικ. Επειδή το ευρετήριο περιέχει ήδη τα απαιτούμενα μεταδεδομένα, η μηχανή μπορεί να απαντήσει σε αυτά τα ερωτήματα σε χρόνο κάτω από το δευτερόλεπτο, ακόμη και όταν η υποκείμενη συλλογή περιέχει εκατοντάδες χιλιάδες αρχεία.

## Συνηθισμένες περιπτώσεις χρήσης
- **Enterprise document portals** όπου οι χρήστες χρειάζονται να αναζητούν μεταξύ συμβάσεων, πολιτικών και αναφορών.  
- **Legal e‑discovery** λύσεις που απαιτούν ακριβή φιλτράρισμα εύρους ημερομηνιών σε μεγάλα αρχεία υποθέσεων.  
- **Content management systems** που πρέπει να εξαιρούν μη‑κειμενικά αρχεία χρησιμοποιώντας το file extension filtering java.  

## Αντιμετώπιση προβλημάτων & συμβουλές
- **Large files:** Αυξήστε τη μνήμη heap της JVM ή ενεργοποιήστε τη λειτουργία streaming για να αποφύγετε σφάλματα OutOfMemory.  
- **Unsupported formats:** Επαληθεύστε ότι ο τύπος αρχείου εμφανίζεται στη λίστα υποστηριζόμενων μορφών του GroupDocs.Search· διαφορετικά, ενσωματώστε έναν προσαρμοσμένο parser.  
- **Performance bottlenecks:** Προσθέστε έγγραφα σε παρτίδες αντί για ένα‑ένα για να μειώσετε το φόρτο I/O.  
- **Pro tip:** Αποθηκεύστε συχνά αναζητούμενα μεταδεδομένα (π.χ., ημερομηνία δημιουργίας) ως ξεχωριστό πεδίο ευρετηρίου για να επιταχύνετε τα ερωτήματα εύρους ημερομηνιών.

## Διαθέσιμα tutorials

### [Αναζήτηση εγγράφων με βάση τα τμήματα σε Java&#58; Ολοκληρωμένος οδηγός με χρήση του GroupDocs.Search](./groupdocs-search-java-chunk-based-search-tutorial/)
Μάθετε πώς να υλοποιήσετε αποδοτικές αναζητήσεις εγγράφων με βάση τα τμήματα με το GroupDocs.Search για Java. Βελτιώστε την παραγωγικότητα και διαχειριστείτε μεγάλες συλλογές δεδομένων απρόσκοπτα.

### [Faceted και σύνθετες αναζητήσεις σε Java&#58; Κατακτήστε το GroupDocs.Search για προχωρημένα χαρακτηριστικά](./faceted-complex-search-groupdocs-java/)
Μάθετε πώς να υλοποιήσετε faceted και σύνθετες αναζητήσεις σε εφαρμογές Java χρησιμοποιώντας το GroupDocs.Search, βελτιώνοντας τη λειτουργικότητα αναζήτησης και την εμπειρία χρήστη.

### [Υλοποίηση GroupDocs.Search Java&#58; Ολοκληρωμένος οδηγός ευρετηρίασης και αναφοράς](./groupdocs-search-java-index-report-guide/)
Κατακτήστε το GroupDocs.Search σε Java για αποδοτική ευρετηρίαση εγγράφων και αναφορές. Μάθετε να δημιουργείτε ευρετήρια, να προσθέτετε έγγραφα και να παράγετε αναφορές με αυτόν τον λεπτομερή οδηγό.

### [Κατακτήστε τις αναζητήσεις εύρους ημερομηνιών σε Java με το GroupDocs.Search](./master-date-range-searches-groupdocs-java/)
Ένας οδηγός κώδικα για το GroupDocs.Search Java

### [Κατακτήστε το GroupDocs.Search Java&#58; Προηγμένα χαρακτηριστικά αναζήτησης για αποδοτική ανάκτηση δεδομένων](./groupdocs-search-java-advanced-search-features/)
Μάθετε να κατακτήσετε τα προχωρημένα χαρακτηριστικά αναζήτησης στο GroupDocs.Search για Java, συμπεριλαμβανομένου του χειρισμού σφαλμάτων, διαφόρων τύπων ερωτημάτων και βελτιστοποίησης απόδοσης.

### [Κατακτήστε το φιλτράρισμα αρχείων Java χρησιμοποιώντας το GroupDocs.Search&#58; Οδηγός βήμα‑βήμα](./master-java-file-filtering-groupdocs-search/)
Μάθετε πώς να διαχειρίζεστε και να φιλτράρετε αποδοτικά αρχεία σε Java χρησιμοποιώντας το GroupDocs.Search, συμπεριλαμβανομένων των επεκτάσεων αρχείων, λογικών τελεστών και άλλων.

### [Κατακτώντας το GroupDocs.Search για Java&#58; Ο πλήρης οδηγός σας για ευρετηρίαση και αναζήτηση εγγράφων](./groupdocs-search-java-implementation-guide/)
Μάθετε πώς να υλοποιήσετε το GroupDocs.Search σε Java με αυτόν τον ολοκληρωμένο οδηγό. Ανακαλύψτε ισχυρή εξαγωγή κειμένου, σειριοποίηση, ευρετηρίαση και χαρακτηριστικά αναζήτησης.

## Πρόσθετοι πόροι
- [Τεκμηρίωση GroupDocs.Search for Java](https://docs.groupdocs.com/search/java/)
- [Αναφορά API GroupDocs.Search for Java](https://reference.groupdocs.com/search/java/)
- [Λήψη GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- [Φόρουμ GroupDocs.Search](https://forum.groupdocs.com/c/search)
- [Δωρεάν υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/)

## Συχνές ερωτήσεις

**Q: Μπορώ να προσθέσω έγγραφα σε υπάρχον ευρετήριο χωρίς επαναδημιουργία;**  
A: Ναι. Το GroupDocs.Search υποστηρίζει την επαυξητική ευρετηρίαση· απλώς καλέστε τη μέθοδο add με νέα αρχεία και δεσμεύστε τις αλλαγές.

**Q: Πώς λειτουργεί το file extension filtering java κατά την ευρετηρίαση;**  
A: Μπορείτε να παρέχετε μια λίστα επιτρεπόμενων ή αποκλεισμένων επεκτάσεων (π.χ., `.pdf`, `.docx`). Η μηχανή θα συμπεριλάβει μόνο τα αντίστοιχα αρχεία όταν προσθέτετε έγγραφα στο ευρετήριο.

**Q: Είναι δυνατόν να φιλτράρετε τα αποτελέσματα αναζήτησης κατά εύρος ημερομηνιών μετά την ευρετηρίαση;**  
A: Απολύτως. Αποθηκεύστε την ημερομηνία δημιουργίας ή τροποποίησης του εγγράφου ως μεταδεδομένα, στη συνέχεια χρησιμοποιήστε ένα ερώτημα εύρους ημερομηνιών για να ανακτήσετε τα αντίστοιχα στοιχεία.

**Q: Τι συμβαίνει αν προσπαθήσω να προσθέσω ένα κατεστραμμένο αρχείο;**  
A: Η βιβλιοθήκη ρίχνει ένα `DocumentProcessingException`. Τυλίξτε την κλήση add σε ένα μπλοκ try‑catch και καταγράψτε τη διαδρομή του αρχείου για μελλοντική ανασκόπηση.

**Q: Χρειάζεται να επανευρετηριάσω όταν αλλάζω τις ρυθμίσεις του αναλυτή;**  
A: Ναι. Οι αλλαγές του αναλυτή επηρεάζουν την τοκενικοποίηση, έτσι μια πλήρης επανευρετηρίαση εξασφαλίζει τη συνέπεια σε όλα τα έγγραφα.

---

**Τελευταία ενημέρωση:** 2026-08-26  
**Δοκιμάστηκε με:** GroupDocs.Search for Java 23.12  
**Συγγραφέας:** GroupDocs

## Σχετικά tutorials

- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με ευρετηρίαση μεταδεδομένων σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Φίλτρο επεκτάσεων αρχείων java με το GroupDocs.Search – Οδηγός](/search/java/advanced-features/master-java-file-filtering-groupdocs-search/)
- [Προσθήκη εγγράφων στο ευρετήριο με αναζήτηση με βάση τα τμήματα σε Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)