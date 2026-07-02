---
date: '2026-07-02'
description: Μάθετε πώς να αποκτήσετε μια προσωρινή άδεια για το GroupDocs.Search,
  να προσθέσετε καταλόγους στο ευρετήριο και να προσθέσετε προσαρμοσμένα χαρακτηριστικά
  εγγράφων ενώ διαχειρίζεστε τους κόμβους δικτύου αναζήτησης Java.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Απόκτηση προσωρινής άδειας GroupDocs – Master Search Nodes (Java)
type: docs
url: /el/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Απόκτηση Προσωρινής Άδειας GroupDocs – Κόμβοι Κύριου Αναζήτησης (Java)

Σε αυτόν τον ολοκληρωμένο οδηγό θα **αποκτήσετε μια προσωρινή άδεια για το GroupDocs.Search**, θα διαμορφώσετε ένα δίκτυο αναζήτησης πολλαπλών κόμβων και θα μάθετε πώς να **προσθέτετε καταλόγους προς ευρετηρίαση** και **προσθέτετε προσαρμοσμένα χαρακτηριστικά εγγράφων** χρησιμοποιώντας Java. Είτε δημιουργείτε ένα εταιρικό σύστημα διαχείρισης εγγράφων είτε έναν αναζητήσιμο κατάλογο προϊόντων, η κατανόηση αυτών των βημάτων σας επιτρέπει να αξιολογήσετε την πλατφόρμα χωρίς περιορισμούς και να κλιμακώσετε τις δυνατότητες αναζήτησης γρήγορα.

## Γρήγορες Απαντήσεις
- **Ποιο είναι το πρώτο βήμα για να ξεκινήσετε τη χρήση του GroupDocs.Search;** Αποκτήστε μια προσωρινή άδεια από το portal του GroupDocs.  
- **Ποιο αποθετήριο Maven φιλοξενεί τη βιβλιοθήκη;** `https://releases.groupdocs.com/search/java/`.  
- **Πώς προσθέτω καταλόγους προς ευρετηρίαση;** Καλέστε τη βοηθητική μέθοδο `addDirectoriesToIndex` στον κύριο κόμβο.  
- **Μπορώ να προσθέσω προσαρμοσμένα χαρακτηριστικά εγγράφου;** Ναι—καλέστε το `addAttribute` με το κλειδί του εγγράφου και το όνομα του χαρακτηριστικού.  
- **Πώς κλείνω τους κόμβους καθαρά;** Καλέστε το `closeNodes` για να απελευθερώσετε πόρους.

## Τι είναι μια προσωρινή άδεια και γιατί τη χρειάζομαι;
Μια προσωρινή άδεια σας επιτρέπει να αξιολογήσετε το GroupDocs.Search χωρίς περιορισμούς αξιολόγησης. Είναι ιδανική για ανάπτυξη, δοκιμές ή έργα proof‑of‑concept πριν από την πλήρη αγορά. Η άδεια παρέχει πλήρη πρόσβαση σε όλες τις λειτουργίες για περιορισμένο χρονικό διάστημα, επιτρέποντάς σας να μετρήσετε την απόδοση, να δοκιμάσετε σημεία ενσωμάτωσης και να διασφαλίσετε ότι η λύση καλύπτει τις απαιτήσεις σας χωρίς οικονομική δέσμευση.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

### Απαιτούμενες Βιβλιοθήκες και Εξαρτήσεις
Για να εργαστείτε με το GroupDocs.Search για Java, συμπεριλάβετε τις απαραίτητες εξαρτήσεις Maven:
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
Μπορείτε επίσης να κατεβάσετε την πιο πρόσφατη έκδοση απευθείας από [GroupDocs.Search για Java εκδόσεις](https://releases.groupdocs.com/search/java/).

### Ρύθμιση Περιβάλλοντος
- Βεβαιωθείτε ότι έχετε εγκατεστημένο ένα συμβατό JDK (Java 8 ή νεότερο).  
- Ρυθμίστε το IDE σας ώστε να υποστηρίζει έργα Maven.

### Προαπαιτούμενες Γνώσεις
Μια βασική κατανόηση του προγραμματισμού Java και εξοικείωση με τη διαχείριση έργων Maven θα είναι χρήσιμη. Εάν είστε νέοι σε αυτές τις έννοιες, εξετάστε πόρους εισαγωγικού επιπέδου για να ξεκινήσετε.

## Πώς να αποκτήσετε μια προσωρινή άδεια
Μια προσωρινή άδεια αποκτάται επισκεπτόμενοι το portal του GroupDocs, συμπληρώνοντας μια σύντομη φόρμα αίτησης και τοποθετώντας το ληφθέν αρχείο `.lic` στον φάκελο `resources` του έργου σας. Στη συνέχεια, αρχικοποιήστε την άδεια με μερικές γραμμές κώδικα (δείτε το απόσπασμα παρακάτω). Για τη φόρμα αίτησης, χρησιμοποιήστε τη σελίδα: [Προσωρινή Άδεια GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Ρύθμιση GroupDocs.Search για Java

### Πληροφορίες Εγκατάστασης
Για να αρχίσετε να χρησιμοποιείτε το GroupDocs.Search για Java στο έργο σας, ακολουθήστε τα βήματα Maven παραπάνω ή κατεβάστε την πιο πρόσφατη έκδοση απευθείας από τη σελίδα των επίσημων εκδόσεων.

#### Βήματα Απόκτησης Άδειας
1. **Δωρεάν Δοκιμή** – Εξερευνήστε τις δυνατότητες χωρίς καμία δέσμευση.  
2. **Προσωρινή Άδεια** – Αποκτήστε ένα βραχυπρόθεσμο κλειδί για δοκιμές (δείτε την ενότητα παραπάνω).  
3. **Αγορά** – Για παραγωγική χρήση, αγοράστε μια πλήρη άδεια από τη **[Σελίδα Αγοράς GroupDocs](https://purchase.groupdocs.com/)**.

### Βασική Αρχικοποίηση και Ρύθμιση
Αρχικοποιήστε το έργο σας με το GroupDocs.Search ως εξής:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Αυτό το βήμα αρχικοποίησης είναι κρίσιμο για να διασφαλιστεί ότι όλα τα συστατικά λειτουργούν αδιάλειπτα μέσα στο δίκτυο αναζήτησης.

## Οδηγός Υλοποίησης
Τώρα, ας διασπάσουμε τη διαδικασία σε διαχειρίσιμες ενότητες, η καθεμία εστιάζει σε μια συγκεκριμένη λειτουργία της ανάπτυξης και διαχείρισης κόμβων δικτύου αναζήτησης.

### Χαρακτηριστικό 1: Ρύθμιση Διαμόρφωσης
**Επισκόπηση:** Η ρύθμιση της διαμόρφωσης για το δίκτυο αναζήτησής σας είναι το πρώτο βήμα στην ανάπτυξη κόμβων. Αυτή η ρύθμιση περιλαμβάνει τον καθορισμό διαδρομών και θυρών που είναι κρίσιμες για την ανάπτυξη των κόμβων.

#### Βήματα Υλοποίησης:
##### Βήμα 1: Ορισμός Βασικής Διαδρομής και Θύρας
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Βήμα 2: Διαμόρφωση Δικτύου Αναζήτησης
Η συνάρτηση `configureSearchNetwork` προετοιμάζει το αντικείμενο διαμόρφωσης που απαιτείται για την ανάπτυξη κόμβων.  
Η `Configuration` είναι μια κλάση που περιέχει όλες τις ρυθμίσεις όπως φάκελο ευρετηρίου, θύρες δικτύου και ρόλους κόμβων.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Παράμετροι:** Η βασική διαδρομή και η θύρα χρησιμοποιούνται για τον εντοπισμό πόρων και τη δημιουργία καναλιών επικοινωνίας.  
- **Τιμή Επιστροφής:** Ένα διαμορφωμένο αντικείμενο `Configuration` προσαρμοσμένο στις ανάγκες της ανάπτυξής σας.

### Χαρακτηριστικό 2: Ανάπτυξη Δικτύου Αναζήτησης
**Επισκόπηση:** Η ανάπτυξη κόμβων είναι απαραίτητη για την κλιμάκωση των δυνατοτήτων αναζήτησης σας σε διαφορετικά περιβάλλοντα ή τμήματα δεδομένων.

#### Βήματα Υλοποίησης:
##### Βήμα 1: Ανάπτυξη Κόμβων
Η συνάρτηση `deploySearchNetwork` αρχικοποιεί και επιστρέφει έναν πίνακα κόμβων δικτύου αναζήτησης.  
Το `SearchNetworkNodes` αντιπροσωπεύει κάθε παρουσία κόμβου που συμμετέχει στο κατανεμημένο σύμπλεγμα αναζήτησης.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Παράμετροι:** Η βασική διαδρομή, η θύρα και η διαμόρφωση χρησιμοποιούνται για τον καθορισμό του περιβάλλοντος ανάπτυξης.  
- **Τιμή Επιστροφής:** Ένας πίνακας που περιέχει αρχικοποιημένα `SearchNetworkNodes`.

### Χαρακτηριστικό 3: Εγγραφή σε Συμβάντα Δικτύου
**Επισκόπηση:** Η παρακολούθηση των δραστηριοτήτων του δικτύου αναζήτησής σας είναι κρίσιμη για τη διατήρηση βέλτιστης απόδοσης και αξιοπιστίας.

#### Βήματα Υλοποίησης:
##### Βήμα 1: Εγγραφή σε Συμβάντα Κύριου Κόμβου
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Σκοπός:** Αυτό το βήμα εξασφαλίζει ότι θα ειδοποιηθείτε για σημαντικά συμβάντα ή αλλαγές εντός του δικτύου αναζήτησης.

### Χαρακτηριστικό 4: Ευρετηρίαση Εγγράφων
**Επισκόπηση:** Η προσθήκη καταλόγων που περιέχουν έγγραφα προς ευρετηρίαση επιτρέπει αποδοτική ανάκτηση δεδομένων σε όλο το δίκτυό σας.

#### Πώς να προσθέσετε καταλόγους προς ευρετηρίαση
Η `addDirectoriesToIndex` είναι μια βοηθητική μέθοδος που καταχωρεί διαδρομές φακέλων για ευρετηρίαση στον κύριο κόμβο.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Σκοπός:** Διευκολύνει την γρήγορη πρόσβαση και αναζητησιμότητα όλων των εγγράφων εντός των καθορισμένων καταλόγων.

### Χαρακτηριστικό 5: Προσθήκη Χαρακτηριστικών σε Έγγραφα
**Επισκόπηση:** Τα προσαρμοσμένα χαρακτηριστικά ενισχύουν τα μεταδεδομένα των εγγράφων, καθιστώντας τις αναζητήσεις πιο ευέλικτες και ενημερωτικές.

#### Πώς να προσθέσετε προσαρμοσμένα χαρακτηριστικά εγγράφου
Η `addAttribute` προσθέτει ένα προσαρμοσμένο χαρακτηριστικό μεταδεδομένων σε ένα συγκεκριμένο έγγραφο στο ευρετήριο.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Παράμετροι:** Καθορίστε τον κόμβο, το κλειδί του εγγράφου και το χαρακτηριστικό που θα προστεθεί.  
- **Σκοπός:** Επεκτείνει τη λειτουργικότητα αναζήτησης εμπλουτίζοντας τα έγγραφα με πρόσθετα μεταδεδομένα.

### Χαρακτηριστικό 6: Ανάκτηση Ευρετηριασμένων Εγγράφων
**Επισκόπηση:** Η αποδοτική ανάκτηση και λίστα των ευρετηριασμένων εγγράφων διασφαλίζει την ακρίβεια και πληρότητα των δεδομένων.

#### Βήματα Υλοποίησης:
##### Βήμα 1: Λήψη Ευρετηριασμένων Εγγράφων
```java
getIndexedDocuments(nodes[0]);
```  
- **Σκοπός:** Επαληθεύει την επιτυχή ευρετηρίαση όλων των απαραίτητων εγγράφων εντός του δικτύου αναζήτησης.

### Χαρακτηριστικό 7: Κλείσιμο Κόμβων Δικτύου
**Επισκόπηση:** Το σωστό κλείσιμο των κόμβων είναι κρίσιμο για τη διαχείριση πόρων και την αποφυγή διαρροών μνήμης.

#### Βήματα Υλοποίησης:
##### Βήμα 1: Κλείσιμο Όλων των Κόμβων
Η `closeNodes` κλείνει όλους τους ενεργούς κόμβους αναζήτησης και απελευθερώνει τους κατανεμημένους πόρους.  
```java
closeNodes(nodes);
```  
- **Σκοπός:** Απελευθερώνει τους πόρους που κατέχει κάθε κόμβος, εξασφαλίζοντας μια καθαρή διαδικασία τερματισμού.

## Γιατί να χρησιμοποιήσετε μια προσωρινή άδεια για το GroupDocs.Search;
Μια προσωρινή άδεια παρέχει **πλήρη πρόσβαση σε όλες τις λειτουργίες για 30 ημέρες** και υποστηρίζει έως **50.000 ευρετηριασμένα έγγραφα** χωρίς περιορισμό απόδοσης. Αυτό σας επιτρέπει να μετρήσετε την ταχύτητα ευρετηρίασης, τη λανθάνουσα απόκριση ερωτημάτων και την κλιμακωσιμότητα σε πραγματικά δεδομένα πριν αγοράσετε μια παραγωγική άδεια. Επιπλέον, αφαιρεί τα υδατογραφήματα αξιολόγησης, προσφέροντάς σας μια ακριβή εικόνα των τελικών δυνατοτήτων του προϊόντος.

## Συνηθισμένες Περιπτώσεις Χρήσης
1. **Διαχείριση Εγγράφων Επιχειρήσεων** – Ευρετηρίαση εκατομμυρίων εσωτερικών αρχείων σε όλα τα τμήματα, επιτρέποντας άμεση πλήρη κειμενική αναζήτηση.  
2. **Πλατφόρμες Ηλεκτρονικού Εμπορίου** – Δημιουργία ενός αναζητήσιμου καταλόγου προϊόντων που καλύπτει πολλαπλές αποθήκες και τροφοδοσίες τρίτων.  
3. **Νομικά Γραφεία** – Οργάνωση φακέλων υποθέσεων, συμβάσεων και αποδεικτικών στοιχείων με προσαρμοσμένα μεταδεδομένα για γρήγορη ανάκτηση.

Οι δυνατότητες ενσωμάτωσης με άλλα συστήματα περιλαμβάνουν πλατφόρμες CRM, συστήματα διαχείρισης περιεχομένου (CMS) και εργαλεία ανάλυσης δεδομένων, αξιοποιώντας τις ισχυρές δυνατότητες ευρετηρίασης και αναζήτησης που προσφέρει το GroupDocs.Search για Java.

## Σκέψεις Απόδοσης
Για βελτιστοποίηση της απόδοσης κατά τη χρήση του GroupDocs.Search για Java:
- **Βελτιστοποίηση Διαμόρφωσης** – Προσαρμόστε τις ρυθμίσεις διαμόρφωσης ώστε να ταιριάζουν στο συγκεκριμένο περιβάλλον ανάπτυξής σας.  
- **Παρακολούθηση Χρήσης Πόρων** – Ελέγχετε τακτικά CPU, μνήμη και I/O για να αποτρέψετε σημεία συμφόρησης ή διαρροές μνήμης.  
- **Τήρηση Καλών Πρακτικών** – Ακολουθήστε τις οδηγίες διαχείρισης μνήμης της Java, διασφαλίζοντας αποδοτική αξιοποίηση των πόρων του συστήματος.

## Συχνές Ερωτήσεις

**Ε: Πόσο διαρκεί μια προσωρινή άδεια;**  
Α: Οι προσωρινές άδειες ισχύουν συνήθως για 30 ημέρες, παρέχοντάς σας επαρκή χρόνο για αξιολόγηση του προϊόντος.

**Ε: Μπορώ να μεταβώ από προσωρινή σε πλήρη άδεια χωρίς επανεγκατάσταση;**  
Α: Ναι—απλώς αντικαταστήστε το αρχείο προσωρινής άδειας με το αρχείο πλήρους άδειας και επανεκκινήστε την εφαρμογή σας.

**Ε: Χρειάζεται να επανευρετηριάσω τα έγγραφα μετά την εφαρμογή νέας άδειας;**  
Α: Όχι, το ευρετήριο παραμένει αμετάβλητο· η άδεια επηρεάζει μόνο τα δικαιώματα χρήσης.

**Ε: Τι συμβαίνει αν ξεχάσω να κλείσω τους κόμβους;**  
Α: Οι μη απελευθερωμένοι πόροι μπορεί να προκαλέσουν διαρροές μνήμης· πάντα καλέστε το `closeNodes` κατά το τερματισμό.

**Ε: Είναι δυνατόν να προσθέσω περισσότερα από ένα προσαρμοσμένα χαρακτηριστικά ανά έγγραφο;**  
Α: Απόλυτα—καλέστε το `addAttribute` πολλές φορές με διαφορετικά ονόματα χαρακτηριστικών.

**Last Updated:** 2026-07-02  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs

## Σχετικά Μαθήματα

- [Ανάπτυξη Κόμβου Δικτύου Αναζήτησης σε .NET χρησιμοποιώντας το GroupDocs για Αποτελεσματική Ευρετηρίαση και Ανάκτηση Εγγράφων](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Πώς να Υλοποιήσετε ένα Δίκτυο Αναζήτησης με το GroupDocs.Search σε .NET για Συστήματα Διαχείρισης Εγγράφων](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Διαμόρφωση Aspose.Search Network & Προσθήκη Χαρακτηριστικών Εγγράφων με το GroupDocs.Redaction για .NET: Ένας Πλήρης Οδηγός](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)