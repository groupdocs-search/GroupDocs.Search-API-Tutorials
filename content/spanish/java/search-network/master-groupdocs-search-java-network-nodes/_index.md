---
date: '2026-07-02'
description: Aprenda cómo obtener una licencia temporal para GroupDocs.Search, añadir
  directorios al índice y agregar atributos de documento personalizados mientras gestiona
  los nodos de red de búsqueda de Java.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Obtener licencia temporal GroupDocs – Nodos maestros de búsqueda (Java)
type: docs
url: /es/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Obtener Licencia Temporal GroupDocs – Nodos Maestros de Búsqueda (Java)

En esta guía completa **obtendrá una licencia temporal para GroupDocs.Search**, configurará una red de búsqueda multi‑nodo y aprenderá cómo **agregar directorios al índice** y **agregar atributos de documento personalizados** usando Java. Ya sea que esté construyendo un sistema de gestión documental empresarial o un catálogo de productos searchable, dominar estos pasos le permite evaluar la plataforma sin restricciones y escalar sus capacidades de búsqueda rápidamente.

## Respuestas Rápidas
- **¿Cuál es el primer paso para comenzar a usar GroupDocs.Search?** Obtenga una licencia temporal del portal de GroupDocs.  
- **¿Qué repositorio Maven aloja la biblioteca?** `https://releases.groupdocs.com/search/java/`.  
- **¿Cómo agrego directorios al índice?** Llame al asistente `addDirectoriesToIndex` en el nodo maestro.  
- **¿Puedo agregar atributos de documento personalizados?** Sí—invocar `addAttribute` con la clave del documento y el nombre del atributo.  
- **¿Cómo cerrar los nodos correctamente?** Invocar `closeNodes` para liberar recursos.

## Qué es una licencia temporal y por qué la necesito?
Una licencia temporal le permite evaluar GroupDocs.Search sin limitaciones de evaluación. Es perfecta para desarrollo, pruebas o proyectos de prueba de concepto antes de comprometerse con una compra completa. La licencia otorga acceso a todas las funciones durante un período limitado, lo que le permite medir el rendimiento, probar puntos de integración y asegurarse de que la solución cumpla con sus requisitos sin compromiso financiero.

## Requisitos Previos

Antes de comenzar, asegúrese de que tiene los siguientes requisitos preparados:

### Bibliotecas y Dependencias Requeridas
Para trabajar con GroupDocs.Search para Java, incluya las dependencias Maven necesarias:
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
También puede descargar la última versión directamente desde [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Configuración del Entorno
- Asegúrese de tener un JDK compatible instalado (Java 8 o posterior).  
- Configure su IDE para soportar proyectos Maven.

### Prerrequisitos de Conocimientos
Un entendimiento básico de la programación en Java y familiaridad con la gestión de proyectos Maven será beneficioso. Si es nuevo en estos conceptos, considere explorar recursos introductorios para comenzar.

## Cómo obtener una licencia temporal
Una licencia temporal se obtiene visitando el portal de GroupDocs, completando un breve formulario de solicitud y colocando el archivo `.lic` recibido en la carpeta `resources` de su proyecto. Luego inicialice la licencia con unas pocas líneas de código (vea el fragmento a continuación). Para el formulario de solicitud, use la página oficial: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Configuración de GroupDocs.Search para Java

### Información de Instalación
Para comenzar a usar GroupDocs.Search para Java en su proyecto, siga los pasos de Maven anteriores o descargue la última versión directamente desde la página oficial de lanzamientos.

#### Pasos para la Adquisición de Licencia
1. **Free Trial** – Explore las funciones sin ningún compromiso.  
2. **Temporary License** – Obtenga una clave a corto plazo para pruebas (vea la sección anterior).  
3. **Purchase** – Para uso en producción, compre una licencia completa desde la **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Inicialización y Configuración Básica
Inicialice su proyecto con GroupDocs.Search de la siguiente manera:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Este paso de inicialización es crucial para garantizar que todos los componentes funcionen sin problemas dentro de su red de búsqueda.

## Guía de Implementación

Ahora, desglosaremos el proceso en secciones manejables, cada una enfocada en una característica específica de la implementación y gestión de nodos de la red de búsqueda.

### Función 1: Configuración
**Visión general:** Configurar la configuración de su red de búsqueda es el primer paso para desplegar nodos. Esta configuración implica especificar rutas y puertos críticos para el despliegue de nodos.

#### Pasos de Implementación:
##### Paso 1: Definir Ruta Base y Puerto
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Paso 2: Configurar la Red de Búsqueda
La función `configureSearchNetwork` prepara el objeto de configuración necesario para desplegar nodos.  
`Configuration` es una clase que contiene todos los ajustes como la carpeta de índice, puertos de red y roles de nodo.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parameters:** La ruta base y el puerto se utilizan para localizar recursos y establecer canales de comunicación.  
- **Return Value:** Un objeto `Configuration` configurado adaptado a sus necesidades de despliegue.

### Función 2: Despliegue de la Red de Búsqueda
**Visión general:** Desplegar nodos es esencial para escalar sus capacidades de búsqueda a través de diferentes entornos o segmentos de datos.

#### Pasos de Implementación:
##### Paso 1: Desplegar Nodos
La función `deploySearchNetwork` inicializa y devuelve una matriz de nodos de la red de búsqueda.  
`SearchNetworkNodes` representa cada instancia de nodo que participa en el clúster de búsqueda distribuido.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parameters:** La ruta base, el puerto y la configuración se utilizan para determinar el entorno de despliegue.  
- **Return Value:** Una matriz que contiene `SearchNetworkNodes` inicializados.

### Función 3: Suscripción a Eventos de la Red
**Visión general:** Monitorear las actividades de su red de búsqueda es crucial para mantener un rendimiento y fiabilidad óptimos.

#### Pasos de Implementación:
##### Paso 1: Suscribirse a Eventos del Nodo Maestro
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Propósito:** Este paso asegura que sea notificado de eventos o cambios significativos dentro de su red de búsqueda.

### Función 4: Indexación de Documentos
**Visión general:** Agregar directorios que contienen documentos para ser indexados permite una recuperación de datos eficiente a través de su red.

#### Cómo agregar directorios al índice
`addDirectoriesToIndex` es un método auxiliar que registra rutas de carpetas para indexar en el nodo maestro.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Propósito:** Facilita el acceso rápido y la capacidad de búsqueda de todos los documentos dentro de los directorios especificados.

### Función 5: Agregar Atributos a Documentos
**Visión general:** Los atributos personalizados mejoran los metadatos de los documentos, haciendo que las búsquedas sean más flexibles e informativas.

#### Cómo agregar atributos de documento personalizados
`addAttribute` agrega un atributo de metadatos personalizado a un documento especificado en el índice.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parameters:** Especifique el nodo, la clave del documento y el atributo a agregar.  
- **Propósito:** Amplía la funcionalidad de búsqueda al enriquecer los documentos con metadatos adicionales.

### Función 6: Recuperar Documentos Indexados
**Visión general:** Recuperar y listar eficientemente los documentos indexados para garantizar la precisión y completitud de los datos.

#### Pasos de Implementación:
##### Paso 1: Obtener Documentos Indexados
```java
getIndexedDocuments(nodes[0]);
```  
- **Propósito:** Verifica la indexación exitosa de todos los documentos necesarios dentro de su red de búsqueda.

### Función 7: Cerrar Nodos de la Red
**Visión general:** Cerrar correctamente los nodos es crucial para la gestión de recursos y prevenir fugas de memoria.

#### Pasos de Implementación:
##### Paso 1: Cerrar Todos los Nodos
`closeNodes` cierra todos los nodos de búsqueda activos y libera los recursos asignados.  
```java
closeNodes(nodes);
```  
- **Propósito:** Libera los recursos ocupados por cada nodo, asegurando un proceso de apagado limpio.

## ¿Por qué usar una licencia temporal para GroupDocs.Search?
Una licencia temporal proporciona **acceso a todas las funciones durante 30 días** y soporta hasta **50,000 documentos indexados** sin limitaciones de rendimiento. Esto le permite medir la velocidad de indexación, la latencia de consultas y la escalabilidad con datos reales antes de comprar una licencia de producción. También elimina las marcas de agua de evaluación, brindándole una representación real de las capacidades del producto final.

## Casos de Uso Comunes
1. **Enterprise Document Management** – Indexe millones de archivos internos a través de departamentos, habilitando búsqueda de texto completo instantánea.  
2. **E‑commerce Platforms** – Construya un catálogo de productos searchable que abarque múltiples almacenes y fuentes de terceros.  
3. **Legal Firms** – Organice archivos de casos, contratos y evidencias con metadatos personalizados para una recuperación rápida.

Las posibilidades de integración con otros sistemas incluyen plataformas CRM, sistemas de gestión de contenido (CMS) y herramientas de análisis de datos, aprovechando las robustas funciones de indexación y búsqueda proporcionadas por GroupDocs.Search para Java.

## Consideraciones de Rendimiento
Para optimizar el rendimiento al usar GroupDocs.Search para Java:
- **Optimizar Configuración** – Adapte su configuración a su entorno de despliegue específico.  
- **Monitorear Uso de Recursos** – Verifique regularmente CPU, memoria y E/S para prevenir cuellos de botella o fugas de memoria.  
- **Seguir Mejores Prácticas** – Siga las directrices de gestión de memoria de Java, asegurando una utilización eficiente de los recursos del sistema.

## Preguntas Frecuentes

**Q: ¿Cuánto tiempo permanece válida una licencia temporal?**  
A: Las licencias temporales suelen ser válidas durante 30 días, dándole tiempo suficiente para evaluar el producto.

**Q: ¿Puedo cambiar de una licencia temporal a una completa sin reinstalar?**  
A: Sí—reemplace el archivo de licencia temporal con el archivo de licencia completa y reinicie su aplicación.

**Q: ¿Necesito volver a indexar los documentos después de aplicar una nueva licencia?**  
A: No, el índice permanece intacto; la licencia solo regula los derechos de uso.

**Q: ¿Qué ocurre si olvido cerrar los nodos?**  
A: Los recursos no liberados pueden provocar fugas de memoria; siempre invoque `closeNodes` durante el apagado.

**Q: ¿Es posible agregar más de un atributo personalizado por documento?**  
A: Absolutamente—llame a `addAttribute` varias veces con diferentes nombres de atributos.

---

**Última actualización:** 2026-07-02  
**Probado con:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs

## Tutoriales Relacionados

- [Desplegar un Nodo de Red de Búsqueda en .NET usando GroupDocs para Indexación y Recuperación Eficiente de Documentos](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Cómo Implementar una Red de Búsqueda con GroupDocs.Search en .NET para Sistemas de Gestión Documental](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Configuración de Aspose.Search Network y Agregado de Atributos de Documentos con GroupDocs.Redaction para .NET: Guía Completa](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)