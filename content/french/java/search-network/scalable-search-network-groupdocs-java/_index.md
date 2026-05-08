---
date: '2026-01-24'
description: Apprenez à configurer le port de base de GroupDocs pour des réseaux de
  recherche évolutifs en utilisant GroupDocs.Search Java, à optimiser la vitesse de
  récupération et à mettre en place des systèmes multi‑nœuds.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Configurer le port de base groupdocs dans le réseau de recherche Java
type: docs
url: /fr/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

 de base groupdocs dans le réseau de recherche Java

Dans autres sans conflit. Ce tutoriel vous guide à travers chaque détail — desnœuds complète — afin que vous puissiez lancer en toute confiance un réseau de recherche évolutif avec GroupDocs.Search for Java.

## Réponses rapides
- **Quel est le but principal ?** Définir des ports et répertoires uniques pour chaque nœud de recherche, afin d'éviter les conflits.
- **Ai-je besoin d'une licence ?** Oui, une licence d'essai ou complète est requise pour une utilisation en production.
- **Quelle version de Java est supportée ?** Java 8 ou supérieure.
- **Puis-je exécuter cela sur des serveurs cloud ? nœuds puis‑je ajouter ?** Il n’y a pas de limite stricte ; ajoutez autant que votre matériel et votre réseau le permettent.

## Qu’est‑ce que « configurer le port de base groupdocs » ?
Lorsque vous **configurez le port de base groupdocs**, vous attribuez un port TCP de départ que chaque nœud utilisera (et incrémenterez pour les nœuds suivants). Cette étape simple élimine les redoutées erreurs « port déjà utilisé » et prépare le terrain pour un cluster de recherche propre et horizontalement évolutif.

## Pourquoi utiliser GroupDocs.Search pour un réseau évolutif ?
- **Haute performance** – algorithmes d’indexation et de recherche optimisés.
- **Architecture flexible** – vous pouvez mélanger indexeurs, moteurs de recherche, fragments et extracteurs entre les nœuds.
- **Intégration facile** – fonctionne avec n’importe quelle application Java, sur site ou dans le cloud.
- **Licence robuste** – les options d’essai vous permettent de tester avant de vous engager.

## Prérequis
- **Java Development Kit (JDK)** 8 ou plus récent.
- **IDE** tel que IntelliJ IDEA ou Eclipse.
- **GroupDocs.Search for Java** bibliothèque (version 25.4 ou ultérieure) installée via Maven ou téléchargement manuel.
- Connaissances de base en réseau (ports TCP, localhost vs. hôtes distants).

## Configuration de GroupDocs.Search pour Java

### Instructions d’installation

**Maven Setup:**

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

**Direct Download:**

Sinon, téléchargez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence

- **Essai gratuit** – commencez les tests immédiatement.
- **Licence temporaire** – obtenez un essai prolongé sur [Temporary License](https://purchase.groupdocs.com/temporary-license).
- **Achat complet** – requis pour les déploiements en production.

### Initialisation et configuration de base

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Guide de mise en œuvre

### Comment configurer le port de base groupdocs

#### Configuration des chemins de base

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Pourquoi** : Une structure de répertoires cohérente permet à chaque nœud de localiser ses fichiers d’index, de fragment ou d’extracteur sans ambiguïté.

#### Configuration du port de base

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Pourquoi** : Commencer avec un numéro de port élevé (par ex., 49100) réduit le risque de conflit avec les services courants. Incrémentez le port pour chaque nœud supplémentaire.

#### Définir l’adresse de l’hôte

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Pourquoi** : Utiliser `localhost` est idéal pour le développement ; remplacez‑le par l’IP ou le nom DNS de votre serveur en production.

#### Créer la configuration réseau

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Pourquoi** : Ces options équilibrent vitesse et efficacité de stockage, vous offrant un index de recherche à la fois léger et puissant.

#### Ajouter des nœuds

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Pourquoi** : Répartir les responsabilités entre les nœuds (indexation vs recherche, fragmentation vs extraction) améliore le parallélisme et la tolérance aux pannes.

#### Finaliser la configuration

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Problèmes courants & solutions
- **Conflits de ports** – Incrémentez toujours `basePort` pour chaque nouveau nœud. Vérifiez avec `netstat` ou le moniteur de ports de votre OS.
- **Répertoires manquants** – Assurez‑vous que chaque dossier référencé (`Indexer0`, `Searcher0`, etc.) existe et que le processus Java possède les permissions de lecture/écriture.
- **Accessibilité réseau** – Lors du passage à une configuration multi‑machines, remplacez `127.0.0.1` par l’IP les ports choisis dans les pare‑feux.

##--------|
| Gestion d’entreprise de documents | Mise à l’échelle transparente entre les départements sans interruption |
| Grandes plateformes CMS | Récupération de contenu plus rapide grâce à la distribution de l’index |
| Gestion de dossiers juridiques | Extraction parallèle de PDF réduit la latence de recherche |

## Considérations de performance
- **Surveiller le CPU/mémoire** – Utilisez JMX de Java ou un outil de profilage pour observer l’utilisation des threads.
- **Ajuster la compression** – `Compression.High` économise de ; testez à la fois `High` et `Normal`.
- **Mettre à jour régulièrement** – Les nouvelles versions de GroupDocs.Search incluent souvent des correctifs de performance.

## Conclusion

Vous avez maintenant appris comment **configurer le port de base groupdocs** et mettre en place un réseau de recherche multi‑nœuds en utilisant GroupDocs.Search pour Java. Expérimentez avec des nœuds supplémentaires, ajustez les paramètres d’index et intégrez le réseau à vos applications existantes pour une solution de recherche véritablement évolutive.

## Foire aux questions

**Q : Quel est le but de désactiver les mots vides lors de lactiver les mots vides peut améliorer la précision de la recherche en conservant des termes courants qui peuvent être cruciaux dans des domaines spécialisés.

**Q : Comment gérer les49100) et incrémentez’: Quelle est la différence entre NormalIndex et les autres types d’index ?**  
R : `NormalIndex` offre un compromis équilibré entre vitesse et utilisation de la mémoire, tandis que les index spécialisés (par ex., `FastIndex`) ciblent des scénarios de performance spécifiques.

**Q : Existe‑t‑il une limite au nombre de nœuds que je peux ajouter ?**  
R : Techniquement non ; la limite dépend de vos ressources matérielles et de la bande passante du réseau.

---

**Dernière mise à jour :** 2026-01-24  
**Testé avec :** GroupDocs.Search Java 25.4  
**Auteur :** GroupDocs