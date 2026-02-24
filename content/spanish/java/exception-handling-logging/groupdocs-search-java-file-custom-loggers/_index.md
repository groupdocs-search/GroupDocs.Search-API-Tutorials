---
date: '2026-02-24'
description: Aprende cómo crear un registrador personalizado, establecer el tamaño
  máximo del registro y configurar el registrador de consola o de archivo en GroupDocs.Search
  para Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Cómo crear un registrador personalizado y limitar el tamaño del archivo de
  registro con GroupDocs.Search Java
type: docs
url: /es/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

.# Limitar el tamaño del archivo de registro con los registradores de GroupDocs.Search Java

En esta guía crearás implementaciones de **custom logger** y aprenderás a **limit log file size** mientras usas GroupDocs.Search para Java. Controlar el crecimiento de los registros es crucial para la indexación de documentos a gran escala, y los registradores incorporados te permiten **set max log size**, **roll over log file**, o cambiar a un **use console logger** para obtener retroalimentación instantánea. Revisemos la configuración completa, desde la configuración de Maven hasta la ejecución de una consulta de búsqueda, y veamos cómo **add documents index** con el registrador activo.

## Respuestas rápidas
- **¿Qué significa “limit log file size”?** Limita el tamaño máximo de un archivo de registro, evitando un crecimiento descontrolado en el disco.  
- **¿Qué registrador permite limitar el tamaño del archivo de registro?** El `FileLogger` incorporado acepta un parámetro de tamaño máximo.  
- **¿Cómo uso console logger java?** Instancia `ConsoleLogger` y configúralo en `IndexSettings`.  
- **¿Necesito una licencia para GroupDocs.Search?** Una prueba funciona para evaluación; se requiere una licencia comercial para producción.  
- **¿Cuál es el primer paso?** Añade la dependencia de GroupDocs.Search a tu proyecto Maven.  

## ¿Qué es limitar el tamaño del archivo de registro?
Limitar el tamaño del archivo de registro significa configurar el registrador de modo que, una vez que el archivo alcanza un umbral predefinido (p. ej., 4 MB), deje de crecer o se renueve. Esto mantiene predecible la huella de almacenamiento de tu aplicación y evita la degradación del rendimiento.

## ¿Por qué usar registradores de archivo y personalizados con GroupDocs.Search?
- **Auditabilidad:** Mantén un registro permanente de los eventos de indexación y búsqueda.  
- **Depuración:** Identifica rápidamente problemas revisando registros concisos.  
- **Flexibilidad:** Elige entre registros persistentes en archivo y salida instantánea en consola (`use console logger`).  

## Requisitos previos
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 o superior, IDE (IntelliJ IDEA, Eclipse, etc.).  
- Conocimientos básicos de Java y Maven.  

## Configuración de GroupDocs.Search para Java

Añade la biblioteca a tu proyecto usando uno de los métodos siguientes.

**Configuración Maven:**

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

**Descarga directa:**  
Descarga el JAR más reciente desde el sitio oficial: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
Obtén una prueba o compra una licencia a través de la [licensing page](https://purchase.groupdocs.com/temporary-license/).

## Cómo crear un registrador personalizado para GroupDocs.Search
GroupDocs.Search te permite conectar cualquier implementación de la interfaz `ILogger`. Al extender `FileLogger` o `ConsoleLogger`, puedes añadir comportamiento extra, como renovar el archivo de registro o reenviar mensajes a un servicio de monitoreo remoto. Esta flexibilidad es la razón por la que muchos equipos **create custom logger** soluciones que se ajustan a sus necesidades operativas.

## Cómo limitar el tamaño del archivo de registro con File Logger
A continuación se muestra una guía paso a paso que indica cómo **configure file logger** para que el archivo de registro nunca supere el tamaño que especifiques.

### 1️⃣ Importar paquetes necesarios
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Configurar Index Settings con File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Crear o cargar el índice
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Añadir documentos al índice
```java
index.add(documentsFolder);
```

### 5️⃣ Ejecutar una consulta de búsqueda
```java
SearchResult result = index.search(query);
```

**Punto clave:** El segundo argumento del constructor de `FileLogger` (`4.0`) define el **set max log size** en megabytes, abordando directamente el requisito de **limit log file size**.

## Cómo usar console logger java
Si prefieres retroalimentación inmediata en la terminal, sustituye el file logger por un console logger.

### 1️⃣ Importar el Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Configurar Index Settings con Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Crear o cargar el índice
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Añadir documentos y ejecutar una búsqueda
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Consejo:** El console logger es ideal durante el desarrollo porque imprime cada entrada de registro al instante, ayudándote a verificar que la indexación y la búsqueda se comporten como se espera.

## Aplicaciones prácticas
1. **Sistemas de gestión documental:** Mantén auditorías de cada documento indexado.  
2. **Motores de búsqueda empresarial:** Supervisa el rendimiento de consultas y tasas de error en tiempo real.  
3. **Software legal y de cumplimiento:** Registra los términos de búsqueda para informes regulatorios.

## Consideraciones de rendimiento
- **Tamaño del registro:** Con **set max log size**, evitas un uso excesivo de disco que podría ralentizar tu aplicación.  
- **Registro asíncrono:** Si necesitas mayor rendimiento, considera envolver el registrador en una cola async (fuera del alcance de esta guía).  
- **Gestión de memoria:** Libera objetos `Index` grandes cuando ya no sean necesarios para mantener baja la huella de la JVM.

## Problemas comunes y soluciones
- **Ruta del registro no accesible:** Verifica que el directorio exista y que la aplicación tenga permisos de escritura.  
- **El registrador no se dispara:** Asegúrate de llamar a `settings.setLogger(...)` *antes* de crear el objeto `Index`.  
- **Salida de consola ausente:** Confirma que estás ejecutando la aplicación en una terminal que muestra `System.out`.

## Preguntas frecuentes

**Q:** ¿Qué controla el segundo parámetro de `FileLogger`?  
**A:** Define el tamaño máximo del archivo de registro en megabytes, permitiéndote **set max log size**.

**Q:** ¿Puedo combinar registradores de archivo y consola?  
**A:** Sí, creando un registrador personalizado que reenvíe los mensajes a ambas destinaciones.

**Q:** ¿Cómo añado documentos al índice después de la creación inicial?  
**A:** Llama a `index.add(pathToNewDocs)` en cualquier momento; el registrador registrará la operación.

**Q:** ¿Es `ConsoleLogger` thread‑safe?  
**A:** Escribe directamente a `System.out`, que está sincronizado por la JVM, por lo que es seguro para la mayoría de los casos.

**Q:** ¿Limitar el tamaño del archivo de registro afecta la cantidad de información almacenada?  
**A:** Cuando se alcanza el límite, las nuevas entradas pueden descartarse o el archivo puede **roll over log file**, según la implementación del registrador.

## Recursos
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Última actualización:** 2026-02-24  
**Probado con:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs  

---