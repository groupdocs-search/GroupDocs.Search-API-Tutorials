---
date: '2026-06-07'
description: Aprenda como implementar alta compressão .NET para armazenamento de texto
  e redigir dados confidenciais usando GroupDocs.Search e GroupDocs.Redaction em aplicações
  .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Implementar Alta Compressão .NET com GroupDocs: Guia de Texto e Redação'
type: docs
url: /pt/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementar Alta Compressão .NET com GroupDocs: Guia de Texto e Redação

Em soluções .NET modernas, **implement high compression .net** é essencial quando você precisa armazenar coleções massivas de texto sem aumentar o uso de disco. Ao mesmo tempo, proteger informações sensíveis — como identificadores pessoais ou dados financeiros — requer redação confiável. Este tutorial mostra, passo a passo, como configurar o armazenamento de texto com alta compressão usando **GroupDocs.Search** e como redigir com segurança dados confidenciais usando **GroupDocs.Redaction**. Ao final, você poderá comprimir texto indexado em até 90 % e remover conteúdo privado de PDFs, arquivos Word e muitos outros formatos.

## Respostas Rápidas
- **Qual biblioteca fornece indexação de alta compressão?** GroupDocs.Search for .NET.  
- **Qual ferramenta redige dados sensíveis?** GroupDocs.Redaction for .NET.  
- **Posso adicionar documentos ao índice automaticamente?** Sim — use a API `AddDocument` dentro de um loop de varredura de pasta.  
- **A compressão é sem perdas para busca?** Sim, o texto permanece totalmente pesquisável após a compressão.  
- **Preciso de licença para produção?** Uma licença permanente do GroupDocs é necessária para uso comercial.

## O que é “implement high compression .net”?
Implement high compression .net significa configurar o mecanismo de indexação GroupDocs.Search para armazenar o conteúdo textual extraído em forma comprimida. Isso reduz o tamanho do índice em disco drasticamente, mantendo o texto totalmente pesquisável. A compressão é sem perdas, portanto a relevância das consultas e a extração de trechos funcionam exatamente como em um índice não comprimido.

## Por que usar GroupDocs para compressão e redação?
GroupDocs.Search suporta mais de cinquenta formatos de entrada e pode comprimir texto indexado em até noventa por cento, permitindo que grandes coleções de documentos ocupem apenas uma fração de seu tamanho original. GroupDocs.Redaction complementa isso apagando ou mascarando permanentemente informações sensíveis em mais de trinta tipos de arquivos, ajudando você a cumprir regulamentos rigorosos de conformidade como GDPR e HIPAA sem ferramentas adicionais.

## Pré-requisitos
- **Ambiente de desenvolvimento:** Visual Studio 2022 ou posterior, .NET 6+ (ou .NET Framework 4.7.2).  
- **Bibliotecas:** pacotes NuGet `GroupDocs.Search` e `GroupDocs.Redaction`.  
- **Permissões:** Acesso de leitura/gravação às pastas que contêm os documentos de origem e o local de saída do índice.  
- **Conhecimento básico:** sintaxe C#, I/O de arquivos e familiaridade com a estrutura de projetos .NET.

## Como implementar alta compressão .NET com GroupDocs?
Para implementar alta compressão .NET com GroupDocs, primeiro crie uma instância `TextStorageSettings` e defina seu `CompressionLevel` como `High`. Em seguida, instancie um objeto `Index`, passando as configurações e a pasta onde o índice será armazenado. Depois que o índice estiver pronto, adicione documentos usando `AddDocument` e, finalmente, execute buscas com o método `Search`, tudo enquanto o mecanismo lida de forma transparente com compressão e descompressão.

### Etapa 1: Instalar os pacotes NuGet necessários
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Pesquise por “GroupDocs.Search” e clique em **Install**.  

### Etapa 2: Instalar GroupDocs.Redaction (para redação de dados)
- Abra o **NuGet Package Manager**.  
- Pesquise por **GroupDocs.Redaction** e instale a versão estável mais recente.  

### Etapa 3: Obter e aplicar uma licença
- **Teste gratuito:** Registre-se no portal GroupDocs para obter uma chave de avaliação de 30 dias.  
- **Licença temporária:** Solicite uma chave temporária para ambientes de desenvolvimento.  
- **Licença permanente:** Compre uma licença de produção para remover limitações de avaliação.  

### Etapa 4: Inicialização básica de ambas as bibliotecas
O `Search` e o `Redaction` engines compartilham um modelo de licenciamento comum. Inicialize-os na inicialização da aplicação:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Recurso 1: Configurações de Armazenamento de Texto com Alta Compressão

### Configurando a Configuração de Indexação
`TextStorageSettings` é a classe que indica ao GroupDocs.Search como manter o texto extraído. Habilitar alta compressão reduz o tamanho do índice em até **10×** sem afetar a velocidade de busca.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explicação:**  
- `CompressionLevel.High` ativa um algoritmo baseado em ZSTD que comprime blocos de texto de forma eficiente.  
- `UseMemoryCache = false` força o mecanismo a transmitir dados do disco, o que é ideal para implantações em grande escala.

### Criando e Gerenciando o Índice
O objeto `Index` representa o repositório pesquisável no disco. Você especifica a pasta onde os arquivos de índice serão armazenados e passa as configurações de compressão definidas acima.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Explicação:**  
- `indexFolder` determina onde os arquivos de índice comprimidos residem.  
- `settings` injeta a configuração de alta compressão, garantindo que cada documento adicionado se beneficie dela.

## Recurso 2: Adicionando Documentos ao Índice

### Adicionar Documentos ao Seu Índice
`AddDocument` adiciona um único arquivo ao índice, extraindo seu texto, comprimindo-o de acordo com as configurações definidas e armazenando o resultado. GroupDocs.Search pode ingerir arquivos de uma árvore de diretórios. O loop a seguir percorre `documentsFolder`, adiciona cada arquivo e registra o progresso.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Explicação:**  
- `AddDocument` analisa o arquivo, extrai texto pesquisável, comprime-o de acordo com `TextStorageSettings` e o armazena no índice.  
- Essa abordagem funciona para **PDF, DOCX, TXT, HTML** e mais de **30** outros formatos.

## Recurso 3: Executando uma Consulta de Busca

### Executar uma Busca
`Search` executa uma consulta contra o índice comprimido e retorna uma coleção de objetos `DocumentResult` correspondentes com pontuações de relevância e trechos destacados. Uma vez que o índice esteja populado, você pode executar consultas rápidas. O método `Search` retorna uma coleção de objetos `DocumentResult` que incluem caminhos de arquivo e trechos destacados.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Explicação:**  
- O motor de busca varre o texto comprimido diretamente, portanto a latência da consulta permanece baixa mesmo para índices que contêm **milhões de páginas**.  
- `Score` indica relevância; valores mais altos significam uma correspondência melhor.

## Como redigir dados confidenciais com GroupDocs.Redaction?
Redigir dados confidenciais com GroupDocs.Redaction começa criando uma instância `Redactor` para o arquivo alvo. Defina um ou mais objetos `SearchPattern` que descrevem o texto a ser removido, como expressões regulares para números de segurança social. Aplique cada padrão usando `Redact`, especificando um `RedactionType` como `BlackOut`, e salve o resultado como um novo documento, garantindo que o original permaneça intocado.

`Redactor` é a classe principal no GroupDocs.Redaction usada para carregar um documento e executar operações de redação.  
`SearchPattern` define uma expressão regular que identifica o texto a ser redigido.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explicação:**  
- `SearchPattern` usa uma expressão regular para localizar números de segurança social.  
- `RedactionType.BlackOut` substitui o texto correspondido por um retângulo preto sólido, garantindo que os dados não possam ser recuperados.

## Aplicações Práticas
1. **Gerenciamento de Documentos Legais:** Comprima automaticamente arquivos de casos massivos e redija identificadores de clientes antes de arquivar.  
2. **Registros de Saúde:** Armazene anos de notas de pacientes em um índice comprimido e remova PHI (Informação de Saúde Protegida) antes de compartilhar com parceiros de pesquisa.  
3. **Relatórios Financeiros:** Proteja relatórios trimestrais redigindo números de conta enquanto mantém o texto pesquisável para consultas de auditoria.

## Considerações de Desempenho
- **Impacto da compressão:** Alta compressão reduz o tamanho do índice em até **90 %**, o que diminui o desgaste do SSD e acelera as operações de backup.  
- **Uso de memória:** Desative o cache em memória para índices muito grandes para manter a pegada do processo abaixo de **500 MB**.  
- **Otimização de I/O:** Adicione documentos em lotes de 100 para minimizar a sobrecarga de disco.  
- **Processamento assíncrono:** Envolva chamadas `AddDocument` em `Task.Run` para manter as threads de UI responsivas em aplicativos desktop.

## Armadilhas Comuns & Solução de Problemas
- **Caminhos de arquivo incorretos:** Verifique se `documentsFolder` e `indexFolder` são caminhos absolutos e se o aplicativo tem permissões de leitura/gravação.  
- **Erros de licença:** Certifique-se de que os arquivos `.lic` estejam implantados ao lado do executável ou incorporados como recursos.  
- **Busca não retorna resultados:** Verifique se o nível de compressão `TextStorageSettings` corresponde ao usado durante a indexação; configurações incompatíveis podem causar falhas de desserialização.  

## Perguntas Frequentes

**Q: Posso adicionar documentos ao índice após a construção inicial?**  
A: Sim — basta chamar `index.AddDocument` para novos arquivos; o mecanismo atualiza o índice comprimido incrementalmente.

**Q: A redação altera o arquivo original?**  
A: Não — o arquivo original permanece intocado; a versão redigida é salva como um novo arquivo, preservando a integridade do documento.

**Q: Quais formatos o GroupDocs.Redaction suporta?**  
A: Mais de **30** formatos, incluindo PDF, DOCX, PPTX, XLSX, imagens (PNG, JPEG) e texto simples.

**Q: Como a alta compressão afeta a relevância da busca?**  
A: Não afeta. A compressão é sem perdas para texto, portanto as pontuações de relevância são idênticas a um índice não comprimido.

**Q: Existe um limite para o tamanho dos documentos que posso indexar?**  
A: O GroupDocs.Search pode lidar com arquivos de vários gigabytes transmitindo o conteúdo; porém, garanta espaço em disco suficiente para o índice comprimido (aproximadamente 10 % do tamanho original).

## Recursos
- [Documentação](https://docs.groupdocs.com/search/net/)
- [Referência da API](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction para .NET](https://releases.groupdocs.com/search/net/)
- [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/search/10)
- [Aquisição de Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

---

**Última Atualização:** 2026-06-07  
**Testado com:** GroupDocs.Search 23.12 e GroupDocs.Redaction 23.12 para .NET  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Implementando GroupDocs.Search e Redaction em .NET para Gerenciamento de Documentos](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Como Otimizar GroupDocs.Redaction para .NET: Guia de Gerenciamento Eficiente de Índice e Ortografia](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Domine GroupDocs Redaction e Search em .NET: Gerenciamento Eficiente de Documentos e Busca Segura](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)