---
date: '2026-02-21'
description: Aprende cómo agregar documentos al índice y aumentar el rendimiento de
  búsqueda con la búsqueda basada en fragmentos en Java usando GroupDocs.Search, optimizando
  la memoria del índice de búsqueda de Java para conjuntos de documentos grandes.
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

En aplicaciones modernas que necesitan **agregar documentos al índice** rápidamente y luego realizar consultas rápidas basadas en fragmentos, querrás una solución que escale sin agotar la memoria. Este tutorial te guía a través de la configuración de GroupDocs.Search para Java, la adición de múltiples carpetas de documentos y la configuración del motor para **aumentar el rendimiento de búsqueda** mientras mantienes bajo control el uso de **memoria del índice de búsqueda java**. Ya sea que estés indexando contratos legales, tickets de soporte o artículos de investigación, los pasos a continuación te proporcionarán una implementación lista para producción.

## Respuestas rápidas
- **¿Cuál es el primer paso?** Crear una carpeta de índice de búsqueda.  
- **¿Cómo incluyo muchos archivos?** Usa `index.add()` para cada carpeta de documentos.  
- **¿Qué opción habilita la búsqueda por fragmentos?** `options.setChunkSearch(true)`.  
- **¿Puedo seguir buscando después del primer fragmento?** Sí, llama a `index.searchNext()` con el token.  
- **¿Necesito una licencia?** Una prueba gratuita o una licencia temporal funciona para desarrollo; se requiere una licencia completa para producción.  

## Lo que aprenderás
- Cómo crear un índice de búsqueda en una carpeta especificada.  
- Pasos para **agregar documentos al índice** desde múltiples ubicaciones.  
- Configuración de opciones de búsqueda para habilitar la búsqueda basada en fragmentos.  
- Realización de búsquedas iniciales y subsecuentes basadas en fragmentos.  
- Escenarios del mundo real donde la búsqueda de documentos basada en fragmentos destaca.  

## Requisitos previos
Para seguir esta guía, asegúrate de contar con:

- **Bibliotecas requeridas**: GroupDocs.Search para Java 25.4 o posterior.  
- **Configuración del entorno**: Un JDK (Java Development Kit) compatible instalado.  
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

### Adquisición de licencia
Para probar GroupDocs.Search:

- **Prueba gratuita** – prueba las funciones principales sin compromiso.  
- **Licencia temporal** – acceso extendido para desarrollo.  
- **Compra** – licencia completa para uso en producción.

### Inicialización y configuración básicas
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
**Descripción general**: Configura un directorio para el índice de búsqueda.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Agregar documentos al índice
**Descripción general**: Importa archivos desde varias carpetas de origen.

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
Ejecuta la primera consulta usando las opciones con fragmentos habilitados.

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

1. **Los equipos legales** necesitan localizar cláusulas específicas entre miles de contratos.  
2. **Los portales de soporte al cliente** deben mostrar artículos relevantes de la base de conocimientos al instante.  
3. **Los investigadores** examinan conjuntos de datos extensos sin cargar archivos completos en memoria.

## Cómo este enfoque **aumenta el rendimiento de búsqueda**
Al buscar fragmentos más pequeños en lugar de archivos completos, el motor puede:

- Omitir secciones irrelevantes temprano, reduciendo ciclos de CPU.  
- Mantener solo el fragmento activo en memoria, lo que disminuye directamente el consumo de **memoria del índice de búsqueda java**.  
- Paralelizar el procesamiento de fragmentos en máquinas multinúcleo para obtener resultados más rápidos.

## Gestión de la **memoria del índice de búsqueda java**
Aunque la búsqueda basada en fragmentos ya reduce la huella de memoria, puedes afinar aún más la JVM:

- Asigna suficiente heap (`-Xmx2g` o superior) según el tamaño del índice.  
- Usa `index.optimize()` después de adiciones masivas para comprimir la estructura del índice.  
- Monitorea las pausas del GC con herramientas como VisualVM para evitar picos de latencia.

## Consideraciones de rendimiento
- **Gestión de memoria** – Asigna suficiente espacio de heap (`-Xmx`) para índices grandes.  
- **Monitoreo de recursos** – Vigila el uso de CPU durante las operaciones de indexado y búsqueda.  
- **Mantenimiento del índice** – Reconstruye o limpia periódicamente el índice para descartar datos obsoletos.

## Errores comunes y solución de problemas
| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| `OutOfMemoryError` durante el indexado | Tamaño de heap insuficiente | Incrementa el heap de la JVM (`-Xmx2g` o superior) |
| No se devuelven resultados | Token de fragmento no procesado | Asegúrate de que el bucle `while` se ejecute hasta que `getNextChunkSearchToken()` sea `null` |
| Rendimiento de búsqueda lento | Índice no optimizado | Ejecuta `index.optimize()` después de adiciones masivas |

## Preguntas frecuentes

**P: ¿Qué es la búsqueda basada en fragmentos?**  
R: La búsqueda basada en fragmentos divide el conjunto de datos en piezas más pequeñas, permitiendo consultas eficientes sobre grandes volúmenes de datos sin cargar documentos completos en memoria.

**P: ¿Cómo actualizo mi índice con archivos nuevos?**  
R: Simplemente llama a `index.add()` con la ruta a los nuevos documentos; el índice los incorporará automáticamente.

**P: ¿GroupDocs.Search puede manejar diferentes formatos de archivo?**  
R: Sí, admite PDFs, DOCX, XLSX, PPTX y muchos otros formatos comunes.

**P: ¿Cuáles son los cuellos de botella de rendimiento típicos?**  
R: Las limitaciones de memoria y los índices no optimizados son los más comunes; asigna suficiente heap y optimiza el índice regularmente.

**P: ¿Dónde puedo encontrar documentación más detallada?**  
R: Visita la documentación oficial de [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) para guías en profundidad y referencias de API.

**P: ¿La búsqueda basada en fragmentos funciona con PDFs encriptados?**  
R: Sí, siempre que proporciones la contraseña mediante la sobrecarga de API correspondiente.

**P: ¿Cómo puedo monitorear el progreso del indexado?**  
R: Usa la sobrecarga `Index.add()` que devuelve un objeto `Progress` o conecta callbacks de registro.

## Recursos
- **Documentación**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referencia de API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Descarga**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Soporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licencia temporal**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última actualización:** 2026-02-21  
**Probado con:** GroupDocs.Search 25.4 para Java  
**Autor:** GroupDocs  

---