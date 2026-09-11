---
date: '2026-09-11'
description: Apprenez à mettre en évidence les résultats de recherche Java et à indexer
  des documents Java en utilisant GroupDocs.Search for Java avec une indexation synchronous
  et asynchronous.
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: Mettez en évidence les résultats de recherche Java avec GroupDocs.Search.
  Apprenez l'indexation synchronous et asynchronous, les mises à jour en temps réel,
  et la mise en évidence des résultats dans les applications Java.
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: Mettre en évidence les résultats de recherche Java – Indexation rapide synchronous
  & async
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: Mettre en évidence les résultats de recherche Java – Indexation synchronous
  & async
type: docs
url: /fr/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Mettre en évidence les résultats de recherche Java – Indexation synchrone et asynchrone

Dans ce guide, vous découvrirez comment **highlight search results Java** en utilisant la bibliothèque GroupDocs.Search, et vous verrez étape par étape comment indexer des documents Java à la fois de manière synchrone et asynchrone. Que vous construisiez un petit outil de bureau ou un service de recherche d'entreprise à grande échelle, ces techniques vous permettent de fournir des correspondances instantanées et visuellement claires sans bloquer les threads de votre application.

## Réponses rapides
- **Que signifie “highlight search results Java” ?** Cela signifie entourer chaque terme correspondant dans les extraits retournés avec un balisage (par ex., `<mark>`) afin que les utilisateurs puissent voir instantanément le contexte du résultat.  
- **Quand devrais‑je utiliser l'indexation synchrone ?** Utilisez‑la pour des collections petites à moyennes où vous avez besoin que le document soit searchable dès qu'il est ajouté.  
- **Quand l'indexation asynchrone est‑elle préférable ?** Choisissez‑la pour de gros lots ou lorsque le thread UI doit rester réactif pendant que l'index se construit en arrière‑plan.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour le développement ; une licence complète supprime les limites et débloque les fonctionnalités avancées.  
- **Quelle version de Java est prise en charge ?** Java 8 ou ultérieure.

## Qu’est‑ce que “highlight search results Java” ?
`highlight search results java` est le processus consistant à prendre les données brutes de correspondance de GroupDocs.Search et à insérer des repères visuels—généralement des balises HTML `<mark>`—autour de chaque terme trouvé. Cela rend les extraits de résultats immédiatement lisibles dans une page Web ou un composant Swing, améliorant l'expérience utilisateur en montrant exactement où apparaît la requête.

## Pourquoi utiliser GroupDocs.Search pour Java ?
GroupDocs.Search fournit un moteur haute performance, indépendant du langage, capable de **traiter jusqu'à 5 000 documents par seconde**, **supporter plus de 30 formats de fichiers**, et **indexer des collections de 10 millions de documents** sans charger l'ensemble du corpus en mémoire. Son surlignage intégré, son indexation en temps réel et ses analyseurs multilingues le rendent idéal pour les systèmes de gestion de contenu, les catalogues e‑commerce et les dépôts de documents d'entreprise.

## Prérequis
- **Java Development Kit** (JDK 8 ou plus récent) installé et `JAVA_HOME` correctement défini.  
- Un IDE tel que **IntelliJ IDEA** ou **Eclipse**.  
- Un dossier (par ex., `documents/`) contenant les fichiers que vous souhaitez indexer—texte brut, PDF, DOCX, etc.  
- Maven pour la gestion des dépendances (ou vous pouvez ajouter le JAR manuellement).

### Bibliothèques et dépendances requises
Ajoutez GroupDocs.Search à votre `pom.xml` Maven :

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

Pour les téléchargements directs, obtenez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Configuration de l’environnement
- Vérifiez que `JAVA_HOME` pointe vers un JDK compatible.  
- Créez un nouveau projet Maven et collez le fragment ci‑dessus dans la section `<dependencies>`.  
- Placez des fichiers d'exemple dans un répertoire tel que `src/main/resources/documents/`.

## Comment configurer GroupDocs.Search pour Java
`Index` est la classe principale représentant une collection searchable stockée sur disque.

Créez une instance `Index` pointant vers un dossier sur le disque, appliquez une licence si vous en avez une, et configurez éventuellement un analyseur pour la tokenisation spécifique à une langue. Cette étape de préparation garantit que le moteur peut lire, écrire et rechercher dans l'index de manière efficace.

La classe `Index` est le composant central qui représente une collection searchable sur disque. Après l'avoir instanciée, toutes les opérations d'indexation et de requête passent par cet objet.

1. **Installer la bibliothèque** – Utilisez le fragment Maven ci‑dessus ou téléchargez le JAR depuis [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Obtenir une licence** – Commencez avec une licence d'essai ; remplacez‑la par une clé de production avant le déploiement.  
3. **Initialiser l'index** – Le fragment suivant montre comment créer (ou ouvrir) un dossier d'index :

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Comment mettre en évidence les résultats de recherche Java – indexation synchrone
`DocumentHighlighter` est une classe utilitaire qui génère des extraits surlignés à partir des résultats de recherche.

Chargez l'index, ajoutez des documents avec `index.add(documentPath)`, exécutez une requête, puis appelez `DocumentHighlighter` pour entourer les correspondances de balises `<mark>`. Le processus complet s'exécute sur le thread appelant, de sorte que le document devienne searchable immédiatement après le retour de `add` pour les utilisateurs finaux.

### Étape 1 : créer l'index et ajouter la gestion des erreurs
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Étape 2 : ajouter des documents et exécuter une recherche
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Étape 3 : traiter les résultats et mettre en évidence les résultats de recherche Java
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## Comment mettre en évidence les résultats de recherche Java – indexation asynchrone
`IndexingOptions` configure la façon dont le processus d'indexation s'exécute, y compris le mode synchrone ou asynchrone.

Configurez `IndexingOptions` pour fonctionner en mode arrière‑plan, abonnez‑vous aux événements `StatusChanged`, et laissez le moteur indexer les fichiers pendant que votre UI continue de répondre à d'autres requêtes. Une fois le statut passé à `Ready`, vous pouvez exécuter des recherches et obtenir des extraits surlignés comme en mode synchrone.

`AsyncIndexingListener` reçoit les mises à jour de progression, vous permettant d'afficher une barre de progression ou de consigner le statut sans bloquer le thread principal.

### Étape 1 : configurer l'index avec les écouteurs d'événements
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Étape 2 : activer le mode asynchrone et démarrer l'indexation
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## Comment indexer des documents Java – conseils pratiques
`index.update(path)` met à jour un document existant dans l'index avec le fichier au chemin spécifié.

Divisez les grandes collections en lots de 1 000 à 5 000 fichiers, filtrez par extension pour éviter les analyses inutiles, et utilisez `index.update(path)` pour les fichiers modifiés au lieu de reconstruire l'intégralité de l'index. Ces pratiques maintiennent une faible consommation de mémoire et un temps d'indexation prévisible afin de garantir la cohérence.

- **Taille du lot** : Pour les très grandes collections, divisez le dossier en lots plus petits afin d'éviter les pics de mémoire.  
- **Filtres de fichiers** : Utilisez `IndexingOptions.setFileExtensions` pour n'inclure que les formats dont vous avez besoin (par ex., `.pdf`, `.docx`).  
- **Ré‑indexation** : Lorsqu'un document change, appelez `index.update(documentPath)` plutôt que de recréer l'index à partir de zéro.

## Considérations de performance
- **Mémoire** : Surveillez l'utilisation du tas ; augmentez `-Xmx` si vous traitez de nombreux fichiers volumineux simultanément.  
- **CPU** : L'indexation asynchrone répartit la charge de travail sur plusieurs threads mais consomme toujours du CPU—suivez l'utilisation avec JVisualVM.  
- **Surlignage des résultats** : Le surlignage ajoute une surcharge modeste (≈ 2–5 ms par résultat). Mettez en cache le HTML généré si vous devez afficher les mêmes extraits à plusieurs reprises.

## Questions fréquentes
**Q : Puis‑je combiner l'indexation synchrone et asynchrone dans la même application ?**  
R : Oui. Utilisez l'indexation synchrone pour des ensembles petits et fréquemment mis à jour et l'indexation asynchrone pour les importations massives ou les tâches en arrière‑plan.

**Q : Comment personnaliser le style de surlignage ?**  
R : Fournissez une implémentation personnalisée de `DocumentHighlighter` qui écrit le HTML, CSS ou XML souhaité autour des termes correspondants.

**Q : Quels types de fichiers GroupDocs.Search prend‑il en charge nativement ?**  
R : Texte, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, et bien d’autres via les analyseurs intégrés—plus de 30 formats au total.

**Q : Est‑il possible de rechercher dans plusieurs langues simultanément ?**  
R : Absolument. GroupDocs.Search inclut des analyseurs multilingues ; il suffit de configurer le `Analyzer` approprié lors de la création de l'index.

**Q : Comment sécuriser le dossier d'index ?**  
R : Stockez l'index dans un répertoire protégé, définissez des permissions strictes sur le système de fichiers, et chiffrez éventuellement l'index en utilisant les fonctionnalités de sécurité de la bibliothèque.

---

**Dernière mise à jour :** 2026-09-11  
**Testé avec :** GroupDocs.Search 25.4 for Java  
**Auteur :** GroupDocs

## Tutoriels associés

- [Comment créer un index de documents et ajouter des documents en utilisant l'API GroupDocs.Search pour Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Comment créer un référentiel d'index Java avec GroupDocs.Search : indexation et recherche de documents efficaces](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [Recherche d'indexation de documents efficace Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)