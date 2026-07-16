---
date: '2026-07-16'
description: Μάθετε πώς να χρησιμοποιείτε το GroupDocs και να λαμβάνετε τις επεκτάσεις
  αρχείων Java ανακτώντας όλες τις υποστηριζόμενες μορφές αρχείων με το GroupDocs.Search
  για Java. Ιδανικό για προγραμματιστές που ενσωματώνουν βιβλιοθήκες επεξεργασίας
  εγγράφων.
keywords:
- how to use groupdocs
- get file extensions java
- validate file extensions java
lastmod: '2026-07-16'
og_description: Πώς να χρησιμοποιήσετε το GroupDocs για την ανάκτηση της πλήρους λίστας
  των υποστηριζόμενων μορφών αρχείων σε Java. Αυτός ο οδηγός παρουσιάζει βήμα‑βήμα
  τη ρύθμιση, αποσπάσματα κώδικα και πρακτικές συμβουλές για την επικύρωση των επεκτάσεων
  αρχείων στις εφαρμογές σας.
og_image_alt: Guide showing Java code to list GroupDocs supported file extensions
og_title: Πώς να χρησιμοποιήσετε το GroupDocs – Λάβετε τις υποστηριζόμενες μορφές
  αρχείων σε Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to use GroupDocs and get file extensions java by retrieving
    all supported file formats with GroupDocs.Search for Java. Ideal for developers
    integrating document processing libraries.
  headline: How to Use GroupDocs to Retrieve Supported File Formats in Java
  type: TechArticle
- description: Learn how to use GroupDocs and get file extensions java by retrieving
    all supported file formats with GroupDocs.Search for Java. Ideal for developers
    integrating document processing libraries.
  name: How to Use GroupDocs to Retrieve Supported File Formats in Java
  steps:
  - name: '**Document Management Systems** – Dynamically list supported uploads.'
    text: '**Document Management Systems** – Dynamically list supported uploads.'
  - name: '**Web‑Based File Uploads** – Validate file types client‑side using the
      retrieved list.'
    text: '**Web‑Based File Uploads** – Validate file types client‑side using the
      retrieved list.'
  - name: '**Backup Solutions** – Filter out unsupported files before archiving.'
    text: '**Backup Solutions** – Filter out unsupported files before archiving.'
  type: HowTo
- questions:
  - answer: It’s a Java library that enables full‑text search across many document
      formats without needing separate parsers.
    question: What is GroupDocs.Search?
  - answer: Change the `<version>` tag in `pom.xml` and run `mvn clean install`.
    question: How do I update the library version?
  - answer: The API shown is Java‑specific, but GroupDocs provides similar capabilities
      for .NET, Python, and other platforms.
    question: Can I use this feature in a non‑Java project?
  - answer: Contact GroupDocs support; they frequently add new formats in subsequent
      releases.
    question: What if a needed file type is missing?
  - answer: Yes, a full license removes trial limitations and grants commercial usage
      rights.
    question: Is a commercial license required for production?
  type: FAQPage
tags:
- convert PDF
- GroupDocs.Search
- Java document processing
title: Πώς να χρησιμοποιήσετε το GroupDocs για την ανάκτηση των υποστηριζόμενων μορφών
  αρχείων σε Java
type: docs
url: /el/java/licensing-configuration/retrieve-supported-file-formats-groupdocs-search-java/
weight: 1
---

# Πώς να χρησιμοποιήσετε το GroupDocs για την ανάκτηση υποστηριζόμενων μορφών αρχείων σε Java

Αν αναρωτιέστε **πώς να χρησιμοποιήσετε το GroupDocs** για να ανακαλύψετε τους ακριβείς τύπους αρχείων που μπορεί να διαχειριστεί η εφαρμογή σας, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από την ανάκτηση της πλήρους λίστας των υποστηριζόμενων μορφών με το GroupDocs.Search για Java, ώστε να μπορείτε με σιγουριά να εμφανίζετε ή να επικυρώνετε τις επεκτάσεις αρχείων στο UI σας. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που επιστρέφει κάθε υποστηριζόμενη επέκταση, μαζί με συμβουλές για caching του αποτελέσματος σε σενάρια υψηλής απόδοσης.

## Σύντομες Απαντήσεις
- **Τι κάνει η λειτουργία;** Επιστρέφει κάθε επέκταση αρχείου που μπορεί να ευρετηριάσει το GroupDocs.Search.  
- **Γιατί είναι χρήσιμη;** Σας επιτρέπει να ενημερώνετε δυναμικά τους χρήστες για τα υποστηριζόμενα αρχεία ανεβάσματος και να αποφεύγετε σφάλματα μη υποστηριζόμενων αρχείων.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται πλήρης άδεια για παραγωγή.  
- **Ποια έκδοση της Java απαιτείται;** Java 8 ή νεότερη.  
- **Απαιτείται κάποια επιπλέον ρύθμιση;** Όχι—απλώς προσθέστε την εξάρτηση Maven και καλέστε το API.

## Τι είναι το GroupDocs.Search;
Το GroupDocs.Search είναι μια βιβλιοθήκη Java που παρέχει γρήγορη, πλήρη αναζήτηση κειμένου σε ένα ευρύ φάσμα μορφών εγγράφων. Αποσπά τις πολυπλοκότητες της ανάλυσης PDF, αρχείων Word, λογιστικών φύλλων και πολλών άλλων τύπων, παρέχοντας ένα απλό API για ευρετηρίαση και ερωτήματα.

## Γιατί να ανακτήσετε τις υποστηριζόμενες μορφές αρχείων;
Η ανάκτηση των υποστηριζόμενων μορφών αρχείων σας παρέχει μια σαφή πηγή αλήθειας για το τι μπορεί να ευρετηριάσει η βιβλιοθήκη. Σας επιτρέπει να δημιουργείτε προγραμματιστικά στοιχεία UI, κανόνες επικύρωσης και τεκμηρίωση χωρίς σκληρή κωδικοποίηση τιμών, διασφαλίζοντας ότι τυχόν μελλοντικές ενημερώσεις της βιβλιοθήκης αντικατοπτρίζονται αυτόματα στην εφαρμογή σας.

Το GroupDocs.Search υποστηρίζει **πάνω από 120** διαφορετικές επεκτάσεις αρχείων, καλύπτοντας τα πάντα από κοινά αρχεία γραφείου έως εξειδικευμένες μορφές εικόνας και αρχείων. Η γνώση αυτής της λίστας σας επιτρέπει να:
- Δημιουργήσετε δυναμικά widgets ανεβάσματος που επιτρέπουν μόνο υποστηριζόμενα αρχεία.  
- Δημιουργήσετε ακριβή τεκμηρίωση για τους τελικούς χρήστες.  
- Μειώσετε σφάλματα χρόνου εκτέλεσης που προκύπτουν από προσπάθεια ευρετηρίασης μη υποστηριζόμενων μορφών.  
- Ελέγξετε γρήγορα τις απαιτήσεις συμμόρφωσης εξάγοντας τη λίστα σε CSV.

## Προαπαιτούμενα
- **Java Development Kit (JDK) 8+**  
- **Maven** για διαχείριση εξαρτήσεων  
- **IDE** όπως IntelliJ IDEA ή Eclipse  

Η εξοικείωση με βασικές έννοιες της Java και του Maven θα κάνει τα βήματα πιο ομαλά.

## Ρύθμιση του GroupDocs.Search για Java

### Ρύθμιση Maven
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

### Άμεση Λήψη
Αν προτιμάτε, μπορείτε να κατεβάσετε την τελευταία έκδοση απευθείας από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Βήματα Απόκτησης Άδειας
- **Free trial** – εξερευνήστε τις βασικές δυνατότητες.  
- **Temporary license** – δοκιμάστε χωρίς περιορισμούς λειτουργιών.  
- **Full license** – ξεκλειδώστε λειτουργίες έτοιμες για παραγωγή.

#### Βασική Αρχικοποίηση και Ρύθμιση
Μόλις προστεθεί η εξάρτηση, μπορείτε να δημιουργήσετε ένα ευρετήριο και να προσθέσετε έγγραφα:

```java
import com.groupdocs.search.*;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("path/to/index/folder");
        
        // Add documents to the index from a folder
        index.add("path/to/documents/folder");
    }
}
```

## Πώς να χρησιμοποιήσετε το GroupDocs για την απόκτηση επεκτάσεων αρχείων Java
Φορτώστε τις υποστηριζόμενες επεκτάσεις σε μόλις τρεις γραμμές κώδικα. Αυτή η προσέγγιση είναι ελαφριά, εκτελείται σε χιλιοστά του δευτερολέπτου και μπορεί να κληθεί κατά την εκκίνηση της εφαρμογής ή κατόπιν ζήτησης.

### Ανάκτηση Υποστηριζόμενων Μορφών Αρχείων
Τα παρακάτω βήματα δείχνουν πώς να εξάγετε την πλήρη λίστα επεκτάσεων αρχείων που υποστηρίζει το GroupDocs.Search.

#### Βήμα 1 – Εισαγωγή της Απαιτούμενης Κλάσης
Η κλάση `FileType` παρέχει μεταδεδομένα για κάθε υποστηριζόμενη μορφή αρχείου, συμπεριλαμβανομένης της επέκτασης και μιας φιλικής περιγραφής.

```java
import com.groupdocs.search.results.FileType;
```

#### Βήμα 2 – Λήψη της Συλλογής των Υποστηριζόμενων Τύπων
Καλώντας το `FileType.getSupportedFileTypes()` επιστρέφει μια συλλογή μόνο για ανάγνωση που περιέχει κάθε μορφή που μπορεί να ευρετηριάσει το GroupDocs.Search.

```java
Iterable<FileType> supportedFileTypes = FileType.getSupportedFileTypes();
```

#### Βήμα 3 – Επανάληψη και Εκτύπωση Κάθε Μορφής
Διέλθετε τη συλλογή και εκτυπώστε την επέκταση μαζί με την περιγραφή της. Μπορείτε να αποθηκεύσετε τα αποτελέσματα σε μια `List<String>` για μελλοντική επαναχρησιμοποίηση.

```java
for (FileType fileType : supportedFileTypes) {
    System.out.println(fileType.getExtension() + " - " + fileType.getDescription());
}
```

Η εκτέλεση αυτού του αποσπάσματος εκτυπώνει γραμμές όπως `pdf - Portable Document Format`, παρέχοντάς σας μια έτοιμη προς χρήση λίστα για αναπτυσσόμενα μενού UI ή λογική επικύρωσης.

## Συμβουλές Επίλυσης Προβλημάτων
- **Class Not Found** – Επαληθεύστε ότι η εξάρτηση Maven έχει επιλυθεί σωστά.  
- **Path Issues** – Βεβαιωθείτε ότι η διαδρομή του φακέλου ευρετηρίου υπάρχει και είναι εγγράψιμη.  

## Πρακτικές Εφαρμογές
1. **Document Management Systems** – Λίστα υποστηριζόμενων ανεβάσματος δυναμικά.  
2. **Web‑Based File Uploads** – Επικυρώστε τύπους αρχείων στην πλευρά του πελάτη χρησιμοποιώντας τη ληφθείσα λίστα.  
3. **Backup Solutions** – Φιλτράρετε τα μη υποστηριζόμενα αρχεία πριν την αρχειοθέτηση.

## Σκέψεις Απόδοσης
- Αποθηκεύστε τη ληφθείσα λίστα στη μνήμη εάν χρειάζεται να την προσπελάζετε συχνά· η κλήση αυτή καθαυτή είναι ελαφριά (κάτω από 10 ms σε τυπικό διακομιστή).  
- Διατηρήστε τη βιβλιοθήκη GroupDocs.Search ενημερωμένη για να επωφεληθείτε από βελτιώσεις απόδοσης—κάθε κύρια έκδοση προσθέτει υποστήριξη για ~5 νέες μορφές και μειώνει την καθυστέρηση ευρετηρίασης έως και 15 %.

## Συχνά Προβλήματα και Λύσεις
| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| `FileType` class missing | Η εξάρτηση δεν προστέθηκε | Εκτελέστε ξανά `mvn clean install` μετά την προσθήκη της εξάρτησης |
| No output printed | `System.out` καταστέλλεται στο IDE | Ελέγξτε τη διαμόρφωση της κονσόλας ή εκτελέστε από τη γραμμή εντολών |

## Συχνές Ερωτήσεις

**Q: Τι είναι το GroupDocs.Search;**  
A: Είναι μια βιβλιοθήκη Java που επιτρέπει πλήρη αναζήτηση κειμένου σε πολλές μορφές εγγράφων χωρίς την ανάγκη ξεχωριστών αναλυτών.

**Q: Πώς ενημερώνω την έκδοση της βιβλιοθήκης;**  
A: Αλλάξτε την ετικέτα `<version>` στο `pom.xml` και εκτελέστε `mvn clean install`.

**Q: Μπορώ να χρησιμοποιήσω αυτή τη λειτουργία σε έργο μη‑Java;**  
A: Το API που εμφανίζεται είναι ειδικό για Java, αλλά το GroupDocs παρέχει παρόμοιες δυνατότητες για .NET, Python και άλλες πλατφόρμες.

**Q: Τι γίνεται αν λείπει ένας απαιτούμενος τύπος αρχείου;**  
A: Επικοινωνήστε με την υποστήριξη του GroupDocs· προσθέτουν συχνά νέες μορφές σε επόμενες εκδόσεις.

**Q: Απαιτείται εμπορική άδεια για παραγωγή;**  
A: Ναι, μια πλήρης άδεια αφαιρεί τους περιορισμούς της δοκιμής και παρέχει δικαιώματα εμπορικής χρήσης.

## Πόροι
- [Τεκμηρίωση GroupDocs Search](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download Latest Version](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία Ενημέρωση:** 2026-07-16  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs  

## Σχετικά Μαθήματα

- [Ορισμός Άδειας Java – Οδηγός Διαμόρφωσης GroupDocs.Search Java](/search/java/licensing-configuration/)
- [Φίλτρο Επεκτάσεων Αρχείων Java με GroupDocs.Search – Οδηγός](/search/java/advanced-features/master-java-file-filtering-groupdocs-search/)
- [Δημιουργία & Διαχείριση Ευρετηρίου GroupDocs.Search Java](/search/java/indexing/create-manage-groupdocs-search-java-index/)