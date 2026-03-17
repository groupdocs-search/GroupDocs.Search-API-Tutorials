---
date: '2026-03-17'
description: Aprenda a criar um índice com o GroupDocs.Search para Java, configurar
  caracteres regulares e combinados e otimizar a pesquisa para números de processos
  judiciais e imagens OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Como criar índice com reconhecimento de caracteres em Java
type: docs
url: /pt/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

 URLs.

Now produce final markdown content.# Como Criar Índice com Reconhecimento de Caracteres usando GroupDocs.Search para Java

Em aplicações modernas que lidam com muitos documentos, **how to create index** que respeita as nuances do seu texto—como hífens, sublinhados ou símbolos específicos de idioma—é essencial para uma recuperação rápida e precisa. Neste tutorial, vamos percorrer a configuração de reconhecimento de caracteres no **GroupDocs.Search for Java**, abordando tanto caracteres regulares (letras, dígitos, sublinhados) quanto caracteres combinados (por exemplo, hífens). Ao final, você será capaz de personalizar um índice que atenda às necessidades exatas do seu cenário de OCR ou busca de imagens, seja indexando números de processos judiciais, repositórios de código‑fonte ou PDFs multilíngues.

## Respostas Rápidas
- **What does “create custom search index” mean?** Significa configurar um índice para tratar símbolos específicos como letras ou caracteres combinados, em vez de ignorá‑los.  
- **Which library is used?** GroupDocs.Search for Java (v25.4 at the time of writing).  
- **Do I need a license?** Um teste gratuito funciona para desenvolvimento; uma licença paga é necessária para produção.  
- **Can I index both PDFs and images?** Sim—GroupDocs.Search suporta OCR em imagens e PDFs quando configurado corretamente.  
- **Is Maven required?** Maven é a forma recomendada de gerenciar dependências, mas você também pode usar Gradle ou JARs manuais.

## O que é um Índice de Busca Personalizado?
Um índice de busca personalizado permite definir como o motor de busca interpreta os caracteres. Por padrão, muitos símbolos são ignorados, o que pode levar a correspondências perdidas para coisas como números de processos (`2023-AB-456`) ou trechos de código (`my_variable`). Ajustar o dicionário de alfabeto lhe dá controle total sobre o que o motor trata como texto pesquisável.

## Por que Configurar Caracteres Regulares e Combinados para Números de Processos Legais?
- **Regular characters** (letters, digits, underscores) são tokenizados separadamente, permitindo buscas de correspondência exata para identificadores.  
- **Blended characters** (hyphens, slashes) mantêm tokens relacionados juntos, evitando a divisão indesejada de números de processos, códigos de produto ou caminhos de arquivos.  
- Esta configuração **optimizes search index** o desempenho ao reduzir a fragmentação de tokens e melhorar a relevância para conteúdo gerado por OCR.

## Pré-requisitos
- **JDK 8** ou posterior instalado.  
- **Maven** para gerenciamento de dependências.  
- Acesso à biblioteca **GroupDocs.Search for Java** (baixada via Maven ou site oficial).  

### Bibliotecas e Dependências Necessárias
Adicione as entradas de repositório e dependência ao seu `pom.xml` (conforme mostrado abaixo). O bloco XML deve permanecer inalterado.

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

Você também pode baixar os JARs mais recentes em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de Licença
- **Free Trial** – perfeito para experimentação inicial.  
- **Temporary License** – útil para ciclos de desenvolvimento mais longos.  
- **Production License** – necessária para implantação comercial.  

Obtenha uma licença no portal oficial: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inicialização Básica
O trecho abaixo mostra o código mínimo necessário para iniciar um índice vazio. Mantenha‑o como está; construiremos sobre ele mais tarde.

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

## Configurando GroupDocs.Search para Java

### Instalação via Maven
A configuração Maven da seção *Pré-requisitos* é tudo o que você precisa. Após adicioná‑la, execute `mvn clean install` para obter os binários.

### Requisitos de Configuração do Ambiente
- Garanta que a **index folder** e a **document folder** existam no disco.  
- Use caminhos absolutos ou configure sua IDE para resolver caminhos relativos corretamente.  

## Guia de Implementação

A seguir, percorremos duas funcionalidades distintas: **regular characters** e **blended characters**. Cada funcionalidade segue o mesmo padrão—definir caminhos, criar o índice, definir o dicionário de caracteres e, finalmente, indexar seus documentos.

### Recurso 1 – Caracteres Regulares

#### Visão Geral
Caracteres regulares são tratados como tokens independentes. Isso é ideal quando você deseja que dígitos, letras e sublinhados sejam pesquisáveis exatamente como aparecem.

#### Implementação Passo a Passo

**1️⃣ Set Up Paths**  
Defina onde o índice será armazenado e onde seus documentos de origem estão.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
Instancie o índice e limpe qualquer configuração de alfabeto pré‑existente.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
Construa um array de caracteres que inclua dígitos, letras latinas e o sublinhado.

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

**4️⃣ Index Documents**  
Adicione todos os arquivos da pasta de origem ao índice recém‑configurado.

```java
index.add(documentFolder);
```

### Recurso 2 – Caracteres Combinados

#### Visão Geral
Caracteres combinados (como hífens) frequentemente conectam duas palavras. Marcá‑los como *blended* indica ao motor para manter os tokens circundantes juntos durante a indexação.

#### Implementação Passo a Passo

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
Aqui informamos ao dicionário que o hífen deve ser tratado como um caractere blended.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## Aplicações Práticas

### Caso de Uso 1 – Gerenciamento de Documentos Legais
Arquivos legais frequentemente contêm números de processos como `2023-AB-456`. Ao configurar sublinhados e hífens, as buscas retornam correspondências exatas sem dividir o identificador, ajudando você a **search legal case numbers** de forma eficiente.

### Caso de Uso 2 – Repositórios de Código‑Fonte
Desenvolvedores precisam buscar trechos de código onde sublinhados (`my_variable`) e hífens (`my-function`) são significativos. O reconhecimento de caracteres personalizado garante que o motor de busca respeite esses símbolos.

### Caso de Uso 3 – Conjuntos de Dados Multilíngues
Ao trabalhar com idiomas que utilizam alfabetos adicionais, você pode **extend Unicode character set** para incluir esses intervalos, garantindo resultados de busca precisos entre idiomas.

### Caso de Uso 4 – Indexar Imagens PDF
Se você está indexando PDFs escaneados ou arquivos de imagem, a saída de OCR frequentemente contém caracteres misturados. Configurar corretamente caracteres regulares e combinados **optimizes search index** o desempenho para conteúdo baseado em imagens.

## Considerações de Performance

- **Resource Management** – Monitore o uso de heap; índices grandes se beneficiam de commits incrementais.  
- **Garbage Collection** – Libere objetos `Index` quando terminar para que a JVM recupere a memória.  
- **Index Optimization** – Chame periodicamente `index.optimize()` (se disponível) para compactar o índice e melhorar a velocidade de consulta.  

## Conclusão

Agora você sabe **how to create index** que distingue entre caracteres regulares e combinados usando GroupDocs.Search para Java. Esse controle granular permite que você construa soluções de busca de alto desempenho e conscientes de OCR, adaptadas a ambientes legais, de desenvolvimento ou multilíngues.

### Próximos Passos
- Experimente intervalos Unicode adicionais para alfabetos não‑Latinos.  
- Combine a configuração de caracteres com outros recursos do GroupDocs.Search, como stemming ou sinônimos.  
- Integre o índice em uma API REST para expor capacidades de busca a aplicações front‑end.

## Perguntas Frequentes

**Q:** *What is the purpose of `CharacterType.Letter`?*  
**A:** Ele informa ao índice para tratar os caracteres fornecidos como letras regulares, de modo que sejam tokenizados separadamente durante a indexação.

**Q:** *Can I mix regular and blended characters in the same index?*  
**A:** Sim—basta chamar `setRange` para cada tipo; o dicionário lidará com ambas as configurações simultaneamente.

**Q:** *Do I need to rebuild the index after changing the alphabet?*  
**A:** Absolutamente. Alterações no dicionário de caracteres afetam a tokenização, portanto você deve re‑indexar os documentos para aplicar as novas regras.

**Q:** *Is there a limit to the number of custom characters I can define?*  
**A:** A biblioteca suporta todo o intervalo Unicode; o desempenho pode degradar se você adicionar um conjunto extremamente grande, portanto limite aos caracteres que realmente precisa.

**Q:** *How does this affect OCR accuracy?*  
**A:** Ao alinhar o conjunto de caracteres do índice com a saída do motor de OCR, você reduz falsos negativos e melhora a relevância geral da busca.

---

**Última Atualização:** 2026-03-17  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---