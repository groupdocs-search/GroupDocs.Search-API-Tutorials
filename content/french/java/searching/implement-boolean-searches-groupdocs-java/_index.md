---
date: '2026-07-21'
description: Le tutoriel Create Boolean Query Java montre comment implémenter les
  recherches booléennes AND, OR, NOT avec GroupDocs.Search for Java, ajouter des documents
  à un index et améliorer la récupération des documents.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Le tutoriel Create Boolean Query Java explique étape par étape comment
  créer des requêtes AND, OR, NOT avec GroupDocs.Search for Java, ajouter des documents
  à un index et améliorer les performances de récupération.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – Maîtrisez les recherches booléennes avec GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Créer une requête booléenne Java : maîtrisez les recherches booléennes avec
  GroupDocs.Search for Java'
type: docs
url: /fr/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Créez une requête booléenne Java : Maîtrisez les recherches booléennes avec GroupDocs.Search pour Java

Rechercher dans d'énormes collections de documents peut ressembler à chercher une aiguille dans une botte de foin. **Create Boolean Query Java** vous permet d'indiquer au moteur exactement ce dont vous avez besoin — des documents qui contiennent *les deux* termes, *l'un ou l'autre* terme, ou *exclure* les mots indésirables. Dans ce guide, nous parcourrons la configuration de **GroupDocs.Search for Java**, l'ajout de documents à un index, et la création de requêtes booléennes puissantes qui améliorent vos flux de travail de **document retrieval java**. À la fin, vous serez capable d'écrire du code propre et maintenable qui crée des requêtes booléennes en Java en quelques lignes seulement.

## Réponses rapides
- **Qu'est‑ce qu'une requête booléenne AND ?** Renvoie uniquement les documents qui contiennent *tous* les termes spécifiés.  
- **En quoi OR diffère-t-il de AND ?** OR correspond aux documents contenant *n'importe quel* des termes, élargissant ainsi le jeu de résultats.  
- **Quand devrais‑je utiliser NOT ?** Utilisez NOT pour filtrer les documents contenant des mots indésirables.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour les tests ; une licence commerciale est requise pour la production.  
- **Quelle version de Java est requise ?** Java 8+ est pris en charge ; JDK 11+ est recommandé.

## Qu'est‑ce que **create boolean query java** ?
`create boolean query java` fait référence à la construction d'une requête de recherche en Java qui combine des opérateurs logiques tels que AND, OR et NOT en utilisant l'API GroupDocs.Search. En assemblant ces opérateurs, vous pouvez contrôler précisément quels documents correspondent, permettant un filtrage avancé, un réglage de pertinence et des scénarios de recherche complexes.

## Pourquoi utiliser GroupDocs.Search pour Java ?
- **High performance** sur de grands ensembles de documents – il peut indexer et rechercher 500 GB de texte en moins d'une minute sur un serveur standard.  
- **Rich API** qui prend en charge les requêtes basées sur le texte et sur les objets, vous permettant de choisir le style qui correspond à votre architecture.  
- **Built‑in language support** pour le stemming, les mots‑vides et la correspondance floue sur plus de 30 langues.  
- **Easy integration** avec Maven ou téléchargement direct du JAR, ne nécessitant que quelques lignes de code pour démarrer.

## Prérequis
Avant de commencer, assurez‑vous d'avoir :

- **GroupDocs.Search for Java** (v25.4 ou ultérieur) – voir le lien de téléchargement ci‑dessous.  
- JDK 8+ installé et configuré dans votre IDE (IntelliJ IDEA, Eclipse, etc.).  
- Connaissances de base en Java et Maven pour la gestion des dépendances.  

## Configuration de GroupDocs.Search pour Java

### Configuration Maven
Ajoutez le dépôt et la dépendance à votre `pom.xml` :

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

### Téléchargement direct
Sinon, téléchargez le dernier JAR depuis le site officiel : [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
Commencez avec une licence d'essai gratuite pour explorer toutes les fonctionnalités. Pour une utilisation en production, achetez une licence commerciale afin de débloquer toutes les fonctionnalités.

### Initialisation et configuration de base
Créez un dossier d'index et instanciez l'objet `Index` :

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Comment créer une requête booléenne java ?
La classe `Index` représente une collection de documents recherchables stockée sur disque. Un `BooleanQuery` combine plusieurs sous‑requêtes avec des opérateurs logiques. `createAndQuery`, `createOrQuery` et `createNotQuery` construisent respectivement des sous‑requêtes AND, OR et NOT. Chargez ou créez une instance `Index`, ajoutez des documents, puis construisez un objet `BooleanQuery` en utilisant `createAndQuery`, `createOrQuery` ou `createNotQuery`. Appelez `index.search(query)` pour récupérer les documents correspondants. Ce modèle fonctionne aussi bien pour des scénarios simples que complexes et ne nécessite que trois étapes logiques : initialisation de l'index, ajout de documents et exécution de la requête.

## Recherche booléenne AND

### Vue d'ensemble
Une requête AND restreint les résultats, améliorant la pertinence lorsque vous avez besoin de documents qui correspondent à plusieurs critères.

### Étapes de mise en œuvre

1. **Initialize Index** – cela montre également **add documents to index** pour le scénario AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Indexer les documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Effectuer une recherche de requête texte** – en utilisant la syntaxe de chaîne simple.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Effectuer une recherche d'objet** – utile lors de la construction de requêtes programmatiquement (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Recherche booléenne OR

### Vue d'ensemble
Une requête OR est idéale pour les recherches exploratoires où vous souhaitez capturer les documents contenant au moins un des plusieurs mots‑clés (**search with or java**).

### Étapes de mise en œuvre

1. **Initialiser l'index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Indexer les documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Effectuer une recherche de requête texte**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Effectuer une recherche d'objet**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Recherche booléenne NOT

### Vue d'ensemble
Une requête NOT vous aide à éliminer les documents non pertinents, comme filtrer le nom de marque d'un concurrent (**boolean search examples java**).

### Étapes de mise en œuvre

1. **Initialiser l'index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Indexer les documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Effectuer une recherche de requête texte**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Effectuer une recherche d'objet**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Requêtes booléennes complexes

### Vue d'ensemble
Les requêtes complexes vous permettent de modéliser des scénarios de recherche réels, comme « trouver des articles sportifs favorables mais exclure toute mention d'athlètes spécifiques ».

### Étapes de mise en œuvre

1. **Initialiser l'index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Indexer les documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Effectuer une recherche de requête texte**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Effectuer une recherche d'objet**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Applications pratiques des requêtes **java boolean and or**
- **Document Management Systems** – localisez les contrats qui contiennent à la fois « confidential » **AND** « renewal ».  
- **Legal Research** – filtrez la jurisprudence avec **AND**/ **OR** tout en excluant les lois obsolètes à l'aide de **NOT**.  
- **Customer Support** – récupérez les tickets qui mentionnent « login » **AND** « error » mais pas « resolved ».  
- **Content Curation** – rassemblez les articles de blog sur « cloud » **OR** « serverless » pour une newsletter.

## Pièges courants et dépannage

- **Missing Index Refresh** – après l'ajout de nouveaux documents, appelez `index.update()` pour garantir qu'ils sont recherchables.  
- **Incorrect Operator Spacing** – GroupDocs.Search attend des espaces autour des opérateurs (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – les requêtes sont insensibles à la casse par défaut, mais les analyseurs personnalisés peuvent affecter cela.  
- **Large Result Sets** – utilisez la pagination (`search(query, 0, 100)`) pour éviter la surcharge mémoire.  

## Questions fréquemment posées

**Q : Puis‑je combiner plus de deux termes dans une requête AND ?**  
R : Absolument. Vous pouvez chaîner plusieurs objets `createWordQuery` avec `createAndQuery`, ou simplement écrire `"term1 AND term2 AND term3"` dans la requête texte.

**Q : GroupDocs.Search prend‑il en charge les recherches avec joker ou floues ?**  
R : Oui. Ajoutez `*` pour le joker (par ex., `promot*`) ou utilisez `~` pour la correspondance floue (par ex., `comfort~`).

**Q : Comment limiter la recherche à des types de fichiers spécifiques ?**  
`FileTypeQuery` limite les résultats de recherche à des formats de fichiers particuliers tels que PDF ou DOCX.  
R : Utilisez la classe `FileTypeQuery` pour restreindre les résultats aux PDF, DOCX, etc., et combinez‑la avec votre requête booléenne.

**Q : Quelle est la meilleure façon de surveiller les performances d'indexation ?**  
R : Activez le logger intégré (`index.getLogger().setLevel(Level.INFO)`) et examinez les métriques de temps après chaque opération `add`.

**Q : Existe‑t‑il un moyen d'augmenter la pertinence de certains termes ?**  
`BoostQuery` augmente le score de pertinence des termes spécifiés dans une requête de recherche.  
R : Oui. Enveloppez les mots importants avec `BoostQuery` pour augmenter leur poids dans l'algorithme de notation.

---

**Dernière mise à jour :** 2026-07-21  
**Testé avec :** GroupDocs.Search 25.4 (Java)  
**Auteur :** GroupDocs

## Tutoriels associés

- [Opérateurs booléens Java – Créer un index de recherche & recherche facettée](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Maîtriser GroupDocs.Search Java : Recherche de documents efficace et gestion d'index](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Maîtriser GroupDocs.Search Java – Créer et gérer un index de recherche](/search/java/indexing/groupdocs-search-java-create-index-guide/)