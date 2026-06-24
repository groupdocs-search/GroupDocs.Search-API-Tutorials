---
date: '2026-03-17'
description: Apprenez à créer un index avec GroupDocs.Search pour Java, à configurer
  les caractères réguliers et combinés, et à optimiser la recherche des numéros de
  dossiers juridiques et des images OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Comment créer un index avec reconnaissance de caractères en Java
type: docs
url: /fr/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

 There's "---". Keep.

Then "**Last Updated:** 2026-03-17" keep same.

"**Tested With:** GroupDocs.Search 25.4 for Java" keep.

"**Author:** GroupDocs" keep.

Then final "---".

We must ensure we keep all markdown formatting.

Now produce final content.# Comment créer un index avec reconnaissance de caractères en utilisant GroupDocs.Search pour Java

Dans les applications modernes très axées sur les documents, **how to create index** qui respecte les nuances de votre texte—comme les tirets, les soulignements ou les symboles spécifiques à une langue—est essentiel pour une récupération rapide et précise. Dans ce tutoriel, nous parcourrons la configuration de la reconnaissance de caractères dans **GroupDocs.Search for Java**, en couvrant à la fois les caractères réguliers (lettres, chiffres, soulignements) et les caractères mélangés (par ex., les tirets). À la fin, vous pourrez personnaliser un index qui répond exactement aux besoins de votre scénario OCR ou de recherche d'images, que vous indexiez des numéros de dossiers juridiques, des dépôts de code source ou des PDF multilingues.

## Réponses rapides
- **What does “create custom search index” mean?** Cela signifie configurer un index pour traiter des symboles spécifiques comme des lettres ou des caractères mélangés, plutôt que de les ignorer.  
- **Which library is used?** GroupDocs.Search for Java (v25.4 at the time of writing).  
- **Do I need a license?** Un essai gratuit suffit pour le développement ; une licence payante est requise pour la production.  
- **Can I index both PDFs and images?** Oui—GroupDocs.Search prend en charge l’OCR sur les images et les PDF lorsqu’ils sont correctement configurés.  
- **Is Maven required?** Maven est la méthode recommandée pour gérer les dépendances, mais vous pouvez également utiliser Gradle ou des JARs manuels.

## Qu'est-ce qu'un index de recherche personnalisé ?
Un index de recherche personnalisé vous permet de définir comment le moteur de recherche interprète les caractères. Par défaut, de nombreux symboles sont ignorés, ce qui peut entraîner des correspondances manquées pour des éléments tels que les numéros de dossiers (`2023-AB-456`) ou les extraits de code (`my_variable`). Ajuster le dictionnaire d’alphabet vous donne un contrôle total sur ce que le moteur considère comme texte recherché.

## Pourquoi configurer les caractères réguliers et mélangés pour les numéros de dossiers juridiques ?
- **Regular characters** (letters, digits, underscores) sont tokenisés séparément, permettant des recherches en correspondance exacte pour les identifiants.  
- **Blended characters** (hyphens, slashes) maintiennent les jetons liés ensemble, évitant la division indésirable des numéros de dossiers, des codes produit ou des chemins de fichiers.  
- Cette configuration **optimizes search index** les performances en réduisant la fragmentation des jetons et en améliorant la pertinence du contenu généré par l’OCR.

## Prérequis
- **JDK 8** ou version ultérieure installé.  
- **Maven** pour la gestion des dépendances.  
- Accès à la bibliothèque **GroupDocs.Search for Java** (téléchargée via Maven ou le site officiel).  

### Bibliothèques et dépendances requises
Ajoutez les entrées de dépôt et de dépendance à votre `pom.xml` (comme indiqué ci-dessous). Le bloc XML doit rester inchangé.

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

Vous pouvez également télécharger les derniers JARs depuis [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Acquisition de licence
- **Free Trial** – parfait pour les premières expérimentations.  
- **Temporary License** – utile pour des cycles de développement plus longs.  
- **Production License** – requise pour le déploiement commercial.  

Obtenez une licence via le portail officiel : [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Initialisation de base
L’extrait ci‑dessous montre le code minimal nécessaire pour créer un index vide. Conservez-le tel quel ; nous le développerons plus tard.

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
La configuration Maven de la section *Prerequisites* est tout ce dont vous avez besoin. Après l’avoir ajoutée, exécutez `mvn clean install` pour récupérer les binaires.

### Exigences de configuration de l’environnement
- Assurez-vous que le **index folder** et le **document folder** existent sur le disque.  
- Utilisez des chemins absolus ou configurez votre IDE pour résoudre correctement les chemins relatifs.  

## Guide d’implémentation

Ci-dessous, nous parcourons deux fonctionnalités distinctes : **regular characters** et **blended characters**. Chaque fonctionnalité suit le même schéma—définir les chemins, créer l’index, définir le dictionnaire de caractères, puis indexer vos documents.

### Fonctionnalité 1 – Caractères réguliers

#### Vue d’ensemble
Les caractères réguliers sont traités comme des jetons indépendants. C’est idéal lorsque vous souhaitez que les chiffres, lettres et soulignements soient recherchables exactement tels qu’ils apparaissent.

#### Implémentation étape par étape

**1️⃣ Set Up Paths**  
Définissez où l’index sera stocké et où se trouvent vos documents source.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
Instanciez l’index et effacez toute configuration d’alphabet pré‑existante.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
Construisez un tableau de caractères incluant les chiffres, les lettres latines et le soulignement.

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

**4️⃣ Index Documents**  
Ajoutez tous les fichiers du dossier source à l’index nouvellement configuré.

```java
index.add(documentFolder);
```

### Fonctionnalité 2 – Caractères mélangés

#### Vue d’ensemble
Les caractères mélangés (comme les tirets) relient souvent deux mots. Les marquer comme *blended* indique au moteur de garder les jetons environnants ensemble lors de l’indexation.

#### Implémentation étape par étape

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
Ici, nous indiquons au dictionnaire que le tiret doit être traité comme un caractère mélangé.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## Applications pratiques

### Cas d’utilisation 1 – Gestion de documents juridiques
Les fichiers juridiques contiennent souvent des numéros de dossiers comme `2023-AB-456`. En configurant les soulignements et les tirets, les recherches renvoient des correspondances exactes sans diviser l’identifiant, vous aidant à **search legal case numbers** efficacement.

### Cas d’utilisation 2 – Répertoires de code source
Les développeurs doivent rechercher des extraits de code où les soulignements (`my_variable`) et les tirets (`my-function`) sont significatifs. La reconnaissance de caractères personnalisée garantit que le moteur de recherche respecte ces symboles.

### Cas d’utilisation 3 – Jeux de données multilingues
Lorsque vous travaillez avec des langues qui utilisent des alphabets supplémentaires, vous pouvez **extend Unicode character set** pour inclure ces plages, garantissant des résultats de recherche inter‑langues précis.

### Cas d’utilisation 4 – Indexation d’images PDF
Si vous indexez des PDF numérisés ou des fichiers image, la sortie OCR contient souvent des caractères mixtes. Configurer correctement les caractères réguliers et mélangés **optimizes search index** les performances pour le contenu basé sur les images.

## Considérations de performance

- **Resource Management** – Surveillez l’utilisation du tas ; les gros index bénéficient des validations incrémentielles.  
- **Garbage Collection** – Libérez les objets `Index` une fois terminés pour permettre à la JVM de récupérer la mémoire.  
- **Index Optimization** – Appelez périodiquement `index.optimize()` (si disponible) pour compacter l’index et améliorer la vitesse des requêtes.  

## Conclusion

Vous savez maintenant **how to create index** qui distingue les caractères réguliers des caractères mélangés en utilisant GroupDocs.Search pour Java. Ce contrôle fin vous permet de créer des solutions de recherche haute performance, conscientes de l’OCR, adaptées aux environnements juridiques, de développement ou multilingues.

### Prochaines étapes
- Expérimentez avec des plages Unicode supplémentaires pour les alphabets non latins.  
- Combinez la configuration des caractères avec d’autres fonctionnalités de GroupDocs.Search comme le stemming ou les synonymes.  
- Intégrez l’index dans une API REST pour exposer les capacités de recherche aux applications front‑end.

## Questions fréquentes

**Q:** *Quel est le but de `CharacterType.Letter` ?*  
**A:** Il indique à l’index de traiter les caractères fournis comme des lettres régulières, de sorte qu’ils soient tokenisés séparément lors de l’indexation.

**Q:** *Puis-je mélanger des caractères réguliers et mélangés dans le même index ?*  
**A:** Oui—il suffit d’appeler `setRange` pour chaque type ; le dictionnaire gérera les deux configurations simultanément.

**Q:** *Do I need to rebuild the index after changing the alphabet?*  
**A:** Absolument. Les modifications du dictionnaire de caractères affectent la tokenisation, il faut donc ré‑indexer les documents pour appliquer les nouvelles règles.

**Q:** *Is there a limit to the number of custom characters I can define?*  
**A:** La bibliothèque prend en charge l’ensemble complet Unicode ; les performances peuvent se dégrader si vous ajoutez un ensemble extrêmement grand, il faut donc le limiter aux caractères réellement nécessaires.

**Q:** *How does this affect OCR accuracy?*  
**A:** En alignant le jeu de caractères de l’index avec la sortie du moteur OCR, vous réduisez les faux négatifs et améliorez la pertinence globale de la recherche.

---

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---