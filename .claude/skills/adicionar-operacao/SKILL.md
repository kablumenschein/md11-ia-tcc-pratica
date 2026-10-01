---
name: adicionar-operacao
description: Adiciona uma nova operação sobre a lista de tarefas (ex.: remover, editar título, listar pendentes) no Program.cs do GerenciadorDeTarefas, seguindo o padrão das funções locais existentes. Use quando o pedido for criar uma nova funcionalidade de manipulação de tarefas.
---

# Adicionar operação ao GerenciadorDeTarefas

## Quando usar
Quando o usuário pedir uma nova ação sobre as tarefas (remover, editar, filtrar, contar, etc.).
Não use para refatorações, mudanças de estrutura de dados ou criação de novos arquivos.

## Passos
1. Leia `GerenciadorDeTarefas/Program.cs` inteiro antes de alterar qualquer coisa.
2. Identifique o padrão das funções existentes (`Adicionar`, `Concluir`, `Listar`).
3. Crie a nova operação como **função local**, com nome em português e verbo no infinitivo
   (ex.: `Remover`, `EditarTitulo`, `ListarPendentes`), logo após as funções existentes
   e antes do fluxo principal.
4. Siga as convenções:
   - parâmetros simples (`int id`, `string titulo`);
   - busca por Id com laço `for` sobre `tarefas`, como em `Concluir`;
   - para alterar uma tarefa, substitua a tupla inteira (tuplas são imutáveis na lista);
   - saída no formato `[ ] #Id — Titulo` / `[X] #Id — Titulo`;
   - se o Id não existir, não lançar exceção — apenas não alterar nada
     (ou exibir uma mensagem curta em português, se o usuário pedir).
5. Adicione **uma** chamada de demonstração no fluxo principal, antes do `Console.ReadLine()`,
   com um `Console.WriteLine` de cabeçalho no mesmo estilo (`=== ... ===`).
6. Não altere funções existentes, não crie classes, arquivos ou pacotes.

## Verificação
- [ ] `dotnet build` dentro de `GerenciadorDeTarefas/` compila sem erros
- [ ] `dotnet run` mostra a nova operação funcionando
- [ ] Nenhum arquivo além de `Program.cs` foi alterado
- [ ] `Console.ReadLine()` continua no final

Ao terminar, informe ao usuário: o nome da função criada, onde foi inserida e o resultado do build.