---
date: '2026-05-28'
description: Aprenda cómo buscar una frase con patrones de comodines usando GroupDocs.Search
  para Java. Incluye crear un índice de búsqueda, agregar documentos y ejecutar consultas
  de frase exacta y de comodines.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Cómo buscar una frase con comodines en GroupDocs.Search para Java
type: docs
url: /es/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Cómo buscar frases con comodines en GroupDocs.Search para Java

En aplicaciones modernas centradas en documentos, **cómo buscar una frase** rápida y precisamente es un factor decisivo para la experiencia del usuario. Ya sea que estés construyendo una base de conocimientos, un catálogo de comercio electrónico o un repositorio impulsado por cumplimiento, la capacidad de localizar una frase exacta—o una variación flexible de la misma—mantiene a los usuarios productivos y reduce la carga de soporte. Este tutorial te guía a través de la instalación de **GroupDocs.Search for Java**, la creación de un índice de búsqueda, la carga de documentos y la ejecución de consultas tanto de frase exacta como mejoradas con comodines, todo con fragmentos de código claros y listos para producción.

## Respuestas rápidas
- **¿Cuál es el beneficio principal de las búsquedas de frases?** Coincidencia precisa del orden de palabras y proximidad, garantizando que solo se devuelvan documentos que contengan la secuencia exacta.  
- **¿Se pueden usar comodines dentro de una frase?** Sí—los comodines te permiten omitir o reemplazar palabras mientras se preserva el orden general.  
- **¿Necesito una licencia para desarrollo?** Una prueba gratuita funciona para pruebas; se requiere una licencia completa para implementaciones en producción.  
- **¿Qué versión de Maven debo usar?** La última versión de GroupDocs.Search for Java (por ejemplo, 25.4 al momento de escribir).  
- **¿Es este enfoque adecuado para conjuntos de documentos grandes?** Absolutamente—GroupDocs.Search puede manejar colecciones de cientos de miles de documentos con latencia de consulta subsegundo cuando el índice está optimizado.

## ¿Qué es “cómo buscar una frase”?
**Buscar una frase significa buscar una secuencia específica de palabras en un documento.**  
Cuando ejecutas una consulta de frase, el motor verifica que las palabras aparezcan en el orden exacto y dentro de la proximidad definida, eliminando coincidencias irrelevantes que contengan las mismas palabras en un contexto diferente. Esto hace que las búsquedas de frases sean ideales para localizar cláusulas legales, códigos de producto o cualquier texto donde el orden importe.

## ¿Por qué usar GroupDocs.Search para consultas de frases y comodines?
GroupDocs.Search ofrece **indexación de alto rendimiento de hasta 1 millón de documentos manteniendo tiempos de respuesta de consulta subsegundo** en hardware de servidor típico. Su lenguaje de consultas soporta frases exactas, comodines simples `*` y `?`, y patrones avanzados como rangos numéricos (`*2~5`). La biblioteca se integra con cualquier aplicación Java mediante Maven o una descarga directa de JAR, y funciona en Java 8+ sin servicios externos.

## Requisitos previos
- Java 8 o superior (se recomienda Java 11 LTS).  
- Maven 3 o posterior (si prefieres la gestión de dependencias).  
- Familiaridad básica con la estructura de proyectos Java y conceptos orientados a objetos.  

## Configuración de GroupDocs.Search para Java

### Usando Maven
Agrega el repositorio oficial y la dependencia de GroupDocs.Search a tu `pom.xml`:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Descarga directa
Alternativamente, descarga el JAR más reciente desde la página oficial de lanzamientos: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
- **Prueba gratuita:** Ideal para experimentos rápidos; limitada a 100 MB de datos indexados.  
- **Licencia temporal:** Solicita una clave de evaluación de 30 días desde el portal de GroupDocs.  
- **Licencia completa:** Requerida para uso en producción y capacidad de indexación ilimitada.

## Inicialización y configuración básica
Crea una carpeta que contendrá los archivos de índice e instancia el objeto `Index`. La clase `Index` representa el índice buscable almacenado en disco y proporciona métodos para agregar, actualizar y consultar documentos.

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

Agrega los documentos que deseas que sean buscables:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Cómo buscar frases con comodines en GroupDocs.Search
Esta sección muestra tres niveles de búsqueda de frases—coincidencia exacta, comodín simple y patrones de comodín avanzados—demostrando cómo crear un índice, agregar documentos y ejecutar cada tipo de consulta con código Java conciso. Los ejemplos ilustran tanto consultas basadas en texto como en objetos, permitiendo a los desarrolladores integrar capacidades de búsqueda flexibles en sus aplicaciones.

### Búsqueda de frase simple

#### Visión general
Usa este enfoque cuando necesites una **coincidencia exacta** de una secuencia de palabras, como una cláusula legal o un número de modelo de producto.

#### Respuesta directa
Carga el índice, llama a `search` con una frase entre comillas (p. ej., `"quick brown fox"`), y el motor devuelve solo los documentos que contienen esa secuencia exacta, preservando el orden y el espaciado de las palabras. La consulta se ejecuta en milisegundos, incluso en índices que contienen cientos de miles de archivos.

#### Paso 1: Crear un índice
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Paso 2: Agregar documentos al índice
```java
Index index = new Index(indexFolder);
```

#### Paso 3: Buscar una frase específica (forma de texto)
```java
index.add(documentsFolder);
```

#### Paso 4: Consultas basadas en objetos (buscar frase exacta)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Búsqueda de frase con comodines

#### Visión general
Los marcadores de posición comodín (`*` para cualquier número de caracteres, `?` para un solo carácter) te permiten **omitir palabras variables** mientras se sigue imponiendo el orden circundante.

#### Respuesta directa
Inserta un token comodín (`*`) dentro de una frase entre comillas—p. ej., `"quick * fox"`—para hacer coincidir cualquier palabra(s) entre *quick* y *fox*. El motor expande el comodín en tiempo de consulta, escaneando solo los términos indexados que satisfacen el patrón, lo que mantiene el rendimiento comparable a una consulta de frase simple.

#### Paso 1: Crear un índice
*(Mismo que Búsqueda de frase simple.)*

#### Paso 2: Agregar documentos al índice
*(Mismo que arriba.)*

#### Paso 3: Búsqueda en forma de texto con comodines
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Paso 4: Consultas basadas en objetos con comodines (Búsqueda con comodines Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Búsqueda avanzada con comodines

#### Visión general
Combina rangos numéricos, caracteres opcionales y patrones tipo regex para **coincidencias sofisticadas**, como números de versión o códigos de producto.

#### Respuesta directa
Utiliza la sintaxis de comodín extendida `*min~max` para definir un rango de distancias de palabras permitidas, o `?` para coincidir un solo carácter. Por ejemplo, `"error *2~5 code"` encuentra la palabra *error* seguida de entre dos y cinco palabras y luego *code*. Esta precisión reduce falsos positivos mientras sigue ofreciendo flexibilidad.

#### Paso 1: Crear un índice
*(Repetido para mayor claridad.)*

#### Paso 2: Agregar documentos al índice
*(Repetido.)*

#### Paso 3: Búsqueda en forma de texto con patrones de comodines complejos
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Paso 4: Consultas basadas en objetos con comodines avanzados
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Aplicaciones prácticas
- **Sistemas de gestión de contenido:** Los editores pueden localizar cláusulas exactas o fragmentos flexibles sin escanear manualmente cientos de páginas.  
- **Catálogos de comercio electrónico:** Los compradores encuentran productos incluso cuando omiten un descriptor o usan sinónimos, gracias a la tolerancia de comodines.  
- **Legal y cumplimiento:** Aísla rápidamente el lenguaje contractual que puede aparecer con pequeñas variaciones en los acuerdos.  

## Consideraciones de rendimiento
- **Crear índice de búsqueda** solo una vez por conjunto de documentos estable; reutiliza la misma instancia `Index` para todas las consultas.  
- **Agregar documentos incrementalmente** cuando llegan nuevos archivos—evita reconstruir todo el índice para mantener bajo el uso de CPU.  
- **Diseñar patrones de comodines precisos**; los patrones más amplios (`*`) aumentan el número de expansiones de términos y pueden elevar la carga de CPU.  
- **Llamar a `index.optimize()`** periódicamente (si está soportado) para compactar el índice y mantener bajo el consumo de memoria.  

## Problemas comunes y soluciones

| Problema | Solución |
|----------|----------|
| No se devuelven resultados para una consulta con comodín | Verifica la sintaxis del comodín (`*min~max`) y asegura que las palabras objetivo existan dentro de la distancia definida. |
| El índice se vuelve obsoleto después de actualizaciones de archivos | Usa `index.add(updatedFolder)` o la API de actualización incremental para refrescar solo los archivos modificados. |
| Alto consumo de memoria en conjuntos de datos grandes | Aumenta el heap de JVM (`-Xmx4g` o superior) y considera dividir el índice en múltiples fragmentos para procesamiento paralelo. |

## Preguntas frecuentes

**Q: ¿Cuál es la diferencia entre un comodín y una búsqueda de frase?**  
A: Una búsqueda de frase requiere el orden exacto de palabras y el espaciado, mientras que un comodín permite reemplazar u omitir palabras dentro de ese orden, ofreciendo coincidencia flexible.

**Q: ¿Puedo usar comodines con datos numéricos en las búsquedas?**  
A: Sí—los parámetros de rango de comodín (`*min~max`) funcionan con números así como con palabras, permitiendo consultas como `"version *1~3"`.

**Q: ¿Cómo debo manejar colecciones de documentos muy grandes?**  
A: Mantén el índice optimizado, realiza actualizaciones incrementales y crea patrones de comodín específicos para limitar la expansión de términos. GroupDocs.Search puede indexar 1 millón de documentos manteniendo la latencia de consulta bajo 200 ms en hardware estándar.

**Q: ¿Es GroupDocs.Search adecuado para escenarios de búsqueda en tiempo real?**  
A: Absolutamente—una vez construido el índice, las consultas se ejecutan en milisegundos, lo que lo hace ideal para cajas de búsqueda interactivas y funciones de autocompletar.

**Q: ¿Puedo integrar esta biblioteca en un proyecto Java existente?**  
A: Sí. Añade la dependencia Maven o el JAR, instancia el `Index` como se muestra, y estarás listo para consultar sin modificar el código existente.

---

**Última actualización:** 2026-05-28  
**Probado con:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

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

## Tutoriales relacionados

- [Crear índice de búsqueda Java – Tutoriales de GroupDocs.Search](/search/java/)
- [Agregar documentos al índice – Tutoriales de GroupDocs.Search Java](/search/java/document-management/)
- [Crear índice de búsqueda - Tutoriales de GroupDocs.Search Java](/search/java/advanced-features/)