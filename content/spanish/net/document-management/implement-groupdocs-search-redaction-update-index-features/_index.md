---
date: '2026-06-07'
description: Aprenda cómo actualizar el índice de manera eficiente con GroupDocs.Search
  y Redaction para .NET, mejorando su sistema de gestión de documentos.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Cómo actualizar el índice con GroupDocs.Search & Redaction (.NET)
type: docs
url: /es/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Cómo actualizar el índice con GroupDocs.Search y Redaction (.NET)

En las empresas modernas impulsadas por datos, **cómo actualizar el índice** de forma rápida y fiable puede determinar el éxito de su experiencia de búsqueda. Ya sea que maneje miles de contratos o una base de conocimientos extensa, mantener el índice de búsqueda sincronizado con los últimos cambios de documentos es esencial para obtener resultados rápidos y precisos. Este tutorial le guía a través del uso de GroupDocs.Search para .NET junto con GroupDocs.Redaction para **actualizar archivos de índice**, gestionar índices versionados y proteger contenido sensible, todo dentro de un proyecto .NET limpio.

## Respuestas rápidas
- **¿Qué significa “how to update index”?** Es el proceso de modificar un índice de búsqueda existente para que los documentos nuevos o modificados sean buscables sin reconstruirlo desde cero.  
- **¿Qué bibliotecas se requieren?** GroupDocs.Search y GroupDocs.Redaction para .NET (ambas disponibles vía NuGet).  
- **¿Necesito una licencia?** Una prueba gratuita funciona para pruebas; una licencia de producción desbloquea la funcionalidad completa.  
- **¿Puedo ejecutar esto en .NET Core?** Sí, las bibliotecas soportan .NET Framework 4.5+, .NET Core 3.1+, y .NET 5/6+.  
- **¿Qué rendimiento puedo esperar?** Actualizar un índice de 1 GB con 2 hilos finaliza en menos de un minuto en un servidor típico de 4 núcleos.

## Qué es “how to update index”?
**How to update index** se refiere a la técnica de aplicar cambios incrementales a un índice de búsqueda existente en lugar de recrearlo por completo. Este enfoque reduce el tiempo de inactividad, ahorra ciclos de CPU y mantiene sus resultados de búsqueda actualizados a medida que se añaden, editan o eliminan documentos.

## Por qué usar GroupDocs.Search y Redaction para actualizar índices?
GroupDocs.Search admite **más de 50 formatos de archivo** (PDF, DOCX, XLSX, PPTX, HTML, imágenes, etc.) y puede procesar documentos de cientos de páginas sin cargar el archivo completo en memoria. Combinado con GroupDocs.Redaction, puede eliminar o enmascarar automáticamente datos sensibles antes de la indexación, garantizando el cumplimiento mientras se mantiene la relevancia de la búsqueda.

## Requisitos previos

- **GroupDocs.Search** – instalar vía NuGet.  
- **GroupDocs.Redaction for .NET** – requerido para capacidades de redacción.  
- Visual Studio (o cualquier IDE .NET) con .NET 6+ instalado.  
- Conocimientos básicos de C# y familiaridad con conceptos de indexación.

### Bibliotecas requeridas y versiones
- **GroupDocs.Search** – última versión estable disponible en NuGet.  
- **GroupDocs.Redaction for .NET** – última versión estable disponible en NuGet.

### Requisitos de configuración del entorno
- Una máquina Windows o Linux con .NET SDK instalado.  
- Acceso a una carpeta donde se almacenarán los archivos de índice.

### Prerrequisitos de conocimiento
- Comprensión de la indexación de documentos y los fundamentos de búsqueda.  
- Conciencia de la gestión del ciclo de vida de documentos en sistemas empresariales.

## Configuración de GroupDocs.Redaction para .NET

### Instalar los paquetes

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Busque “GroupDocs.Redaction” e instale la última versión.

### Pasos para adquirir la licencia
1. **Free Trial** – comience con una prueba para explorar todas las funciones.  
2. **Temporary License** – solicite una clave temporal para pruebas extendidas.  
3. **Purchase** – obtenga una licencia completa para implementaciones en producción.

### Inicialización y configuración básica
`Redactor` es la clase principal que aplica reglas de redacción a los documentos.  
Para comenzar, haga referencia al espacio de nombres Redaction y cree una instancia de `Redactor`:

```csharp
using GroupDocs.Redaction;
```

Esto le prepara para aplicar reglas de redacción antes de alimentar los documentos al índice de búsqueda.

## Guía de implementación

Abordaremos dos capacidades principales: actualizar documentos indexados y mantener el control de versiones del índice.

### ¿Cómo actualizar el índice usando GroupDocs.Search?

`Index` representa la colección buscable almacenada en disco.  
`UpdateOptions` configura cómo se realizan las actualizaciones incrementales (p. ej., número de hilos).  
`UpdateDocument` aplica cambios a un solo documento, y `Commit` finaliza todas las actualizaciones pendientes.

**Respuesta directa (40‑70 palabras):**  
Cree un objeto `Index` que apunte a su carpeta de índice, use `UpdateOptions` para especificar el número de hilos, llame a `UpdateDocument` para cada archivo modificado y, finalmente, invoque `Commit` para persistir los cambios. Este enfoque incremental actualiza solo las partes modificadas, manteniendo el índice actual sin una reconstrucción completa.

#### Función 1: Actualizar documentos indexados

##### Visión general
Actualizar documentos indexados garantiza que sus resultados de búsqueda reflejen el contenido más reciente, incluso cuando los documentos se editan o reemplazan.

##### Paso 1: Crear un índice  
La clase `Index` es el objeto de nivel superior que representa una colección buscable en disco.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Paso 2: Añadir documentos al índice  
Añada archivos de un directorio; la biblioteca extrae automáticamente el texto buscable.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Paso 3: Buscar y actualizar  
Ejecútese una consulta, modifique el archivo fuente y luego llame a `UpdateDocument` con las mismas `UpdateOptions` usadas durante la indexación.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Por qué funciona:** Al establecer `Threads = 2`, la actualización aprovecha dos núcleos de CPU, reduciendo el tiempo de procesamiento aproximadamente a la mitad en una máquina de cuatro núcleos.

### ¿Cómo mantener el control de versiones del índice?

`IndexUpdater` es una clase de utilidad que actualiza formatos de índices antiguos a la última versión admitida por la biblioteca.  

**Respuesta directa (40‑70 palabras):** Instancie `IndexUpdater` con la ruta a su índice existente, llame a `CanUpdateVersion()` para verificar la compatibilidad y, si es necesario, ejecute `UpdateVersion()`. Después de la actualización, recargue el índice con el nuevo formato y realice una búsqueda para confirmar que todo funciona. Esto garantiza una migración sin problemas entre versiones de la biblioteca.

#### Función 2: Mantener el control de versiones del índice

##### Visión general
El control de versiones garantiza que los índices antiguos sigan siendo buscables después de una actualización de la biblioteca.

##### Paso 1: Verificar compatibilidad  
`IndexUpdater` verifica si el índice actual puede actualizarse al último formato.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Paso 2: Cargar y buscar  
Después de la actualización, cargue el índice renovado y ejecute una consulta para verificar la integridad.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Por qué funciona:** La verificación `CanUpdateVersion` evita excepciones en tiempo de ejecución causadas por esquemas de índice incompatibles, proporcionando una ruta de actualización segura.

## Aplicaciones prácticas

Escenarios del mundo real donde **how to update index** es importante:

1. **Gestión de documentos legales** – Re‑indexe rápidamente los contratos después de enmiendas mientras redacta cláusulas confidenciales.  
2. **Archivos corporativos** – Mantenga los registros históricos buscables sin volver a procesar millones de archivos.  
3. **Sistemas de gestión de contenidos (CMS)** – Envíe actualizaciones incrementales al índice de búsqueda a medida que los autores publican nuevos artículos.

## Consideraciones de rendimiento

- **Opciones de subprocesamiento:** Ajuste `UpdateOptions.Threads` según los núcleos de CPU; más hilos mejoran el rendimiento pero aumentan el uso de memoria.  
- **Uso de recursos:** Monitoree la RAM; la biblioteca transmite archivos, por lo que los picos de memoria son mínimos incluso para PDFs de 500 páginas.  
- **Mejores prácticas:** Programe actualizaciones incrementales regulares y elimine versiones de índice obsoletas para mantener un rendimiento óptimo.

## Problemas comunes y soluciones

| Problema | Causa | Solución |
|----------|-------|----------|
| **Index not found** | Ruta de carpeta incorrecta | Verifique que el constructor `Index` apunte al directorio correcto. |
| **Version mismatch error** | Uso de un índice antiguo con una biblioteca más nueva | Ejecute el flujo `IndexUpdater` antes de la indexación normal. |
| **Redaction not applied** | Reglas de redacción cargadas después de la indexación | Aplique la redacción **antes** de añadir documentos al índice. |

## Preguntas frecuentes

**Q: ¿Cuál es la diferencia entre `UpdateDocument` y `Rebuild`?**  
A: `UpdateDocument` modifica solo los archivos cambiados, mientras que `Rebuild` recrea todo el índice desde cero, consumiendo más tiempo y recursos.

**Q: ¿Puedo actualizar varios documentos en paralelo?**  
A: Sí, establezca `UpdateOptions.Threads` al número de núcleos que desea utilizar; la biblioteca gestiona el procesamiento paralelo internamente.

**Q: ¿GroupDocs.Search admite PDFs encriptados?**  
A: Absolutamente. Proporcione la contraseña mediante `SearchOptions.Password` al cargar el documento.

**Q: ¿Cómo verifico que la redacción fue exitosa antes de indexar?**  
A: Llame a `Redactor.Apply()` y examine el tamaño del archivo de salida; un tamaño reducido suele indicar una redacción exitosa.

**Q: ¿Qué versiones de .NET son oficialmente compatibles?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 y .NET 6+.

## Conclusión

Ahora dispone de una guía completa y lista para producción sobre **how to update index** usando GroupDocs.Search y sobre cómo mantener esos índices compatibles con versiones mediante GroupDocs.Redaction para .NET. Siguiendo los pasos anteriores, puede asegurarse de que su capa de búsqueda permanezca rápida, precisa y cumpla con las regulaciones de privacidad de datos.

**Próximos pasos:**  
- Experimente con diferentes configuraciones de `Threads` para encontrar el punto óptimo para su hardware.  
- Explore patrones avanzados de redacción (p. ej., eliminación de SSN basada en expresiones regulares) antes de la indexación.  
- Integre la rutina de actualización de índice en su canal CI/CD para una gestión de documentos totalmente automatizada.

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs  

## Recursos
- [Documentación](https://docs.groupdocs.com/search/net/)
- [Referencia API](https://reference.groupdocs.com/redaction/net)
- [Descargar GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/search/10)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

## Tutoriales relacionados

- [Dominar GroupDocs.Redaction .NET: Creación eficiente de índices y gestión de alias para búsqueda avanzada de documentos](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implementar búsqueda de sinónimos con GroupDocs.Redaction .NET para una gestión de documentos mejorada](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Dominar GroupDocs Search y Redaction en .NET: Gestión avanzada de documentos](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)