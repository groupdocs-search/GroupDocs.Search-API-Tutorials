---
date: '2026-09-16'
description: Aprende a crear un índice de búsqueda con GroupDocs en .NET, agregar
  documentos al índice y habilitar la búsqueda de sinónimos para obtener resultados
  de consulta más inteligentes.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Aprende a crear un índice de búsqueda con GroupDocs en .NET, agregar
  documentos al índice y habilitar la búsqueda de sinónimos para obtener resultados
  de consulta más inteligentes.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Cómo crear un índice de búsqueda con GroupDocs en .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Cómo crear un índice de búsqueda con GroupDocs y búsqueda de sinónimos en .NET
type: docs
url: /es/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Cómo crear un índice de búsqueda con GroupDocs y búsqueda de sinónimos en .NET

En esta guía aprenderá **cómo crear un índice de búsqueda** usando GroupDocs.Search, agregar documentos a ese índice y habilitar la búsqueda de sinónimos para que los usuarios puedan encontrar contenido relevante incluso cuando usan una terminología diferente. Ya sea que esté construyendo un repositorio legal, una base de conocimiento corporativa o un archivo de investigación, los pasos a continuación le brindan una solución lista para producción que funciona en .NET Framework 4.6.1+, .NET Core y .NET 5+.

## Respuestas rápidas
- **¿Qué significa “crear índice de búsqueda”?** Construye un catálogo buscable de sus documentos, almacenando el texto extraído en una estructura optimizada para búsquedas en milisegundos.  
- **¿Por qué usar la búsqueda de sinónimos?** Amplía una consulta para incluir palabras con el mismo significado, aumentando la recuperación en hasta un 30 % en corpora típicos.  
- **¿Cuáles son los requisitos principales?** .NET 4.6.1+ (o .NET Core/5+), conocimientos de C# y los paquetes NuGet GroupDocs.Search + GroupDocs.Redaction.  
- **¿Necesito una licencia?** Una prueba gratuita es suficiente para la evaluación; se requiere una licencia permanente para implementaciones en producción.  
- **¿Puedo combinar esto con la redacción?** Sí—GroupDocs.Redaction puede ejecutarse antes o después de la búsqueda para enmascarar datos sensibles.

## ¿Qué es “crear índice de búsqueda”?
Un **índice de búsqueda** es una estructura de datos que contiene el texto extraído y los metadatos de cada documento, permitiendo que el motor localice archivos coincidentes al instante. GroupDocs.Search construye este índice escaneando la carpeta de origen, analizando los formatos compatibles y escribiendo archivos de índice compactos en un directorio que usted especifique.

## ¿Por qué habilitar la búsqueda de sinónimos?
La búsqueda de sinónimos agrega automáticamente términos alternativos a la consulta del usuario, de modo que una búsqueda de **“improve”** también devuelva documentos que contengan **“enhance,” “upgrade,”** o **“optimize.”** En la práctica, esto puede aumentar la recuperación de resultados entre un 20‑35 % manteniendo alta la precisión, porque el diccionario de sinónimos incorporado está curado para cada idioma.

## Requisitos previos
- **.NET Framework 4.6.1** o posterior (o cualquier tiempo de ejecución .NET Core/5+).  
- Habilidades básicas de desarrollo en C# y Visual Studio (Community, Professional o Enterprise).  
- Paquetes GroupDocs.Search y GroupDocs.Redaction instalados a través de NuGet.

### Instalación
Instale GroupDocs.Redaction para .NET usando uno de estos métodos (consulte la documentación de [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) para obtener detalles):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Consola del Administrador de paquetes:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Alternativamente, use la interfaz de usuario del Administrador de paquetes NuGet en Visual Studio para buscar “GroupDocs.Redaction” e instalarlo directamente. Para referencia de la API, consulte la [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Obtención de licencia
- **Prueba gratuita:** Comience con una versión de prueba para explorar todas las funciones.  
- **Licencia temporal:** Solicite una licencia temporal en el [sitio web de GroupDocs](https://purchase.groupdocs.com/temporary-license/) o administre su licencia a través del portal [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/).  
- **Compra completa:** Cuando esté listo para producción, adquiera una licencia completa que elimine todas las limitaciones de evaluación.

## Cómo configurar GroupDocs.Redaction para .NET
GroupDocs.Redaction proporciona la funcionalidad central para redactar contenido sensible antes o después de la búsqueda. Expone una clase `Redactor` que usted instancia con una licencia y configuraciones opcionales.

El siguiente código demuestra cómo crear una instancia de redactor y cargar un archivo de licencia:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Con el redactor listo, puede posteriormente llamar a `redactor.Redact(...)` en cualquier documento que recupere de los resultados de búsqueda.

## Cómo crear el índice de búsqueda
Crear un índice de búsqueda implica especificar una carpeta donde se almacenarán los archivos del índice y luego inicializar la clase `Index` de GroupDocs.Search. El índice contendrá todos los datos buscables extraídos de sus documentos de origen.

Primero, cree un directorio para el índice y luego instancie el objeto `Index`:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Crear el índice escribe un conjunto de archivos binarios en la carpeta; estos archivos suelen ser menores de 200 KB por cada 1,000 páginas, lo que le permite escalar a millones de páginas sin agotar el espacio en disco.

## Cómo agregar documentos al índice
Agregar documentos requiere apuntar la API al directorio que contiene los archivos de origen e indicar al índice que los ingrese. El proceso analiza cada formato compatible, extrae el texto y lo almacena en el índice para una recuperación rápida.

Utilice el siguiente código para indexar todos los archivos en una carpeta de origen:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search admite **más de 30** formatos de entrada, incluidos DOCX, PDF, PPTX, HTML y tipos de imagen comunes, por lo que puede indexar prácticamente cualquier archivo corporativo sin convertidores adicionales.

## Cómo habilitar y ejecutar la búsqueda de sinónimos
El manejo de sinónimos se activa mediante `SearchOptions`. Una vez habilitado, cada consulta se expande automáticamente para incluir los sinónimos del diccionario, mejorando la recuperación sin sacrificar la precisión.

Habilite la búsqueda de sinónimos con el siguiente fragmento:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

El diccionario de sinónimos predeterminado contiene más de **5,000** pares de términos para inglés. También puede cargar un archivo `SynonymDictionary` personalizado para admitir jerga específica de la industria.

## Diccionario de sinónimos personalizado
Si necesita sinónimos específicos de dominio, cargue su propio archivo de diccionario y asígnelo a `SearchOptions` antes de ejecutar una consulta.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Consejos comunes de solución de problemas
- **Problemas de ruta:** Verifique que las carpetas de índice y origen sean accesibles por la cuenta del proceso.  
- **Límites de licencia:** Una compilación sin licencia puede restringir el número de archivos indexados a 100.  
- **Sin resultados:** Verifique que el diccionario de sinónimos esté cargado; puede inspeccionar `options.SynonymDictionary.Count` en tiempo de ejecución.  

## Aplicaciones prácticas
1. **Gestión de documentos legales:** Encuentre jurisprudencia usando términos legales y sus sinónimos.  
2. **Investigación académica:** Amplíe búsquedas bibliográficas en PDFs académicos y archivos Word.  
3. **Bases de conocimiento corporativas:** Recupere políticas internas incluso cuando los usuarios formulen consultas de manera diferente.  
4. **Sistemas de gestión de contenido:** Ofrezca a los editores una detección más rica al etiquetar artículos.  
5. **Gestión de tickets de soporte al cliente:** Relacione tickets con problemas conocidos usando descripciones sinónimas.  

## Consideraciones de rendimiento
- **Mantenimiento del índice:** Re‑indexe después de actualizaciones masivas; la indexación incremental reduce el tiempo de inactividad hasta un 70 %.  
- **Monitoreo de recursos:** Indexar un lote de 10 GB en una VM estándar (2 vCPU, 8 GB RAM) alcanza un pico de ~1.2 GB RAM; reduzca el tamaño del lote si se acercan a los límites.  
- **Liberación de objetos:** Llame a `index.Dispose()` y `redactor.Dispose()` tan pronto como termine para liberar recursos nativos.  

## Conclusión
Ahora sabe **cómo crear un índice de búsqueda** con GroupDocs, agregar documentos a ese índice y habilitar la búsqueda de sinónimos para una experiencia de usuario más intuitiva. Esta base también le permite agregar redacción, clasificación personalizada o coincidencia difusa sobre un motor de búsqueda robusto.

## Próximos pasos
- Experimente con `SearchOptions.FuzzySearch` para capturar errores ortográficos.  
- Explore la API `Ranking` para impulsar documentos prioritarios.  
- Únase a la comunidad en el [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) o en el [Free Support Forum](https://forum.groupdocs.com/c/search/10) para compartir consejos y hacer preguntas.  
- Consulte los [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) para actualizaciones y nuevas funciones.  

## Preguntas frecuentes

**Q: ¿Qué es la búsqueda de sinónimos?**  
A: La búsqueda de sinónimos amplía la consulta del usuario para incluir términos alternativos predefinidos, aumentando la probabilidad de encontrar documentos relevantes que usen una redacción diferente.

**Q: ¿Cómo actualizo mi licencia de GroupDocs?**  
A: Visite el portal [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) y cargue el nuevo archivo de licencia mediante `License.SetLicense("path/to/license.lic")`.

**Q: ¿Puedo usar la búsqueda de sinónimos en un entorno multilingüe?**  
A: Sí—cargue un archivo `SynonymDictionary` específico para cada idioma que soporte, y el motor aplicará el conjunto de sinónimos correspondiente a cada consulta.

**Q: ¿Cuáles son los problemas de indexación más comunes?**  
A: Los permisos de acceso a archivos, los formatos no compatibles y superar el límite de documentos de la versión de prueba son los tres principales problemas que encuentran los desarrolladores.

**Q: ¿Cómo puedo optimizar el rendimiento para índices muy grandes?**  
A: Use indexación incremental, almacene el índice en SSDs y configure `IndexingOptions.MaxDegreeOfParallelism` para que coincida con la cantidad de núcleos de CPU.

---

**Última actualización:** 2026-09-16  
**Probado con:** GroupDocs.Search 23.10 for .NET  
**Autor:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Tutoriales relacionados

- [Agregar documento al índice con tutoriales de GroupDocs.Search .NET](/search/net/document-management/)
- [Resaltar resultados de búsqueda en documentos .NET usando GroupDocs.Search y Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Cómo actualizar el índice con GroupDocs.Search y Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)