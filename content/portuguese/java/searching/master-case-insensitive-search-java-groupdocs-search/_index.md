---
date: '2026-07-31'
description: Aprenda como implementar pesquisa sem distinção de maiúsculas e minúsculas
  em Java adicionando documentos a um índice com o GroupDocs.Search, usando substituição
  de caracteres para normalizar o texto durante a indexação.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: A pesquisa sem distinção de maiúsculas e minúsculas em Java permite
  adicionar documentos a um índice e consultá‑los sem se preocupar com a caixa das
  letras. Este guia mostra como o GroupDocs.Search normaliza o texto durante a indexação
  para resultados rápidos e confiáveis.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Pesquisa sem distinção de maiúsculas e minúsculas em Java – Indexar documentos
  com o GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Adicionar documentos ao índice para pesquisa sem distinção de maiúsculas e
  minúsculas em Java
type: docs
url: /pt/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Adicionar documentos ao índice para pesquisa sem distinção entre maiúsculas e minúsculas em Java

Quando você precisa de **case insensitive search java** que encontre informações de forma confiável independentemente de como os usuários as digitam, a chave é adicionar documentos a um índice enquanto normaliza o texto. Neste tutorial, percorremos a configuração do GroupDocs.Search para Java para que cada documento indexado seja automaticamente convertido para minúsculas (ou transformado de outra forma) durante a indexação, garantindo resultados sem distinção entre maiúsculas e minúsculas sem lógica adicional no momento da consulta.

## Respostas rápidas
- **O que significa “add documents to index”?** Significa carregar arquivos de origem em uma estrutura de dados pesquisável para que possam ser consultados posteriormente.  
- **Por que usar substituição de caracteres?** Ela normaliza cada caractere — tipicamente para minúsculas — para que as pesquisas ignorem diferenças de maiúsculas/minúsculas automaticamente.  
- **Preciso de uma licença?** Um teste gratuito funciona para desenvolvimento; uma licença completa é necessária para implantações em produção.  
- **Qual versão do Java é necessária?** Java 8 ou mais recente; a biblioteca tem como alvo Java 11+ para desempenho ideal.  
- **Posso mudar para pesquisa sensível a maiúsculas/minúsculas quando necessário?** Sim — as opções de pesquisa permitem alternar a sensibilidade a maiúsculas/minúsculas por consulta.

## O que é “add documents to index” no GroupDocs.Search?
Carregue seus arquivos de origem (PDF, DOCX, TXT, etc.) em um índice pesquisável para que o mecanismo possa recuperá‑los rapidamente. Adicionar documentos a um índice analisa cada arquivo, extrai o texto puro e o armazena em uma estrutura de dados otimizada que permite buscas rápidas.

## Por que habilitar a substituição de caracteres durante a indexação?
A substituição de caracteres converte cada caractere para um equivalente predefinido — mais comumente para minúsculas — enquanto o índice é construído. Isso garante que variações de capitalização, diacríticos ou símbolos específicos de localidade não afetem os resultados da pesquisa. Ao normalizar o texto no momento da indexação, o mecanismo pode comparar consultas com um conjunto consistente de tokens, proporcionando comportamento rápido e confiável sem distinção entre maiúsculas e minúsculas sem processamento adicional em cada pesquisa.

## Pré‑requisitos
- **GroupDocs.Search for Java** versão 25.4 ou mais recente (a biblioteca suporta mais de 30 formatos de arquivo e pode indexar documentos com centenas de páginas sem carregar o arquivo inteiro na memória).  
- **Java Development Kit (JDK)** 8 ou posterior instalado.  
- Familiaridade básica com **Maven** (ou capacidade de adicionar JARs manualmente).  

## Configurando o GroupDocs.Search para Java

### Configuração Maven
Adicione o repositório GroupDocs e a dependência ao seu `pom.xml`:

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

### Download direto
Se preferir não usar Maven, obtenha o JAR mais recente no site oficial: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de licença
- **Free Trial** – baixe uma licença de teste para começar a experimentar.  
- **Temporary License** – solicite uma licença de teste estendida no portal GroupDocs.  
- **Full License** – adquira uma licença de produção quando estiver pronto para entrar em operação.

### Inicialização básica (Criar o índice)
O trecho a seguir cria uma pasta de índice e habilita substituições de caracteres:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Guia de implementação

### Habilitar substituição de caracteres nas configurações do índice
Ativar este recurso indica ao mecanismo que ele deve substituir caracteres durante a indexação, que é a etapa central para o comportamento sem distinção entre maiúsculas e minúsculas.

#### Etapa 1: Configurar `IndexSettings`
`IndexSettings` é o objeto de configuração que controla como o índice armazena e processa texto. Definindo `useCharacterReplacements` como **true**, você ativa a conversão automática para minúsculas (ou qualquer mapeamento personalizado que fornecer).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Configurar substituições de caracteres
Mapeie cada caractere para sua contraparte em minúsculas (ou qualquer mapeamento personalizado que precisar).

#### Etapa 2: Definir e adicionar pares de substituição
O dicionário de substituição contém pares como `'A' → 'a'`, `'É' → 'e'`, etc. Adicionar esses pares antes da indexação garante que cada token seja normalizado.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Indexando documentos
Agora que o índice está pronto, você pode **add documents to index** a partir de qualquer pasta.

#### Etapa 3: Adicionar documentos para indexação
O GroupDocs.Search varre o diretório de destino, extrai texto de cada tipo de arquivo suportado, aplica o mapa de substituição e grava os tokens no armazenamento do índice.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Executar pesquisa sensível a maiúsculas/minúsculas (Opcional)

#### Etapa 4: Executar pesquisas sensíveis a maiúsculas/minúsculas
`SearchOptions` configura o comportamento da consulta, como alternar a sensibilidade a maiúsculas/minúsculas, permitindo controle detalhado sobre como as pesquisas são realizadas.  
`SearchOptions.setUseCaseSensitiveSearch(true)` força o mecanismo a tratar caracteres maiúsculos e minúsculos como distintos durante uma consulta específica, sobrescrevendo o comportamento padrão sem distinção entre maiúsculas e minúsculas.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Aplicações práticas
1. **Campanhas de marketing** – Normalizar nomes de produtos para que as equipes de vendas possam localizar ativos sem se preocupar com maiúsculas/minúsculas.  
2. **Suporte ao cliente** – Alimentar caixas de pesquisa de help‑desk que retornam o artigo correto, independentemente de o usuário digitar “login” ou “Login”.  
3. **Catálogos de e‑commerce** – Garantir que os compradores encontrem itens independentemente de como digitam os títulos dos produtos, melhorando as taxas de conversão.

## Considerações de desempenho
- **Organizar arquivos de origem** – Uma hierarquia de pastas bem organizada reduz o tempo gasto na varredura durante a etapa **add documents to index**.  
- **Monitorar memória** – Indexar grandes corpora pode consumir RAM significativa; processar arquivos em lotes de 500 – 1 000 itens mantém o uso do heap sob controle.  
- **Indexação assíncrona** – Quando suportada, execute a indexação em uma thread em segundo plano para manter a UI responsiva e evitar bloquear operações do usuário.

## Problemas comuns e solução de problemas
| Sintoma | Causa provável | Correção |
|---------|----------------|----------|
| Nenhum resultado retornado para um termo conhecido | Substituições de caracteres não habilitadas | Verifique `settings.setUseCharacterReplacements(true)` e que o mapa de substituição contém os caracteres necessários. |
| Erro de falta de memória durante a indexação | Indexação de muitos arquivos grandes de uma vez | Indexe em lotes menores ou aumente o heap da JVM (`-Xmx4g`). |
| A pesquisa retorna resultados sensíveis a maiúsculas/minúsculas inesperadamente | `SearchOptions.setUseCaseSensitiveSearch(true)` foi definido | Remova ou defina como `false` para o comportamento padrão sem distinção entre maiúsculas e minúsculas. |
| Tempo de carregamento do índice excede o esperado | Layout de pastas ineficiente ou SSD não utilizado | Reorganize arquivos, remova documentos não usados e armazene o índice em um SSD rápido. |
| Caracteres especiais são ignorados | Mapa de substituição sem entradas Unicode | Adicione mapeamentos para caracteres como “é”, “ß”, “ø” aos seus equivalentes desejados. |

## Perguntas frequentes

**Q: Como lidar com caracteres especiais (por exemplo, “é”, “ß”) durante a indexação?**  
A: Inclua esses caracteres no seu mapa de substituição, mapeando-os para seus equivalentes ASCII ou mantendo-os inalterados conforme os requisitos de pesquisa.

**Q: Posso limitar a substituição de caracteres a um idioma específico?**  
A: Sim. Crie um array de substituição personalizado que contenha apenas os caracteres do idioma alvo antes de adicioná‑lo ao dicionário.

**Q: O que fazer se o índice demorar muito para carregar?**  
A: Otimize a estrutura de pastas, remova arquivos desnecessários e armazene o índice em um SSD de alta velocidade. A indexação incremental também reduz a sobrecarga de carregamento.

**Q: É possível reverter as substituições de caracteres após a indexação?**  
A: Não. As substituições são incorporadas aos dados indexados; você deve reconstruir o índice com novas configurações para alterá‑las.

**Q: Onde posso encontrar documentação de API mais detalhada?**  
A: A documentação oficial e a referência da API fornecem detalhes completos (veja os Recursos abaixo).

## Recursos
- [Documentação](https://docs.groupdocs.com/search/java/)
- [Referência da API](https://reference.groupdocs.com/search/java)
- [Baixar GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [Repositório no GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Fórum de suporte gratuito](https://forum.groupdocs.com/c/search/10)
- [Informações sobre licença temporária](https://purchase.groupdocs.com/temporary-license/) 

---

**Última atualização:** 2026-07-31  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---

## Tutoriais relacionados

- [Substituição de caracteres no GroupDocs.Search Java: Um guia abrangente para melhorar a pesquisa de texto e indexação](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Adicionar documentos ao índice: pesquisa Java sensível a maiúsculas/minúsculas com GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Como adicionar documentos ao índice com GroupDocs.Search para Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)