---
date: '2026-11-02'
description: Μάθετε πώς να προσθέσετε φάκελο στο ευρετήριο με το GroupDocs.Search
  σε Java, να διαμορφώσετε high compression και να εκτελείτε γρήγορα full‑text queries.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Μάθετε πώς να προσθέσετε φάκελο στο ευρετήριο με το GroupDocs.Search
  σε Java, να διαμορφώσετε compression και να εκτελείτε γρήγορες full‑text searches.
  Ιδανικό για μεγάλα σύνολα εγγράφων.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Πώς να προσθέσετε φάκελο στο ευρετήριο με το GroupDocs.Search σε Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: Πώς να προσθέσετε φάκελο στο ευρετήριο με το GroupDocs.Search σε Java
type: docs
url: /el/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# Πώς να προσθέσετε φάκελο στο ευρετήριο με το GroupDocs.Search σε Java

Αν χρειάζεστε **java full text search** που μπορεί να κλιμακωθεί σε εκατομμύρια έγγραφα, βρίσκεστε στο σωστό μέρος. Σε αυτό το σεμινάριο θα μάθετε πώς να **add folder to index** χρησιμοποιώντας το GroupDocs.Search, να διαμορφώσετε αποθήκευση υψηλής συμπίεσης και να εκτελέσετε εξαιρετικά γρήγορα ερωτήματα. Στο τέλος θα έχετε μια λύση έτοιμη για παραγωγή που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

## Γρήγορες απαντήσεις
- **Ποια είναι η κύρια βιβλιοθήκη;** GroupDocs.Search for Java  
- **Πώς να προσθέσετε φάκελο στο ευρετήριο;** Use `index.add(folderPath)`  
- **Μπορώ να διαμορφώσω συμπίεση κειμένου;** Yes, via `TextStorageSettings(Compression.High)`  
- **Ποια έκδοση Java απαιτείται;** JDK 8 or higher  
- **Από πού μπορώ να αποκτήσω δοκιμαστική άδεια;** From the GroupDocs website or the repository page  

## Τι είναι η java full text search και γιατί είναι σημαντική;
Η java full text search μετατρέπει ακατέργαστα έγγραφα σε ανεστραμμένο ευρετήριο, επιτρέποντας ανάκτηση υποδευτερολέπτου οποιουδήποτε όρου σε χιλιάδες αρχεία. Αυτή η δυνατότητα είναι απαραίτητη για νομικές αποθήκες, ερευνητικές βιβλιοθήκες και επιχειρησιακές βάσεις γνώσης όπου οι χρήστες αναμένουν άμεσα αποτελέσματα. Επίσης βελτιώνει την παραγωγικότητα σε σύγχρονες εφαρμογές.

## Γιατί να χρησιμοποιήσετε το groupdocs.search για java full text search;
Το GroupDocs.Search παρέχει υψηλή απόδοση ευρετηρίου και εκτέλεσης ερωτημάτων ενώ προσφέρει ενσωματωμένη υψηλή συμπίεση. Υποστηρίζει **50+ input and output formats** — συμπεριλαμβανομένων των PDF, DOCX, EML και HTML — και μπορεί να επεξεργαστεί έγγραφα πολλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, διατηρώντας το αποτύπωμα μνήμης κάτω από 200 MB για τυπικά φορτία εργασίας.

## Προαπαιτούμενα
- **GroupDocs.Search for Java** (version 25.4 or later) – η βασική βιβλιοθήκη που τροφοδοτεί το ευρετήριο και την αναζήτηση.  
- **JDK 8+** εγκατεστημένο και διαμορφωμένο – το ελάχιστο runtime που απαιτείται για το SDK.  
- **Maven** για διαχείριση εξαρτήσεων – απλοποιεί την προσθήκη της βιβλιοθήκης στο έργο σας.  
- Ένα IDE όπως το **IntelliJ IDEA** ή το **Eclipse** – για συγγραφή και αποσφαλμάτωση κώδικα Java.  

## Ρύθμιση του GroupDocs.Search για java

### Ρύθμιση Maven
Προσθέστε το αποθετήριο και την εξάρτηση στο αρχείο `pom.xml` σας:

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
Εναλλακτικά, κατεβάστε την τελευταία έκδοση από [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Απόκτηση άδειας
- **Free trial** – εξερευνήστε όλες τις δυνατότητες χωρίς δέσμευση.  
- **Temporary license** – παρατεταμένη περίοδος δοκιμής.  
- **Purchase** – ξεκλειδώστε πλήρεις δυνατότητες παραγωγής.  

### Βασική αρχικοποίηση και ρύθμιση
`Index` είναι η βασική κλάση που χρησιμοποιείται για δημιουργία, άνοιγμα και διαχείριση ενός ευρετηρίου αναζήτησης.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Ευρετηρίαση κειμένου με προσαρμοσμένη συμπίεση

### Βήμα 1: ορίστε το φάκελο του ευρετηρίου
Επιλέξτε έναν φάκελο όπου θα αποθηκευτούν τα αρχεία του ευρετηρίου:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Βήμα 2: διαμορφώστε τις ρυθμίσεις του ευρετηρίου
`TextStorageSettings` διαμορφώνει τον τρόπο αποθήκευσης του κειμένου στο ευρετήριο, συμπεριλαμβανομένου του επιπέδου συμπίεσης. `Compression` είναι ένα enum που καθορίζει τον επιθυμητό αλγόριθμο συμπίεσης.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Βήμα 3: δημιουργήστε το ευρετήριο με προσαρμοσμένες ρυθμίσεις
Δημιουργήστε το ευρετήριο χρησιμοποιώντας τη διαμόρφωση που ορίστηκε παραπάνω:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Πώς να προσθέσετε φάκελο στο ευρετήριο
`Index` είναι η κύρια κλάση που αντιπροσωπεύει το ευρετήριο αναζήτησης.

Φορτώστε το υπάρχον ευρετήριο (ή δημιουργήστε ένα νέο) και στη συνέχεια καλέστε τη μέθοδο `add` στο αντικείμενο `Index`. Η λειτουργία `add` σαρώει τον παρεχόμενο φάκελο, εξάγει κείμενο από κάθε υποστηριζόμενο αρχείο και το αποθηκεύει στο συμπιεσμένο ευρετήριο, έτοιμο για άμεση αναζήτηση.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## Πώς να αναζητήσετε τα ευρετηριασμένα έγγραφα
`SearchResult` αντιπροσωπεύει ένα μεμονωμένο αποτέλεσμα με τη διαδρομή του εγγράφου και τη σχετικότητα.

Ορίστε μια συμβολοσειρά ερωτήματος αναζήτησης που αντιπροσωπεύει τον όρο ή τη φράση που θέλετε να εντοπίσετε, στη συνέχεια καλέστε τη μέθοδο `search` στο αντικείμενο `Index`. Η μέθοδος επιστρέφει μια συλλογή από αντικείμενα `SearchResult`, το καθένα περιέχει τη διαδρομή του εγγράφου, το σκορ σχετικότητας και ένα απόσπασμα που επισημαίνει το αποτέλεσμα.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Πρακτικές εφαρμογές
Πραγματικά σενάρια όπου η **java full text search** διαπρέπει:
1. **Legal document management** – άμεση ανάκτηση αρχείων υποθέσεων.  
2. **Academic research libraries** – γρήγορη αναζήτηση ερευνών και διπλωματικών.  
3. **Enterprise knowledge bases** – γρήγορη πρόσβαση σε εγχειρίδια και Συχνές Ερωτήσεις.  
4. **Content management systems** – αποδοτική ανακάλυψη περιεχομένου για μεγάλους ιστότοπους.  
5. **Customer service archives** – γρήγορη αναζήτηση παλαιών αιτημάτων και συνομιλιών.  

## Παράγοντες απόδοσης
- **Compression vs. speed**: Η υψηλή συμπίεση εξοικονομεί έως και 70 % του χώρου στο δίσκο, αλλά προσθέτει ένα μέτριο κόστος ευρετηρίου· εκτελέστε δοκιμές απόδοσης για τον όγκο των δεδομένων σας.  
- **Memory management**: Κατανείμετε τουλάχιστον 2 GB heap για ευρετήρια μεγαλύτερα από 10 GB ώστε να αποφύγετε το `OutOfMemoryError`.  
- **Index updates**: Προσθέτετε σταδιακά νέα έγγραφα με `index.add()` και περιοδικά καλείτε το `index.optimize()` για να διατηρήσετε το ευρετήριο συμπαγές.  
- **Query optimization**: Χρησιμοποιήστε την προχωρημένη σύνταξη ερωτημάτων (wildcards, proximity, fuzzy search) για να περιορίσετε τα αποτελέσματα και να μειώσετε τον χρόνο απόκρισης.  

## Συνηθισμένα λάθη & συμβουλές
- **Pitfall:** Ξεχάσατε να καλέσετε το `index.optimize()` μετά από μαζικές προσθήκες.  
  **Pro tip:** Εκτελέστε το `index.optimize()` κάθε βράδυ για να διατηρήσετε το ευρετήριο συμπαγές.  

- **Pitfall:** Χρήση της προεπιλεγμένης (χαμηλής) συμπίεσης σε τεράστιες βάσεις δεδομένων.  
  **Pro tip:** Μεταβείτε στο `Compression.High` για περιβάλλοντα παραγωγής ώστε να μειώσετε το κόστος αποθήκευσης.  

- **Pitfall:** Μη διαχείριση του `IOException` κατά την προσθήκη αρχείων από δικτυακό κοινόχρηστο.  
  **Pro tip:** Τυλίξτε το `index.add()` σε block try‑catch και καταγράψτε τυχόν αποτυχίες για μελλοντική ανασκόπηση.  

## Συχνές ερωτήσεις
**Q: Τι είναι το GroupDocs.Search?**  
A: Είναι μια ισχυρή βιβλιοθήκη Java που παρέχει προηγμένες δυνατότητες full‑text search, συμπεριλαμβανομένου του ευρετηρίου, της συμπίεσης και της υποστήριξης σύνθετων ερωτημάτων.

**Q: Πώς διαχειρίζομαι μεγάλες βάσεις δεδομένων με το GroupDocs.Search;**  
A: Ενεργοποιήστε την υψηλή συμπίεση (`Compression.High`) και περιοδικά δεσμεύστε τις αλλαγές για να διατηρήσετε το ευρετήριο ελαφρύ. Επίσης, διαθέστε επαρκή μνήμη heap (π.χ., 4 GB για ευρετήρια άνω των 20 GB).

**Q: Μπορώ να ενσωματώσω το GroupDocs.Search σε υπάρχοντα επιχειρηματικά συστήματα;**  
A: Ναι, η βιβλιοθήκη μπορεί να ενσωματωθεί σε οποιοδήποτε backend βασισμένο σε Java, υπηρεσίες REST ή αρχιτεκτονική μικρο‑υπηρεσιών.

**Q: Τι γίνεται αν το ευρετήριό μου γίνει παρωχημένο;**  
A: Χρησιμοποιήστε τη μέθοδο `index.add()` για να προσθέσετε νέα αρχεία και το `index.delete()` για να αφαιρέσετε παλαιά, στη συνέχεια εκτελέστε ξανά το `index.optimize()` αν χρειάζεται.

**Q: Πού μπορώ να λάβω βοήθεια ή υποστήριξη;**  
A: Επισκεφθείτε το φόρουμ της κοινότητας στο [GroupDocs forums](https://forum.groupdocs.com/c/search/10) για αντιμετώπιση προβλημάτων και συμβουλές βέλτιστων πρακτικών.

## Πρόσθετοι πόροι
- Λεπτομερής οδηγός χρήσης: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Πλήρης αναφορά API: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Μείνετε ενημερωμένοι για νέες λειτουργίες: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Τελευταία ενημέρωση:** 2026-11-02  
**Δοκιμάστηκε με:** GroupDocs.Search 25.4  
**Συγγραφέας:** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Σχετικά Μαθήματα
- [Οδηγός Δημιουργίας Ευρετηρίου Groupdocs Search Java](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Οδηγός Διαχείρισης Ευρετηρίου Groupdocs Search Java](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Βιβλιοθήκη Java Full Text Search – Βελτιστοποίηση Ευρετηρίου με GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)