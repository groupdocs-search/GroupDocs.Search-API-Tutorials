---
date: '2026-03-04'
description: Apprenez à mettre en œuvre des recherches Java avec un format de date
  personnalisé grâce à GroupDocs.Search, en couvrant les requêtes de plage de dates,
  les modèles personnalisés et les conseils de performance.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: Format de date personnalisé Java | Recherche de plage de dates avec GroupDocs
type: docs
url: /fr/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Format de date personnalisé Java | Recherche de plage de dates avec GroupDocs

La recherche de documents par date est une exigence fréquente—que vous construisiez un système d’archivage, un outil de reporting financier ou un portail de gestion de contenu. Dans ce tutoriel, vous apprendrez les techniques de **custom date format java** avec GroupDocs.Search, couvrant les requêtes de plage de dates, la définition de modèles personnalisés et des conseils pour **optimiser les performances de recherche**. À la fin, vous pourrez permettre aux utilisateurs de récupérer les enregistrements qui se situent dans n’importe quel intervalle de dates, quel que soit le format utilisé.

## Réponses rapides
- **Quelle est la classe principale pour l'indexation ?** `Index` du package `com.groupdocs.search`.  
- **Comment définir un modèle de date personnalisé ?** Utilisez `DateFormat` avec des objets `DateFormatElement` et un séparateur.  
- **Puis-je rechercher avec une requête texte ?** Oui, la syntaxe `daterange(start ~~ end)` fonctionne directement dans la chaîne de requête.  
- **Quelles coordonnées Maven sont requises ?** `com.groupdocs:groupdocs-search:25.4` (ou plus récent).  
- **Ai-je besoin d'une licence pour le développement ?** Un essai gratuit ou une licence temporaire suffit pour les tests ; une licence commerciale est requise pour la production.

## Qu'est-ce que **custom date format java** ?
Un **custom date format java** indique à GroupDocs.Search comment interpréter les chaînes de date qui ne suivent pas le modèle ISO par défaut (YYYY‑MM‑DD). En définissant votre propre modèle—tel que `MM/dd/yyyy` ou `dd‑MM‑yyyy`—vous permettez au moteur de reconnaître les dates intégrées dans les documents qui utilisent des formats régionaux ou hérités.

## Pourquoi utiliser GroupDocs.Search pour les requêtes de plage de dates ?
- **Vitesse :** L'indexation intégrée rend les recherches O(log n).  
- **Flexibilité :** Prend en charge la création de requêtes basées sur du texte et sur des objets.  
- **Support multi‑format :** Gère les PDF, Word, Excel, le texte brut, et plus sans code supplémentaire.  

## Comment **rechercher des documents par date** avec GroupDocs.Search
Vous trouverez ci‑dessous un guide étape par étape qui vous accompagne dans la configuration de la bibliothèque, l'indexation des fichiers et l'exécution de recherches de plage de dates simples et avancées.

### Prérequis
- Java 8 ou version supérieure installé.  
- Maven pour la gestion des dépendances.  
- Accès à une licence GroupDocs.Search (essai ou temporaire fonctionne pour le développement).  

### Configuration de GroupDocs.Search pour Java

#### Installation avec Maven
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

#### Téléchargement direct
Alternativement, vous pouvez télécharger la dernière version directement depuis [GroupDocs.Search pour les versions Java](https://releases.groupdocs.com/search/java/).

#### Initialisation et configuration de base
Créez une instance `Index` et ajoutez vos documents :

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Fonctionnalité 1 : Création de requêtes de recherche de plage de dates

### Utilisation de la requête sous forme texte
La façon la plus simple consiste à intégrer la plage de dates directement dans la chaîne de requête :

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Explication** : La syntaxe `daterange` attend des dates au format `YYYY‑MM‑DD`. Elle renvoie tous les documents dont les dates indexées se situent dans l’intervalle.

### Utilisation d’un objet Query
Pour un contrôle programmatique et une analyse personnalisée, construisez un objet `SearchQuery` :

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Explication** : `createDateRangeQuery` vous permet de fournir des objets `java.util.Date`, vous offrant une flexibilité totale concernant les fuseaux horaires et la gestion spécifique aux paramètres régionaux.

## Fonctionnalité 2 : Spécification des modèles **custom date format java**
### Définition de formats de date personnalisés
Définissez un `DateFormat` qui correspond à la représentation de date de votre document :

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Explication** : En supprimant les formats par défaut et en ajoutant un `DateFormat` qui utilise `/` comme séparateur, le moteur comprend désormais les dates écrites sous la forme `MM/dd/yyyy`. Ceci est essentiel pour **rechercher des documents par date** dans les régions qui privilégient la notation mois‑jour‑année.

## Conseils pour **optimiser les performances de recherche**
- **Indexer de façon incrémentale** : Ajoutez de nouveaux fichiers à l’index existant au lieu de le reconstruire à partir de zéro.  
- **Élaguer les données obsolètes** : Supprimez périodiquement les documents qui ne sont plus nécessaires.  
- **Ajuster les paramètres de mémoire** : Augmentez le tas JVM (`-Xmx`) lorsque vous travaillez avec de grands index.  

## Problèmes courants et solutions
- **Erreurs d’analyse de date** : Vérifiez que les chaînes de date du document correspondent exactement au modèle personnalisé que vous avez défini.  
- **Résultats manquants** : Assurez‑vous que les champs indexés contiennent des métadonnées de date ; sinon, le moteur ne peut pas faire correspondre les requêtes de date.  
- **Exceptions d’accès à l’index** : Confirmez que le chemin `indexFolder` est accessible en écriture et n’est pas verrouillé par un autre processus.  

## Applications pratiques
1. **Systèmes d’archivage** – Récupérer des enregistrements d’une période historique spécifique.  
2. **Gestion de contenu** – Prendre en charge les formats de date régionaux comme `dd/MM/yyyy` pour les audiences européennes.  
3. **Logiciel financier** – Filtrer rapidement les transactions par trimestre fiscal ou par année.  

## Pourquoi cela importe
Mettre en œuvre la prise en charge de **custom date format java** élimine les frictions liées à la gestion de représentations de dates incohérentes à travers les documents. Cela vous permet de **gérer plusieurs formats de date** dans un seul index, garantissant que les utilisateurs finaux obtiennent des résultats précis, quel que soit le format d’origine des dates.

## Prochaines étapes
- Explorez des combinaisons de requêtes plus avancées en utilisant les opérateurs `AND`, `OR` et `NOT`.  
- Expérimentez avec des analyseurs personnalisés si vous devez indexer des métadonnées temporelles supplémentaires.  
- Consultez le guide d’optimisation des performances dans la documentation officielle pour faire évoluer votre solution à des millions de documents.  

## Questions fréquemment posées

**Q : Quelle est la différence entre les requêtes de date sous forme texte et basées sur des objets ?**  
R : La forme texte est rapide et facile mais limitée au format ISO par défaut ; les requêtes basées sur des objets vous permettent de fournir des objets `Date` et des formats personnalisés pour plus de flexibilité.

**Q : Puis‑je rechercher plusieurs plages de dates dans une seule requête ?**  
R : Oui, combinez des clauses `daterange` avec des opérateurs logiques comme `AND` ou `OR` pour créer des requêtes complexes.

**Q : Les formats de date personnalisés ralentiront-ils la recherche ?**  
R : Il y a un léger surcoût lié à l’analyse supplémentaire, mais l’impact est négligeable pour les charges de travail typiques et est compensé par les gains de précision.

**Q : GroupDocs.Search est‑il adapté aux déploiements à grande échelle ?**  
R : Absolument. Avec des stratégies d’indexation appropriées et un réglage JVM, il s’adapte à des millions de documents.

**Q : Où puis‑je trouver plus d’exemples Java ?**  
R : Explorez le [dépôt GitHub de GroupDocs](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) pour des exemples supplémentaires et des implémentations de cas d’utilisation.

---

- **Documentation** : [Documentation GroupDocs Search](https://docs.groupdocs.com/search/java/)
- **Référence API** : [Référence API GroupDocs](https://reference.groupdocs.com/search/java)
- **Téléchargement** : [Obtenez la dernière version ici](https://releases.groupdocs.com/search/java/)
- **Dépôt GitHub** : [Voir sur GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum d’assistance gratuit** : [Rejoindre la discussion](https://forum.groupdocs.com/c/search/10)
- **Licence temporaire** : [Obtenez une licence temporaire ici](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour :** 2026-03-04  
**Testé avec :** GroupDocs.Search Java 25.4  
**Auteur :** GroupDocs  

---