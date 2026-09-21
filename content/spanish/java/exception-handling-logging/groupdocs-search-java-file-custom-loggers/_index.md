---
date: '2026-09-21'
description: Aprenda cómo crear logger, establecer el tamaño máximo del log y usar
  console logger en GroupDocs.Search para Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Aprenda cómo crear logger, establecer el tamaño máximo del log y usar
  console logger en GroupDocs.Search para Java. Siga instrucciones paso a paso y consejos
  de buenas prácticas.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Cómo crear logger y limitar el tamaño del log en GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Cómo crear logger y limitar el tamaño del log en GroupDocs.Search para Java
type: docs
url: /es/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Cómo crear un logger y limitar el tamaño del archivo de registro en GroupDocs.Search para Java

En este tutorial aprenderás **cómo crear logger** implementaciones para GroupDocs.Search, configurar un tamaño máximo para el archivo de registro y alternar entre el registro basado en archivo y el registro en consola. Una gestión adecuada de los registros evita que los discos se llenen durante trabajos de indexación grandes, mejora la resolución de problemas y te brinda retroalimentación instantánea al desarrollar. Comenzaremos con la configuración de Maven, revisaremos la configuración del logger y terminaremos con una consulta de búsqueda simple que demuestra el logger en acción.

## Respuestas rápidas
- **¿Qué significa “limitar el tamaño del archivo de registro”?** Limita el tamaño máximo de un archivo de registro, evitando un crecimiento descontrolado en el disco.  
- **¿Qué logger permite limitar el tamaño del archivo de registro?** El `FileLogger` incorporado acepta un parámetro de tamaño máximo.  
- **¿Cómo utilizo console logger java?** Instancia `ConsoleLogger` y establécelo en `IndexSettings`.  
- **¿Necesito una licencia para GroupDocs.Search?** Una versión de prueba funciona para evaluación; se requiere una licencia comercial para producción.  
- **¿Cuál es el primer paso?** Añade la dependencia de GroupDocs.Search a tu proyecto Maven.  

## ¿Qué es limitar el tamaño del archivo de registro?
La configuración **limit log file size** indica al logger que deje de escribir nuevas entradas una vez que el archivo alcance un umbral definido (por ejemplo, 4 MB). Cuando se alcanza el límite, el logger descarta los mensajes posteriores o crea un nuevo archivo, manteniendo predecible el uso del disco.

## ¿Por qué usar loggers de archivo y personalizados con GroupDocs.Search?
Los loggers de archivo y personalizados te brindan auditoría, información de depuración y flexibilidad. En entornos de producción, los registros en archivo proporcionan un registro permanente de cada operación de indexación y búsqueda, mientras que los registros en consola ofrecen retroalimentación instantánea durante el desarrollo. Estos registros ayudan a los equipos a monitorear el rendimiento, rastrear errores y cumplir con los requisitos de cumplimiento al preservar una pista de actividad detallada.

## Requisitos previos
- GroupDocs.Search para Java ≥ 25.4.  
- JDK 8 o superior, con un IDE como IntelliJ IDEA o Eclipse.  
- Familiaridad básica con Maven y programación Java.  

## Configuración de GroupDocs.Search para Java

Añade la biblioteca a tu proyecto usando uno de los métodos a continuación.

**Configuración Maven:**  

```text
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
```

**Descarga directa:**  
Descarga el último JAR del sitio oficial: [lanzamientos de GroupDocs.Search para Java](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
Obtén una versión de prueba o compra una licencia a través de la [página de licencias](https://purchase.groupdocs.com/temporary-license/).

## Cómo crear un logger personalizado para GroupDocs.Search
Crear un logger personalizado es sencillo porque GroupDocs.Search se basa en la interfaz `ILogger`. Al implementar esta interfaz —o al extender los `FileLogger` o `ConsoleLogger` proporcionados— puedes inyectar comportamientos adicionales como reenvío remoto o rotación de registros. También puedes agregar lógica de inicialización, como abrir conexiones de red, y asegurar que los recursos se cierren en el método de apagado del logger. Este enfoque te permite integrarte con plataformas de monitoreo como ELK o Splunk.

### Definición
`ILogger` es el contrato central de registro en GroupDocs.Search; cualquier clase que implemente su método `log(Level, String)` puede convertirse en un logger.

### Enfoque de ejemplo (sin bloque de código)
1. Crea una clase que implemente `ILogger`.  
2. Sobrescribe el método `log` para escribir mensajes en el destino que elijas (archivo, base de datos, endpoint HTTP).  
3. En la configuración del índice, llama a `settings.setLogger(new YourCustomLogger())`.  

## Cómo limitar el tamaño del archivo de registro con File Logger
La clase `FileLogger` escribe entradas de registro en un archivo en disco y acepta un argumento de tamaño máximo. Al especificar el límite de tamaño, el logger deja automáticamente de agregar nuevas entradas o crea un nuevo archivo cuando se alcanza el umbral, evitando un crecimiento descontrolado del disco. Este comportamiento garantiza que el registro no interfiera con el rendimiento de la indexación mientras mantiene un registro conciso de los eventos.

### Definición
`FileLogger` es un logger incorporado que persiste los mensajes en un archivo de texto y soporta un tamaño máximo de archivo configurable.

### Guía paso a paso
1️⃣ **Importar paquetes necesarios**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Configurar index settings con File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Crear o cargar el índice**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Agregar documentos al índice**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Ejecutar una consulta de búsqueda**  
```text
```java
SearchResult result = index.search(query);
```
```

**Punto clave:** El segundo argumento del constructor de `FileLogger` (`4.0`) define el **tamaño máximo del registro** en megabytes, abordando directamente el requisito de **limitar el tamaño del archivo de registro**.

## Cómo usar console logger java
Cuando necesitas visibilidad instantánea de los eventos de registro, el `ConsoleLogger` escribe cada mensaje en `System.out`. Este logger es ligero y seguro para hilos, lo que lo hace adecuado para sesiones de desarrollo y depuración. Proporciona retroalimentación inmediata sobre el progreso de la indexación, consultas de búsqueda y condiciones de error sin requerir I/O de archivo, lo que puede acelerar las pruebas iterativas.

### Definición
`ConsoleLogger` es un logger ligero que envía las entradas de registro al flujo de consola estándar, lo que lo hace ideal para sesiones de depuración.

### Pasos de configuración
1️⃣ **Importar el console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Configurar index settings con Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Crear o cargar el índice**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Agregar documentos y ejecutar una búsqueda**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Consejo:** El console logger es ideal durante el desarrollo porque imprime cada entrada de registro instantáneamente, ayudándote a verificar que la indexación y la búsqueda se comporten como se espera.

## Aplicaciones prácticas
1. **Sistemas de gestión documental:** Mantener rastros de auditoría de cada documento indexado, cumpliendo con los requisitos de cumplimiento.  
2. **Motores de búsqueda empresarial:** Monitorear el rendimiento de consultas y tasas de error en tiempo real, permitiendo verificaciones rápidas de cumplimiento de SLA.  
3. **Software legal y de cumplimiento:** Registrar términos de búsqueda y marcas de tiempo para informes regulatorios, con registros conservados durante el período de retención mandatorio.

## Consideraciones de rendimiento
- **Tamaño del registro:** Al **establecer el tamaño máximo del registro**, evitas un uso excesivo de disco que de otro modo podría ralentizar el recolector de basura de la JVM.  
- **Registro asíncrono:** Para escenarios de alto rendimiento, envuelve tu logger en una cola asíncrona para desacoplar I/O del hilo de indexación (implementación fuera del alcance de esta guía).  
- **Gestión de memoria:** Libera objetos `Index` grandes con `index.close()` cuando ya no se necesiten para mantener bajo el consumo de memoria de la JVM.

## Problemas comunes y soluciones
- **Ruta de registro no accesible:** Verifica que el directorio exista y que la aplicación tenga permisos de escritura para la cuenta de usuario que ejecuta la JVM.  
- **Logger no se dispara:** Asegúrate de llamar a `settings.setLogger(...)` *antes* de crear el objeto `Index`; de lo contrario se usará el logger predeterminado.  
- **Salida de consola ausente:** Confirma que estás ejecutando la aplicación en una terminal que muestra `System.out`, y que ningún framework de registro (p. ej., SLF4J) esté interceptando la salida.

## Preguntas frecuentes

**P: ¿Qué controla el segundo parámetro de `FileLogger`?**  
A: Establece el tamaño máximo del archivo de registro en megabytes, permitiéndote **establecer el tamaño máximo del registro** y evitar un crecimiento descontrolado.

**P: ¿Puedo combinar loggers de archivo y consola?**  
A: Sí. Crea un logger personalizado que reenvíe cada llamada `log` tanto a un `FileLogger` como a un `ConsoleLogger`, y registra ese logger compuesto con `IndexSettings`.

**P: ¿Cómo agrego documentos al índice después de la creación inicial?**  
A: Llama a `index.add(pathToNewDocs)` en cualquier momento; el logger configurado registrará automáticamente la adición.

**P: ¿Es `ConsoleLogger` seguro para hilos?**  
A: Escribe directamente a `System.out`, que la JVM sincroniza internamente, lo que lo hace seguro para casos de uso multihilo típicos.

**P: ¿Limitar el tamaño del archivo de registro afectará la cantidad de información almacenada?**  
A: Una vez que se alcanza el límite de tamaño, las nuevas entradas se descartan o el logger crea un nuevo archivo, según la implementación que elijas.

## Recursos
- [Documentación](https://docs.groupdocs.com/search/java/)
- [Referencia API](https://reference.groupdocs.com/search/java/)

---

**Última actualización:** 2026-09-21  
**Probado con:** GroupDocs.Search para Java 25.4  
**Autor:** GroupDocs  

---

## Tutoriales relacionados

- [Cómo implementar registro - Tutoriales de manejo de excepciones y registro para GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implementar registro asíncrono en Java con GroupDocs.Search – Guía de logger personalizado](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Crear índice de búsqueda Java – Tutoriales de GroupDocs.Search](/search/java/indexing/)