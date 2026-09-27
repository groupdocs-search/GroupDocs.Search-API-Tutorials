---
date: '2026-09-27'
description: Μάθετε πώς να υλοποιήσετε java full text search χρησιμοποιώντας το GroupDocs.Search
  for Java, προσθέστε files στην αναζήτηση, διαμορφώστε directories, και ενεργοποιήστε
  real time indexing.
keywords:
- java full text search
- event driven indexing
- java search engine
- add files to search
- real time indexing java
lastmod: '2026-09-27'
og_description: Υλοποιήστε java full text search χρησιμοποιώντας το GroupDocs.Search.
  Μάθετε πώς να προσθέσετε files, διαμορφώστε nodes, και ενεργοποιήστε real time indexing
  σε λίγα λεπτά.
og_image_alt: Guide to setting up java full text search with GroupDocs.Search
og_title: Πώς να υλοποιήσετε java full text search με το GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to implement java full text search using GroupDocs.Search
    for Java, add files to search, configure directories, and enable real time indexing.
  headline: How to implement java full text search with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: Yes. The library works with any Java runtime, and you can point `basePath`
      to a network‑mounted folder or a cloud storage mount.
    question: Can I use GroupDocs.Search on a cloud‑based Java application?
  - answer: Subscribe to node events (see Feature 3) and call `addFiles` or `addDirectories`
      again for the modified paths.
    question: How do I update the index when a file changes?
  - answer: Practically, the limit is defined by your hardware and network bandwidth.
      The API imposes no hard cap.
    question: Is there a limit to the number of nodes I can deploy?
  - answer: No. Adding files triggers indexing automatically; you only need to commit
      if you defer the operation.
    question: Do I need to restart nodes after adding new files?
  - answer: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, and many image types—over
      50 formats in total.
    question: Which document formats are supported out of the box?
  type: FAQPage
tags:
- java full text search
- GroupDocs.Search
- search indexing
title: Πώς να υλοποιήσετε java full text search με το GroupDocs.Search
type: docs
url: /el/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να υλοποιήσετε αναζήτηση πλήρους κειμένου java με το GroupDocs.Search

Στην εποχή των εφαρμογών που βασίζονται στα δεδομένα, η **java full text search** είναι απαραίτητη για τη μετατροπή τεράστιων συλλογών εγγράφων σε άμεσα αναζητήσιμες βάσεις γνώσης. Είτε δημιουργείτε μια επιχειρησιακή πύλη είτε μια ελαφριά επιτραπέζια εφαρμογή, ένα καλά διαμορφωμένο δίκτυο αναζήτησης μπορεί να μειώσει την καθυστέρηση των ερωτημάτων από δευτερόλεπτα σε χιλιοστά του δευτερολέπτου και να διατηρεί τα αποτελέσματα σχετικές καθώς τα δεδομένα αυξάνονται. Αυτό το σεμινάριο σας καθοδηγεί στη διανομή του **GroupDocs.Search for Java**, στην προσθήκη αρχείων στην αναζήτηση, στη διαμόρφωση καταλόγων στους κόμβους και στην ενεργοποίηση της ευρετηρίασης σε πραγματικό χρόνο ώστε το ευρετήριο σας να παραμένει ενημερωμένο χωρίς χειροκίνητη παρέμβαση.

> **Γιατί είναι σημαντικό:** Ένα ευρετήριο java full text search μειώνει την καθυστέρηση των ερωτημάτων, κλιμακώνεται με τον όγκο των δεδομένων και προσφέρει ισχυρές δυνατότητες πλήρους κειμένου σε οποιαδήποτε λύση βασισμένη σε Java — web portals, desktop apps, ή cloud microservices.

## Γρήγορες απαντήσεις
- **Ποιος είναι ο κύριος σκοπός του GroupDocs.Search;** Παρέχει μια κλιμακώσιμη, java μηχανή αναζήτησης που ευρετηριάζει και αναζητά έγγραφα σε ένα κατανεμημένο δίκτυο.  
- **Ποια έκδοση πρέπει να χρησιμοποιήσω;** Η πιο πρόσφατη σταθερή έκδοση (π.χ., 25.4) συνιστάται για νέα έργα.  
- **Χρειάζομαι άδεια;** Διατίθεται δωρεάν δοκιμή 30 ημερών· απαιτείται μόνιμη άδεια για παραγωγική χρήση.  
- **Μπορώ να προσθέσω τόσο αρχεία όσο και ολόκληρους καταλόγους;** Ναι – χρησιμοποιήστε τις βοηθητικές συναρτήσεις `addFiles` και `addDirectories` για την εισαγωγή περιεχομένου.  
- **Ποια έκδοση της Java απαιτείται;** Java 8 ή νεότερη, με Maven για τη διαχείριση εξαρτήσεων.  
- **Πώς λειτουργεί η ευρετηρίαση σε πραγματικό χρόνο java;** Με την εγγραφή σε γεγονότα κόμβου μπορείτε να ενεργοποιήσετε αυτόματη επανευρετηρίαση όταν αλλάζουν τα αρχεία.

## Τι είναι το “create searchable index java”;
Η δημιουργία ενός ευρετηρίου αναζήτησης σε Java σημαίνει την κατασκευή μιας δομής δεδομένων που αντιστοιχίζει όρους στα έγγραφα που τα περιέχουν, επιτρέποντας γρήγορα ερωτήματα πλήρους κειμένου. Το **GroupDocs.Search for Java** αφαιρεί το βάρος της εργασίας, επιτρέποντάς σας να εστιάσετε στην παροχή εγγράφων και στη βελτιστοποίηση της συμπεριφοράς αναζήτησης.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Search for Java;
Το GroupDocs.Search παρέχει μια java μηχανή αναζήτησης που κλιμακώνεται οριζόντια, υποστηρίζει πάνω από 50 μορφές εισόδου και εξόδου, και προσφέρει ευρετηρίαση βασισμένη σε γεγονότα. Η ανάπτυξη πολλαπλών κόμβων διανέμει το φορτίο ευρετηρίασης, ενώ οι ενσωματωμένοι έλεγχοι υγείας διατηρούν το δίκτυο αξιόπιστο. Παρέχει επίσης RESTful APIs και προσαρμόσιμους αναλυτές για λεπτομερή βελτιστοποίηση της συνάφειας.

## Προαπαιτούμενα
- **JDK 8+** εγκατεστημένο στο μηχάνημά σας για ανάπτυξη.  
- Ένα IDE όπως το **IntelliJ IDEA** ή το **Eclipse**.  
- Βασικές γνώσεις **Java** και **Maven**.  
- Πρόσβαση στη βιβλιοθήκη **GroupDocs.Search for Java** (λήψη ή Maven).

## Ρύθμιση του GroupDocs.Search for Java

### Εξάρτηση Maven
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

> **Συμβουλή:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο ελέγχοντας τη σελίδα επίσημων εκδόσεων.

Μπορείτε επίσης να κατεβάσετε το JAR απευθείας από την επίσημη ιστοσελίδα: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Απόκτηση άδειας
- **Δωρεάν δοκιμή:** αξιολόγηση 30 ημερών.  
- **Προσωρινή άδεια:** Αίτηση για εκτεταμένη δοκιμή.  
- **Αγορά:** Απαιτείται για παραγωγικές εγκαταστάσεις.

### Βασική αρχικοποίηση
Δημιουργήστε ένα αντικείμενο διαμόρφωσης που δείχνει σε έναν φάκελο όπου θα αποθηκευτούν τα αρχεία ευρετηρίου και ορίζει τη βασική θύρα επικοινωνίας:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## Πώς να δημιουργήσετε searchable index java με το GroupDocs.Search;
Φορτώστε ένα αντικείμενο `SearchConfiguration`, ξεκινήστε ένα `SearchNetworkNode` και καλέστε `node.getIndexer().addFiles(...)` για να γεμίσετε το ευρετήριο. Αυτό το μοτίβο μίας γραμμής εκκινεί ένα πλήρως λειτουργικό δίκτυο java full text search, έτοιμο να δέχεται ερωτήματα αμέσως. Στη συνέχεια μπορείτε να κλιμακώσετε προσθέτοντας περισσότερους κόμβους που μοιράζονται την ίδια βασική διαδρομή και εύρος θυρών.

### Χαρακτηριστικό 1 – διαμόρφωση και ρύθμιση δικτύου
Η κλάση `SearchConfiguration` περιέχει όλες τις ρυθμίσεις που απαιτούνται για την εκκίνηση ενός κόμβου.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – Κατάλογος όπου θα αποθηκευτούν τα δεδομένα του ευρετηρίου.  
- **`basePort`** – Αρχική θύρα· κάθε κόμβος θα αυξάνει από αυτή την τιμή.

### Χαρακτηριστικό 2 – ανάπτυξη κόμβων δικτύου αναζήτησης
`SearchNetworkNode` αντιπροσωπεύει μια μεμονωμένη υπηρεσία ευρετηρίασης που μπορεί να εκτελείται σε οποιοδήποτε μηχάνημα.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

`SearchNetworkNode` είναι το κύριο στοιχείο χρόνου εκτέλεσης που φιλοξενεί ένα ευρετήριο, επεξεργάζεται γεγονότα προσθήκης/αφαίρεσης και ανταποκρίνεται σε ερωτήματα αναζήτησης. Η ανάπτυξη πολλαπλών κόμβων σας επιτρέπει να **create java full text search** συστοιχίες που κλιμακώνονται οριζόντια.

### Χαρακτηριστικό 3 – εγγραφή σε γεγονότα κόμβου
Οι ενημερώσεις σε πραγματικό χρόνο διατηρούν το ευρετήριο συγχρονισμένο με τις αλλαγές του συστήματος αρχείων.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Ακούγοντας τα γεγονότα, μπορείτε αυτόματα να ενεργοποιήσετε επανευρετηρίαση όταν φτάνουν νέα αρχεία, επιτυγχάνοντας **event driven indexing** χωρίς χειροκίνητα σενάρια.

### Χαρακτηριστικό 4 – προσθήκη καταλόγων στον κόμβο δικτύου
Χρησιμοποιήστε αυτή τη βοηθητική συνάρτηση για **add directories to node**, συλλέγοντας αναδρομικά όλα τα υποστηριζόμενα έγγραφα.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### Χαρακτηριστικό 5 – προσθήκη αρχείων στον κόμβο δικτύου
Όταν χρειάζεστε λεπτομερή έλεγχο, **add files to search** μεμονωμένα:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Συνηθισμένες περιπτώσεις χρήσης
- **Επιχειρηματικές πύλες εγγράφων** που χρειάζονται άμεση αναζήτηση σε χιλιάδες PDF και αρχεία Office.  
- **Πλατφόρμες νομικής e‑discovery** όπου νέες αποδείξεις προστίθενται συνεχώς και πρέπει να είναι αναζητήσιμες σε πραγματικό χρόνο.  
- **Συστήματα διαχείρισης περιεχομένου** που αποθηκεύουν εικόνες, παρουσιάσεις και λογιστικά φύλλα και απαιτούν αναζήτηση πλήρους κειμένου.

## Συνηθισμένα προβλήματα & λύσεις
| Πρόβλημα | Αιτία | Διόρθωση |
|-------|--------|-----|
| **Δεν εμφανίζονται έγγραφα στα αποτελέσματα αναζήτησης** | Το ευρετήριο δεν έχει δεσμευτεί | Κλήση `node.getIndexer().commit()` μετά την προσθήκη αρχείων. |
| **Σφάλμα σύγκρουσης θύρας** | Μια άλλη υπηρεσία χρησιμοποιεί το `basePort` | Επιλέξτε διαφορετικό `basePort` ή ελέγξτε τις ελεύθερες θύρες. |
| **Μη υποστηριζόμενη μορφή αρχείου** | Η βιβλιοθήκη δεν διαθέτει αναλυτή | Βεβαιωθείτε ότι η επέκταση αρχείου υποστηρίζεται ή προσθέστε έναν προσαρμοσμένο εξαγωγέα. |

## Συμβουλές αντιμετώπισης προβλημάτων
- **Επαλήθευση υγείας κόμβου:** Χρησιμοποιήστε το ενσωματωμένο endpoint ελέγχου υγείας (`http://localhost:{port}/health`) για να επιβεβαιώσετε ότι κάθε κόμβος λειτουργεί.  
- **Παρακολούθηση χρήσης μνήμης:** Μεγάλες παρτίδες εγγράφων μπορούν να αυξήσουν τη μνήμη· ευρετηριάζετε σε μικρότερα τμήματα και καλείτε `commit()` περιοδικά.  
- **Έλεγχος αρχείων καταγραφής:** Το GroupDocs.Search γράφει λεπτομερή logs στον φάκελο `basePath`—ανασκοπήστε τα για σφάλματα ανάλυσης ή χρονικά όρια δικτύου.

## Συχνές ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω το GroupDocs.Search σε μια εφαρμογή Java βασισμένη στο cloud;**  
Α: Ναι. Η βιβλιοθήκη λειτουργεί με οποιοδήποτε runtime Java, και μπορείτε να ορίσετε το `basePath` σε φάκελο δικτυακής προσάρτησης ή σε αποθήκευση cloud.

**Ε: Πώς ενημερώνω το ευρετήριο όταν αλλάζει ένα αρχείο;**  
Α: Εγγραφείτε σε γεγονότα κόμβου (δείτε το Χαρακτηριστικό 3) και καλέστε ξανά `addFiles` ή `addDirectories` για τις τροποποιημένες διαδρομές.

**Ε: Υπάρχει όριο στον αριθμό των κόμβων που μπορώ να αναπτύξω;**  
Α: Στην πράξη, το όριο καθορίζεται από το υλικό και το εύρος ζώνης του δικτύου σας. Το API δεν επιβάλλει σκληρό όριο.

**Ε: Πρέπει να επανεκκινήσω τους κόμβους μετά την προσθήκη νέων αρχείων;**  
Α: Όχι. Η προσθήκη αρχείων ενεργοποιεί αυτόματα την ευρετηρίαση· χρειάζεται μόνο να κάνετε commit αν καθυστερείτε τη λειτουργία.

**Ε: Ποιες μορφές εγγράφων υποστηρίζονται έτοιμες για χρήση;**  
Α: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, και πολλοί τύποι εικόνων—πάνω από 50 μορφές συνολικά.

**Ε: Πώς μπορώ να ενεργοποιήσω την ευρετηρίαση σε πραγματικό χρόνο java για έναν φάκελο που λαμβάνει συνεχώς μεταφορτώσεις;**  
Α: Υλοποιήστε έναν παρατηρητή συστήματος αρχείων (π.χ., `java.nio.file.WatchService`) που καλεί `DirectoryAdder.addDirectories(node, path)` κάθε φορά που εντοπίζεται νέο αρχείο.

---

**Τελευταία ενημέρωση:** 2026-09-27  
**Δοκιμάστηκε με:** GroupDocs.Search for Java 25.4  
**Συγγραφέας:** GroupDocs

## Σχετικά Σεμινάρια

- [Πώς να υλοποιήσετε java full text search: δημιουργία καταλόγου ευρετηρίου με το GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Υλοποίηση Full Text Search Java Groupdocs Search](/search/java/searching/implement-full-text-search-java-groupdocs-search/)
- [Πώς να διαμορφώσετε την Αναζήτηση με το GroupDocs.Search σε Java - Οδηγός Διαμόρφωσης & Ανάπτυξης](/search/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}