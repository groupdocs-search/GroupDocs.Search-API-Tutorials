---
date: '2026-02-21'
description: Apprenez à générer les formes singulier/pluriel en Java à l'aide de l'API
  GroupDocs.Search. Créez un fournisseur de formes de mots personnalisé pour une recherche
  et une analyse de texte précises.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Générer les formes singulier/pluriel en Java avec GroupDocs.Search
type: docs
url: /fr/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Générer des formes singulier/pluriel en Java avec GroupDocs.Search

Si vous devez **générer des formes singulier/pluriel en Java**, un fournisseur de formes de mots personnalisé est la clé pour que votre moteur de recherche ou d'analyse de texte comprenne chaque variante d'un terme. Dans ce tutoriel, nous vous guiderons dans la création d'un tel fournisseur avec l'API Java de GroupDocs.Search, afin que votre application puisse automatiquement faire correspondre « cat », « cats », « city » et « citis » sans effort supplémentaire.

## Réponses rapides
- **À quoi sert un fournisseur de formes de mots ?** Il génère des formes alternatives (singulier, pluriel, etc.) d'un mot donné afin que les recherches puissent correspondre à toutes les variantes.  
- **Quelle bibliothèque est requise ?** GroupDocs.Search pour Java (version 25.4 ou plus récente).  
- **Ai-je besoin d'une licence ?** Un essai gratuit suffit pour l'évaluation ; une licence permanente est requise pour la production.  
- **Quelle version de Java est prise en charge ?** JDK 8 ou supérieur.  
- **Combien de lignes de code sont nécessaires ?** Environ 30 lignes pour une implémentation simple du fournisseur.

## Qu'est-ce que la fonctionnalité « Create Word Forms Provider » ?
Un composant **create word forms provider** est une classe personnalisée qui implémente `IWordFormsProvider`. Elle reçoit un mot et renvoie un tableau de formes possibles — singulier, pluriel ou autres variations linguistiques — selon les règles que vous définissez. Cela permet à l'index de recherche de traiter « cat » et « cats » comme équivalents, améliorant le rappel sans sacrifier la précision.

## Pourquoi utiliser GroupDocs.Search pour la génération de formes de mots ?
- **Extensibilité intégrée :** Branchez votre propre fournisseur directement dans le pipeline d'indexation.  
- **Optimisé pour la performance :** Gère efficacement les grands index, et vous pouvez mettre en cache les résultats pour plus de rapidité.  
- **Support multi‑langage :** Les concepts s'appliquent également à .NET et à d'autres plateformes.

## Prérequis
Avant d'implémenter le **create word forms provider**, assurez‑vous d'avoir :

- **Maven** installé et un JDK 8 ou plus récent configuré sur votre machine.  
- Une familiarité de base avec le développement Java et la configuration `pom.xml` de Maven.  
- Accès à la bibliothèque GroupDocs.Search Java (version 25.4 ou ultérieure).  

## Configuration de GroupDocs.Search pour Java

### Configuration Maven

Ajoutez le dépôt et la dépendance à votre fichier `pom.xml` exactement comme indiqué ci‑dessous :

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

Sinon, téléchargez le dernier JAR depuis la page officielle des versions : [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Étapes d'obtention de licence
1. **Essai gratuit :** Inscrivez‑vous pour un essai afin d'explorer les fonctionnalités principales.  
2. **Licence temporaire :** Demandez une clé temporaire pour des tests prolongés.  
3. **Achat :** Obtenez une licence commerciale pour une utilisation en production sans restriction.

### Initialisation et configuration de base

Le fragment suivant montre comment créer un index — votre point de départ pour ajouter des documents et la logique de formes de mots :

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Guide d'implémentation

Ci‑dessous, nous parcourons les étapes pour **create word forms provider** qui gère les transformations simples du singulier au pluriel et du pluriel au singulier.

### Implémentation de SimpleWordFormsProvider

#### Vue d'ensemble
Notre fournisseur personnalisé :

- Supprime le suffixe « es » ou « s » à la fin pour deviner une forme singulière.  
- Change un « y » final en « is » pour produire une forme plurielle (par ex., « city » → « citis »).  
- Ajoute « s » et « es » pour générer des candidats pluriels de base.

#### Étape 1 – Créer le squelette de classe

Commencez par définir une classe qui implémente `IWordFormsProvider`. Conservez les instructions d'importation telles quelles :

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Étape 2 – Implémenter `getWordForms`

Ajoutez la méthode qui construit la liste des formes possibles. Ce bloc contient la logique principale ; vous pourrez l'étendre plus tard pour couvrir des règles plus complexes.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Explication de la logique
- **Singularisation :** Détecte les suffixes pluriels courants (`es`, `s`) et les supprime pour approximer le mot de base.  
- **Pluralisation :** Gère les noms se terminant par `y` en le remplaçant par `is`, une règle simple qui fonctionne pour de nombreux mots anglais.  
- **Ajout de suffixe :** Ajoute `s` et `es` pour couvrir les formes plurielles régulières qui pourraient ne pas être capturées par les vérifications précédentes.

#### Conseils de dépannage
- **Sensibilité à la casse :** La méthode utilise `toLowerCase()` pour la comparaison, garantissant que « Cats » et « cats » se comportent de la même façon.  
- **Cas limites :** Les mots plus courts que la longueur du suffixe sont ignorés afin d'éviter de renvoyer des chaînes vides.  
- **Performance :** Pour de grands vocabulaires, envisagez de mettre en cache les résultats dans un `ConcurrentHashMap`.

## Applications pratiques

Implémenter un **create word forms provider** peut améliorer plusieurs scénarios réels :

1. **Moteurs de recherche :** Les utilisateurs tapant « mouse » devraient également trouver des documents contenant « mice ». Un fournisseur peut générer de telles formes irrégulières.  
2. **Outils d'analyse de texte :** L'analyse de sentiment ou l'extraction d'entités devient plus fiable lorsque toutes les variantes d'un mot sont reconnues.  
3. **Systèmes de gestion de contenu :** La génération automatique de tags peut inclure des synonymes pluriels, améliorant le SEO et les liens internes.

## Considérations de performance

Lorsque vous intégrez le fournisseur dans un système de production, gardez ces conseils à l'esprit :

- **Mettre en cache les formes fréquemment utilisées :** Stockez les résultats en mémoire pour éviter de recomputer le même mot à plusieurs reprises.  
- **Surveiller le tas JVM :** Les grands index peuvent augmenter la pression mémoire ; ajustez `-Xmx` en conséquence.  
- **Utiliser des collections efficaces :** `ArrayList` convient aux petits ensembles, mais pour des milliers de formes, envisagez `HashSet` pour éliminer rapidement les doublons.

**Bonnes pratiques**
- Maintenez la bibliothèque à jour pour bénéficier des correctifs de performance.  
- Profiliez le fournisseur avec des charges de requêtes réalistes afin d'identifier les goulets d'étranglement tôt.  

## Conclusion

Vous avez maintenant appris comment **générer des formes singulier/pluriel en Java** en utilisant un `SimpleWordFormsProvider` personnalisé avec GroupDocs.Search. Ce composant léger peut améliorer de façon spectaculaire la pertinence des résultats de recherche et la précision de l'analyse linguistique dans de nombreuses applications.

**Prochaines étapes :**  
- Expérimentez avec des règles linguistiques plus sophistiquées (pluriels irréguliers, stemming).  
- Intégrez le fournisseur dans un pipeline d'indexation et mesurez les améliorations du rappel.  
- Explorez d'autres fonctionnalités de GroupDocs.Search telles que les dictionnaires de synonymes et les analyseurs personnalisés.

**Appel à l'action :** Essayez d'ajouter le `SimpleWordFormsProvider` à votre propre projet dès aujourd'hui et voyez comment il enrichit votre expérience de recherche !

## Section FAQ

**1. Qu’est‑ce que GroupDocs.Search pour Java ?**  
C’est une bibliothèque puissante qui offre la recherche en texte intégral, l'indexation et des fonctionnalités linguistiques — y compris la possibilité d'intégrer des fournisseurs de formes de mots personnalisés.

**2. Comment fonctionne le SimpleWordFormsProvider ?**  
Il génère des formes alternatives en appliquant des règles simples basées sur les suffixes (suppression de « s/es », conversion de « y » en « is », et ajout de « s/es »).

**3. Puis‑je personnaliser les règles de génération des formes de mots ?**  
Absolument. Modifiez la méthode `getWordForms` pour inclure des formes irrégulières, des règles spécifiques à une locale ou une intégration avec des dictionnaires externes.

**4. Quelles sont les applications courantes de cette fonctionnalité ?**  
Les moteurs de recherche, les pipelines d'analyse de texte et les plateformes CMS bénéficient de la reconnaissance des variantes singulier/pluriel.

**5. Ai‑je besoin d’une licence commerciale pour une utilisation en production ?**  
Oui — bien qu’un essai vous permette d'explorer l'API, une licence achetée supprime les limites d'utilisation et offre un support.

---  
**Dernière mise à jour :** 2026-02-21  
**Testé avec :** GroupDocs.Search 25.4 (Java)  
**Auteur :** GroupDocs  
---