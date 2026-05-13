---
date: '2026-01-26'
description: Aprende a buscar frases usando patrones comodín en GroupDocs.Search para
  Java. Esta guía cubre la creación de un índice de búsqueda, la adición de documentos
  al índice y la realización de búsquedas con comodines en Java.
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: Cómo buscar una frase con comodines en GroupDocs.Search Java
type: docs
url: /es/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Cómo buscar frases con comodines en GroupDocs.Search para Java

En el mundo acelerado de la gestión de documentos de hoy, **how to search phrase** de manera eficiente puede hacer o deshacer la usabilidad de una aplicación. Ya sea que estés construyendo un sistema de gestión de contenidos, un catálogo de comercio electrónico o un repositorio de documentos legales, poder localizar frases exactas—o variaciones flexibles de las mismas—es importante. En este tutorial recorreremos la configuración de **GroupDocs.Search for Java**, la creación de un índice de búsqueda, la adición de documentos al índice y el dominio tanto de búsquedas de frases simples como de potentes técnicas de búsqueda con comodines en Java.

## Respuestas rápidas
- **¿Cuál es el beneficio principal de las búsquedas de frases?** Coincidencia precisa del orden de palabras y la proximidad.  
- **¿Se pueden usar comodines dentro de una frase?** Sí, puedes combinar comodines con palabras exactas para una coincidencia flexible.  
- **¿Necesito una licencia para desarrollo?** Una prueba gratuita funciona para pruebas; se requiere una licencia completa para producción.  
- **¿Qué versión de Maven debo usar?** La última versión de GroupDocs.Search for Java (por ejemplo, 25.4 al momento de escribir).  
- **¿Este enfoque es adecuado para grandes conjuntos de documentos?** Absolutamente—solo mantén el índice optimizado y usa patrones de comodines dirigidos.

## Qué es “how to search phrase”?
Buscar una frase significa buscar una secuencia específica de palabras en un documento. Cuando añades comodines, permites que el motor de búsqueda omita o reemplace palabras, dándote la flexibilidad de coincidir variaciones sin sacrificar la relevancia.

## Por qué usar GroupDocs.Search para consultas de frases y comodines?
- **Alto rendimiento** en colecciones grandes gracias a un índice invertido optimizado.  
- **Lenguaje de consultas rico** que soporta frases exactas, comodines simples y patrones avanzados.  
- **Fácil integración** con cualquier aplicación basada en Java mediante Maven o descarga directa.  

## Requisitos previos
- Java 8 o superior instalado.  
- Maven 3 o posterior (si prefieres la gestión de dependencias con Maven).  
- Familiaridad básica con la sintaxis de Java y la estructura del proyecto.  

## Configuración de GroupDocs.Search para Java

### Usando Maven
Agrega el repositorio y la dependencia a tu archivo `pom.xml`:

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

### Descarga directa
Alternativamente, descarga el último JAR desde [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
- **Prueba gratuita:** Ideal para experimentos rápidos.  
- **Licencia temporal:** Solicítala a través del portal de GroupDocs para pruebas extendidas.  
- **Compra completa:** Recomendada para despliegues en producción.  

### Inicialización y configuración básica
Crea una carpeta para el índice e inicialízala:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

Añade los documentos que deseas que sean buscables:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## Cómo buscar frases con comodines en GroupDocs.Search
A continuación desglosamos tres escenarios progresivos: búsqueda de frase exacta, uso simple de comodines y patrones avanzados de comodines.

### Búsqueda de frase simple

#### Visión general
Utilízalo cuando necesites una coincidencia exacta de una secuencia de palabras.

##### Paso 1: Crear un índice
```java
Index index = new Index(indexFolder);
```

##### Paso 2: Añadir documentos al índice
```java
index.add(documentsFolder);
```

##### Paso 3: Buscar una frase específica (forma de texto)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Paso 4: Consultas basadas en objetos (buscar frase exacta)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Búsqueda de frase con comodines

#### Visión general
Los marcadores de posición de comodines te permiten omitir un número variable de palabras entre términos exactos.

##### Paso 1: Crear un índice
*(Igual que los pasos de Búsqueda de frase simple.)*

##### Paso 2: Añadir documentos al índice
*(Igual que arriba.)*

##### Paso 3: Búsqueda en forma de texto con comodines
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Paso 4: Consultas basadas en objetos con comodines (Wildcard Search Java)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Búsqueda avanzada de comodines

#### Visión general
Combina rangos numéricos, caracteres opcionales y patrones personalizados para coincidencias sofisticadas.

##### Paso 1: Crear un índice
*(Repetido para mayor claridad.)*

##### Paso 2: Añadir documentos al índice
*(Repetido.)*

##### Paso 3: Búsqueda en forma de texto con patrones de comodines complejos
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### Paso 4: Consultas basadas en objetos con comodines avanzados
```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Aplicaciones prácticas
- **Sistemas de gestión de contenidos:** Permiten a los editores localizar cláusulas exactas o fragmentos flexibles.  
- **Catálogos de comercio electrónico:** Permiten a los compradores encontrar productos incluso si omiten una palabra o usan sinónimos.  
- **Legal y cumplimiento:** Aísla rápidamente el lenguaje contractual que puede aparecer con pequeñas variaciones.  

## Consideraciones de rendimiento
- **Crear índice de búsqueda** solo una vez por conjunto de documentos, luego reutilízalo.  
- **Añadir documentos al índice** de forma incremental cuando llegan nuevos archivos—no reconstruyas todo el índice cada vez.  
- Usa **patrones de comodines precisos** para evitar escaneos innecesarios; los patrones más amplios aumentan la carga de CPU.  
- Llama periódicamente a `index.optimize()` (si está disponible) para mantener bajo el uso de memoria.  

## Problemas comunes y soluciones
| Problema | Solución |
|----------|----------|
| No se devuelven resultados para una consulta con comodín | Verifica la sintaxis del comodín (`*min~~max`) y asegura que las palabras existan dentro de la distancia especificada. |
| El índice se vuelve obsoleto después de actualizaciones de archivos | Vuelve a ejecutar `index.add(updatedFolder)` o usa la API de actualización incremental. |
| Alto consumo de memoria en conjuntos de datos grandes | Aumenta el tamaño del heap de JVM y considera dividir el índice en varios fragmentos. |

## Preguntas frecuentes

**Q: ¿Cuál es la diferencia entre un comodín y una búsqueda de frase?**  
A: Una búsqueda de frase busca un orden exacto de palabras, mientras que un comodín te permite reemplazar u omitir palabras dentro de ese orden.

**Q: ¿Puedo usar comodines con datos numéricos en las búsquedas?**  
A: Sí, los parámetros de rango del comodín funcionan con números así como con palabras.

**Q: ¿Cómo debo manejar colecciones de documentos muy grandes?**  
A: Mantén el índice optimizado, usa actualizaciones incrementales y diseña tus patrones de comodines para que sean lo más específicos posible.

**Q: ¿GroupDocs.Search es adecuado para escenarios de búsqueda en tiempo real?**  
A: Absolutamente—una vez que el índice está construido, las consultas se ejecutan en milisegundos, lo que lo hace apto para aplicaciones interactivas.

**Q: ¿Puedo integrar esta biblioteca en un proyecto Java existente?**  
A: Sí. Añade la dependencia Maven o el JAR, inicializa el índice como se muestra, y estarás listo para usarlo.

---

**Última actualización:** 2026-01-26  
**Probado con:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs