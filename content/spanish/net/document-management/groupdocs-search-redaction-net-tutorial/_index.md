---
date: '2026-06-12'
description: Aprenda cómo crear un índice de búsqueda .NET y aplicar redacción a PDF
  usando GroupDocs.Search y GroupDocs.Redaction. Configuración, implementación, indexación
  y búsqueda avanzada explicadas.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Crear índice de búsqueda .NET con GroupDocs.Search y GroupDocs.Redaction –
  Guía completa
type: docs
url: /es/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Crear índice de búsqueda .NET con GroupDocs Search y Redaction – Guía completa

En el panorama digital actual, **crear un índice de búsqueda .NET** solución que pueda tanto localizar información rápidamente como proteger datos sensibles es una prioridad principal para cualquier organización. Este tutorial le guía a través de la configuración de una red escalable de GroupDocs.Search, el despliegue de nodos, la indexación de documentos y el uso de GroupDocs.Redaction para **aplicar redacción a PDF** archivos—todo dentro de un entorno .NET.

## Respuestas rápidas
- **¿Cuál es el primer paso para crear un índice de búsqueda .NET?** Defina una ruta base y un puerto, luego despliegue los nodos de la red.  
- **¿Cómo aplico redacción a PDF con GroupDocs?** Inicialice una instancia de `Redactor`, cargue el PDF y llame a `Redact` con los patrones deseados.  
- **¿Puedo ejecutar la red de búsqueda en múltiples máquinas?** Sí—despliegue nodos en servidores separados y permita que el nodo maestro coordine la indexación y las consultas.  
- **¿Necesito una licencia para uso en producción?** Se requiere una licencia válida de GroupDocs para producción; una licencia de prueba temporal está disponible para evaluación.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.7.2+, .NET Core 3.1+ y .NET 5/6/7 son totalmente compatibles.

## Qué es “crear índice de búsqueda .net”?
*Crear un índice de búsqueda .NET* se refiere a construir un repositorio buscable de metadatos y contenido de documentos usando bibliotecas .NET, que extrae texto, tokeniza términos y los almacena en una estructura de índice optimizada. Esto permite respuestas instantáneas a consultas a través de nodos distribuidos, soportando varios formatos de archivo y permitiendo una recuperación de documentos escalable y de alto rendimiento en aplicaciones empresariales.

## ¿Por qué usar GroupDocs Search y Redaction juntos?
GroupDocs.Search soporta **más de 50 formatos de archivo**—incluidos DOCX, PDF, PPTX y HTML—y puede indexar documentos de cientos de páginas sin cargar el archivo completo en memoria. Combinado con GroupDocs.Redaction, que puede **aplicar redacción a PDF** en menos de 200 ms por página, obtiene una canalización de gestión de documentos segura y de alto rendimiento.

## Requisitos previos

### Bibliotecas y dependencias requeridas
Para seguir este tutorial, instale los siguientes paquetes:
- **GroupDocs.Search** para .NET
- **GroupDocs.Redaction** para .NET  

Puede usar cualquiera de estos métodos para instalar las bibliotecas necesarias:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Busque "GroupDocs.Search" y "GroupDocs.Redaction" e instale la versión más reciente.

### Requisitos de configuración del entorno
- .NET Framework 4.7.2 o superior (o .NET Core 3.1+)
- IDE Visual Studio (Community, Professional o Enterprise)

### Prerrequisitos de conocimientos
- Programación básica en C#
- Conceptos de programación orientada a objetos
- Familiaridad con configuraciones de red y sistemas de gestión documental

## Configuración de GroupDocs.Redaction para .NET

### Información de instalación
Para integrar funciones de redacción en su aplicación, comience añadiendo la biblioteca GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Busque "GroupDocs.Redaction" e instálelo.

### Obtención de licencia
Para comenzar con una prueba gratuita o una licencia temporal, siga estos pasos:
- Visite el [sitio web de GroupDocs](https://purchase.groupdocs.com/temporary-license/) para solicitar una licencia temporal.  
- Para opciones de compra, navegue a su [página de precios](https://groupdocs.com/pricing).

Una vez que tenga su archivo de licencia, aplíquelo en la configuración de su aplicación:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Inicialización básica
Para inicializar GroupDocs.Redaction para operaciones básicas, use el siguiente fragmento de código:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Guía de implementación

### Configuración

#### Visión general
Esta característica configura su red de búsqueda usando una ruta base y un número de puerto, formando la base de su sistema de gestión documental.

#### Ancla de definición
`SearchNetworkDeployment` es la clase que orquesta el despliegue de nodos de búsqueda a través de la red.

#### Paso 1: Definir ruta base y puerto  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Paso 2: Configurar la red
Utilice el método `Configure` para configurar la red de búsqueda con la ruta y el puerto especificados:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Despliegue de nodos de red

#### Visión general
Despliegue nodos dentro de su red de búsqueda configurada para búsqueda distribuida de documentos.

#### Ancla de definición
`SearchNetworkNode` representa un nodo buscable individual que se comunica con el nodo maestro.

#### Paso 1: Inicializar despliegue  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Suscripción a eventos para el nodo maestro

#### Visión general
Suscríbase a eventos en el nodo maestro para monitorear y gestionar las operaciones de la red de manera eficaz.

#### Ancla de definición
`SearchNetworkNodeEvents` proporciona devoluciones de llamada para indexación, ejecución de consultas y manejo de errores.

#### Paso 1: Identificar el nodo maestro  
Seleccione el primer nodo como su maestro:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Paso 2: Suscribirse a eventos  
Suscríbase a eventos usando:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Indexación de documentos

#### Visión general
Indexe documentos para operaciones de búsqueda eficientes. Este paso es crucial para asegurar que su red pueda recuperar rápidamente los datos necesarios.

#### Ancla de definición
`SearchIndex` es el objeto central que almacena tokens buscables y metadatos para cada archivo indexado.

#### Paso 1: Añadir directorios al índice  
Especifique los directorios que contienen sus documentos:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Funcionalidad de búsqueda – Uso básico

#### Visión general
Realice operaciones básicas de búsqueda a través de los nodos de la red.

#### Respuesta directa
Llame a `SearchNetwork.Query("your term")` en el nodo maestro para recuperar documentos coincidentes instantáneamente. El método devuelve una colección de objetos `SearchResult` que incluyen rutas de archivo y puntuaciones de relevancia.  
`SearchNetwork.Query` es un método que ejecuta una consulta de búsqueda en toda la red y devuelve los resultados coincidentes.

#### Paso 1: Definir parámetros de búsqueda  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Funcionalidad de búsqueda avanzada

#### Visión general
Utilice técnicas de búsqueda avanzadas con parámetros personalizables para obtener resultados más precisos.

#### Respuesta directa
Implemente un método que construya un objeto `SearchOptions`, establezca las propiedades `UseFuzzySearch`, `Highlight` y `PageSize`, y luego lo pase a `SearchNetwork.QueryAdvanced`. Esto produce resultados paginados y resaltados con coincidencia difusa habilitada.  
`SearchNetwork.QueryAdvanced` es un método que ejecuta una consulta con opciones avanzadas como coincidencia difusa y paginación.

#### Paso 1: Implementar el método de búsqueda avanzada  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Aplicación de redacción a archivos PDF

#### Visión general
Proteja información sensible redactando el contenido PDF antes de que se almacene o comparta.

#### Respuesta directa
Cree una instancia de `Redactor`, cargue el PDF objetivo, defina un `RedactionPattern` (p. ej., expresión regular de SSN), llame a `redactor.Apply(pattern)`, y finalmente guarde el documento redactado. Este proceso asegura que los datos personales se eliminen permanentemente.

#### Ancla de definición
`Redactor` es la clase principal en GroupDocs.Redaction que procesa documentos y aplica reglas de redacción.

#### Flujo de trabajo de ejemplo (sin nuevo bloque de código)  
1. Inicialice `Redactor` con su licencia.  
2. Cargue el PDF usando `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` representa una regla que especifica el texto o patrón a redactar. Defina patrones como `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Ejecute `redactor.Apply(pattern)`.  
5. Guarde la salida con `redactor.Save("sample_redacted.pdf")`.

### Aplicaciones prácticas

#### Casos de uso del mundo real
1. **Gestión de documentos legales** – Busque contratos de manera eficiente y redacte automáticamente los identificadores de clientes.  
2. **Registros de salud** – Localice notas de pacientes mientras asegura la redacción conforme a HIPAA de la PHI.  
3. **Cumplimiento corporativo** – Analice comunicaciones internas en busca de términos prohibidos y redacte antes de archivar.

## Conclusión 
Esta guía proporciona una ruta completa para **crear un índice de búsqueda .NET** solución que escala, indexa rápidamente y protege los datos mediante redacción. Al configurar nodos, indexar documentos, aprovechar funciones de búsqueda avanzadas y aplicar redacción, los desarrolladores pueden mejorar drásticamente los flujos de trabajo de gestión documental mientras mantienen estrictos estándares de seguridad.

## Preguntas frecuentes

**P:** ¿Cómo configuro una red de búsqueda distribuida en .NET con GroupDocs?  
**R:** Defina una ruta base y un puerto, luego llame a `SearchNetworkDeployment.Deploy()` para lanzar nodos maestros y de trabajo en diferentes máquinas.

**P:** ¿Puedo realizar búsquedas avanzadas con múltiples parámetros en GroupDocs?  
**R:** Sí—utilice `SearchOptions` para combinar coincidencia difusa, soporte de comodines y resaltado de resultados en una sola consulta.

**P:** ¿Es posible monitorear la actividad de la red en el nodo maestro?  
**R:** Absolutamente—suscríbase a `SearchNetworkNodeEvents` como `IndexingCompleted` y `QueryExecuted` para obtener información en tiempo real.

**P:** ¿Cómo aplico redacción a archivos PDF usando GroupDocs?  
**R:** Inicialice un `Redactor`, cargue el PDF, defina objetos `RedactionPattern` (expresiones regulares o cadenas literales), llame a `Apply` y guarde el documento sanitizado.

**P:** ¿Cuál es la forma más fácil de mejorar el rendimiento de búsqueda en un entorno en red?  
**R:** Indexe completamente su conjunto de documentos antes de las consultas, distribuya nodos para utilizar procesamiento paralelo y ajuste `SearchOptions` para caché y paginación.

---

**Última actualización:** 2026-06-12  
**Probado con:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Dominio maestro de indexación de documentos .NET con GroupDocs.Search: Guía completa](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Dominio maestro de indexación de documentos y consultas de búsqueda avanzadas con GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Dominar GroupDocs Search y Redaction en .NET: Gestión avanzada de documentos](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)