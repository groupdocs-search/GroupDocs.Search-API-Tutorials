---
date: '2026-03-01'
description: Apprenez à optimiser les performances de recherche et à améliorer la
  latence de recherche en utilisant les fonctionnalités avancées d’indexation de GroupDocs.Search
  pour Java, y compris l’annulation, les opérations asynchrones, le multithreading
  et la personnalisation des métadonnées.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: Optimisez les performances de recherche avec des techniques d'indexation avancées
  dans GroupDocs.Search pour Java
type: docs
url: /fr/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Optimiser les performances de recherche avec des techniques d'indexation avancées dans GroupDocs.Search pour Java

Dans l'environnement numérique actuel, où tout va très vite, **optimiser les performances de recherche** est essentiel pour fournir des résultats instantanés aux utilisateurs. Que vous construisiez un moteur de recherche personnalisé ou amélioriez un système de gestion de documents existant, la bonne stratégie d'indexation peut réduire considérablement la latence, diminuer la consommation de ressources, et **améliorer la latence de recherche** dans tous les cas. Dans ce tutoriel, nous passerons en revue les fonctionnalités les plus puissantes de GroupDocs.Search pour Java — annulation, indexation asynchrone, multithreading et personnalisation des métadonnées — afin que vous puissiez **ajouter des documents à l'index** plus rapidement et plus efficacement.

**Ce que vous apprendrez**

- Comment annuler une opération d'indexation après un temps spécifié  
- Effectuer des opérations d'indexation asynchrones et gérer les changements d'état  
- Configurer le multithreading pour une indexation plus rapide  
- Personnaliser les options d'indexation des métadonnées  

Assurons-nous que vous avez tout ce dont vous avez besoin avant de plonger dans le code.

## Prérequis

- **GroupDocs.Search Library** – version 25.4 ou ultérieure.  
- **Java Development Environment** – JDK 8 ou supérieur est recommandé.  
- Familiarité de base avec Java et le concept d'indexation.

### Configuration de GroupDocs.Search pour Java

#### Installation Maven

Add the repository and dependency to your `pom.xml` file:

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

Alternativement, téléchargez le JAR le plus récent depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Acquisition de licence** – Commencez avec un essai gratuit ou demandez une licence temporaire pour débloquer l'ensemble complet des fonctionnalités.

### Initialisation et configuration de base

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

## Réponses rapides
- **Que fait l'annulation ?** Arrête l'indexation après un temps défini pour libérer les ressources.  
- **Puis-je indexer des documents de manière asynchrone ?** Oui – définissez `options.setAsync(true)`.  
- **Combien de threads puis-je utiliser ?** Tout entier positif ; les valeurs typiques sont 2‑4 pour la plupart des serveurs.  
- **L'indexation des métadonnées est‑elle optionnelle ?** Absolument – vous pouvez l'activer ou l'ajuster par champ.  
- **Ai‑je besoin d'une licence pour ces fonctionnalités ?** Un essai fonctionne pour les tests ; une licence complète est requise en production.

## Qu’est‑ce que « Optimiser les performances de recherche » dans ce contexte ?

Optimiser les performances de recherche signifie configurer le processus d'indexation afin qu'il consomme la bonne quantité de CPU, de mémoire et de temps tout en délivrant instantanément les résultats les plus pertinents. En contrôlant l'annulation, l'exécution asynchrone, le multithreading et la gestion des métadonnées, vous influencez directement la rapidité avec laquelle le moteur peut **ajouter des documents à l'index** et répondre aux requêtes.

## Pourquoi utiliser les fonctionnalités d'indexation avancées ?

- **Latence réduite** – L'indexation asynchrone et multithreadée maintient votre application réactive.  
- **Meilleure gestion des ressources** – L'annulation empêche les processus incontrôlés.  
- **Pertinence de recherche adaptée** – Les options de métadonnées vous permettent de mettre en avant les informations les plus importantes.  

## Comment améliorer la latence de recherche avec l'indexation avancée ?

Lorsque vous devez **améliorer la latence de recherche**, envisagez de combiner les fonctionnalités que nous explorerons : annuler les tâches longues, exécuter l'indexation en arrière‑plan et répartir le travail sur plusieurs cœurs CPU. Cette approche multi‑facettes offre souvent les plus grands gains de vitesse.

## Guide d'implémentation

### Propriété d'annulation

**Vue d'ensemble** – Annule l'indexation après une durée spécifiée afin d'éviter une surconsommation de ressources.

#### Étape 1 : Configurer l'environnement

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : Créer les options d'indexation avec annulation

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

**Vue d'ensemble** – Exécute l'indexation sur un thread en arrière‑plan et écoute les changements d'état.

#### Étape 1 : Configurer l'environnement

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : S'abonner à l'événement StatusChanged

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

#### Étape 3 : Configurer les options asynchrones

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Propriété des threads

**Vue d'ensemble** – Accélère l'indexation en exploitant plusieurs cœurs CPU.

#### Étape 1 : Configurer l'environnement

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : Configurer le multithreading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Propriété des options d'indexation des métadonnées

**Vue d'ensemble** – Ajuste finement quelles métadonnées de document sont indexées et comment elles sont stockées.

#### Étape 1 : Configurer l'environnement

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Étape 2 : Configurer les options de métadonnées

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

1. **Systèmes de gestion de documents** – Utilisez l'indexation asynchrone pour garder l'interface utilisateur réactive pendant que de gros lots sont traités en arrière‑plan.  
2. **Moteurs de recherche de contenu** – Appliquez l'annulation pour empêcher les tâches longues de monopoliser les ressources serveur pendant les pics de trafic.  
3. **Pipelines d'ingestion à grande échelle** – Exploitez le multithreading pour **ajouter des documents à l'index** à grande échelle, réduisant considérablement le temps de traitement.

## Considérations de performance

- **Gestion des threads** – Surveillez l'utilisation du CPU ; trop de threads peuvent engendrer un surcoût de commutation de contexte.  
- **Empreinte mémoire** – Les limites de métadonnées (par ex., `setMaxBytesToIndexField`) aident à garder une utilisation mémoire prévisible.  
- **Garbage Collection** – Utilisez les drapeaux JVM appropriés (`-Xmx`, `-XX:+UseG1GC`) lors de l'indexation de corpus massifs.

## Problèmes courants et solutions

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| L'indexation ne se termine jamais | Annulation définie trop basse | Augmentez la valeur de `cancelAfter` ou supprimez l'annulation pour les longues tâches |
| Aucun mise à jour de statut en mode async | Gestionnaire d'événement non attaché correctement | Assurez‑vous que `index.getEvents().StatusChanged.add(...)` est appelé avant `index.add` |
| Erreurs de mémoire insuffisante | Trop de threads ou limites de métadonnées élevées | Réduisez `options.setThreads` et baissez les limites des champs de métadonnées |
| Métadonnées manquantes dans les résultats | Indexation des métadonnées désactivée | Vérifiez que `options.getMetadataIndexingOptions()` est configuré et n'est pas réglé pour ignorer les champs |

## Questions fréquentes

**Q : Comment obtenir une licence temporaire pour GroupDocs.Search ?**  
R : Visitez la [page de licence temporaire de GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q : Puis‑je annuler une opération d'indexation en cours ?**  
R : Oui – utilisez la propriété d'annulation avec `cancelAfter()` ou appelez `Cancellation.cancel()` programmétiquement.

**Q : Quels sont les cas d'utilisation de l'indexation asynchrone ?**  
R : La récupération de documents en temps réel, le traitement de lots en arrière‑plan et les applications avec interface réactive bénéficient de l'indexation asynchrone.

**Q : Est‑il sûr d'augmenter le nombre de threads sur un serveur partagé ?**  
R : Augmentez progressivement et surveillez la charge CPU ; sur des environnements très partagés, maintenez le nombre de threads modeste (2‑4).

**Q : Comment l'indexation des métadonnées affecte‑t‑elle la pertinence des recherches ?**  
R : Des métadonnées correctement indexées (auteur, date de création, tags) peuvent être pondérées davantage dans les requêtes, améliorant la précision des résultats.

## Conclusion

En adoptant ces fonctionnalités avancées de GroupDocs.Search pour Java, vous **optimiserez les performances de recherche** dans une variété de scénarios — de l'ingestion rapide de documents au contrôle fin des métadonnées. Expérimentez avec différentes configurations, surveillez l'utilisation des ressources et adaptez les paramètres à votre charge de travail spécifique pour obtenir les meilleurs résultats.

---

**Dernière mise à jour** : 2026-03-01  
**Testé avec** : GroupDocs.Search 25.4 for Java  
**Auteur** : GroupDocs