---
date: '2026-10-02'
description: Μάθετε πώς να χρησιμοποιήσετε μια temporary license για να προσθέσετε
  έγγραφα στο ευρετήριο με chunk‑based search σε Java, ενισχύοντας την απόδοση της
  αναζήτησης ενώ ελέγχετε τη memory usage.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Χρησιμοποιήστε μια temporary license για να προσθέσετε έγγραφα στο
  ευρετήριο με chunk‑based search σε Java, βελτιώνοντας την ταχύτητα της αναζήτησης
  και μειώνοντας την memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Χρησιμοποιήστε μια temporary license για chunk‑based indexing σε Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Χρησιμοποιήστε μια temporary license για chunk‑based indexing σε Java
type: docs
url: /el/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Χρησιμοποιήστε προσωρινή άδεια για ευρετηρίαση με βάση τα τμήματα σε Java

Σε αυτό το εκπαιδευτικό υλικό θα **χρησιμοποιήσετε μια προσωρινή άδεια** για να προσθέσετε έγγραφα στο ευρετήριο με τη λειτουργία αναζήτησης με βάση τα τμήματα του GroupDocs.Search. Η προσέγγιση σας επιτρέπει να διαχειρίζεστε τεράστιες συλλογές εγγράφων—νομικά συμβόλαια, αιτήματα υποστήριξης, ερευνητικές εργασίες—διατηρώντας χαμηλή χρήση **java search index memory** και **αυξάνοντας δραματικά την απόδοση της αναζήτησης**. Θα δείτε πώς να ρυθμίσετε το φάκελο του ευρετηρίου, να τροφοδοτήσετε πολλαπλές πηγές εγγράφων, να ενεργοποιήσετε την αναζήτηση τμημάτων και να εκτελέσετε τόσο την πρώτη όσο και τις επόμενες ερωτήσεις τμημάτων.

## Γρήγορες Απαντήσεις
- **Ποιο είναι το πρώτο βήμα;** Δημιουργήστε ένα φάκελο ευρετηρίου αναζήτησης.  
- **Πώς μπορώ να συμπεριλάβω πολλά αρχεία;** Χρησιμοποιήστε `index.add()` για κάθε φάκελο εγγράφων.  
- **Ποια επιλογή ενεργοποιεί την αναζήτηση τμημάτων;** `options.setChunkSearch(true)`.  
- **Μπορώ να συνεχίσω την αναζήτηση μετά το πρώτο τμήμα;** Ναι, καλέστε `index.searchNext()` με το token.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή ή προσωρινή άδεια λειτουργεί για ανάπτυξη· απαιτείται πλήρης άδεια για παραγωγή.  

## Τι θα μάθετε
- Πώς να δημιουργήσετε ένα ευρετήριο αναζήτησης σε καθορισμένο φάκελο.  
- Βήματα για **προσθήκη εγγράφων στο ευρετήριο** από πολλαπλές τοποθεσίες.  
- Διαμόρφωση επιλογών αναζήτησης για ενεργοποίηση της αναζήτησης με βάση τα τμήματα.  
- Εκτέλεση αρχικών και επόμενων αναζητήσεων με βάση τα τμήματα.  
- Πραγματικά σενάρια όπου η αναζήτηση εγγράφων με βάση τα τμήματα διαπρέπει.  

## Προαπαιτούμενα
- **Απαιτούμενες βιβλιοθήκες**: GroupDocs.Search for Java 25.4 ή νεότερη.  
- **Ρύθμιση περιβάλλοντος**: Ένα συμβατό Java Development Kit (JDK) εγκατεστημένο.  
- **Προαπαιτούμενες γνώσεις**: Βασικός προγραμματισμός Java και εξοικείωση με Maven.  

## Ρύθμιση του GroupDocs.Search για Java
Για να ξεκινήσετε, ενσωματώστε το GroupDocs.Search στο έργο σας χρησιμοποιώντας Maven:

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

Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση από [Κυκλοφορίες GroupDocs.Search για Java](https://releases.groupdocs.com/search/java/).

### Απόκτηση άδειας
Για να δοκιμάσετε το GroupDocs.Search:
- **Δωρεάν δοκιμή** – δοκιμάστε τις βασικές λειτουργίες χωρίς δέσμευση.  
- **Προσωρινή άδεια** – εκτεταμένη πρόσβαση για ανάπτυξη.  
- **Αγορά** – πλήρης άδεια για χρήση σε παραγωγή.  

## Πώς να προσθέσετε έγγραφα στο ευρετήριο;
**Άμεση απάντηση:** Καλέστε `index.add()` για κάθε φάκελο που περιέχει αρχεία που θέλετε να είναι αναζητήσιμα· η μέθοδος σαρώσει το φάκελο αναδρομικά και προσθέτει κάθε υποστηριζόμενο έγγραφο στο ευρετήριο με μια ενιαία λειτουργία. Αυτό εξαλείφει την ανάγκη χειροκίνητης επεξεργασίας αρχείου‑αρχείου και επιταχύνει την μαζική εισαγωγή.

`SearchIndex` είναι η κεντρική κλάση που αντιπροσωπεύει τη συλλογή αναζητήσιμων δεδομένων στον δίσκο. Αφού την δημιουργήσετε, όλες οι λειτουργίες ευρετηρίου και ερωτημάτων περνούν μέσω αυτού του αντικειμένου.

### 1. Δημιουργία ευρετηρίου
**Άμεση απάντηση:** Δημιουργήστε ένα αντικείμενο `SearchIndex` με τη διαδρομή όπου πρέπει να αποθηκευτούν τα αρχεία του ευρετηρίου, στη συνέχεια καλέστε `index.create()` για να αρχικοποιήσετε τη δομή αποθήκευσης. Η κλήση δημιουργεί τους απαραίτητους φακέλους και τα αρχεία μεταδεδομένων κατά την πρώτη χρήση.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Προσθήκη εγγράφων στο ευρετήριο
**Άμεση απάντηση:** Χρησιμοποιήστε τη μέθοδο `index.add()` και περάστε την απόλυτη διαδρομή κάθε φακέλου προέλευσης· το API ανιχνεύει αυτόματα τις υποστηριζόμενες μορφές (PDF, DOCX, XLSX, κ.λπ.) και εξάγει το αναζητήσιμο κείμενο στο ευρετήριο.

`SearchOptions` είναι ένα αντικείμενο διαμόρφωσης που σας επιτρέπει να ρυθμίσετε λεπτομερώς πώς επεξεργάζονται τα έγγραφα κατά την ευρετηρίαση και την αναζήτηση. Θα το χρησιμοποιήσετε αργότερα για να ενεργοποιήσετε ερωτήματα με βάση τα τμήματα.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```
```java
Index index = new Index(indexFolder);
```

### 3. Διαμόρφωση επιλογών αναζήτησης για αναζήτηση τμημάτων
**Άμεση απάντηση:** Ορίστε `options.setChunkSearch(true)` σε μια παρουσία του `SearchOptions` πριν εκτελέσετε ένα ερώτημα· αυτό ενημερώνει τη μηχανή να χωρίσει κάθε έγγραφο σε λογικά τμήματα (συνήθως παραγράφους) και να επιστρέφει τα αποτελέσματα ανά τμήμα αντί για ολόκληρο το αρχείο.

`SearchResult` περιέχει τα τμήματα που ταιριάζουν, τις θέσεις τους και τις βαθμολογίες συνάφειας. Όταν η αναζήτηση τμημάτων είναι ενεργή, κάθε `SearchResult` αντιστοιχεί σε ένα μόνο απόσπασμα του αρχικού εγγράφου.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```
```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Εκτέλεση αρχικής αναζήτησης με βάση τα τμήματα
**Άμεση απάντηση:** Εκτελέστε `index.search("your query", options)`· η κλήση επιστρέφει μια συλλογή `SearchResult` για το πρώτο σύνολο τμημάτων που ταιριάζουν και ένα token που αντιπροσωπεύει την κατάσταση της αναζήτησης για συνέχιση.

Το επιστρεφόμενο token είναι απαραίτητο για την πλοήγηση σε μεγάλα σύνολα αποτελεσμάτων χωρίς να εκτελείται ξανά ολόκληρο το ερώτημα.

```java
SearchOptions options = new SearchOptions();
```
```java
options.setChunkSearch(true);
```

### 5. Συνέχιση αναζήτησης με βάση τα τμήματα
**Άμεση απάντηση:** Περάστε το token που επιστράφηκε από την προηγούμενη κλήση στο `index.searchNext(token, options)`· επαναλάβετε μέχρι η μέθοδος να επιστρέψει `null`, υποδεικνύοντας ότι έχουν ανακτηθεί όλα τα ταιριαστά τμήματα.

Αυτή η επαναληπτική προσέγγιση διατηρεί τη χρήση μνήμης χαμηλή, επειδή μόνο η τρέχουσα παρτίδα τμημάτων βρίσκεται στη μνήμη.

```java
String query = "invitation";
```
```java
SearchResult result = index.search(query, options);
```

## Γιατί να χρησιμοποιήσετε αναζήτηση με βάση τα τμήματα;
Η αναζήτηση με βάση τα τμήματα διασπά τεράστιες συλλογές εγγράφων σε διαχειρίσιμα κομμάτια, μειώνοντας την πίεση στη μνήμη και επιταχύνοντας τους χρόνους απόκρισης. Με την ευρετηρίαση σε επίπεδο παραγράφου ή ενότητας, η μηχανή μπορεί να ανακτήσει μόνο τα σχετικά αποσπάσματα, μειώνοντας τη χρήση CPU και βελτιώνοντας την καθυστέρηση για τους τελικούς χρήστες. Είναι ιδιαίτερα ωφέλιμη όταν:

1. **Οι νομικές ομάδες** χρειάζονται να εντοπίσουν συγκεκριμένες ρήτρες σε χιλιάδες συμβόλαια.  
2. **Οι πύλες εξυπηρέτησης πελατών** πρέπει να εμφανίζουν άμεσα σχετικά άρθρα βάσης γνώσεων.  
3. **Οι ερευνητές** εξετάζουν εκτενείς σύνολα δεδομένων χωρίς να φορτώνουν ολόκληρα αρχεία στη μνήμη.  

Περιορισμένη δήλωση: Το GroupDocs.Search μπορεί να επεξεργαστεί **PDF με πάνω από 500 σελίδες** σε λιγότερο από **2 δευτερόλεπτα ανά τμήμα** σε έναν τυπικό διακομιστή 8‑πυρήνων, διατηρώντας το μέγιστο heap κάτω από **200 MB**.

## Πώς αυτή η προσέγγιση αυξάνει την απόδοση της αναζήτησης
**Άμεση απάντηση:** Αναζητώντας μικρότερα τμήματα αντί για ολόκληρα αρχεία, η μηχανή μπορεί να παραλείψει άσχετες ενότητες νωρίς, να μειώσει τους κύκλους CPU και να διατηρεί μόνο το ενεργό τμήμα στη μνήμη, κάτι που μειώνει άμεσα την κατανάλωση **java search index memory** και προσφέρει ταχύτερους χρόνους απόκρισης. Αυτή η στοχευμένη προσέγγιση επιτρέπει επίσης πιο αποτελεσματική προσωρινή αποθήκευση (caching) και παράλληλη επεξεργασία, επιτρέποντας σε πολλούς πυρήνες να διαχειρίζονται διαφορετικά τμήματα ταυτόχρονα, βελτιώνοντας περαιτέρω τη διαμεριστική ικανότητα σε διακομιστές πολλαπλών πυρήνων.

- Παράλληλη επεξεργασία τμημάτων σε πολλαπλούς πυρήνες.  
- Πρόωρη διακοπή όταν βρεθεί ένα αποτέλεσμα υψηλής συνάφειας.  

## Διαχείριση μνήμης java search index
**Άμεση απάντηση:** Κατανείμετε επαρκή heap JVM (π.χ., `-Xmx2g` ή μεγαλύτερο) ανάλογα με το αναμενόμενο μέγεθος του ευρετηρίου, εκτελέστε `index.optimize()` μετά από μαζικές προσθήκες για να συμπιέσετε τη δομή του ευρετηρίου και παρακολουθήστε τις παύσεις GC με το VisualVM για να αποφύγετε αιχμές καθυστέρησης.

- Χρησιμοποιήστε `index.flush()` μετά από μεγάλες παρτίδες για να γράψετε ενδιάμεσα δεδομένα στο δίσκο.  
- Ενεργοποιήστε `options.setMemoryLimit(256)` για να περιορίσετε τη μνήμη ανά αναζήτηση.  

## Σκέψεις απόδοσης
- **Διαχείριση μνήμης** – Κατανείμετε επαρκή χώρο heap (`-Xmx`) για μεγάλα ευρετήρια.  
- **Παρακολούθηση πόρων** – Παρακολουθείτε τη χρήση CPU κατά τη διάρκεια της ευρετηρίασης και των λειτουργιών αναζήτησης.  
- **Συντήρηση ευρετηρίου** – Επαναδημιουργήστε ή καθαρίστε περιοδικά το ευρετήριο για να απορρίψετε παλιά δεδομένα.  

## Συνηθισμένα προβλήματα & αντιμετώπιση
| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| `OutOfMemoryError` during indexing | Το μέγεθος heap είναι πολύ μικρό | Αυξήστε το heap της JVM (`-Xmx2g` ή μεγαλύτερο) |
| No results returned | Το token τμήματος δεν επεξεργάζεται | Βεβαιωθείτε ότι ο βρόχος `while` εκτελείται μέχρι το `getNextChunkSearchToken()` να είναι `null` |
| Slow search performance | Το ευρετήριο δεν είναι βελτιστοποιημένο | Εκτελέστε `index.optimize()` μετά από μαζικές προσθήκες |

## Συχνές ερωτήσεις
**Q: Τι είναι η αναζήτηση με βάση τα τμήματα;**  
A: Η αναζήτηση με βάση τα τμήματα διαιρεί το σύνολο δεδομένων σε μικρότερα κομμάτια, επιτρέποντας αποδοτικά ερωτήματα σε μεγάλα όγκους δεδομένων χωρίς τη φόρτωση ολόκληρων εγγράφων στη μνήμη.

**Q: Πώς ενημερώνω το ευρετήριό μου με νέα αρχεία;**  
A: Απλώς καλέστε `index.add()` με τη διαδρομή προς τα νέα έγγραφα· το ευρετήριο θα τα ενσωματώσει αυτόματα.

**Q: Μπορεί το GroupDocs.Search να διαχειριστεί διαφορετικές μορφές αρχείων;**  
A: Ναι, υποστηρίζει **PDF, DOCX, XLSX, PPTX, HTML, TXT και πάνω από 30 άλλες μορφές**.

**Q: Ποια είναι τα τυπικά εμπόδια στην απόδοση;**  
A: Οι περιορισμοί μνήμης και τα μη βελτιστοποιημένα ευρετήρια είναι τα πιο συνηθισμένα· κατανείμετε επαρκές heap και βελτιστοποιήστε τακτικά το ευρετήριο.

**Q: Πού μπορώ να βρω πιο λεπτομερή τεκμηρίωση;**  
A: Επισκεφθείτε την επίσημη [Τεκμηρίωση GroupDocs.Search](https://docs.groupdocs.com/search/java/) για αναλυτικούς οδηγούς και αναφορές API.

**Q: Λειτουργεί η αναζήτηση με βάση τα τμήματα με κρυπτογραφημένα PDF;**  
A: Ναι, εφόσον παρέχετε τον κωδικό πρόσβασης μέσω του κατάλληλου υπερφορτωμένου API.

**Q: Πώς μπορώ να παρακολουθήσω την πρόοδο της ευρετηρίασης;**  
A: Χρησιμοποιήστε το υπερφορτωμένο `Index.add()` που επιστρέφει ένα αντικείμενο `Progress` ή συνδέστε σε callbacks καταγραφής.

## Πόροι
- **Τεκμηρίωση**: [Τεκμηρίωση GroupDocs.Search για Java](https://docs.groupdocs.com/search/java/)  
- **Αναφορά API**: [Αναφορά API GroupDocs.Search](https://reference.groupdocs.com/search/java)  
- **Λήψη**: [Κυκλοφορίες GroupDocs.Search](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [Αποθετήριο GitHub GroupDocs.Search](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Δωρεάν υποστήριξη**: [Φόρουμ GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Προσωρινή άδεια**: [Απόκτηση προσωρινής άδειας](https://purchase.groupdocs.com/temporary-license)

---

**Τελευταία ενημέρωση:** 2026-10-02  
**Δοκιμάστηκε με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Σχετικά Μαθήματα

- [Δημιουργία καταλόγου ευρετηρίου αναζήτησης & ρύθμιση άδειας – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Βελτίωση απόδοσης ερωτημάτων με GroupDocs.Search Java: Βελτιστοποίηση ευρετηρίου & αναζήτησης](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java Προηγμένες δυνατότητες αναζήτησης](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)