---
date: '2026-04-21'
description: Aprende a filtrar archivos usando GroupDocs.Redaction para .NET, incluyendo
  filtrado por fecha de creación, tamaño de archivo, fecha de modificación y cómo
  aplicar filtros NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Cómo filtrar archivos con GroupDocs.Redaction para .NET
type: docs
url: /es/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Cómo filtrar archivos con GroupDocs.Redaction para .NET

En el entorno digital de hoy, **cómo filtrar archivos** de manera eficiente puede marcar la diferencia en su productividad. Ya sea que necesite aislar documentos por extensión, fecha de creación, tamaño o fecha de modificación, una estrategia de filtrado sólida ahorra tiempo, reduce costos de almacenamiento y mantiene su índice de búsqueda ordenado. En este tutorial recorreremos ejemplos reales usando GroupDocs.Redaction para .NET, mostrándole exactamente cómo filtrar archivos para satisfacer necesidades empresariales comunes.

## Respuestas rápidas
- **¿Qué biblioteca necesito?** GroupDocs.Redaction for .NET (instalar vía NuGet).  
- **¿Puedo filtrar por fecha de creación?** Sí – use `CreateCreationTimeRange`.  
- **¿Cómo excluyo ciertos tipos?** Aplique un filtro NOT con `DocumentFilter.CreateNot`.  
- **¿Se admite el filtrado por tamaño de archivo?** Absolutamente, mediante `CreateFileLengthRange` o límites superior/inferior.  
- **¿Necesito una licencia?** Se requiere una licencia de prueba o completa para uso en producción.

## ¿Qué es el filtrado de archivos con GroupDocs.Redaction?
El filtrado de archivos le permite indicar al motor de indexación qué documentos incluir o ignorar en función de metadatos como la extensión, fechas, patrones de ruta o tamaño. Al definir reglas precisas de `DocumentFilter`, mantiene su índice liviano y sus búsquedas rápidas.

## ¿Por qué usar GroupDocs.Redaction para .NET?
- **Ayudantes de filtro integrados** – no es necesario escribir código personalizado del sistema de archivos.  
- **Operadores lógicos** – combine múltiples criterios con AND, OR y NOT.  
- **Optimizado para rendimiento** – los filtros se aplican durante la indexación, no después.  
- **Multiplataforma** – funciona con .NET Framework, .NET Core y .NET 5/6+.

## Requisitos previos
- .NET Framework 4.6+ o .NET Core 3.1+ instalado.  
- Visual Studio o su IDE de C# preferido.  
- Conocimientos básicos de C#.  

### Bibliotecas requeridas y configuración
Instale el paquete NuGet usando su método preferido:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Consejo profesional:** Después de instalar, agregue su archivo de licencia a la raíz del proyecto y llame a `License.SetLicense("license-file-path")` antes de crear cualquier objeto Redactor o Index.

## Configuración de GroupDocs.Redaction para .NET

Primero, cree una instancia de `Redactor` que apunte al documento con el que desea trabajar:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Por qué es importante:** Inicializar el Redactor garantiza que la biblioteca esté lista para aplicar filtros y reglas de redacción más adelante en el flujo de trabajo.

## Cómo filtrar archivos por extensión

Filtrar por extensión de archivo es la forma más común de reducir un conjunto de documentos. A continuación solo conservamos archivos FB2, EPUB y TXT.

### Filtrar por extensión de archivo

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cómo aplicar filtro NOT para excluir tipos no deseados

Si necesita **aplicar lógica de filtro NOT**—por ejemplo, excluir archivos HTML y PDF—use `CreateNot`.

### Excluir archivos HTM, HTML y PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cómo filtrar archivos por fecha de creación

Cuando necesite **filtrar por fecha de creación**, especifique un `DateTime` de inicio y fin.

### Filtrar por rango de fechas de creación

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cómo filtrar archivos por fecha de modificación

Similar a las fechas de creación, puede limitar los resultados a archivos modificados antes de un punto determinado.

### Filtrar por fecha de modificación

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cómo filtrar archivos por ruta usando expresiones regulares

Si la estructura de sus carpetas sigue convenciones de nombres, una expresión regular puede apuntar a rutas específicas.

### Filtrar por patrón de ruta de archivo

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cómo filtrar archivos por tamaño

Controlar el tamaño de los documentos es esencial al manejar límites de ancho de banda o almacenamiento.

### Filtrar por tamaño de archivo (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cómo combinar múltiples condiciones con AND

Cuando necesite **filtrar archivos** usando varios criterios a la vez, combínelos con `CreateAnd`.

### Ejemplo de AND lógico

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cómo combinar múltiples condiciones con OR

Use `CreateOr` cuando cualquiera de varias reglas deba aprobar.

### Ejemplo de OR lógico

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Problemas comunes y soluciones
- **Filtro no aplicado:** Asegúrese de asignar `settings.DocumentFilter` **antes** de crear la instancia `Index`.  
- **Aparecen archivos inesperados:** Verifique que las extensiones de archivo incluyan el punto inicial (`.txt`).  
- **Ralentización del rendimiento:** Combine filtros con AND para reducir la cantidad de archivos escaneados temprano en la canalización de indexación.  
- **Errores de regex:** Escape los caracteres especiales en su patrón de ruta o use `RegexOptions.IgnoreCase` para coincidencias sin distinción de mayúsculas.

## Preguntas frecuentes

**P: ¿Puedo combinar un filtro NOT con un filtro AND?**  
R: Sí. Construya primero el filtro NOT (`DocumentFilter.CreateNot`) y luego inclúyalo como uno de los argumentos de `DocumentFilter.CreateAnd`.

**P: ¿Cómo filtro archivos mayores de 10 MB?**  
R: Use `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` para incluir solo los archivos que superen ese tamaño.

**P: ¿Es posible filtrar por fechas de creación y modificación simultáneamente?**  
R: Absolutamente. Cree cada filtro por separado y combínelos con `CreateAnd`.

**P: ¿Estos filtros funcionan con rutas de almacenamiento en la nube?**  
R: Los filtros operan sobre el sistema de archivos local. Para fuentes en la nube, descargue los archivos a una carpeta temporal primero, luego aplique los mismos filtros.

**P: ¿Cambiar el filtro requerirá re‑indexar?**  
R: Sí. Los filtros se evalúan cuando llama a `index.Add`. Cambiar un filtro implica que debe reconstruir el índice para reflejar los nuevos criterios.

## Conclusión

Al dominar **cómo filtrar archivos** con GroupDocs.Redaction para .NET—ya sea por extensión, fecha de creación, fecha de modificación, tamaño de archivo o usando lógica NOT—puede optimizar la gestión de documentos, mantener los índices eficientes y centrarse en el contenido que realmente importa. Experimente con los operadores lógicos para adaptar el filtrado a sus reglas de negocio exactas, y verá mejoras inmediatas en velocidad y eficiencia de almacenamiento.

---

**Última actualización:** 2026-04-21  
**Probado con:** GroupDocs.Redaction 24.11 for .NET  
**Autor:** GroupDocs  

---