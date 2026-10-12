---
date: 2026-10-12
description: Μάθετε πώς να ενημερώσετε το index, να προσθέσετε έγγραφα και να διαγράψετε
  καταχωρήσεις του index χρησιμοποιώντας το GroupDocs.Search για Java. Λεπτομερή βήματα,
  βέλτιστες πρακτικές και παραδείγματα κώδικα.
keywords:
- how to update index
- how to add documents
- how to delete index
lastmod: 2026-10-12
og_description: Μάθετε πώς να ενημερώσετε το index, να προσθέσετε έγγραφα και να διαγράψετε
  καταχωρήσεις του index με το GroupDocs.Search για Java. Ακολουθήστε καθοδήγηση βήμα‑βήμα
  και συμβουλές απόδοσης.
og_image_alt: Guide to updating index, adding and deleting documents using GroupDocs.Search
  Java SDK
og_title: Πώς να ενημερώσετε το index και να προσθέσετε έγγραφα με GroupDocs.Search
  Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: Learn how to update index, add documents, and delete index entries
    using GroupDocs.Search for Java. Detailed steps, best practices, and code examples.
  headline: How to update index and add docs with GroupDocs.Search Java
  type: TechArticle
- description: Learn how to update index, add documents, and delete index entries
    using GroupDocs.Search for Java. Detailed steps, best practices, and code examples.
  name: How to update index and add docs with GroupDocs.Search Java
  steps:
  - name: open or create the index
    text: '`Index index = new Index("path/to/index");` creates the folder if it does
      not exist and prepares internal structures for fast lookup.'
  - name: add a single document
    text: '`index.addDocument(new File("contracts/contract1.pdf"));` inserts the PDF,
      automatically detecting its format and extracting text.'
  - name: add multiple documents in a batch
    text: Iterate over a directory and call `addDocument` for each file. Batch processing
      reduces I/O overhead and improves overall throughput.
  type: HowTo
- questions:
  - answer: Call `deleteDocument(documentId)` with the unique identifier; the entry
      is instantly purged and storage is reclaimed.
    question: How do I remove documents from index?
  - answer: Yes, you can set custom metadata (e.g., category, author) via the `Document`
      object's attribute API before adding it to the index.
    question: Can I modify document attributes to enhance search accuracy?
  - answer: The official GroupDocs.Search documentation includes a step‑by‑step tutorial
      that covers index creation, document addition, and query execution.
    question: Is there a “search index tutorial” for beginners?
  - answer: The library includes linguistic features that improve accuracy for homophones
      and similar‑sounding words.
    question: Does GroupDocs.Search support homophone recognition?
  - answer: Java 8 or later is required; the library is fully compatible with Java
      11 and newer LTS releases.
    question: What version of Java is required for the latest GroupDocs.Search?
  type: FAQPage
tags:
- update index
- document management
- GroupDocs.Search Java
- add documents
title: Πώς να ενημερώσετε το index και να προσθέσετε έγγραφα με GroupDocs.Search Java
type: docs
url: /el/java/document-management/
weight: 6
---

# Πώς να ενημερώσετε το ευρετήριο και να προσθέσετε έγγραφα με το GroupDocs.Search Java

Η αποτελεσματική διαχείριση ενός ευρετηρίου αναζήτησης είναι ουσιώδης για κάθε εφαρμογή βασισμένη σε Java που χρειάζεται γρήγορη, ακριβή ανάκτηση πληροφοριών. Σε αυτό το σεμινάριο θα μάθετε **πώς να ενημερώσετε το ευρετήριο**, καθώς και πώς να προσθέτετε και να διαγράφετε έγγραφα, χρησιμοποιώντας το GroupDocs.Search για Java. Θα δείτε πρότυπα βέλτιστων πρακτικών, συμβουλές απόδοσης και παραδείγματα πραγματικών περιπτώσεων χρήσης που διατηρούν το ευρετήριό σας ελαφρύ και τα ερωτήματά σας αστραπιαία γρήγορα.

## Γρήγορες απαντήσεις
- **Ποιο είναι το πρώτο βήμα για την προσθήκη εγγράφων στο ευρετήριο;** Δημιουργήστε ή ανοίξτε μια παρουσία `Index` και καλέστε `addDocument(...)`.
- **Μπορώ να αφαιρέσω έγγραφα από το ευρετήριο;** Ναι, καλέστε `deleteDocument(...)` με το αναγνωριστικό του εγγράφου.
- **Χρειάζομαι ειδική άδεια;** Απαιτείται έγκυρη άδεια GroupDocs.Search for Java για παραγωγική χρήση.
- **Ποια έκδοση της Java υποστηρίζεται;** Η Java 8 και νεότερες εκδόσεις υποστηρίζονται πλήρως.
- **Πού μπορώ να βρω περισσότερα παραδείγματα;** Δείτε την επίσημη τεκμηρίωση GroupDocs.Search for Java και την αναφορά API.

## Τι σημαίνει “προσθήκη εγγράφων στο ευρετήριο” στο GroupDocs.Search;
Η λειτουργία `addDocument` εισάγει το αναζητήσιμο περιεχόμενο ενός αρχείου (PDF, DOCX, TXT κ.λπ.) στη δομή δεδομένων του ευρετηρίου. Αυτό καθιστά το έγγραφο άμεσα αναζητήσιμο και εξασφαλίζει ότι οι επόμενες ενημερώσεις ή διαγραφές παραμένουν συγχρονισμένες με τα αρχικά αρχεία. Επίσης καταγράφει μεταδεδομένα όπως το όνομα και το μέγεθος του αρχείου, τα οποία μπορούν να χρησιμοποιηθούν για φιλτράρισμα των αποτελεσμάτων αναζήτησης.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για έργα διαχείρισης εγγράφων Java;
Το GroupDocs.Search επεξεργάζεται έως και **10 εκατομμύρια έγγραφα** με καθυστέρηση κάτω του δευτερολέπτου, υποστηρίζει **πάνω από 100 μορφές αρχείων** και προσφέρει ενσωματωμένη ρύθμιση σχετικότητας. Το API είναι ελαφρύ, απαιτεί μόνο λίγες γραμμές κώδικα και ενσωματώνεται ομαλά σε οποιαδήποτε εφαρμογή Java—είτε τρέχει σε επιτραπέζιο υπολογιστή, διακομιστή ή περιβάλλον cloud.

## Προαπαιτούμενα
- Περιβάλλον ανάπτυξης Java 8 + (IDE, JDK, Maven/Gradle).  
- Βιβλιοθήκη GroupDocs.Search for Java (λήψη από την επίσημη ιστοσελίδα).  
- Έγκυρη άδεια GroupDocs.Search (προσωρινές άδειες διατίθενται για δοκιμές).

## Πώς να προσθέσετε έγγραφα στο ευρετήριο στο GroupDocs.Search for Java;
Φορτώστε το αρχείο-στόχο και καλέστε `addDocument` σε μια παρουσία `Index`—αυτή η ενιαία κλήση εξάγει το κείμενο, ανιχνεύει τη γλώσσα και αποθηκεύει τα αναζητήσιμα tokens. Η μέθοδος επιστρέφει επίσης ένα αναγνωριστικό εγγράφου που πρέπει να αποθηκεύσετε για μελλοντικές λειτουργίες ενημέρωσης ή διαγραφής.

Η κλάση `Index` είναι το βασικό αντικείμενο που αντιπροσωπεύει μια αναζητήσιμη συλλογή αποθηκευμένη στο δίσκο. Αφού τη δημιουργήσετε, όλες οι επόμενες λειτουργίες—προσθήκη, ενημέρωση, διαγραφή και βελτιστοποίηση—εκτελούνται μέσω αυτής της παρουσίας.

### Βήμα 1: ανοίξτε ή δημιουργήστε το ευρετήριο
```java
Index index = new Index("path/to/index");
```
Δημιουργεί το φάκελο εάν δεν υπάρχει και προετοιμάζει τις εσωτερικές δομές για γρήγορη αναζήτηση.

### Βήμα 2: προσθέστε ένα μόνο έγγραφο
```java
index.addDocument(new File("contracts/contract1.pdf"));
```
Εισάγει το PDF, ανιχνεύοντας αυτόματα τη μορφή του και εξάγοντας το κείμενο.

### Βήμα 3: προσθέστε πολλαπλά έγγραφα σε παρτίδα
Επανάληψη πάνω σε έναν κατάλογο και κλήση του `addDocument` για κάθε αρχείο. Η επεξεργασία σε παρτίδες μειώνει το φορτίο I/O και βελτιώνει τη συνολική απόδοση.

## Πώς να ενημερώσετε το ευρετήριο όταν αλλάζει ένα αρχείο προέλευσης;
`updateDocument` ενημερώνει ένα υπάρχον έγγραφο στο ευρετήριο χρησιμοποιώντας το αναγνωριστικό του. Αντικαταστήστε το παλιό περιεχόμενο με την πιο πρόσφατη έκδοση καλώντας αυτή τη μέθοδο και περνώντας το ίδιο αναγνωριστικό εγγράφου που λάβατε όταν προσθέσατε αρχικά το αρχείο. Αυτή η λειτουργία ξαναγράφει μόνο τα τροποποιημένα tokens, διατηρώντας το υπόλοιπο ευρετήριο αμετάβλητο για μέγιστη αποδοτικότητα.

### Ενημέρωση βήμα‑βήμα
1. Ανακτήστε το αναγνωριστικό του εγγράφου (αποθηκεύστε το όταν προσθέτετε αρχικά το αρχείο).  
2. Καλέστε `index.updateDocument(documentId, new File("contracts/contract1_v2.pdf"));` για να ανανεώσετε την καταχώρηση.  
3. Προαιρετικά, εκτελέστε ξανά `index.optimize()` μετά από μια μεγάλη παρτίδα ενημερώσεων για να διατηρήσετε το ευρετήριο συμπαγές.

## Πώς να διαγράψετε εγγραφές ευρετηρίου με ασφάλεια;
`deleteDocument` αφαιρεί ένα έγγραφο από το ευρετήριο με το αναγνωριστικό του. Η αφαίρεση ενός εγγράφου ελευθερώνει χώρο αποθήκευσης και αποτρέπει τα παλαιά δεδομένα να επηρεάζουν τις βαθμολογίες σχετικότητας. Καλέστε `deleteDocument` με το αναγνωριστικό· το ευρετήριο εξαιρεί αμέσως το αρχείο από μελλοντικές αναζητήσεις και ενημερώνει τις εσωτερικές λίστες καταχωρίσεων για να διατηρήσει την απόδοση των ερωτημάτων.

## Πώς να βελτιστοποιήσετε το ευρετήριο για μέγιστη απόδοση;
`optimize()` συμπιέζει το ευρετήριο συγχωνεύοντας τμήματα και καθαρίζοντας τις διαγραμμένες εγγραφές. Μετά από μαζικές προσθήκες, ενημερώσεις ή διαγραφές, καλέστε αυτή τη μέθοδο για να συμπιέσετε τις λίστες καταχωρίσεων και να αναδιοργανώσετε τις δομές αποθήκευσης. Αυτό το βήμα μπορεί να βελτιώσει την καθυστέρηση ερωτημάτων έως και **30 %** για μεγάλα ευρετήρια και βοηθά να διατηρηθεί το μέγεθος του ευρετηρίου διαχειρίσιμο.

## Συνηθισμένες περιπτώσεις χρήσης
- **Αποθετήρια νομικών εγγράφων:** Προσθέστε, ενημερώστε και διαγράψτε αρχεία υποθέσεων διατηρώντας υψηλή σχετικότητα για αναζητήσεις λέξεων-κλειδιών.  
- **Εταιρικές βάσεις γνώσης:** Κρατήστε εσωτερικά εγχειρίδια, πολιτικές και FAQ αναζητήσιμα καθώς εξελίσσονται.  
- **Κατάλογοι ηλεκτρονικού εμπορίου:** Ευρετηρίαση προδιαγραφών προϊόντων και αφαίρεση αντικειμένων που έχουν διακοπεί χωρίς διακοπές λειτουργίας.

## Αντιμετώπιση προβλημάτων & συμβουλές
- **Συμβουλή επαγγελματία:** Προσθέστε έγγραφα σε παρτίδες κατά τις ώρες χαμηλής κίνησης για να αποφύγετε αιχμές απόδοσης.  
- **Παγίδα:** Η παράλειψη του `optimize()` μετά από μαζικές διαγραφές μπορεί να οδηγήσει σε κατακερματισμένα ευρετήρια και πιο αργά ερωτήματα.  
- **Διαχείριση σφαλμάτων:** Τυλίξτε όλες τις λειτουργίες ευρετηρίου σε μπλοκ `try‑catch` για να διαχειρίζεστε ομαλά το `IndexException`.  
- **Συμβουλή απόδοσης:** Χρησιμοποιήστε `IndexSettings` για να ρυθμίσετε τη χρήση μνήμης όταν εργάζεστε με πολύ μεγάλα σύνολα δεδομένων (π.χ., ορίστε `maxMemoryUsage` σε υψηλότερη τιμή σε διακομιστές με άφθονη RAM).  
- **Ασφάλεια μνήμης:** Για αρχεία μεγαλύτερα από 500 MB, σκεφτείτε τη ροή εισόδου στο `addDocument` ώστε το αποτύπωμα της στοίβας JVM να παραμένει χαμηλό.

## Συχνές ερωτήσεις

**Q: Πώς αφαιρώ έγγραφα από το ευρετήριο;**  
A: Καλέστε `deleteDocument(documentId)` με το μοναδικό αναγνωριστικό· η καταχώρηση διαγράφεται άμεσα και ο χώρος αποθήκευσης ανακτάται.

**Q: Μπορώ να τροποποιήσω τα χαρακτηριστικά του εγγράφου για να βελτιώσω την ακρίβεια αναζήτησης;**  
A: Ναι, μπορείτε να ορίσετε προσαρμοσμένα μεταδεδομένα (π.χ., κατηγορία, συγγραφέας) μέσω του API χαρακτηριστικών του αντικειμένου `Document` πριν το προσθέσετε στο ευρετήριο.

**Q: Υπάρχει κάποιο “σεμινάριο ευρετηρίου αναζήτησης” για αρχάριους;**  
A: Η επίσημη τεκμηρίωση GroupDocs.Search περιλαμβάνει ένα βήμα‑βήμα σεμινάριο που καλύπτει τη δημιουργία ευρετηρίου, την προσθήκη εγγράφων και την εκτέλεση ερωτημάτων.

**Q: Υποστηρίζει το GroupDocs.Search την αναγνώριση ομοφώνων;**  
A: Η βιβλιοθήκη περιλαμβάνει γλωσσικά χαρακτηριστικά που βελτιώνουν την ακρίβεια για ομοφωνίες και παρόμοιες λέξεις.

**Q: Ποια έκδοση της Java απαιτείται για το πιο πρόσφατο GroupDocs.Search;**  
A: Απαιτείται Java 8 ή νεότερη· η βιβλιοθήκη είναι πλήρως συμβατή με Java 11 και νεότερες εκδόσεις LTS.

## Διαθέσιμα σεμινάρια

### [Πώς να ενημερώσετε και να διαχειριστείτε εκδόσεις ευρετηρίου στο GroupDocs.Search for Java: Ένας ολοκληρωμένος οδηγός](./guide-updating-index-versions-groupdocs-search-java/)
Μάθετε πώς να ενημερώνετε και να διαχειρίζεστε εκδόσεις ευρετηρίου χρησιμοποιώντας το GroupDocs.Search for Java. Αυτός ο οδηγός καλύπτει την ευρετηρίαση εγγράφων, τις ενημερώσεις εκδόσεων και τη βελτιστοποίηση απόδοσης.

### [Διαχείριση εγγράφων με το GroupDocs.Search for Java: Οδηγός αναγνώρισης ομοφώνων και ευρετηρίασης](./groupdocs-search-java-homophone-document-management-guide/)
Μάθετε πώς να διαχειρίζεστε έγγραφα χρησιμοποιώντας το GroupDocs.Search for Java, εστιάζοντας στην αναγνώριση ομοφώνων και την αποδοτική ευρετηρίαση. Βελτιώστε την ακρίβεια και την απόδοση της αναζήτησης.

### [Κατακτώντας τα χαρακτηριστικά εγγράφων με το GroupDocs.Search σε Java για βελτιωμένη ευρετηρίαση και διαχείριση](./groupdocs-search-java-modify-attributes-indexing/)
Μάθετε πώς να τροποποιείτε δυναμικά και να προσθέτετε χαρακτηριστικά εγγράφων χρησιμοποιώντας το GroupDocs.Search for Java. Βελτιώστε το σύστημα διαχείρισης εγγράφων σας με την κατάκτηση τεχνικών ευρετηρίασης.

### [Κατακτώντας το GroupDocs.Search σε Java: Πλήρης οδηγός διαχείρισης ευρετηρίου και αναζήτησης εγγράφων](./mastering-groupdocs-search-java-index-management-guide/)
Μάθετε πώς να διαχειρίζεστε αποτελεσματικά ευρετήρια εγγράφων με το GroupDocs.Search for Java. Ενισχύστε τις δυνατότητες αναζήτησης σας σε διάφορα έγγραφα, από νομικά έγγραφα μέχρι επιχειρηματικές αναφορές.

## Πρόσθετοι πόροι
- [Τεκμηρίωση GroupDocs.Search for Java](https://docs.groupdocs.com/search/java/)
- [Αναφορά API GroupDocs.Search for Java](https://reference.groupdocs.com/search/java/)
- [Λήψη GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- [Φόρουμ GroupDocs.Search](https://forum.groupdocs.com/c/search)
- [Δωρεάν υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία ενημέρωση:** 2026-10-12  
**Δοκιμή με:** GroupDocs.Search for Java 23.11  
**Συγγραφέας:** GroupDocs

## Σχετικά σεμινάρια
- [Πώς να ενημερώσετε το ευρετήριο Java με το GroupDocs.Search – Ένας ολοκληρωμένος οδηγός](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Πώς να δημιουργήσετε ευρετήριο εγγράφων και να προσθέσετε έγγραφα χρησιμοποιώντας το API GroupDocs.Search για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Πώς να προσθέσετε πολλαπλά ψευδώνυμα και έγγραφα στο ευρετήριο στο GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)