# Evidência de uso real da IA (Questão 11)

## Ferramenta
- **Claude Code** v2.1.241 (CLI), rodando no terminal na raiz do repositório
- Modelo: Claude Opus 5
- Modo de permissão: Auto mode
- Contexto usado: `CLAUDE.md` da raiz + skill `.claude/skills/adicionar-operacao/SKILL.md`

## Prompt exato
```
Use a skill adicionar-operacao para criar uma função Remover(int id) que remove uma tarefa pelo Id. Siga o CLAUDE.md do projeto.
```

## O que a IA fez
1. Carregou a skill `adicionar-operacao` (`Skill(adicionar-operacao) — Successfully loaded skill`).
2. Leu o `Program.cs` antes de alterar.
3. Criou a função local `Remover(int id)` logo após `Listar()` e antes do fluxo principal:
```csharp
   void Remover(int id)
   {
       for (var i = 0; i < tarefas.Count; i++)
       {
           if (tarefas[i].Id == id)
           {
               tarefas.RemoveAt(i);
               break;
           }
       }
   }
```
4. Adicionou uma demonstração antes do `Console.ReadLine()`:
```csharp
   Remover(2);

   Console.WriteLine();
   Console.WriteLine("=== Depois de remover a tarefa #2 ===");
   Listar();
```
5. Rodou `dotnet build`: **0 erros, 0 avisos**.
6. Terminou com um resumo: função criada, onde foi inserida e resultado do build. Tempo total: ~27s.

## Seguiu o CLAUDE.md e a Skill?
**Sim, quase totalmente:**
- ✅ Função local, nome em português com verbo no infinitivo
- ✅ Busca por Id com `for`, no mesmo padrão de `Concluir`
- ✅ Não lança exceção se o Id não existir
- ✅ Cabeçalho no estilo `=== ... ===` e `Console.ReadLine()` mantido no final
- ✅ Nenhuma classe, arquivo ou pacote novo; só `Program.cs` foi alterado
- ✅ Rodou `dotnet build` e informou o resultado (regra do CLAUDE.md)

**O que não seguiu:**
- ⚠️ A skill pede no checklist que `dotnet run` mostre a operação funcionando, mas a IA só rodou `dotnet build`. Executei `dotnet run` manualmente e confirmei que a tarefa #2 é removida da listagem.

## O que eu ajustaria
Na skill, deixar explícito no passo final: "rode `dotnet run` e mostre a saída", em vez de deixar só no checklist. Isso mostra que instruções em formato de checklist podem ser tratadas como opcionais pelo modelo; passos numerados são seguidos com mais rigor.

## Observação
O `CLAUDE.md` e a skill foram redigidos com apoio de IA (Claude) e revisados por mim antes do uso.