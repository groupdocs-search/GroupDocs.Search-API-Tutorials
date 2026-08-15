---
date: '2026-08-15'
description: Aprenda cómo mejorar la latencia de búsqueda utilizando las funciones
  de indexación avanzada de GroupDocs.Search for Java, incluyendo cancelación, operaciones
  asíncronas, multihilo y personalización de metadatos.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Mejore la latencia de búsqueda con GroupDocs.Search for Java mediante
  cancelación, indexación asíncrona, multihilo y personalización de metadatos. Aumente
  el rendimiento y reduzca el uso de recursos.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Mejore la latencia de búsqueda con indexación avanzada en GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Mejore la latencia de búsqueda con indexación avanzada en GroupDocs
type: docs
url: /es/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Mejorar la latencia de búsqueda con indexación avanzada en GroupDocs

En el entorno digital de hoy, rápido, **mejorar la latencia de búsqueda** es esencial para ofrecer resultados instantáneos a los usuarios. Ya sea que estés construyendo un motor de búsqueda personalizado o mejorando un sistema de gestión de documentos existente, la estrategia de indexación adecuada puede reducir drásticamente la latencia, disminuir el consumo de recursos y **mejorar la latencia de búsqueda** en general. En este tutorial repasaremos las funciones más potentes de GroupDocs.Search para Java—cancelación, indexación asíncrona, multihilo y personalización de metadatos—para que puedas **agregar documentos al índice** más rápido y de manera más eficiente.

**Qué aprenderás**

- Cómo cancelar una operación de indexación después de un tiempo especificado  
- Realizar operaciones de indexación asíncrona y manejar cambios de estado  
- Configurar multihilo para una indexación más rápida  
- Personalizar las opciones de indexación de metadatos para **personalizar los metadatos de búsqueda**  

Asegurémonos de que tienes todo lo necesario antes de sumergirnos en el código.

## Respuestas rápidas
- **¿Qué hace la cancelación?** Detiene la indexación después de un tiempo límite establecido, liberando CPU y memoria para otras tareas.  
- **¿Puedo indexar documentos de forma asíncrona?** Sí – habilítalo con `options.setAsync(true)`.  
- **¿Cuántos hilos puedo usar?** Cualquier entero positivo; 2‑4 hilos son típicos para la mayoría de los servidores.  
- **¿La indexación de metadatos es opcional?** Absolutamente – puedes habilitarla o ajustarla por campo.  
- **¿Necesito una licencia para estas funciones?** Una prueba funciona para pruebas; se requiere una licencia completa para producción.

## Requisitos previos

- **Biblioteca GroupDocs.Search** – versión 25.4 o posterior.  
- **Entorno de desarrollo Java** – se recomienda JDK 8 o superior.  
- Familiaridad básica con Java y el concepto de indexación.

### Configuración de GroupDocs.Search para Java

#### Instalación con Maven

Agrega el repositorio y la dependencia a tu archivo `pom.xml`:

`pom.xml` configuration tells Maven which GroupDocs.Search artifacts to download and include in your project.

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

#### Descarga directa

Alternativamente, descarga el JAR más reciente desde [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Adquisición de licencia** – Comienza con una prueba gratuita o solicita una licencia temporal para desbloquear el conjunto completo de funciones.

### Inicialización y configuración básica

La clase `SearchIndex` es el punto de entrada que representa un índice buscable almacenado en disco o en memoria.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## ¿Qué significa “optimizar el rendimiento de búsqueda” en este contexto?

Optimizar el rendimiento de búsqueda significa configurar el proceso de indexación para que consuma la cantidad adecuada de CPU, memoria y tiempo mientras entrega los resultados más relevantes al instante. Al controlar la cancelación, la ejecución asíncrona, el multihilo y el manejo de metadatos, influyes directamente en la rapidez con la que el motor puede **agregar documentos al índice** y responder a las consultas.

## ¿Por qué usar funciones avanzadas de indexación?

La indexación asíncrona y multihilo mantiene tu aplicación receptiva, mientras que la cancelación evita procesos descontrolados. Las opciones de metadatos afinadas te permiten mostrar la información más importante, lo que directamente **mejora la latencia de búsqueda** para los usuarios finales. Además, estas funciones reducen los picos de CPU, disminuyen la presión de memoria y permiten una escalabilidad más fluida al manejar grandes volúmenes de documentos.

## ¿Cómo mejorar la latencia de búsqueda con indexación avanzada?

Carga tu instancia `SearchIndex`, configura `IndexingOptions` con cancelación, asincronía y ajustes de hilos, luego llama a `index.add(document)` — esta combinación reduce el tiempo total de indexación hasta en un 60 % en cargas de trabajo típicas y garantiza que los trabajos de larga duración no bloqueen otras operaciones. También puedes ajustar los límites de indexación de metadatos y monitorear el progreso mediante los eventos de cambio de estado para asegurar que la canalización se mantenga dentro de los presupuestos de rendimiento.

## Guía de implementación

### Propiedad de cancelación

**Visión general** – Cancelar la indexación después de una duración especificada para evitar el consumo excesivo de recursos.

#### Paso 1: configurar el entorno

Crea una instancia `SearchIndex` que apunte a tu carpeta de índice.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Paso 2: crear opciones de indexación con cancelación

`IndexingOptions` te permite especificar cómo se comporta el motor de indexación.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Puntos clave**

- `setCancellation()` activa la función.  
- `cancelAfter(int milliseconds)` define el tiempo de espera (3 segundos en este ejemplo).

### Propiedad asíncrona

**Visión general** – Ejecutar la indexación en un hilo en segundo plano y escuchar los cambios de estado.

#### Paso 1: configurar el entorno

Instancia el índice y prepara la colección de documentos.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Paso 2: suscribirse al evento de cambio de estado

El evento `StatusChanged` te notifica cuando el trabajo de indexación cambia de estado.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Paso 3: configurar opciones asíncronas

Habilita el modo asíncrono para que la llamada devuelva inmediatamente y el procesamiento continúe en segundo plano.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Propiedad de hilos

**Visión general** – Acelerar la indexación aprovechando múltiples núcleos de CPU.

#### Paso 1: configurar el entorno

Prepara el índice y asegura que la JVM tenga suficiente memoria heap.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Paso 2: configurar multihilo

Establece el número de hilos de trabajo; cada hilo procesa un subconjunto de documentos.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Propiedad de opciones de indexación de metadatos

**Visión general** – Ajustar finamente qué metadatos del documento se indexan y cómo se almacenan.

#### Paso 1: configurar el entorno

Carga un documento que contenga campos de metadatos como autor, título y etiquetas personalizadas.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Paso 2: configurar opciones de metadatos

`MetadataIndexingOptions` te permite habilitar o deshabilitar campos de metadatos individuales y definir límites de tamaño.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Aplicaciones prácticas

1. **Sistemas de gestión de documentos** – Usa indexación asíncrona para mantener la UI receptiva mientras se procesan grandes lotes en segundo plano.  
2. **Motores de búsqueda de contenido** – Aplica cancelación para evitar que trabajos de larga duración consuman recursos del servidor durante picos de tráfico.  
3. **Canales de ingestión a gran escala** – Aprovecha el multihilo para **agregar documentos al índice** a gran escala, reduciendo drásticamente el tiempo de procesamiento.  

## Consideraciones de rendimiento

- **Gestión de hilos** – Monitorea el uso de CPU; demasiados hilos pueden causar sobrecarga por cambios de contexto.  
- **Huella de memoria** – Los límites de metadatos (p. ej., `setMaxBytesToIndexField`) mantienen predecible el uso de memoria.  
- **Recolección de basura** – Usa banderas JVM apropiadas (`-Xmx`, `-XX:+UseG1GC`) al indexar corpora masivos.  

## Problemas comunes y soluciones

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| La indexación nunca termina | Cancelación configurada demasiado baja | Aumenta el valor de `cancelAfter` o elimina la cancelación para trabajos largos |
| No hay actualizaciones de estado en modo asíncrono | Manejador de eventos no adjuntado correctamente | Asegúrate de que `index.getEvents().StatusChanged.add(...)` se llame antes de `index.add` |
| Errores de falta de memoria | Demasiados hilos o límites de metadatos altos | Reduce `options.setThreads` y disminuye los límites de los campos de metadatos |
| Metadatos faltantes en los resultados | Indexación de metadatos deshabilitada | Verifica que `options.getMetadataIndexingOptions()` esté configurado y no se haya establecido para ignorar campos |

## Preguntas frecuentes

**P: ¿Cómo obtengo una licencia temporal para GroupDocs.Search?**  
R: Visita la [página de licencia temporal de GroupDocs](https://purchase.groupdocs.com/temporary-license/) y sigue las instrucciones en pantalla.

**P: ¿Puedo cancelar una operación de indexación a mitad de proceso?**  
R: Sí – usa la propiedad de cancelación con `cancelAfter()` o invoca `Cancellation.cancel()` programáticamente.

**P: ¿Cuáles son algunos casos de uso para la indexación asíncrona?**  
R: Recuperación de documentos en tiempo real, procesamiento por lotes en segundo plano y aplicaciones con UI receptiva se benefician de la indexación asíncrona.

**P: ¿Es seguro aumentar el número de hilos en un servidor compartido?**  
R: Aumenta gradualmente y monitorea la carga de CPU; en entornos muy compartidos, mantén el número de hilos moderado (2‑4).

**P: ¿Cómo afecta la indexación de metadatos a la relevancia de búsqueda?**  
R: Los metadatos indexados correctamente (autor, fecha de creación, etiquetas) pueden tener mayor peso en las consultas, mejorando la precisión de los resultados.

## Conclusión

Al adoptar estas funciones avanzadas de GroupDocs.Search para Java, **mejorarás la latencia de búsqueda** en una variedad de escenarios—desde la ingestión rápida de documentos hasta el control granular de metadatos. Experimenta con diferentes configuraciones, monitorea el uso de recursos y adapta los ajustes a tu carga de trabajo específica para obtener los mejores resultados.

---

**Última actualización:** 2026-08-15  
**Probado con:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Mejorar el rendimiento de consultas con GroupDocs.Search Java: Optimizar índice y búsqueda](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Cómo agregar documentos al índice con indexación de metadatos en Java usando GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Cómo agregar múltiples alias y agregar documentos al índice en GroupDocs.Search para Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)