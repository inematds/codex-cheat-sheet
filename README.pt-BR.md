<div align="center">

# Codex Cheat Sheet

<a href="https://openai.com/codex/"><img width="763" height="341" alt="Codex cheat sheet" src="assets/image.png" /></a>

> **Seu guia completo para dominar o OpenAI Codex — do zero ao produtivo em minutos.**

Uma referência prática para usar o OpenAI Codex CLI com eficiência. O foco são padrões que ajudam você a pensar criticamente sobre o que delegar e o que fazer você mesmo.

**Baseado na documentação oficial do OpenAI Codex** — todos os comandos e exemplos vêm da [documentação oficial do Codex](https://developers.openai.com/codex). Para informação sempre atualizada, consulte a doc oficial.

🇺🇸 [English version](README.md)

</div>

## 📖 Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/codex-cheat-sheet/guia/**

## Início rápido

```bash
# Instalar com o instalador oficial (recomendado)
curl -fsSL https://chatgpt.com/codex/install.sh | sh

# Ou com npm
npm install -g @openai/codex

# Ou com Homebrew
brew install --cask codex

# Ou com pnpm (gerenciador oficial do monorepo)
pnpm install -g @openai/codex

# Windows: script oficial de instalação
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"

# Auto-atualização (instalações feitas pelo instalador)
codex update

# Abrir o Codex
codex

# Ver a versão
codex --version
```

## Índice

- **[Nível 1: Primeiros passos](#nível-1-primeiros-passos)**
- **[Nível 2: Comandos básicos](#nível-2-comandos-básicos)**
- **[Nível 3: Uso intermediário](#nível-3-uso-intermediário)**
- **[Nível 4: Recursos avançados](#nível-4-recursos-avançados)**
- **[Skills](#skills)** — capacidades nativas e reutilizáveis
- **[Nível 5: Workflows de especialista](#nível-5-workflows-de-especialista)**

## Nível 1: Primeiros passos

Comandos essenciais para começar com o Codex.

<details>
<summary><strong>Instalação</strong></summary>

```bash
# Instalar globalmente com npm
npm install -g @openai/codex

# Instalar com Homebrew (macOS)
brew install --cask codex

# Instalar com pnpm (gerenciador oficial do monorepo)
pnpm install -g @openai/codex

# Instalador oficial standalone (macOS/Linux)
curl -fsSL https://chatgpt.com/codex/install.sh | sh

# Windows: script oficial de instalação
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"

# Atualizar com npm
npm install -g @openai/codex

# Atualizar com Homebrew
brew upgrade --cask codex

# Auto-atualização (quando a release instalada suportar)
codex update

# Baixar o binário das releases do GitHub
# Acesse: https://github.com/openai/codex/releases/latest
```

</details>

<details>
<summary><strong>Primeiros comandos</strong></summary>

```bash
# Iniciar o modo interativo
codex

# Rodar com um prompt específico
codex "explain this project"

# Execução não interativa
codex exec "explain utils.ts"
```

</details>

<details>
<summary><strong>Autenticação</strong></summary>

```bash
# Entrar com a conta ChatGPT (recomendado)
codex
# Depois escolha "Sign in with ChatGPT"

# Usar chave de API (alternativa — cobrança por uso)
printenv OPENAI_API_KEY | codex login --with-api-key
# Ou a partir de um arquivo:
codex login --with-api-key < my_key.txt

# Usar um access token
printenv CODEX_ACCESS_TOKEN | codex login --with-access-token

# Autenticação por dispositivo
codex login --device-auth

# Conferir o status do login (saída 0 = credenciais presentes)
codex login status
```

</details>

<details>
<summary><strong>Navegação básica</strong></summary>

```bash
# Atalhos de teclado
Ctrl+C                    # Cancela a operação atual (ou use /exit para fechar a sessão)
Tab                       # Enfileira o próximo prompt, slash command ou comando de shell enquanto o Codex trabalha
↑/↓                       # Recupera o histórico de rascunhos
Esc Esc                   # Edita a mensagem anterior (composer vazio; bifurca a conversa daquele ponto)
Ctrl+R                    # Busca no histórico de prompts
Ctrl+O                    # Copia a última saída concluída
Enter                     # Injeta novas instruções no turno atual
!comando                  # Roda um comando local de shell sob a política de aprovação/sandbox atual

# Entrada especial
@                         # Dispara a busca de arquivos (fuzzy find)
```

</details>

## Nível 2: Comandos básicos

Comandos centrais para o dia a dia.

<details>
<summary><strong>Slash commands — essenciais</strong></summary>

```bash
/model                    # Escolhe o modelo e o esforço de raciocínio
/permissions              # Configura o que o Codex pode fazer sem aprovação
/fast                     # Liga/desliga o modo Fast nos modelos suportados
/personality              # Escolhe um estilo de comunicação
/review                   # Revisa as mudanças atuais e aponta problemas
/new                      # Começa um novo chat durante a conversa
/init                     # Cria um arquivo AGENTS.md com instruções
/compact                  # Resume a conversa para não estourar o contexto
/diff                     # Mostra o git diff (inclusive arquivos não rastreados)
/mention                  # Menciona um arquivo
/status                   # Mostra a config da sessão e o uso de tokens
/mcp                      # Lista as ferramentas MCP configuradas
/side                     # Abre uma conversa lateral efêmera (/btw)
/fork                     # Bifurca a conversa atual em uma nova thread
/ps                       # Mostra os terminais em segundo plano e suas saídas
/stop                     # Para todos os terminais em segundo plano
/logout                   # Sai da conta do Codex
/quit                     # Fecha o Codex
/exit                     # Fecha o Codex
/feedback                 # Envia logs para os mantenedores
/goal                     # Define ou mostra um objetivo persistente da tarefa
/plan                     # Entra no modo de plano, para planejamento multi-etapas
/approve                  # Aprova uma nova tentativa após negativa da revisão automática
/copy                     # Copia a última saída concluída (ou Ctrl+O)
/clear                    # Limpa o terminal e começa um novo chat
/rename                   # Renomeia o chat atual
/archive                  # Arquiva a sessão atual e fecha o Codex
/delete                   # Apaga a sessão atual em definitivo e fecha
/resume                   # Retoma um chat salvo da sua lista de sessões
/app                      # Continua a sessão no app desktop do ChatGPT
/agent                    # Troca a thread de agente ativa (também /subagents)
/apps                     # Navega pelos apps (conectores) e insere no prompt
/plugins                  # Navega pelos plugins instalados e disponíveis
/hooks                    # Vê e gerencia os hooks de ciclo de vida
/memories                 # Configura o uso e a geração de memória
/import                   # Importa a configuração do Claude Code ou do Cursor
/experimental             # Liga/desliga recursos experimentais
/usage                    # Mostra o uso de tokens da conta
/debug-config             # Imprime o diagnóstico das camadas de config
/statusline               # Configura os itens do rodapé da TUI
/title                    # Configura os itens do título do terminal
/theme                    # Escolhe um tema de sintaxe
/pets                     # Escolhe ou esconde um bichinho de terminal (/pet)
/keymap                   # Remapeia os atalhos de teclado da TUI
/vim                      # Liga/desliga o modo Vim no composer
/ide                      # Inclui os arquivos abertos e o contexto da IDE
/raw                      # Liga/desliga o modo de scrollback bruto
/skills                   # Navega e usa as skills

# /debug não é mais documentado; use /debug-config para diagnóstico de config
```

</details>

<details>
<summary><strong>Operações com arquivos e diretórios</strong></summary>

```bash
# O Codex lê, escreve e edita arquivos
"Leia o conteúdo de src/app.js"
"Crie um arquivo novo chamado utils.js"
"Edite a função em main.py para adicionar tratamento de erro"

# Ver a estrutura do projeto
"Explique a estrutura deste projeto"
"Que arquivos existem no diretório src?"
```

</details>

<details>
<summary><strong>Trabalhando com código</strong></summary>

```bash
# Análise de código
"Explique o que este código faz"
"Revise esta função procurando bugs"
"Sugira melhorias para este arquivo"

# Geração de código
"Escreva uma função para fazer parse de JSON"
"Crie testes unitários para este módulo"
"Adicione tratamento de erro a este código"
```

</details>

<details>
<summary><strong>Gerenciamento de sessões</strong></summary>

```bash
# Retomar sessões
codex resume                          # Abre o seletor de sessões
codex resume --last                   # Retoma a sessão mais recente
codex resume <SESSION_ID>             # Retoma uma sessão específica pelo ID

# Retomada de sessão não interativa
codex exec resume <SESSION_ID>        # Retoma uma sessão não interativa
codex exec resume --last              # Retoma a última sessão não interativa
```

</details>

<details>
<summary><strong>Referência de subcomandos (0.147.0)</strong></summary>

| Comando | Para que serve |
|---|---|
| `codex exec` | Roda de forma não interativa (apelido: `e`) |
| `codex review` | Revisão de código não interativa (veja a [seção abaixo](#nível-4-recursos-avançados)) |
| `codex login` / `codex logout` | Gerencia a autenticação; `codex login status` confere as credenciais |
| `codex resume` | Retoma uma sessão salva (seletor; `--last` para a mais recente) |
| `codex fork` | Bifurca uma sessão em um novo chat |
| `codex archive` / `codex unarchive` | Arquiva / restaura sessões salvas |
| `codex delete` | Apaga uma sessão em definitivo |
| `codex apply` | Aplica um diff de chat do Codex Cloud na árvore local (apelido: `a`) |
| `codex cloud` | Navega ou executa tarefas do Codex Cloud (experimental) |
| `codex plugin` | Instala, lista e remove plugins; `codex plugin marketplace` gerencia as fontes |
| `codex mcp` | Gerencia servidores MCP (listar, adicionar, remover, autenticar) |
| `codex mcp-server` | Descontinuado; use o app server |
| `codex doctor` | Diagnostica instalação, config, auth e saúde de execução |
| `codex features` | Inspeciona feature flags (listar / ligar / desligar) |
| `codex sandbox` | Roda comandos dentro de um sandbox fornecido pelo Codex |
| `codex update` | Auto-atualiza para a versão mais recente |
| `codex completion` | Gera completions de shell (bash, zsh, fish, powershell) |
| `codex app-server` | Roda o app server (experimental) |
| `codex exec-server` | Roda o serviço exec-server standalone (experimental) |
| `codex remote-control` | Gerencia o daemon do app server por controle remoto (experimental) |
| `codex debug` | Ferramentas de depuração (subcomandos experimentais) |

</details>

<details>
<summary><strong>Flags úteis da CLI</strong></summary>

```bash
# Escolha de modelo
codex --model gpt-5 "seu prompt"
codex -m gpt-5.6-terra "tarefa complexa"

# Diretório de trabalho
codex --cd /caminho/do/projeto        # Muda o diretório de trabalho
codex -C ../outro-projeto             # Forma curta

# Vários diretórios
codex --add-dir ../backend --add-dir ../shared "analise tudo"

# Aprovações
codex --ask-for-approval untrusted    # Pergunta em comandos não confiáveis
codex -a on-request                   # O modelo decide quando perguntar (interativo)
codex exec -a never "tarefa"          # Nunca pergunta (execuções não interativas)

# Sandbox
codex --sandbox read-only             # Sandbox somente leitura (padrão)
codex --sandbox workspace-write       # Permite escrita no workspace
codex --sandbox danger-full-access    # Desliga o sandbox (perigoso!)

# Entrada de imagem
codex -i screenshot.png "explique este erro"
codex --image img1.png,img2.jpg "resuma estes diagramas"

# Busca na web ao vivo
codex --search "qual é a versão mais recente de X"

# Automação de aprovações
codex --approve-for-me "refatore isto"                     # Aprovações por revisão automática
codex --dangerously-bypass-approvals-and-sandbox "tarefa"  # Sem aprovação e sem sandbox (apelido: --yolo)
codex --yolo "tarefa"                                      # Apelido curto do anterior

# Config estrita
codex --strict-config                                      # Erra em campos desconhecidos do config.toml

# Provedores open-source locais
codex --oss                                                # Usa provedor open-source local
codex --oss --local-provider ollama                        # Escolhe o provedor (lmstudio | ollama)

# Perfis de configuração
codex -p work "seu prompt"                                 # Sobrepõe ~/.codex/work.config.toml

# App server remoto
codex --remote ws://host:porta                             # Conecta a TUI a um app server remoto
codex --remote wss://host:porta --remote-auth-token-env TOKEN_ENV  # Bearer token vindo de variável de ambiente

# Completions de shell
codex completion bash                 # Gera completions do bash
codex completion zsh                  # Gera completions do zsh
codex completion fish                 # Gera completions do fish
```

</details>

## Nível 3: Uso intermediário

Configuração e personalização.

<details>
<summary><strong>Configuração</strong></summary>

```bash
# Local do arquivo de config: ~/.codex/config.toml
# Sobrescritas por projeto: .codex/config.toml (carregado só em projetos confiáveis;
# chaves de provider/auth/notificação/telemetria são ignoradas nos arquivos por projeto)

# Edite a config à mão ou use flags da CLI
codex --model gpt-5.6-terra "seu prompt"
codex --config model="gpt-5.6-terra"

# Configurações comuns no config.toml:
# - escolha de modelo
# - approval_policy
# - sandbox_mode
# - mcp_servers
# - profiles
```

</details>

<details>
<summary><strong>Escolha de modelo</strong></summary>

```bash
# Defina o modelo no config.toml
model = "gpt-6-astra"               # Novo carro-chefe: trabalho ponta a ponta mais difícil em código, apps e pesquisa (em liberação gradual)
model = "gpt-5.6-sol"              # Carro-chefe: código complexo, uso de computador, pesquisa (recomendado, setembro de 2026)
model = "gpt-5.6-terra"            # Equilibrado: código e trabalho de conhecimento do dia a dia
model = "gpt-5.6-luna"             # Rápido: tarefas leves, menor custo

# Para modelos de raciocínio (gpt-6-astra, gpt-5.6-sol, gpt-5.6-terra):
model_reasoning_effort = "medium"  # minimal, low, medium, high, xhigh
model_reasoning_summary = "auto"   # auto, concise, detailed, none

# Para a família GPT-5:
model_verbosity = "medium"         # low, medium, high

# Modelos disponíveis (em setembro de 2026):
# - gpt-6-astra - novo carro-chefe para trabalho complexo em código, apps e pesquisa (em liberação)
# - gpt-5.6-sol (recomendado) - carro-chefe para código complexo, uso de computador, pesquisa e segurança
# - gpt-5.6-terra - equilibra capacidade e custo no código e no trabalho do dia a dia
# - gpt-5.6-luna - opção mais rápida e barata para tarefas leves
# - gpt-5.3-codex-spark - preview de pesquisa, só texto, para iteração quase instantânea (ChatGPT Pro)
# - gpt-5.5 - carro-chefe da geração anterior
# - gpt-5.4 / gpt-5.4-mini - aposentados do Codex com login ChatGPT em 31/08/2026
# - gpt-5.2 / gpt-5.3-codex - descontinuados no Codex com login ChatGPT
# - Outros modelos da OpenAI via provedores customizados
```

### Novidades de modelo (setembro de 2026)

**GPT-6 Astra** é o novo carro-chefe, chegando aos poucos a todos os clientes:
- Feito para o trabalho ponta a ponta mais difícil em código, apps e pesquisa
- Combina raciocínio avançado, uso de computador e melhor julgamento
- Use quando a tarefa exigir raciocínio sustentado por várias etapas e ferramentas

**GPT-5.6 Sol** continua sendo o carro-chefe da linha 5.6:
- Feito para código complexo, uso de computador, pesquisa e trabalho de segurança
- Segue instruções melhor e tem mais precisão técnica

**GPT-5.6 Terra** equilibra capacidade e custo:
- Otimizado para código e trabalho de conhecimento do dia a dia
- Raciocínio forte com uso eficiente de tokens

**GPT-5.6 Luna** é o mais rápido e barato:
- Ideal para tarefas leves e iterações rápidas
- Mantém a qualidade minimizando a latência

**Aposentadorias:** gpt-5.4 e gpt-5.4-mini saíram do Codex com login ChatGPT em 31 de agosto de 2026 (troque por gpt-5.6-terra e gpt-5.6-luna); gpt-5.2 e gpt-5.3-codex estão descontinuados. A API da OpenAI e o login por chave de API não são afetados.

Veja a [página oficial de modelos](https://developers.openai.com/codex/models) para detalhes.

</details>

<details>
<summary><strong>Prompts customizados</strong></summary>

```bash
# Crie prompts customizados em ~/.codex/prompts/

# Exemplo: crie ~/.codex/prompts/review.md
# Depois use assim:
"Use o prompt review neste código"
```

</details>

<details>
<summary><strong>Memória com AGENTS.md</strong></summary>

```bash
# Crie um AGENTS.md na raiz do projeto
# O Codex passa a lembrar o contexto específico do projeto

# Exemplo de conteúdo do AGENTS.md:
"""
Este projeto usa:
- Node.js com Express
- Banco PostgreSQL
- Jest para testes

Padrões de código:
- Usar TypeScript
- Seguir as regras do ESLint
- Escrever testes para toda funcionalidade nova
"""
```

</details>

## Nível 4: Recursos avançados

Recursos poderosos para workflows avançados.

<details>
<summary><strong>Model Context Protocol (MCP)</strong></summary>

```bash
# Configure servidores MCP em ~/.codex/config.toml

# Exemplo de servidor STDIO
[mcp_servers.filesystem]
command = "npx"
args = ["-y", "@modelcontextprotocol/server-filesystem", "/caminho/permitido"]
env = { API_KEY = "valor" }

# Exemplo de servidor HTTP streamable
[mcp_servers.figma]
url = "https://mcp.figma.com/mcp"
bearer_token_env_var = "FIGMA_TOKEN"

# Comandos MCP da CLI
codex mcp list                        # Lista os servidores configurados
codex mcp add <nome> -- <comando>     # Adiciona um servidor stdio
codex mcp add <nome> --url <URL>      # Adiciona um servidor HTTP streamable
codex mcp get <nome>                  # Mostra os detalhes do servidor
codex mcp remove <nome>               # Remove um servidor
codex mcp login <nome>                # Login OAuth (HTTP streamable)
codex mcp logout <nome>               # Logout OAuth

# Faz a inicialização falhar se um servidor não subir:
[mcp_servers.figma]
url = "https://mcp.figma.com/mcp"
required = true

# Plugins são a superfície estável para integrações empacotadas
codex plugin list                     # Lista plugins dos marketplaces configurados
codex plugin add <plugin>             # Instala um plugin (ou PLUGIN@MARKETPLACE)
codex plugin marketplace list         # Gerencia os marketplaces de plugins

# Nota: codex mcp-server está descontinuado; use o app server

# Servidores MCP populares:
# - Context7 (documentação para desenvolvedores)
# - Figma (acesso a design)
# - Playwright (controle de navegador)
# - GitHub (acesso à API do GitHub)
# - Sentry (acesso a logs)
```

Veja a [documentação de MCP](https://developers.openai.com/codex/configuration) para detalhes.

</details>

<details>
<summary><strong>Sandbox e permissões</strong></summary>

```bash
# Configure o modo de sandbox no config.toml
sandbox_mode = "read-only"              # Padrão: somente leitura
sandbox_mode = "workspace-write"        # Permite escrita no workspace
sandbox_mode = "danger-full-access"     # Desliga o sandbox (perigoso!)

# Configure a política de aprovação (válidos: untrusted | on-request | never; "on-failure" foi descontinuado)
approval_policy = "untrusted"           # Pergunta em comandos não confiáveis
approval_policy = "on-request"          # O modelo decide quando perguntar (interativo)
approval_policy = "never"               # Nunca pergunta (execuções não interativas)

# Opções do workspace-write
[sandbox_workspace_write]
writable_roots = ["/caminho/extra"]
network_access = false
exclude_tmpdir_env_var = false
exclude_slash_tmp = false
```

Veja [Sandbox e aprovações](https://developers.openai.com/codex/sandboxing) para detalhes.

</details>

<details>
<summary><strong>Modo não interativo</strong></summary>

```bash
# Executa e sai, com codex exec
codex exec "resuma todos os comentários TODO deste projeto"

# Aprovações por revisão automática (sandbox workspace-write)
codex exec --approve-for-me "refatore este código"

# Totalmente desassistido (perigoso — pula todas as aprovações e o sandbox)
codex exec --dangerously-bypass-approvals-and-sandbox "refatore este código"

# Acesso total (perigoso!)
codex exec --sandbox danger-full-access "sua tarefa"

# Saída em JSON para automação
codex exec --json "analise este projeto"

# Saída estruturada com JSON schema
codex exec --output-schema schema.json "extraia os detalhes do projeto"

# Salvar a saída em arquivo (grava só a última mensagem do agente, não a execução inteira)
codex exec -o output.txt "gere a documentação"

# Combine com --json em CI: eventos JSONL no stdout + resumo final no arquivo
codex exec --json -o output.txt "gere a documentação"
```

Veja [Modo não interativo (exec)](https://developers.openai.com/codex/non-interactive-mode) para detalhes.

</details>

<details>
<summary><strong>Revisão de código não interativa</strong></summary>

Roda uma revisão dedicada sem abrir a TUI. Relata achados priorizados sem modificar a árvore de trabalho.

```bash
codex review --uncommitted                    # Revisa mudanças staged, unstaged e não rastreadas
codex review --base main                      # Revisa as mudanças contra uma branch base
codex review --commit <SHA>                   # Revisa as mudanças introduzidas por um commit
codex review --uncommitted --title "wip: auth"  # Título opcional no resumo da revisão
codex review "foque em problemas de segurança"  # Instruções customizadas de revisão
```

Veja [Code Review](https://developers.openai.com/codex/code-review) para detalhes.

</details>

<details>
<summary><strong>Pipes e scripts</strong></summary>

```bash
# Mande conteúdo para o Codex por pipe
cat logs.txt | codex exec "encontre o erro"

# Use em scripts
git diff | codex exec "crie uma mensagem de commit no padrão conventional"

# Combine comandos
codex exec "explique este arquivo" < app.js > explicacao.md
```

</details>

<details>
<summary><strong>Skills</strong></summary>

<a id="skills"></a>

- **O que são:** capacidades nativas, reutilizáveis e em disco, que o Codex descobre sozinho. Cada skill é um pacote com `name`, `description` e um corpo opcional mantido em disco. Já estão disponíveis para todos — não precisa de feature flag.
- **Onde ficam:** `~/.codex/skills/**/SKILL.md` (recursivo). Só valem arquivos chamados exatamente `SKILL.md`; entradas ocultas e symlinks são ignoradas.
- **Formato do arquivo (frontmatter YAML + corpo):**
  ```markdown
  ---
  name: nome-da-sua-skill        # obrigatório, ≤ 100 caracteres, uma linha
  description: quando/por que usar  # obrigatório, ≤ 500 caracteres, uma linha
  ---

  # Corpo opcional (fica em disco)
  Coloque aqui referências, fluxos de trabalho ou exemplos.
  ```
- **Como usar:** mencione com `$<nome-da-skill>` no chat, ou navegue/insira pelo `/skills` na TUI. O Codex injeta apenas `name`, `description` e o caminho absoluto do arquivo.
- **Validação:** frontmatter inválido gera um aviso dispensável na inicialização e entradas de log; skills inválidas são ignoradas até serem corrigidas.
- **Skills de exemplo neste repositório:** copie ou crie um symlink de qualquer uma delas em `~/.codex/skills/<nome>/SKILL.md` e reinicie o Codex:
  - `skills/pdf-processing/SKILL.md`
  - `skills/log-review/SKILL.md`
  - `skills/form-filling/SKILL.md`
  - `skills/project-management/SKILL.md`

</details>

## Novidades 2025–2026

Adições recentes ao Codex que vale conhecer:

<details>
<summary><strong>Objetivos de tarefa (/goal)</strong></summary>

O comando `/goal` define um objetivo persistente para uma tarefa longa. Ele repete planejar → agir → testar → revisar até bater a sua condição de parada.

**Uso:**

```bash
/goal Termine a migração mantendo os testes verdes   # Define o objetivo
/goal                                                 # Mostra o objetivo atual
/goal pause                                           # Pausa a execução
/goal resume                                          # Retoma uma execução pausada
/goal clear                                           # Limpa o objetivo atual
```

**Quando usar:** trabalho de várias horas, validável, com uma definição clara de "pronto".
**Quando não usar:** quando você ainda está explorando ou tomando decisões de julgamento.

> **Nota:** defina uma condição de parada mensurável. Use `/goal pause` ou `/goal clear` se ele começar a derivar. Rode em uma branch descartável.

Veja a [documentação de follow-a-goal](https://developers.openai.com/codex/developer-commands#set-or-view-a-task-goal-with-goal).

</details>

<details>
<summary><strong>Skill babysit-pr</strong></summary>

A skill `babysit-pr` automatiza a manutenção de PRs:
- Corrige falhas de CI sozinha
- Trata comentários de revisão
- Fica de olho em conflitos de merge
- Mantém seus PRs andando no pipeline

```bash
# Use com a integração MCP do GitHub
codex "babysit this PR with $github"
```

</details>

<details>
<summary><strong>REPL de JavaScript (js_repl)</strong></summary>

REPL de JavaScript persistente para execução incremental de código:
- Testa trechos de código em tempo real
- Itera a lógica sem re-executar tudo
- Depura expressões complexas

```bash
# Ative no config.toml
[mcp_servers.js_repl]
command = "node"
args = ["-e", "process.stdin.on('data', d => eval(d.toString()))"]
```

</details>

<details>
<summary><strong>App server em processo</strong></summary>

Nova arquitetura para o modo `exec` não interativo:
- Inicialização mais rápida
- Melhor para integração com CI/CD
- Menos sobrecarga em scripts de automação

</details>

## Gestão de projetos com o Codex

O Codex não serve só para código — é um bom assistente de gestão de projetos. Como usá-lo para tocar projetos, sprints e tarefas:

<details>
<summary><strong>Planejamento e quebra de escopo</strong></summary>

```bash
# Quebrar um pedido grande de feature
codex "Quebre este pedido de feature em tarefas acionáveis:
- Sistema de autenticação de usuário
- Precisa suportar OAuth e e-mail
- Incluir fluxo de recuperação de senha
- Adicionar opção de 2FA"

# Gerar backlog de sprint
codex exec "Analise este projeto e crie um backlog de sprint:
- Priorize por complexidade
- Estime o esforço em horas
- Identifique dependências"

# Criar histórias de usuário
codex "Converta estes requisitos em histórias de usuário com critérios de aceite"
```

</details>

<details>
<summary><strong>Integração com o GitHub</strong></summary>

```bash
# Gerar descrições de PR automaticamente
git diff | codex exec "Crie uma descrição detalhada de PR com:
- Resumo das mudanças
- Testes realizados
- Breaking changes (se houver)"

# Criar issues a partir de comentários TODO
codex exec "Varra o projeto atrás de TODO/FIXME e crie issues no GitHub"

# Gerar notas de release
codex exec "Crie notas de release a partir dos commits recentes"
```

</details>

<details>
<summary><strong>Acompanhamento e status</strong></summary>

```bash
# Gerar relatório de status
codex "Revise os commits recentes e gere um relatório de status para os stakeholders"

# Acompanhar progresso
codex "Que porcentagem das tarefas do sprint está concluída, com base nos PRs mergeados?"

# Identificar riscos
codex "Analise este projeto e identifique possíveis bloqueios ou riscos"
```

</details>

<details>
<summary><strong>Padrões de colaboração em time</strong></summary>

```bash
# Automação de revisão de código
codex "Revise este PR quanto a:
- Vulnerabilidades de segurança
- Problemas de performance
- Padrões de qualidade de código
- Lacunas de cobertura de testes"

# Sincronizar documentação
codex "Atualize o README com base nas features adicionadas recentemente"

# Ajuda no onboarding
codex "Crie um guia de onboarding de desenvolvedor para este projeto"
```

</details>

<details>
<summary><strong>Criando skills de gestão de projeto</strong></summary>

Você pode criar skills sob medida para o fluxo do seu time:

```markdown
# ~/.codex/skills/team-sprint/SKILL.md
---
name: team-sprint
description: Gerencia o planejamento e o acompanhamento de sprint do nosso time
---

# Fluxo do sprint
1. Use `/standup` para gerar resumos de daily
2. Use `/retro` para coletar feedback de retrospectiva
3. Use `/velocity` para calcular a velocidade do time

# Templates
- Template de planejamento de sprint em docs/sprint-template.md
- Formato de retrospectiva: Começar/Parar/Continuar
```

</details>

## Nível 5: Workflows de especialista

Padrões avançados e automação.

<details>
<summary><strong>Integração com GitHub Actions</strong></summary>

```yaml
# Use a codex-action no CI/CD
name: Code Review
on: [pull_request]
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: openai/codex-action@v1
        with:
          task: "Review this PR for security issues"
```

Veja a [GitHub Action](https://github.com/openai/codex-action) para detalhes.

</details>

<details>
<summary><strong>Revisão de código automatizada</strong></summary>

```bash
# Revisar o PR inteiro
codex "Revise este PR quanto a segurança, performance e manutenibilidade"

# Gerar mensagens de commit no padrão conventional
git diff HEAD~1 | codex exec "Crie uma mensagem de commit no padrão conventional"

# Corrigir problemas comuns automaticamente
codex "Corrija todos os erros de ESLint deste projeto"
```

</details>

<details>
<summary><strong>Apoio ao pipeline de CI/CD</strong></summary>

```bash
# Gerar config de CI
codex "Crie um workflow do GitHub Actions para:
- Projeto TypeScript
- Rodar testes no PR
- Fazer deploy na Vercel na main"

# Depurar falhas de CI
cat .github/workflows/build.log | codex exec "Encontre a causa raiz"
```

</details>

<details>
<summary><strong>Migração de código legado</strong></summary>

```bash
# Converter entre linguagens
codex "Converta este utilitário Python para TypeScript"

# Atualizar APIs descontinuadas
codex "Converta todos os componentes de classe React em componentes funcionais com hooks"

# Adicionar segurança de tipos
codex "Adicione tipos TypeScript a este projeto JavaScript"
```

</details>

<details>
<summary><strong>Otimização de performance</strong></summary>

```bash
# Analisar gargalos
codex "Faça o profiling deste código e identifique gargalos de performance"

# Otimizar consultas ao banco
codex "Refatore estas consultas N+1 para usar carregamento em lote"

# Otimizar o bundle
codex "Sugira otimizações de webpack para reduzir o tamanho do bundle"
```

</details>

<details>
<summary><strong>Auditoria de segurança</strong></summary>

```bash
# Encontrar vulnerabilidades
codex "Audite este código em busca de vulnerabilidades de segurança"

# Checar dependências
codex "Revise o package.json procurando dependências desatualizadas ou vulneráveis"

# Checar conformidade
codex "Verifique se este código segue as diretrizes de segurança da OWASP"
```

</details>

<details>
<summary><strong>Diagnóstico e depuração</strong></summary>

```bash
# Analisar logs de erro
cat error.log | codex exec "encontre a causa raiz"

# Depurar uma função específica
codex "Descubra por que a função de login está falhando"

# Reproduzir e corrigir
codex "Crie um caso de teste que reproduza este bug e depois corrija"
```

</details>

<details>
<summary><strong>Documentação</strong></summary>

```bash
# Gerar README
codex exec "Crie um README completo para este projeto"

# Documentação de API
codex exec "Gere a documentação de API a partir dos comentários JSDoc"

# Comentários de código
codex "Adicione comentários detalhados a esta função complexa"
```

</details>

<details>
<summary><strong>Testes</strong></summary>

```bash
# Gerar testes
codex "Crie testes unitários para todas as funções de utils.js"

# Cobertura de testes
codex "Analise a cobertura de testes e sugira os testes que faltam"

# Testes E2E
codex "Crie testes E2E com Playwright para o fluxo do usuário"
```

</details>

<details>
<summary><strong>Refatoração</strong></summary>

```bash
codex "Refatore este código para:
1. Melhorar a legibilidade
2. Adicionar tratamento de erro
3. Seguir as boas práticas de TypeScript
4. Adicionar definições de tipo"
```

</details>

## Recursos adicionais

**Documentação oficial do OpenAI Codex:**
- [Repositório oficial](https://github.com/openai/codex) — repositório principal e central de documentação
- [Guia de início](https://developers.openai.com/codex/quickstart) — guia completo para começar
- [Referência de configuração](https://developers.openai.com/codex/configuration) — referência completa do config.toml
- [Comandos de desenvolvedor](https://developers.openai.com/codex/developer-commands) — comandos, flags e slash commands
- [Modo não interativo (exec)](https://developers.openai.com/codex/non-interactive-mode) — automação com codex exec
- [Autenticação](https://developers.openai.com/codex/auth) — métodos de autenticação
- [Sandbox e aprovações](https://developers.openai.com/codex/sandboxing) — segurança e sandbox
- [Documentação do AGENTS.md](https://developers.openai.com/codex/agent-configuration/agents-md) — instruções por projeto
- [Integração MCP](https://developers.openai.com/codex/configuration) — configuração e uso de MCP
- [Prompts customizados](https://developers.openai.com/codex/prompting) — como criar prompts próprios
- [FAQ](https://developers.openai.com/codex/reference/troubleshooting) — perguntas frequentes
- [Skills](https://developers.openai.com/codex/skills-and-plugins) — guia oficial

**Extensões e integrações:**
- [GitHub Action](https://github.com/openai/codex-action) — integração com CI/CD
- [SDK TypeScript](https://developers.openai.com/codex/codex-sdk) — uso programático
- [Extensão do VS Code](https://developers.openai.com/codex/ide) — integração com a IDE

**Model Context Protocol:**
- [Especificação do MCP](https://modelcontextprotocol.io/) — documentação oficial do protocolo
- [Exemplos de servidores MCP](https://github.com/modelcontextprotocol/servers) — servidores da comunidade

> **Dica:** confira sempre a [documentação oficial do Codex](https://github.com/openai/codex) para os recursos e atualizações mais recentes. Esta folha de consulta é uma referência rápida; a doc oficial é a fonte mais completa e atual.

## Contribuindo

Achou um problema ou tem uma sugestão? Contribuições são bem-vindas!

- Reporte bugs ou problemas
- Sugira novos exemplos
- Melhore a documentação
- Compartilhe seus workflows

## Licença

Licença MIT — livre para usar e modificar.
