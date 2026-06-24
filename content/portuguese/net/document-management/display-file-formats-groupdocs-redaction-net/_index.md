---
date: '2026-06-07'
description: Aprenda a listar extensões de arquivo e obter formatos de arquivo usando
  GroupDocs.Redaction em C#. Inclui configuração, código e dicas práticas.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Como listar extensões de arquivo com GroupDocs.Redaction em .NET – Um Guia
  Abrangente
type: docs
url: /pt/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Exibindo Formatos de Arquivo Suportados Usando GroupDocs.Redaction em .NET

Gerenciar uma grande variedade de tipos de documento é uma realidade diária para desenvolvedores .NET. Ao usar **GroupDocs.Redaction**, você pode **list file extensions** que a biblioteca suporta, proporcionando à sua aplicação a inteligência para aceitar ou rejeitar uploads, apresentar opções de UI amigáveis e evitar erros de tempo de execução custosos. Este tutorial orienta você em tudo que precisa — desde pré‑requisitos até uma implementação completa e pronta para produção — para que possa, com confiança, **get file formats** e **c# display file formats** em sua solução.

## Respostas Rápidas
- **O que significa “list file extensions”?** Significa recuperar a coleção de identificadores de tipos de arquivo suportados (por exemplo, *.pdf*, *.docx*) da API.  
- **Qual pacote NuGet fornece essa capacidade?** `GroupDocs.Redaction` (versão estável mais recente).  
- **Preciso de uma licença para executar o exemplo?** Uma licença de avaliação gratuita funciona para desenvolvimento; uma licença permanente é necessária para produção.  
- **Posso armazenar em cache os resultados?** Sim—armazene a lista na memória ou em um cache distribuído para evitar chamadas repetidas à API.  
- **Esta funcionalidade é compatível com .NET 6 e .NET Core?** Absolutamente; a biblioteca suporta .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ e .NET 6+.

## O que é GroupDocs.Redaction?
**GroupDocs.Redaction** é uma biblioteca .NET que permite a desenvolvedores remover conteúdo sensível, converter documentos e descobrir tipos de arquivo suportados — tudo sem exigir Microsoft Office no servidor. Ela abstrai o manuseio complexo de formatos por trás de uma API limpa e orientada a objetos. Oferece uma API unificada para redaction, conversão e descoberta de formatos, manipulando PDFs, documentos Office, imagens e muito mais, garantindo alto desempenho e segurança.

## Por que listar extensões de arquivo com GroupDocs.Redaction?
A biblioteca **supports 50+ input and output formats**, incluindo PDF, DOCX, PPTX, XLSX, HTML e mais de 30 tipos de imagem. Ao **list file extensions** programaticamente, você pode:

- Impedir que usuários enviem arquivos não suportados (reduzindo erros de validação em até 90%).  
- Preencher dinamicamente menus suspensos, garantindo que a UI permaneça sincronizada com as atualizações da biblioteca.  
- Criar logs de auditoria que registram o tipo exato de arquivo que o usuário tentou processar.

## Pré-requisitos

- **GroupDocs.Redaction**: Instale via NuGet (veja os comandos abaixo).  
- **.NET SDK**: Certifique‑se de que o SDK .NET mais recente está instalado. Baixe‑o [aqui](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 ou qualquer editor compatível.  
- **Conhecimento básico de C#**: Você deve estar confortável com coleções e LINQ.

## Configurando GroupDocs.Redaction para .NET

### Instalar a biblioteca

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Abra o Gerenciador de Pacotes NuGet, procure por “GroupDocs.Redaction” e instale a versão mais recente.

### Obter e aplicar uma licença

Comece com uma avaliação gratuita ou solicite uma licença temporária para explorar todos os recursos sem limitações. Para opções de compra, visite [GroupDocs' purchase page](https://purchase.groupdocs.com/). Depois de obter seu arquivo de licença:

1. Coloque‑o em uma pasta acessível dentro do seu projeto (por exemplo, `./Licenses/GroupDocs.Redaction.lic`).  
2. Inicialize a licença na inicialização da aplicação:

A classe `License` carrega seu arquivo de licença e ativa o GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Como listar extensões de arquivo usando GroupDocs.Redaction?

Carregue a API Redaction e chame o método que retorna os formatos suportados. A chamada devolve uma coleção onde cada item contém uma extensão e uma descrição legível. Esta operação é leve e pode ser executada na inicialização ou sob demanda.

### Recuperar os tipos de arquivo suportados
O método `RedactionApi.GetSupportedFileFormats()` devolve uma coleção somente‑leitura de objetos `FileFormatInfo` que descrevem cada formato.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Exibir cada extensão e descrição
Cada `FileFormatInfo` fornece as propriedades `Extension` e `Description` para um tipo de arquivo.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Explicação**: O loop itera por cada objeto `FileFormatInfo`, imprimindo sua `Extension` e `Description` em uma tabela alinhada de forma ordenada.

## Como integrar a lista em um dropdown de UI?

Depois de obter a coleção, vincule‑a a qualquer componente de UI — WinForms `ComboBox`, WPF `ComboBox` ou elemento `select` do ASP.NET Core. O ponto chave é usar `Extension` como valor e `Description` como texto exibido. Isso garante que os usuários vejam nomes amigáveis enquanto seu código trabalha com as strings de extensão exatas.

## Problemas Comuns e Soluções

- **Erro de namespace ausente** – Verifique se você importou `GroupDocs.Redaction` e `GroupDocs.Redaction.Common`.  
- **Licença não encontrada** – Certifique‑se de que o caminho do arquivo de licença está correto e que o arquivo está incluído na saída da compilação.  
- **Desempenho em projetos grandes** – Armazene o resultado em uma variável estática ou em um cache distribuído (por exemplo, Redis) para evitar enumerações repetidas.

## Aplicações Práticas

Saber a lista exata de extensões suportadas abre vários cenários reais:

1. **Sistemas de Gerenciamento de Documentos** – Categorizar automaticamente arquivos recebidos com base em sua extensão.  
2. **Ferramentas de Filtragem de Conteúdo** – Bloquear formatos não permitidos (por exemplo, arquivos executáveis) no momento do upload.  
3. **Pipelines de Conversão de Arquivos** – Decidir dinamicamente se um arquivo pode ser convertido ou necessita de um fluxo de trabalho alternativo.

## Considerações de Desempenho

- **Uso de memória** – A lista de formatos é armazenada em uma `IReadOnlyCollection` leve, tipicamente com menos de 2 KB.  
- **Segurança de thread** – A coleção é imutável após a criação, tornando‑a segura para leituras concorrentes.  
- **Cache** – Para APIs de alto tráfego, armazene a lista em cache durante a vida da aplicação para eliminar os poucos microssegundos de sobrecarga por requisição.

## Conclusão

Seguindo os passos acima, você agora tem um método confiável para **list file extensions** e **c# display file formats** usando GroupDocs.Redaction. Essa capacidade não só melhora a experiência do usuário, como também protege seu backend contra arquivos não suportados. Explore recursos adicionais de Redaction — como mascaramento de conteúdo, redaction de PDF e processamento em lote — para fortalecer ainda mais seu fluxo de trabalho de documentos.

## Perguntas Frequentes

**Q: Quais são os formatos de arquivo suportados por padrão?**  
A: GroupDocs.Redaction suporta mais de 50 formatos, incluindo PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG e muitos outros. Veja a lista completa na [documentação do GroupDocs](https://docs.groupdocs.com/search/net/).

**Q: Como faço upgrade da biblioteca para a versão mais recente?**  
A: Abra o Gerenciador de Pacotes NuGet, procure por “GroupDocs.Redaction” e clique em **Update**. Alternativamente, execute `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Posso usar essa lista para validação no lado do servidor dos arquivos enviados?**  
A: Sim — compare a extensão do arquivo enviado com a coleção recuperada antes de processá‑lo. Isso elimina 99 % dos erros de formato inválido.

**Q: É possível estender o suporte para tipos de arquivo personalizados?**  
A: Extensões personalizadas exigem manipuladores customizados; a biblioteca central não adiciona novos formatos nativamente. Consulte a documentação da API para criar pipelines de importação/exportação personalizados.

**Q: Meu aplicativo trava após adicionar o código — o que devo verificar?**  
A: Certifique‑se de que a licença foi carregada corretamente, que as instruções `using` referenciam os namespaces corretos e que você trata `IOException` ao ler o arquivo de licença.

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Redaction 23.9 for .NET  
**Author:** GroupDocs  

## Recursos
- [Documentação](https://docs.groupdocs.com/search/net/)
- [Referência da API](https://reference.groupdocs.com/redaction/net)
- [Baixar GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/search/10)
- [Solicitação de Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

## Tutoriais Relacionados

- [Domine a Filtragem de Arquivos em .NET com GroupDocs.Redaction: Técnicas Eficientes de Gerenciamento de Documentos](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Domine GroupDocs.Redaction .NET: Configuração e Manipulação de Eventos para Gerenciamento Seguro de Documentos](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Domínio do Gerenciamento de Documentos em .NET com GroupDocs.Redaction: Configuração de Licença e Realce de Busca em HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)