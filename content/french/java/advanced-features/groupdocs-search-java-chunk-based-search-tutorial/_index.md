---
date: '2026-02-21'
description: Apprenez comment ajouter des documents à l'index et améliorer les performances
  de recherche avec la recherche basée sur des fragments en Java en utilisant GroupDocs.Search,
  en optimisant la mémoire de l'index de recherche Java pour de grands ensembles de
  documents.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Ajouter des documents à l'index avec une recherche par morceaux en Java
type: docs
url: /fr/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Ajouter des documents à l'index avec la recherche par morceaux en Java

Dans les applications modernes qui doivent **ajouter des documents à l'index** rapidement puis exécuter des requêtes rapides basées sur des morceaux, vous voudrez une solution qui s'adapte sans exploser la mémoire. Ce tutoriel vous guide dans la configuration de GroupDocs.Search pour Java, l'ajout de plusieurs dossiers de documents, et la configuration du moteur pour **augmenter les performances de recherche** tout en maintenant la consommation de **java search index memory** sous contrôle. Que vous indexiez des contrats juridiques, des tickets de support ou des articles de recherche, les étapes ci‑dessous vous fourniront une implémentation prête pour la production.

## Réponses rapides
- **Quelle est la première étape ?** Créez un dossier d'index de recherche.  
- **Comment inclure de nombreux fichiers ?** Utilisez `index.add()` pour chaque dossier de documents.  
- **Quelle option active la recherche par morceaux ?** `options.setChunkSearch(true)`.  
- **Puis-je continuer la recherche après le premier morceau ?** Oui, appelez `index.searchNext()` avec le jeton.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit ou une licence temporaire suffit pour le développement ; une licence complète est requise pour la production.  

## Ce que vous apprendrez
- Comment créer un index de recherche dans un dossier spécifié.  
- Étapes pour **ajouter des documents à l'index** depuis plusieurs emplacements.  
- Configurer les options de recherche pour activer la recherche par morceaux.  
- Effectuer des recherches initiales et ultérieures basées sur des morceaux.  
- Scénarios réels où la recherche de documents par morceaux excelle.  

## Prérequis
- **Bibliothèques requises** : GroupDocs.Search for Java 25.4 ou plus.  
- **Configuration de l'environnement** : Un JDK (Java Development Kit) compatible installé.  
- **Pré-requis de connaissances** : Programmation Java de base et familiarité avec Maven.  

## Configuration de GroupDocs.Search pour Java
Pour commencer, intégrez GroupDocs.Search à votre projet en utilisant Maven :

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

Sinon, téléchargez la dernière version depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
- **Essai gratuit** – testez les fonctionnalités de base sans engagement.  
- **Licence temporaire** – accès prolongé pour le développement.  
- **Achat** – licence complète pour une utilisation en production.  

### Initialisation et configuration de base
Créez un index dans le dossier où vous souhaitez que les données recherchables résident :

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Comment ajouter des documents à l'index
Maintenant que l'index existe, l'étape logique suivante est de **ajouter des documents à l'index** depuis les emplacements où vos fichiers sont stockés.

### 1. Création d'un index
**Vue d'ensemble** : Configurez un répertoire pour l'index de recherche.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Ajout de documents à l'index
**Vue d'ensemble** : Importez des fichiers depuis plusieurs dossiers sources.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Configuration des options de recherche pour la recherche par morceaux
Activez la recherche par morceaux en ajustant l'objet d'options.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Exécution de la recherche initiale par morceaux
Exécutez la première requête en utilisant les options activées pour les morceaux.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Poursuite de la recherche par morceaux
Itérez à travers les morceaux restants jusqu'à ce que la recherche soit terminée.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Pourquoi utiliser la recherche par morceaux ?
La recherche par morceaux divise d'énormes collections de documents en morceaux gérables, réduisant la pression sur la mémoire et accélérant les temps de réponse. Elle est particulièrement bénéfique lorsqu :

1. **Les équipes juridiques** doivent localiser des clauses spécifiques parmi des milliers de contrats.  
2. **Les portails de support client** doivent afficher instantanément les articles pertinents de la base de connaissances.  
3. **Les chercheurs** parcourent d'importants ensembles de données sans charger les fichiers entiers en mémoire.  

## Comment cette approche **augmente les performances de recherche**
En recherchant de plus petits morceaux plutôt que des fichiers entiers, le moteur peut :

- Ignorer les sections non pertinentes tôt, réduisant les cycles CPU.  
- Ne garder en mémoire que le morceau actif, ce qui réduit directement la consommation de **java search index memory**.  
- Paralléliser le traitement des morceaux sur des machines multi‑cœurs pour des résultats plus rapides.  

## Gestion de **java search index memory**
Bien que la recherche par morceaux réduise déjà l'empreinte mémoire, vous pouvez affiner davantage la JVM :

- Allouez un tas suffisant (`-Xmx2g` ou plus) en fonction de la taille de l'index.  
- Utilisez `index.optimize()` après des ajouts massifs pour compresser la structure de l'index.  
- Surveillez les pauses du GC avec des outils comme VisualVM pour éviter les pics de latence.  

## Considérations de performance
- **Gestion de la mémoire** – Allouez un espace de tas suffisant (`-Xmx`) pour les grands index.  
- **Surveillance des ressources** – Gardez un œil sur l'utilisation du CPU pendant les opérations d'indexation et de recherche.  
- **Maintenance de l'index** – Reconstruisez ou nettoyez périodiquement l'index pour éliminer les données obsolètes.  

## Pièges courants & dépannage
| Problème | Pourquoi cela se produit | Solution |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Taille du tas trop faible | Augmentez le tas JVM (`-Xmx2g` ou plus) |
| No results returned | Jeton de morceau non traité | Assurez‑vous que la boucle `while` s'exécute jusqu'à ce que `getNextChunkSearchToken()` soit `null` |
| Slow search performance | Index non optimisé | Exécutez `index.optimize()` après des ajouts massifs |

## Questions fréquemment posées

**Q : Qu’est‑ce que la recherche par morceaux ?**  
R : La recherche par morceaux divise l’ensemble de données en plus petites pièces, permettant des requêtes efficaces sur de grands volumes de données sans charger les documents entiers en mémoire.

**Q : Comment mettre à jour mon index avec de nouveaux fichiers ?**  
R : Il suffit d’appeler `index.add()` avec le chemin des nouveaux documents ; l'index les incorporera automatiquement.

**Q : GroupDocs.Search peut‑il gérer différents formats de fichiers ?**  
R : Oui, il prend en charge les PDF, DOCX, XLSX, PPTX et de nombreux autres formats courants.

**Q : Quels sont les goulets d’étranglement de performance typiques ?**  
R : Les contraintes de mémoire et les index non optimisés sont les plus courants ; allouez un tas suffisant et optimisez régulièrement l'index.

**Q : Où puis‑je trouver une documentation plus détaillée ?**  
R : Visitez la documentation officielle [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) pour des guides approfondis et des références API.

**Q : La recherche par morceaux fonctionne‑t‑elle avec des PDF chiffrés ?**  
R : Oui, tant que vous fournissez le mot de passe via la surcharge d'API appropriée.

**Q : Comment puis‑je surveiller la progression de l'indexation ?**  
R : Utilisez la surcharge `Index.add()` qui renvoie un objet `Progress` ou branchez‑vous aux callbacks de journalisation.

## Ressources
- **Documentation** : [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Référence API** : [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Téléchargement** : [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub** : [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Support gratuit** : [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licence temporaire** : [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Dernière mise à jour :** 2026-02-21  
**Testé avec :** GroupDocs.Search 25.4 for Java  
**Auteur :** GroupDocs  

---