---
date: '2026-06-07'
description: Aprenda cómo implementar compresión alta en .NET para el almacenamiento
  de texto y redactar datos confidenciales usando GroupDocs.Search y GroupDocs.Redaction
  en aplicaciones .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Implementar compresión alta en .NET con GroupDocs: Guía de texto y redacción'
type: docs
url: /es/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementar compresión alta .NET con GroupDocs: Guía de texto y redacción

En soluciones .NET modernas, **implement high compression .net** es esencial cuando necesitas almacenar colecciones masivas de texto sin agotar el espacio en disco. Al mismo tiempo, proteger información sensible —como identificadores personales o cifras financieras— requiere una redacción confiable. Este tutorial te muestra, paso a paso, cómo configurar el almacenamiento de texto con alta compresión usando **GroupDocs.Search** y cómo redactar de forma segura datos confidenciales con **GroupDocs.Redaction**. Al final, podrás comprimir el texto indexado hasta en un 90 % y eliminar contenido privado de PDFs, archivos Word y muchos otros formatos.

## Respuestas rápidas
- **¿Qué biblioteca proporciona indexación de alta compresión?** GroupDocs.Search for .NET.  
- **¿Qué herramienta redacta datos sensibles?** GroupDocs.Redaction for .NET.  
- **¿Puedo agregar documentos al índice automáticamente?** Sí—use the `AddDocument` API inside a folder‑scan loop.  
- **¿La compresión es sin pérdida para la búsqueda?** Sí, the text remains fully searchable after compression.  
- **¿Necesito una licencia para producción?** Se requiere una licencia permanente de GroupDocs para uso comercial.

## Qué es “implement high compression .net”?
Implement high compression .net significa configurar el motor de indexación GroupDocs.Search para almacenar el contenido textual extraído en forma comprimida. Esto reduce drásticamente el tamaño del índice en disco mientras mantiene el texto completamente buscable. La compresión es sin pérdida, por lo que la relevancia de las consultas y la extracción de fragmentos funcionan exactamente como con un índice sin comprimir.

## ¿Por qué usar GroupDocs para compresión y redacción?
GroupDocs.Search admite más de cincuenta formatos de entrada y puede comprimir el texto indexado hasta en un noventa por ciento, permitiendo que grandes colecciones de documentos ocupen solo una fracción de su tamaño original. GroupDocs.Redaction complementa esto borrando o enmascarando permanentemente información sensible en más de treinta tipos de archivos, ayudándote a cumplir regulaciones estrictas como GDPR y HIPAA sin herramientas adicionales.

## Requisitos previos
- **Entorno de desarrollo:** Visual Studio 2022 o posterior, .NET 6+ (o .NET Framework 4.7.2).  
- **Bibliotecas:** paquetes NuGet `GroupDocs.Search` y `GroupDocs.Redaction`.  
- **Permisos:** Acceso de lectura/escritura a las carpetas que contienen los documentos fuente y la ubicación de salida del índice.  
- **Conocimientos básicos:** sintaxis de C#, I/O de archivos y familiaridad con la estructura de proyectos .NET.

## ¿Cómo implementar compresión alta .NET con GroupDocs?
Para implementar compresión alta .NET con GroupDocs, primero crea una instancia de `TextStorageSettings` y establece su `CompressionLevel` a `High`. Luego instancia un objeto `Index`, pasando la configuración y la carpeta donde se almacenará el índice. Después de que el índice esté listo, agrega documentos usando `AddDocument`, y finalmente ejecuta búsquedas con el método `Search`, todo mientras el motor maneja de forma transparente la compresión y descompresión.

### Paso 1: Instalar los paquetes NuGet requeridos
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Busca “GroupDocs.Search” y haz clic en **Install**.  

### Paso 2: Instalar GroupDocs.Redaction (para la redacción de datos)
- Abre el **NuGet Package Manager**.  
- Busca **GroupDocs.Redaction** e instala la versión estable más reciente.  

### Paso 3: Obtener y aplicar una licencia
- **Prueba gratuita:** Regístrate en el portal de GroupDocs para obtener una clave de prueba de 30 días.  
- **Licencia temporal:** Solicita una clave temporal para entornos de desarrollo.  
- **Licencia permanente:** Compra una licencia de producción para eliminar las limitaciones de evaluación.  

### Paso 4: Inicialización básica de ambas bibliotecas
Los motores `Search` y `Redaction` comparten un modelo de licencia común. Inicialízalos al iniciar la aplicación:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Función 1: Configuración de almacenamiento de texto con alta compresión

### Configuración de la indexación
`TextStorageSettings` es la clase que indica a GroupDocs.Search cómo mantener el texto extraído. Habilitar la alta compresión reduce el tamaño del índice hasta en **10×** sin afectar la velocidad de búsqueda.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explicación:**  
- `CompressionLevel.High` activa un algoritmo basado en ZSTD que comprime bloques de texto de manera eficiente.  
- `UseMemoryCache = false` obliga al motor a transmitir datos desde el disco, lo cual es ideal para implementaciones a gran escala.

### Creación y gestión del índice
El objeto `Index` representa el repositorio buscable en disco. Especificas la carpeta donde se almacenarán los archivos del índice y pasas la configuración de compresión definida anteriormente.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Explicación:**  
- `indexFolder` determina dónde viven los archivos de índice comprimidos.  
- `settings` inyecta la configuración de alta compresión, asegurando que cada documento agregado se beneficie de ella.

## Función 2: Agregar documentos al índice

### Agregar documentos a tu índice
`AddDocument` agrega un solo archivo al índice, extrayendo su texto, comprimiéndolo según la configuración establecida y almacenando el resultado. GroupDocs.Search puede ingerir archivos de un árbol de directorios. El siguiente bucle recorre `documentsFolder`, agrega cada archivo y registra el progreso.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Explicación:**  
- `AddDocument` analiza el archivo, extrae texto buscable, lo comprime según `TextStorageSettings` y lo almacena en el índice.  
- Este enfoque funciona para **PDF, DOCX, TXT, HTML** y más de **30** formatos adicionales.

## Función 3: Ejecutar una consulta de búsqueda

### Realizar una búsqueda
`Search` ejecuta una consulta contra el índice comprimido y devuelve una colección de objetos `DocumentResult` coincidentes con puntuaciones de relevancia y fragmentos resaltados. Una vez que el índice está poblado, puedes ejecutar consultas rápidas. El método `Search` devuelve una colección de objetos `DocumentResult` que incluyen rutas de archivo y fragmentos resaltados.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Explicación:**  
- El motor de búsqueda escanea el texto comprimido directamente, por lo que la latencia de la consulta se mantiene baja incluso para índices que contienen **millones de páginas**.  
- `Score` indica la relevancia; valores más altos significan una mejor coincidencia.

## ¿Cómo redactar datos confidenciales con GroupDocs.Redaction?
La redacción de datos confidenciales con GroupDocs.Redaction comienza creando una instancia `Redactor` para el archivo objetivo. Define uno o más objetos `SearchPattern` que describen el texto a eliminar, como expresiones regulares para números de seguro social. Aplica cada patrón usando `Redact`, especificando un `RedactionType` como `BlackOut`, y guarda el resultado como un nuevo documento, asegurando que el original permanezca intacto.

`Redactor` es la clase principal en GroupDocs.Redaction utilizada para cargar un documento y realizar operaciones de redacción.  
`SearchPattern` define una expresión regular que identifica el texto a redactar.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explicación:**  
- `SearchPattern` usa una expresión regular para localizar números de seguro social.  
- `RedactionType.BlackOut` reemplaza el texto coincidente con un rectángulo negro sólido, asegurando que los datos no puedan recuperarse.

## Aplicaciones prácticas
1. **Gestión de documentos legales:** Comprime automáticamente archivos de casos masivos y redacta los identificadores de clientes antes de archivarlos.  
2. **Registros de salud:** Almacena años de notas de pacientes en un índice comprimido y elimina PHI (Información de Salud Protegida) antes de compartir con socios de investigación.  
3. **Informes financieros:** Asegura los informes trimestrales redactando números de cuenta mientras mantienes el texto buscable para consultas de auditoría.

## Consideraciones de rendimiento
- **Impacto de la compresión:** La alta compresión reduce el tamaño del índice hasta en **90 %**, lo que disminuye el desgaste del SSD y acelera las operaciones de respaldo.  
- **Uso de memoria:** Desactiva el caché en memoria para índices muy grandes para mantener la huella del proceso por debajo de **500 MB**.  
- **Optimización de I/O:** Agrupa la adición de documentos en lotes de 100 para minimizar la sobrecarga del disco.  
- **Procesamiento asíncrono:** Envuelve las llamadas a `AddDocument` en `Task.Run` para mantener los hilos de UI responsivos en aplicaciones de escritorio.

## Problemas comunes y solución de errores
- **Rutas de archivo incorrectas:** Verifica que `documentsFolder` y `indexFolder` sean rutas absolutas y que la aplicación tenga permisos de lectura/escritura.  
- **Errores de licencia:** Asegúrate de que los archivos `.lic` estén desplegados junto al ejecutable o incrustados como recursos.  
- **La búsqueda no devuelve resultados:** Comprueba que el nivel de compresión de `TextStorageSettings` coincida con el usado durante la indexación; configuraciones incompatibles pueden causar fallas de deserialización.  

## Preguntas frecuentes

**Q: ¿Puedo agregar documentos al índice después de la construcción inicial?**  
A: Sí—simplemente llama a `index.AddDocument` para archivos nuevos; el motor actualiza el índice comprimido de forma incremental.

**Q: ¿La redacción altera el archivo original?**  
A: No—el archivo original permanece intacto; la versión redactada se guarda como un nuevo archivo, preservando la integridad del documento.

**Q: ¿Qué formatos admite GroupDocs.Redaction?**  
A: Más de **30** formatos, incluidos PDF, DOCX, PPTX, XLSX, imágenes (PNG, JPEG) y texto plano.

**Q: ¿Cómo afecta la alta compresión a la relevancia de la búsqueda?**  
A: No lo hace. La compresión es sin pérdida para el texto, por lo que las puntuaciones de relevancia son idénticas a un índice sin comprimir.

**Q: ¿Existe un límite al tamaño de los documentos que puedo indexar?**  
A: GroupDocs.Search puede manejar archivos de varios gigabytes transmitiendo el contenido; sin embargo, asegúrate de contar con suficiente espacio en disco para el índice comprimido (aproximadamente el 10 % del tamaño original).

## Recursos
- [Documentación](https://docs.groupdocs.com/search/net/)
- [Referencia de API](https://reference.groupdocs.com/redaction/net)
- [Descargar GroupDocs.Redaction para .NET](https://releases.groupdocs.com/search/net/)
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/search/10)
- [Obtención de licencia temporal](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2026-06-07  
**Probado con:** GroupDocs.Search 23.12 y GroupDocs.Redaction 23.12 para .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Implementación de GroupDocs.Search y Redaction en .NET para la gestión de documentos](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Cómo optimizar GroupDocs.Redaction para .NET: Guía de gestión eficiente de índices y ortografía](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Domina GroupDocs Redaction y Search en .NET: Gestión eficiente de documentos y búsqueda segura](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)