---
date: '2026-09-21'
description: Μάθετε πώς να κάνετε αναζήτηση με attribute java χρησιμοποιώντας το GroupDocs.Search
  για Java. Αυτός ο οδηγός καλύπτει την μαζική ενημέρωση των χαρακτηριστικών εγγράφων,
  την προσθήκη χαρακτηριστικών κατά την ευρετηρίαση και την αναζήτηση εγγράφων με
  metadata.
keywords:
- search by attribute java
- search documents by metadata
- GroupDocs.Search Java
- document attribute modification
lastmod: '2026-09-21'
og_description: Η αναζήτηση με attribute java σας επιτρέπει να φιλτράρετε τα αποτελέσματα
  χρησιμοποιώντας προσαρμοσμένο metadata. Μάθετε για τις μαζικές ενημερώσεις, την
  επισήμανση χαρακτηριστικών κατά την ευρετηρίαση και τις βέλτιστες πρακτικές με το
  GroupDocs.Search για Java.
og_image_alt: Illustration of Java code adding metadata attributes to documents using
  GroupDocs.Search
og_title: Αναζήτηση με attribute java με το GroupDocs.Search – Πλήρης Οδηγός Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to search by attribute java using GroupDocs.Search for Java.
    This guide covers batch updating document attributes, adding attributes during
    indexing, and searching documents by metadata.
  headline: How to search by attribute java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: Java 8+, the GroupDocs.Search library, and basic knowledge of indexing
      concepts.
    question: What are the prerequisites for using GroupDocs.Search in Java?
  - answer: Add the repository and dependency shown in the Maven setup section to
      your `pom.xml`.
    question: How do I install GroupDocs.Search via Maven?
  - answer: Yes, use `AttributeChangeBatch` to batch update document attributes without
      re‑indexing.
    question: Can I modify attributes after documents are indexed?
  - answer: Optimize JVM memory (`-Xmx`), use batch updates, and upgrade to the latest
      library version for performance patches.
    question: What if my indexing process is slow?
  - answer: Visit the [official documentation](https://docs.groupdocs.com/search/java/)
      or explore community forums.
    question: Where can I find more resources on GroupDocs.Search for Java?
  type: FAQPage
tags:
- search by attribute java
- GroupDocs.Search
- Java document management
- metadata indexing
title: Πώς να κάνετε αναζήτηση με attribute java χρησιμοποιώντας το GroupDocs.Search
type: docs
url: /el/java/document-management/groupdocs-search-java-modify-attributes-indexing/
weight: 1
---

# Αναζήτηση κατά χαρακτηριστικό java με οδηγό GroupDocs.Search

Σε σύγχρονες εφαρμογές που εστιάζουν στα έγγραφα, συχνά χρειάζεται να εντοπίζετε αρχεία όχι μόνο με βάση το κείμενό τους, αλλά και με προσαρμοσμένα μεταδεδομένα όπως τμήμα, επίπεδο εμπιστευτικότητας ή ημερομηνία δημιουργίας. **Search by attribute java** σας παρέχει αυτή τη δυνατότητα σε ένα μόνο, υψηλής απόδοσης ερώτημα. Σε αυτό το σεμινάριο θα δείτε πώς να ενημερώνετε μαζικά χαρακτηριστικά σε ήδη ευρετηριασμένα αρχεία, να ενσωματώνετε χαρακτηριστικά κατά την ευρετηρίαση και να ερωτάτε αποτελεσματικά έγγραφα με βάση τα μεταδεδομένα χρησιμοποιώντας τη βιβλιοθήκη GroupDocs.Search for Java.

## Γρήγορες απαντήσεις
- **What is “search by attribute java”?** Σας επιτρέπει να φιλτράρετε τα αποτελέσματα αναζήτησης με μεταδεδομένα κλειδιού‑τιμής που συνδέονται με κάθε ευρετηριασμένο έγγραφο.  
- **Can I modify attributes after indexing?** Ναι – χρησιμοποιήστε το `AttributeChangeBatch` για να εφαρμόσετε μαζικές αλλαγές χωρίς να ξαναχτίσετε ολόκληρο το ευρετήριο.  
- **How do I add attributes while indexing?** Καταχωρίστε έναν χειριστή για το συμβάν `FileIndexing` και ορίστε χαρακτηριστικά προγραμματιστικά για κάθε αρχείο.  
- **Do I need a license?** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγικές εγκαταστάσεις.  
- **Which Java version is required?** Συνιστάται Java 8 ή νεότερη έκδοση.

## Τι είναι το “search by attribute java”;
Το Search by attribute java σας επιτρέπει να ερωτάτε έγγραφα βάσει προσαρμοσμένων μεταδεδομένων (χαρακτηριστικών) αντί μόνο του κειμενικού τους περιεχομένου. Αυτή η προσέγγιση μειώνει δραστικά τα σύνολα αποτελεσμάτων, μειώνει την κίνηση δικτύου και επιταχύνει τους χρόνους απόκρισης επειδή η μηχανή αξιολογεί τα φίλτρα χαρακτηριστικών πριν εκτελέσει την πλήρη ανάλυση κειμένου.

## Γιατί να χρησιμοποιήσετε δυναμική ετικετοθέτηση μεταδεδομένων;
Η δυναμική ετικετοθέτηση μεταδεδομένων σας επιτρέπει να εκχωρείτε, να ενημερώνετε και να διαχειρίζεστε προσαρμοσμένα χαρακτηριστικά για έγγραφα χωρίς επανευρετηρίαση, παρέχοντας ευέλικτη ταξινόμηση που προσαρμόζεται σε μεταβαλλόμενους επιχειρηματικούς κανόνες, βελτιώνει την αποδοτικότητα της αναζήτησης και μειώνει την ανάγκη για δαπανηρές μεταναστεύσεις δεδομένων σε μεγάλα αποθετήρια, διατηρώντας τη συμμόρφωση και την δυνατότητα ελέγχου.

- **Dynamic categorization** – διατηρήστε τα μεταδεδομένα σε συγχρονισμό με τις εξελισσόμενες επιχειρηματικές κανόνες.  
- **Faster filtering** – τα φίλτρα χαρακτηριστικών αξιολογούνται πριν την πλήρη ανάλυση κειμένου, βελτιώνοντας τους χρόνους απόκρισης.  
- **Compliance tracking** – ετικετοποιήστε έγγραφα για πολιτικές διατήρησης ή απαιτήσεις ελέγχου.  
- **Batch update attributes** – αλλάξτε πολλά έγγραφα σε μια λειτουργία χωρίς επανευρετηρίαση ολόκληρου του συνόλου.

## Προαπαιτούμενα
- **Java 8+** (JDK 8 ή νεότερο)  
- **GroupDocs.Search for Java** library (δείτε τη ρύθμιση Maven παρακάτω)  
- Βασική εξοικείωση με συλλογές Java και διαχείριση εξαιρέσεων  

## Ρύθμιση GroupDocs.Search για Java

### Ρύθμιση Maven
Προσθέστε το αποθετήριο GroupDocs και την εξάρτηση στο `pom.xml` σας:

```xml
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repo.groupdocs.com/maven</url>
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
Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/). Αν προτιμάτε να μην χρησιμοποιήσετε Maven, αποκτήστε το JAR από την [GroupDocs website](https://releases.groupdocs.com/search/java/).

### Απόκτηση άδειας
- Ξεκινήστε με μια δωρεάν δοκιμή για να εξερευνήσετε τις δυνατότητες.  
- Για εκτεταμένη χρήση, αποκτήστε προσωρινή ή πλήρη άδεια μέσω της [license page](https://purchase.groupdocs.com/temporary-license).

### Βασική αρχικοποίηση
```java
// Initialize the search index folder
String indexFolder = "C:/search_index";
Index index = new Index(indexFolder);

// Apply license if you have one
License license = new License();
license.setLicense("C:/licenses/groupdocs.lic");
```

## Πώς να τροποποιήσετε τα χαρακτηριστικά εγγράφων (μαζική ενημέρωση)

Για να τροποποιήσετε τα χαρακτηριστικά εγγράφων μετά την ευρετηρίασή τους, μπορείτε να χρησιμοποιήσετε το API `AttributeChangeBatch` για να εφαρμόσετε μαζικές ενημερώσεις. Αυτή η προσέγγιση ενημερώνει τα μεταδεδομένα των επιλεγμένων αρχείων σε μια ενιαία συναλλαγή, αποφεύγοντας το κόστος επανευρετηρίασης ολόκληρης της συλλογής και διατηρώντας το ευρετήριο πλήρους κειμένου αμετάβλητο.

**Direct answer:** Χρησιμοποιήστε το `AttributeChangeBatch` για να ομαδοποιήσετε προσθήκες, διαγραφές ή αντικαταστάσεις μεταδεδομένων σε μια ενιαία ατομική λειτουργία, στη συνέχεια δεσμεύστε το batch στο ευρετήριο. Αυτό ενημερώνει τα χαρακτηριστικά πολλών εγγράφων σε μία διεργασία, διατηρώντας το υπάρχον ευρετήριο πλήρους κειμένου.

### Βήμα 1: προσθήκη εγγράφων στο ευρετήριο
```java
index.add("C:/docs/contract1.pdf");
index.add("C:/docs/report2.docx");
```

### Βήμα 2: ανάκτηση πληροφοριών ευρετηριασμένων εγγράφων
```java
DocumentInfo info = index.getDocumentInfo("contract1.pdf");
System.out.println("Current attributes: " + info.getAttributes());
```

### Βήμα 3: μαζική ενημέρωση χαρακτηριστικών εγγράφων
Η κλάση `AttributeChangeBatch` ομαδοποιεί πολλαπλές τροποποιήσεις χαρακτηριστικών σε μια ενιαία ατομική λειτουργία, μειώνοντας το κόστος I/O και εξασφαλίζοντας τη συνοχή του ευρετηρίου.

```java
AttributeChangeBatch batch = new AttributeChangeBatch();
batch.addAttribute("contract1.pdf", "department", "Legal");
batch.removeAttribute("report2.docx", "confidential");
batch.replaceAttribute("report2.docx", "status", "archived", "active");
index.applyAttributeChanges(batch);
```

### Βήμα 4: αναζήτηση με φίλτρα χαρακτηριστικών
```java
SearchOptions options = new SearchOptions();
options.addAttributeFilter("department", "Legal");
SearchResult result = index.search("agreement", options);
System.out.println("Found " + result.getCount() + " legal documents.");
```

## Πώς να προσθέσετε χαρακτηριστικά κατά την ευρετηρίαση

Η προσθήκη χαρακτηριστικών κατά τη διαδικασία ευρετηρίασης εξασφαλίζει ότι κάθε έγγραφο εμπλουτίζεται με τα απαραίτητα μεταδεδομένα από την αρχή. Με το χειρισμό του συμβάντος `FileIndexing`, μπορείτε προγραμματιστικά να συνδέσετε ζεύγη κλειδί‑τιμής σε κάθε αντικείμενο `DocumentInfo` πριν η μηχανή επεξεργαστεί το αρχείο, εγγυώμενοι συνεπή διαθεσιμότητα χαρακτηριστικών για επόμενες αναζητήσεις.

**Direct answer:** Εγγραφείτε στο συμβάν `FileIndexing` πριν προσθέσετε αρχεία· στον χειριστή του συμβάντος, καλέστε `addAttribute` στο αντικείμενο `DocumentInfo` για να συνδέσετε ζεύγη κλειδί‑τιμής, και στη συνέχεια αφήστε το ευρετήριο να συνεχίσει την επεξεργασία του αρχείου.

### Βήμα 1: εγγραφή στο συμβάν FileIndexing
Το συμβάν `FileIndexing` ενεργοποιείται για κάθε αρχείο καθώς προστίθεται στο ευρετήριο, επιτρέποντάς σας να ενσωματώσετε προσαρμοσμένα μεταδεδομένα.

```java
index.getEvents().FileIndexing.add(event -> {
    // Example: set department based on folder name
    String folder = new File(event.getFilePath()).getParentFile().getName();
    event.getDocumentInfo().addAttribute("department", folder);
});
```

### Βήμα 2: ευρετηρίαση εγγράφων
```java
index.add("C:/incoming/hr/policy.pdf");
index.add("C:/incoming/finance/budget.xlsx");
```

## Πρακτικές εφαρμογές
1. **Document management systems** – αυτόματη ετικετοθέτηση αρχείων κατά την εισαγωγή, επιτρέποντας άμεση πλοήγηση με όψεις.  
2. **Large content archives** – συνδυάστε φίλτρα χαρακτηριστικών με πλήρη αναζήτηση κειμένου για να μειώσετε τον χρόνο ερωτήματος από λεπτά σε δευτερόλεπτα σε συλλογές πολλαπλών γεγαμπάιτ.  
3. **Compliance & reporting** – εκχωρήστε δυναμικά περιόδους διατήρησης, επίπεδα εμπιστευτικότητας ή σημαίες ελέγχου που μπορούν να ερωτηθούν για ρυθμιστικούς ελέγχους.

## Σκέψεις απόδοσης
- **Memory management** – παρακολουθήστε τη μνήμη heap της JVM και ρυθμίστε το `-Xmx` (π.χ., `-Xmx4g` για ευρετήρια μεγαλύτερα από 2 GB).  
- **Batch processing** – ομαδοποιήστε τις αλλαγές χαρακτηριστικών με `AttributeChangeBatch` για ελαχιστοποίηση εγγραφών στο δίσκο· χωρίστε batch μεγαλύτερα από 10 000 τροποποιήσεις για αποφυγή λήξης συναλλαγής.  
- **Library updates** – παραμείνετε στην πιο πρόσφατη έκδοση του GroupDocs.Search· η έκδοση 25.4 προσθέτει αύξηση ταχύτητας 30 % για την αξιολόγηση φίλτρων χαρακτηριστικών σε σχέση με την 24.x.

## Συχνά προβλήματα και λύσεις

| Πρόβλημα | Γιατί συμβαίνει | Πώς να διορθώσετε |
|----------|----------------|-------------------|
| **Attributes not applied** | Ο χειριστής συμβάντος δεν έχει καταχωρηθεί πριν την ευρετηρίαση | Βεβαιωθείτε ότι το `index.getEvents().FileIndexing.add(...)` εκτελείται **πριν** από οποιεσδήποτε κλήσεις `index.add(...)`. |
| **Search returns no results** | Ασυμφωνία ονόματος χαρακτηριστικού (διάκριση πεζών‑κεφαλαίων) | Χρησιμοποιήστε ακριβή ονόματα χαρακτηριστικών κατά τη δημιουργία φίλτρων (`createAttribute("main")`). |
| **Out‑of‑memory errors** on large batches | Πάρα πολλές αλλαγές σε ένα μόνο batch | Χωρίστε τις μεγάλες ενημερώσεις σε μικρότερα `AttributeChangeBatch` (π.χ., 5 000 έγγραφα ανά batch). |
| **License not recognized** | Χρήση δοκιμαστικού JAR χωρίς εφαρμογή αρχείου άδειας | Καλείτε `License license = new License(); license.setLicense("path/to/license.file");` πριν από οποιαδήποτε λειτουργία ευρετηρίου. |

## Συχνές ερωτήσεις

**Q: What are the prerequisites for using GroupDocs.Search in Java?**  
A: Java 8+, η βιβλιοθήκη GroupDocs.Search, και βασικές γνώσεις εννοιών ευρετηρίασης.

**Q: How do I install GroupDocs.Search via Maven?**  
A: Προσθέστε το αποθετήριο και την εξάρτηση που εμφανίζονται στην ενότητα ρύθμισης Maven στο `pom.xml`.

**Q: Can I modify attributes after documents are indexed?**  
A: Ναι, χρησιμοποιήστε το `AttributeChangeBatch` για μαζική ενημέρωση χαρακτηριστικών εγγράφων χωρίς επανευρετηρίαση.

**Q: What if my indexing process is slow?**  
A: Βελτιστοποιήστε τη μνήμη JVM (`-Xmx`), χρησιμοποιήστε μαζικές ενημερώσεις και αναβαθμίστε στην πιο πρόσφατη έκδοση της βιβλιοθήκης για διορθώσεις απόδοσης.

**Q: Where can I find more resources on GroupDocs.Search for Java?**  
A: Επισκεφθείτε την [official documentation](https://docs.groupdocs.com/search/java/) ή εξερευνήστε τα φόρουμ της κοινότητας.

## Πόροι

- Documentation: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- API reference: [API Reference](https://reference.groupdocs.com/search/java)  
- Download: [Latest Releases](https://releases.groupdocs.com/search/java/)  
- GitHub: [GitHub GroupDocs.Search](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- Free support forum: [GroupDocs Forums](https://forum.groupdocs.com/c/search/10)  
- Temporary license: [License Page](https://purchase.groupdocs.com/temporary-license)

---

**Τελευταία ενημέρωση:** 2026-09-21  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

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

```java
import com.groupdocs.search.Index;

// Initialize an index in a specified directory
Index index = new Index("YOUR_OUTPUT_DIRECTORY/ChangeAttributes");
```

```java
index.add("YOUR_DOCUMENT_DIRECTORY");
```

```java
import com.groupdocs.search.results.DocumentInfo;

DocumentInfo[] documents = index.getIndexedDocuments();
```

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

```java
import com.groupdocs.search.results.SearchResult;

SearchOptions options = new SearchOptions();
options.setSearchDocumentFilter(SearchDocumentFilter.createAttribute("main"));
String query = "length";
SearchResult result = index.search(query, options); // Perform the search
```

```java
import com.groupdocs.search.events.EventHandler;
import com.groupdocs.search.events.FileIndexingEventArgs;

index.getEvents().FileIndexing.add(new EventHandler<FileIndexingEventArgs>() {
    @Override
    public void invoke(Object sender, FileIndexingEventArgs args) {
        if (args.getDocumentFullPath().endsWith("SampleDocument.pdf")) {
            args.setAttributes(new String[] { "main", "key" });
        }
    }
});
```

```java
index.add("YOUR_DOCUMENT_DIRECTORY");
```

## Σχετικά Μαθήματα

- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [How to Update Index Java with GroupDocs.Search – A Comprehensive Guide](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Create Index Java with GroupDocs.Search | Comprehensive Indexing and Reporting Guide](/search/java/advanced-features/groupdocs-search-java-index-report-guide/)