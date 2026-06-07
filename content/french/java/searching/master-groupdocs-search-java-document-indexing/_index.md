---
date: '2026-02-08'
description: Apprenez à mettre en surbrillance les résultats de recherche Java et
  à indexer des documents Java à l'aide de GroupDocs.Search for Java avec une indexation
  synchrone et asynchrone.
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: Mise en évidence des résultats de recherche Java – Indexation synchrone et
  asynchrone
type: docs
url: /fr/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

 content.# Mise en évidence des résultats de recherche Java – Indexation synchrone et asynchrone

Boostez vos applications Java en **mise en évidence des résultats de recherche Java** avec la puissante bibliothèque GroupDocs.Search. Que vous manipuliez quelques fichiers ou un référentiel massif, maîtriser à la fois l'indexation synchrone et asynchrone vous permet de fournir des résultats rapides et précis sans bloquer les threads de votre application.

## Réponses rapides
- **Que signifie « mise en évidence des résultats de recherche Java » ?** Il s'agit de rendre les termes correspondants dans les résultats de recherche avec des repères visuels (par ex., les balises HTML `<mark>`) afin que les utilisateurs puissent voir où la requête apparaît dans chaque document.  
- **Quand devrais-je utiliser l'indexation synchrone ?** Pour des ensembles de données petits à moyens où la disponibilité immédiate des documents nouvellement ajoutés est requise.  
- **Quand l'indexation asynchrone est-elle préférable ?** Lors du traitement de grandes collections de documents ou lors de l'exécution sur un thread UI où il faut garder l'application réactive.  
- **Ai-je besoin d'une licence ?** Un essai gratuit suffit pour le développement ; une licence complète débloque les fonctionnalités avancées et supprime les limites d'utilisation.  
- **Quelle version de Java est prise en charge ?** Java 8 ou plus récent.

## Qu'est-ce que la « mise en évidence des résultats de recherche Java » ?
La mise en évidence des résultats de recherche en Java consiste à prendre les correspondances brutes renvoyées par GroupDocs.Search et à entourer les termes correspondants avec du HTML (ou un autre balisage) afin qu'ils se démarquent lorsqu'ils sont affichés dans une interface ou une page web. Cela améliore l'expérience utilisateur en affichant instantanément le contexte de chaque résultat.

## Pourquoi utiliser GroupDocs.Search pour Java ?
GroupDocs.Search fournit un moteur haute performance, indépendant du langage, qui prend en charge :
- Indexation et recherche en temps réel
- Traitement asynchrone pour de lourdes charges de travail
- Mise en évidence des résultats intégrée
- Prise en charge multilingue et d'analyseurs personnalisés  

Ces capacités le rendent idéal pour les systèmes de gestion de contenu, les catalogues e‑commerce et les dépôts de documents d'entreprise.

## Prérequis
Avant de commencer, assurez‑vous d'avoir :

- **Java Development Kit** (JDK 8 ou plus récent) installé.
- Un IDE tel que **IntelliJ IDEA** ou **Eclipse**.
- Un dossier contenant les documents que vous souhaitez indexer.
- Maven pour la gestion des dépendances (ou vous pouvez télécharger le JAR manuellement).

### Bibliothèques et dépendances requises
Ajoutez GroupDocs.Search à votre projet Maven :

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

### Configuration de l'environnement
- Vérifiez que votre **JAVA_HOME** pointe vers un JDK compatible.
- Créez un projet dans votre IDE et ajoutez la configuration Maven ci‑dessus.
- Préparez un répertoire (par ex., `documents/`) contenant des fichiers texte, PDF ou Word d'exemple.

## Comment configurer GroupDocs.Search pour Java
1. **Installer la bibliothèque** – Utilisez le fragment Maven ci‑dessus ou téléchargez le JAR depuis [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Obtenir une licence** – Commencez avec une licence d'essai, puis passez à une licence complète lorsque vous passez en production.  
3. **Initialiser l'index** – Le fragment suivant montre comment créer (ou ouvrir) un dossier d'index :

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Comment mettre en évidence les résultats de recherche Java – Indexation synchrone
L'indexation synchrone traite les documents immédiatement, rendant les fichiers nouvellement ajoutés recherchables dès que possible.

### Étape 1 : Créer l'index et ajouter la gestion des erreurs
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

### Étape 2 : Ajouter des documents et lancer une recherche
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Étape 3 : Traiter les résultats et **mise en évidence des résultats de recherche Java**
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

Le `DocumentHighlighter` entoure automatiquement les termes correspondants avec des balises `<mark>` (ou tout autre format que vous configurez), vous fournissant des **résultats de recherche mis en évidence** prêts à être affichés.

## Comment mettre en évidence les résultats de recherche Java – Indexation asynchrone
Lorsque vous traitez des milliers de fichiers, bloquer le thread principal est indésirable. L'indexation asynchrone permet au moteur de travailler en arrière‑plan.

### Étape 1 : Configurer l'index avec des écouteurs d'événements
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

### Étape 2 : Activer le mode asynchrone et démarrer l'indexation
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

Pendant que l'index est en cours de construction, votre application peut continuer à traiter d'autres requêtes. Une fois que l'événement `StatusChanged` indique `Ready`, vous pouvez lancer des recherches en toute sécurité et obtenir des **résultats de recherche mis en évidence Java**.

## Comment **indexer des documents java** – Conseils pratiques
- **Taille de lot** : pour d'énormes collections, divisez le dossier en lots plus petits afin d'éviter les pics de mémoire.  
- **Filtres de fichiers** : utilisez `IndexingOptions.setFileExtensions` pour n'inclure que les formats nécessaires (par ex., `.pdf`, `.docx`).  
- **Ré‑indexation** : lorsque les documents changent, appelez `index.update(documentPath)` au lieu de reconstruire l'intégralité de l'index.

## Considérations de performance
- **Mémoire** : surveillez l'utilisation du tas ; augmentez `-Xmx` si vous traitez de nombreux fichiers volumineux.  
- **CPU** : l'indexation asynchrone répartit la charge, mais consomme toujours du CPU—surveillez avec JVisualVM.  
- **Mise en évidence des résultats** : la mise en évidence ajoute une petite surcharge de traitement ; mettez en cache le HTML généré si vous devez afficher les résultats de façon répétée.

## Foire aux questions

**Q : Puis‑je combiner l'indexation synchrone et asynchrone dans la même application ?**  
R : Oui. Utilisez l'indexation synchrone pour les petits ensembles fréquemment mis à jour et l'indexation asynchrone pour les importations massives ou les tâches en arrière‑plan.

**Q : Comment personnaliser le style de mise en évidence ?**  
R : Fournissez une implémentation personnalisée de `DocumentHighlighter` qui écrit les balises HTML, CSS ou XML souhaitées autour des termes correspondants.

**Q : Quels types de fichiers GroupDocs.Search prend‑il en charge nativement ?**  
R : Texte, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, et bien d’autres via ses analyseurs intégrés.

**Q : Est‑il possible de rechercher dans plusieurs langues simultanément ?**  
R : Absolument. GroupDocs.Search inclut des analyseurs multilingues ; il suffit de configurer l'`Analyzer` approprié lors de la création de l'index.

**Q : Comment sécuriser le dossier d'index ?**  
R : Stockez l'index dans un répertoire protégé, définissez les permissions système appropriées et envisagez de chiffrer l'index avec les fonctionnalités de sécurité de la bibliothèque.

---

**Dernière mise à jour :** 2026-02-08  
**Testé avec :** GroupDocs.Search 25.4 for Java  
**Auteur :** GroupDocs