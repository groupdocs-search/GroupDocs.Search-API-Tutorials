---
date: '2026-07-21'
description: Το tutorial Create Boolean Query Java δείχνει πώς να υλοποιήσετε αναζητήσεις
  boolean AND, OR, NOT χρησιμοποιώντας το GroupDocs.Search for Java, να προσθέσετε
  έγγραφα σε ένα index και να boost την ανάκτηση εγγράφων.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Το tutorial Create Boolean Query Java εξηγεί βήμα‑βήμα πώς να δημιουργήσετε
  ερωτήματα AND, OR, NOT με το GroupDocs.Search for Java, να προσθέσετε έγγραφα σε
  ένα index και να βελτιώσετε την απόδοση της ανάκτησης.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – Κατακτήστε τις Boolean αναζητήσεις με το GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Δημιουργία ερωτήματος Boolean Java: Κατακτήστε τις Boolean αναζητήσεις με
  το GroupDocs.Search for Java'
type: docs
url: /el/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Δημιουργία Boolean Query Java: Μάθετε τις Boolean Αναζητήσεις με το GroupDocs.Search για Java

Η αναζήτηση σε τεράστιες συλλογές εγγράφων μπορεί να μοιάζει με το να ψάχνεις για βελόνι σε άχυρο. **Create Boolean Query Java** σας επιτρέπει να πείτε στη μηχανή ακριβώς τι χρειάζεστε — έγγραφα που περιέχουν *και* τους δύο όρους, *οποιονδήποτε* από τους όρους, ή *εξαίρεση* ανεπιθύμητων λέξεων. Σε αυτόν τον οδηγό θα περάσουμε από τη ρύθμιση του **GroupDocs.Search for Java**, την προσθήκη εγγράφων σε ευρετήριο, και τη δημιουργία ισχυρών boolean ερωτημάτων που ενισχύουν τις **document retrieval java** ροές εργασίας σας. Στο τέλος θα μπορείτε να γράψετε καθαρό, συντηρήσιμο κώδικα που δημιουργεί boolean ερωτήματα σε Java με λίγες μόνο γραμμές.

## Γρήγορες Απαντήσεις
- **Τι είναι ένα boolean AND query;** Επιστρέφει μόνο έγγραφα που περιέχουν *όλες* τις καθορισμένες λέξεις-κλειδιά.  
- **Πώς διαφέρει το OR από το AND;** Το OR ταιριάζει με έγγραφα που περιέχουν *οποιαδήποτε* από τις λέξεις-κλειδιά, διευρύνοντας το σύνολο αποτελεσμάτων.  
- **Πότε πρέπει να χρησιμοποιήσω το NOT;** Χρησιμοποιήστε το NOT για να φιλτράρετε έγγραφα που περιέχουν ανεπιθύμητες λέξεις.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμαστική άδεια λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποια έκδοση της Java απαιτείται;** Υποστηρίζεται η Java 8+· συνιστάται η JDK 11+.

## Τι είναι **create boolean query java**;
`create boolean query java` αναφέρεται στην κατασκευή ενός ερωτήματος αναζήτησης σε Java που συνδυάζει λογικούς τελεστές όπως AND, OR και NOT χρησιμοποιώντας το GroupDocs.Search API. Συγκροτώντας αυτούς τους τελεστές μπορείτε να ελέγχετε με ακρίβεια ποια έγγραφα ταιριάζουν, επιτρέποντας προηγμένο φιλτράρισμα, ρύθμιση σχετικότητας και σύνθετα σενάρια αναζήτησης.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
- **High performance** σε μεγάλα σύνολα εγγράφων – μπορεί να ευρετηριάσει και να αναζητήσει 500 GB κειμένου σε λιγότερο από ένα λεπτό σε τυπικό διακομιστή.  
- **Rich API** που υποστηρίζει ερωτήματα κειμένου και αντικειμένου, επιτρέποντάς σας να επιλέξετε το στυλ που ταιριάζει στην αρχιτεκτονική σας.  
- **Built‑in language support** για στέμμινγκ, stop‑words και fuzzy matching σε πάνω από 30 γλώσσες.  
- **Easy integration** με Maven ή άμεση λήψη JAR, απαιτώντας μόνο λίγες γραμμές κώδικα για να ξεκινήσετε.

## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **GroupDocs.Search for Java** (v25.4 ή νεότερη) – δείτε τον σύνδεσμο λήψης παρακάτω.  
- Εγκατεστημένη και ρυθμισμένη JDK 8+ στο IDE σας (IntelliJ IDEA, Eclipse κ.λπ.).  
- Βασικές γνώσεις Java και Maven για διαχείριση εξαρτήσεων.  

## Ρύθμιση του GroupDocs.Search για Java

### Ρύθμιση Maven
Προσθέστε το αποθετήριο και την εξάρτηση στο `pom.xml`:

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
Ξεκινήστε με μια δωρεάν δοκιμαστική άδεια για να εξερευνήσετε όλες τις δυνατότητες. Για παραγωγική χρήση, αγοράστε εμπορική άδεια ώστε να ξεκλειδώσετε πλήρη λειτουργικότητα.

### Βασική Αρχικοποίηση και Ρύθμιση
Δημιουργήστε έναν φάκελο ευρετηρίου και δημιουργήστε το αντικείμενο `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Πώς δημιουργείτε boolean query java;
Η κλάση `Index` αντιπροσωπεύει μια αναζητήσιμη συλλογή εγγράφων αποθηκευμένων στο δίσκο. Ένα `BooleanQuery` συνδυάζει πολλαπλά υπο‑ερωτήματα με λογικούς τελεστές. Οι μέθοδοι `createAndQuery`, `createOrQuery` και `createNotQuery` δημιουργούν υπο‑ερωτήματα AND, OR και NOT αντίστοιχα. Φορτώστε ή δημιουργήστε μια παρουσία `Index`, προσθέστε έγγραφα, στη συνέχεια δημιουργήστε ένα αντικείμενο `BooleanQuery` χρησιμοποιώντας `createAndQuery`, `createOrQuery` ή `createNotQuery`. Καλέστε `index.search(query)` για να ανακτήσετε τα ταιριαστά έγγραφα. Αυτό το πρότυπο λειτουργεί τόσο για απλά όσο και για σύνθετα σενάρια και απαιτεί μόνο τρία λογικά βήματα: αρχικοποίηση ευρετηρίου, προσθήκη εγγράφων και εκτέλεση ερωτήματος.

## Αναζήτηση Boolean AND

### Επισκόπηση
Ένα ερώτημα AND περιορίζει τα αποτελέσματα, βελτιώνοντας τη σχετικότητα όταν χρειάζεστε έγγραφα που ταιριάζουν με πολλαπλά κριτήρια.

### Βήματα Υλοποίησης

1. **Initialize Index** – αυτό επίσης δείχνει **add documents to index** για το σενάριο AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – χρησιμοποιώντας τη σύνταξη απλού κειμένου.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – χρήσιμο όταν δημιουργείτε ερωτήματα προγραμματιστικά (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Αναζήτηση Boolean OR

### Επισκόπηση
Ένα ερώτημα OR είναι ιδανικό για εξερευνητικές αναζητήσεις όπου θέλετε να εντοπίσετε έγγραφα που περιέχουν τουλάχιστον μία από τις λέξεις-κλειδιά (**search with or java**).

### Βήματα Υλοποίησης

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Αναζήτηση Boolean NOT

### Επισκόπηση
Ένα ερώτημα NOT σας βοηθά να εξαλείψετε άσχετα έγγραφα, όπως το φιλτράρισμα του ονόματος ανταγωνιστή (**boolean search examples java**).

### Βήματα Υλοποίησης

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Σύνθετα Boolean Ερωτήματα

### Επισκόπηση
Τα σύνθετα ερωτήματα σας επιτρέπουν να μοντελοποιήσετε πραγματικά σενάρια αναζήτησης, όπως “βρείτε άρθρα αθλητισμού που είναι θετικά αλλά εξαιρέστε οποιαδήποτε αναφορά σε συγκεκριμένους αθλητές”.

### Βήματα Υλοποίησης

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Πρακτικές Εφαρμογές των **java boolean and or** Ερωτημάτων
- **Document Management Systems** – εντοπίστε συμβάσεις που περιέχουν τόσο “confidential” **AND** “renewal”.  
- **Legal Research** – φιλτράρετε νομολογία με **AND**/**OR** ενώ εξαιρείτε παλαιούς νόμους χρησιμοποιώντας **NOT**.  
- **Customer Support** – ανακτήστε αιτήματα που αναφέρουν “login” **AND** “error” αλλά όχι “resolved”.  
- **Content Curation** – συγκεντρώστε αναρτήσεις blog για “cloud” **OR** “serverless” για ένα newsletter.

## Συνηθισμένα Πιθανά Σφάλματα & Επίλυση Προβλημάτων

- **Missing Index Refresh** – μετά την προσθήκη νέων εγγράφων, καλέστε `index.update()` ώστε να γίνουν αναζητήσιμα.  
- **Incorrect Operator Spacing** – το GroupDocs.Search απαιτεί κενά γύρω από τους τελεστές (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – τα ερωτήματα είναι προεπιλογή case‑insensitive, αλλά προσαρμοσμένοι αναλυτές μπορεί να το αλλάξουν.  
- **Large Result Sets** – χρησιμοποιήστε σελιδοποίηση (`search(query, 0, 100)`) για να αποφύγετε υπερφόρτωση μνήμης.  

## Συχνές Ερωτήσεις

**Q: Μπορώ να συνδυάσω περισσότερους από δύο όρους σε ένα ερώτημα AND;**  
A: Απόλυτα. Μπορείτε να συνδέσετε πολλαπλά αντικείμενα `createWordQuery` με `createAndQuery`, ή απλώς να γράψετε `"term1 AND term2 AND term3"` στο ερώτημα κειμένου.

**Q: Υποστηρίζει το GroupDocs.Search wildcard ή fuzzy αναζητήσεις;**  
A: Ναι. Προσθέστε `*` για wildcard (π.χ., `promot*`) ή χρησιμοποιήστε `~` για fuzzy matching (π.χ., `comfort~`).

**Q: Πώς περιορίζω την αναζήτηση σε συγκεκριμένους τύπους αρχείων;**  
`FileTypeQuery` περιορίζει τα αποτελέσματα σε συγκεκριμένες μορφές αρχείων όπως PDF ή DOCX.  
A: Χρησιμοποιήστε την κλάση `FileTypeQuery` για να περιορίσετε τα αποτελέσματα σε PDFs, DOCX κ.λπ., και συνδυάστε το με το boolean ερώτημά σας.

**Q: Ποιος είναι ο καλύτερος τρόπος για να παρακολουθήσω την απόδοση του ευρετηρίου;**  
A: Ενεργοποιήστε τον ενσωματωμένο logger (`index.getLogger().setLevel(Level.INFO)`) και ελέγξτε τις μετρήσεις χρόνου μετά από κάθε λειτουργία `add`.

**Q: Υπάρχει τρόπος να ενισχύσω τη σχετικότητα ορισμένων όρων;**  
`BoostQuery` αυξάνει το σκορ σχετικότητας των καθορισμένων όρων σε ένα ερώτημα αναζήτησης.  
A: Ναι. Τυλίξτε τις σημαντικές λέξεις με `BoostQuery` για να αυξήσετε το βάρος τους στον αλγόριθμο βαθμολόγησης.

---

**Τελευταία ενημέρωση:** 2026-07-21  
**Δοκιμή με:** GroupDocs.Search 25.4 (Java)  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Boolean Operators Java – Create Search Index & Faceted Search](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java&#58; Efficient Document Search and Index Management](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Mastering GroupDocs.Search Java – Create and Manage a Search Index](/search/java/indexing/groupdocs-search-java-create-index-guide/)