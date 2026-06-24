---
date: '2026-05-28'
description: Μάθετε πώς να αναζητήσετε φράση με μοτίβα μπαλαντέρ χρησιμοποιώντας το
  GroupDocs.Search για Java. Περιλαμβάνει τη δημιουργία ευρετηρίου αναζήτησης, την
  προσθήκη εγγράφων και την εκτέλεση ακριβών φράσεων και ερωτημάτων μπαλαντέρ.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Πώς να αναζητήσετε φράση με μπαλαντέρ στο GroupDocs.Search για Java
type: docs
url: /el/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Πώς να αναζητήσετε φράση με μπαλαντέρ στο GroupDocs.Search για Java

Σε σύγχρονες εφαρμογές που επικεντρώνονται στα έγγραφα, η **πώς να αναζητήσετε φράση** γρήγορα και ακριβώς είναι ένας κρίσιμος παράγοντας για την εμπειρία του χρήστη. Είτε δημιουργείτε μια βάση γνώσεων, έναν κατάλογο ηλεκτρονικού εμπορίου ή μια αποθήκη που καθορίζεται από συμμόρφωση, η δυνατότητα εντοπισμού μιας ακριβούς φράσης — ή μιας ευέλικτης παραλλαγής της — διατηρεί τους χρήστες παραγωγικούς και μειώνει το φορτίο υποστήριξης. Αυτό το σεμινάριο σας καθοδηγεί στη εγκατάσταση του **GroupDocs.Search for Java**, στη δημιουργία ευρετηρίου αναζήτησης, στη φόρτωση εγγράφων και στην εκτέλεση τόσο ακριβών φράσεων όσο και ερωτημάτων με μπαλαντέρ, όλα με σαφή, έτοιμο για παραγωγή, αποσπάσματα κώδικα.

## Γρήγορες Απαντήσεις
- **Ποιο είναι το κύριο όφελος των αναζητήσεων φράσεων;** Ακριβής αντιστοίχιση της σειράς των λέξεων και της εγγύτητας, εξασφαλίζοντας ότι επιστρέφονται μόνο έγγραφα που περιέχουν την ακριβή ακολουθία.
- **Μπορούν τα μπαλαντέρ να χρησιμοποιηθούν μέσα σε φράση;** Ναι — τα μπαλαντέρ σας επιτρέπουν να παραλείψετε ή να αντικαταστήσετε λέξεις διατηρώντας τη συνολική σειρά.
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται πλήρης άδεια για παραγωγικές εγκαταστάσεις.
- **Ποια έκδοση του Maven πρέπει να χρησιμοποιήσω;** Η πιο πρόσφατη έκδοση του GroupDocs.Search for Java (π.χ., 25.4 τη στιγμή της συγγραφής).
- **Είναι αυτή η προσέγγιση κατάλληλη για μεγάλα σύνολα εγγράφων;** Απόλυτα — το GroupDocs.Search μπορεί να διαχειριστεί συλλογές εκατοντάδων χιλιάδων εγγράφων με λανθάνοντα χρόνο ερωτημάτων κάτω του δευτερολέπτου όταν το ευρετήριο είναι βελτιστοποιημένο.

## Τι είναι το “πώς να αναζητήσετε φράση”;
**Η αναζήτηση μιας φράσης σημαίνει την αναζήτηση μιας συγκεκριμένης ακολουθίας λέξεων σε ένα έγγραφο.**  
Όταν εκτελείτε ένα ερώτημα φράσης, η μηχανή ελέγχει ότι οι λέξεις εμφανίζονται στην ακριβή σειρά και εντός του ορισμένου εύρους εγγύτητας, εξαλείφοντας άσχετα αποτελέσματα που περιέχουν τις ίδιες λέξεις σε διαφορετικό πλαίσιο. Αυτό καθιστά τις αναζητήσεις φράσεων ιδανικές για τον εντοπισμό νομικών ρήσεων, κωδικών προϊόντων ή οποιουδήποτε κειμένου όπου η σειρά έχει σημασία.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search για ερωτήματα φράσης και μπαλαντέρ;
Το GroupDocs.Search παρέχει **υψηλή απόδοση ευρετηρίου έως 1 εκατομμύριο έγγραφα διατηρώντας χρόνους απόκρισης ερωτημάτων κάτω του δευτερολέπτου** σε τυπικό εξοπλισμό διακομιστή. Η γλώσσα ερωτημάτων του υποστηρίζει ακριβείς φράσεις, απλά μπαλαντέρ `*` και `?`, και προχωρημένα μοτίβα όπως αριθμητικά εύρη (`*2~5`). Η βιβλιοθήκη ενσωματώνεται σε οποιαδήποτε εφαρμογή Java μέσω Maven ή άμεσης λήψης JAR, και λειτουργεί σε Java 8+ χωρίς εξωτερικές υπηρεσίες.

## Προαπαιτούμενα
- Java 8 ή νεότερη (συνιστάται Java 11 LTS).  
- Maven 3 ή νεότερο (αν προτιμάτε διαχείριση εξαρτήσεων).  
- Βασική εξοικείωση με τη δομή έργου Java και τις αντικειμενοστραφείς έννοιες.

## Ρύθμιση του GroupDocs.Search για Java

### Χρήση Maven
Προσθέστε το επίσημο αποθετήριο και την εξάρτηση GroupDocs.Search στο `pom.xml` σας:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Άμεση Λήψη
Εναλλακτικά, κατεβάστε το πιο πρόσφατο JAR από τη σελίδα κυκλοφορίας: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση Άδειας
- **Δωρεάν Δοκιμή:** Ιδανική για γρήγορα πειράματα· περιορισμένη σε 100 MB δεδομένων ευρετηρίου.  
- **Προσωρινή Άδεια:** Ζητήστε κλειδί αξιολόγησης 30 ημερών από το portal του GroupDocs.  
- **Πλήρης Άδεια:** Απαιτείται για παραγωγική χρήση και απεριόριστη χωρητικότητα ευρετηρίου.

## Βασική Αρχικοποίηση και Ρύθμιση
Δημιουργήστε έναν φάκελο που θα κρατά τα αρχεία του ευρετηρίου και δημιουργήστε το αντικείμενο `Index`. Η κλάση `Index` αντιπροσωπεύει το ευρετήσιμο ευρετήριο αποθηκευμένο στο δίσκο και παρέχει μεθόδους για προσθήκη, ενημέρωση και ερώτηση εγγράφων.

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

Προσθέστε τα έγγραφα που θέλετε να είναι αναζητήσιμα:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Πώς να αναζητήσετε φράση με μπαλαντέρ στο GroupDocs.Search
Αυτή η ενότητα παρουσιάζει τρία επίπεδα αναζήτησης φράσεων — ακριβής αντιστοίχιση, απλό μπαλαντέρ και προχωρημένα μοτίβα μπαλαντέρ — δείχνοντας πώς να δημιουργήσετε ένα ευρετήριο, να προσθέσετε έγγραφα και να εκτελέσετε κάθε τύπο ερωτήματος με συνοπτικό κώδικα Java. Τα παραδείγματα απεικονίζουν τόσο ερωτήματα βασισμένα σε κείμενο όσο και κατασκευή ερωτημάτων αντικειμένου, επιτρέποντας στους προγραμματιστές να ενσωματώσουν ευέλικτες δυνατότητες αναζήτησης στις εφαρμογές τους.

### Απλή Αναζήτηση Φράσης

#### Επισκόπηση
Χρησιμοποιήστε αυτήν την προσέγγιση όταν χρειάζεστε μια **ακριβή αντιστοίχιση** μιας ακολουθίας λέξεων, όπως μια νομική ρήση ή έναν αριθμό μοντέλου προϊόντος.

#### Άμεση Απάντηση
Φορτώστε το ευρετήριο, καλέστε `search` με μια φράση σε εισαγωγικά (π.χ., `"quick brown fox"`), και η μηχανή επιστρέφει μόνο έγγραφα που περιέχουν αυτήν την ακριβή ακολουθία, διατηρώντας τη σειρά και τα κενά των λέξεων. Το ερώτημα εκτελείται σε χιλιοστά του δευτερολέπτου, ακόμη και σε ευρετήρια που περιέχουν εκατοντάδες χιλιάδες αρχεία.

#### Βήμα 1: Δημιουργία Ευρετηρίου
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Βήμα 2: Προσθήκη Εγγράφων στο Ευρετήριο
```java
Index index = new Index(indexFolder);
```

#### Βήμα 3: Αναζήτηση Συγκεκριμένης Φράσης (Μορφή Κειμένου)
```java
index.add(documentsFolder);
```

#### Βήμα 4: Ερωτήματα Βασισμένα σε Αντικείμενο (Αναζήτηση Ακριβούς Φράσης)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Αναζήτηση Φράσης με Μπαλαντέρ

#### Επισκόπηση
Οι θέσεις μπαλαντέρ (`*` για οποιονδήποτε αριθμό χαρακτήρων, `?` για έναν χαρακτήρα) σας επιτρέπουν να **παραλείψετε μεταβλητές λέξεις** διατηρώντας παράλληλα τη σειρά των γύρω λέξεων.

#### Άμεση Απάντηση
Εισάγετε ένα σύμβολο μπαλαντέρ (`*`) μέσα σε φράση με εισαγωγικά — π.χ., `"quick * fox"` — για να ταιριάξει οποιαδήποτε λέξη(ες) μεταξύ *quick* και *fox*. Η μηχανή επεκτείνει το μπαλαντέρ κατά το χρόνο ερωτήματος, σαρρώνοντας μόνο τους ευρετηριασμένους όρους που ικανοποιούν το μοτίβο, διατηρώντας την απόδοση συγκρίσιμη με ένα απλό ερώτημα φράσης.

#### Βήμα 1: Δημιουργία Ευρετηρίου
*(Ίδιο με την Απλή Αναζήτηση Φράσης.)*

#### Βήμα 2: Προσθήκη Εγγράφων στο Ευρετήριο
*(Ίδιο με παραπάνω.)*

#### Βήμα 3: Αναζήτηση Μορφής Κειμένου με Μπαλαντέρ
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Βήμα 4: Ερωτήματα Βασισμένα σε Αντικείμενο με Μπαλαντέρ (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Προχωρημένη Αναζήτηση Μπαλαντέρ

#### Επισκόπηση
Συνδυάστε αριθμητικά εύρη, προαιρετικούς χαρακτήρες και προσαρμοσμένα μοτίβα παρόμοια με regex για **προηγμένη αντιστοίχιση**, όπως αριθμούς εκδόσεων ή κωδικούς προϊόντων.

#### Άμεση Απάντηση
Χρησιμοποιήστε την εκτεταμένη σύνταξη μπαλαντέρ `*min~max` για να ορίσετε ένα εύρος επιτρεπόμενων αποστάσεων λέξεων, ή `?` για να ταιριάξετε έναν χαρακτήρα. Για παράδειγμα, `"error *2~5 code"` βρίσκει τη λέξη *error* ακολουθούμενη από οποιεσδήποτε δύο έως πέντε λέξεις και στη συνέχεια *code*. Αυτή η ακρίβεια μειώνει τα ψευδώς θετικά αποτελέσματα ενώ εξακολουθεί να προσφέρει ευελιξία.

#### Βήμα 1: Δημιουργία Ευρετηρίου
*(Επαναλαμβάνεται για σαφήνεια.)*

#### Βήμα 2: Προσθήκη Εγγράφων στο Ευρετήριο
*(Επαναλαμβάνεται.)*

#### Βήμα 3: Αναζήτηση Μορφής Κειμένου με Πολύπλοκα Μοτίβα Μπαλαντέρ
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Βήμα 4: Ερωτήματα Βασισμένα σε Αντικείμενο με Προχωρημένα Μπαλαντέρ
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Πρακτικές Εφαρμογές
- **Συστήματα Διαχείρισης Περιεχομένου:** Οι συντάκτες μπορούν να εντοπίσουν ακριβείς ρήσεις ή ευέλικτα αποσπάσματα χωρίς να σαρώσουν χειροκίνητα εκατοντάδες σελίδες.  
- **Κατάλογοι Ηλεκτρονικού Εμπορίου:** Οι αγοραστές βρίσκουν προϊόντα ακόμη και όταν παραλείπουν έναν περιγραφικό όρο ή χρησιμοποιούν συνώνυμα, χάρη στην ανεκτικότητα των μπαλαντέρ.  
- **Νομικά & Συμμόρφωση:** Γρήγορη απομόνωση γλωσσικού περιεχομένου συμβάσεων που μπορεί να εμφανίζεται με μικρές παραλλαγές σε διάφορες συμφωνίες.

## Σκέψεις για την Απόδοση
- **Δημιουργία Ευρετηρίου Αναζήτησης** μόνο μία φορά ανά σταθερό σύνολο εγγράφων· επαναχρησιμοποιήστε την ίδια παρουσία `Index` για όλα τα ερωτήματα.  
- **Προσθήκη Εγγράφων Σταδιακά** όταν φτάνουν νέα αρχεία — αποφύγετε την επαναδημιουργία ολόκληρου του ευρετηρίου για να διατηρήσετε τη χρήση CPU χαμηλή.  
- **Σχεδίαση Ακριβών Μοτίβων Μπαλαντέρ**· ευρύτερα μοτίβα (`*`) αυξάνουν τον αριθμό επεκτάσεων όρων και μπορούν να αυξήσουν το φορτίο CPU.  
- **Κλήση `index.optimize()`** περιοδικά (αν υποστηρίζεται) για συμπίεση του ευρετηρίου και διατήρηση της κατανάλωσης μνήμης υπό έλεγχο.

## Συχνά Προβλήματα & Λύσεις

| Πρόβλημα | Λύση |
|----------|------|
| Δεν επιστρέφονται αποτελέσματα για ερώτημα μπαλαντέρ | Επαληθεύστε τη σύνταξη μπαλαντέρ (`*min~max`) και βεβαιωθείτε ότι οι λέξεις-στόχοι υπάρχουν εντός του ορισμένου εύρους. |
| Το ευρετήριο γίνεται παρωχημένο μετά από ενημερώσεις αρχείων | Χρησιμοποιήστε `index.add(updatedFolder)` ή το API σταδιακής ενημέρωσης για να ανανεώσετε μόνο τα αλλαγμένα αρχεία. |
| Υψηλή κατανάλωση μνήμης σε μεγάλα σύνολα δεδομένων | Αυξήστε το heap της JVM (`-Xmx4g` ή περισσότερο) και εξετάστε το διαχωρισμό του ευρετηρίου σε πολλαπλές θραύσεις για παράλληλη επεξεργασία. |

## Συχνές Ερωτήσεις

**Ε: Ποια είναι η διαφορά μεταξύ μπαλαντέρ και αναζήτησης φράσης;**  
Α: Η αναζήτηση φράσης απαιτεί την ακριβή σειρά και τα κενά των λέξεων, ενώ το μπαλαντέρ σας επιτρέπει να αντικαταστήσετε ή να παραλείψετε λέξεις εντός αυτής της σειράς, προσφέροντας ευέλικτη αντιστοίχιση.

**Ε: Μπορώ να χρησιμοποιήσω μπαλαντέρ με αριθμητικά δεδομένα στις αναζητήσεις;**  
Α: Ναι — οι παράμετροι εύρους μπαλαντέρ (`*min~max`) λειτουργούν και με αριθμούς καθώς και με λέξεις, επιτρέποντας ερωτήματα όπως `"version *1~3"`.

**Ε: Πώς πρέπει να διαχειριστώ πολύ μεγάλες συλλογές εγγράφων;**  
Α: Διατηρήστε το ευρετήριο βελτιστοποιημένο, εκτελέστε σταδιακές ενημερώσεις και δημιουργήστε συγκεκριμένα μοτίβα μπαλαντέρ για περιορισμό της επέκτασης όρων. Το GroupDocs.Search μπορεί να ευρετηριάσει 1 εκατομμύριο έγγραφα διατηρώντας τη λανθάνουσα απόκριση ερωτήσεων κάτω των 200 ms σε τυπικό υλικό.

**Ε: Είναι το GroupDocs.Search κατάλληλο για σενάρια αναζήτησης σε πραγματικό χρόνο;**  
Α: Απόλυτα — μόλις δημιουργηθεί το ευρετήριο, τα ερωτήματα εκτελούνται σε χιλιοστά του δευτερολέπτου, καθιστώντας το ιδανικό για διαδραστικά πλαίσια αναζήτησης και λειτουργίες αυτόματης συμπλήρωσης.

**Ε: Μπορώ να ενσωματώσω αυτή τη βιβλιοθήκη σε υπάρχον έργο Java;**  
Α: Ναι. Προσθέστε την εξάρτηση Maven ή το JAR, δημιουργήστε το `Index` όπως φαίνεται, και είστε έτοιμοι να κάνετε ερωτήματα χωρίς να τροποποιήσετε τον υπάρχοντα κώδικα.

---

**Τελευταία Ενημέρωση:** 2026-05-28  
**Δοκιμάστηκε Με:** GroupDocs.Search 25.4 for Java  
**Συγγραφέας:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Σχετικά Μαθήματα

- [Δημιουργία Ευρετηρίου Αναζήτησης Java – GroupDocs.Search Tutorials](/search/java/)
- [Προσθήκη Εγγράφων στο Ευρετήριο – GroupDocs.Search Java Tutorials](/search/java/document-management/)
- [Δημιουργία Ευρετηρίου Αναζήτησης - GroupDocs.Search Java Tutorials](/search/java/advanced-features/)