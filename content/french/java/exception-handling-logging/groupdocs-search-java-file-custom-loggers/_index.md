---
date: '2026-09-21'
description: Apprenez à créer un logger, définir la taille maximale du journal et
  utiliser le logger console dans GroupDocs.Search pour Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Apprenez à créer un logger, définir la taille maximale du journal
  et utiliser le logger console dans GroupDocs.Search pour Java. Suivez des instructions
  étape par étape et des conseils de bonnes pratiques.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Comment créer un logger et limiter la taille du journal dans GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Comment créer un logger et limiter la taille du journal dans GroupDocs.Search
  pour Java
type: docs
url: /fr/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Comment créer un logger et limiter la taille du fichier journal dans GroupDocs.Search pour Java

Dans ce tutoriel, vous apprendrez **comment créer un logger** pour GroupDocs.Search, configurer une taille maximale de fichier journal et basculer entre la journalisation basée sur fichier et la console. Une bonne gestion des journaux empêche les disques de se remplir lors de gros travaux d'indexation, améliore le dépannage et vous fournit un retour instantané pendant le développement. Nous commencerons par la configuration Maven, parcourrons la configuration du logger, et terminerons par une requête de recherche simple qui montre le logger en action.

## Réponses rapides
- **Que signifie « limiter la taille du fichier journal » ?** Cela limite la taille maximale d'un fichier journal, empêchant une croissance incontrôlée sur le disque.  
- **Quel logger vous permet de limiter la taille du fichier journal ?** Le `FileLogger` intégré accepte un paramètre de taille maximale.  
- **Comment utiliser le logger console en Java ?** Instanciez `ConsoleLogger` et définissez-le sur `IndexSettings`.  
- **Ai-je besoin d'une licence pour GroupDocs.Search ?** Un essai fonctionne pour l'évaluation ; une licence commerciale est requise pour la production.  
- **Quelle est la première étape ?** Ajoutez la dépendance GroupDocs.Search à votre projet Maven.  

## Qu'est-ce que la limitation de la taille du fichier journal ?
Le paramètre **limit log file size** indique au logger d'arrêter d'écrire de nouvelles entrées une fois que le fichier atteint un seuil défini (par exemple, 4 Mo). Lorsque la limite est atteinte, le logger soit supprime les messages supplémentaires, soit passe à un nouveau fichier, maintenant ainsi une utilisation du disque prévisible.

## Pourquoi utiliser des loggers fichier et personnalisés avec GroupDocs.Search ?
Les loggers fichier et personnalisés vous offrent traçabilité, visibilité de débogage et flexibilité. En environnements de production, les journaux fichier fournissent un enregistrement permanent de chaque opération d'indexation et de recherche, tandis que les journaux console offrent un retour instantané pendant le développement. Ces journaux aident les équipes à surveiller les performances, à tracer les erreurs et à satisfaire les exigences de conformité en préservant une trace détaillée des activités.

## Prérequis
- GroupDocs.Search pour Java ≥ 25.4.  
- JDK 8 ou plus récent, avec un IDE tel qu'IntelliJ IDEA ou Eclipse.  
- Familiarité de base avec Maven et la programmation Java.  

## Configuration de GroupDocs.Search pour Java

Ajoutez la bibliothèque à votre projet en utilisant l'une des méthodes ci‑dessous.

**Configuration Maven :**  

```text
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
```

**Téléchargement direct :**  
Téléchargez le dernier JAR depuis le site officiel : [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtention de licence
Obtenez un essai ou achetez une licence via la [page de licence](https://purchase.groupdocs.com/temporary-license/).

## Comment créer un logger personnalisé pour GroupDocs.Search
Créer un logger personnalisé est simple car GroupDocs.Search repose sur l'interface `ILogger`. En implémentant cette interface — ou en étendant les classes fournies `FileLogger` ou `ConsoleLogger` — vous pouvez injecter un comportement supplémentaire tel que le transfert à distance ou la rotation des journaux. Vous pouvez également ajouter une logique d'initialisation, comme l'ouverture de connexions réseau, et vous assurer que les ressources sont fermées dans la méthode d'arrêt du logger. Cette approche vous permet d'intégrer des plateformes de surveillance comme ELK ou Splunk.

### Ancre de définition
`ILogger` est le contrat de base de la journalisation dans GroupDocs.Search ; toute classe qui implémente sa méthode `log(Level, String)` peut devenir un logger.

### Exemple d'approche (sans bloc de code)
1. Créez une classe qui implémente `ILogger`.  
2. Surchargez la méthode `log` pour écrire les messages vers la destination de votre choix (fichier, base de données, point de terminaison HTTP).  
3. Dans la configuration de l'index, appelez `settings.setLogger(new YourCustomLogger())`.  

## Comment limiter la taille du fichier journal avec le File Logger
La classe `FileLogger` écrit les entrées du journal dans un fichier sur le disque et accepte un argument de taille maximale. En spécifiant la limite de taille, le logger arrête automatiquement d'ajouter de nouvelles entrées ou crée un nouveau fichier lorsque le seuil est atteint, empêchant une croissance incontrôlée du disque. Ce comportement garantit que la journalisation n'interfère pas avec les performances d'indexation tout en conservant un enregistrement concis des événements.

### Ancre de définition
`FileLogger` est un logger intégré qui persiste les messages dans un fichier texte et prend en charge une taille de fichier maximale configurable.

### Guide étape par étape
1️⃣ **Importer les packages nécessaires**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Configurer les paramètres d'index avec File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Créer ou charger l'index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Ajouter des documents à l'index**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Exécuter une requête de recherche**  
```text
```java
SearchResult result = index.search(query);
```
```

**Point clé :** Le deuxième argument du constructeur `FileLogger` (`4.0`) définit le **set max log size** en mégaoctets, répondant directement à l'exigence de **limit log file size**.

## Comment utiliser le console logger en Java
Lorsque vous avez besoin d'une visibilité instantanée des événements de journalisation, le `ConsoleLogger` écrit chaque message sur `System.out`. Ce logger est léger et thread‑safe, ce qui le rend adapté aux sessions de développement et de débogage. Il fournit un retour immédiat sur la progression de l'indexation, les requêtes de recherche et les conditions d'erreur sans nécessiter d'opérations d'E/S sur fichier, ce qui peut accélérer les tests itératifs.

### Ancre de définition
`ConsoleLogger` est un logger léger qui écrit les entrées du journal sur le flux console standard, le rendant idéal pour les sessions de débogage.

### Étapes de configuration
1️⃣ **Importer le console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Configurer les paramètres d'index avec Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Créer ou charger l'index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Ajouter des documents et exécuter une recherche**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Conseil :** Le console logger est idéal pendant le développement car il imprime chaque entrée de journal instantanément, vous aidant à vérifier que l'indexation et la recherche se comportent comme prévu.

## Applications pratiques
1. **Systèmes de gestion de documents :** Conservez des traces d'audit de chaque document indexé, répondant aux exigences de conformité.  
2. **Moteurs de recherche d'entreprise :** Surveillez les performances des requêtes et les taux d'erreur en temps réel, permettant des vérifications rapides de conformité aux SLA.  
3. **Logiciels juridiques et de conformité :** Enregistrez les termes de recherche et les horodatages pour les rapports réglementaires, les journaux étant conservés pendant la période de rétention imposée.

## Considérations de performance
- **Taille du journal :** En utilisant **set max log size**, vous évitez une utilisation excessive du disque qui pourrait autrement ralentir le ramasse-miettes de la JVM.  
- **Journalisation asynchrone :** Pour les scénarios à haut débit, encapsulez votre logger dans une file d'attente asynchrone afin de découpler les I/O du thread d'indexation (implémentation hors du cadre de ce guide).  
- **Gestion de la mémoire :** Libérez les gros objets `Index` avec `index.close()` lorsqu'ils ne sont plus nécessaires afin de réduire l'empreinte de la JVM.

## Problèmes courants et solutions
- **Chemin du journal inaccessible :** Vérifiez que le répertoire existe et que l'application possède les permissions d'écriture pour le compte utilisateur exécutant la JVM.  
- **Logger ne se déclenche pas :** Assurez-vous d'appeler `settings.setLogger(...)` *avant* de créer l'objet `Index` ; sinon le logger par défaut est utilisé.  
- **Sortie console manquante :** Confirmez que vous exécutez l'application dans un terminal affichant `System.out`, et qu'aucun framework de journalisation (par ex., SLF4J) n'intercepte la sortie.

## Questions fréquemment posées

**Q : Que contrôle le deuxième paramètre de `FileLogger` ?**  
R : Il définit la taille maximale du fichier journal en mégaoctets, vous permettant de **set max log size** et d'éviter une croissance incontrôlée.

**Q : Puis-je combiner les loggers fichier et console ?**  
R : Oui. Créez un logger personnalisé qui transmet chaque appel `log` à la fois à un `FileLogger` et à un `ConsoleLogger`, puis enregistrez ce logger composite avec `IndexSettings`.

**Q : Comment ajouter des documents à l'index après la création initiale ?**  
R : Appelez `index.add(pathToNewDocs)` à tout moment ; le logger configuré enregistrera automatiquement l'ajout.

**Q : `ConsoleLogger` est‑il thread‑safe ?**  
R : Il écrit directement sur `System.out`, que la JVM synchronise en interne, ce qui le rend sûr pour les cas d'utilisation multi‑thread typiques.

**Q : La limitation de la taille du fichier journal affectera‑t‑elle la quantité d'informations stockées ?**  
R : Une fois la limite de taille atteinte, les nouvelles entrées sont soit rejetées, soit le logger passe à un nouveau fichier, selon l'implémentation choisie.

## Ressources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Dernière mise à jour :** 2026-09-21  
**Testé avec :** GroupDocs.Search for Java 25.4  
**Auteur :** GroupDocs  

## Tutoriels associés

- [Comment implémenter la journalisation - Tutoriels de gestion des exceptions et de journalisation pour GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implémenter la journalisation asynchrone en Java avec GroupDocs.Search – Guide du logger personnalisé](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Créer un index de recherche Java – Tutoriels GroupDocs.Search](/search/java/indexing/)