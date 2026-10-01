# Avaliação Individual — Módulo 11 — Tecnologias Emergentes e IA

**Data de entrega:** DD/MM/AAAA
**Formato:** individual, de consulta aberta — use slides, anotações e a própria IA à vontade para pesquisar e testar suas respostas.

## Como participar

1. Faça um **fork** deste repositório.
2. Clone o seu fork localmente.
3. Responda as questões teóricas **direto neste README**, abaixo de cada uma.
4. Complete a parte prática (veja abaixo) editando `CLAUDE.md`, `.claude/skills/minha-skill/SKILL.md` e `EVIDENCIAS.md`.
5. Abra um **Pull Request** do seu fork de volta para este repositório.

> O PR não será mergeado — ele existe só para eu avaliar o seu diff. Pode deixar aberto depois de enviar.

O objetivo não é decorar definições, e sim demonstrar que você entende os conceitos e sabe aplicá-los para ganhar eficiência ao usar IA no seu projeto de TCC. Responda com suas próprias palavras — copiar e colar resposta pronta de IA sem entender não demonstra o aprendizado esperado.

---

## Questões dissertativas

### Questão 1 — O que é um "agent"?
O que é um "agent" (agente de IA)? Explique com suas próprias palavras e dê um exemplo de situação em que faz mais sentido usar um agente do que um chat comum.

Um agent é uma IA que não só responde, mas age: recebe um objetivo, decide os passos, usa ferramentas (ler e editar arquivos, rodar comandos, pesquisar) e avalia o resultado de cada ação antes de seguir, em ciclo, até concluir. Um chat comum só devolve texto e depende de mim para executar e testar. Faz mais sentido usar um agente quando a tarefa exige várias ações no código, por exemplo: "adicione uma função Remover, compile e confirme que não quebrou nada". Foi o que fiz neste projeto com o Claude Code: ele leu o Program.cs, editou e rodou o dotnet build sozinho.


### Questão 2 — O que são guidelines?
O que são "guidelines" (diretrizes) ao usar uma IA generativa? Qual é o papel delas na qualidade das respostas geradas pelo modelo?

Guidelines são as regras e o contexto fixos que eu dou para a IA seguir: padrões de código, tom, o que pode e o que não pode fazer. Elas reduzem a "adivinhação" do modelo, deixando as respostas mais consistentes e alinhadas ao projeto. Sem guidelines, a IA tende a usar o estilo dela (criar classes, trocar estruturas, adicionar pacotes); com elas, segue o padrão já existente e eu preciso corrigir menos.


### Questão 4 — Escolha de modelo e nível de esforço
Qual modelo de IA utilizar para cada tipo de tarefa? Dê um exemplo de tarefa simples e outra mais complexa, explicando como você escolheria o modelo em cada caso. O que é o "nível de esforço" (effort level) e quando faz sentido aumentá-lo ou diminuí-lo?

Para tarefas simples e repetitivas (renomear variáveis, gerar um texto curto, explicar um erro de compilação) uso um modelo menor e mais rápido, como o Haiku ou o Sonnet — é barato e suficiente. Para tarefas complexas (projetar a arquitetura do TCC, depurar um bug que envolve vários arquivos, revisar segurança) uso um modelo mais capaz, como o Opus. O nível de esforço (effort level) define quanto o modelo "pensa" antes de responder. Aumento quando a tarefa exige raciocínio em várias etapas ou quando a primeira resposta veio rasa; diminuo em perguntas diretas, onde mais esforço só gasta tempo e tokens.


### Questão 5 — Como estruturar um bom prompt
Descreva os elementos que tornam um prompt mais eficaz (ex.: contexto, objetivo, formato esperado, exemplos, restrições).

Um bom prompt tem: (1) contexto — qual é o projeto, a tecnologia e a situação; (2) objetivo claro — o que exatamente eu quero; (3) formato esperado — código, lista, tabela, tamanho; (4) exemplos quando o formato é específico; e (5) restrições — o que não fazer. Exemplo: "No meu console app em C# .NET 8 (contexto), crie uma função ListarPendentes (objetivo), seguindo o padrão das funções locais existentes, sem criar classes (restrição), e mostre só o trecho alterado (formato)."


### Questão 6 — Iteração de prompt
O que significa "iterar" um prompt? Por que a primeira resposta de uma IA geralmente não é a versão final, e como você usaria a resposta recebida para melhorar o próximo prompt?

Iterar é refinar o prompt em rodadas, usando a resposta anterior como diagnóstico. A primeira resposta raramente é a final porque a IA preenche com suposições o que eu não especifiquei. Eu leio o resultado, identifico o que ficou diferente do esperado (estilo errado, faltou validação, formato longo demais) e transformo isso em instrução no próximo prompt. Na minha evidência, por exemplo, percebi que a IA não rodou o dotnet run; a melhoria seria colocar esse passo de forma explícita na skill.


### Questão 7 — Zero-shot vs. few-shot
Qual é a diferença entre um prompt "zero-shot" e um prompt "few-shot"? Dê um exemplo de situação em que vale a pena incluir exemplos dentro do próprio prompt.

Zero-shot é pedir a tarefa sem nenhum exemplo; few-shot é incluir alguns exemplos do resultado esperado dentro do próprio prompt. Vale a pena usar few-shot quando o formato é específico e difícil de descrever só com palavras. Exemplo: padronizar mensagens de commit do TCC — mostro 2 ou 3 commits no formato "feat: ...", "docs: ...", "fix: ..." e peço que a IA gere as próximas seguindo o mesmo padrão.


### Questão 8 — Memória e contexto entre sessões
O que significa uma IA "ter memória" entre sessões diferentes de conversa? Por que, em um projeto longo como o TCC, é importante decidir o que precisa ser "lembrado" e como fornecer esse contexto para a IA a cada nova conversa?

Por padrão, cada conversa nova começa do zero: a IA não lembra decisões, nomes ou padrões combinados em sessões anteriores. "Ter memória" significa ter um mecanismo para levar esse contexto adiante — arquivos como o CLAUDE.md, memória da ferramenta ou um resumo que eu colo no início. No TCC, que dura meses, isso é essencial: preciso decidir o que é permanente (stack, arquitetura, convenções, decisões já tomadas) e manter isso num arquivo de contexto. Assim não repito explicações e a IA não sugere algo que contradiz o que já foi decidido.


### Questão 9 — Avaliar a resposta da IA
Antes de aplicar a sugestão de uma IA no seu projeto, como você verifica se ela está correta? Descreva pelo menos 2 formas práticas de checar a confiabilidade de uma resposta gerada por IA.

Não aplico nada sem conferir. Formas práticas: (1) compilar e executar — rodar dotnet build e dotnet run e testar o comportamento, inclusive casos de erro (ex.: remover um Id que não existe); (2) revisar o diff linha a linha antes do commit, para ver exatamente o que mudou e se a IA mexeu em algo fora do pedido; (3) conferir na documentação oficial (Microsoft Learn, docs da biblioteca) quando a IA cita uma API ou configuração, porque ela pode inventar métodos que não existem.


### Questão 10 — Dividir tarefas complexas em etapas
Por que, em tarefas mais complexas, pode ser melhor dividir o trabalho em um fluxo de etapas (ex.: primeiro classificar/organizar, depois processar, depois revisar) em vez de pedir tudo em um único prompt? Dê um exemplo aplicado a uma tarefa do seu TCC.

Em tarefas complexas, um único prompt faz a IA tentar resolver tudo de uma vez e os erros se acumulam sem que eu perceba. Dividindo em etapas, cada parte é menor, mais fácil de conferir e corrigir antes de seguir. Exemplo no projeto final (GlicHelp, app de acompanhamento de glicemia): em vez de pedir "crie o módulo de registros de glicemia", eu faria: 1) pedir para a IA levantar e organizar os campos e regras (valor, data/hora, jejum ou pós-refeição, limites de alerta); 2) gerar o CRUD com base nessa estrutura aprovada; 3) pedir uma revisão focada em validação e casos de erro; 4) testar e só então integrar à interface.


> **Questão 3** (como escrever um bom CLAUDE.md) e a **Questão 11** (prática, evidência de uso real da IA) são respondidas nos próprios arquivos `CLAUDE.md` e `EVIDENCIAS.md` — veja a parte prática abaixo.

---

## Parte prática

1. **Complete o `CLAUDE.md`** na raiz deste repositório — é onde você responde a Questão 3, documentando o projeto para orientar um assistente de IA.
2. **Complete a Skill** em `.claude/skills/minha-skill/SKILL.md`, com instruções reutilizáveis para uma tarefa recorrente do projeto. Renomeie a pasta `minha-skill/` para o nome real da sua skill.
3. **Conecte um assistente de IA ao código local** (Claude Code, GitHub Copilot, Cursor, ou outro de sua escolha) e use-o pelo menos uma vez de verdade, aplicando o `CLAUDE.md` e/ou a Skill que você criou em uma tarefa real do projeto `GerenciadorDeTarefas`.
4. **Complete o `EVIDENCIAS.md`** — é onde você responde a Questão 11, documentando essa experiência (ferramenta usada, prompt exato, o que a IA fez, se seguiu suas instruções).

### O que NÃO fazer

- ❌ Copiar as respostas, o CLAUDE.md ou a Skill de um colega
- ❌ Inventar uma evidência que não aconteceu de verdade
- ❌ Alterar arquivos fora do escopo pedido

## Sobre o projeto de exemplo

Dentro de `GerenciadorDeTarefas/` tem um console app simples em C# — um gerenciador de tarefas fictício — que serve de base para você praticar. Não é necessário adicionar funcionalidades novas ao app; o foco é a configuração e o uso da IA em cima desse código.

Abra `GerenciadorDeTarefas.sln` no Visual Studio, ou rode pelo terminal:

```bash
cd GerenciadorDeTarefas
dotnet run
```

---

## Critérios de avaliação (10 pontos)

| Critério | Pontos |
|---|---|
| Questões dissertativas (conjunto) | 4 |
| `CLAUDE.md` bem estruturado e específico ao projeto (Questão 3) | 2 |
| Skill funcional e realmente reutilizável | 2 |
| `EVIDENCIAS.md` — uso real da IA, seguindo (ou não) o CLAUDE.md/Skill (Questão 11) | 1 |
| Qualidade do Pull Request (descrição clara, organizado, dentro do escopo) | 1 |

## Entrega

Envie o **link do seu Pull Request** pelo Akademos até a data acima.
