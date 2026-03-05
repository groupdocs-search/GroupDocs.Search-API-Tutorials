---
date: '2026-02-24'
description: Μάθετε πώς να πραγματοποιείτε αναζήτηση ανά χαρακτηριστικό Java χρησιμοποιώντας
  το GroupDocs.Search. Αυτός ο οδηγός δείχνει τη μαζική ενημέρωση των χαρακτηριστικών
  εγγράφων, καθώς και την προσθήκη και τροποποίηση χαρακτηριστικών κατά την ευρετηρίαση.
keywords:
- GroupDocs.Search Java
- document attribute modification
- Java indexing techniques
title: Αναζήτηση κατά χαρακτηριστικό Java με τον οδηγό GroupDocs.Search
type: docs
url: /el/java/document-management/groupdocs-search-java-modify-attributes-indexing/
weight: 1
---

# Αναζήτηση κατά χαρακτηριστικό Java με τον οδηγό GroupDocs.Search

Αναζητάτε να βελτιώσετε το σύστημα διαχείρισης εγγράφων σας τροποποιώντας δυναμικά και ευρετηριάζοντας τα χαρακτηριστικά των εγγράφων χρησιμοποιώντας Java; Βρίσκεστε στο σωστό μέρος! Αυτό το tutorial εμβαθύνει στη χρήση της ισχυρής βιβλιοθήκης GroupDocs.Search for Java για **search by attribute java**, την αλλαγή των ευρετηριασμένων χαρακτηριστικών εγγράφων και την προσθήκη τους κατά τη διαδικασία ευρετηρίασης. Είτε δημιουργείτε μια αναζητήσιμη πύλη, ένα αρχείο συμμόρφωσης ή μια έξυπνη εφαρμογή που βασίζεται σε περιεχόμενο, η κατανόηση αυτών των τεχνικών θα σας εξοικονομήσει χρόνο και θα βελτιώσει την απόδοση.

## Γρήγορες Απαντήσεις
- **Τι είναι το “search by attribute java”;** Είναι η δυνατότητα φιλτραρίσματος των αποτελεσμάτων αναζήτησης χρησιμοποιώντας προσαρμοσμένα μεταδεδομένα που συνδέονται με κάθε έγγραφο.  
- **Μπορώ να τροποποιήσω τα χαρακτηριστικά μετά την ευρετηρίαση;** Ναι—χρησιμοποιήστε `AttributeChangeBatch` για μαζική ενημέρωση χαρακτηριστικών εγγράφων.  
- **Πώς μπορώ να προσθέσω χαρακτηριστικά κατά την ευρετηρίαση;** Εγγραφείτε στο συμβάν `FileIndexing` και ορίστε τα χαρακτηριστικά προγραμματιστικά.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Ποια έκδοση της Java απαιτείται;** Συνιστάται Java 8 ή νεότερη.

## Τι είναι το “search by attribute java”;
**Search by attribute java** σας επιτρέπει να ερωτάτε έγγραφα βάσει των μεταδεδομένων τους (χαρακτηριστικά) αντί μόνο του περιεχομένου τους. Συνδέοντας ζεύγη κλειδιού‑τιμής όπως `public`, `main`, ή `key` σε κάθε αρχείο, μπορείτε γρήγορα να περιορίσετε τα αποτελέσματα στο πιο σχετικό υποσύνολο.

## Γιατί να χρησιμοποιήσετε δυναμική ετικετοποίηση μεταδεδομένων;
- **Δυναμική κατηγοριοποίηση** – διατηρήστε τα μεταδεδομένα συγχρονισμένα με τους εξελισσόμενους επιχειρηματικούς κανόνες.  
- **Γρηγορότερο φιλτράρισμα** – τα φίλτρα χαρακτηριστικών αξιολογούνται πριν την αναζήτηση πλήρους κειμένου, βελτιώνοντας τους χρόνους απόκρισης.  
- **Παρακολούθηση συμμόρφωσης** – ετικετοθετήστε έγγραφα για πολιτικές διατήρησης ή απαιτήσεις ελέγχου.  
- **Μαζική ενημέρωση χαρακτηριστικών** – αλλάξτε πολλά έγγραφα σε μία λειτουργία χωρίς επανευρετηρίαση όλων.

## Προαπαιτούμενα

- **Java 8+** (JDK 8 ή νεότερο)  
- **GroupDocs.Search for Java** βιβλιοθήκη (δείτε τη ρύθμιση Maven παρακάτω)  
- Βασική κατανόηση της Java και των εννοιών ευρετηρίασης  

## Ρύθμιση του GroupDocs.Search για Java

### Ρύθμιση Maven

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

### Άμεση λήψη

Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).  
Αν προτιμάτε να μην χρησιμοποιήσετε εργαλείο κατασκευής όπως το Maven, κατεβάστε το JAR από την [ιστοσελίδα GroupDocs](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας

- Ξεκινήστε με μια δωρεάν δοκιμή για να εξερευνήσετε τις δυνατότητες.  
- Για εκτεταμένη χρήση, αποκτήστε προσωρινή ή πλήρη άδεια μέσω της [σελίδας αδειών](https://purchase.groupdocs.com/temporary-license).

### Βασική Αρχικοποίηση

```java
import com.groupdocs.search.Index;

// Initialize an index in a specified directory
Index index = new Index("YOUR_OUTPUT_DIRECTORY/ChangeAttributes");
```

## Πώς να τροποποιήσετε τα χαρακτηριστικά εγγράφων (Μαζική ενημέρωση)

### Search by Attribute Java – Αλλαγή χαρακτηριστικών εγγράφων

Μπορείτε να προσθέσετε, να αφαιρέσετε ή να αντικαταστήσετε χαρακτηριστικά σε ήδη ευρετηριασμένα έγγραφα, επιτρέποντας **batch update document attributes** χωρίς επανευρετηρίαση ολόκληρης της συλλογής.

### Βήμα‑βήμα

**Βήμα 1: Προσθήκη εγγράφων στο ευρετήριο**  

```java
index.add("YOUR_DOCUMENT_DIRECTORY");
```

**Βήμα 2: Ανάκτηση πληροφοριών ευρετηριασμένων εγγράφων**  

```java
import com.groupdocs.search.results.DocumentInfo;

DocumentInfo[] documents = index.getIndexedDocuments();
```

**Βήμα 3: Μαζική ενημέρωση χαρακτηριστικών εγγράφων**  

```java
import com.groupdocs.search.common.AttributeChangeBatch;
import com.groupdocs.search.SearchOptions;

AttributeChangeBatch batch = new AttributeChangeBatch();
batch.addToAll("public"); // Add 'public' to all documents
batch.remove(documents[0].getFilePath(), "public"); // Remove 'public' from a specific document
batch.add(documents[0].getFilePath(), "main", "key"); // Add 'main' and 'key' attributes

// Apply changes
index.changeAttributes(batch);
```

**Βήμα 4: Αναζήτηση με φίλτρα χαρακτηριστικών**  

```java
import com.groupdocs.search.results.SearchResult;

SearchOptions options = new SearchOptions();
options.setSearchDocumentFilter(SearchDocumentFilter.createAttribute("main"));
String query = "length";
SearchResult result = index.search(query, options); // Perform the search
```

### Μαζική ενημέρωση χαρακτηριστικών εγγράφων με AttributeChangeBatch
Η κλάση `AttributeChangeBatch` είναι το βασικό εργαλείο για **batch update document attributes**. Ομαδοποιώντας τις αλλαγές σε ένα ενιαίο batch, μειώνετε το φόρτο I/O και διατηρείτε το ευρετήριο συνεπές.

## Πώς να προσθέσετε χαρακτηριστικά κατά την ευρετηρίαση

### Search by Attribute Java – Προσθήκη χαρακτηριστικών κατά την ευρετηρίαση

Συνδέστε στο συμβάν `FileIndexing` για να εκχωρήσετε προσαρμοσμένα χαρακτηριστικά καθώς κάθε αρχείο προστίθεται στο ευρετήριο.

### Βήμα‑βήμα

**Βήμα 1: Εγγραφή στο συμβάν FileIndexing**  

```java
import com.groupdocs.search.events.EventHandler;
import com.groupdocs.search.events.FileIndexingEventArgs;

index.getEvents().FileIndexing.add(new EventHandler<FileIndexingEventArgs>() {
    @Override
    public void invoke(Object sender, FileIndexingEventArgs args) {
        if (args.getDocumentFullPath().endsWith("Lorem ipsum.pdf")) {
            args.setAttributes(new String[] { "main", "key" });
        }
    }
});
```

**Βήμα 2: Ευρετηρίαση εγγράφων**  

```java
index.add("YOUR_DOCUMENT_DIRECTORY");
```

## Πρακτικές Εφαρμογές

1. **Συστήματα Διαχείρισης Εγγράφων** – Αυτοματοποιήστε την κατηγοριοποίηση προσθέτοντας μεταδεδομένα κατά την εισαγωγή.  
2. **Μεγάλα Αρχεία Περιεχομένου** – Χρησιμοποιήστε φίλτρα χαρακτηριστικών για να περιορίσετε τις αναζητήσεις, μειώνοντας δραστικά τους χρόνους απόκρισης.  
3. **Συμμόρφωση & Αναφορές** – Ετικετοθετήστε δυναμικά έγγραφα για προγράμματα διατήρησης ή ίχνη ελέγχου.

## Σκέψεις Απόδοσης

- **Διαχείριση μνήμης** – Παρακολουθήστε τη μνήμη heap της JVM και ρυθμίστε το `-Xmx` όπως απαιτείται.  
- **Μαζική επεξεργασία** – Ομαδοποιήστε τις αλλαγές χαρακτηριστικών με `AttributeChangeBatch` για ελαχιστοποίηση των εγγραφών στο ευρετήριο.  
- **Ενημερώσεις βιβλιοθήκης** – Διατηρήστε το GroupDocs.Search ενημερωμένο για να επωφεληθείτε από διορθώσεις απόδοσης.

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Γιατί συμβαίνει | Πώς να διορθώσετε |
|----------|----------------|-------------------|
| **Attributes not applied** | Ο διαχειριστής συμβάντων δεν έχει καταχωρηθεί πριν την ευρετηρίαση | Βεβαιωθείτε ότι το `index.getEvents().FileIndexing.add(...)` εκτελείται πριν το `index.add(...)`. |
| **Search returns no results** | Ασυμφωνία ονόματος χαρακτηριστικού (διάκριση πεζών‑κεφαλαίων) | Χρησιμοποιήστε ακριβή ονόματα χαρακτηριστικών κατά τη δημιουργία φίλτρων (`createAttribute("main")`). |
| **Out‑of‑memory errors** on large batches | Πάρα πολλές αλλαγές σε ένα ενιαίο batch | Διαιρέστε τις μεγάλες ενημερώσεις σε μικρότερα `AttributeChangeBatch` instances. |
| **License not recognized** | Χρήση δοκιμαστικού JAR χωρίς εφαρμογή αρχείου άδειας | Καλέστε `License license = new License(); license.setLicense("path/to/license.file");` πριν από οποιαδήποτε λειτουργία ευρετηρίου. |

## Συχνές Ερωτήσεις

**Q: Ποια είναι τα προαπαιτούμενα για τη χρήση του GroupDocs.Search σε Java;**  
A: Χρειάζεστε Java 8+, τη βιβλιοθήκη GroupDocs.Search και βασικές γνώσεις των εννοιών ευρετηρίασης.

**Q: Πώς εγκαθιστώ το GroupDocs.Search μέσω Maven;**  
A: Προσθέστε το αποθετήριο και την εξάρτηση που εμφανίζονται στην ενότητα Ρύθμιση Maven στο αρχείο `pom.xml` σας.

**Q: Μπορώ να τροποποιήσω τα χαρακτηριστικά μετά την ευρετηρίαση των εγγράφων;**  
A: Ναι, χρησιμοποιήστε `AttributeChangeBatch` για μαζική ενημέρωση χαρακτηριστικών εγγράφων χωρίς επανευρετηρίαση.

**Q: Τι κάνω αν η διαδικασία ευρετηρίασης είναι αργή;**  
A: Βελτιστοποιήστε τις ρυθμίσεις μνήμης της JVM, χρησιμοποιήστε μαζικές ενημερώσεις και βεβαιωθείτε ότι χρησιμοποιείτε την πιο πρόσφατη έκδοση της βιβλιοθήκης.

**Q: Πού μπορώ να βρω περισσότερους πόρους για το GroupDocs.Search για Java;**  
A: Επισκεφθείτε την [επίσημη τεκμηρίωση](https://docs.groupdocs.com/search/java/) ή εξερευνήστε τα φόρουμ της κοινότητας.

## Πόροι

- Τεκμηρίωση: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)
- Αναφορά API: [API Reference](https://reference.groupdocs.com/search/java)
- Λήψη: [Latest Releases](https://releases.groupdocs.com/search/java/)
- GitHub: [GitHub GroupDocs.Search](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- Δωρεάν Φόρουμ Υποστήριξης: [GroupDocs Forums](https://forum.groupdocs.com/c/search/10)
- Προσωρινή Άδεια: [License Page](https://purchase.groupdocs.com/temporary-license)

---

**Τελευταία ενημέρωση:** 2026-02-24  
**Δοκιμάστηκε με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs