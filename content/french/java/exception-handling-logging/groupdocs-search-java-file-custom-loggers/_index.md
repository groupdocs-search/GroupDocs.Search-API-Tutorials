---
date: '2026-02-24'
description: Apprenez à créer un logger personnalisé, à définir la taille maximale
  du journal et à configurer le logger console ou fichier dans GroupDocs.Search pour
  Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Comment créer un logger personnalisé et limiter la taille du fichier journal
  avec GroupDocs.Search Java
type: docs
url: /fr/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

 URLs unchanged.

Then "---" line.

Then "**Last Updated:** 2026-02-24" keep date.

"**Tested With:** GroupDocs.Search for Java 25.4" keep.

"**Author:** GroupDocs" keep.

Now ensure we keep markdown formatting exactly.

Also note "For French, ensure proper RTL formatting if needed" - not needed.

Now produce final content.

Let's craft translation.

Be careful to keep bold formatting **text**.

Also keep code placeholders unchanged.

Now produce final answer.# Limiter la taille du fichier journal avec les loggers GroupDocs.Search Java

Dans ce guide, vous allez **créer des implémentations de logger personnalisés** et apprendre comment **limiter la taille du fichier journal** tout en utilisant GroupDocs.Search pour Java. Contrôler la croissance des journaux est crucial pour l'indexation de documents à grande échelle, et les loggers intégrés vous permettent de **définir la taille maximale du journal**, **faire rouler le fichier journal**, ou de passer à un **logger console** pour un retour instantané. Parcourons la configuration complète, de la configuration Maven à l'exécution d'une requête de recherche, et voyons comment **ajouter des documents à l'index** avec le logger en place.

## Réponses rapides
- **What does “limit log file size” mean?** : Cela limite la taille maximale d’un fichier journal, empêchant une croissance incontrôlée sur le disque.  
- **Which logger lets you limit log file size?** : Le `FileLogger` intégré accepte un paramètre de taille maximale.  
- **How do I use console logger java?** : Instanciez `ConsoleLogger` et affectez‑le à `IndexSettings`.  
- **Do I need a license for GroupDocs.Search?** : Un essai fonctionne pour l’évaluation ; une licence commerciale est requise pour la production.  
- **What’s the first step?** : Ajoutez la dépendance GroupDocs.Search à votre projet Maven.  

## Qu’est‑ce que la limitation de la taille du fichier journal ?
Limiter la taille du fichier journal consiste à configurer le logger de sorte que, une fois le fichier atteint un seuil prédéfini (par ex., 4 Mo), il cesse de croître ou effectue un roulement. Cela rend l’empreinte de stockage de votre application prévisible et évite la dégradation des performances.

## Pourquoi utiliser des loggers de fichier et personnalisés avec GroupDocs.Search ?
- **Auditabilité :** Conservez un enregistrement permanent des événements d’indexation et de recherche.  
- **Débogage :** Identifiez rapidement les problèmes en consultant des journaux concis.  
- **Flexibilité :** Choisissez entre des journaux persistants sur fichier et une sortie instantanée sur console (`use console logger`).  

## Prérequis
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 ou supérieur, IDE (IntelliJ IDEA, Eclipse, etc.).  
- Connaissances de base en Java et Maven.  

## Configuration de GroupDocs.Search pour Java

Ajoutez la bibliothèque à votre projet en utilisant l’une des méthodes ci‑dessous.

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
Téléchargez le dernier JAR depuis le site officiel : [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
Obtenez un essai ou achetez une licence via la [licensing page](https://purchase.groupdocs.com/temporary-license/).

## Comment créer un logger personnalisé pour GroupDocs.Search
GroupDocs.Search vous permet d’intégrer n’importe quelle implémentation de l’interface `ILogger`. En étendant `FileLogger` ou `ConsoleLogger`, vous pouvez ajouter un comportement supplémentaire — tel que le roulement du fichier journal ou le transfert des messages vers un service de surveillance distant. Cette flexibilité explique pourquoi de nombreuses équipes **créent des solutions de logger personnalisées** qui répondent à leurs besoins opérationnels.

## Comment limiter la taille du fichier journal avec le File Logger
Ci‑dessous, un guide étape par étape montrant comment **configurer le file logger** afin que le fichier journal ne dépasse jamais la taille que vous spécifiez.

### 1️⃣ Importer les packages nécessaires
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Configurer les paramètres d'index avec le File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Créer ou charger l'index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Ajouter des documents à l'index
```java
index.add(documentsFolder);
```

### 5️⃣ Exécuter une requête de recherche
```java
SearchResult result = index.search(query);
```

**Key point:** Le deuxième argument du constructeur `FileLogger` (`4.0`) définit le **set max log size** en mégaoctets, répondant directement à l’exigence de **limit log file size**.

## Comment utiliser le console logger java
Si vous préférez un retour immédiat dans le terminal, remplacez le file logger par un console logger.

### 1️⃣ Importer le Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Configurer les paramètres d'index avec le Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Créer ou charger l'index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Ajouter des documents et exécuter une recherche
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** Le console logger est idéal pendant le développement car il imprime chaque entrée de journal instantanément, vous aidant à vérifier que l’indexation et la recherche se comportent comme prévu.

## Applications pratiques
1. **Systèmes de gestion de documents :** Conservez des pistes d’audit pour chaque document indexé.  
2. **Moteurs de recherche d’entreprise :** Surveillez les performances des requêtes et les taux d’erreur en temps réel.  
3. **Logiciels juridiques et de conformité :** Enregistrez les termes de recherche pour les rapports réglementaires.

## Considérations de performance
- **Log Size :** En **set max log size**, vous évitez une utilisation excessive du disque qui pourrait ralentir votre application.  
- **Asynchronous Logging :** Si vous avez besoin d’un débit plus élevé, envisagez d’envelopper le logger dans une file d’attente asynchrone (hors du cadre de ce guide).  
- **Memory Management :** Libérez les gros objets `Index` lorsqu’ils ne sont plus nécessaires afin de garder une empreinte JVM faible.

## Problèmes courants et solutions
- **Log path not accessible :** Vérifiez que le répertoire existe et que l’application dispose des droits d’écriture.  
- **Logger not firing :** Assurez‑vous d’appeler `settings.setLogger(...)` *avant* de créer l’objet `Index`.  
- **Console output missing :** Confirmez que vous exécutez l’application dans un terminal qui affiche `System.out`.

## Questions fréquemment posées

**Q : What does the second parameter of `FileLogger` control?**  
R : Il définit la taille maximale du fichier journal en mégaoctets, vous permettant de **set max log size**.

**Q : Can I combine file and console loggers?**  
R : Oui, en créant un logger personnalisé qui transmet les messages aux deux destinations.

**Q : How do I add documents to index after the initial creation?**  
R : Appelez `index.add(pathToNewDocs)` à tout moment ; le logger enregistrera l’opération.

**Q : Is `ConsoleLogger` thread‑safe?**  
R : Il écrit directement sur `System.out`, qui est synchronisé par la JVM, ce qui le rend sûr pour la plupart des cas d’utilisation.

**Q : Will limiting the log file size affect the amount of information stored?**  
R : Une fois la limite atteinte, les nouvelles entrées peuvent être rejetées ou le fichier peut **roll over log file**, selon l’implémentation du logger.

## Ressources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Last Updated:** 2026-02-24  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs