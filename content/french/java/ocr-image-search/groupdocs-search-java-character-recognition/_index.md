---
date: '2026-11-02'
description: Créer un index de recherche personnalisé Java en utilisant GroupDocs.Search
  pour gérer les caractères réguliers et mélangés, optimiser la recherche d'images
  OCR et améliorer la récupération des numéros de dossiers juridiques.
keywords:
- custom search index java
- GroupDocs.Search Java
- character recognition java
- OCR search Java
- search library Java
lastmod: '2026-11-02'
og_description: Créer un index de recherche personnalisé Java en utilisant GroupDocs.Search
  pour gérer les caractères réguliers et mélangés, optimiser la recherche d'images
  OCR et améliorer la récupération des numéros de dossiers juridiques.
og_image_alt: Guide showing custom search index creation in Java with GroupDocs.Search
og_title: Créer un index de recherche personnalisé Java avec GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Create a custom search index java using GroupDocs.Search to handle
    regular and blended characters, optimize OCR image search, and improve legal case
    number retrieval.
  headline: Create a custom search index java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It means configuring an index to treat specific symbols as letters or
      blended characters, rather than ignoring them.
    question: What does “create custom search index” mean?
  - answer: GroupDocs.Search for Java (v25.4 at the time of writing).
    question: Which library is used?
  - answer: A free trial works for development; a paid license is required for production.
    question: Do I need a license?
  - answer: Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.
    question: Can I index both PDFs and images?
  - answer: Maven is the recommended way to manage dependencies, but you can also
      use Gradle or manual JARs.
    question: Is Maven required?
  type: FAQPage
tags:
- custom search index
- GroupDocs.Search
- Java OCR
- character recognition
- search library
title: Créer un index de recherche personnalisé Java avec GroupDocs.Search
type: docs
url: /fr/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Créer un index de recherche personnalisé java avec GroupDocs.Search

Dans les applications modernes très axées sur les documents, créer un **custom search index java** qui respecte les nuances de votre texte — comme les tirets, les underscores ou les symboles spécifiques à une langue — est essentiel pour une récupération rapide et précise. Ce tutoriel vous guide à travers la configuration de la reconnaissance des caractères dans **GroupDocs.Search for Java**, couvrant à la fois les caractères réguliers (lettres, chiffres, underscores) et les caractères mélangés (par ex., les tirets). À la fin, vous pourrez personnaliser un index qui répond exactement aux besoins des scénarios OCR ou de recherche d’images, que vous indexiez des numéros de dossiers juridiques, des dépôts de code source ou des PDF multilingues.

## Réponses rapides
- **What does “create custom search index” mean?** Cela signifie configurer un index pour traiter des symboles spécifiques comme des lettres ou des caractères mélangés, plutôt que de les ignorer.  
- **Quelle bibliothèque est utilisée ?** GroupDocs.Search for Java (v25.4 at the time of writing).  
- **Ai-je besoin d’une licence ?** Un essai gratuit fonctionne pour le développement ; une licence payante est requise pour la production.  
- **Puis‑je indexer à la fois les PDF et les images ?** Oui—GroupDocs.Search prend en charge l’OCR sur les images et les PDF lorsqu’il est correctement configuré.  
- **Maven est‑il requis ?** Maven est la méthode recommandée pour gérer les dépendances, mais vous pouvez également utiliser Gradle ou des JARs manuels.  

## Qu’est‑ce qu’un custom search index java ?
Le **custom search index java** est une structure de données interrogeable que vous pouvez façonner en définissant quels caractères sont traités comme des lettres, des chiffres ou des symboles mélangés. Par défaut, de nombreux symboles sont ignorés, ce qui peut entraîner des correspondances manquées pour des identifiants tels que les numéros de dossier (`2023-AB-456`) ou les extraits de code (`my_variable`). Ajuster le dictionnaire d’alphabet vous donne un contrôle complet sur la tokenisation, menant à une pertinence accrue et à une exécution de requêtes plus rapide.

## Pourquoi configurer les caractères réguliers et mélangés pour les numéros de dossiers juridiques ?
Traiter les tirets et les barres obliques comme des caractères mélangés maintient les jetons associés ensemble, évitant la division indésirable d’identifiants tels que les numéros de dossiers, les codes produit ou les chemins de fichiers. Cette configuration **optimise les performances de l’index de recherche** en réduisant la fragmentation des jetons et améliore la pertinence du contenu généré par OCR, surtout lorsqu’on travaille avec des documents juridiques qui reposent fortement sur des identifiants structurés.

## Prérequis
- **JDK 8** ou version ultérieure installé.  
- **Maven** pour la gestion des dépendances.  
- Accès à la bibliothèque **GroupDocs.Search for Java** (téléchargée via Maven ou le site officiel).  

### Bibliothèques et dépendances requises
Ajoutez le dépôt et les entrées de dépendance à votre `pom.xml` (comme indiqué ci‑dessous). Le bloc XML doit rester inchangé.

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

Vous pouvez également télécharger les derniers JAR depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
- **Free trial** – parfait pour les premières expérimentations.  
- **Temporary license** – utile pour des cycles de développement plus longs.  
- **Production license** – requise pour le déploiement commercial.  

Obtenez une licence depuis le portail officiel : [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Initialisation de base
L’extrait ci‑dessous montre le code minimal nécessaire pour créer un index vide. La classe `Index` est le composant central qui stocke et gère les données interrogeables. Conservez‑le tel quel ; nous le développerons plus tard.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Configuration de GroupDocs.Search pour Java

### Installation via Maven
La configuration Maven de la section *Prérequis* est tout ce dont vous avez besoin. Après l’avoir ajoutée, exécutez `mvn clean install` pour récupérer les binaires.

### Exigences de configuration de l’environnement
- Assurez‑vous que le **dossier d’index** et le **dossier de documents** existent sur le disque.  
- Utilisez des chemins absolus ou configurez votre IDE pour résoudre correctement les chemins relatifs.  

## Guide d’implémentation

Ci‑dessous, nous parcourons deux fonctionnalités distinctes : **caractères réguliers** et **caractères mélangés**. Chaque fonctionnalité suit le même schéma — définir les chemins, créer l’index, définir le dictionnaire de caractères, puis indexer vos documents.

### Fonctionnalité 1 – caractères réguliers

#### Vue d’ensemble
Les caractères réguliers sont traités comme des jetons indépendants. C’est idéal lorsque vous souhaitez que les chiffres, les lettres et les underscores soient recherchables exactement tels qu’ils apparaissent.

#### Implémentation étape par étape

**1️⃣ Définir les chemins**  
Spécifiez où l’index sera stocké et où se trouvent vos documents source.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Créer et configurer l’index**  
Instanciez l’index et effacez toute configuration d’alphabet pré‑existante.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Définir les caractères réguliers**  
Construisez un tableau de caractères incluant les chiffres, les lettres latines et l’underscore.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Indexer les documents**  
Ajoutez tous les fichiers du dossier source à l’index nouvellement configuré.

```java
index.add(documentFolder);
```

### Fonctionnalité 2 – caractères mélangés

#### Vue d’ensemble
Les caractères mélangés (comme les tirets) relient souvent deux mots. Les marquer comme *blended* indique au moteur de garder les jetons environnants ensemble lors de l’indexation.

#### Implémentation étape par étape

**1️⃣ Définir les chemins**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Créer et configurer l’index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Définir les caractères mélangés**  
Ici, nous indiquons au dictionnaire que le tiret doit être traité comme un caractère mélangé.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexer les documents**  

```java
index.add(documentFolder);
```

## Applications pratiques

### Cas d’utilisation 1 – gestion de documents juridiques
Les fichiers juridiques contiennent souvent des numéros de dossier comme `2023-AB-456`. En configurant les underscores et les tirets, les recherches renvoient des correspondances exactes sans diviser l’identifiant, vous aidant à **rechercher des numéros de dossiers juridiques** efficacement.

### Cas d’utilisation 2 – dépôts de code source
Les développeurs ont besoin de rechercher des extraits de code où les underscores (`my_variable`) et les tirets (`my-function`) sont significatifs. La reconnaissance personnalisée des caractères garantit que le moteur de recherche respecte ces symboles.

### Cas d’utilisation 3 – ensembles de données multilingues
Lorsque vous travaillez avec des langues qui utilisent des alphabets supplémentaires, vous pouvez **étendre le jeu de caractères Unicode** pour inclure ces plages, garantissant des résultats de recherche inter‑langues précis.

### Cas d’utilisation 4 – indexer des images PDF
Si vous indexez des PDF numérisés ou des fichiers image, la sortie OCR contient souvent des caractères mixtes. Configurer correctement les caractères réguliers et mélangés **optimise les performances de l’index de recherche** pour le contenu basé sur des images.

## Considérations de performance
- **Gestion des ressources** – surveillez l’utilisation du tas ; les grands index bénéficient des validations incrémentielles.  
- **Garbage collection** – libérez les objets `Index` une fois terminés pour permettre à la JVM de récupérer la mémoire.  
- **Optimisation de l’index** – appelez périodiquement `index.optimize()` (si disponible) pour compacter l’index et améliorer la vitesse des requêtes.  

## Conclusion
Vous savez maintenant **comment créer un custom search index java** qui distingue les caractères réguliers des caractères mélangés en utilisant GroupDocs.Search for Java. Ce contrôle granulaire vous permet de créer des solutions de recherche haute performance, compatibles OCR, adaptées aux environnements juridiques, de développement ou multilingues.

### Prochaines étapes
- Expérimentez avec des plages Unicode supplémentaires pour les alphabets non latins.  
- Combinez la configuration des caractères avec d’autres fonctionnalités de GroupDocs.Search comme le stemming ou les synonymes.  
- Exposez l’index via une API REST pour permettre aux applications front‑end d’effectuer des recherches via HTTP.  

## Questions fréquemment posées

**Q :** *Quel est le but de `CharacterType.Letter` ?*  
**R :** Il indique à l’index de traiter les caractères fournis comme des lettres régulières, de sorte qu’ils soient tokenisés séparément lors de l’indexation.

**Q :** *Puis‑je mélanger des caractères réguliers et mélangés dans le même index ?*  
**R :** Oui — il suffit d’appeler `setRange` pour chaque type ; le dictionnaire gérera les deux configurations simultanément.

**Q :** *Dois‑je reconstruire l’index après avoir modifié l’alphabet ?*  
**R :** Absolument. Les changements du dictionnaire de caractères affectent la tokenisation, il faut donc ré‑indexer les documents pour appliquer les nouvelles règles.

**Q :** *Existe‑t‑il une limite au nombre de caractères personnalisés que je peux définir ?*  
**R :** La bibliothèque prend en charge l’ensemble complet de la plage Unicode ; les performances peuvent se dégrader si vous ajoutez un ensemble extrêmement vaste, il faut donc le limiter aux caractères réellement nécessaires.

**Q :** *Comment cela affecte‑t‑il la précision de l’OCR ?*  
**R :** En alignant le jeu de caractères de l’index avec la sortie du moteur OCR, vous réduisez les faux négatifs et améliorez la pertinence globale de la recherche.

---

**Dernière mise à jour :** 2026-11-02  
**Testé avec :** GroupDocs.Search 25.4 for Java  
**Auteur :** GroupDocs

## Tutoriels associés

- [Créer et gérer l’index GroupDocs Search Java](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Créer le répertoire d’index de recherche & définir la licence – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Bibliothèque de recherche en texte complet Java – Optimiser l’index avec GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)