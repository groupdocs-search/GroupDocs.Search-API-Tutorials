---
date: '2026-03-17'
description: Aprende cómo crear un índice con GroupDocs.Search para Java, configurar
  caracteres regulares y combinados, y optimizar la búsqueda de números de casos legales
  e imágenes OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Cómo crear un índice con reconocimiento de caracteres en Java
type: docs
url: /es/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

 formatting, code block placeholders unchanged.

Also note the note "For Spanish, ensure proper RTL formatting if needed" - not needed.

Now produce final content.# Cómo crear un índice con reconocimiento de caracteres usando GroupDocs.Search para Java

En aplicaciones modernas con gran cantidad de documentos, **cómo crear un índice** que respete los matices de su texto—como guiones, guiones bajos o símbolos específicos de cada idioma—es esencial para una recuperación rápida y precisa. En este tutorial recorreremos la configuración del reconocimiento de caracteres en **GroupDocs.Search para Java**, cubriendo tanto caracteres regulares (letras, dígitos, guiones bajos) como caracteres combinados (p. ej., guiones). Al final, podrá adaptar un índice que se ajuste a las necesidades exactas de su escenario de OCR o búsqueda de imágenes, ya sea que esté indexando números de casos legales, repositorios de código fuente o PDFs multilingües.

## Respuestas rápidas
- **¿Qué significa “crear índice de búsqueda personalizado”?** Significa configurar un índice para tratar símbolos específicos como letras o caracteres combinados, en lugar de ignorarlos.  
- **¿Qué biblioteca se utiliza?** GroupDocs.Search para Java (v25.4 al momento de escribir).  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia de pago para producción.  
- **¿Puedo indexar tanto PDFs como imágenes?** Sí—GroupDocs.Search admite OCR en imágenes y PDFs cuando está configurado correctamente.  
- **¿Se requiere Maven?** Maven es la forma recomendada para gestionar dependencias, pero también puede usar Gradle o JARs manuales.

## ¿Qué es un índice de búsqueda personalizado?
Un índice de búsqueda personalizado le permite definir cómo el motor de búsqueda interpreta los caracteres. Por defecto, muchos símbolos se ignoran, lo que puede provocar coincidencias perdidas para cosas como números de caso (`2023-AB-456`) o fragmentos de código (`my_variable`). Ajustar el diccionario del alfabeto le brinda control total sobre lo que el motor trata como texto buscable.

## ¿Por qué configurar caracteres regulares y combinados para números de casos legales?
- **Caracteres regulares** (letras, dígitos, guiones bajos) se tokenizan por separado, lo que permite búsquedas de coincidencia exacta para identificadores.  
- **Caracteres combinados** (guiones, barras) mantienen los tokens relacionados juntos, evitando la división no deseada de números de caso, códigos de producto o rutas de archivo.  
- Esta configuración **optimiza el rendimiento del índice de búsqueda** al reducir la fragmentación de tokens y mejorar la relevancia para contenido generado por OCR.

## Requisitos previos
- **JDK 8** o posterior instalado.  
- **Maven** para la gestión de dependencias.  
- Acceso a la biblioteca **GroupDocs.Search para Java** (descargada vía Maven o el sitio oficial).  

### Bibliotecas y dependencias requeridas
Agregue las entradas del repositorio y la dependencia a su `pom.xml` (como se muestra a continuación). El bloque XML debe permanecer sin cambios.

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

También puede descargar los JAR más recientes desde [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Obtención de licencia
- **Prueba gratuita** – perfecta para la experimentación inicial.  
- **Licencia temporal** – útil para ciclos de desarrollo más largos.  
- **Licencia de producción** – requerida para despliegue comercial.  

Obtenga una licencia en el portal oficial: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inicialización básica
El fragmento a continuación muestra el código mínimo necesario para crear un índice vacío. Manténgalo tal cual; lo ampliaremos más adelante.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Configuración de GroupDocs.Search para Java

### Instalación vía Maven
La configuración de Maven de la sección *Requisitos previos* es todo lo que necesita. Después de agregarla, ejecute `mvn clean install` para obtener los binarios.

### Requisitos de configuración del entorno
- Asegúrese de que la **carpeta de índice** y la **carpeta de documentos** existan en el disco.  
- Use rutas absolutas o configure su IDE para resolver rutas relativas correctamente.  

## Guía de implementación

A continuación recorremos dos características distintas: **caracteres regulares** y **caracteres combinados**. Cada característica sigue el mismo patrón: definir rutas, crear el índice, establecer el diccionario de caracteres y, finalmente, indexar sus documentos.

### Característica 1 – Caracteres regulares

#### Visión general
Los caracteres regulares se tratan como tokens independientes. Esto es ideal cuando desea que los dígitos, letras y guiones bajos sean buscables exactamente como aparecen.

#### Implementación paso a paso

**1️⃣ Configurar rutas**  
Defina dónde se almacenará el índice y dónde se encuentran sus documentos fuente.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Crear y configurar el índice**  
Instancie el índice y borre cualquier configuración de alfabeto preexistente.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definir caracteres regulares**  
Construya una matriz de caracteres que incluya dígitos, letras latinas y el guión bajo.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Indexar documentos**  
Agregue todos los archivos de la carpeta fuente al índice recién configurado.

```java
index.add(documentFolder);
```

### Característica 2 – Caracteres combinados

#### Visión general
Los caracteres combinados (como los guiones) a menudo conectan dos palabras. Marcarlos como *combinados* indica al motor que mantenga los tokens circundantes juntos durante la indexación.

#### Implementación paso a paso

**1️⃣ Configurar rutas**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Crear y configurar el índice**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definir caracteres combinados**  
Aquí indicamos al diccionario que el guión debe tratarse como un carácter combinado.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexar documentos**  

```java
index.add(documentFolder);
```

## Aplicaciones prácticas

### Caso de uso 1 – Gestión de documentos legales
Los archivos legales a menudo contienen números de caso como `2023-AB-456`. Al configurar guiones bajos y guiones, las búsquedas devuelven coincidencias exactas sin dividir el identificador, ayudándole a **buscar números de casos legales** de manera eficiente.

### Caso de uso 2 – Repositorios de código fuente
Los desarrolladores necesitan buscar fragmentos de código donde los guiones bajos (`my_variable`) y los guiones (`my-function`) son significativos. El reconocimiento de caracteres personalizado garantiza que el motor de búsqueda respete estos símbolos.

### Caso de uso 3 – Conjuntos de datos multilingües
Al trabajar con idiomas que utilizan alfabetos adicionales, puede **extender el conjunto de caracteres Unicode** para incluir esos rangos, garantizando resultados de búsqueda precisos entre idiomas.

### Caso de uso 4 – Indexar imágenes PDF
Si está indexando PDFs escaneados o archivos de imagen, la salida de OCR a menudo contiene caracteres mixtos. Configurar correctamente los caracteres regulares y combinados **optimiza el rendimiento del índice de búsqueda** para contenido basado en imágenes.

## Consideraciones de rendimiento

- **Gestión de recursos** – Vigile el uso del heap; los índices grandes se benefician de confirmaciones incrementales.  
- **Recolección de basura** – Libere los objetos `Index` cuando haya terminado para que la JVM recupere la memoria.  
- **Optimización del índice** – Llame periódicamente a `index.optimize()` (si está disponible) para compactar el índice y mejorar la velocidad de consulta.  

## Conclusión

Ahora sabe **cómo crear un índice** que distingue entre caracteres regulares y combinados usando GroupDocs.Search para Java. Este control granular le permite crear soluciones de búsqueda de alto rendimiento y conscientes de OCR, adaptadas a entornos legales, de desarrollo o multilingües.

### Próximos pasos
- Experimente con rangos Unicode adicionales para alfabetos no latinos.  
- Combine la configuración de caracteres con otras funciones de GroupDocs.Search como stemming o sinónimos.  
- Integre el índice en una API REST para exponer capacidades de búsqueda a aplicaciones front‑end.  

## Preguntas frecuentes

**Q:** *¿Cuál es el propósito de `CharacterType.Letter`?*  
**A:** Indica al índice que trate los caracteres suministrados como letras regulares, de modo que se tokenicen por separado durante la indexación.

**Q:** *¿Puedo mezclar caracteres regulares y combinados en el mismo índice?*  
**A:** Sí—simplemente llame a `setRange` para cada tipo; el diccionario manejará ambas configuraciones simultáneamente.

**Q:** *¿Necesito reconstruir el índice después de cambiar el alfabeto?*  
**A:** Absolutamente. Los cambios en el diccionario de caracteres afectan la tokenización, por lo que debe volver a indexar los documentos para aplicar las nuevas reglas.

**Q:** *¿Existe un límite al número de caracteres personalizados que puedo definir?*  
**A:** La biblioteca admite todo el rango Unicode; el rendimiento puede degradarse si agrega un conjunto extremadamente grande, así que limítelo a los caracteres que realmente necesita.

**Q:** *¿Cómo afecta esto a la precisión del OCR?*  
**A:** Al alinear el conjunto de caracteres del índice con la salida del motor OCR, reduce los falsos negativos y mejora la relevancia general de la búsqueda.

---

**Última actualización:** 2026-03-17  
**Probado con:** GroupDocs.Search 25.4 para Java  
**Autor:** GroupDocs