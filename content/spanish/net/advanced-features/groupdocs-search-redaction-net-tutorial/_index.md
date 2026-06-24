---
date: '2026-04-04'
description: Aprende a buscar documentos legales y gestionar índices usando GroupDocs.Search,
  e integrar la redacción de registros médicos con GroupDocs.Redaction en .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Buscar documentos legales con GroupDocs Search & Redaction para .NET
type: docs
url: /es/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Buscar documentos legales con GroupDocs Search & Redaction en .NET

En el entorno actual impulsado por datos, **buscar documentos legales** de forma rápida y segura es un requisito crítico para cualquier organización. Ya sea que esté manejando contratos, presentaciones judiciales o informes de cumplimiento, GroupDocs.Search le brinda un índice rápido y escalable, mientras que GroupDocs.Redaction garantiza que la información sensible permanezca oculta. Este tutorial le guía a través de la configuración de un índice buscable, la adición de documentos desde múltiples carpetas y la configuración de la redacción para que pueda buscar de forma segura registros médicos y otros archivos confidenciales.

## Respuestas rápidas
- **¿Qué hace GroupDocs.Search?** Crea un índice buscable de texto completo para una amplia gama de formatos de documento.  
- **¿Puedo redactar información antes de buscar?** Sí – use GroupDocs.Redaction para ocultar o eliminar datos sensibles.  
- **¿Cómo añado documentos al índice?** Llame a `index.Add("folderPath")` para cada carpeta que desee incluir.  
- **¿Qué tipos de archivo son compatibles?** PDFs, DOCX, PPTX, TXT y muchos más.  
- **¿Necesito una licencia para producción?** Hay una prueba temporal disponible; se requiere una licencia permanente para uso comercial.

## Requisitos previos
Para seguir este tutorial, asegúrese de tener:
- SDK de .NET Core (3.1 o posterior) instalado.
- Visual Studio Code, Visual Studio o cualquier otro IDE que soporte .NET.
- Familiaridad básica con la programación en C#.

### Adquisición de licencia
Puede comenzar con una prueba gratuita de ambas bibliotecas. Para un uso prolongado, considere adquirir una licencia temporal o comprar una en el [sitio web de GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Instalación de los paquetes requeridos

**Instalación de GroupDocs.Search:**  
Usando **.NET CLI**, ejecute:
```bash
dotnet add package GroupDocs.Search
```
Alternativamente, use la consola del Administrador de paquetes en Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**Instalación de GroupDocs.Redaction:**  
- Use .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- O, a través del Administrador de paquetes:
```powershell
Install-Package GroupDocs.Redaction
```

Visite la interfaz de usuario del Administrador de paquetes NuGet y busque "GroupDocs.Redaction" para instalarlo si prefiere una GUI.

## Configurar la configuración del redactor
Antes de comenzar a redactar, puede que desee ajustar el comportamiento del redactor (p. ej., establecer el color de redacción o definir patrones personalizados). El siguiente fragmento muestra la inicialización básica:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Consejo profesional:** Ajuste `redactorSettings` para que coincida con las políticas de cumplimiento de su organización (p. ej., reemplace texto con cuadros negros, aplique OCR antes de la redacción, etc.).

## Guía de implementación

### ¿Cómo buscar documentos legales?
Crear un índice buscable es la base para la recuperación rápida de documentos legales. GroupDocs.Search le permite apuntar a cualquier carpeta, crear un índice y luego ejecutar consultas complejas a través de miles de archivos.

### ¿Cómo añadir documentos al índice?
Añadir documentos es sencillo: simplemente indique a la biblioteca las carpetas que contienen sus archivos. Puede agregar múltiples carpetas, lo cual es útil cuando su corpus legal está distribuido en diferentes ubicaciones.

#### Creación y gestión de un índice
**Visión general:**  
Crear un índice es el primer paso hacia operaciones de búsqueda de documentos eficientes. GroupDocs.Search le permite crear un índice buscable en cualquier directorio que elija, facilitando la recuperación rápida de documentos.

##### Paso 1: Crear el índice
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Explicación:* `Index` inicializa un índice de búsqueda en el directorio especificado. Asegúrese de que la ruta refleje la estructura de carpetas de su proyecto.

##### Paso 2: Añadir documentos a un índice
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Explicación:* El método `Add` escanea la carpeta dada e incluye cada documento compatible en el índice. Use esto para **añadir documentos al índice** desde múltiples fuentes, como contratos, expedientes de casos o registros médicos.

### Recuperación y visualización de informes de indexación
**Visión general:**  
Los informes de indexación le brindan información sobre cuántos documentos fueron procesados, el recuento total de términos y el tamaño de almacenamiento, métricas esenciales para la optimización del rendimiento.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Explicación:* `GetIndexingReports` devuelve una matriz de informes que detallan el proceso de indexación, ayudándole a monitorear y optimizar el rendimiento.

## Aplicaciones prácticas
1. **Gestión de documentos legales:** Automatice la indexación de expedientes de casos para la recuperación instantánea de estatutos, escritos y sentencias.  
2. **Sistema de registros médicos:** Busque registros de pacientes mientras preserva la privacidad usando GroupDocs.Redaction para ocultar PHI.  
3. **Portal corporativo de RR.HH.:** Combine archivos de empleados buscables con redacción para proteger datos personales.

## Consideraciones de rendimiento
- **Optimización del tamaño del índice:** Depure periódicamente las entradas obsoletas y reconstruya el índice para mantenerlo ligero.  
- **Gestión de memoria:** Aproveche el recolector de basura de .NET; libere los objetos `Index` cuando ya no sean necesarios.  
- **Mejores prácticas de escalabilidad:** Almacene el índice en un almacenamiento SSD rápido y considere dividir grandes corpus en múltiples índices.

## Preguntas frecuentes

**P: ¿Cuáles son los usos principales de GroupDocs.Search?**  
R: Es ideal para crear índices buscables a partir de grandes colecciones de documentos, permitiendo una recuperación rápida de archivos legales y médicos.

**P: ¿Cómo garantiza GroupDocs.Redaction la privacidad de los datos?**  
R: Le permite definir patrones de redacción que eliminan o ocultan permanentemente la información sensible antes de que el documento sea indexado o compartido.

**P: ¿Puedo usar estas bibliotecas en un entorno cloud?**  
R: Sí, ambas bibliotecas funcionan en Azure, AWS o cualquier despliegue .NET en contenedores con la licencia adecuada.

**P: ¿Qué formatos de archivo son compatibles con GroupDocs.Search?**  
R: PDFs, Word, Excel, PowerPoint, TXT, HTML y muchos más formatos empresariales.

**P: ¿Cómo soluciono errores de indexación?**  
R: Verifique las rutas de las carpetas, revise los permisos de los archivos y examine la salida de consola de `IndexingReport` para códigos de error específicos.

## Recursos
- **Documentación:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **Referencia de API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Descarga:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Soporte gratuito:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licencia temporal:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Última actualización:** 2026-04-04  
**Probado con:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 para .NET  
**Autor:** GroupDocs