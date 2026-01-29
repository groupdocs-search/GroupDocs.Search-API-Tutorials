---
date: '2026-01-29'
description: Μάθετε πώς να υλοποιείτε λογικές ερωτήσεις AND/OR σε Java χρησιμοποιώντας
  το GroupDocs.Search για Java, προσθέστε έγγραφα στο ευρετήριο και βελτιώστε την
  ανάκτηση εγγράφων.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: Κατακτήστε τις Boolean Αναζητήσεις με το GroupDocs.Search
  για Java'
type: docs
url: /el/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Αποκτήστε τον έλεγχο των Boolean Αναζητήσεων με το GroupDocs.Search για Java

Η αναζήτηση σε τεράστιες συλλογές εγγράφων μπορεί να μοιάζει με το να ψάχνεις για μια βελόνα σε άχυρο. Με ερωτήματα **java boolean and or** μπορείτε να πείτε στη μηχανή ακριβώς τι χρειάζεστε — έγγραφα που περιέχουν *και* τους δύο όρους, *οποιονδήποτε* από αυτούς, ή *να εξαιρέσετε* ανεπιθύμητες λέξεις. Σε αυτόν τον οδηγό θα περάσουμε από τη ρύθμιση του **GroupDocs.Search for Java**, την προσθήκη εγγράφων σε ευρετήριο και τη δημιουργία ισχυρών boolean ερωτημάτων που ενισχύουν τις **document retrieval java** ροές εργασίας σας.

## Γρήγορες Απαντήσεις
- **Τι είναι ένα boolean AND ερώτημα;** Επιστρέφει μόνο τα έγγραφα που περιέχουν *όλες* τις καθορισμένες λέξεις.  
- **Πώς διαφέρει το OR από το AND;** Το OR ταιριάζει με έγγραφα που περιέχουν *οποιαδήποτε* από τις λέξεις, διευρύνοντας το σύνολο αποτελεσμάτων.  
- **Πότε πρέπει να χρησιμοποιήσω το NOT;** Χρησιμοποιήστε το NOT για να φιλτράρετε έγγραφα που περιέχουν ανεπιθύμητες λέξεις.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποια έκδοση της Java απαιτείται;** Υποστηρίζεται η Java 8+· συνιστάται JDK 11+.

## Τι είναι το **java boolean and or**;
Ένα ερώτημα **java boolean and or** συνδυάζει λογικούς τελεστές (AND, OR, NOT) για να βελτιώσει τα αποτελέσματα αναζήτησης. Με τη δομή των ερωτημάτων λέτε στο GroupDocs.Search ακριβώς πώς σχετίζονται οι όροι μεταξύ τους, προσφέροντας ακριβή έλεγχο της διαδικασίας ανάκτησης.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για Java;
- **Υψηλή απόδοση** σε μεγάλα σύνολα εγγράφων.  
- **Πλούσιο API** που υποστηρίζει τόσο ερωτήματα κειμένου όσο και αντικειμενοστραφή ερωτήματα.  
- **Ενσωματωμένη υποστήριξη γλώσσας** για stemming, stop‑words και fuzzy matching.  
- **Εύκολη ενσωμάτωση** με Maven ή άμεση λήψη JAR.

## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **GroupDocs.Search for Java** (v25.4 ή νεότερη) – δείτε τον σύνδεσμο λήψης παρακάτω.  
- Εγκατεστημένο και ρυθμισμένο JDK 8+ στο IDE σας (IntelliJ IDEA, Eclipse κ.λπ.).  
- Βασικές γνώσεις Java και Maven για διαχείριση εξαρτήσεων.  

## Ρύθμιση του GroupDocs.Search για Java

### Maven Setup
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

### Άμεση Λήψη
Εναλλακτικά, κατεβάστε το πιο πρόσφατο JAR από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας
Ξεκινήστε με δωρεάν δοκιμαστική άδεια για να εξερευνήσετε όλες τις δυνατότητες. Για παραγωγική χρήση, αγοράστε εμπορική άδεια ώστε να ξεκλειδώσετε πλήρη λειτουργικότητα.

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

## java boolean and or: Υλοποίηση Boolean Αναζητήσεων

Παρακάτω καλύπτουμε **AND**, **OR**, **NOT** και **complex** ερωτήματα. Κάθε ενότητα δείχνει τόσο ερώτημα κειμένου όσο και το ισοδύναμο αντικειμενοστραφές ερώτημα, ώστε να διαλέξετε το στυλ που ταιριάζει στον κώδικά σας.

### Boolean AND Search
Συνδυάστε όρους με **AND** για να ανακτήσετε μόνο τα έγγραφα που περιέχουν *όλες* τις λέξεις‑κλειδιά.

#### Overview
Ένα ερώτημα AND περιορίζει τα αποτελέσματα, βελτιώνοντας τη συνάφεια όταν χρειάζεστε έγγραφα που ταιριάζουν με πολλαπλά κριτήρια.

#### Implementation Steps

1. **Initialize Index** – δείχνει επίσης πώς να **add documents to index** για το σενάριο AND.

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

### Boolean OR Search
Χρησιμοποιήστε **OR** για να διευρύνετε τα αποτελέσματα, ταιριάζοντας με οποιονδήποτε από τους παρεχόμενους όρους.

#### Overview
Ένα ερώτημα OR είναι ιδανικό για εξερευνητικές αναζητήσεις όπου θέλετε να συλλάβετε έγγραφα που περιέχουν τουλάχιστον μία από τις πολλές λέξεις‑κλειδιά (**search with or java**).

#### Implementation Steps

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

### Boolean NOT Search
Εξαιρέστε ανεπιθύμητους όρους με **NOT** για να φιλτράρετε το «θόρυβο» από τα αποτελέσματά σας.

#### Overview
Ένα ερώτημα NOT σας βοηθά να αφαιρέσετε άσχετα έγγραφα, όπως το φιλτράρισμα του ονόματος ενός ανταγωνιστή (**boolean search examples java**).

#### Implementation Steps

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

### Complex Boolean Queries
Συνδυάστε **AND**, **OR**, και **NOT** για να δημιουργήσετε πολύπλοκη λογική αναζήτησης με εξαιρετικά συγκεκριμένες ανάγκες ανάκτησης.

#### Overview
Τα σύνθετα ερωτήματα σας επιτρέπουν να μοντελοποιήσετε πραγματικά σενάρια αναζήτησης, όπως «βρείτε άρθρα αθλητισμού που είναι θετικά αλλά εξαιρέστε οποιαδήποτε αναφορά σε συγκεκριμένους αθλητές».

#### Implementation Steps

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

## Πρακτικές Εφαρμογές των java boolean and or Ερωτημάτων
- **Συστήματα Διαχείρισης Εγγράφων** – εντοπίστε συμβάσεις που περιέχουν τόσο το “confidential” **AND** “renewal”.  
- **Νομική Έρευνα** – φιλτράρετε νομολογίες με **AND**/ **OR** ενώ εξαιρείτε παλαιές διατάξεις χρησιμοποιώντας **NOT**.  
- **Υποστήριξη Πελατών** – ανακτήστε αιτήματα που αναφέρουν “login” **AND** “error” αλλά όχι “resolved”.  
- **Κατηγοριοποίηση Περιεχομένου** – συγκεντρώστε blog posts για “cloud” **OR** “serverless” για ένα newsletter.

## Συχνά Λάθη & Επίλυση Προβλημάτων
- **Missing Index Refresh** – μετά την προσθήκη νέων εγγράφων, καλέστε `index.update()` ώστε να γίνουν αναζητήσιμα.  
- **Incorrect Operator Spacing** – το GroupDocs.Search απαιτεί κενά γύρω από τους τελεστές (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – τα ερωτήματα είναι προεπιλογή case‑insensitive, αλλά προσαρμοσμένοι αναλυτές μπορεί να το αλλάξουν.  
- **Large Result Sets** – χρησιμοποιήστε σελιδοποίηση (`search(query, 0, 100)`) για να αποφύγετε υπερφόρτωση μνήμης.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να συνδυάσω περισσότερους από δύο όρους σε ένα ερώτημα AND;**  
Α: Φυσικά. Μπορείτε να αλυσίδετε πολλαπλά αντικείμενα `createWordQuery` με `createAndQuery`, ή απλώς να γράψετε `"term1 AND term2 AND term3"` στο ερώτημα κειμένου.

**Ε: Υποστηρίζει το GroupDocs.Search wildcard ή fuzzy αναζητήσεις;**  
Α: Ναι. Προσθέστε `*` για wildcard (π.χ., `promot*`) ή `~` για fuzzy matching (π.χ., `comfort~`).

**Ε: Πώς περιορίζω την αναζήτηση σε συγκεκριμένους τύπους αρχείων;**  
Α: Χρησιμοποιήστε την κλάση `FileTypeQuery` για να περιορίσετε τα αποτελέσματα σε PDF, DOCX κ.λπ., και συνδυάστε την με το boolean ερώτημά σας.

**Ε: Ποιος είναι ο καλύτερος τρόπος για να παρακολουθώ την απόδοση του ευρετηρίου;**  
Α: Ενεργοποιήστε τον ενσωματωμένο logger (`index.getLogger().setLevel(Level.INFO)`) και ελέγξτε τα μετρικά χρόνου μετά από κάθε λειτουργία `add`.

**Ε: Υπάρχει τρόπος να ενισχύσω τη συνάφεια ορισμένων όρων;**  
Α: Ναι. Τυλίξτε τις σημαντικές λέξεις με `BoostQuery` για να αυξήσετε το βάρος τους στον αλγόριθμο βαθμολόγησης.

---

**Τελευταία ενημέρωση:** 2026-01-29  
**Δοκιμή με:** GroupDocs.Search 25.4 (Java)  
**Συγγραφέας:** GroupDocs