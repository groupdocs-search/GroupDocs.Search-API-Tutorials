---
date: '2026-08-15'
description: Apprenez comment améliorer la latence de recherche en utilisant les fonctionnalités
  d'indexation avancée de GroupDocs.Search pour Java, y compris cancellation, async
  operations, multithreading et metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Améliorez la latence de recherche avec GroupDocs.Search pour Java
  en utilisant cancellation, asynchronous indexing, multithreading et metadata customization.
  Boost performance and reduce resource use.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Améliorer la latence de recherche avec l'indexation avancée dans GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Améliorer la latence de recherche avec l'indexation avancée dans GroupDocs
type: docs
url: /fr/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Améliorer la latence de recherche avec l'indexation avancée dans GroupDocs

Dans l'environnement numérique actuel au rythme rapide, **améliorer la latence de recherche** est essentiel pour fournir des résultats instantanés aux utilisateurs. Que vous construisiez un moteur de recherche personnalisé ou que vous amélioriez un système de gestion de documents existant, la bonne stratégie d'indexation peut réduire considérablement la latence, diminuer la consommation de ressources, et **améliorer la latence de recherche** dans l'ensemble. Dans ce tutoriel, nous passerons en revue les fonctionnalités les plus puissantes de GroupDocs.Search pour Java — l'annulation, l'indexation asynchrone, le multithreading et la personnalisation des métadonnées — afin que vous puissiez **ajouter des documents à l'index** plus rapidement et plus efficacement.

**Ce que vous apprendrez**

- Comment annuler une opération d'indexation après un temps spécifié  
- Effectuer des opérations d'indexation asynchrones et gérer les changements d'état  
- Configurer le multithreading pour une indexation plus rapide  
- Personnaliser les options d'indexation des métadonnées pour **personnaliser les métadonnées de recherche**  

Assurons-nous que vous avez tout ce dont vous avez besoin avant de plonger dans le code.

## Réponses rapides
- **Que fait l'annulation ?** Elle arrête l'indexation après un délai défini, libérant le CPU et la mémoire pour d'autres tâches.  
- **Puis-je indexer des documents de façon asynchrone ?** Oui – activez-le avec `options.setAsync(true)`.  
- **Combien de threads puis-je utiliser ?** Tout entier positif ; 2‑4 threads sont typiques pour la plupart des serveurs.  
- **L'indexation des métadonnées est‑elle optionnelle ?** Absolument – vous pouvez l'activer ou l'ajuster finement par champ.  
- **Ai‑je besoin d'une licence pour ces fonctionnalités ?** Un essai fonctionne pour les tests ; une licence complète est requise en production.

## Prérequis

- **Bibliothèque GroupDocs.Search** – version 25.4 ou ultérieure.  
- **Environnement de développement Java** – JDK 8 ou supérieur est recommandé.  
- Familiarité de base avec Java et le concept d'indexation.

### Configuration de GroupDocs.Search pour Java

#### Installation Maven

Ajoutez le dépôt et la dépendance à votre fichier `pom.xml` :

`pom.xml` configuration indique à Maven quels artefacts GroupDocs.Search télécharger et inclure dans votre projet.

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

#### Téléchargement direct

Alternativement, téléchargez le dernier JAR depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Acquisition de licence** – Commencez avec un essai gratuit ou demandez une licence temporaire pour débloquer l'ensemble complet des fonctionnalités.

### Initialisation et configuration de base

La classe `SearchIndex` est le point d'entrée qui représente un index interrogeable stocké sur disque ou en mémoire.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Qu’est‑ce que « optimiser les performances de recherche » dans ce contexte ?

Optimiser les performances de recherche signifie configurer le processus d'indexation afin qu'il consomme la bonne quantité de CPU, de mémoire et de temps tout en livrant instantanément les résultats les plus pertinents. En contrôlant l'annulation, l'exécution asynchrone, le multithreading et la gestion des métadonnées, vous influencez directement la rapidité avec laquelle le moteur peut **ajouter des documents à l'index** et répondre aux requêtes.

## Pourquoi utiliser les fonctionnalités d'indexation avancées ?

L'indexation asynchrone et multithreadée maintient votre application réactive, tandis que l'annulation empêche les processus incontrôlés. Des options de métadonnées finement réglées vous permettent de mettre en avant les informations les plus importantes, ce qui **améliore la latence de recherche** pour les utilisateurs finaux. De plus, ces fonctionnalités réduisent les pics de CPU, diminuent la pression sur la mémoire et permettent une mise à l'échelle plus fluide lors du traitement de gros volumes de documents.

## Comment améliorer la latence de recherche avec l'indexation avancée ?

Chargez votre instance `SearchIndex`, configurez `IndexingOptions` avec les paramètres d'annulation, d'asynchrone et de threads, puis appelez `index.add(document)` — cette combinaison réduit le temps d'indexation global jusqu'à 60 % sur des charges de travail typiques et garantit que les tâches de longue durée ne bloqueront pas d'autres opérations. Vous pouvez également ajuster les limites d'indexation des métadonnées et surveiller la progression via les événements de changement d'état afin de vous assurer que le pipeline reste dans les budgets de performance.

## Guide d'implémentation

### Propriété d'annulation

**Vue d'ensemble** – Annuler l'indexation après une durée spécifiée pour éviter une surconsommation des ressources.

#### Étape 1 : configurer l'environnement

Créez une instance `SearchIndex` pointant vers votre dossier d'index.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : créer les options d'indexation avec annulation

`IndexingOptions` vous permet de spécifier le comportement du moteur d'indexation.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Points clés**

- `setCancellation()` active la fonctionnalité.  
- `cancelAfter(int milliseconds)` définit le délai d'expiration (3 secondes dans cet exemple).

### Propriété asynchrone

**Vue d'ensemble** – Exécuter l'indexation sur un thread en arrière-plan et écouter les changements d'état.

#### Étape 1 : configurer l'environnement

Instanciez l'index et préparez la collection de documents.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : s'abonner à l'événement de changement d'état

L'événement `StatusChanged` vous notifie lorsque le travail d'indexation passe d'un état à un autre.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Étape 3 : configurer les options asynchrones

Activez le mode asynchrone afin que l'appel retourne immédiatement et que le traitement continue en arrière-plan.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Propriété des threads

**Vue d'ensemble** – Accélérer l'indexation en exploitant plusieurs cœurs CPU.

#### Étape 1 : configurer l'environnement

Préparez l'index et assurez-vous que la JVM dispose de suffisamment de mémoire heap.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : configurer le multithreading

Définissez le nombre de threads de travail ; chaque thread traite un sous‑ensemble de documents.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Propriété des options d'indexation des métadonnées

**Vue d'ensemble** – Ajuster finement quelles métadonnées de document sont indexées et comment elles sont stockées.

#### Étape 1 : configurer l'environnement

Chargez un document contenant des champs de métadonnées tels que l'auteur, le titre et des balises personnalisées.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : configurer les options de métadonnées

`MetadataIndexingOptions` vous permet d'activer ou de désactiver des champs de métadonnées individuels et de définir des limites de taille.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Applications pratiques

1. **Systèmes de gestion de documents** – Utilisez l'indexation asynchrone pour garder l'interface utilisateur réactive pendant que de gros lots sont traités en arrière-plan.  
2. **Moteurs de recherche de contenu** – Appliquez l'annulation pour empêcher les tâches de longue durée de monopoliser les ressources du serveur pendant les pics de trafic.  
3. **Pipelines d'ingestion à grande échelle** – Exploitez le multithreading pour **ajouter des documents à l'index** à grande échelle, réduisant considérablement le temps de traitement.  

## Considérations de performance

- **Gestion des threads** – Surveillez l'utilisation du CPU ; trop de threads peuvent entraîner un surcoût de commutation de contexte.  
- **Empreinte mémoire** – Les limites de métadonnées (par ex., `setMaxBytesToIndexField`) maintiennent une utilisation de mémoire prévisible.  
- **Collecte des déchets** – Utilisez les drapeaux JVM appropriés (`-Xmx`, `-XX:+UseG1GC`) lors de l'indexation de corpus massifs.  

## Problèmes courants et solutions

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| L'indexation ne se termine jamais | Annulation définie trop basse | Augmentez la valeur de `cancelAfter` ou supprimez l'annulation pour les longues tâches |
| Aucune mise à jour de statut en mode asynchrone | Gestionnaire d'événement non attaché correctement | Assurez-vous que `index.getEvents().StatusChanged.add(...)` est appelé avant `index.add` |
| Erreurs de dépassement de mémoire | Trop de threads ou limites de métadonnées élevées | Réduisez `options.setThreads` et diminuez les limites des champs de métadonnées |
| Métadonnées manquantes dans les résultats | Indexation des métadonnées désactivée | Vérifiez que `options.getMetadataIndexingOptions()` est configuré et n'est pas réglé pour ignorer les champs |

## Questions fréquemment posées

**Q : Comment obtenir une licence temporaire pour GroupDocs.Search ?**  
R : Visitez la [page de licence temporaire de GroupDocs](https://purchase.groupdocs.com/temporary-license/) et suivez les instructions à l'écran.

**Q : Puis‑je annuler une opération d'indexation en cours ?**  
R : Oui – utilisez la propriété d'annulation avec `cancelAfter()` ou invoquez `Cancellation.cancel()` programmétiquement.

**Q : Quels sont quelques cas d'utilisation de l'indexation asynchrone ?**  
R : La récupération de documents en temps réel, le traitement de lots en arrière-plan et les applications à interface réactive bénéficient de l'indexation asynchrone.

**Q : Est‑il sûr d'augmenter le nombre de threads sur un serveur partagé ?**  
R : Augmentez progressivement et surveillez la charge CPU ; sur des environnements fortement partagés, maintenez le nombre de threads modeste (2‑4).

**Q : Comment l'indexation des métadonnées affecte‑t‑elle la pertinence de la recherche ?**  
R : Des métadonnées correctement indexées (auteur, date de création, balises) peuvent être pondérées davantage dans les requêtes, améliorant la précision des résultats.

## Conclusion

En adoptant ces fonctionnalités avancées de GroupDocs.Search pour Java, vous **améliorerez la latence de recherche** dans une variété de scénarios — de l'ingestion rapide de documents au contrôle granulaire des métadonnées. Expérimentez avec différentes configurations, surveillez l'utilisation des ressources et adaptez les paramètres à votre charge de travail spécifique pour obtenir les meilleurs résultats.

---

**Dernière mise à jour :** 2026-08-15  
**Testé avec :** GroupDocs.Search 25.4 for Java  
**Auteur :** GroupDocs

## Tutoriels associés

- [Améliorer les performances des requêtes avec GroupDocs.Search Java : optimiser l'index et la recherche](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Comment ajouter des documents à l'index avec l'indexation des métadonnées en Java en utilisant GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Comment ajouter plusieurs alias et ajouter des documents à l'index dans GroupDocs.Search pour Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)