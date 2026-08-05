---
date: '2026-08-05'
description: Μάθετε πώς να κάνετε index έγγραφα Java γρήγορα με GroupDocs.Search for
  Java. Αυτός ο οδηγός καλύπτει την προσθήκη εγγράφων στο index, τη διαγραφή εγγράφων
  από το index και τη φόρτωση εγγράφων από το filesystem.
keywords:
- how to index java
- delete documents from index
- add documents to index
- java search performance
- GroupDocs.Search Java
lastmod: '2026-08-05'
og_description: Μάθετε πώς να κάνετε index έγγραφα java γρήγορα χρησιμοποιώντας GroupDocs.Search
  for Java, καλύπτοντας την προσθήκη, τη διαγραφή και την αναζήτηση αρχείων με υψηλή
  απόδοση.
og_image_alt: Developer guide showing Java code for indexing documents with GroupDocs.Search
og_title: πώς να κάνετε index java – fast document search με GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to index java documents quickly with GroupDocs.Search for
    Java. This guide covers adding documents to index, deleting documents from index,
    and loading documents from filesystem.
  headline: How to Index Java – Fast Document Search with GroupDocs
  type: TechArticle
- description: Learn how to index java documents quickly with GroupDocs.Search for
    Java. This guide covers adding documents to index, deleting documents from index,
    and loading documents from filesystem.
  name: How to Index Java – Fast Document Search with GroupDocs
  steps:
  - name: '**Enterprise document portals** – employees locate policies, contracts,
      or manuals in seconds.'
    text: '**Enterprise document portals** – employees locate policies, contracts,
      or manuals in seconds.'
  - name: '**Legal case management** – lawyers quickly find precedent clauses across
      thousands of PDFs and Word files.'
    text: '**Legal case management** – lawyers quickly find precedent clauses across
      thousands of PDFs and Word files.'
  - name: '**Digital libraries** – universities expose full‑text search over research
      papers and theses.'
    text: '**Digital libraries** – universities expose full‑text search over research
      papers and theses.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search supports a wide range of formats out of the box,
      handling over 50 file types without additional converters.
    question: Can I index PDFs, DOCX, and PPTX together?
  - answer: The `delete` method removes postings for the specified document keys and
      updates internal structures, so the index stays consistent without a full rebuild.
    question: How does “delete documents from index” work under the hood?
  - answer: Use `index.getStatistics()` to retrieve document count, total size, and
      other useful metrics.
    question: Is there a way to monitor index size?
  - answer: No. Deletions are incremental; only the affected entries are removed,
      and you can call `index.optimize()` periodically to keep performance optimal.
    question: Do I need to rebuild the whole index after each deletion?
  - answer: Create a new `Index` instance pointing to a different folder, add all
      documents again, and then switch your application to use the new index path.
    question: What if I need to re‑index all files after a schema change?
  type: FAQPage
tags:
- index java
- GroupDocs.Search
- Java document search
- search performance
- document indexing
title: Πώς να κάνετε index Java – Fast Document Search με GroupDocs
type: docs
url: /el/java/indexing/efficient-document-indexing-search-groupdocs-java/
weight: 1
---

# Πώς να Δεικτοδοτήσετε Java – Γρήγορη Αναζήτηση Εγγράφων με το GroupDocs

Αν αναρωτιέστε **πώς να δεικτοδοτήσετε java** αρχεία αποδοτικά, βρίσκεστε στο σωστό μέρος. Στον σημερινό κόσμο που βασίζεται στα δεδομένα, η γρήγορη εύρεση του σωστού εγγράφου μπορεί να εξοικονομήσει ώρες χειροκίνητης εργασίας. **GroupDocs.Search for Java** σας παρέχει έναν απλό τρόπο να μετατρέψετε έναν φάκελο αρχείων σε ένα αναζητήσιμο ευρετήριο, επιτρέποντάς σας να προσθέτετε έγγραφα στο ευρετήριο, να διαγράφετε έγγραφα από το ευρετήριο και να φορτώνετε έγγραφα από το σύστημα αρχείων με λίγες μόνο γραμμές κώδικα. Αυτό το σεμινάριο σας καθοδηγεί μέσα από τη ρύθμιση, τη δεικτοδότηση, την αναζήτηση και τον καθαρισμό, ώστε να ενσωματώσετε γρήγορη αναζήτηση εγγράφων σε οποιαδήποτε εφαρμογή Java.

## Γρήγορες απαντήσεις
- **Ποιος είναι ο κύριος σκοπός;** Να δεικτοδοτούνται και να αναζητούνται αποδοτικά έγγραφα Java.  
- **Ποια βιβλιοθήκη απαιτείται;** GroupDocs.Search for Java (v25.4+).  
- **Χρειάζομαι άδεια;** Διατίθεται δωρεάν δοκιμή ή προσωρινή άδεια· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Μπορώ να διαγράψω έγγραφα από το ευρετήριο;** Ναι, χρησιμοποιώντας τη μέθοδο `delete` με κλειδιά εγγράφων.  
- **Είναι το Apache Commons IO υποχρεωτικό;** Συνιστάται για βοηθητικά εργαλεία διαχείρισης αρχείων.

## Τι σημαίνει “πώς να δεικτοδοτήσετε java”;
Η δεικτοδότηση εγγράφων Java σημαίνει τη δημιουργία μιας αναζητήσιμης δομής δεδομένων (ευρετήριο) που αντιστοιχεί το περιεχόμενο του εγγράφου σε όρους αναζήτησης, επιτρέποντας γρήγορη ανάκτηση σχετικών αρχείων βάσει ερωτημάτων λέξεων‑κλειδιών. Δημιουργώντας αυτό το ευρετήριο μία φορά, οι επόμενες αναζητήσεις εκτελούνται σε χιλιοστά του δευτερολέπτου ακόμη και σε χιλιάδες αρχεία, βελτιώνοντας δραστικά την παραγωγικότητα των προγραμματιστών και την εμπειρία του τελικού χρήστη.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search for Java;
Το GroupDocs.Search υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** — συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, HTML και κοινών τύπων εικόνων — και μπορεί να επεξεργαστεί έγγραφα εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Οι βελτιστοποιημένοι αλγόριθμοί του παρέχουν απαντήσεις σε ερωτήματα κάτω από 100 ms για σύνολα δεδομένων έως 1 εκατομμύριο έγγραφα, καθιστώντας το μια κλιμακώσιμη επιλογή για επιχειρηματικές λύσεις αναζήτησης.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **GroupDocs.Search for Java** (έκδοση 25.4 ή νεότερη).  
- **Apache Commons IO** για βολικές βοηθητικές συναρτήσεις αρχείων.  
- JDK 8 ή νεότερο και ένα IDE όπως IntelliJ IDEA ή Eclipse.  
- Βασικές γνώσεις Java και, προαιρετικά, εξοικείωση με Maven.

## Ρύθμιση του GroupDocs.Search for Java

### Maven configuration
Προσθέστε το αποθετήριο και την εξάρτηση στο `pom.xml` σας:

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

> **Συμβουλή:** Διατηρήστε τον αριθμό έκδοσης συγχρονισμένο με την τελευταία κυκλοφορία για να επωφεληθείτε από βελτιώσεις απόδοσης.

### Direct download (if you prefer not to use Maven)

Μπορείτε επίσης να κατεβάσετε το τελευταίο JAR από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License acquisition
- **Δωρεάν δοκιμή:** Δοκιμάστε τη βιβλιοθήκη χωρίς κλειδί άδειας.  
- **Προσωρινή άδεια:** Ζητήστε μία για εκτεταμένη αξιολόγηση.  
- **Πλήρης άδεια:** Απαιτείται για παραγωγικές εγκαταστάσεις.

### Basic initialization
Δημιουργήστε μια απλή κλάση Java για να επαληθεύσετε ότι η βιβλιοθήκη φορτώνεται σωστά:

```java
import com.groupdocs.search.*;

public class DocumentIndexing {
    public static void main(String[] args) {
        Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\DeleteIndexedDocuments");
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

Η εκτέλεση αυτού του προγράμματος θα πρέπει να εκτυπώσει το μήνυμα επιβεβαίωσης, υποδεικνύοντας ότι ο φάκελος του ευρετηρίου είναι έτοιμος.

## Πώς να προσθέσετε έγγραφα στο ευρετήριο

Η κλάση `Document` αντιπροσωπεύει μια αναζητήσιμη οντότητα που περιέχει το δυαδικό περιεχόμενο του αρχείου και τα μεταδεδομένα του.  
Για να προσθέσετε ένα έγγραφο, δημιουργήστε ένα στιγμιότυπο `Document` που τυλίγει τα byte του αρχείου και αναθέτει ένα μοναδικό κλειδί, στη συνέχεια καλέστε `index.add(document)`. Η βιβλιοθήκη εξάγει το κείμενο, το τοκενίζει και αποθηκεύει τις αναρτήσεις στον φάκελο του ευρετηρίου αυτόματα. Η λειτουργία αυτή εκτελείται σε γραμμικό χρόνο σε σχέση με το μέγεθος του αρχείου και υποστηρίζει lazy loading για μεγάλα αρχεία.  

**Άμεση απάντηση:**  

```java
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\DeleteIndexedDocuments", true);
```
- Το πρώτο όρισμα είναι ο φάκελος όπου θα αποθηκευτούν τα αρχεία του ευρετηρίου.  
- Το δεύτερο όρισμα (`true`) λέει στο GroupDocs να δημιουργήσει τον φάκελο αν δεν υπάρχει και να ενημερώσει αυτόματα ένα υπάρχον ευρετήριο.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY\\English.docx";
DocumentLoader documentLoader = new DocumentLoader(filePath);
Document document = Document.createLazy(DocumentSourceKind.Stream, documentLoader.getDocumentKey(), documentLoader);
Document[] documents = new Document[]{document};
index.add(documents, new IndexingOptions());
```
- `DocumentLoader` (ορίζεται παρακάτω) διαβάζει το αρχείο και παρέχει ένα μοναδικό κλειδί.  
- `createLazy` εξασφαλίζει ότι τα μεγάλα αρχεία επεξεργάζονται αποδοτικά, φορτώνοντας το περιεχόμενο μόνο όταν χρειάζεται.

## Πώς να φορτώσετε έγγραφα από το σύστημα αρχείων

Η βοηθητική κλάση `DocumentLoader` διαβάζει ένα αρχείο από το δίσκο και δημιουργεί το αντίστοιχο αντικείμενο `Document` με έναν σταθερό ταυτοποιητή.  
Για να φορτώσετε αρχεία, ο φορτωτής διαβάζει τα byte του αρχείου, δημιουργεί ένα μοναδικό κλειδί (π.χ. ένα hash του μονοπατιού) και κατασκευάζει ένα στιγμιότυπο `Document`. Αυτό το αντικείμενο μπορεί στη συνέχεια να περάσει στο `index.add(document)`. Η χρήση ενός αφιερωμένου φορτωτή απομονώνει τις ανησυχίες του συστήματος αρχείων, καθιστώντας τον κώδικα δεικτοδότησης επαναχρησιμοποιήσιμο και πιο εύκολο στη δοκιμή σε διαφορετικά αποθηκευτικά back‑ends.  

**Άμεση απάντηση:**  

```java
class DocumentLoader {
    private final String filePath;
    private final String documentKey;

    public DocumentLoader(String filePath) {
        this.filePath = filePath;
        documentKey = FilenameUtils.getName(filePath);
    }

    public String getDocumentKey() { return documentKey; }

    public Document loadDocument() throws IOException {
        Path path = Paths.get(filePath);
        byte[] buffer = Files.readAllBytes(path);
        ByteArrayInputStream stream = new ByteArrayInputStream(buffer);
        return Document.createFromStream(documentKey, new Date(System.currentTimeMillis()), "." + FilenameUtils.getExtension(filePath), stream);
    }
}
```

## Πώς να εκτελέσετε αναζήτηση λέξεων‑κλειδιών σε ένα ευρετήριο

Η κλάση `SearchQuery` περιλαμβάνει τη συμβολοσειρά ερωτήματος του χρήστη, ενώ η `SearchResult` περιέχει τα αναγνωριστικά των εγγράφων που ταιριάζουν, αποσπάσματα και βαθμολογίες συνάφειας.  
Δημιουργήστε ένα `SearchQuery` με τις επιθυμητές λέξεις‑κλειδιά και προαιρετικά ρυθμίστε fuzzy matching ή φίλτρα, στη συνέχεια καλέστε `index.search(query)`. Η μέθοδος επιστρέφει ένα αντικείμενο `SearchResult` που περιέχει το αναγνωριστικό κάθε ταιριαστού εγγράφου, επισημασμένα αποσπάσματα και μια βαθμολογία συνάφειας. Μπορείτε να επαναλάβετε τα αποτελέσματα για να εμφανίσετε αποσπάσματα ή να επεξεργαστείτε περαιτέρω τις αντιστοιχίες.  

**Άμεση απάντηση:**  

```java
String query = "moment";
SearchResult searchResult1 = index.search(query);
```
- Περνάτε οποιαδήποτε συμβολοσειρά κειμένου στο `search` και λαμβάνετε ένα `SearchResult` που περιέχει τα αναγνωριστικά εγγράφων, αποσπάσματα και βαθμολογίες συνάφειας.

## Πώς να διαγράψετε έγγραφα από το ευρετήριο

Η κλάση `UpdateOptions` σας επιτρέπει να ελέγξετε πώς εφαρμόζονται αλλαγές όπως διαγραφές στο ευρετήριο.  
Παρέχετε τα μοναδικά κλειδιά των εγγράφων στο `index.delete(keys)`, και η βιβλιοθήκη αφαιρεί όλες τις αναρτήσεις που σχετίζονται με αυτά τα κλειδιά. Μπορείτε να περάσετε ένα στιγμιότυπο `UpdateOptions` για να καθορίσετε αν οι διαγραφές εφαρμόζονται άμεσα ή ομαδοποιημένα για καλύτερη απόδοση. Μετά τη διαγραφή, το ευρετήριο παραμένει συνεπές χωρίς ανάγκη πλήρους επαναδημιουργίας.  

**Άμεση απάντηση:**  

```java
String[] documentKeys = new String[]{documentLoader.getDocumentKey()};
DeleteResult deleteResult = index.delete(new UpdateOptions(), documentKeys);
```
- Παρέχετε τα κλειδιά των εγγράφων που θέλετε να αφαιρέσετε.  
- Το `UpdateOptions` σας επιτρέπει να ελέγξετε πώς εφαρμόζεται η διαγραφή (π.χ. άμεση vs. ομαδική).

## Πώς να ανακτήσετε τα έγγραφα που είναι ακόμη στο ευρετήριο μετά από διαγραφές

Η μέθοδος `getDocumentList()` επιστρέφει μια συλλογή όλων των αναγνωριστικών εγγράφων που είναι αυτή τη στιγμή αποθηκευμένα στο ευρετήριο.  
Καλώντας `index.getDocumentList()` λαμβάνετε το τρέχον σύνολο κλειδιών εγγράφων, το οποίο αντικατοπτρίζει όλες τις προσθήκες και διαγραφές που έχουν πραγματοποιηθεί μέχρι τώρα. Αυτή η λίστα μπορεί να χρησιμοποιηθεί για να επαληθεύσετε ότι ανεπιθύμητες καταχωρήσεις έχουν αφαιρεθεί επιτυχώς ή για να επαναλάβετε τα υπόλοιπα έγγραφα για περαιτέρω επεξεργασία. Είναι μια ελαφριά λειτουργία που δεν τροποποιεί το ευρετήριο.  

**Άμεση απάντηση:**  

```java
DocumentInfo[] indexedDocuments2 = index.getIndexedDocuments();
```
- Αυτή η κλήση επιστρέφει τη τρέχουσα λίστα εγγράφων που εξακολουθούν να υπάρχουν στο ευρετήριο, βοηθώντας σας να επαληθεύσετε ότι οι διαγραφές ήταν επιτυχείς.

## Συμβουλές απόδοσης αναζήτησης Java

Η βελτιστοποίηση **java search performance** περιλαμβάνει τρεις βασικές ενέργειες: (1) εκτελέστε `index.optimize()` μετά από μαζικές εισαγωγές ή διαγραφές για να συμπιέσετε τα αρχεία αναρτήσεων, (2) ενεργοποιήστε lazy loading για αρχεία μεγαλύτερα από 10 MB ώστε να αποφύγετε σφάλματα OutOfMemory, και (3) διαθέστε επαρκή heap στη JVM (π.χ. `-Xmx2g` για μεσαίου μεγέθους φορτία). Ακολουθώντας αυτές τις πρακτικές διατηρείτε τη λανθάνοντα ερώτησης κάτω από 100 ms ακόμη και καθώς το ευρετήριο μεγαλώνει.

## Πρακτικές εφαρμογές

Το GroupDocs.Search for Java διαπρέπει σε σενάρια όπως:

1. **Εταιρικές πύλες εγγράφων** – οι εργαζόμενοι εντοπίζουν πολιτικές, συμβάσεις ή εγχειρίδια σε δευτερόλεπτα.  
2. **Διαχείριση νομικών υποθέσεων** – οι δικηγόροι βρίσκουν γρήγορα σχετικές ρήτρες σε χιλιάδες PDF και Word αρχεία.  
3. **Ψηφιακές βιβλιοθήκες** – τα πανεπιστήμια προσφέρουν πλήρη αναζήτηση κειμένου σε ερευνητικές εργασίες και διπλωματικές.

## Συχνά προβλήματα και λύσεις

| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| Δεν επιστρέχονται αποτελέσματα | Οι όροι ερωτήματος δεν έχουν δεικτοδοτηθεί ή τα stop‑words έχουν φιλτραριστεί | Ελέγξτε τις `IndexingOptions` και προσαρμόστε τη λίστα stop‑words |
| Σφάλματα Out‑of‑memory | Μεγάλα αρχεία φορτώνονται άμεσα | Μεταβείτε σε `Document.createLazy` ή αυξήστε το heap της JVM |
| Τα διαγραμμένα έγγραφα εμφανίζονται ακόμα | Το ευρετήριο δεν έχει ανανεωθεί μετά τη διαγραφή | Καλέστε `index.optimize()` ή ανοίξτε ξανά το αντικείμενο ευρετηρίου |

## Συχνές ερωτήσεις

**Ε: Μπορώ να δεικτοδοτήσω PDFs, DOCX και PPTX μαζί;**  
Α: Ναι, το GroupDocs.Search υποστηρίζει ευρύ φάσμα μορφών έτοιμο για χρήση, επεξεργαζόμενο πάνω από 50 τύπους αρχείων χωρίς πρόσθετους μετατροπείς.

**Ε: Πώς λειτουργεί η “διαγραφή εγγράφων από το ευρετήριο” εσωτερικά;**  
Α: Η μέθοδος `delete` αφαιρεί τις αναρτήσεις για τα συγκεκριμένα κλειδιά εγγράφων και ενημερώνει τις εσωτερικές δομές, ώστε το ευρετήριο να παραμένει συνεπές χωρίς πλήρη επαναδημιουργία.

**Ε: Υπάρχει τρόπος να παρακολουθήσω το μέγεθος του ευρετηρίου;**  
Α: Χρησιμοποιήστε `index.getStatistics()` για να λάβετε τον αριθμό εγγράφων, το συνολικό μέγεθος και άλλες χρήσιμες μετρήσεις.

**Ε: Πρέπει να ξαναδημιουργήσω ολόκληρο το ευρετήριο μετά από κάθε διαγραφή;**  
Α: Όχι. Οι διαγραφές είναι επαυξητικές· αφαιρούνται μόνο οι επηρεαζόμενες καταχωρήσεις, και μπορείτε να καλέσετε `index.optimize()` περιοδικά για να διατηρήσετε την απόδοση βέλτιστη.

**Ε: Τι κάνω αν πρέπει να ξανα‑δείκτοδοτήσω όλα τα αρχεία μετά από αλλαγή σχήματος;**  
Α: Δημιουργήστε ένα νέο αντικείμενο `Index` που δείχνει σε διαφορετικό φάκελο, προσθέστε ξανά όλα τα έγγραφα και, στη συνέχεια, μεταβείτε στην εφαρμογή σας ώστε να χρησιμοποιεί τη νέα διαδρομή ευρετηρίου.

## Συμπέρασμα

Τώρα έχετε έναν πλήρη οδηγό για **πώς να δεικτοδοτήσετε java** έγγραφα χρησιμοποιώντας το GroupDocs.Search for Java — από τη ρύθμιση του περιβάλλοντος, την προσθήκη εγγράφων στο ευρετήριο, τη φόρτωση από το σύστημα αρχείων, την εκτέλεση αναζητήσεων, μέχρι τη διαγραφή και επαλήθευση του περιεχομένου του ευρετηρίου. Ενσωματώνοντας αυτά τα βήματα στην εφαρμογή σας, θα βελτιώσετε δραστικά την ανακάλυψη εγγράφων, θα μειώσετε το χρόνο αναζήτησης και θα αυξήσετε τη συνολική παραγωγικότητα.

**Επόμενα βήματα:**  
- Πειραματιστείτε με σύνθετα ερωτήματα (wildcards, fuzzy matching).  
- Εξερευνήστε προχωρημένα χαρακτηριστικά όπως faceted search, προσαρμοσμένους αναλυτές και δεικτοδότηση μεταδεδομένων.  

Καλή δεικτοδότηση!

---

**Τελευταία ενημέρωση:** 2026-08-05  
**Δοκιμάστηκε με:** GroupDocs.Search Java 25.4  
**Συγγραφέας:** GroupDocs

## Σχετικά Tutorials

- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [How to Add Documents to Index and Manage Aliases in GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
- [Master GroupDocs.Search Java: Efficient Document Search and Index Management](/search/java/searching/groupdocs-search-java-efficient-document-search/)