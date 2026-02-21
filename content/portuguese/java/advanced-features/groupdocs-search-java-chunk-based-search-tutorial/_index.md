---
date: '2026-02-21'
description: Aprenda como adicionar documentos ao índice e aumentar o desempenho da
  pesquisa com busca baseada em blocos em Java usando o GroupDocs.Search, otimizando
  a memória do índice de pesquisa Java para grandes conjuntos de documentos.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Adicionar documentos ao índice com busca baseada em fragmentos em Java
type: docs
url: /pt/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Adicionar documentos ao índice com pesquisa baseada em blocos em Java

Em aplicações modernas que precisam **adicionar documentos ao índice** rapidamente e, em seguida, executar consultas rápidas baseadas em blocos, você desejará uma solução que escale sem estourar a memória. Este tutorial orienta você a configurar o GroupDocs.Search para Java, adicionar várias pastas de documentos e configurar o mecanismo para **aumentar o desempenho da pesquisa** enquanto mantém o uso de **java search index memory** sob controle. Seja indexando contratos legais, tickets de suporte ou artigos de pesquisa, os passos abaixo fornecerão uma implementação pronta para produção.

## Respostas Rápidas
- **Qual é o primeiro passo?** Crie uma pasta de índice de pesquisa.  
- **Como incluo muitos arquivos?** Use `index.add()` para cada pasta de documentos.  
- **Qual opção habilita a pesquisa por blocos?** `options.setChunkSearch(true)`.  
- **Posso continuar a pesquisa após o primeiro bloco?** Sim, chame `index.searchNext()` com o token.  
- **Preciso de uma licença?** Um teste gratuito ou licença temporária funciona para desenvolvimento; uma licença completa é necessária para produção.  

## O que você aprenderá
- Como criar um índice de pesquisa em uma pasta especificada.  
- Passos para **adicionar documentos ao índice** a partir de múltiplas localidades.  
- Configurar opções de pesquisa para habilitar a pesquisa baseada em blocos.  
- Executar pesquisas iniciais e subsequentes baseadas em blocos.  
- Cenários reais onde a pesquisa de documentos baseada em blocos se destaca.  

## Pré-requisitos
Para seguir este guia, certifique-se de que você tem:

- **Bibliotecas necessárias**: GroupDocs.Search for Java 25.4 ou posterior.  
- **Configuração do ambiente**: Um Java Development Kit (JDK) compatível instalado.  
- **Pré-requisitos de conhecimento**: Programação básica em Java e familiaridade com Maven.

## Configurando o GroupDocs.Search para Java
Para começar, integre o GroupDocs.Search ao seu projeto usando Maven:

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

Alternativamente, faça o download da versão mais recente em [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Aquisição de Licença
Para experimentar o GroupDocs.Search:

- **Teste gratuito** – teste os recursos principais sem compromisso.  
- **Licença temporária** – acesso estendido para desenvolvimento.  
- **Compra** – licença completa para uso em produção.

### Inicialização e Configuração Básicas
Crie um índice na pasta onde você deseja que os dados pesquisáveis residam:

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

## Como adicionar documentos ao índice
Agora que o índice existe, o próximo passo lógico é **adicionar documentos ao índice** a partir dos locais onde seus arquivos estão armazenados.

### 1. Criando um Índice
**Visão geral**: Configure um diretório para o índice de pesquisa.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Adicionando Documentos ao Índice
**Visão geral**: Traga arquivos de várias pastas de origem.

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

### 3. Configurando Opções de Pesquisa para Busca por Blocos
Habilite a pesquisa baseada em blocos ajustando o objeto de opções.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Executando a Busca Inicial Baseada em Blocos
Execute a primeira consulta usando as opções habilitadas para blocos.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuando a Busca Baseada em Blocos
Itere pelos blocos restantes até que a busca esteja completa.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Por que usar busca baseada em blocos?
A busca baseada em blocos divide coleções massivas de documentos em peças manejáveis, reduzindo a pressão de memória e acelerando os tempos de resposta. É especialmente benéfica quando:

1. **Equipes jurídicas** precisam localizar cláusulas específicas em milhares de contratos.  
2. **Portais de suporte ao cliente** devem exibir artigos relevantes da base de conhecimento instantaneamente.  
3. **Pesquisadores** vasculham conjuntos de dados extensos sem carregar arquivos inteiros na memória.  

## Como esta abordagem **aumenta o desempenho da pesquisa**
Ao pesquisar blocos menores em vez de arquivos inteiros, o mecanismo pode:

- Ignorar seções irrelevantes cedo, reduzindo ciclos de CPU.  
- Manter apenas o bloco ativo na memória, o que reduz diretamente o consumo de **java search index memory**.  
- Paralelizar o processamento de blocos em máquinas multi‑core para resultados mais rápidos.  

## Gerenciando **java search index memory**
Embora a busca baseada em blocos já reduza a pegada de memória, você pode ajustar ainda mais a JVM:

- Alocar heap suficiente (`-Xmx2g` ou superior) com base no tamanho do índice.  
- Use `index.optimize()` após adições em massa para comprimir a estrutura do índice.  
- Monitore pausas de GC com ferramentas como VisualVM para evitar picos de latência.  

## Considerações de Desempenho
- **Gerenciamento de memória** – Alocar espaço de heap suficiente (`-Xmx`) para índices grandes.  
- **Monitoramento de recursos** – Fique de olho no uso de CPU durante as operações de indexação e busca.  
- **Manutenção do índice** – Reconstrua ou limpe periodicamente o índice para descartar dados obsoletos.  

## Armadilhas Comuns & Solução de Problemas
| Problema | Por que acontece | Solução |
|----------|------------------|--------|
| `OutOfMemoryError` during indexing | Tamanho do heap muito baixo | Aumente o heap da JVM (`-Xmx2g` ou superior) |
| No results returned | Token de bloco não processado | Garanta que o loop `while` execute até que `getNextChunkSearchToken()` seja `null` |
| Slow search performance | Índice não otimizado | Execute `index.optimize()` após adições em massa |

## Perguntas Frequentes

**Q: O que é busca baseada em blocos?**  
A: A busca baseada em blocos divide o conjunto de dados em peças menores, permitindo consultas eficientes sobre grandes volumes de dados sem carregar documentos inteiros na memória.

**Q: Como atualizo meu índice com novos arquivos?**  
A: Basta chamar `index.add()` com o caminho para os novos documentos; o índice os incorporará automaticamente.

**Q: O GroupDocs.Search pode lidar com diferentes formatos de arquivo?**  
A: Sim, ele suporta PDFs, DOCX, XLSX, PPTX e muitos outros formatos comuns.

**Q: Quais são os gargalos de desempenho típicos?**  
A: Restrições de memória e índices não otimizados são os mais comuns; aloque heap suficiente e otimize o índice regularmente.

**Q: Onde posso encontrar documentação mais detalhada?**  
A: Visite a [Documentação oficial do GroupDocs.Search](https://docs.groupdocs.com/search/java/) para guias detalhados e referências de API.

**Q: A busca baseada em blocos funciona com PDFs criptografados?**  
A: Sim, desde que você forneça a senha via a sobrecarga de API apropriada.

**Q: Como posso monitorar o progresso da indexação?**  
A: Use a sobrecarga `Index.add()` que retorna um objeto `Progress` ou conecte-se a callbacks de registro.

## Recursos
- **Documentação**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referência de API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Suporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licença temporária**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última atualização:** 2026-02-21  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---