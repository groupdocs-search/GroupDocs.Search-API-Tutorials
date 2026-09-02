---
date: '2026-04-02'
description: Aprende a filtrar por extensión de archivo y buscar solo archivos txt
  con GroupDocs.Redaction para .NET—mejora la eficiencia de la gestión documental.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtrar por extensión de archivo en .NET usando GroupDocs.Redaction
type: docs
url: /es/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filtrar por extensión de archivo en .NET usando GroupDocs.Redaction

Buscar a través de una gran colección de archivos puede resultar abrumador, especialmente cuando solo necesitas resultados de tipos de archivo específicos. En este tutorial descubrirás **cómo filtrar por extensión de archivo** con GroupDocs.Redaction para .NET, lo que te permite buscar solo archivos txt o cualquier otra extensión que elijas. Te guiaremos a través de la configuración de filtros tanto por tipo de archivo como por ruta, para que puedas localizar rápidamente los documentos que necesitas.

## Respuestas rápidas
- **¿Qué hace “filtrar por extensión de archivo”?** Limita una búsqueda a documentos que coinciden con una extensión de archivo dada (p. ej., *.txt).  
- **¿Por qué usar GroupDocs.Redaction para esto?** Proporciona APIs de filtrado integradas que son rápidas y fáciles de integrar.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para pruebas; se requiere una licencia de pago para producción.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **¿Puedo combinar filtros por tipo de archivo y por ruta?** Sí—aplica múltiples filtros para búsquedas altamente precisas.

## Lo que aprenderás
- Cómo **filtrar por extensión de archivo** para que solo se busquen archivos de texto.  
- Cómo configurar **filtros de ruta de archivo** para limitar los resultados a carpetas específicas o patrones de nombres.  
- Consejos para mantener tu índice rápido y eficiente en memoria.

## Requisitos previos

Antes de profundizar, asegúrate de tener:

- **Biblioteca GroupDocs.Redaction** instalada y compatible con tu proyecto .NET.  
- Un entorno de desarrollo como Visual Studio o VS Code.  
- Conocimientos básicos de C# y familiaridad con la estructura de proyectos .NET.

## Configuración de GroupDocs.Redaction para .NET

Primero, agrega la biblioteca a tu proyecto.

**Usando .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Usando Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

O localiza “GroupDocs.Redaction” en la interfaz de NuGet Package Manager y instala la última versión.

### Obtención de licencia

Puedes comenzar con una prueba gratuita o solicitar una licencia temporal. Para proyectos a largo plazo, compra una licencia en el sitio oficial.

### Inicialización básica

Después de instalar el paquete, crea un índice que contendrá referencias a tus documentos:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Guía de implementación

### Función 1: Configurar un filtro para documentos de texto (.txt)

#### Cómo filtrar por extensión de archivo para documentos de texto

1. **Definir el índice y las carpetas de documentos**  
   Establece las rutas donde se encuentran tus archivos de origen:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Crear un índice**  
   Carga todos los archivos de la carpeta de origen en el índice:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Configurar opciones de búsqueda con un filtro de extensión de archivo**  
   Indica al motor que solo considere archivos *.txt:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Ejecutar la búsqueda**  
   Ejecuta una consulta; el filtro garantiza que se ignoren los archivos que no son de texto:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explicación*: El método `Search` devuelve coincidencias que cumplen con el filtro, reduciendo drásticamente el ruido y mejorando el rendimiento.

### Función 2: Filtros de ruta de archivo

#### ¿Por qué usar filtros de ruta de archivo?

A veces necesitas limitar las búsquedas a una carpeta de departamento específica o a un conjunto de archivos que comparten una convención de nombres. Los filtros de ruta te permiten hacer precisamente eso.

1. **Definir el índice y las carpetas de documentos**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Crear un índice**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Configurar opciones de búsqueda con una expresión regular basada en la ruta**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Esta expresión regular coincide con cualquier archivo cuya ruta completa contenga la palabra “Lorem”, permitiéndote apuntar a subcarpetas específicas.

4. **Ejecutar la búsqueda basada en la ruta**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Aplicaciones prácticas
- **Gestión de documentos legales** – Localiza rápidamente los contratos relevantes almacenados como archivos de texto plano.  
- **Investigación académica** – Extrae solo notas de investigación *.txt que pertenecen a una carpeta de proyecto específica.  
- **Informes corporativos** – Filtra los informes internos por ruta de departamento (p. ej., `/Finance/2025/`).  

## Consideraciones de rendimiento
- Indexa solo los tipos de documentos que realmente necesitas; los archivos innecesarios aumentan el tamaño del índice y el tiempo de búsqueda.  
- Mantén tu índice actualizado con una tarea programada que llame a `index.Add()` para archivos nuevos o modificados.  
- Usa expresiones regulares simples; los patrones demasiado complejos pueden ralentizar el motor de búsqueda.  
- Desecha los objetos `Index` cuando ya no sean necesarios para liberar memoria.

## Conclusión
Ahora sabes cómo **filtrar por extensión de archivo** y aplicar **filtros de ruta de archivo** usando GroupDocs.Redaction para .NET. Estas técnicas te brindan un control granular sobre grandes colecciones de documentos, haciendo que las búsquedas sean más rápidas y relevantes. A continuación, experimenta combinando múltiples filtros o integrando la búsqueda en un flujo de trabajo de aplicación más amplio.

## Sección de preguntas frecuentes

**P1: ¿Puedo filtrar documentos que no sean archivos de texto?**  
R1: Sí, GroupDocs.Redaction admite muchos formatos. Cambia el argumento en `CreateFileExtension` a la extensión deseada (p. ej., ".pdf").

**P2: ¿Cómo actualizo mi índice de búsqueda regularmente?**  
R2: Programa un servicio en segundo plano o una tarea cron que ejecute `index.Add()` en los directorios que deseas mantener actualizados.

**P3: ¿Hay un impacto en el rendimiento al filtrar por ruta de archivo?**  
R3: Las expresiones regulares bien optimizadas tienen un impacto mínimo, pero siempre realiza pruebas de rendimiento con tu propio conjunto de datos.

**P4: ¿Puedo combinar múltiples filtros para búsquedas más refinadas?**  
R4: Absolutamente. Puedes encadenar filtros o crear filtros compuestos para dirigirte tanto al tipo de archivo como a la ruta simultáneamente.

**P5: ¿Dónde puedo encontrar más recursos sobre GroupDocs.Redaction?**  
R5: Visita la documentación oficial en [Documentación de GroupDocs](https://docs.groupdocs.com/search/net/) para guías detalladas y referencias de API.

## Preguntas frecuentes

**P: ¿El `SearchDocumentFilter` funciona con archivos cifrados?**  
R: El filtro en sí opera sobre los metadatos del archivo, por lo que los archivos cifrados siguen siendo indexados si proporcionas las credenciales de descifrado necesarias durante la indexación.

**P: ¿Puedo usar comodines en lugar de una expresión regular para filtrar rutas?**  
R: Actualmente la API requiere una expresión regular, pero puedes simular comodines simples (p. ej., `.*` para cualquier carácter).

**P: ¿Qué tan grande puede ser el índice antes de que necesite considerar fragmentación?**  
R: Los índices de varios cientos de gigabytes pueden beneficiarse de dividirse en varios índices lógicos; prueba el rendimiento a medida que tu colección crezca.

**P: ¿Existen métodos incorporados para eliminar documentos del índice?**  
R: Sí—llama a `index.Delete(documentId)` o `index.DeleteAll()` para gestionar entradas obsoletas.

**P: ¿Hay una forma de previsualizar los resultados de búsqueda antes de cargar el documento completo?**  
R: El objeto `SearchResult` incluye información de fragmento que puedes mostrar en la UI sin abrir todo el archivo.

## Recursos
- **Documentación**: [Documentación de GroupDocs](https://docs.groupdocs.com/search/net/)
- **Referencia de API**: [Referencia de API de GroupDocs](https://reference.groupdocs.com/redaction/net)
- **Descarga**: [Descargas de GroupDocs](https://releases.groupdocs.com/search/net/)
- **Soporte gratuito**: [Foro de GroupDocs](https://forum.groupdocs.com/c/search/10)
- **Licencia temporal**: [Licencia temporal de GroupDocs](https://purchase.groupdocs.com/temporary-license)

---

**Última actualización:** 2026-04-02  
**Probado con:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs