---
date: '2026-05-12'
description: 'Learn java full text search with GroupDocs.Search: add documents to
  index, configure merge options, and cancel merge operation. Ideal for document management
  java solutions.'
keywords:
- java full text search
- document management java
- GroupDocs.Search merging
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: 'Learn java full text search with GroupDocs.Search: add documents to
    index, configure merge options, and cancel merge operation. Ideal for document
    management java solutions.'
  headline: java full text search – add docs & merge with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It tells GroupDocs.Search to scan a folder, extract searchable tokens,
      and store metadata for each file.
    question: What does “add documents to index” mean?
  - answer: Yes—use the `Cancellation` object to abort a merge after a configurable
      timeout.
    question: Can I stop a long merge?
  - answer: A free trial or temporary license works for testing; a commercial license
      unlocks full features.
    question: Do I need a license?
  - answer: JDK 8 or newer.
    question: Which Java version is required?
  - answer: Absolutely—GroupDocs.Search can handle multi‑hundred‑page documents with
      incremental indexing.
    question: Is this suitable for large datasets?
  type: FAQPage
title: java full text search – add docs & merge with GroupDocs.Search
type: docs
url: /el/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# java πλήρης αναζήτηση κειμένου – προσθήκη εγγράφων & συγχώνευση με GroupDocs.Search

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “προσθήκη εγγράφων στο ευρετήριο”;** Ενημερώνει το GroupDocs.Search να σαρώσει έναν φάκελο, να εξάγει διακριτικά αναζήτησης και να αποθηκεύσει μεταδεδομένα για κάθε αρχείο.  
- **Μπορώ να σταματήσω μια μακρά συγχώνευση;** Ναι—χρησιμοποιήστε το αντικείμενο `Cancellation` για να ακυρώσετε μια συγχώνευση μετά από ένα ρυθμιζόμενο χρονικό όριο.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή ή προσωρινή άδεια λειτουργεί για δοκιμές· μια εμπορική άδεια ξεκλειδώνει όλες τις δυνατότητες.  
- **Ποια έκδοση της Java απαιτείται;** JDK 8 ή νεότερη.  
- **Είναι κατάλληλο για μεγάλα σύνολα δεδομένων;** Απόλυτα—το GroupDocs.Search μπορεί να διαχειριστεί έγγραφα πολλαπλών εκατοντάδων σελίδων με σταδιακή ευρετηρίαση.

## Τι σημαίνει “προσθήκη εγγράφων στο ευρετήριο” στο GroupDocs.Search;
**Η προσθήκη εγγράφων σε ένα ευρετήριο σημαίνει την τροφοδοσία μιας συλλογής αρχείων στο GroupDocs.Search ώστε η βιβλιοθήκη να μπορεί να αναλύσει το περιεχόμενό τους, να εξάγει διακριτικά και να δημιουργήσει μια δομή δεδομένων αναζήτησης.** Η διαδικασία δημιουργεί μια συμπαγή αναπαράσταση που επιτρέπει εξαιρετικά γρήγορα ερωτήματα πλήρους κειμένου σε όλα τα ευρετηριασμένα αρχεία.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για διαχείριση εγγράφων java;
Το GroupDocs.Search παρέχει **κλιμακωτή ευρετηρίαση για 50+ μορφές εισόδου** (PDF, DOCX, XLSX, PPTX, HTML, εικόνες κ.λπ.) και μπορεί να επεξεργαστεί **έγγραφα έως 2 GB χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη**. Το API του σας δίνει λεπτομερή έλεγχο της ευρετηρίασης, της συγχώνευσης και της ακύρωσης, καθιστώντας το κορυφαία επιλογή για λύσεις java πλήρους αναζήτησης κειμένου επιχειρησιακού επιπέδου.

## Προαπαιτούμενα
- **GroupDocs.Search for Java** έκδοση 25.4 ή νεότερη.  
- Maven (ή χειροκίνητη λήψη JAR).  
- Βασικές γνώσεις Java και περιβάλλον JDK 8+.

## Ρύθμιση του GroupDocs.Search για Java

### Εγκατάσταση Maven
Αν διαχειρίζεστε τις εξαρτήσεις με Maven, προσθέστε το αποθετήριο και την εξάρτηση στο `pom.xml` σας:

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

### Άμεση Λήψη
Εναλλακτικά, κατεβάστε το τελευταίο JAR από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας
- **Δωρεάν Δοκιμή:** Εγγραφείτε στον ιστότοπο GroupDocs για άδεια δοκιμής.  
- **Προσωρινή Άδεια:** Αιτηθείτε ένα προσωρινό κλειδί εάν χρειάζεστε εκτεταμένη αξιολόγηση.  
- **Εμπορική Άδεια:** Αγοράστε για χρήση σε παραγωγή.

Αφού έχετε το αρχείο άδειας, τοποθετήστε το στο έργο σας και αρχικοποιήστε τη βιβλιοθήκη όπως φαίνεται παρακάτω.

## Οδηγός Υλοποίησης

### Πώς να προσθέσετε έγγραφα στο ευρετήριο – Δημιουργία του Πρώτου Ευρετηρίου
**Φορτώστε ή δημιουργήστε ένα κενό ευρετήριο δημιουργώντας ένα αντικείμενο της κλάσης `Index`, η οποία αντιπροσωπεύει ένα αναζητήσιμο δοχείο στον δίσκο.** Αυτό το βήμα προετοιμάζει μια τοποθεσία αποθήκευσης για όλα τα διακριτικά που θα παραχθούν από τα έγγραφά σας.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Γιατί:** Αυτό το βήμα δημιουργεί ένα δοχείο αποθήκευσης όπου θα αποθηκευτούν τα ευρετηριασμένα διακριτικά.

#### Προσθήκη εγγράφων στο ευρετήριο
**Καλέστε `index.add` με μια διαδρομή φακέλου· η μέθοδος σαρώει κάθε αρχείο, εξάγει κείμενο και αποθηκεύει μεταδεδομένα αναζήτησης στο ευρετήριο.** Η λειτουργία εκτελείται σε μία μόνο διέλευση και σέβεται τις ρυθμίσεις του `IndexSettings`.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Γιατί:** Η βιβλιοθήκη διαβάζει κάθε αρχείο, εξάγει κείμενο και το αποθηκεύει στο `index1`.

### Δημιουργία δεύτερου ευρετηρίου για ευέλικτες ροές εργασίας
**Δημιουργήστε ένα άλλο αντικείμενο `Index` για να κρατήσετε ένα ξεχωριστό σύνολο εγγράφων, επιτρέποντας απομονωμένη επεξεργασία πριν από μια συγχώνευση.** Αυτό το μοτίβο είναι χρήσιμο για σενάρια multi‑tenant ή σταδιακής ευρετηρίασης.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Γιατί:** Πολλαπλά ευρετήρια σας επιτρέπουν να διαχειρίζεστε διαφορετικά σύνολα εγγράφων και να τα συνδυάζετε αργότερα.

### Πώς να ρυθμίσετε τις επιλογές συγχώνευσης και να ακυρώσετε τη λειτουργία συγχώνευσης
**Δημιουργήστε μια παρουσία `MergeOptions`, ορίστε τις επιθυμητές παραμέτρους και συνδέστε ένα διακριτικό `Cancellation` που ακυρώνει τη συγχώνευση μετά από ένα καθορισμένο χρονικό όριο.** Αυτό σας δίνει πλήρη έλεγχο της χρήσης πόρων κατά τις μεγάλες συγχωνεύσεις.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Γιατί:** Το `Cancellation` σας δίνει τον έλεγχο για **ακύρωση της λειτουργίας συγχώνευσης** αυτόματα, αποτρέποντας ατέρμονες εργασίες.

### Συγχώνευση των ευρετηρίων
**Κληθείτε `index1.merge(index2, mergeOptions)`· το κύριο ευρετήριο απορροφά όλα τα έγγραφα από το δευτερεύον ευρετήριο διατηρώντας την ακεραιότητα των διακριτικών.** Μετά τη συγχώνευση, έχετε μια ενοποιημένη αναζητήσιμη αποθήκη.

```java
index1.merge(index2, options);
```

- **Γιατί:** Μετά από αυτήν την κλήση, το `index1` περιέχει όλα τα έγγραφα και από τις δύο πηγές, παρέχοντάς σας μια ενοποιημένη εμπειρία αναζήτησης.

## Πρακτικές Εφαρμογές για Διαχείριση Εγγράφων Java
- **Νομικά γραφεία:** Ενοποίηση φακέλων υποθέσεων από πολλαπλά γραφεία σε ένα ενιαίο αναζητήσιμο ευρετήριο.  
- **Οικονομικά ιδρύματα:** Συγχώνευση τριμηνιαίων εκθέσεων σε μια ενοποιημένη αποθήκη για γρήγορα ερωτήματα ελέγχου.  
- **Επιχειρήσεις:** Συνδυάστε πολιτικές HR, εγχειρίδια συμμόρφωσης και εσωτερικούς οδηγούς για αναζήτηση σε όλη την επιχείρηση.

## Σκέψεις Απόδοσης
- **Σταδιακή ευρετηρίαση:** Προσθέστε νέα αρχεία περιοδικά αντί να ξαναχτίζετε ολόκληρο το ευρετήριο.  
- **Παρακολούθηση μνήμης:** Μεγάλες παρτίδες μπορούν να καταναλώσουν RAM· επεξεργαστείτε αρχεία σε μικρότερα τμήματα ή ενεργοποιήστε τη λειτουργία streaming.  
- **Συλλογή απορριμμάτων:** Απελευθερώστε αχρησιμοποίητα αντικείμενα `Index` άμεσα για να ελευθερώσετε πόρους.  
- **Αποθήκευση SSD:** Η αποθήκευση αρχείων ευρετηρίου σε SSD μπορεί να βελτιώσει την ταχύτητα συγχώνευσης έως και 2×.

## Συχνά Προβλήματα & Λύσεις
| Πρόβλημα | Λύση |
|----------|------|
| **Λανθασμένη διαδρομή φακέλου** | Επαληθεύστε τη απόλυτη διαδρομή και βεβαιωθείτε ότι η εφαρμογή έχει δικαιώματα ανάγνωσης. |
| **Ανεπαρκής μνήμη** | Αυξήστε τη μνήμη heap του JVM (`-Xmx`) ή ευρετηριάστε αρχεία σε παρτίδες. |
| **Η ακύρωση δεν ενεργοποιείται** | Βεβαιωθείτε ότι το `cancelAfter` έχει οριστεί πριν καλέσετε το `merge`. |
| **Μη υποστηριζόμενη μορφή αρχείου** | Εγκαταστήστε πρόσθετα plugins μορφής από το GroupDocs εάν χρειάζεται. |

## Συχνές Ερωτήσεις

**Ε:** *Γιατί θα δημιουργούσα πολλαπλά ευρετήρια αντί για ένα μόνο;*  
**Α:** Τα ξεχωριστά ευρετήρια σας επιτρέπουν να απομονώσετε περιοχές δεδομένων, να εφαρμόσετε διαφορετικές πολιτικές ασφαλείας και να συγχωνεύετε μόνο όταν χρειάζεται, κάτι που βελτιώνει την απόδοση και την οργάνωση.

**Ε:** *Μπορώ να ακυρώσω μια λειτουργία ευρετηρίασης με τον ίδιο τρόπο που ακυρώνω μια συγχώνευση;*  
**Α:** Ναι—χρησιμοποιήστε το αντικείμενο `Cancellation` με τη μέθοδο `add` για να σταματήσετε εργασίες ευρετηρίασης μεγάλης διάρκειας.

**Ε:** *Πώς μπορώ να εξασφαλίσω βέλτιστη απόδοση με πολύ μεγάλες συλλογές εγγράφων;*  
**Α:** Εκτελέστε σταδιακή ευρετηρίαση, παρακολουθήστε τη μνήμη JVM και αποθηκεύστε το ευρετήριο σε SSD. Σκεφτείτε να χρησιμοποιήσετε τη ρύθμιση `BatchSize` για να περιορίσετε τα έγγραφα στη μνήμη.

**Ε:** *Τι πρέπει να κάνω αν λάβω σφάλματα “Access denied”;*  
**Α:** Ελέγξτε τα δικαιώματα φακέλου για τον χρήστη που εκτελεί τη διαδικασία Java και βεβαιωθείτε ότι το αρχείο άδειας είναι αναγνώσιμο.

**Ε:** *Είναι το GroupDocs.Search συμβατό με άλλες βιβλιοθήκες GroupDocs;*  
**Α:** Απόλυτα—μπορείτε να το ενσωματώσετε με το GroupDocs.Viewer, το GroupDocs.Conversion και άλλα για να δημιουργήσετε μια πλήρη λύση εγγράφων.

## Συμπέρασμα
Ακολουθώντας αυτόν τον οδηγό, τώρα γνωρίζετε πώς να **προσθέσετε έγγραφα στο ευρετήριο**, να ρυθμίσετε τη συμπεριφορά συγχώνευσης και να ακυρώσετε με ασφάλεια τη **λειτουργία συγχώνευσης** όταν χρειάζεται—όλα μέσα σε μια ισχυρή ροή εργασίας **java πλήρης αναζήτηση κειμένου**. Πειραματιστείτε με μεγαλύτερα σύνολα δεδομένων, εξερευνήστε προσαρμοσμένους διακριτικούς ή συνδυάστε το GroupDocs.Search με άλλα προϊόντα GroupDocs για να δημιουργήσετε μια λύση επιχειρησιακού επιπέδου.

**Πόροι**
- **Τεκμηρίωση:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **Αναφορά API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Λήψη:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **Αποθετήριο GitHub:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Δωρεάν Φόρουμ Υποστήριξης:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Αίτηση για Προσωρινή Άδεια:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Τελευταία Ενημέρωση:** 2026-05-12  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να προσθέσετε έγγραφα στο ευρετήριο με ευρετηρίαση μεταδεδομένων σε Java χρησιμοποιώντας το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Προσθήκη Εγγράφων στο Ευρετήριο και Απενεργοποίηση Λέξεων-Διακοπής στο GroupDocs.Search Java για Βελτιωμένη Ακρίβεια Αναζήτησης](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
- [Προσθήκη Εγγράφων στο Ευρετήριο – Μαθήματα GroupDocs.Search Java](/search/java/document-management/)