---
date: '2026-02-06'
description: Apprenez à ajouter des documents à l'index et à activer la recherche
  sensible à la casse en Java avec GroupDocs.Search, améliorant la précision de votre
  application.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Ajouter des documents à l''index : recherche Java sensible à la casse avec
  GroupDocs'
type: docs
url: /fr/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Ajouter des documents à l'index : Maîtriser les recherches sensibles à la casse en Java avec GroupDocs

Récupérer la bonne information au sein d’une collection massive de documents est une exigence fondamentale pour les applications modernes. Dans ce guide, vous apprendrez **comment ajouter des documents à l'index** et effectuer des **recherches sensibles à la casse** en utilisant GroupDocs.Search pour Java. Que vous construisiez un dépôt de documents juridiques, un catalogue e‑commerce ou un système de gestion de contenu, des résultats de recherche précis maintiennent les utilisateurs satisfaits et vos données fiables.

## Réponses rapides
- **Quelle est l’étape principale pour commencer à rechercher ?** Ajouter des documents à un index avec `index.add(...)`.
- **Comment activer la recherche sensible à la casse ?** Définir `options.setUseCaseSensitiveSearch(true)`.
- **Puis‑je rechercher dans plusieurs répertoires ?** Oui – appelez `index.add()` pour chaque dossier que vous souhaitez inclure.
- **Quelle méthode permet de rechercher avec des objets ?** Utilisez `SearchQuery.createWordQuery(...)`.
- **Ai‑je besoin d’une licence pour les tests ?** Une licence temporaire est disponible à des fins d’essai.

## Que signifie « ajouter des documents à l'index » ?
Ajouter des documents à un index consiste à alimenter vos fichiers sources (PDF, documents Word, texte brut, etc.) dans GroupDocs.Search afin qu’il puisse construire une structure de données interrogeable. Une fois indexés, le moteur peut exécuter des requêtes rapides, y compris celles sensibles à la casse.

## Pourquoi activer la recherche sensible à la casse en Java ?
- **Correspondance exacte des termes** – différencier « Apple » (l’entreprise) de « apple » (le fruit).  
- **Conformité réglementaire** – certaines industries exigent une correspondance exacte des phrases.  
- **Pertinence améliorée** – les utilisateurs s’attendent souvent à des résultats spécifiques à la casse dans des contextes techniques ou juridiques.

## Prérequis
- JDK (Java 17 ou version ultérieure recommandée)  
- Maven pour la gestion des dépendances  
- Un IDE tel qu’IntelliJ IDEA ou Eclipse  
- Familiarité de base avec la programmation Java  

## Configuration de GroupDocs.Search pour Java
Tout d’abord, ajoutez le dépôt GroupDocs et la dépendance à votre `pom.xml` :

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

Vous pouvez également télécharger la dernière version directement depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licence
Pour commencer avec un essai, rendez‑vous sur le site GroupDocs afin d’obtenir une licence temporaire. Cela vous permettra de tester toutes les fonctionnalités sans aucune limitation.

## Comment ajouter des documents à l'index – Recherche par requête texte

### Étape 1 : Créer un index et ajouter vos documents
Créez un dossier où les fichiers d’index seront stockés, puis ajoutez le répertoire source contenant les documents que vous souhaitez rechercher.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Astuce :** Vous pouvez appeler `index.add()` plusieurs fois pour **rechercher dans plusieurs répertoires** au sein d’un même index.

### Étape 2 : Activer la recherche sensible à la casse
Configurez les options de recherche pour respecter la casse des lettres.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Étape 3 : Exécuter une requête texte sensible à la casse
Lancez une requête qui différencie « Advantages » de « advantages ».

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

La boucle affiche le chemin complet de chaque document contenant le terme exactement correspondant à la casse.

## Comment ajouter des documents à l'index – Recherche par requête d’objet

Les requêtes d’objet offrent plus de flexibilité, notamment lorsque vous devez combiner plusieurs critères.

### Étape 1 : Initialiser un second index (facultatif)
Si vous préférez garder les recherches basées sur les objets séparées, créez un autre dossier d’index.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Étape 2 : Réutiliser l’option sensible à la casse
La même instance de `SearchOptions` fonctionne pour les requêtes d’objet.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Étape 3 : Construire et exécuter une requête d’objet
Créez un objet de requête de mot et transmettez‑le au moteur de recherche.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Utiliser `createWordQuery` vous permet ensuite de le combiner avec des requêtes de phrase, de caractère générique ou booléennes pour des scénarios plus complexes.

## Applications pratiques
- **Gestion de documents juridiques :** Récupérer des statuts spécifiques où la capitalisation compte.  
- **Plateformes e‑commerce :** Distinguer des SKU produits comme « PRO‑X » vs. « pro‑x ».  
- **Systèmes de gestion de contenu (CMS) :** Garantir que les auteurs trouvent les titres ou tags exacts.

## Considérations de performance
- **Maintenir l’index à jour** – ré‑indexer lorsque de nouveaux fichiers sont ajoutés ou que les existants changent.  
- **Surveiller l’utilisation de la mémoire** – les grands corpus bénéficient d’un indexage incrémental et d’une taille de heap JVM appropriée.  
- **Exploiter le ramasse‑miettes Java** – libérer les objets `Index` lorsqu’ils ne sont plus nécessaires.

## Problèmes courants et solutions
| Problème | Solution |
|----------|----------|
| `useCaseSensitiveSearch` semble ignoré | Vérifiez que vous utilisez la dernière version de GroupDocs.Search et que l’index a été reconstruit après modification de l’option. |
| Aucun résultat retourné pour un terme connu | Assurez‑vous que la casse du terme correspond exactement et que le document a bien été ajouté à l’index. |
| La recherche dans de nombreux dossiers ralentit | Ajoutez chaque dossier individuellement avec `index.add()` et envisagez de diviser l’index en fragments pour des ensembles de données très volumineux. |

## Questions fréquemment posées

**Q :** Comment gérer de grands ensembles de données avec GroupDocs.Search ?  
**R :** Utilisez le partitionnement d’index, ajustez les paramètres de mémoire JVM et compactez périodiquement l’index pour maintenir des performances optimales.

**Q :** Puis‑je rechercher simultanément dans plusieurs répertoires ?  
**R :** Oui – appelez `index.add()` pour chaque répertoire que vous souhaitez inclure, puis exécutez une seule requête sur l’index combiné.

**Q :** Quels sont les pièges courants lors de la configuration des recherches sensibles à la casse ?  
**R :** Oublier de reconstruire l’index après avoir activé `useCaseSensitiveSearch`, ou utiliser une casse incorrecte dans la chaîne de requête.

**Q :** Comment dépanner les erreurs de recherche ?  
**R :** Consultez les fichiers journaux générés par GroupDocs.Search pour les traces de pile, et confirmez que toutes les dépendances Maven sont correctement résolues.

**Q :** GroupDocs.Search est‑il adapté aux applications en temps réel ?  
**R :** Avec des stratégies d’indexation appropriées (mises à jour incrémentales et mise en cache en mémoire), il peut fournir des résultats de recherche quasi temps réel.

## Ressources
- **Documentation :** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **Référence API :** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Téléchargement :** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **Dépôt GitHub :** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum d’assistance :** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Licence temporaire :** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour :** 2026-02-06  
**Testé avec :** GroupDocs.Search 25.4  
**Auteur :** GroupDocs  

---