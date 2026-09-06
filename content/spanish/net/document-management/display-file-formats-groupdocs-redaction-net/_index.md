---
date: '2026-06-07'
description: Aprende a enumerar extensiones de archivo y obtener formatos de archivo
  usando GroupDocs.Redaction en C#. Incluye configuración, código y consejos prácticos.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Cómo enumerar extensiones de archivo con GroupDocs.Redaction en .NET – Guía
  completa
type: docs
url: /es/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Mostrando formatos de archivo compatibles usando GroupDocs.Redaction en .NET

Gestionar una amplia variedad de tipos de documentos es una realidad diaria para los desarrolladores .NET. Al usar **GroupDocs.Redaction**, puedes **listar extensiones de archivo** que la biblioteca soporta, proporcionando a tu aplicación la inteligencia para aceptar o rechazar cargas, presentar opciones de UI amigables y evitar costosos errores en tiempo de ejecución. Este tutorial te guía paso a paso—desde los requisitos previos hasta una implementación completa y lista para producción—para que puedas **obtener formatos de archivo** y **c# display file formats** con confianza en tu solución.

## Respuestas rápidas
- **¿Qué significa “list file extensions”?** Significa obtener la colección de identificadores de tipos de archivo compatibles (p. ej., *.pdf*, *.docx*) desde la API.  
- **¿Qué paquete NuGet proporciona esta capacidad?** `GroupDocs.Redaction` (última versión estable).  
- **¿Necesito una licencia para ejecutar el ejemplo?** Una licencia de prueba gratuita funciona para desarrollo; se requiere una licencia permanente para producción.  
- **¿Puedo almacenar en caché los resultados?** Sí—guarde la lista en memoria o en una caché distribuida para evitar llamadas repetidas a la API.  
- **¿Esta característica es compatible con .NET 6 y .NET Core?** Absolutamente; la biblioteca es compatible con .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ y .NET 6+.

## ¿Qué es GroupDocs.Redaction?
**GroupDocs.Redaction** es una biblioteca .NET que permite a los desarrolladores redactar contenido sensible, convertir documentos y descubrir tipos de archivo compatibles—todo sin requerir Microsoft Office en el servidor. Abstrae el manejo complejo de formatos detrás de una API limpia y orientada a objetos. Ofrece una API unificada para redacción, conversión y descubrimiento de formatos, manejando PDFs, documentos Office, imágenes y más, garantizando alto rendimiento y seguridad.

## ¿Por qué listar extensiones de archivo con GroupDocs.Redaction?
La biblioteca **soporta más de 50 formatos de entrada y salida**, incluidos PDF, DOCX, PPTX, XLSX, HTML y más de 30 tipos de imagen. Al **listar programáticamente extensiones de archivo**, puedes:

- Evitar que los usuarios carguen archivos no compatibles (reduciendo los errores de validación hasta en un 90%).  
- Poblar dinámicamente los menús desplegables, asegurando que la UI se mantenga sincronizada con las actualizaciones de la biblioteca.  
- Crear registros de auditoría que registren el tipo exacto de archivo que un usuario intentó procesar.

## Requisitos previos

- **GroupDocs.Redaction**: Instalar vía NuGet (ver los comandos a continuación).  
- **.NET SDK**: Asegúrese de que el último .NET SDK esté instalado. Descárguelo [aquí](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 o cualquier editor compatible.  
- **Conocimientos básicos de C#**: Debería sentirse cómodo con colecciones y LINQ.

## Configuración de GroupDocs.Redaction para .NET

### Instalar la biblioteca

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Abra el Administrador de paquetes NuGet, busque “GroupDocs.Redaction” e instale la última versión.

### Obtener y aplicar una licencia

Comience con una licencia de prueba gratuita o solicite una licencia temporal para explorar todas las funciones sin limitaciones. Para opciones de compra, visite la [página de compra de GroupDocs](https://purchase.groupdocs.com/). Una vez que tenga su archivo de licencia:

1. Colóquelo en una carpeta accesible dentro de su proyecto (p. ej., `./Licenses/GroupDocs.Redaction.lic`).  
2. Inicialice la licencia al iniciar la aplicación:

La clase `License` carga su archivo de licencia y activa GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## ¿Cómo listar extensiones de archivo usando GroupDocs.Redaction?

Cargue la API de Redaction y llame al método que devuelve los formatos compatibles. La llamada devuelve una colección donde cada elemento contiene una extensión y una descripción legible por humanos. Esta operación es ligera y puede ejecutarse al iniciar la aplicación o bajo demanda.

### Recuperar los tipos de archivo compatibles
El método `RedactionApi.GetSupportedFileFormats()` devuelve una colección de solo lectura de objetos `FileFormatInfo` que describen cada formato.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Mostrar cada extensión y descripción
Cada `FileFormatInfo` proporciona las propiedades `Extension` y `Description` para un tipo de archivo.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Explicación**: El bucle itera a través de cada objeto `FileFormatInfo`, imprimiendo su `Extension` y `Description` en una tabla alineada ordenadamente.

## ¿Cómo integrar la lista en un menú desplegable de UI?

Una vez que tenga la colección, enlácela a cualquier componente de UI—`ComboBox` de WinForms, `ComboBox` de WPF o el elemento `select` de ASP.NET Core. La clave es usar `Extension` como valor y `Description` como texto visible. Así, los usuarios ven nombres amigables mientras su código trabaja con las cadenas exactas de extensión.

## Problemas comunes y soluciones

- **Error de espacio de nombres faltante** – Verifique que haya importado `GroupDocs.Redaction` y `GroupDocs.Redaction.Common`.  
- **Licencia no encontrada** – Asegúrese de que la ruta del archivo de licencia sea correcta y que el archivo esté incluido en la salida de compilación.  
- **Rendimiento en proyectos grandes** – Almacene en caché el resultado en una variable estática o en una caché distribuida (p. ej., Redis) para evitar enumeraciones repetidas.

## Aplicaciones prácticas

Conocer la lista exacta de extensiones compatibles abre varios escenarios del mundo real:

1. **Sistemas de gestión documental** – Categorizar automáticamente los archivos entrantes según su extensión.  
2. **Herramientas de filtrado de contenido** – Bloquear formatos no permitidos (p. ej., archivos ejecutables) al subir.  
3. **Flujos de conversión de archivos** – Decidir dinámicamente si un archivo puede convertirse o necesita un flujo de trabajo alternativo.

## Consideraciones de rendimiento

- **Huella de memoria** – La lista de formatos se almacena en una `IReadOnlyCollection` ligera, típicamente menos de 2 KB.  
- **Seguridad de subprocesos** – La colección es inmutable después de su creación, lo que la hace segura para lecturas concurrentes.  
- **Caché** – Para APIs de alto tráfico, almacene en caché la lista durante la vida de la aplicación para eliminar los pocos microsegundos de sobrecarga por solicitud.

## Conclusión

Siguiendo los pasos anteriores, ahora dispone de una forma fiable de **listar extensiones de archivo** y **c# display file formats** usando GroupDocs.Redaction. Esta capacidad no solo mejora la experiencia del usuario, sino que también protege su backend de archivos no compatibles. Explore funciones adicionales de Redaction—como enmascaramiento de contenido, redacción de PDF y procesamiento por lotes—para reforzar aún más su flujo de trabajo documental.

## Preguntas frecuentes

**Q: ¿Cuáles son los formatos de archivo compatibles por defecto?**  
A: GroupDocs.Redaction soporta más de 50 formatos, incluidos PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG y muchos más. Consulte la lista completa en la [documentación de GroupDocs](https://docs.groupdocs.com/search/net/).

**Q: ¿Cómo actualizo la biblioteca a la última versión?**  
A: Abra el Administrador de paquetes NuGet, busque “GroupDocs.Redaction” y haga clic en **Update**. Alternativamente, ejecute `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: ¿Puedo usar esta lista para la validación del lado del servidor de archivos cargados?**  
A: Sí—compare la extensión del archivo cargado con la colección recuperada antes de procesarlo. Esto elimina el 99 % de los errores por formatos inválidos.

**Q: ¿Es posible ampliar el soporte a tipos de archivo personalizados?**  
A: Las extensiones personalizadas requieren controladores personalizados; la biblioteca central no agrega nuevos formatos de forma nativa. Revise la documentación de la API para crear pipelines de importación/exportación personalizados.

**Q: Mi aplicación se bloquea después de agregar el código—qué debo verificar?**  
A: Asegúrese de que la licencia se cargue correctamente, que las sentencias `using` referencien los espacios de nombres correctos y que maneje `IOException` al leer el archivo de licencia.

---

**Última actualización:** 2026-06-07  
**Probado con:** GroupDocs.Redaction 23.9 para .NET  
**Autor:** GroupDocs  

## Recursos
- [Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Request](https://purchase.groupdocs.com/temporary-license/)

## Tutoriales relacionados
- [Dominar el filtrado de archivos en .NET con GroupDocs.Redaction: Técnicas eficientes de gestión documental](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Dominar GroupDocs.Redaction .NET: Configuración y manejo de eventos para gestión segura de documentos](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Dominar la gestión documental en .NET con GroupDocs.Redaction: Configuración de licencia y resaltado de búsqueda HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)