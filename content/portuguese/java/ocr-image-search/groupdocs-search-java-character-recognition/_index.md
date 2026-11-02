---
date: '2026-11-02'
description: Criar um índice de pesquisa personalizado em java usando o GroupDocs.Search
  para lidar com caracteres regulares e combinados, otimizar a pesquisa de imagens
  OCR e melhorar a recuperação de números de processos judiciais.
keywords:
- custom search index java
- GroupDocs.Search Java
- character recognition java
- OCR search Java
- search library Java
lastmod: '2026-11-02'
og_description: Criar um índice de pesquisa personalizado em java usando o GroupDocs.Search
  para lidar com caracteres regulares e combinados, otimizar a pesquisa de imagens
  OCR e melhorar a recuperação de números de processos judiciais.
og_image_alt: Guide showing custom search index creation in Java with GroupDocs.Search
og_title: Criar um índice de pesquisa personalizado em java com GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Create a custom search index java using GroupDocs.Search to handle
    regular and blended characters, optimize OCR image search, and improve legal case
    number retrieval.
  headline: Create a custom search index java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It means configuring an index to treat specific symbols as letters or
      blended characters, rather than ignoring them.
    question: What does “create custom search index” mean?
  - answer: GroupDocs.Search for Java (v25.4 at the time of writing).
    question: Which library is used?
  - answer: A free trial works for development; a paid license is required for production.
    question: Do I need a license?
  - answer: Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.
    question: Can I index both PDFs and images?
  - answer: Maven is the recommended way to manage dependencies, but you can also
      use Gradle or manual JARs.
    question: Is Maven required?
  type: FAQPage
tags:
- custom search index
- GroupDocs.Search
- Java OCR
- character recognition
- search library
title: Criar um índice de pesquisa personalizado em java com GroupDocs.Search
type: docs
url: /pt/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Criar um índice de pesquisa personalizado java com GroupDocs.Search

Em aplicações modernas que lidam com muitos documentos, criar um **índice de pesquisa personalizado java** que respeite as nuances do seu texto — como hífens, sublinhados ou símbolos específicos de idioma — é essencial para uma recuperação rápida e precisa. Este tutorial orienta você na configuração do reconhecimento de caracteres no **GroupDocs.Search for Java**, abrangendo tanto caracteres regulares (letras, dígitos, sublinhados) quanto caracteres combinados (por exemplo, hífens). Ao final, você será capaz de adaptar um índice que atenda exatamente às necessidades de cenários de OCR ou busca em imagens, seja indexando números de processos judiciais, repositórios de código‑fonte ou PDFs multilíngues.

## Respostas rápidas
- **O que significa “criar índice de pesquisa personalizado”?** Significa configurar um índice para tratar símbolos específicos como letras ou caracteres combinados, em vez de ignorá‑los.  
- **Qual biblioteca é usada?** GroupDocs.Search for Java (v25.4 na data de escrita).  
- **Preciso de licença?** Um teste gratuito funciona para desenvolvimento; uma licença paga é necessária para produção.  
- **Posso indexar PDFs e imagens?** Sim — o GroupDocs.Search oferece suporte a OCR em imagens e PDFs quando configurado corretamente.  
- **É necessário Maven?** Maven é a forma recomendada de gerenciar dependências, mas você também pode usar Gradle ou JARs manuais.

## O que é um índice de pesquisa personalizado java?
O **índice de pesquisa personalizado java** é uma estrutura de dados pesquisável que pode ser moldada definindo quais caracteres são tratados como letras, dígitos ou símbolos combinados. Por padrão, muitos símbolos são ignorados, o que pode causar falhas de correspondência para identificadores como números de processos (`2023-AB-456`) ou trechos de código (`my_variable`). Ajustar o dicionário alfabético oferece controle total sobre a tokenização, resultando em maior relevância e execução de consultas mais rápida.

## Por que configurar caracteres regulares e combinados para números de processos judiciais?
Tratar hífens e barras como caracteres combinados mantém os tokens relacionados juntos, evitando a divisão indesejada de identificadores como números de processos, códigos de produto ou caminhos de arquivos. Essa configuração **otimiza o desempenho do índice de pesquisa** ao reduzir a fragmentação de tokens e melhora a relevância para conteúdo gerado por OCR, especialmente ao lidar com documentos legais que dependem fortemente de identificadores estruturados.

## Pré-requisitos
- **JDK 8** ou superior instalado.  
- **Maven** para gerenciamento de dependências.  
- Acesso à biblioteca **GroupDocs.Search for Java** (baixada via Maven ou pelo site oficial).  

### Bibliotecas e dependências necessárias
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

Você também pode baixar os JARs mais recentes em [lançamentos do GroupDocs.Search para Java](https://releases.groupdocs.com/search/java/).

### Aquisição de licença
- **Teste gratuito** – ideal para experimentação inicial.  
- **Licença temporária** – útil para ciclos de desenvolvimento mais longos.  
- **Licença de produção** – necessária para implantação comercial.  

Obtenha uma licença no portal oficial: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inicialização básica
O trecho abaixo mostra o código mínimo necessário para iniciar um índice vazio. A classe `Index` é o componente central que armazena e gerencia os dados pesquisáveis. Mantenha‑o como está; construiremos sobre ele mais adiante.

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

## Configurando o GroupDocs.Search para Java

### Instalação via Maven
A configuração Maven da seção *Pré-requisitos* é tudo o que você precisa. Após adicioná‑la, execute `mvn clean install` para baixar os binários.

### Requisitos de configuração do ambiente
- Garanta que a **pasta do índice** e a **pasta de documentos** existam no disco.  
- Use caminhos absolutos ou configure sua IDE para resolver caminhos relativos corretamente.  

## Guia de implementação

A seguir, percorremos duas funcionalidades distintas: **caracteres regulares** e **caracteres combinados**. Cada funcionalidade segue o mesmo padrão — definir caminhos, criar o índice, definir o dicionário de caracteres e, finalmente, indexar seus documentos.

### Recurso 1 – caracteres regulares

#### Visão geral
Caracteres regulares são tratados como tokens independentes. Isso é ideal quando você deseja que dígitos, letras e sublinhados sejam pesquisáveis exatamente como aparecem.

#### Implementação passo a passo

**1️⃣ Definir caminhos**  
Especifique onde o índice será armazenado e onde seus documentos de origem estão localizados.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Criar e configurar o índice**  
Instancie o índice e limpe qualquer configuração de alfabeto pré‑existente.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definir caracteres regulares**  
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

**4️⃣ Indexar documentos**  
Adicione todos os arquivos da pasta de origem ao índice recém‑configurado.

```java
index.add(documentFolder);
```

### Recurso 2 – caracteres combinados

#### Visão geral
Caracteres combinados (como hífens) costumam conectar duas palavras. Marcá‑los como *combinados* indica ao mecanismo que mantenha os tokens circundantes juntos durante a indexação.

#### Implementação passo a passo

**1️⃣ Definir caminhos**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Criar e configurar o índice**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definir caracteres combinados**  
Aqui informamos ao dicionário que o hífen deve ser tratado como um caractere combinado.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indexar documentos**  

```java
index.add(documentFolder);
```

## Aplicações práticas

### Caso de uso 1 – gerenciamento de documentos legais
Arquivos jurídicos frequentemente contêm números de processos como `2023-AB-456`. Ao configurar sublinhados e hífens, as buscas retornam correspondências exatas sem dividir o identificador, ajudando você a **pesquisar números de processos legais** de forma eficiente.

### Caso de uso 2 – repositórios de código‑fonte
Desenvolvedores precisam buscar trechos de código onde sublinhados (`my_variable`) e hífens (`my-function`) são significativos. O reconhecimento de caracteres personalizado garante que o motor de busca respeite esses símbolos.

### Caso de uso 3 – conjuntos de dados multilíngues
Ao trabalhar com idiomas que utilizam alfabetos adicionais, você pode **estender o conjunto de caracteres Unicode** para incluir esses intervalos, garantindo resultados de busca precisos entre diferentes línguas.

### Caso de uso 4 – indexar imagens PDF
Se você está indexando PDFs escaneados ou arquivos de imagem, a saída do OCR costuma conter caracteres mistos. Configurar corretamente caracteres regulares e combinados **otimiza o desempenho do índice de pesquisa** para conteúdo baseado em imagens.

## Considerações de desempenho

- **Gerenciamento de recursos** – monitore o uso de heap; índices grandes se beneficiam de commits incrementais.  
- **Coleta de lixo** – libere objetos `Index` ao terminar para que a JVM recupere a memória.  
- **Otimização do índice** – chame periodicamente `index.optimize()` (se disponível) para compactar o índice e melhorar a velocidade das consultas.  

## Conclusão

Agora você sabe **como criar um índice de pesquisa personalizado java** que distingue entre caracteres regulares e combinados usando o GroupDocs.Search for Java. Esse controle granular permite construir soluções de busca conscientes de OCR, de alto desempenho e adaptadas a ambientes legais, de desenvolvimento ou multilíngues.

### Próximos passos
- Experimente intervalos Unicode adicionais para alfabetos não latinos.  
- Combine a configuração de caracteres com outros recursos do GroupDocs.Search, como stemming ou sinônimos.  
- Exponha o índice por meio de uma API REST para que aplicações front‑end realizem buscas via HTTP.  

## Perguntas frequentes

**Q:** *Qual é a finalidade de `CharacterType.Letter`?*  
**A:** Ele indica ao índice que os caracteres fornecidos devem ser tratados como letras regulares, de modo que sejam tokenizados separadamente durante a indexação.

**Q:** *Posso misturar caracteres regulares e combinados no mesmo índice?*  
**A:** Sim — basta chamar `setRange` para cada tipo; o dicionário lidará com ambas as configurações simultaneamente.

**Q:** *Preciso reconstruir o índice após alterar o alfabeto?*  
**A:** Absolutamente. Alterações no dicionário de caracteres afetam a tokenização, portanto é necessário reindexar os documentos para aplicar as novas regras.

**Q:** *Existe um limite para a quantidade de caracteres personalizados que posso definir?*  
**A:** A biblioteca suporta todo o intervalo Unicode; o desempenho pode degradar se você adicionar um conjunto extremamente grande, portanto limite‑se aos caracteres realmente necessários.

**Q:** *Como isso afeta a precisão do OCR?*  
**A:** Ao alinhar o conjunto de caracteres do índice com a saída do motor OCR, você reduz falsos negativos e melhora a relevância geral da busca.

---

**Última atualização:** 2026-11-02  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Criar e Gerenciar Índice de Pesquisa GroupDocs Java](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Criar Diretório de Índice de Busca & Definir Licença – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Biblioteca Java de Busca de Texto Completo – Otimizar Índice com GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)