---
date: '2026-08-15'
description: Μάθετε ένα παράδειγμα αναζήτησης πλήρους κειμένου σε Java με το GroupDocs.Search,
  καλύπτοντας την προσθήκη εγγράφων στο ευρετήριο, το boolean query java και τη βελτιστοποίηση
  απόδοσης.
keywords:
- full text search example
- add documents to index
- boolean query java
lastmod: '2026-08-15'
og_description: Εξερευνήστε ένα παράδειγμα αναζήτησης πλήρους κειμένου σε Java με
  το GroupDocs.Search. Μάθετε πώς να προσθέτετε έγγραφα στο ευρετήριο, να δημιουργείτε
  δηλώσεις boolean query java και να ενισχύετε την απόδοση της αναζήτησης.
og_image_alt: Guide showing how to implement a full text search example in Java with
  GroupDocs.Search
og_title: Παράδειγμα αναζήτησης πλήρους κειμένου σε Java χρησιμοποιώντας το GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  headline: Full text search example in Java using GroupDocs.Search
  type: TechArticle
- description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  name: Full text search example in Java using GroupDocs.Search
  steps:
  - name: create an index
    text: The `Index` class is the searchable container that stores indexed documents
      on disk.
  - name: add documents (add documents to index)
    text: You can index everything in a folder or limit to certain extensions using
      a `DocumentFilter`. > **Explanation:** > - `Index` represents the searchable
      database. > - `add()` ingests files; the wildcard `*.*` grabs all files, while
      `DocumentFilter` lets you fine‑tune the **add documents to index** ste
  - name: execute the search
    text: '> **Explanation:** > - `search()` runs the query against the index. > -
      `getDocumentCount()` tells you how many documents matched—useful for quick sanity
      checks.'
  type: HowTo
- questions:
  - answer: It indexes the raw text of every document so you can query any word or
      phrase instantly.
    question: What is full text search example?
  - answer: GroupDocs.Search for Java handles PDF, DOCX, XLSX, PPTX, HTML, TXT, and
      over 50 other file types.
    question: Which library supports multiple formats?
  - answer: Call the `index.add()` method with a folder path or a custom `DocumentFilter`.
    question: How do I add documents to index?
  - answer: Yes—combine terms with AND, OR, NOT for precise results.
    question: Can I run Boolean queries?
  - answer: Use incremental indexing, enable result caching, and disable phonetic
      search unless needed.
    question: How do I improve performance?
  type: FAQPage
tags:
- full text search
- GroupDocs.Search
- Java document indexing
- search performance
title: Παράδειγμα αναζήτησης πλήρους κειμένου σε Java χρησιμοποιώντας το GroupDocs.Search
type: docs
url: /el/java/searching/implement-full-text-search-java-groupdocs-search/
weight: 1
---

# Παράδειγμα πλήρους αναζήτησης κειμένου σε Java με GroupDocs.Search

Αν χρειάζεστε ένα **παράδειγμα πλήρους αναζήτησης κειμένου** που λειτουργεί σε PDF, αρχεία Word, υπολογιστικά φύλλα και άλλα, βρίσκεστε στο σωστό μέρος. Η χειροκίνητη σάρωση χιλιάδων εγγράφων αποτελεί μεγάλο εμπόδιο, αλλά το GroupDocs.Search για Java αυτοματοποιεί την ευρετηρίαση και την εκτέλεση ερωτημάτων με αστραπιαία ταχύτητα. Σε αυτό το tutorial θα καλύψουμε όλα όσα χρειάζεστε για να ξεκινήσετε — από την προσθήκη εγγράφων στο ευρετήριο, τη δημιουργία boolean ερωτημάτων Java, μέχρι τη βελτιστοποίηση της απόδοσης αναζήτησης για παραγωγικά φορτία.

## Σύντομες απαντήσεις
- **Τι είναι το παράδειγμα πλήρους αναζήτησης κειμένου;** Ευρετηριάζει το ακατέργαστο κείμενο κάθε εγγράφου ώστε να μπορείτε να ερωτήσετε οποιαδήποτε λέξη ή φράση άμεσα.  
- **Ποια βιβλιοθήκη υποστηρίζει πολλαπλές μορφές;** Το GroupDocs.Search για Java διαχειρίζεται PDF, DOCX, XLSX, PPTX, HTML, TXT και πάνω από 50 άλλους τύπους αρχείων.  
- **Πώς προσθέτω έγγραφα στο ευρετήριο;** Καλέστε τη μέθοδο `index.add()` με διαδρομή φακέλου ή ένα προσαρμοσμένο `DocumentFilter`.  
- **Μπορώ να εκτελέσω Boolean ερωτήματα;** Ναι — συνδυάστε όρους με AND, OR, NOT για ακριβή αποτελέσματα.  
- **Πώς βελτιώνω την απόδοση;** Χρησιμοποιήστε επαυξητική (incremental) ευρετηρίαση, ενεργοποιήστε την προσωρινή αποθήκευση αποτελεσμάτων και απενεργοποιήστε την φωνητική αναζήτηση εκτός εάν είναι απαραίτητη.

## Τι είναι το παράδειγμα πλήρους αναζήτησης κειμένου;
Ένα παράδειγμα πλήρους αναζήτησης κειμένου σας επιτρέπει να σαρώσετε όλο το κειμενικό περιεχόμενο των εγγράφων, να το αποθηκεύσετε σε ένα αποδοτικό ευρετήριο και να ανακτήσετε τα αντίστοιχα αρχεία άμεσα. Σε αντίθεση με τις αναζητήσεις μόνο με βάση το όνομα αρχείου, ψάχνει μέσα σε PDF, έγγραφα Word, υπολογιστικά φύλλα και άλλες υποστηριζόμενες μορφές, καθιστώντας το ιδανικό για συστήματα διαχείρισης εγγράφων, πύλες υποστήριξης και οποιαδήποτε εφαρμογή όπου οι χρήστες χρειάζονται γρήγορη εύρεση πληροφοριών.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
Το GroupDocs.Search για Java παρέχει υποστήριξη πολλαπλών μορφών για πάνω από 50 τύπους αρχείων, συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, HTML και απλού κειμένου. Κλιμακώνεται σε εκατομμύρια αρχεία διατηρώντας χαμηλή χρήση μνήμης, αποθηκεύοντας το ευρετήριο στον δίσκο. Η βιβλιοθήκη περιλαμβάνει μια προχωρημένη γλώσσα ερωτημάτων με ενσωματωμένες Boolean, fuzzy και φωνητικές αναζητήσεις, και ενσωματώνεται με μία μόνο εξάρτηση Maven, επιτρέποντάς σας να ξεκινήσετε την ευρετηρίαση μέσα σε λίγα λεπτά.

## Προαπαιτήσεις
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **Java 11+** (Java 8 λειτουργεί, αλλά συνιστάται Java 11 ή νεότερη για καλύτερη απόδοση).  
- **Maven** για διαχείριση εξαρτήσεων.  
- Μια άδεια **GroupDocs.Search** (ένα κλειδί δοκιμής είναι επαρκές για ανάπτυξη).  

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις
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

Για λεπτομερή χρήση δείτε την [τεκμηρίωση](https://docs.groupdocs.com/search/java/).

### Ρύθμιση περιβάλλοντος
- Εγκαταστήστε το JDK (8 ή νεότερο) και διαμορφώστε το `JAVA_HOME`.  
- Χρησιμοποιήστε ένα IDE όπως IntelliJ IDEA ή Eclipse για πιο εύκολη αποσφαλμάτωση.  

### Προαπαιτούμενες γνώσεις
- Βασικές έννοιες προγραμματισμού Java.  
- Εξοικείωση με τη δομή `pom.xml` του Maven.  

## Ρύθμιση του GroupDocs.Search για Java
Μπορείτε να ενσωματώσετε τη βιβλιοθήκη μέσω Maven (όπως φαίνεται παραπάνω) ή να κατεβάσετε το JAR χειροκίνητα.

### Άμεση λήψη (αν προτιμάτε χειροκίνητη εγκατάσταση)
Κατεβάστε το πιο πρόσφατο πακέτο από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Βήματα απόκτησης άδειας
1. **Free trial** – Εγγραφείτε και λάβετε ένα προσωρινό κλειδί.  
2. **Temporary license** – Ζητήστε ένα κλειδί μακροπρόθεσμης δοκιμής για εκτεταμένη αξιολόγηση.  
3. **Purchase** – Αναβαθμίστε σε πλήρη εμπορική άδεια όταν είστε έτοιμοι για παραγωγή.

### Βασική αρχικοποίηση και ρύθμιση
Δημιουργήστε έναν φάκελο ευρετηρίου στο δίσκο και ελέγξτε ότι η βιβλιοθήκη φορτώνεται σωστά:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index in the specified directory
        Index index = new Index("C:\\MyIndex");
        
        System.out.println("GroupDocs.Search initialized!");
    }
}
```

> **Συμβουλή:** Κρατήστε το φάκελο του ευρετηρίου σε γρήγορο SSD για να ελαχιστοποιήσετε την καθυστέρηση ερωτημάτων.

## Προσθήκη εγγράφων στο ευρετήριο
**Γιατί είναι σημαντικό:** Δεν είναι δυνατά τα αποτελέσματα αναζήτησης χωρίς περιεχόμενο που έχει ευρετηριαστεί. Παρακάτω δείχνουμε πώς να προσθέσετε ολόκληρους φακέλους ή να φιλτράρετε συγκεκριμένους τύπους αρχείων.

### Βήμα 1: δημιουργία ευρετηρίου
Η κλάση `Index` είναι το αναζητήσιμο κοντέινερ που αποθηκεύει τα ευρετηριασμένα έγγραφα στον δίσκο.

```java
Index index = new Index("C:\\MyIndex");
```

### Βήμα 2: προσθήκη εγγράφων (προσθήκη εγγράφων στο ευρετήριο)
Μπορείτε να ευρετηριάσετε όλα τα αρχεία ενός φακέλου ή να περιορίσετε σε συγκεκριμένες επεκτάσεις χρησιμοποιώντας ένα `DocumentFilter`.

```java
index.add("C:\\Documents\\*.*"); // Adds all documents from the specified directory
// For specific file types, use:
index.add("C:\\Reports", new DocumentFilter() {
    @Override
    public boolean accept(String fileName) {
        return fileName.endsWith(".pdf") || fileName.endsWith(".docx");
    }
});
```

> **Επεξήγηση:**  
> - Το `Index` αντιπροσωπεύει τη βάση δεδομένων αναζήτησης.  
> - Η `add()` εισάγει αρχεία· το σύμβολο μπαλαντέρ `*.*` παίρνει όλα τα αρχεία, ενώ το `DocumentFilter` σας επιτρέπει να ρυθμίσετε λεπτομερώς το βήμα **προσθήκη εγγράφων στο ευρετήριο**.

## Εκτέλεση αναζήτησης (search documents java)
Τώρα που το ευρετήριο περιέχει δεδομένα, μπορείτε να το ερωτήσετε.

### Βήμα 1: δημιουργία ερωτήματος
```java
String query = "GroupDocs";
```

### Βήμα 2: εκτέλεση της αναζήτησης
```java
SearchResult result = index.search(query);
System.out.println("Documents found: " + result.getDocumentCount());
```

> **Επεξήγηση:**  
> - Η `search()` εκτελεί το ερώτημα εναντίον του ευρετηρίου.  
> - Η `getDocumentCount()` σας λέει πόσα έγγραφα ταιριάζουν — χρήσιμο για γρήγορους ελέγχους.

## Προηγμένες τεχνικές ερωτημάτων (boolean query java)
Για ακριβή έλεγχο, συνδυάστε όρους με λογική Boolean.

### Boolean ερωτήματα
Η κλάση `BooleanQuery` σας επιτρέπει να δημιουργήσετε σύνθετες εκφράσεις χρησιμοποιώντας τους τελεστές AND, OR, NOT.

```java
String booleanQuery = "GroupDocs AND Java";
SearchResult booleanResult = index.search(booleanQuery);
```

### Φωνητικές αναζητήσεις (προαιρετικό για fuzzy matching)
Η δυνατότητα `PhoneticSearch` ενεργοποιεί φωνητικό ταίριασμα για λανθασμένες γραφές, αλλά προσθέτει επιπλέον φόρτο.

```java
index.getSettings().setPhoneticSearch(true);
```

> **Πότε να χρησιμοποιηθεί:** Ενεργοποιήστε τη φωνητική αναζήτηση μόνο εάν οι χρήστες συχνά γράφουν λανθασμένα τους όρους· διαφορετικά, κρατήστε την απενεργοποιημένη για **βελτιστοποίηση της απόδοσης αναζήτησης**.

## Συχνά προβλήματα και λύσεις
| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Missing documents** | Λανθασμένη διαδρομή αρχείου ή ανεπαρκή δικαιώματα | Επαληθεύστε τη διαδρομή και δώστε δικαιώματα ανάγνωσης |
| **Slow queries** | Μεγάλο ευρετήριο χωρίς προσωρινή αποθήκευση ή περιττή φωνητική αναζήτηση | Ενεργοποιήστε caching, απενεργοποιήστε τη φωνητική αναζήτηση και εξετάστε το διαχωρισμό του ευρετηρίου |
| **Out‑of‑Memory errors** | Το μέγεθος του ευρετηρίου υπερβαίνει τη μνήμη heap του JVM | Αυξήστε το `-Xmx` ή χρησιμοποιήστε επαυξητική ευρετηρίαση |

## Πρακτικές εφαρμογές
Το GroupDocs.Search διαπρέπει σε πραγματικά σενάρια:

1. **Συστήματα διαχείρισης περιεχομένου** – Παρέχουν άμεση πλήρη αναζήτηση κειμένου σε άρθρα, PDF και πολυμέσα.  
2. **Πύλες εξυπηρέτησης πελατών** – Οι πράκτορες μπορούν να εντοπίζουν σχετικούς οδηγούς ή πολιτικές σε δευτερόλεπτα.  
3. **Εταιρικά αποθετήρια εγγράφων** – Αναζητούνται συμβάσεις, εκθέσεις και έγγραφα συμμόρφωσης χωρίς μεταφορά δεδομένων σε ξεχωριστή βάση.

## Σκέψεις απόδοσης
### Βελτιστοποίηση απόδοσης αναζήτησης
- **Incremental indexing:** Προσθέστε ή ενημερώστε μόνο τα αρχεία που έχουν αλλάξει αντί να ξαναδημιουργήσετε ολόκληρο το ευρετήριο.  
- **Caching:** Κρατήστε τα συχνά χρησιμοποιούμενα αποτελέσματα ερωτημάτων στη μνήμη.  
- **Resource monitoring:** Ρυθμίστε το heap του JVM (`-Xmx2g` ή μεγαλύτερο) ανάλογα με το μέγεθος του ευρετηρίου.

### Οδηγίες χρήσης πόρων
- Αποθηκεύστε το φάκελο του ευρετηρίου σε γρήγορο SSD ή NVMe.  
- Παρακολουθείτε CPU και μνήμη κατά την μαζική ευρετηρίαση· περιορίστε τις παρτίδες για να αποφύγετε αιχμές.

### Καλές πρακτικές διαχείρισης μνήμης Java
- Χρησιμοποιήστε `try‑with‑resources` όταν εργάζεστε με ροές.  
- Απενεργοποιήστε (nullify) μεγάλα αντικείμενα μετά τη χρήση για να βοηθήσετε τη συλλογή απορριμμάτων.

## Συμπέρασμα
Τώρα έχετε ένα πλήρες, έτοιμο για παραγωγή **παράδειγμα πλήρους αναζήτησης κειμένου** σε Java χρησιμοποιώντας το GroupDocs.Search. Από τη ρύθμιση της βιβλιοθήκης, **προσθήκη εγγράφων στο ευρετήριο**, τη δημιουργία **boolean query java** δηλώσεων, μέχρι την **βελτιστοποίηση της απόδοσης αναζήτησης**, καλύφθηκε κάθε βήμα.

### Επόμενα βήματα
Εξερευνήστε πιο προχωρημένα χαρακτηριστικά όπως προσαρμοσμένους αναλυτές, λεξικά συνωνύμων και ενσωμάτωση αποθήκευσης στο cloud, ελέγχοντας την επίσημη [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/).

---

## Συχνές ερωτήσεις

**Q:** Ποιες μορφές αρχείων υποστηρίζει το GroupDocs.Search;  
**A:** Πάνω από 50 μορφές, συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, HTML, TXT και πολλών τύπων εικόνων.

**Q:** Πώς πρέπει να διαχειριστώ μεγάλα σύνολα δεδομένων;  
**A:** Διαχωρίστε τα σε πολλαπλά ευρετήρια, ενημερώστε τα επαυξητικά και ενεργοποιήστε την προσωρινή αποθήκευση αποτελεσμάτων για να διατηρήσετε τη λανθασμένη καθυστέρηση χαμηλή.

**Q:** Μπορεί το GroupDocs.Search να λειτουργήσει σε περιβάλλοντα cloud;  
**A:** Ναι — μπορείτε να κατευθύνετε το φάκελο του ευρετηρίου σε προσαρτημένο cloud storage (π.χ., Azure Blob, AWS S3 μέσω οδηγού συστήματος αρχείων).

**Q:** Ποια είναι τα πλεονεκτήματα του GroupDocs.Search σε σχέση με άλλες βιβλιοθήκες;  
**A:** Υποστήριξη πολλαπλών μορφών, ενσωματωμένα Boolean/phonetic ερωτήματα και ένα ελαφρύ API Java που επεξεργάζεται εκατομμύρια έγγραφα με χαμηλό αποτύπωμα μνήμης.

**Q:** Πώς αντιμετωπίζω προβλήματα απόδοσης;  
**A:** Ελέγξτε τις ρυθμίσεις του ευρετηρίου, απενεργοποιήστε τη φωνητική αναζήτηση εάν δεν χρειάζεται, και παρακολουθήστε τη χρήση μνήμης/CPU του JVM κατά την ευρετηρίαση και την εκτέλεση ερωτημάτων.

**Τελευταία ενημέρωση:** 2026-08-15  
**Δοκιμάστηκε με:** GroupDocs.Search 25.4  
**Συγγραφέας:** GroupDocs  

**Πόροι**  
- **Documentation:** [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API reference:** [API Reference Guide](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub:** [Source Code on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Support:** [Forum and Community Support](https://forum.groupdocs.com/c/search/10)  
- **License:** [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)

## Σχετικά Μαθήματα

- [Πώς να υλοποιήσετε java full text search: δημιουργία φακέλου ευρετηρίου με GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με GroupDocs.Search για Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Βελτιώστε την απόδοση ερωτημάτων με GroupDocs.Search Java: βελτιστοποίηση ευρετηρίου & αναζήτησης](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)