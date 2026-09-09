---
date: '2026-08-05'
description: Apprenez à créer un log file extractor pour la full-text search en Java
  avec GroupDocs.Search. Ajoutez des documents à l'index, optimisez les performances
  de recherche et gérez efficacement les large log files.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Le tutoriel Full text search java montre comment créer un log file
  extractor personnalisé avec GroupDocs.Search, ajouter des documents à l'index et
  optimiser les performances de recherche pour d'énormes log archives.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Full text search java : log file extractor avec GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Full text search java : log file extractor avec GroupDocs'
type: docs
url: /fr/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Recherche en texte intégral java : extracteur de fichiers journaux avec GroupDocs

Recherche en texte intégral java est une pierre angulaire pour tout système qui doit localiser rapidement des informations au sein de collections massives de documents. Dans ce tutoriel, vous apprendrez à configurer GroupDocs.Search, créer un extracteur de fichiers journaux personnalisé, ajouter des documents à l'index et optimiser les performances de recherche lorsqu'il s'agit de gigaoctets de données de journaux.

## Ce que vous apprendrez
- Configurer et mettre en place GroupDocs.Search pour Java.  
- Implémenter un **extracteur de fichiers journaux** qui analyse les journaux en texte brut comme vous le souhaitez.  
- **Ajouter des documents à l'index** aux côtés des PDF, DOCX et d'autres formats.  
- Scénarios réels où un **extracteur de fichiers journaux** apporte une valeur mesurable.  
- Conseils éprouvés pour **optimiser les performances de recherche** pour les archives de journaux de plusieurs gigaoctets.

## Réponses rapides
- **Qu'est‑ce qu'un extracteur de fichiers journaux ?** Un composant personnalisé qui indique à GroupDocs.Search comment lire et indexer les fichiers journaux en texte brut.  
- **Pourquoi utiliser GroupDocs.Search ?** Il prend en charge l'indexation de plus de 50 formats, offre la réindexation automatique et gère des index jusqu'à 10 GB avec moins de 2 GB de RAM.  
- **Ai‑je besoin d'une licence ?** Oui – une licence d'essai ou complète est requise pour activer la bibliothèque.  
- **Puis‑je indexer d'autres types de fichiers simultanément ?** Absolument ; mélangez les PDF, DOCX et les fichiers journaux personnalisés dans le même index.  
- **Comment améliorer les performances ?** Utilisez l'indexation incrémentielle, ajustez `IndexSettings`, et activez le drapeau `autoReindex`.

## Prérequis

Avant de commencer, assurez-vous de disposer de ce qui suit :

### Bibliothèques requises
Ajoutez la dépendance Maven GroupDocs.Search à votre `pom.xml`. Utilisez la dernière version correspondant au niveau Java de votre projet.

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

Sinon, téléchargez la dernière version directement depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Configuration de l'environnement
- JDK 8 ou supérieur.  
- Familiarité avec la programmation Java et les concepts de base de la gestion de fichiers.

### Acquisition de licence
Commencez par télécharger une licence d'essai gratuite pour explorer les fonctionnalités de GroupDocs.Search. Pour une utilisation en production, achetez une licence complète ou demandez une licence temporaire via le [site Web de GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Configuration de GroupDocs.Search pour Java

Pour commencer, initialisez la bibliothèque et appliquez votre fichier de licence :

1. **Configuration Maven** – confirmez que la dépendance de l'étape précédente est présente.  
2. **Initialisation de la licence** – chargez le fichier de licence avant tout autre appel d'API.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

Avec l'environnement prêt, vous pouvez passer à la création de l'**extracteur de fichiers journaux** personnalisé.

## Qu'est‑ce qu'un extracteur de fichiers journaux ?

Un extracteur de fichiers journaux est un morceau de code qui indique à GroupDocs.Search comment lire les fichiers journaux bruts (généralement `.log`) et transformer leur contenu en texte interrogeable. En fournissant votre propre extracteur, vous obtenez un contrôle total sur les règles d'analyse, le filtrage du bruit et l'extraction uniquement des informations pertinentes pour votre cas d'utilisation de recherche.

## Créer un extracteur de fichiers journaux

GroupDocs.Search vous permet d'intégrer des extracteurs de texte personnalisés pour tout type de fichier. Suivez ces étapes pour en créer un pour les fichiers journaux.

### Étape 1 : définir l'extracteur personnalisé
`TextExtractorBase` est la classe de base abstraite que vous étendez pour créer un extracteur personnalisé. Elle déclare les extensions de fichiers prises en charge par l'extracteur et contient la logique d'extraction principale.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Points clés**  
- `getFileExtensions()` enregistre l'extracteur pour les fichiers `.log`.  
- `extractText` est l'endroit où vous pouvez supprimer les horodatages, filtrer les lignes de débogage ou appliquer tout prétraitement nécessaire pour **rechercher dans de gros fichiers journaux**.

### Étape 2 : configurer les paramètres d'index avec l'extracteur
Ajoutez votre extracteur aux `IndexSettings` et activez `autoReindex` afin que les nouveaux journaux soient indexés automatiquement sans intervention manuelle.

`IndexSettings` configure le comportement de l'index comme les limites de mémoire et les extracteurs personnalisés.  
`autoReindex` met automatiquement à jour l'index lorsque les fichiers sources changent.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### Étape 3 : ajouter des documents à l'index
Maintenant que l'index reconnaît les fichiers journaux, vous pouvez **ajouter des documents à l'index** comme tout autre format pris en charge.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### Étape 4 : rechercher dans l'index
Effectuez des requêtes en texte brut. L'extracteur personnalisé garantit que chaque entrée de journal est interrogeable.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Conseils pour optimiser les performances de recherche

- **Indexation incrémentielle** – ajoutez uniquement les fichiers journaux nouveaux ou modifiés au lieu de reconstruire l'intégralité de l'index.  
- **Gestion de la mémoire** – le drapeau `autoReindex` maintient une faible utilisation de la RAM en vidant les données intermédiaires sur le disque.  
- **Paramètres d'index** – ajustez `setMaxMemoryUsage` en fonction de la capacité de votre serveur ; un réglage typique est 1 GB pour un index de 10 GB.  
- **Optimisation des requêtes** – utilisez des requêtes de phrase, des caractères génériques ou des filtres pour affiner les résultats lors de la recherche dans d'immenses archives de journaux.

## Applications pratiques

GroupDocs.Search peut être appliqué dans de nombreux scénarios réels, tels que :

- **Gestion des journaux** – localisez les messages d'erreur, les actions des utilisateurs ou des horodatages spécifiques à travers des gigaoctets de données de journal en quelques secondes.  
- **Systèmes de récupération de documents** – maintenez un référentiel unique interrogeable incluant les PDF, documents Word, feuilles de calcul et fichiers journaux personnalisés.  
- **Analyse de contenu** – générez des rapports de fréquence de mots‑clés ou détectez des anomalies dans les données de journaux en flux continu.

## Considérations de performance

Lors du déploiement de GroupDocs.Search à grande échelle, gardez ces meilleures pratiques à l'esprit :

- Stockez les index sur des SSD rapides pour minimiser la latence de lecture/écriture.  
- Surveillez l'utilisation du tas JVM ; envisagez de décharger les gros index vers un processus séparé si la mémoire devient un goulot d'étranglement.  
- Activez `autoReindex` (comme montré) pour garder l'index à jour sans reconstruction manuelle.

## Conclusion

Vous avez maintenant créé un **extracteur de fichiers journaux**, appris comment **ajouter des documents à l'index** et découvert des moyens d'**optimiser les performances de recherche** pour de grandes archives de journaux. Cette combinaison permet à vos applications Java d'offrir une recherche en texte intégral rapide et précise sur tout type de document.

Pour une exploration plus approfondie, consultez la [documentation officielle de GroupDocs](https://docs.groupdocs.com/search/java/) ou expérimentez différentes implémentations d'extracteur pour répondre à votre cas d'utilisation unique.

## Section FAQ
1. **Quels types de fichiers puis‑je indexer avec GroupDocs.Search ?**  
   - Vous pouvez indexer les PDF, les documents Word, les feuilles de calcul et de nombreux autres formats, ainsi que des fichiers journaux personnalisés via des extracteurs de texte.  
2. **Comment gérer efficacement de grandes collections de documents ?**  
   - Utilisez des mises à jour incrémentielles, partitionnez les index et ajustez `IndexSettings` pour gérer les ressources efficacement.  
3. **GroupDocs.Search peut‑il être intégré à d'autres systèmes ?**  
   - Oui, il propose une API Java claire qui peut être intégrée aux services existants, aux micro‑services ou aux applications web.  
4. **Qu'est‑ce qu'une licence temporaire, et comment en obtenir une ?**  
   - Une licence temporaire offre toutes les fonctionnalités pour l'évaluation sans limite de temps. Faites la demande via le [site Web de GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Questions fréquemment posées

**Q : En quoi un extracteur de fichiers journaux diffère‑t‑il de l'extracteur par défaut ?**  
R : L'extracteur par défaut gère les formats courants (PDF, DOCX, etc.). Un extracteur de fichiers journaux personnalisé vous permet de définir exactement comment les entrées de journaux en texte brut sont analysées et indexées.

**Q : Puis‑je indexer des archives de journaux compressées (p. ex., .zip) ?**  
R : Oui, en ajoutant une étape de pré‑traitement qui extrait les fichiers de l'archive avant de les transmettre à l'index.

**Q : Quelle est la meilleure façon de garder l'index à jour avec des journaux générés en continu ?**  
R : Activez `autoReindex` et programmez un observateur en arrière‑plan qui appelle `index.add(newLogFile)` chaque fois qu'un nouveau fichier apparaît.

**Q : Existe‑t‑il une limite à la taille d'un seul fichier journal qui peut être indexé ?**  
R : En pratique, la limite dépend de la mémoire disponible. Il est recommandé de diviser les très gros journaux en morceaux plus petits avant l'indexation.

**Q : GroupDocs.Search prend‑il en charge les recherches floues ou avec caractères génériques ?**  
R : Oui, l'API de recherche inclut la correspondance floue, les caractères génériques et les requêtes de proximité pour améliorer la pertinence des résultats.

---

**Dernière mise à jour :** 2026-08-05  
**Testé avec :** GroupDocs.Search 25.4 pour Java  
**Auteur :** GroupDocs

## Tutoriels associés

- [Recherche en texte intégral Java : créer un index avec GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [Comment ajouter des documents à l'index avec GroupDocs.Search pour Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Améliorer les performances des requêtes avec GroupDocs.Search Java : optimiser l'index et la recherche](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)