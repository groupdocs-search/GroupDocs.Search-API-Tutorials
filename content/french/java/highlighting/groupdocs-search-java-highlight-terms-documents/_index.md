---
date: '2025-12-26'
description: Apprenez à rechercher et à mettre en surbrillance du texte dans les documents
  en utilisant GroupDocs.Search pour Java. Découvrez les techniques de mise en surbrillance
  du document complet et des fragments.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Rechercher et mettre en surbrillance le texte avec GroupDocs.Search pour Java
type: docs
url: /fr/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Recherche et mise en surbrillance du texte dans les documents avec GroupDocs.Search pour Java

À l'ère numérique actuelle, **rechercher et mettre en surbrillance du texte** dans d'immenses collections de documents est une exigence courante. Que vous construisiez un outil de révision juridique, un portail de recherche académique ou un tableau de bord d’assistance client, pouvoir localiser instantanément et mettre en évidence les termes clés améliore considérablement l’utilisabilité. Dans ce guide complet, vous découvrirez comment implémenter **rechercher et mettre en surbrillance du texte** avec GroupDocs.Search pour Java — en couvrant à la fois la mise en surbrillance de documents entiers et la mise en surbrillance au niveau des fragments pour un contexte ciblé.

## Réponses rapides
- **Que signifie « rechercher et mettre en surbrillance du texte » ?** Il s’agit de localiser les termes de requête dans un document et de les mettre visuellement en évidence (par ex. avec une couleur d’arrière‑plan).  
- **Quelle bibliothèque fournit cette fonctionnalité ?** GroupDocs.Search pour Java.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour l’évaluation ; une licence complète est requise pour la production.  
- **Puis‑je personnaliser les couleurs de surbrillance ?** Oui — toute couleur RGB peut être définie via `HighlightOptions`.  
- **La mise en surbrillance de fragments est‑elle prise en charge ?** Absolument ; vous pouvez définir des termes avant/après la correspondance pour créer des extraits concis.

## Qu’est‑ce que la recherche et la mise en surbrillance du texte ?
La recherche et la mise en surbrillance du texte consiste à parcourir un index de documents à la recherche d’une requête donnée, à récupérer les documents correspondants, puis à marquer chaque occurrence du terme de requête dans la sortie du document (HTML, PDF, etc.). Ce repère visuel aide les utilisateurs finaux à repérer instantanément l’information pertinente.

## Pourquoi utiliser GroupDocs.Search pour Java ?
- **Indexation haute performance** avec compression configurable.  
- **API de mise en surbrillance riche** qui fonctionne sur des documents entiers et sur des fragments personnalisés.  
- **Prise en charge multi‑format** (DOCX, PDF, PPTX, TXT, et plus).  
- **Intégration Maven facile** et API claire orientée Java.

## Prérequis
- Java Development Kit (JDK) 8 ou supérieur.  
- Maven pour la gestion des dépendances.  
- Un IDE tel qu’IntelliJ IDEA ou Eclipse.  
- Familiarité de base avec la syntaxe Java.

## Configuration de GroupDocs.Search pour Java

Ajoutez le dépôt GroupDocs et la dépendance à votre `pom.xml` :

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

Vous pouvez également télécharger le JAR le plus récent directement depuis le site officiel : [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
Commencez avec un essai gratuit ou obtenez une licence temporaire pour l’évaluation. Pour les déploiements en production, achetez une licence complète afin de débloquer toutes les fonctionnalités.

## Guide d’implémentation

L’implémentation est divisée en deux sections pratiques : **mise en surbrillance dans des documents entiers** et **mise en surbrillance dans des fragments**. Les deux sections incluent les étapes essentielles pour **comment mettre en surbrillance des documents Java** à l’aide de GroupDocs.Search.

### Configuration des paramètres d’index
Avant l’indexation, configurez le stockage pour utiliser une compression élevée — cela réduit l’utilisation du disque tout en préservant la vitesse de recherche.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Mise en surbrillance dans des documents entiers

#### Étape 1 : Créer et remplir l’index
Créez un dossier d’index et ajoutez tous les fichiers sources que vous souhaitez rechercher.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Étape 2 : Effectuer la recherche et appliquer la mise en surbrillance
Recherchez le terme (par ex. `ipsum`) et générez un fichier HTML avec les correspondances mises en évidence.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Options clés expliquées**
- **Compression** — une compression élevée économise de l’espace de stockage.  
- **HighlightColor** — définissez n’importe quelle valeur RGB pour correspondre à votre palette UI.  
- **UseInlineStyles** — `false` génère un HTML propre qui peut être stylisé globalement avec du CSS.

### Mise en surbrillance dans des fragments

#### Étape 1 : Indexation et recherche (identique à ci‑dessus)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Étape 2 : Définir le contexte du fragment et la mise en surbrillance
Spécifiez le nombre de termes avant et après la correspondance qui doivent apparaître dans chaque fragment.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Étape 3 : Récupérer et écrire les fragments mis en surbrillance
Collectez les fragments générés et écrivez‑les dans un fichier HTML.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Applications pratiques
1. **Révision de documents juridiques** — mettez instantanément en surbrillance les lois, clauses ou références de jurisprudence.  
2. **Recherche académique** — faites ressortir la terminologie clé à travers des dizaines de PDF et de fichiers Word.  
3. **Assistance client** — repérez les numéros de commande ou les codes d’erreur dans les historiques de tickets.

## Considérations de performance
- **Taille de l’index** — une compression élevée (`Compression.High`) réduit l’empreinte disque.  
- **Contexte du fragment** — des valeurs plus grandes pour `termsBefore/After` augmentent la précision mais peuvent affecter la vitesse.  
- **Gestion de la mémoire** — surveillez le tas JVM lors de l’indexation de grands corpus ; envisagez une indexation incrémentale pour des ensembles très volumineux.

## Problèmes courants et solutions
- **Erreurs d’indexation** — vérifiez les chemins de fichiers et assurez‑vous que l’application dispose des permissions de lecture/écriture.  
- **Aucune mise en surbrillance affichée** — confirmez que `UseInlineStyles` correspond à votre format de sortie (HTML vs. PDF).  
- **Couleur non appliquée** — assurez‑vous que les valeurs RGB sont comprises entre 0‑255 et que le visualiseur HTML prend en charge le style.

## Questions fréquentes

**Q : Quels sont les avantages d’utiliser GroupDocs.Search pour Java ?**  
R : Il offre une indexation rapide et évolutive, une mise en surbrillance personnalisable et la prise en charge de nombreux formats de documents.

**Q : Comment intégrer GroupDocs.Search avec une API REST ?**  
R : Exposez les méthodes de recherche et de mise en surbrillance via des contrôleurs Spring Boot, en renvoyant du HTML ou du JSON.

**Q : La bibliothèque gère‑t‑elle les fichiers protégés par mot de passe ?**  
R : Oui — fournissez le mot de passe lors de l’ajout du document à l’index.

**Q : Puis‑je personnaliser le balisage de mise en surbrillance au‑delà de la couleur ?**  
R : Absolument ; vous pouvez injecter des classes CSS via `HighlightOptions` ou modifier le HTML après génération.

**Q : Quelle version a été testée pour ce guide ?**  
R : Le code a été validé avec GroupDocs.Search 25.4.

---

**Dernière mise à jour :** 2025-12-26  
**Testé avec :** GroupDocs.Search 25.4  
**Auteur :** GroupDocs