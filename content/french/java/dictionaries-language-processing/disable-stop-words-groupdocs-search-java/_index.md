---
date: '2026-07-07'
description: Apprenez comment désactiver stop words java et ajouter des documents
  à l'index en utilisant GroupDocs.Search for Java, améliorant la précision et les
  performances de la recherche.
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: Désactiver stop words java et ajouter des documents à l'index avec
  GroupDocs.Search for Java. Suivez ce guide étape par étape pour améliorer la précision
  des requêtes et les performances.
og_title: Désactiver stop words Java – Ajouter des Docs à l'Index avec GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: Désactiver stop words Java – Ajouter des Docs à l'Index avec GroupDocs
type: docs
url: /fr/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Désactiver les mots vides Java – Ajouter des documents à l'index avec GroupDocs

Dans ce tutoriel, vous découvrirez comment **disable stop words java** tout en ajoutant vos fichiers à un index interrogeable avec GroupDocs.Search for Java. En désactivant le filtre intégré des mots vides, chaque jeton—y compris les mots courants comme « on », « by » ou « the »—devient interrogeable, ce qui améliore considérablement la pertinence des résultats pour des domaines spécialisés tels que les contrats juridiques, les catalogues e‑commerce ou les manuels techniques.

## Réponses rapides
- **Que signifie « add documents to index » ?** Cela signifie charger vos fichiers source dans un index interrogeable afin qu'ils puissent être interrogés efficacement.  
- **Pourquoi désactiver les mots vides ?** Pour inclure les mots courants (p. ex., « on », « the ») dans les recherches lorsque ces termes sont pertinents pour votre domaine.  
- **Quelle version de la bibliothèque est requise ?** GroupDocs.Search for Java 25.4 ou ultérieure.  
- **Ai-je besoin d'une licence ?** Un essai gratuit suffit pour l'évaluation ; une licence permanente est requise pour la production.  
- **Puis-je l'utiliser dans un projet Maven ?** Oui – ajoutez simplement le référentiel et la dépendance indiqués ci-dessous.

## Quels sont les mots vides dans la recherche et pourquoi pourriez‑vous vouloir les désactiver ?
Les mots vides sont des termes à haute fréquence que de nombreux moteurs de recherche filtrent automatiquement pour accélérer le traitement des requêtes. Les désactiver garantit que **every word**—y compris ceux traditionnellement ignorés—contribuent à l'index de recherche, ce qui est essentiel lorsque ces mots portent une signification spécifique au domaine. Par exemple, dans un contrat juridique le mot « by » peut distinguer les parties, et dans un catalogue produit « on » peut faire partie d'un nom de modèle.

## Comment l'ajout de documents à l'index fonctionne‑t‑il dans GroupDocs.Search ?
Lorsque vous ajoutez des documents, GroupDocs.Search lit chaque fichier, le tokenise et stocke les jetons dans un index inversé optimisé. Cette structure permet une récupération en moins d'une seconde même pour des collections contenant **hundreds of thousands of files**. La bibliothèque prend également en charge les mises à jour incrémentielles, vous permettant de garder l'index à jour sans le reconstruire à partir de zéro.

## Prérequis
- **Bibliothèques requises** : GroupDocs.Search for Java 25.4 (or newer).  
- **Environnement de développement** : IntelliJ IDEA, Eclipse ou tout IDE Java de votre choix.  
- **Connaissances de base** : Familiarité avec la syntaxe Java et le concept d'indexation.

## Configuration de GroupDocs pour Java

### Installation Maven
Si vous utilisez Maven, ajoutez ce qui suit dans votre `pom.xml` :

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

### Téléchargement direct
Sinon, téléchargez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Étapes d'obtention de licence
- **Essai gratuit** – commencez les tests immédiatement.  
- **Licence temporaire** – obtenez une clé à durée limitée pour la fonctionnalité complète.  
- **Achat** – obtenez une licence permanente pour l'utilisation en production.

## Initialisation et configuration de base
IndexSettings est une classe de configuration qui définit comment l'index est construit, recherché, et quelles fonctionnalités sont activées.

Créez une instance de `IndexSettings` pour contrôler le comportement de l'index :

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Comment désactiver les mots vides dans la recherche (Java) ?
IndexSettings est l'objet de configuration qui contrôle le comportement de l'index de recherche. Par défaut, il active un filtre de mots vides intégré. Pour désactiver ce filtre, appelez la méthode `setUseStopWords(false)` sur l'instance `IndexSettings`. Cet appel unique désactive la suppression des mots vides, garantissant que chaque jeton—y compris les mots courants tels que « on » ou « the »—est indexé et peut être interrogé.

## Comment ajouter des documents à l'index
L'ajout de documents à l'index se fait en créant un objet `Index` avec les `IndexSettings` souhaités, puis en appelant sa méthode `add` pour chaque fichier ou dossier. La bibliothèque lit chaque document, le tokenise et stocke les termes résultants dans l'index inversé, les rendant immédiatement interrogeables. Vous pouvez diriger l'index vers un répertoire de sortie spécifique et spécifier le dossier source contenant les fichiers à indexer.

### Définition du répertoire de sortie

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### Spécification du répertoire des documents

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## Exécution d'une requête de recherche

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Comme `disable stop words java` est actif, une requête contenant le terme "on" sera évaluée, renvoyant des correspondances qui seraient autrement ignorées par le filtre par défaut.

## Applications pratiques
1. **Enterprise Document Search** – Conservez la terminologie critique qui serait supprimée par les listes de mots vides par défaut.  
2. **E‑commerce Platforms** – Améliorez la découvrabilité des produits en indexant chaque mot dans les descriptions, numéros de modèle et spécifications.  
3. **Legal Research Tools** – Capturez chaque terme juridique, même ceux généralement traités comme mots vides, afin d'éviter de manquer des clauses cruciales.

## Considérations de performance
- **Optimization Tips** : Mettez régulièrement à jour et taillez votre index pour maintenir une vitesse de recherche élevée. GroupDocs.Search peut gérer **up to 1 million documents** tout en conservant des temps de requête inférieurs à une seconde.  
- **Resource Usage** : Surveillez la taille du tas JVM ; les gros index peuvent nécessiter un tas maximal (`-Xmx`) de 4 GB ou plus.  
- **Java Memory Management** : Utilisez des options de stockage hors‑tas pour des corpus très volumineux afin de garder l'empreinte sur le tas en dessous de 2 GB.

## Problèmes courants et solutions

| Symptôme | Cause probable | Solution |
|---|---|---|
| Aucun résultat pour les mots courants | `setUseStopWords(true)` (default) | Appelez `setUseStopWords(false)` comme indiqué ci‑dessus. |
| Erreurs de mémoire insuffisante lors de l'indexation | Indexation de trop nombreux fichiers volumineux en même temps | Indexez les fichiers par lots ; augmentez l'option JVM `-Xmx`. |
| La recherche renvoie des données obsolètes | Index non rafraîchi après l'ajout de nouveaux fichiers | Appelez `index.update()` ou ré‑ajoutez les documents modifiés. |

## Questions fréquentes

**Q : Qu’est‑ce que les mots vides ?**  
R : Les mots vides sont des termes courants (p. ex., « the », « is », « on ») que de nombreux moteurs de recherche ignorent pour accélérer les requêtes. Les désactiver vous permet de traiter chaque jeton comme interrogeable.

**Q : Pourquoi désactiver les mots vides dans les index de recherche ?**  
R : Lorsque la correspondance exacte de phrase est requise—comme dans les documents juridiques ou techniques—chaque mot porte une signification, il faut donc inclure les mots vides.

**Q : Comment GroupDocs.Search gère‑t‑il les grands ensembles de données ?**  
R : La bibliothèque utilise des structures de données optimisées et l'indexation incrémentielle pour maintenir une faible consommation de mémoire, même avec **millions of documents**.

**Q : Puis‑je intégrer GroupDocs.Search à d’autres applications Java ?**  
R : Oui, l’API est conçue pour une intégration facile dans tout système basé sur Java, des services web aux applications de bureau.

**Q : Que faire si mes résultats de recherche ne sont pas précis ?**  
R : Vérifiez que l’index inclut tous les fichiers requis (`add documents to index`), assurez‑vous que le filtrage des mots vides est désactivé lorsque nécessaire, et envisagez de reconstruire l’index après des changements majeurs.

## Ressources supplémentaires
- **Documentation** : [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Référence API** : [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Téléchargement** : [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **Dépôt GitHub** : [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Support gratuit** : [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Licence temporaire** : [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

En suivant ce guide, vous savez maintenant comment **add documents to index** et **disable stop words java** pour fournir des résultats de recherche plus précis dans vos applications Java.

---

**Dernière mise à jour :** 2026-07-07  
**Testé avec :** GroupDocs.Search for Java 25.4  
**Auteur :** GroupDocs  

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## Tutoriels associés

- [Traitement du langage Java – Créer un dictionnaire de synonymes avec GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Comment ajouter des documents à l'index avec l'indexation des métadonnées en Java utilisant GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Comment ajouter des documents à l'index avec GroupDocs.Search pour Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)