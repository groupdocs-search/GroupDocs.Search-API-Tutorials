---
date: '2026-02-21'
description: Aprende cómo habilitar la corrección ortográfica en Java usando GroupDocs.Search,
  agregar documentos al índice y establecer el recuento máximo de errores para una
  mejor precisión en la búsqueda.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: Cómo habilitar la ortografía en Java con GroupDocs.Search
type: docs
url: /es/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

 content.# Cómo habilitar la corrección ortográfica en Java usando GroupDocs.Search

Los resultados de búsqueda precisos son esenciales para cualquier aplicación moderna. En este tutorial aprenderá **cómo habilitar la corrección ortográfica** en Java con GroupDocs.Search, de modo que los usuarios obtengan los resultados correctos incluso cuando escriban mal las consultas. Recorreremos la creación de un índice, **agregar documentos al índice**, la configuración de opciones de ortografía y la ejecución de una búsqueda que corrige automáticamente los errores.

## Respuestas rápidas
- **¿Qué significa “how to enable spelling”?** Activa el corrector ortográfico incorporado que corrige los errores tipográficos del usuario durante una búsqueda.  
- **¿Qué biblioteca proporciona esta función?** GroupDocs.Search for Java.  
- **¿Necesito una licencia?** Una licencia de prueba gratuita funciona para evaluación; se requiere una licencia completa para producción.  
- **¿Puedo controlar la tolerancia?** Sí – use `setMaxMistakeCount` para definir cuántos errores tipográficos se permiten.  
- **¿Es adecuado para índices grandes?** Absolutamente – el motor está optimizado para indexación y búsqueda de alto rendimiento.

## Qué es “how to enable spelling” en GroupDocs.Search?
Habilitar la ortografía indica al motor de búsqueda que busque los términos correctos más cercanos cuando una consulta contiene errores. Esta función mejora drásticamente la experiencia del usuario al devolver resultados relevantes incluso con entradas mal escritas.

## ¿Por qué habilitar la corrección ortográfica en aplicaciones Java?
- **Aumenta la satisfacción del usuario** – los usuarios no necesitan escribir perfectamente.  
- **Reduce la tasa de rebote** – resultados más precisos mantienen a los visitantes comprometidos.  
- **Funciona en varios dominios** – desde catálogos de bibliotecas hasta búsquedas de productos en e‑commerce.

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
Alternativamente, descargue la última versión desde [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtención de la licencia
Obtenga una licencia de prueba gratuita para evaluación. Para uso en producción, compre una licencia completa o solicite una clave temporal en el sitio oficial.

## Cómo agregar documentos al índice
Crear un índice es la base de cualquier aplicación con búsqueda habilitada. A continuación se muestra un ejemplo mínimo que **agrega documentos al índice** desde una carpeta.

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

*Consejo:* Verifique que las rutas sean correctas y que la aplicación tenga permisos de escritura en la carpeta del índice.

## Cómo configurar la corrección ortográfica (establecer el recuento máximo de errores)
Puede afinar el corrector ortográfico habilitándolo y estableciendo la tolerancia a los errores.

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

*Por qué `setMaxMistakeCount` es importante:* Define cuántos errores tipográficos tolerará el motor. Ajuste este valor según los patrones típicos de errores de su dominio.

## Cómo realizar una búsqueda con corrección ortográfica
Con el índice listo y las opciones de ortografía configuradas, ejecute una consulta que pueda contener errores.

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

La llamada `search()` devuelve un `SearchResult` que contiene los términos corregidos y los documentos más relevantes.

## Aplicaciones prácticas
1. **Sistemas de bibliotecas:** Corrija títulos de libros o nombres de autores escritos incorrectamente.  
2. **Plataformas de e‑commerce:** Corrija los errores tipográficos de los usuarios en búsquedas de productos para aumentar las conversiones.  
3. **Sistemas de gestión de contenidos:** Mejore la recuperación de artículos para el personal editorial.

## Consideraciones de rendimiento
- **Mantenga el índice actualizado** – vuelva a indexar archivos nuevos o modificados regularmente.  
- **Ajuste la configuración de memoria de la JVM** – asigne suficiente heap para índices grandes.  
- **Monitoree el uso de recursos** – ajuste los flags del recolector de basura si es necesario.

## Problemas comunes y solución de problemas
| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| No results returned after enabling spelling | Index folder path is wrong or empty | Verify `indexFolder` points to a valid index and that `index.add()` succeeded |
| Spell‑checker does not correct obvious typos | `setMaxMistakeCount` is set too low | Increase the count to 2 or 3 for more tolerant correction |
| Application crashes on large document sets | Insufficient JVM heap | Increase `-Xmx` option (e.g., `-Xmx4g`) |

## Preguntas frecuentes

**Q: ¿Qué es GroupDocs.Search?**  
A: Es una biblioteca Java que ofrece indexación rápida, funciones de búsqueda avanzadas y corrección ortográfica incorporada.

**Q: ¿Cómo obtengo una licencia para GroupDocs.Search?**  
A: Visite el sitio oficial para descargar una prueba gratuita o comprar una licencia completa.

**Q: ¿Puedo integrar GroupDocs.Search con otros frameworks Java?**  
A: Sí, funciona con Spring, Jakarta EE y cualquier aplicación Java estándar.

**Q: ¿Cuáles son los problemas comunes al configurar un índice?**  
A: Rutas de carpeta incorrectas, permisos de archivo insuficientes o dependencias faltantes en `pom.xml`.

**Q: ¿Cómo mejora la corrección ortográfica los resultados de búsqueda?**  
A: Reescribe automáticamente las consultas mal escritas a sus términos correctos más cercanos, devolviendo resultados más relevantes.

## Recursos adicionales
- [Documentación](https://docs.groupdocs.com/search/java/)
- [Referencia de API](https://reference.groupdocs.com/search/java)
- [Descarga](https://releases.groupdocs.com/search/java/)
- [Repositorio GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/search/10)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2026-02-21  
**Probado con:** GroupDocs.Search 25.4  
**Autor:** GroupDocs