---
date: '2026-04-02'
description: Aprende cómo crear un índice de búsqueda en GroupDocs y agregar documentos
  al índice mientras implementas búsqueda facetada usando GroupDocs.Search y GroupDocs.Redaction
  en .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Crear índice de búsqueda GroupDocs con redacción .NET y búsqueda facetada
type: docs
url: /es/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Crear índice de búsqueda GroupDocs con Redaction .NET Búsqueda facetada

En aplicaciones modernas, **crear un índice de búsqueda con GroupDocs** es esencial para una recuperación de documentos rápida y precisa. Ya sea que manejes contratos legales, catálogos de productos o grandes bases de conocimiento, un índice bien construido te permite **agregar documentos al índice** y ejecutar búsquedas facetadas potentes en segundos. Este tutorial te guía a través de todo el proceso—desde la configuración de GroupDocs.Redaction hasta la creación de consultas facetadas simples y complejas—para que puedas ofrecer una experiencia de búsqueda receptiva en tus proyectos .NET.

## Respuestas rápidas
- **¿Cuál es el propósito principal?** Para crear un índice de búsqueda con GroupDocs y habilitar la búsqueda facetada.  
- **¿Qué bibliotecas se requieren?** GroupDocs.Redaction y GroupDocs.Search para .NET.  
- **¿Cómo agrego documentos al índice?** Use `index.Add(documentsFolder)` after initializing the index.  
- **¿Puedo ejecutar consultas complejas?** Sí, combina consultas de objetos con operadores lógicos para filtrado avanzado.  
- **¿Se necesita una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.

## Qué es la búsqueda facetada y por qué usarla con GroupDocs?
La búsqueda facetada permite a los usuarios refinar los resultados aplicando múltiples filtros—como categoría, fecha o autor—simultáneamente. Cuando se combina con **GroupDocs.Redaction**, obtienes contenido seguro y buscable que respeta las reglas de redacción, lo que lo hace ideal para entornos con alta normativa de cumplimiento.

## Requisitos previos

### Bibliotecas requeridas, versiones y dependencias
- **GroupDocs.Redaction .NET** – última versión estable.  
- **GroupDocs.Search .NET** – funciona de la mano con Redaction para indexar.

### Requisitos de configuración del entorno
- **IDE**: Visual Studio 2019 o posterior.  
- **Framework**: .NET Core 3.1, .NET 5 o .NET 6.  
- **Compatibilidad del SO**: Windows, Linux, macOS.

### Prerrequisitos de conocimiento
Habilidades básicas en C# y una comprensión a alto nivel de los conceptos de búsqueda facetada ayudarán, pero la guía paso a paso también es amigable para los principiantes.

## Configuración de GroupDocs.Redaction para .NET

### Información de instalación
Puedes agregar el paquete GroupDocs.Redaction usando cualquiera de los siguientes métodos:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Busca "GroupDocs.Redaction" e instala la última versión.

### Pasos para obtener la licencia
Para desbloquear todas las funciones, comienza con una prueba gratuita o adquiere una licencia permanente:

1. Visita [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) para explorar las opciones de licencia.  
2. Sigue las instrucciones en pantalla para recibir tu archivo de licencia de prueba o comprado.

### Inicialización y configuración básica
Una vez instalado el paquete, inicializa el Redactor en tu aplicación:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Cómo crear índice de búsqueda groupdocs

A continuación dividimos la implementación en dos partes: **Simple Faceted Search** y **Complex Query**. Cada parte muestra cómo **crear un índice de búsqueda groupdocs**, agregar documentos y ejecutar consultas.

### Función 1: Búsqueda facetada simple

**Visión general**  
La búsqueda facetada permite a los usuarios reducir los resultados seleccionando múltiples criterios. Esta sección demuestra un enfoque sencillo usando GroupDocs.Search.

#### Paso 1: Definir carpetas de índice y documentos
Configura las rutas de carpetas donde residirá el índice y donde se encuentran tus documentos fuente.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Paso 2: Crear un índice
```csharp
Index index = new Index(indexFolder);
```

#### Paso 3: Agregar documentos al índice
```csharp
index.Add(documentsFolder);
```

#### Paso 4: Realizar una búsqueda de consulta de texto
Ejecuta una consulta de texto básica contra el campo **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Paso 5: Ejecutar una búsqueda de consulta de objeto
Utiliza consultas orientadas a objetos para un control más fino.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Función 2: Consulta compleja

**Visión general**  
Cuando necesitas combinar múltiples filtros—como patrones de nombre de archivo y coincidencias de frases—puedes construir una consulta compleja usando operadores lógicos.

#### Paso 1: Definir carpetas de índice y documentos
Reutiliza la misma estructura de carpetas para un escenario más avanzado.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Paso 2: Crear un índice y agregar documentos
(Ver pasos 2‑3 del ejemplo simple; permanecen igual.)

#### Paso 3: Ejecutar búsqueda de consulta de texto
Ejecuta una consulta de texto compuesta que combina criterios de nombre de archivo y contenido.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Paso 4: Construir y ejecutar consultas de objeto
Construye la misma lógica programáticamente.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Continúa combinando frases, rangos y operadores booleanos para coincidir con tus reglas de negocio exactas.

## Aplicaciones prácticas

1. **Plataformas de comercio electrónico** – Filtra productos por categoría, precio y valoración.  
2. **Sistemas de gestión documental** – Localiza contratos por autor, fecha o nivel de confidencialidad.  
3. **Portales de contenido** – Permite a los lectores profundizar por etiquetas, temas y fechas de publicación.

## Consideraciones de rendimiento

- **Actualización del índice**: Re‑indexa regularmente archivos nuevos o actualizados para mantener la búsqueda rápida.  
- **Gestión de memoria**: Desecha los objetos `Index` cuando termines, especialmente para conjuntos de datos grandes.  
- **Indexación asíncrona**: Usa `Task.Run` o servicios en segundo plano para evitar congelaciones de la UI durante una indexación intensiva.

## Problemas comunes y soluciones

| Problema | Solución |
|----------|----------|
| **Índice no encontrado** | Verifica la ruta `indexFolder` y asegura que la carpeta tenga permisos de escritura. |
| **No se devolvieron resultados** | Verifica que los campos que consultas (p.ej., `Content`, `Filename`) estén indexados. |
| **Errores de falta de memoria** | Procesa los documentos en lotes y considera aumentar el tamaño del heap del GC de .NET. |

## Preguntas frecuentes

**Q: ¿Qué es la búsqueda facetada?**  
**A:** La búsqueda facetada permite a los usuarios refinar los resultados usando múltiples filtros independientes como categoría, fecha o autor.

**Q: ¿Cómo manejo conjuntos de datos grandes con GroupDocs.Search?**  
**A:** Utiliza indexación incremental, procesamiento por lotes y operaciones asíncronas para mantener bajo el uso de memoria y alta el rendimiento.

**Q: ¿Puedo integrar funcionalidades de GroupDocs en aplicaciones .NET existentes?**  
**A:** Sí, las bibliotecas están diseñadas para una integración sin problemas con cualquier proyecto .NET.

**Q: ¿Cuáles son algunos problemas comunes con la búsqueda facetada?**  
**A:** La sintaxis de consultas complejas y asegurar que todos los campos relevantes estén indexados son desafíos típicos; pruebas adecuadas y el mantenimiento del índice los mitigan.

**Q: ¿Cómo obtengo una licencia temporal para GroupDocs?**  
**A:** Visita la [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) para solicitar una licencia de prueba que desbloquea la funcionalidad completa durante la evaluación.

## Recursos
- **Documentación**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Referencia de API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Última actualización:** 2026-04-02  
**Probado con:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Autor:** GroupDocs