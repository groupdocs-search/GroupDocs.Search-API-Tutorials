---
date: '2026-02-16'
description: Μάθετε πώς να χρησιμοποιείτε λογικούς τελεστές Java με το GroupDocs.Search
  για να δημιουργήσετε ένα ευρετήριο αναζήτησης, να εκτελείτε αναζήτηση περιεχομένου
  Java και ερωτήματα φάσεων, ενισχύοντας την απόδοση και την εμπειρία του χρήστη.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Λογικοί τελεστές Java – Δημιουργία ευρετηρίου αναζήτησης & πολυδιάστατη αναζήτηση
type: docs
url: /el/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean Operators Java – Create Search Index & Faceted Search

Η υλοποίηση μιας ισχυρής **εμπειρίας αναζήτησης** σε Java μπορεί να φαίνεται δύσκολη, ειδικά όταν χρειάζεται να **δημιουργήσετε έναν δείκτη αναζήτησης Java** που υποστηρίζει **boolean operators Java** για faceted και σύνθετα ερωτήματα. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τη ρύθμιση του **GroupDocs.Search for Java**, τη δημιουργία ενός δείκτη, την προσθήκη εγγράφων και τη δημιουργία τόσο απλών faceted αναζητήσεων όσο και σύνθετων ερωτημάτων πολλαπλών κριτηρίων που χρησιμοποιούν λογική Boolean. Στο τέλος θα καταλάβετε πώς να αξιοποιήσετε τις λειτουργίες **content search Java**, **filename search Java**, και ακόμη **update index java** για να διατηρείτε τα δεδομένα σας ενημερωμένα.

## Quick Answers
- **Τι είναι μια faceted search;** Ένας τρόπος φιλτραρίσματος των αποτελεσμάτων με βάση προ‑ορισμένες κατηγορίες όπως τύπος αρχείου ή ημερομηνία.  
- **Πώς δημιουργώ έναν δείκτη αναζήτησης Java;** Αρχικοποιήστε ένα αντικείμενο `Index` που δείχνει σε φάκελο και προσθέστε έγγραφα.  
- **Μπορώ να συνδυάσω πολλαπλά κριτήρια με boolean operators;** Ναι—χρησιμοποιήστε ερωτήματα βασισμένα σε αντικείμενα ή Boolean operators σε ερώτημα κειμένου.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· μια εμπορική άδεια αφαιρεί τους περιορισμούς.  
- **Ποιο IDE είναι το καλύτερο;** Οποιοδήποτε Java IDE (IntelliJ IDEA, Eclipse, NetBeans) λειτουργεί καλά.

## What is “create search index java”?
Η δημιουργία ενός δείκτη αναζήτησης σε Java σημαίνει την κατασκευή μιας δομής δεδομένων αναζητήσιμης μορφής που αποθηκεύει μεταδεδομένα και περιεχόμενο εγγράφων, επιτρέποντας γρήγορη ανάκτηση βάσει ερωτημάτων χρήστη. Με το GroupDocs.Search, ο δείκτης αποθηκεύεται στο δίσκο, μπορεί να ενημερώνεται σταδιακά και υποστηρίζει προ‑προχωρημένες λειτουργίες όπως faceting, **boolean operators Java**, και σύνθετη λογική Boolean.

## Why use GroupDocs.Search for faceted and complex queries?
- **Out‑of‑the‑box faceting** – φιλτράρισμα ανά πεδία όπως όνομα αρχείου, μέγεθος ή προσαρμοσμένα μεταδεδομένα.  
- **Rich query language** – συνδυάστε ερωτήματα κειμένου, φράσης και πεδίου χρησιμοποιώντας τους τελεστές AND/OR/NOT (η καρδιά των **boolean operators java**).  
- **Scalable performance** – δείκτες που διαχειρίζονται εκατομμύρια έγγραφα με χαμηλή καθυστέρηση.  
- **Pure Java** – χωρίς εξαρτήσεις native, λειτουργεί σε οποιαδήποτε πλατφόρμα με JDK 8+.  
- **Easy index maintenance** – καλέστε `index.update()` για **update index java** μετά την προσθήκη ή αφαίρεση αρχείων.

## Prerequisites

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- **JDK 8 ή νεότερο** εγκατεστημένο και ρυθμισμένο στο IDE σας.  
- **Maven** (ή Gradle) για διαχείριση εξαρτήσεων.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Βασική εξοικείωση με τις έννοιες OOP της Java και τη δομή έργου Maven.

## Setting Up GroupDocs.Search for Java

### Maven Setup
Προσθέστε το αποθετήριο και την εξάρτηση στο αρχείο `pom.xml`:

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

### Direct Download
Εναλλακτικά, κατεβάστε το τελευταίο JAR από τη σελίδα κυκλοφορίας:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### License Acquisition
Για να ξεκλειδώσετε πλήρη λειτουργικότητα:

1. **Free trial** – ιδανική για ανάπτυξη και δοκιμές.  
2. **Temporary evaluation license** – επεκτείνει τα όρια της δοκιμής.  
3. **Commercial license** – αφαιρεί όλους τους περιορισμούς για παραγωγική χρήση.

### Basic Initialization and Setup
Το παρακάτω απόσπασμα δείχνει πώς να **create a search index Java** δημιουργώντας ένα αντικείμενο `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

Με τον δείκτη έτοιμο, μπορούμε να προχωρήσουμε σε πραγματικές faceted και σύνθετες ερωτήσεις.

## How to use boolean operators java – Simple Faceted Search

Η faceted search επιτρέπει στους τελικούς χρήστες να περιορίζουν τα αποτελέσματα επιλέγοντας τιμές από προ‑ορισμένες κατηγορίες (facets). Ακολουθεί ένας βήμα‑βήμα οδηγός.

### Step 1: Create an Index
Πρώτα, κατευθύνετε το `Index` σε έναν φάκελο όπου θα αποθηκευτούν τα αρχεία του δείκτη.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Step 2: Add Documents to the Index
Δώστε στο GroupDocs.Search τη θέση των πηγαίων εγγράφων σας. Όλοι οι υποστηριζόμενοι τύποι αρχείων (PDF, DOCX, TXT κ.λπ.) θα ευρετηριαστούν αυτόματα.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Step 3: Perform a Search in the Content Field with a Text Query
Ένα γρήγορο ερώτημα κειμένου φιλτράρει με βάση το πεδίο `content`. Η σύνταξη `content: Pellentesque` περιορίζει τα αποτελέσματα σε έγγραφα που περιέχουν τη λέξη *Pellentesque* στο κυρίως κείμενο.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Step 4: Perform a Search Using an Object Query
Τα ερωτήματα βασισμένα σε αντικείμενα προσφέρουν λεπτομερή έλεγχο. Εδώ δημιουργούμε ένα word query, το ενσωματώνουμε σε ένα field query και το εκτελούμε.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## How to use boolean operators java – Complex Query Search

Τα σύνθετα ερωτήματα συνδυάζουν πολλαπλά πεδία, Boolean operators και αναζητήσεις φράσεων. Είναι ιδανικά για σενάρια όπως φίλτρα e‑commerce ή έρευνα νομικών εγγράφων.

### Step 1: Create an Index for Complex Queries
Ξαναχρησιμοποιήστε την ίδια δομή φακέλων· μπορείτε να μοιραστείτε τον δείκτη μεταξύ απλών και σύνθετων σεναρίων.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Step 2: Perform a Search with a Text Query
Το παρακάτω ερώτημα ψάχνει αρχεία με όνομα *lorem* **και** *ipsum* **ή** περιεχόμενο που περιέχει μία από τις δύο ακριβείς φράσεις.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Step 3: Perform a Search with an Object Query
Η κατασκευή με αντικείμενα αντικατοπτρίζει το κειμενικό ερώτημα αλλά προσφέρει ασφάλεια τύπου και υποστήριξη IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Practical Applications of Faceted & Complex Searches

| Scenario | How Faceting Helps | Example Query |
|----------|-------------------|---------------|
| **E‑commerce catalog** | Φιλτράρισμα ανά κατηγορία, τιμή, μάρκα | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | Περιορισμός ανά αριθμό υπόθεσης, δικαιοδοσία | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | Συνδυασμός συγγραφέα, έτους δημοσίευσης, λέξεων‑κλειδιών | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | Αναζήτηση ανά τύπο αρχείου και τμήμα | `filetype: pdf AND department: HR` |

Αυτά τα παραδείγματα δείχνουν γιατί η εξοικείωση με τις τεχνικές **boolean operators java** και **filename search java** αποτελεί καθοριστικό πλεονέκτημα για κάθε εφαρμογή με έντονη χρήση δεδομένων.

## Common Pitfalls & Troubleshooting

- **Empty results** – Ελέγξτε ότι τα έγγραφα προστέθηκαν επιτυχώς (`index.getDocumentCount()` μπορεί να βοηθήσει).  
- **Stale index** – Μετά την προσθήκη ή αφαίρεση αρχείων, καλέστε `index.update()` για **update index java** και διατηρήστε τον δείκτη συγχρονισμένο.  
- **Incorrect field names** – Χρησιμοποιήστε τις σταθερές `CommonFieldNames` (`Content`, `FileName`, κ.λπ.) για να αποφύγετε τυπογραφικά λάθη.  
- **Performance bottlenecks** – Για τεράστιες συλλογές, εξετάστε το ενδεχόμενο ενεργοποίησης `index.setCacheSize()` ή χρήση dedicated SSD για το φάκελο του δείκτη.  
- **Missing highlights** – Για **highlight search results java**, ανακτήστε τα τμήματα που ταιριάζουν μέσω `SearchResult.getFragments()` (δεν εμφανίζεται εδώ αλλά είναι διαθέσιμο στο API).  

## Frequently Asked Questions

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs.Search με Spring Boot;**  
A: Απολύτως. Προσθέστε την εξάρτηση Maven, διαμορφώστε τον δείκτη ως Spring bean και κάντε inject όπου χρειάζεστε δυνατότητες αναζήτησης.

**Q: Υποστηρίζει η βιβλιοθήκη προσαρμοσμένα πεδία μεταδεδομένων;**  
A: Ναι – μπορείτε να προσθέσετε πεδία ορισμένα από τον χρήστη κατά την ευρετηρίαση και στη συνέχεια να κάνετε faceting πάνω σε αυτά.

**Q: Πόσο μεγάλος μπορεί να γίνει ο δείκτης;**  
A: Ο δείκτης είναι βασισμένος σε δίσκο και μπορεί να διαχειριστεί εκατομμύρια έγγραφα· απλώς εξασφαλίστε επαρκή αποθηκευτικό χώρο και παρακολουθήστε τις ρυθμίσεις cache.

**Q: Υπάρχει τρόπος να ταξινομήσω τα αποτελέσματα κατά συνάφεια;**  
A: Το GroupDocs.Search βαθμολογεί αυτόματα τις αντιστοιχίες· μπορείτε να ανακτήσετε τη βαθμολογία μέσω `SearchResult.getDocument(i).getScore()`.

**Q: Τι γίνεται αν ευρετηριάσω κρυπτογραφημένα PDF;**  
A: Παρέχετε τον κωδικό πρόσβασης κατά την προσθήκη του εγγράφου: `index.add(filePath, password)`.

## Conclusion

Μέχρι τώρα θα πρέπει να αισθάνεστε άνετα με τη **δημιουργία ενός δείκτη αναζήτησης Java** χρησιμοποιώντας το GroupDocs.Search, την προσθήκη εγγράφων και τη δημιουργία τόσο απλών faceted ερωτημάτων όσο και σύνθετων Boolean αναζητήσεων με **boolean operators java**. Αυτές οι δυνατότητες σας επιτρέπουν να προσφέρετε γρήγορες, ακριβείς και φιλικές προς το χρήστη εμπειρίες αναζήτησης σε ένα ευρύ φάσμα εφαρμογών—από πλατφόρμες e‑commerce μέχρι εταιρικές βάσεις γνώσης.

Έτοιμοι για το επόμενο βήμα; Εξερευνήστε τις προ‑προχωρημένες λειτουργίες του **GroupDocs.Search** όπως **highlighting**, **suggestions**, και **real‑time indexing** για να ενισχύσετε ακόμη περισσότερο τη δύναμη αναζήτησης της εφαρμογής σας.

---

**Last Updated:** 2026-02-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs