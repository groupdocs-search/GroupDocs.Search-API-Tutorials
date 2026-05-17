---
date: '2026-01-16'
description: Apprenez comment configurer le réseau de recherche GroupDocs en Java
  et ajouter des synonymes à l’index pour améliorer l’efficacité de la recherche.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Configurer le réseau GroupDocs.Search en Java – Optimiser la recherche
type: docs
url: /fr/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Configurer le réseau GroupDocs.Search en Java – Optimiser la recherche

Dans les applications actuelles axées sur les données, **configure groupdocs search network** est l’étape clé pour fournir des résultats rapides et précis sur d’immenses collections de documents. Que vous construisiez un portail de recherche d’entreprise ou que vous étendiez une solution existante, un réseau GroupDocs.Search bien configuré vous permet de mettre à l’échelle horizontalement, d’ajouter la prise en charge des synonymes et de maintenir une latence faible. Dans ce tutoriel, vous apprendrez comment installer, déployer et affiner un réseau GroupDocs.Search avec Java, ainsi que des astuces pratiques pour ajouter des synonymes à l’index et gérer le cycle de vie des nœuds.

## Réponses rapides
- **Quel est le principal avantage de configurer un réseau GroupDocs.Search ?** Il permet l’indexation et l’interrogation distribuées, améliorant les performances et la scalabilité.  
- **Ai‑je besoin d’une licence pour exécuter les exemples ?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Les synonymes peuvent‑ils être ajoutés sans reconstruire l’index ?** Oui — utilisez le dictionnaire de synonymes à l’exécution pour **add synonyms to index**.  
- **Combien de nœuds puis‑je déployer ?** Vous pouvez déployer autant de nœuds que votre infrastructure le permet ; chaque nœud fonctionne sur son propre port.  

## Qu’est‑ce que la configuration d’un réseau GroupDocs.Search ?
Configurer un réseau GroupDocs.Search signifie définir la structure des dossiers, les ports et les paramètres des nœuds qui permettent à plusieurs instances JVM de collaborer à l’indexation et à la recherche. Cette configuration crée un nœud maître qui coordonne les travailleurs (shards) et garantit que les requêtes sont exécutées sur l’ensemble du jeu de données.

## Pourquoi configurer un réseau GroupDocs.Search ?
- **Scalabilité** – Répartir la charge d’indexation sur plusieurs machines.  
- **Fiabilité** – Les nœuds peuvent être ajoutés ou retirés sans interruption.  
- **Pertinence de la recherche** – Ajouter des synonymes à l’index pour des résultats plus riches.  
- **Performance** – L’exécution parallèle des requêtes réduit le temps de réponse.

## Prérequis
- Java Development Kit (JDK) 8 ou version ultérieure  
- Maven pour la construction du projet  
- Familiarité de base avec la syntaxe Java  
- Accès à la bibliothèque GroupDocs.Search for Java (téléchargée via Maven ou la page officielle de téléchargement)

## Configuration de GroupDocs.Search pour Java

Ajoutez le dépôt et la dépendance à votre **pom.xml** Maven :

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

### Acquisition de licence
- **Essai gratuit** – Explorez les fonctionnalités de base sans frais.  
- **Licence temporaire** – Débloquez toutes les capacités pour des tests à court terme.  
- **Licence commerciale** – Obligatoire pour les déploiements en production.

### Initialisation et configuration de base
Créez une classe Java simple pour vérifier que la bibliothèque se charge correctement :

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
Définissez le dossier de documents de base et le port de départ pour la communication entre nœuds.

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

- **basePath** – Emplacement où résident les dictionnaires (par ex. les fichiers de synonymes).  
- **basePort** – Le premier port ; les nœuds suivants incrémentent cette valeur.

### 2. Déploiement des nœuds du réseau de recherche
Lancez plusieurs nœuds travailleurs qui partagent la même configuration.

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

Chaque nœud fonctionne sur son propre port (basePort + index) et détient une partie du grand index.

### 3. Souscription aux événements des nœuds
Surveillez la santé, la progression de l’indexation et les erreurs en attachant un écouteur d’événements au nœud maître.

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

Les rappels d’événements vous permettent de réagir au démarrage/arrêt d’un nœud, à la fin de l’indexation et aux pannes inattendues.

### 4. Ajout de synonymes à l’indexeur d’un nœud  
Améliorez la pertinence en **add synonyms to index** à l’exécution.

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

- **group** – Tableau de termes qui doivent être considérés comme équivalents.  
- **clearBeforeAdding** – Définissez à `true` si vous souhaitez remplacer les entrées existantes.

### 5. Ajout de répertoires pour l’indexation
Indiquez au nœud maître quels dossiers contiennent les documents à rendre recherchables.

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

La méthode parcourt le répertoire de façon récursive et répartit les fichiers entre les shards.

### 6. Exécution d’une recherche textuelle dans le réseau
Exécutez une requête sur tous les nœuds, en forçant éventuellement un comportement de correspondance exacte.

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

Passez `exactMatchOnly` à `true` lorsque vous avez besoin d’une correspondance stricte des termes sans stemming.

### 7. Fermeture des nœuds du réseau
Libérez les ressources de façon ordonnée une fois le traitement terminé.

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

Une fermeture correcte évite les fuites de mémoire et maintient la JVM en bonne santé.

## Applications pratiques
| Scénario | Comment le réseau aide |
|----------|------------------------|
| **Recherche d’entreprise** | Répartir l’indexation sur les serveurs du centre de données pour des corpus à l’échelle du pétaoctet. |
| **Gestion de documents** | Ajouter des synonymes à l’index afin que les utilisateurs trouvent les documents même avec une terminologie variée. |
| **Catalogue e‑commerce** | Déployer des nœuds spécifiques à chaque région pour servir rapidement des recherches de produits localisées. |
| **Gestion de contenu** | Garder le contenu searchable pendant que les éditeurs ajoutent de nouveaux fichiers dans des répertoires spécifiques. |

## Problèmes courants et solutions
- **Conflits de ports** – Assurez‑vous que le port de chaque nœud (basePort + index) est libre ; ajustez `basePort` si nécessaire.  
- **Synonyme non appliqué** – Vérifiez que vous avez appelé `indexer.setDictionary(dictionary)` après avoir ajouté les termes.  
- **Nœud ne répond pas** – Souscrivez aux événements ; recherchez les callbacks `NodeFailed` pour diagnostiquer les problèmes réseau.  
- **Fuite de mémoire à la fermeture** – Appelez toujours `node.close()` pour chaque nœud déployé.

## Questions fréquentes

**Q : Comment le déploiement de plusieurs nœuds améliore‑t‑il les performances de recherche ?**  
R : Chaque nœud indexe une partie des données, ce qui permet un traitement parallèle et réduit la latence des requêtes grâce au partage de la charge.

**Q : Puis‑je ajouter des synonymes sans ré‑indexer les documents existants ?**  
R : Oui, vous pouvez **add synonyms to index** à l’exécution via le dictionnaire de synonymes ; les changements prennent effet immédiatement pour les nouvelles requêtes.

**Q : La souscription aux événements des nœuds est‑elle obligatoire ?**  
R : Ce n’est pas requis pour le fonctionnement de base, mais la souscription aux événements vous donne une visibilité sur la santé des nœuds et vous aide à réagir rapidement aux pannes.

**Q : Quelles sont les meilleures pratiques pour gérer les ressources des nœuds ?**  
R : Fermez régulièrement les nœuds inactifs, surveillez l’utilisation de la mémoire JVM et recyclez les nœuds pendant les heures creuses afin d’optimiser la consommation de ressources.

**Q : GroupDocs.Search prend‑il en charge les formats non textuels comme les PDF ou les images ?**  
R : Absolument. La bibliothèque extrait le texte des PDF, des fichiers Office et effectue même de l’OCR sur les images, les rendant recherchables dès le départ.

**Dernière mise à jour** : 2026-01-16  
**Testé avec** : GroupDocs.Search 25.4 for Java  
**Auteur** : GroupDocs