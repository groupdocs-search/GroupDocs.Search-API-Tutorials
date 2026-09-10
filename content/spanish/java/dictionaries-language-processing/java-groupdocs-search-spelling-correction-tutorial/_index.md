---
date: '2026-09-02'
description: Aprende cómo crear search index java y habilitar la corrección ortográfica
  usando GroupDocs.Search. Sigue instrucciones paso a paso para agregar documentos,
  configurar max mistake count y mejorar la precisión de la búsqueda.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Aprende cómo crear search index java y habilitar la corrección ortográfica
  usando GroupDocs.Search. Sigue instrucciones paso a paso para agregar documentos,
  configurar max mistake count y mejorar la precisión de la búsqueda.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Cómo crear search index java y habilitar la corrección ortográfica
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Cómo crear search index java y habilitar la corrección ortográfica
type: docs
url: /es/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Cómo crear un índice de búsqueda java y habilitar la corrección ortográfica

En las aplicaciones Java modernas, ofrecer resultados de búsqueda precisos es una característica indispensable. Este tutorial muestra **cómo crear un índice de búsqueda java** y activar la corrección ortográfica con GroupDocs.Search, para que los usuarios reciban resultados relevantes incluso cuando escriben consultas con errores. Verás cómo configurar la biblioteca, agregar documentos, establecer el recuento máximo de errores y ejecutar una búsqueda tolerante a errores tipográficos, todo sin escribir una sola línea de código de configuración adicional.

## Respuestas rápidas
- **¿Qué hace “enable spelling”?** Activa el corrector ortográfico incorporado que reescribe los términos mal escritos a sus formas correctas más cercanas durante una búsqueda.  
- **¿Qué biblioteca proporciona esta función?** GroupDocs.Search for Java.  
- **¿Necesito una licencia?** Una prueba gratuita sirve para evaluación; se requiere una licencia completa para uso en producción.  
- **¿Puedo controlar la tolerancia?** Sí – use `setMaxMistakeCount` para definir cuántos errores tipográficos se permiten por consulta.  
- **¿Es adecuada para índices grandes?** Absolutamente – el motor maneja índices con millones de registros manteniendo la latencia de consulta por debajo de 100 ms en hardware de servidor típico.

## ¿Qué es GroupDocs.Search?
GroupDocs.Search es una biblioteca Java que ofrece indexación rápida de texto completo y funciones de búsqueda avanzadas, incluida la corrección ortográfica incorporada. Soporta más de 50 formatos de entrada y puede procesar documentos de cientos de páginas sin cargar todo el archivo en memoria.

## ¿Por qué habilitar la corrección ortográfica en aplicaciones Java?
- **Aumenta la satisfacción del usuario** – los visitantes obtienen resultados correctos incluso con una escritura imperfecta.  
- **Reduce la tasa de rebote** – los resultados precisos mantienen a los usuarios comprometidos por más tiempo.  
- **Funciona en todos los dominios** – desde catálogos de bibliotecas hasta búsquedas de productos en e‑commerce, la corrección ortográfica mejora la relevancia en todas partes.

## Requisitos previos
- Java Development Kit (JDK) instalado.  
- Conocimientos básicos de Java y Maven.  
- Comprensión de los conceptos de indexación.  
- Una prueba o clave licenciada de GroupDocs.Search.

### Configuración de GroupDocs.Search para Java
Integre la biblioteca en su proyecto Maven.

**Configuración de Maven**  
Agregue el repositorio y la dependencia a su archivo `pom.xml`:

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

**Descarga directa**  
Alternativamente, descargue la última versión desde [Versiones de GroupDocs.Search para Java](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
Obtenga una licencia de prueba gratuita para evaluación. Para uso en producción, adquiera una licencia completa o solicite una clave temporal en el sitio oficial.

## ¿Cómo crear un índice de búsqueda en Java?
`SearchIndex` es la clase principal que representa un índice buscable almacenado en disco.  
Cree una instancia de `SearchIndex` apuntando a una carpeta en disco, luego agregue documentos desde un directorio de origen. El motor construye un índice invertido que permite búsquedas rápidas. Puede llamar a `index.add()` para cada archivo; la biblioteca extrae texto automáticamente según el tipo de archivo.

## ¿Cómo habilitar la corrección ortográfica?
`getSpellingOptions()` devuelve el objeto de configuración de ortografía para el índice, permitiéndole habilitar o ajustar las funciones de corrección ortográfica.  
Habilite la corrección ortográfica llamando a `index.getSpellingOptions().setEnabled(true)`. Esto indica al motor que analice los términos de la consulta y sugiera alternativas corregidas cuando se detecten discrepancias. La función funciona de forma inmediata para todos los idiomas indexados que admite la biblioteca.

## ¿Qué es la configuración de recuento máximo de errores?
`setMaxMistakeCount` configura el número máximo de ediciones de caracteres que el corrector ortográfico tolerará por término.  
`setMaxMistakeCount(int)` define el número máximo de ediciones de caracteres (inserciones, eliminaciones, sustituciones) que el corrector ortográfico tolerará por término. Establecerlo en **2** permite al motor corregir errores comunes de dos caracteres mientras evita correcciones demasiado agresivas que podrían devolver resultados no relacionados.

## Cómo realizar una búsqueda con corrección ortográfica
`search()` ejecuta una consulta contra el índice y devuelve un objeto `SearchResult` que contiene coincidencias y cualquier término corregido.  
Ejecute una consulta de búsqueda usando el método `search()`. Si la consulta contiene palabras mal escritas, el motor devuelve un `SearchResult` que incluye los términos corregidos y una lista de los documentos más relevantes. Puede mostrar tanto la consulta original como la versión corregida al usuario para mayor transparencia.  
`SearchResult` contiene la lista de documentos coincidentes e información sobre las correcciones de la consulta.

## Aplicaciones prácticas
1. **Sistemas de bibliotecas** – corrige automáticamente títulos de libros o nombres de autores mal escritos.  
2. **Plataformas de e‑commerce** – corrige errores tipográficos en nombres de productos para aumentar las tasas de conversión.  
3. **Gestión de contenidos** – ayuda al personal editorial a localizar artículos incluso con palabras clave imperfectas.

## Consideraciones de rendimiento
- **Mantenga el índice actualizado** – re‑indexe archivos nuevos o modificados regularmente.  
- **Ajuste la configuración de memoria de la JVM** – asigne suficiente heap para índices grandes (p. ej., `-Xmx4g`).  
- **Monitoree el uso de recursos** – ajuste los flags del recolector de basura si observa pausas durante la indexación masiva.

## Problemas comunes y solución de problemas
| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| No hay resultados después de habilitar la corrección ortográfica | La ruta de la carpeta del índice es incorrecta o está vacía | Verifique que `indexFolder` apunte a un índice válido y que `index.add()` haya tenido éxito |
| El corrector ortográfico no corrige errores tipográficos evidentes | `setMaxMistakeCount` está configurado demasiado bajo | Aumente el recuento a 2 o 3 para una corrección más tolerante |
| La aplicación se bloquea con conjuntos de documentos grandes | Heap de JVM insuficiente | Aumente la opción `-Xmx` (p. ej., `-Xmx4g`) |

## Preguntas frecuentes

**P: ¿Qué es GroupDocs.Search?**  
R: GroupDocs.Search es una biblioteca Java que ofrece indexación rápida, capacidades avanzadas de consulta y corrección ortográfica incorporada para cualquier aplicación Java.

**P: ¿Cómo obtengo una licencia para GroupDocs.Search?**  
R: Visite el sitio oficial para descargar una prueba gratuita o comprar una licencia completa; también hay una clave temporal disponible para pruebas a corto plazo.

**P: ¿Puedo integrar GroupDocs.Search con otros frameworks Java?**  
R: Sí, funciona sin problemas con Spring, Jakarta EE y cualquier aplicación Java estándar.

**P: ¿Cuáles son los problemas comunes al configurar un índice?**  
R: Las rutas de carpeta incorrectas, permisos de archivo faltantes o dependencias Maven ausentes son los culpables típicos.

**P: ¿Cómo mejora la corrección ortográfica los resultados de búsqueda?**  
R: Reescribe automáticamente las consultas mal escritas a sus términos correctos más cercanos, devolviendo resultados más relevantes y reduciendo la frustración del usuario.

## Recursos adicionales
- [Documentación](https://docs.groupdocs.com/search/java/)
- [Referencia de API](https://reference.groupdocs.com/search/java)
- [Descarga](https://releases.groupdocs.com/search/java/)
- [Repositorio de GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/search/10)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2026-09-02  
**Probado con:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Tutoriales relacionados

- [Cómo crear un índice de documentos y agregar documentos usando la API GroupDocs.Search para Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Procesamiento de lenguaje Java – Crear diccionario de sinónimos con GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Palabras vacías en la búsqueda: agregar documentos al índice con GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)