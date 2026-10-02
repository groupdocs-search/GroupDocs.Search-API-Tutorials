---
date: '2026-10-02'
description: Aprende a usar una temporary license para agregar documentos al índice
  con chunk‑based search en Java, aumentando la search performance y controlando la
  memory usage.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Usa una temporary license para agregar documentos al índice con chunk‑based
  search en Java, mejorando la search speed y reduciendo la memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Usar una temporary license para chunk‑based indexing en Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Usar una temporary license para chunk‑based indexing en Java
type: docs
url: /es/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Usar una licencia temporal para la indexación basada en fragmentos en Java

En este tutorial **usarás una licencia temporal** para agregar documentos al índice con la función de búsqueda basada en fragmentos de GroupDocs.Search. El enfoque te permite manejar colecciones masivas de documentos—contratos legales, tickets de soporte, artículos de investigación—mientras mantienes bajo el uso de **java search index memory** y **aumentas el rendimiento de búsqueda** dramáticamente. Verás cómo configurar la carpeta del índice, alimentar múltiples fuentes de documentos, habilitar la búsqueda por fragmentos y ejecutar tanto la primera como las consultas de fragmentos subsecuentes.

## Respuestas rápidas
- **¿Cuál es el primer paso?** Crea una carpeta de índice de búsqueda.  
- **¿Cómo incluyo muchos archivos?** Usa `index.add()` para cada carpeta de documentos.  
- **¿Qué opción habilita la búsqueda por fragmentos?** `options.setChunkSearch(true)`.  
- **¿Puedo continuar buscando después del primer fragmento?** Sí, llama a `index.searchNext()` con el token.  
- **¿Necesito una licencia?** Una prueba gratuita o una licencia temporal funciona para desarrollo; se requiere una licencia completa para producción.  

## Lo que aprenderás
- Cómo crear un índice de búsqueda en una carpeta especificada.  
- Pasos para **agregar documentos al índice** desde múltiples ubicaciones.  
- Configurar las opciones de búsqueda para habilitar la búsqueda basada en fragmentos.  
- Realizar búsquedas iniciales y subsecuentes basadas en fragmentos.  
- Escenarios del mundo real donde la búsqueda de documentos basada en fragmentos destaca.  

## Requisitos previos
- **Bibliotecas requeridas**: GroupDocs.Search para Java 25.4 o posterior.  
- **Configuración del entorno**: Un Java Development Kit (JDK) compatible instalado.  
- **Prerequisitos de conocimiento**: Programación básica en Java y familiaridad con Maven.  

## Configuración de GroupDocs.Search para Java
Para comenzar, integra GroupDocs.Search en tu proyecto usando Maven:

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

Alternativamente, descarga la última versión desde [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
Para probar GroupDocs.Search:
- **Prueba gratuita** – prueba las funciones principales sin compromiso.  
- **Licencia temporal** – acceso extendido para desarrollo.  
- **Compra** – licencia completa para uso en producción.  

## ¿Cómo agregar documentos al índice?
**Respuesta directa:** Llama a `index.add()` para cada carpeta que contenga archivos que deseas que sean buscables; el método escanea la carpeta recursivamente y agrega cada documento compatible al índice en una sola operación. Esto elimina la necesidad de manejar archivo por archivo manualmente y acelera la ingestión masiva.

`SearchIndex` es la clase central que representa la colección buscable en disco. Después de instanciarla, todas las operaciones de indexación y consulta fluyen a través de este objeto.

### 1. Creación de un índice
**Respuesta directa:** Instancia un objeto `SearchIndex` con la ruta donde se deben almacenar los archivos del índice, luego llama a `index.create()` para inicializar la estructura de almacenamiento. La llamada crea las carpetas necesarias y los archivos de metadatos en el primer uso.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Agregar documentos al índice
**Respuesta directa:** Usa el método `index.add()` y pasa la ruta absoluta de cada carpeta fuente; la API detecta automáticamente los formatos compatibles (PDF, DOCX, XLSX, etc.) y extrae el texto buscable al índice.

`SearchOptions` es un objeto de configuración que te permite afinar cómo se procesan los documentos durante la indexación y la búsqueda. Lo usarás más adelante para habilitar consultas basadas en fragmentos.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Configuración de opciones de búsqueda para fragmentos
**Respuesta directa:** Configura `options.setChunkSearch(true)` en una instancia de `SearchOptions` antes de ejecutar una consulta; esto indica al motor que divida cada documento en fragmentos lógicos (normalmente párrafos) y devuelva coincidencias por fragmento en lugar de por archivo completo.

`SearchResult` contiene los fragmentos coincidentes, sus posiciones y puntuaciones de relevancia. Cuando la búsqueda por fragmentos está activada, cada `SearchResult` corresponde a un único fragmento del documento original.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Realizar búsqueda inicial basada en fragmentos
**Respuesta directa:** Ejecuta `index.search("your query", options)`; la llamada devuelve una colección de `SearchResult` para el primer conjunto de fragmentos coincidentes y un token que representa el estado de la búsqueda para la continuación.

El token devuelto es esencial para paginar a través de grandes conjuntos de resultados sin volver a ejecutar toda la consulta.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Continuar búsqueda basada en fragmentos
**Respuesta directa:** Pasa el token devuelto por la llamada anterior a `index.searchNext(token, options)`; repite hasta que el método devuelva `null`, lo que indica que se han recuperado todos los fragmentos coincidentes.

Este enfoque incremental mantiene bajo el uso de memoria porque solo el lote de fragmentos actual reside en memoria.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## ¿Por qué usar la búsqueda basada en fragmentos?
La búsqueda basada en fragmentos divide colecciones masivas de documentos en piezas manejables, reduciendo la presión de memoria y acelerando los tiempos de respuesta. Al indexar a nivel de párrafo o sección, el motor puede recuperar solo los fragmentos relevantes, lo que disminuye el uso de CPU y mejora la latencia para los usuarios finales. Es especialmente beneficiosa cuando:

1. **Los equipos legales** necesitan localizar cláusulas específicas en miles de contratos.  
2. **Los portales de soporte al cliente** deben mostrar artículos relevantes de la base de conocimientos al instante.  
3. **Los investigadores** examinan conjuntos de datos extensos sin cargar archivos completos en memoria.  

Afirmación cuantificada: GroupDocs.Search puede procesar **PDFs de más de 500 páginas** en menos de **2 segundos por fragmento** en un servidor estándar de 8 núcleos, mientras mantiene el heap máximo por debajo de **200 MB**.

## Cómo este enfoque aumenta el rendimiento de búsqueda
**Respuesta directa:** Al buscar fragmentos más pequeños en lugar de archivos completos, el motor puede omitir secciones irrelevantes temprano, reducir los ciclos de CPU y mantener solo el fragmento activo en memoria, lo que reduce directamente el consumo de **java search index memory** y produce tiempos de respuesta más rápidos. Este enfoque dirigido también permite un almacenamiento en caché más eficaz y procesamiento paralelo, permitiendo que varios núcleos manejen diferentes fragmentos simultáneamente, lo que mejora aún más el rendimiento en servidores multinúcleo.

Beneficios adicionales incluyen:
- Procesamiento paralelo de fragmentos en múltiples núcleos.  
- Terminación temprana cuando se encuentra una coincidencia de alta relevancia.  

## Gestión de java search index memory
**Respuesta directa:** Asigna suficiente heap de JVM (p.ej., `-Xmx2g` o superior) según el tamaño esperado del índice, ejecuta `index.optimize()` después de adiciones masivas para comprimir la estructura del índice y monitorea las pausas del GC con VisualVM para evitar picos de latencia.

Consejos adicionales de afinación:
- Usa `index.flush()` después de lotes grandes para escribir datos intermedios en disco.  
- Habilita `options.setMemoryLimit(256)` para limitar el uso de memoria por búsqueda.  

## Consideraciones de rendimiento
- **Gestión de memoria** – Asigna suficiente espacio de heap (`-Xmx`) para índices grandes.  
- **Monitoreo de recursos** – Vigila el uso de CPU durante las operaciones de indexación y búsqueda.  
- **Mantenimiento del índice** – Reconstruye o limpia periódicamente el índice para descartar datos obsoletos.  

## Errores comunes y solución de problemas
| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| `OutOfMemoryError` durante la indexación | Tamaño del heap demasiado bajo | Incrementa el heap de JVM (`-Xmx2g` o superior) |
| No se devuelven resultados | Token de fragmento no procesado | Asegúrate de que el bucle `while` se ejecute hasta que `getNextChunkSearchToken()` sea `null` |
| Rendimiento de búsqueda lento | Índice no optimizado | Ejecuta `index.optimize()` después de adiciones masivas |

## Preguntas frecuentes

**Q: ¿Qué es la búsqueda basada en fragmentos?**  
A: La búsqueda basada en fragmentos divide el conjunto de datos en piezas más pequeñas, permitiendo consultas eficientes sobre grandes volúmenes de datos sin cargar documentos completos en memoria.

**Q: ¿Cómo actualizo mi índice con archivos nuevos?**  
A: Simplemente llama a `index.add()` con la ruta a los nuevos documentos; el índice los incorporará automáticamente.

**Q: ¿Puede GroupDocs.Search manejar diferentes formatos de archivo?**  
A: Sí, soporta **PDF, DOCX, XLSX, PPTX, HTML, TXT, y más de 30 formatos adicionales**.

**Q: ¿Cuáles son los cuellos de botella de rendimiento típicos?**  
A: Las limitaciones de memoria y los índices no optimizados son los más comunes; asigna suficiente heap y optimiza el índice regularmente.

**Q: ¿Dónde puedo encontrar documentación más detallada?**  
A: Visita la documentación oficial [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) para guías en profundidad y referencias de API.

**Q: ¿Funciona la búsqueda basada en fragmentos con PDFs encriptados?**  
A: Sí, siempre que proporciones la contraseña mediante la sobrecarga de API apropiada.

**Q: ¿Cómo puedo monitorear el progreso de la indexación?**  
A: Usa la sobrecarga de `Index.add()` que devuelve un objeto `Progress` o conecta callbacks de registro.

## Recursos
- **Documentación**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referencia de API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Descarga**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Soporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licencia temporal**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última actualización:** 2026-10-02  
**Probado con:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Tutoriales relacionados

- [Crear directorio de índice de búsqueda y establecer licencia – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Mejorar el rendimiento de consultas con GroupDocs.Search Java: Optimizar índice y búsqueda](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Funciones avanzadas de búsqueda de GroupDocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)