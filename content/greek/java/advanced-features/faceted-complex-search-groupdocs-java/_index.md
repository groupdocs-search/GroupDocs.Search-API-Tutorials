---
date: '2026-08-26'
description: Μάθετε πώς οι τελεστές Boolean Java σας επιτρέπουν να δημιουργήσετε ένα
  γρήγορο ευρετήριο αναζήτησης, να εκτελέσετε αναζήτηση περιεχομένου Java και να τρέξετε
  ερωτήματα με φίλτρα με το GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Μάθετε πώς οι τελεστές Boolean Java σας επιτρέπουν να δημιουργήσετε
  ένα γρήγορο ευρετήριο αναζήτησης, να εκτελέσετε αναζήτηση περιεχομένου Java και
  να εκτελέσετε ερωτήματα με φίλτρα με το GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Τελεστές Boolean Java – δημιουργία ευρετηρίου αναζήτησης και αναζήτησης
  με φίλτρα
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Τελεστές Boolean Java – δημιουργία ευρετηρίου αναζήτησης & αναζήτησης με φίλτρα
type: docs
url: /el/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean operators Java – δημιουργία ευρετηρίου αναζήτησης & αναζήτηση με πτυχία

Η υλοποίηση μιας ισχυρής **εμπειρίας αναζήτησης** σε Java μπορεί να φαίνεται συντριπτική, ειδικά όταν χρειάζεται να **δημιουργήσετε ένα ευρετήριο αναζήτησης Java** που υποστηρίζει **boolean operators Java** για φασέτες και σύνθετα ερωτήματα. Σε αυτό το σεμινάριο θα περάσουμε βήμα‑βήμα τη ρύθμιση του **GroupDocs.Search for Java**, τη δημιουργία ενός ευρετηρίου, την προσθήκη εγγράφων και τη δημιουργία τόσο απλών αναζητήσεων με πτυχία όσο και σύνθετων ερωτημάτων πολλαπλών κριτηρίων που χρησιμοποιούν λογική Boolean. Στο τέλος θα κατανοήσετε πώς να αξιοποιήσετε τις λειτουργίες **content search Java**, **filename search Java** και ακόμη **update index Java** για να διατηρείτε τα δεδομένα σας ενημερωμένα.

## Γρήγορες απαντήσεις
- **Τι είναι η αναζήτηση με πτυχία;** Ένας τρόπος φιλτραρίσματος των αποτελεσμάτων με προκαθορισμένες κατηγορίες όπως τύπος αρχείου ή ημερομηνία.  
- **Πώς δημιουργώ ένα ευρετήριο αναζήτησης Java;** Αρχικοποιήστε ένα αντικείμενο `Index` που δείχνει σε έναν φάκελο και προσθέστε έγγραφα.  
- **Μπορώ να συνδυάσω πολλαπλά κριτήρια με boolean operators;** Ναι—χρησιμοποιήστε ερωτήματα βασισμένα σε αντικείμενα ή Boolean operators σε ερώτημα κειμένου.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· μια εμπορική άδεια αφαιρεί τους περιορισμούς.  
- **Ποιο IDE λειτουργεί καλύτερα;** Οποιοδήποτε Java IDE (IntelliJ IDEA, Eclipse, NetBeans) λειτουργεί καλά.

## Τι είναι το “create search index java”;
Η δημιουργία ενός ευρετηρίου αναζήτησης Java σημαίνει την κατασκευή μιας δομής βασισμένης σε δίσκο που αποθηκεύει το κείμενο των εγγράφων και τα μεταδεδομένα, επιτρέποντας άμεση ανάκτηση των ταιριαστών εγγράφων μέσω ερωτημάτων. Το ευρετήριο αντιστοιχίζει όρους σε αναγνωριστικά εγγράφων, υποστηρίζει γρήγορες αναζητήσεις και μπορεί να ενημερώνεται σταδιακά καθώς τα αρχεία αλλάζουν, παρέχοντας τη βάση για ισχυρές λειτουργίες αναζήτησης.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για φασέτες και σύνθετα ερωτήματα;
Το GroupDocs.Search for Java παρέχει ενσωματωμένη φασέτα, υποστήριξη ερωτημάτων Boolean και υψηλής απόδοσης ευρετηρίαση που μπορεί να διαχειριστεί έως και 10 εκατομμύρια έγγραφα διατηρώντας την καθυστέρηση ερωτήματος κάτω από 200 ms σε τυπικό εξοπλισμό διακομιστή. Προσφέρει έτοιμα φίλτρα πεδίου, πλούσια γλώσσα ερωτημάτων και καθαρή συμβατότητα Java, καθιστώντας το ιδανικό για επιχειρησιακά σενάρια αναζήτησης μεγάλης κλίμακας.

## Προαπαιτούμενα

- **JDK 8 ή νεότερο** εγκατεστημένο και ρυθμισμένο στο IDE σας.  
- **Maven** (ή Gradle) για διαχείριση εξαρτήσεων.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Βασική εξοικείωση με τις έννοιες OOP της Java και τη δομή έργου Maven.

## Ρύθμιση του GroupDocs.Search for Java

### Ρύθμιση Maven
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

### Άμεση λήψη
Εναλλακτικά, κατεβάστε το πιο πρόσφατο JAR από τη σελίδα επίσημης κυκλοφορίας:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Απόκτηση άδειας
Για να ξεκλειδώσετε πλήρη λειτουργικότητα:

1. **Δωρεάν δοκιμή** – ιδανική για ανάπτυξη και δοκιμές.  
2. **Προσωρινή άδεια αξιολόγησης** – επεκτείνει τους περιορισμούς της δοκιμής.  
3. **Εμπορική άδεια** – αφαιρεί όλους τους περιορισμούς για χρήση σε παραγωγή.

### Βασική αρχικοποίηση και ρύθμιση
Η κλάση `Index` είναι το κύριο στοιχείο που αντιπροσωπεύει ένα ευρετήριο αναζήτησης αποθηκευμένο σε δίσκο. Το παρακάτω απόσπασμα δείχνει πώς να **δημιουργήσετε ένα ευρετήριο αναζήτησης Java** δημιουργώντας ένα αντικείμενο της κλάσης `Index`:

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

Με το ευρετήριο έτοιμο, μπορούμε να προχωρήσουμε σε πραγματικές φασέτες και σύνθετα ερωτήματα.

## Πώς να χρησιμοποιήσετε boolean operators java – Απλή αναζήτηση με πτυχία

Φορτώστε το ευρετήριό σας, προσθέστε έγγραφα και εκτελέστε ένα ερώτημα πεδίου· το μοτίβο δύο βημάτων σας επιτρέπει να ανακτήσετε μετρήσεις πτυχίων και φιλτραρισμένα αποτελέσματα σε μία κλήση. Αυτή η προσέγγιση παρέχει στους χρήστες έναν διαισθητικό τρόπο να περιορίζουν τα αποτελέσματα ανά κατηγορίες όπως τύπος αρχείου, συγγραφέας ή προσαρμοσμένα μεταδεδομένα.

### Βήμα 1: Δημιουργία ευρετηρίου
Πρώτα, δείξτε το `Index` σε έναν φάκελο όπου θα αποθηκευτούν τα αρχεία του ευρετηρίου.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Βήμα 2: Προσθήκη εγγράφων στο ευρετήριο
Ενημερώστε το GroupDocs.Search πού βρίσκονται τα πηγαία έγγραφά σας. Όλοι οι υποστηριζόμενοι τύποι αρχείων (PDF, DOCX, TXT κ.λπ.) θα ευρετηριαστούν αυτόματα.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Βήμα 3: Εκτέλεση αναζήτησης στο πεδίο content με ερώτημα κειμένου
Ένα γρήγορο ερώτημα κειμένου φιλτράρει με βάση το πεδίο `content`. Η σύνταξη `content: Pellentesque` περιορίζει τα αποτελέσματα σε έγγραφα που περιέχουν τη λέξη *Pellentesque* στο κυρίως κείμενο.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Βήμα 4: Εκτέλεση αναζήτησης χρησιμοποιώντας ερώτημα αντικειμένου
Τα ερωτήματα βασισμένα σε αντικείμενα σας δίνουν λεπτομερή έλεγχο. Εδώ δημιουργούμε ένα ερώτημα λέξης, το ενσωματώνουμε σε ερώτημα πεδίου και το εκτελούμε.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Πώς να χρησιμοποιήσετε boolean operators java – Σύνθετη αναζήτηση ερωτημάτων

Για να εκτελέσετε ένα σύνθετο ερώτημα, συνδυάστε πολλαπλές συνθήκες πεδίου με τελεστές AND/OR/NOT και προαιρετικά συμπεριλάβετε αναζητήσεις φράσεων. Μπορείτε να καθορίσετε κάθε συνθήκη χρησιμοποιώντας ερωτήματα πεδίου, να τα ενσωματώσετε με Boolean operators και να ελέγξετε τη συνάφεια με ενίσχυση, επιτρέποντας την ανάκτηση μόνο των πιο σχετικών εγγράφων που ικανοποιούν όλα τα απαιτούμενα κριτήρια.

### Βήμα 1: Δημιουργία ευρετηρίου για σύνθετα ερωτήματα
Ξαναχρησιμοποιήστε την ίδια δομή φακέλων· μπορείτε να μοιραστείτε το ευρετήριο και για απλά και για σύνθετα σενάρια.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Βήμα 2: Εκτέλεση αναζήτησης με ερώτημα κειμένου
Το παρακάτω ερώτημα αναζητά αρχεία με όνομα *lorem* **και** *ipsum* **ή** περιεχόμενο που περιέχει μία από τις δύο ακριβείς φράσεις.

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

### Βήμα 3: Εκτέλεση αναζήτησης με ερώτημα αντικειμένου
Η κατασκευή βασισμένη σε αντικείμενα αντικατοπτρίζει το κειμενικό ερώτημα αλλά προσφέρει ασφάλεια τύπου και βοήθεια από το IDE.

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

## Πρακτικές εφαρμογές φασέτας & σύνθετων αναζητήσεων

| Σενάριο | Πώς βοηθά η φασέτα | Παράδειγμα ερωτήματος |
|----------|-------------------|---------------|
| **Κατάλογος ηλεκτρονικού εμπορίου** | Φιλτράρισμα ανά κατηγορία, τιμή, μάρκα | `category: Electronics AND price:[100 TO 500]` |
| **Αποθετήριο νομικών εγγράφων** | Περιορισμός ανά αριθμό υπόθεσης, δικαιοδοσία | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Αρχεία έρευνας** | Συνδυασμός συγγραφέα, έτους δημοσίευσης, λέξεων-κλειδιών | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Εταιρικό εσωτερικό δίκτυο** | Αναζήτηση ανά τύπο αρχείου και τμήμα | `filetype: pdf AND department: HR` |

Αυτά τα παραδείγματα δείχνουν γιατί η εξοικείωση με τις τεχνικές **boolean operators java** και **filename search java** αποτελεί αλλαγή παιχνιδιού για κάθε εφαρμογή με έντονη χρήση δεδομένων.

## Συχνά προβλήματα & αντιμετώπιση σφαλμάτων

Το αντικείμενο `SearchResult` περιέχει τα έγγραφα που ταιριάζουν σε ένα ερώτημα και παρέχει πρόσβαση στις βαθμολογίες συνάφειας και στα επισημασμένα τμήματα.  
Η κλάση `CommonFieldNames` ορίζει τυπικά ονόματα πεδίων όπως `Content` και `FileName` που χρησιμοποιούνται σε όλη τη διεπαφή API.

- **Κενά αποτελέσματα** – Επαληθεύστε ότι τα έγγραφα προστέθηκαν επιτυχώς (`index.getDocumentCount()` μπορεί να βοηθήσει).  
- **Παλαιό ευρετήριο** – Μετά την προσθήκη ή αφαίρεση αρχείων, καλέστε `index.update()` για **update index java** και διατηρήστε το ευρετήριο συγχρονισμένο.  
- **Λανθασμένα ονόματα πεδίων** – Χρησιμοποιήστε τις σταθερές `CommonFieldNames` (`Content`, `FileName`, κ.λπ.) για να αποφύγετε τυπογραφικά λάθη.  
- **Σημεία συμφόρησης απόδοσης** – Για τεράστιες συλλογές, σκεφτείτε την ενεργοποίηση του `index.setCacheSize()` ή τη χρήση αποκλειστικού SSD για το φάκελο του ευρετηρίου.  
- **Απουσία επισημάνσεων** – Για **highlight search results java**, ανακτήστε τα ταιριαστά τμήματα μέσω `SearchResult.getFragments()` (δεν εμφανίζεται εδώ αλλά είναι διαθέσιμο στην API).

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs.Search με Spring Boot;**  
A: Απολύτως. Προσθέστε την εξάρτηση Maven, διαμορφώστε το ευρετήριο ως bean του Spring και ενσωματώστε το όπου χρειάζεστε δυνατότητες αναζήτησης.

**Q: Υποστηρίζει η βιβλιοθήκη προσαρμοσμένα πεδία μεταδεδομένων;**  
A: Ναι – μπορείτε να προσθέσετε πεδία ορισμένα από τον χρήστη κατά την ευρετηρίαση και στη συνέχεια να φασέταρετε πάνω τους.

**Q: Πόσο μεγάλο μπορεί να γίνει το ευρετήριο;**  
A: Το ευρετήριο βασισμένο σε δίσκο μπορεί να διαχειριστεί έως και 10 εκατομμύρια έγγραφα· απλώς εξασφαλίστε επαρκή αποθηκευτικό χώρο και παρακολουθήστε τις ρυθμίσεις cache.

**Q: Υπάρχει τρόπος να ταξινομήσετε τα αποτελέσματα κατά συνάφεια;**  
A: Το GroupDocs.Search βαθμολογεί αυτόματα τις αντιστοιχίες· μπορείτε να ανακτήσετε τη βαθμολογία μέσω `SearchResult.getDocument(i).getScore()`.

**Q: Τι συμβαίνει αν ευρετηριάσω κρυπτογραφημένα PDF;**  
A: Παρέχετε τον κωδικό πρόσβασης κατά την προσθήκη του εγγράφου: `index.add(filePath, password)`.

## Συμπέρασμα

Τώρα θα πρέπει να αισθάνεστε άνετα με τη **δημιουργία ενός ευρετηρίου αναζήτησης Java** με το GroupDocs.Search, την προσθήκη εγγράφων και τη δημιουργία τόσο απλών ερωτημάτων με πτυχία όσο και σύνθετων αναζητήσεων Boolean χρησιμοποιώντας **boolean operators java**. Αυτές οι δυνατότητες σας επιτρέπουν να προσφέρετε γρήγορες, ακριβείς και φιλικές προς τον χρήστη εμπειρίες αναζήτησης σε ένα ευρύ φάσμα εφαρμογών—από πλατφόρμες ηλεκτρονικού εμπορίου μέχρι επιχειρησιακές βάσεις γνώσης.

Έτοιμοι για το επόμενο βήμα; Εξερευνήστε τις προχωρημένες δυνατότητες του **GroupDocs.Search**, όπως **highlighting**, **suggestions**, και **real‑time indexing**, για να ενισχύσετε περαιτέρω τη δυνατότητα αναζήτησης της εφαρμογής σας.

---

**Τελευταία ενημέρωση:** 2026-08-26  
**Δοκιμή με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

## Σχετικά Σεμινάρια

- [Αναζήτηση μπαλαντέρ Java με GroupDocs.Search – Προηγμένες δυνατότητες](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Πώς να ενημερώσετε το ευρετήριο Java με το GroupDocs.Search – Ένας ολοκληρωμένος οδηγός](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Πώς να υλοποιήσετε πλήρη αναζήτηση κειμένου java: δημιουργία καταλόγου ευρετηρίου με το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)