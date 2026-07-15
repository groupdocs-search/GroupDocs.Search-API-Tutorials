---
date: '2026-04-02'
description: Aprenda a filtrar por extensão de arquivo e pesquisar apenas arquivos
  txt com o GroupDocs.Redaction para .NET — aumente a eficiência da gestão de documentos.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtrar por extensão de arquivo em .NET usando GroupDocs.Redaction
type: docs
url: /pt/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filtrar por extensão de arquivo no .NET usando GroupDocs.Redaction

Pesquisar em uma coleção massiva de arquivos pode ser assustador, especialmente quando você só precisa de resultados de tipos de arquivo específicos. Neste tutorial você descobrirá **como filtrar por extensão de arquivo** com o GroupDocs.Redaction para .NET, permitindo pesquisar apenas arquivos txt ou qualquer outra extensão que escolher. Vamos percorrer a configuração de filtros baseados em tipo de arquivo e em caminho, para que você possa localizar rapidamente exatamente os documentos que precisa.

## Respostas Rápidas
- **O que faz “filtrar por extensão de arquivo”?** Limita uma pesquisa a documentos que correspondem a uma determinada extensão de arquivo (por exemplo, *.txt).  
- **Por que usar o GroupDocs.Redaction para isso?** Ele fornece APIs de filtragem integradas que são rápidas e fáceis de integrar.  
- **Preciso de uma licença?** Um teste gratuito funciona para testes; uma licença paga é necessária para produção.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Posso combinar filtros de tipo de arquivo e de caminho?** Sim—aplique múltiplos filtros para pesquisas altamente precisas.

## O que você aprenderá
- Como **filtrar por extensão de arquivo** para que apenas arquivos de texto sejam pesquisados.  
- Como configurar **filtros de caminho de arquivo** para restringir resultados a pastas específicas ou padrões de nomenclatura.  
- Dicas para manter seu índice rápido e eficiente em memória.

## Pré-requisitos

Antes de mergulhar, certifique‑se de que você tem:

- **Biblioteca GroupDocs.Redaction** instalada e compatível com seu projeto .NET.  
- Um ambiente de desenvolvimento como Visual Studio ou VS Code.  
- Conhecimento básico de C# e familiaridade com a estrutura de projetos .NET.

## Configurando GroupDocs.Redaction para .NET

Primeiro, adicione a biblioteca ao seu projeto.

**Usando .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Usando Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Ou localize “GroupDocs.Redaction” na UI do NuGet Package Manager e instale a versão mais recente.

### Aquisição de Licença

Você pode começar com um teste gratuito ou solicitar uma licença temporária. Para projetos de longo prazo, compre uma licença no site oficial.

### Inicialização Básica

Depois que o pacote for instalado, crie um índice que armazenará referências aos seus documentos:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Guia de Implementação

### Recurso 1: Definindo um filtro para documentos de texto (.txt)

#### Como filtrar por extensão de arquivo para documentos de texto

1. **Defina o índice e as pastas de documentos**  
   Defina os caminhos onde seus arquivos de origem estão localizados:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Crie um Índice**  
   Carregue todos os arquivos da pasta de origem no índice:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Configure as Opções de Busca com um filtro de extensão de arquivo**  
   Instrua o mecanismo a considerar apenas arquivos *.txt:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Execute a busca**  
   Execute uma consulta; o filtro garante que arquivos não‑texto sejam ignorados:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explicação*: O método `Search` retorna correspondências que atendem ao filtro, reduzindo drasticamente o ruído e melhorando o desempenho.

### Recurso 2: Filtros de Caminho de Arquivo

#### Por que usar filtros de caminho de arquivo?

Às vezes você precisa limitar pesquisas a uma pasta de departamento específica ou a um conjunto de arquivos que compartilham uma convenção de nomenclatura. Filtros de caminho permitem fazer exatamente isso.

1. **Defina o índice e as pastas de documentos**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Crie um Índice**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Configure as Opções de Busca com uma expressão regular baseada em caminho**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Esta expressão regular corresponde a qualquer arquivo cujo caminho completo contenha a palavra “Lorem”, permitindo direcionar sub‑pastas específicas.

4. **Execute a busca baseada em caminho**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Aplicações Práticas
- **Gerenciamento de Documentos Legais** – Localize rapidamente contratos relevantes armazenados como arquivos de texto simples.  
- **Pesquisa Acadêmica** – Extraia apenas notas de pesquisa *.txt que pertençam a uma pasta de projeto específica.  
- **Relatórios Corporativos** – Filtre relatórios internos por caminho de departamento (por exemplo, `/Finance/2025/`).  

## Considerações de Desempenho
- Indexe apenas os tipos de documento que realmente precisa; arquivos desnecessários aumentam o tamanho do índice e o tempo de busca.  
- Mantenha seu índice atualizado com um job agendado que chame `index.Add()` para arquivos novos ou alterados.  
- Use expressões regulares simples; padrões excessivamente complexos podem desacelerar o mecanismo de busca.  
- Libere objetos `Index` quando não forem mais necessários para liberar memória.

## Conclusão
Agora você sabe como **filtrar por extensão de arquivo** e aplicar **filtros de caminho de arquivo** usando o GroupDocs.Redaction para .NET. Essas técnicas dão controle granular sobre grandes coleções de documentos, tornando as buscas mais rápidas e relevantes. Em seguida, experimente combinar múltiplos filtros ou integrar a busca em um fluxo de trabalho de aplicação maior.

## Seção de Perguntas Frequentes

**Q1: Posso filtrar documentos que não sejam arquivos de texto?**  
A1: Sim, o GroupDocs.Redaction suporta muitos formatos. Altere o argumento em `CreateFileExtension` para a extensão desejada (por exemplo, ".pdf").

**Q2: Como atualizo meu índice de busca regularmente?**  
A2: Agende um serviço em segundo plano ou um job cron que execute `index.Add()` nos diretórios que você deseja manter atualizados.

**Q3: Existe impacto de desempenho ao filtrar por caminho de arquivo?**  
A3: Expressões regulares bem otimizadas têm impacto mínimo, mas sempre faça benchmark com seu próprio conjunto de dados.

**Q4: Posso combinar múltiplos filtros para buscas mais refinadas?**  
A4: Absolutamente. Você pode encadear filtros ou criar filtros compostos para direcionar simultaneamente tipo de arquivo e caminho.

**Q5: Onde posso encontrar mais recursos sobre o GroupDocs.Redaction?**  
A5: Visite a documentação oficial em [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) para guias detalhados e referências de API.

## Perguntas Frequentes

**Q: O `SearchDocumentFilter` funciona com arquivos criptografados?**  
A: O filtro opera sobre os metadados do arquivo, portanto arquivos criptografados ainda são indexados se você fornecer as credenciais de descriptografia necessárias durante a indexação.

**Q: Posso usar curingas em vez de uma expressão regular para filtragem de caminho?**  
A: A API atualmente requer uma expressão regular, mas você pode simular curingas simples (por exemplo, `.*` para quaisquer caracteres).

**Q: Quão grande pode ser o índice antes de eu precisar considerar sharding?**  
A: Índices de várias centenas de gigabytes podem se beneficiar de divisão em múltiplos índices lógicos; teste o desempenho à medida que sua coleção cresce.

**Q: Existem métodos incorporados para remover documentos do índice?**  
A: Sim—chame `index.Delete(documentId)` ou `index.DeleteAll()` para gerenciar entradas obsoletas.

**Q: Há como pré‑visualizar resultados de busca antes de carregar o documento completo?**  
A: O objeto `SearchResult` inclui informações de snippet que podem ser exibidas na UI sem abrir o arquivo inteiro.

## Recursos
- **Documentation**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última atualização:** 2026-04-02  
**Testado com:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs