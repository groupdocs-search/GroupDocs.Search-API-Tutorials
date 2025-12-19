---
date: '2025-12-19'
description: Aprenda como adicionar documentos ao índice e habilitar a pesquisa baseada
  em fragmentos em Java usando o GroupDocs.Search, aumentando o desempenho para grandes
  conjuntos de documentos.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Adicionar documentos ao índice com busca baseada em fragmentos em Java
type: docs
url: /pt/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Adicionar documentos ao índice com pesquisa baseada em fragmentos em Java

No mundo orientado a dados de hoje, ser capaz de **adicionar documentos ao índice** rapidamente e, em seguida, executar pesquisas baseadas em fragmentos é essencial para qualquer aplicação que manipule grandes coleções de arquivos. Seja lidando com contratos legais, arquivos de suporte ao cliente ou vastas bibliotecas de pesquisa, este tutorial mostra exatamente como configurar o GroupDocs.Search para Java para que você possa indexar documentos de forma eficiente e recuperar informações relevantes em fragmentos pequenos.

## O que você aprenderá
- Como criar um índice de pesquisa em uma pasta especificada.  
- Etapas para **adicionar documentos ao índice** a partir de múltiplas localizações.  
- Configuração de opções de pesquisa para habilitar a pesquisa baseada em fragmentos.  
- Execução de pesquisas iniciais e subsequentes baseadas em fragmentos.  
- Cenários do mundo real onde a pesquisa de documentos baseada em fragmentos se destaca.

## Respostas rápidas
- **Qual é o primeiro passo?** Crie uma pasta de índice de pesquisa.  
- **Como incluir muitos arquivos?** Use `index.add()` para cada pasta de documentos.  
- **Qual opção habilita a pesquisa por fragmentos?** `options.setChunkSearch(true)`.  
- **Posso continuar pesquisando após o primeiro fragmento?** Sim, chame `index.searchNext()` com o token.  
- **Preciso de licença?** Uma avaliação gratuita ou licença temporária funciona para desenvolvimento; uma licença completa é necessária para produção.

## Pré‑requisitos
Para seguir este guia, certifique‑se de que você tem:

- **Bibliotecas necessárias**: GroupDocs.Search para Java 25.4 ou posterior.  
- **Configuração do ambiente**: Um Java Development Kit (JDK) compatível instalado.  
- **Pré‑requisitos de conhecimento**: Programação básica em Java e familiaridade com Maven.

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

### Aquisição de licença
Para experimentar o GroupDocs.Search:

- **Avaliação gratuita** – teste os recursos principais sem compromisso.  
- **Licença temporária** – acesso estendido para desenvolvimento.  
- **Compra** – licença completa para uso em produção.

### Inicialização e configuração básicas
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
Agora que o índice existe, o próximo passo lógico é **adicionar documentos ao índice** a partir das localizações onde seus arquivos estão armazenados.

### 1. Criando um índice
**Visão geral**: Configure um diretório para o índice de pesquisa.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Adicionando documentos ao índice
**Visão geral**: Importe arquivos de várias pastas de origem.

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

### 3. Configurando opções de pesquisa para pesquisa por fragmentos
Habilite a pesquisa baseada em fragmentos ajustando o objeto de opções.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Executando a pesquisa inicial baseada em fragmentos
Execute a primeira consulta usando as opções habilitadas para fragmentos.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuando a pesquisa baseada em fragmentos
Itere pelos fragmentos restantes até que a pesquisa seja concluída.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Por que usar pesquisa baseada em fragmentos?
A pesquisa baseada em fragmentos divide coleções massivas de documentos em partes gerenciáveis, reduzindo a pressão de memória e acelerando os tempos de resposta. É especialmente benéfica quando:

1. **Equipes jurídicas** precisam localizar cláusulas específicas em milhares de contratos.  
2. **Portais de suporte ao cliente** devem exibir artigos relevantes da base de conhecimento instantaneamente.  
3. **Pesquisadores** analisam conjuntos de dados extensos sem carregar arquivos inteiros na memória.

## Considerações de desempenho
- **Gerenciamento de memória** – Aloque espaço de heap suficiente (`-Xmx`) para índices grandes.  
- **Monitoramento de recursos** – Fique atento ao uso de CPU durante as operações de indexação e pesquisa.  
- **Manutenção do índice** – Reconstrua ou limpe periodicamente o índice para descartar dados obsoletos.

## Armadilhas comuns e solução de problemas
| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| `OutOfMemoryError` durante a indexação | Heap insuficiente | Aumente o heap da JVM (`-Xmx2g` ou superior) |
| Nenhum resultado retornado | Token de fragmento não processado | Garanta que o loop `while` execute até `getNextChunkSearchToken()` ser `null` |
| Desempenho de pesquisa lento | Índice não otimizado | Execute `index.optimize()` após adições em massa |

## Perguntas frequentes

**Q: O que é pesquisa baseada em fragmentos?**  
A: A pesquisa baseada em fragmentos divide o conjunto de dados em partes menores, permitindo consultas eficientes em grandes volumes de dados sem carregar documentos inteiros na memória.

**Q: Como atualizo meu índice com novos arquivos?**  
A: Basta chamar `index.add()` com o caminho para os novos documentos; o índice os incorporará automaticamente.

**Q: O GroupDocs.Search suporta diferentes formatos de arquivo?**  
A: Sim, ele suporta PDFs, DOCX, XLSX, PPTX e muitos outros formatos comuns.

**Q: Quais são os gargalos de desempenho típicos?**  
A: Restrições de memória e índices não otimizados são os mais comuns; aloque heap suficiente e otimize o índice regularmente.

**Q: Onde posso encontrar documentação mais detalhada?**  
A: Visite a documentação oficial do [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) para guias aprofundados e referências de API.

## Recursos
- **Documentação**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referência de API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Suporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Licença temporária**: [Obter uma Licença Temporária](https://purchase.groupdocs.com/temporary-license)

---

**Última atualização:** 2025-12-19  
**Testado com:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

---