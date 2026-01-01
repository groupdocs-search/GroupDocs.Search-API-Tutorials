---
date: '2025-12-19'
description: Aprende a agregar documentos al índice y habilitar la búsqueda basada
  en fragmentos en Java usando GroupDocs.Search, mejorando el rendimiento para conjuntos
  de documentos grandes.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Agregar documentos al índice con búsqueda basada en fragmentos en Java
type: docs
url: /es/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Agregar documentos al índice con búsqueda basada en fragmentos en Java

En el mundo actual impulsado por los datos, poder **agregar documentos al índice** rápidamente y luego realizar búsquedas basadas en fragmentos es esencial para cualquier aplicación que maneje grandes colecciones de archivos. Ya sea que estés trabajando con contratos legales, archivos de soporte al cliente o enormes bibliotecas de investigación, este tutorial muestra exactamente cómo configurar GroupDocs.Search para Java para que puedas indexar documentos de manera eficiente y recuperar información relevante en fragmentos manejables.

## Lo que aprenderás
- Cómo crear un índice de búsqueda en una carpeta especificada.  
- Pasos para **agregar documentos al índice** desde múltiples ubicaciones.  
- Configurar opciones de búsqueda para habilitar la búsqueda basada en fragmentos.  
- Realizar búsquedas iniciales y subsecuentes basadas en fragmentos.  
- Escenarios del mundo real donde la búsqueda de documentos basada en fragmentos destaca.

## Respuestas rápidas
- **¿Cuál es el primer paso?** Crear una carpeta de índice de búsqueda.  
- **¿Cómo incluyo muchos archivos?** Usa `index.add()` para cada carpeta de documentos.  
- **¿Qué opción habilita la búsqueda por fragmentos?** `options.setChunkSearch(true)`.  
- **¿Puedo continuar la búsqueda después del primer fragmento?** Sí, llama a `index.searchNext()` con el token.  
- **¿Necesito una licencia?** Una prueba gratuita o licencia temporal funciona para desarrollo; se requiere una licencia completa para producción.

## Requisitos previos
Para seguir esta guía, asegúrate de tener:

- **Bibliotecas requeridas**: GroupDocs.Search para Java 25.4 o posterior.  
- **Configuración del entorno**: Un Java Development Kit (JDK) compatible instalado.  
- **Conocimientos previos**: Programación básica en Java y familiaridad con Maven.

## Configuración de GroupDocs.Search para Java
Para comenzar, integra GroupDocs.Search en tu proyecto usando Maven:

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

Alternativamente, descarga la última versión desde [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
Para probar GroupDocs.Search:

- **Prueba gratuita** – prueba las funciones principales sin compromiso.  
- **Licencia temporal** – acceso extendido para desarrollo.  
- **Compra** – licencia completa para uso en producción.

### Inicialización y configuración básica
Crea un índice en la carpeta donde deseas que vivan los datos buscables:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Cómo agregar documentos al índice
Ahora que el índice existe, el siguiente paso lógico es **agregar documentos al índice** desde las ubicaciones donde se almacenan tus archivos.

### 1. Creación de un índice
**Visión general**: Configura un directorio para el índice de búsqueda.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Agregar documentos al índice
**Visión general**: Obtén archivos de varias carpetas fuente.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Configuración de opciones de búsqueda para búsqueda por fragmentos
Habilita la búsqueda basada en fragmentos ajustando el objeto de opciones.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Realizar búsqueda inicial basada en fragmentos
Ejecuta la primera consulta usando las opciones habilitadas para fragmentos.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuar la búsqueda basada en fragmentos
Itera a través de los fragmentos restantes hasta que la búsqueda se complete.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## ¿Por qué usar búsqueda basada en fragmentos?
La búsqueda basada en fragmentos divide colecciones masivas de documentos en piezas manejables, reduciendo la presión de memoria y acelerando los tiempos de respuesta. Es especialmente beneficiosa cuando:

1. **Los equipos legales** necesitan localizar cláusulas específicas en miles de contratos.  
2. **Los portales de soporte al cliente** deben mostrar artículos relevantes de la base de conocimientos al instante.  
3. **Los investigadores** examinan conjuntos de datos extensos sin cargar archivos completos en memoria.

## Consideraciones de rendimiento
- **Gestión de memoria** – Asigna suficiente espacio de heap (`-Xmx`) para índices grandes.  
- **Monitoreo de recursos** – Vigila el uso de CPU durante las operaciones de indexado y búsqueda.  
- **Mantenimiento del índice** – Reconstruye o limpia periódicamente el índice para descartar datos obsoletos.

## Errores comunes y solución de problemas
| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| `OutOfMemoryError` during indexing | Tamaño de heap demasiado bajo | Incrementa el heap de JVM (`-Xmx2g` o superior) |
| No results returned | Token de fragmento no procesado | Asegúrate de que el bucle `while` se ejecute hasta que `getNextChunkSearchToken()` sea `null` |
| Slow search performance | Índice no optimizado | Ejecuta `index.optimize()` después de adiciones masivas |

## Preguntas frecuentes

**Q: ¿Qué es la búsqueda basada en fragmentos?**  
A: La búsqueda basada en fragmentos divide el conjunto de datos en piezas más pequeñas, permitiendo consultas eficientes sobre grandes volúmenes de datos sin cargar documentos completos en memoria.

**Q: ¿Cómo actualizo mi índice con archivos nuevos?**  
A: Simplemente llama a `index.add()` con la ruta a los nuevos documentos; el índice los incorporará automáticamente.

**Q: ¿Puede GroupDocs.Search manejar diferentes formatos de archivo?**  
A: Sí, soporta PDFs, DOCX, XLSX, PPTX y muchos otros formatos comunes.

**Q: ¿Cuáles son los cuellos de botella típicos de rendimiento?**  
A: Las limitaciones de memoria y los índices no optimizados son los más comunes; asigna suficiente heap y optimiza el índice regularmente.

**Q: ¿Dónde puedo encontrar documentación más detallada?**  
A: Visita la documentación oficial de [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) para guías detalladas y referencias de API.

## Recursos
- **Documentación**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referencia de API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Descarga**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Soporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licencia temporal**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última actualización:** 2025-12-19  
**Probado con:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---