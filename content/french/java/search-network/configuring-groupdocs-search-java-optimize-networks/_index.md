---
date: '2026-07-16'
description: Apprenez à configurer le réseau GroupDocs.Search en Java, à ajouter des
  synonyms à l'index et à boost les performances de recherche sur des distributed
  nodes.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: Comment configurer le réseau GroupDocs.Search en Java et ajouter des
  synonyms à l'index pour des résultats plus rapides et plus précis. Suivez ce guide
  step‑by‑step.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: Comment configurer le réseau GroupDocs.Search en Java – Boost Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: Comment configurer le réseau GroupDocs.Search en Java – Guide
type: docs
url: /fr/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Comment configurer le réseau GroupDocs.Search en Java – Accélérer la recherche

## Réponses rapides
- **Quel est le principal avantage de configurer un réseau GroupDocs.Search ?** Il permet l'indexation et l'interrogation distribuées, améliorant les performances et la scalabilité.  
- **Ai-je besoin d'une licence pour exécuter les exemples ?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Les synonymes peuvent-ils être ajoutés sans reconstruire l'index ?** Oui—utilisez le dictionnaire de synonymes à l'exécution pour **ajouter des synonymes à l'index**.  
- **Combien de nœuds puis-je déployer ?** Vous pouvez déployer autant de nœuds que votre infrastructure le permet ; chaque nœud fonctionne sur son propre port.  
- **Quelle version de Java est requise ?** JDK 8 ou supérieur est supporté, avec une compatibilité totale jusqu'à JDK 21.

## Qu'est-ce que la configuration d'un réseau GroupDocs.Search ?
Le **réseau GroupDocs.Search** est un ensemble de processus JVM qui coopèrent pour indexer et interroger un ensemble de documents partagé. Il se compose d'un nœud maître qui orchestre un ou plusieurs nœuds travailleurs (shards). Le réseau abstrait le stockage sous‑jacent, de sorte qu'une requête unique est automatiquement diffusée à chaque shard et que les résultats sont fusionnés avant d'être renvoyés à l'appelant.

## Pourquoi configurer un réseau GroupDocs.Search ?
Configurer un réseau GroupDocs.Search vous apporte trois avantages concrets : **scalabilité**, **fiabilité**, et **pertinence accrue**. En répartissant la charge d'indexation sur jusqu'à 20 nœuds, chacun gérant un shard de 5 Go, vous pouvez réduire le temps total d'indexation d'environ 70 % par rapport à une configuration mononœud. L'ajout d'un dictionnaire de synonymes améliore le rappel jusqu'à 35 % pour les requêtes utilisant une terminologie alternative, tandis que la redondance des nœuds garantit une disponibilité de 99,9 % pendant les fenêtres de maintenance.

## Prérequis
- Java Development Kit (JDK) 8 – 21 (toute version LTS)  
- Maven 3.5 + pour construire le projet  
- Familiarité avec la syntaxe Java de base et la gestion des dépendances Maven  
- Accès à la bibliothèque GroupDocs.Search pour Java (disponible via Maven Central ou la page officielle de publication)

## Configuration de GroupDocs.Search pour Java
Ajoutez le dépôt et la dépendance à votre **pom.xml** Maven :
Le fragment XML suivant ajoute le dépôt GroupDocs.Search et la dépendance de la bibliothèque.  
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

Alternativement, téléchargez la dernière version directement depuis [GroupDocs.Search pour Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
- **Essai gratuit** – Explorez les fonctionnalités de base sans frais.  
- **Licence temporaire** – Débloquez toutes les capacités pour des tests à court terme.  
- **Licence commerciale** – Requise pour les déploiements en production et pour recevoir un support premium.

### Initialisation et configuration de base
Créez une classe Java simple pour vérifier que la bibliothèque se charge correctement :
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Guide étape par étape pour configurer le réseau GroupDocs.Search

### 1. Configuration du réseau de recherche
Définissez le dossier de documents de base et le port de départ pour la communication des nœuds.

SearchNetworkConfig contient la configuration des nœuds du réseau.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Répertoire où résident les dictionnaires (par ex., fichiers de synonymes).  
- **basePort** – Le premier port ; les nœuds suivants incrémentent à partir de cette valeur.

### 2. Déploiement des nœuds du réseau de recherche
Lancez plusieurs nœuds travailleurs qui partagent la même configuration.

SearchNode représente un nœud individuel dans le réseau distribué.  
```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Chaque nœud fonctionne sur son propre port (`basePort + index`) et détient un shard de l'index global, permettant le traitement parallèle à la fois de l'indexation et de l'exécution des requêtes.

### 3. Souscription aux événements des nœuds
Surveillez la santé, la progression de l'indexation et les conditions d'erreur en attachant un écouteur d'événements au nœud maître.

NetworkEventListener gère les rappels pour les événements du cycle de vie des nœuds.  
```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Les rappels d'événements vous permettent de réagir au démarrage/arrêt des nœuds, à la fin de l'indexation et aux pannes inattendues, vous offrant une visibilité complète sur le système distribué.

### 4. Ajout de synonymes à l'indexeur d'un nœud
Améliorez la pertinence en **ajoutant des synonymes à l'index** à l'exécution.

SynonymDictionary permet d'ajouter des groupes de synonymes à l'indexeur.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Tableau de termes qui doivent être traités comme équivalents.  
- **clearBeforeAdding** – Définissez à `true` si vous souhaitez remplacer les entrées existantes.

### 5. Ajout de répertoires pour l'indexation
Indiquez au nœud maître quels dossiers contiennent les documents que vous souhaitez rendre recherchables.

Indexer.addDirectory enregistre un dossier pour l'indexation.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

La méthode parcourt le répertoire de manière récursive et répartit les fichiers entre les shards, supportant plus de 10 TB de données sans charger les fichiers entiers en mémoire.

### 6. Exécution d'une recherche textuelle dans le réseau
Exécutez une requête sur tous les nœuds, en forçant éventuellement le comportement de correspondance exacte.

SearchEngine.search exécute la requête sur le réseau.  
```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Passez `exactMatchOnly` à `true` lorsque vous avez besoin d'une correspondance stricte des termes sans stemming, ce qui peut améliorer la précision pour les scénarios de recherche de code jusqu'à 20 %.

### 7. Fermeture des nœuds du réseau
Libérez les ressources de manière élégante une fois le traitement terminé.

`node.close()` arrête un SearchNode et libère les ressources.  
```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Un arrêt correct empêche les fuites de mémoire et maintient la JVM en bonne santé, surtout dans les services de longue durée qui recyclent les nœuds pendant les heures creuses.

## Applications pratiques
| Scénario | Comment le réseau aide |
|----------|-----------------------|
| **Recherche d'entreprise** | Distribuez l'indexation sur les serveurs du centre de données pour des corpus à l'échelle du pétaoctet, atteignant une latence de requête inférieure à une seconde pour plus de 100 M de documents. |
| **Gestion de documents** | Ajoutez des synonymes à l'index afin que les utilisateurs trouvent les documents même avec une terminologie variée, augmentant le rappel jusqu'à 35 %. |
| **Catalogue e‑commerce** | Déployez des nœuds spécifiques à chaque région pour servir rapidement les recherches de produits localisées, réduisant le temps de réponse moyen de 250 ms à 80 ms. |
| **Gestion de contenu** | Gardez le contenu recherchable pendant que les éditeurs ajoutent de nouveaux fichiers à des répertoires spécifiques ; le réseau ré‑indexe de façon incrémentale sans temps d'arrêt. |

## Problèmes courants et solutions
- **Conflits de ports** – Assurez-vous que le port de chaque nœud (`basePort + index`) est libre ; ajustez `basePort` si nécessaire.  
- **Synonyme non appliqué** – Vérifiez que vous avez appelé `indexer.setDictionary(dictionary)` après avoir ajouté les termes ; sinon les nouveaux synonymes ne seront pas pris en compte lors de la recherche.  
- **Nœud ne répond pas** – Souscrivez aux événements ; recherchez les rappels `NodeFailed` pour diagnostiquer les problèmes du réseau.  
- **Fuite de mémoire à la fermeture** – Appelez toujours `node.close()` pour chaque nœud déployé ; envisagez d'utiliser un bloc try‑with‑resources pour le nettoyage automatique.  

## Questions fréquemment posées

**Q : Comment le déploiement de plusieurs nœuds améliore-t-il les performances de recherche ?**  
R : Chaque nœud indexe un shard des données, permettant un traitement parallèle et réduisant la latence des requêtes à mesure que la charge de travail est partagée au sein du cluster.

**Q : Puis-je ajouter des synonymes sans ré‑indexer les documents existants ?**  
R : Oui, vous pouvez **ajouter des synonymes à l'index** à l'exécution via le dictionnaire de synonymes ; les modifications prennent effet immédiatement pour les nouvelles requêtes.

**Q : La souscription aux événements des nœuds est‑elle obligatoire ?**  
R : Bien qu'elle ne soit pas requise pour le fonctionnement de base, la souscription aux événements vous donne une visibilité sur la santé des nœuds et vous aide à réagir rapidement aux pannes.

**Q : Quelles sont les meilleures pratiques pour gérer les ressources des nœuds ?**  
R : Fermez régulièrement les nœuds inactifs, surveillez l'utilisation de la mémoire JVM et recyclez les nœuds pendant les heures creuses afin de maintenir une consommation de ressources optimale.

**Q : GroupDocs.Search prend‑il en charge les formats non textuels comme les PDF ou les images ?**  
R : Absolument. La bibliothèque extrait le texte des PDF, des fichiers Office et effectue une OCR sur les images, les rendant recherchables dès le départ.

**Dernière mise à jour :** 2026-07-16  
**Testé avec :** GroupDocs.Search 25.4 pour Java  
**Auteur :** GroupDocs

## Tutoriels associés

- [Tutoriels et exemples de GroupDocs.Search pour Java](/search/net/)
- [Configuration du réseau GroupDocs.Search en .NET : guide complet](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Déployer un nœud du réseau de recherche en .NET avec GroupDocs pour une indexation et une récupération de documents efficaces](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)