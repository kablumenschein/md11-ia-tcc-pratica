# GerenciadorDeTarefas

## Contexto
Console app simples em C# (.NET 8) que gerencia uma lista de tarefas em memória:
adicionar, concluir e listar. Não há banco de dados nem persistência — os dados
se perdem ao fechar o programa. O projeto é propositalmente pequeno e serve de
base para praticar o uso de IA na avaliação do Módulo 11.

## Estrutura
- `GerenciadorDeTarefas/Program.cs` — todo o código, em top-level statements (sem `class Program` nem `Main`).
- Estado: `tarefas` é uma `List<(int Id, string Titulo, bool Concluida)>` (lista de tuplas nomeadas) e `proximoId` é o contador de IDs.
- Operações são **funções locais**: `Adicionar(string titulo)`, `Concluir(int id)`, `Listar()`.
- Depois das funções vem o fluxo principal: cria tarefas de exemplo, lista, conclui uma e lista de novo.
- `GerenciadorDeTarefas.csproj` — .NET 8, `ImplicitUsings` e `Nullable` habilitados.

## Convenções de código
- Nomes em **português**: variáveis em camelCase (`proximoId`), funções em PascalCase com verbo no infinitivo (`Adicionar`, `Concluir`).
- Novas operações devem ser **funções locais** declaradas junto das existentes, antes do fluxo principal.
- Usar `var` quando o tipo é óbvio e interpolação de string (`$"..."`).
- Tuplas são imutáveis: para alterar uma tarefa, substituir o item inteiro na lista (como `Concluir` faz).
- Formato de saída de uma tarefa: `[ ] #Id — Titulo` (pendente) ou `[X] #Id — Titulo` (concluída).
- Mensagens para o usuário em português.

## Comandos
Executar a partir da pasta `GerenciadorDeTarefas/`:
- Compilar: `dotnet build`
- Executar: `dotnet run`
Não há projeto de testes; a validação é compilar sem erros e conferir a saída no console.

## O que a IA NÃO deve fazer
- Não criar classes, novos arquivos ou pastas sem pedido explícito — manter tudo em `Program.cs`.
- Não trocar a lista de tuplas por classe/record nem mudar a estrutura dos dados.
- Não adicionar pacotes NuGet nem alterar o `.csproj`.
- Não remover o `Console.ReadLine()` do final (ele mantém a janela aberta).
- Não alterar funções existentes quando o pedido for apenas adicionar uma nova.
- Não mexer em `README.md`, `EVIDENCIAS.md` ou arquivos da pasta `.github`.
- Após qualquer alteração, rodar `dotnet build` e informar se compilou.