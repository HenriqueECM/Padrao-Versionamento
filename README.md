# 🧭 Padrões de Versionamento e Contribuição

Este documento define o **guia oficial de versionamento, commits, issues e Pull Requests** do projeto.  
Seguir este padrão garante **organização, rastreabilidade e colaboração eficiente** entre todos os desenvolvedores.

---

## 🧭 Tutorial Completo — Git Flow do Início ao Fim

### 🧩 1. O que é Git Flow

O **Git Flow** é um modelo de ramificação (branching model) criado para organizar o ciclo de vida do desenvolvimento, dividindo o trabalho em **fases claras** e **tipos de branch** específicos:

| Tipo de Branch | Função Principal |
|----------------|-----------------|
| `main` | Contém o código em produção (versões estáveis). |
| `develop` | Contém o código em desenvolvimento (base para novas features). |
| `feature/*` | Usada para desenvolver novas funcionalidades. |
| `release/*` | Usada para preparar uma versão antes do deploy. |
| `hotfix/*` | Usada para corrigir problemas urgentes em produção. |

---

### ⚙️ 2. Inicializando o Git Flow

No terminal, dentro do repositório Git:

```bash
git flow init
```

#### Durante o `init`, o Git Flow pergunta:

| Pergunta | Resposta recomendada |
|-----------|----------------------|
| Branch de produção? | `main` |
| Branch de desenvolvimento? | `develop` |
| Prefixo para feature branches? | `feature/` |
| Prefixo para release branches? | `release/` |
| Prefixo para hotfix branches? | `hotfix/` |
| Prefixo para support branches? | (deixe vazio, pressione Enter) |
| Prefixo de tags de versão? | `v` |

🔹 Isso cria automaticamente uma branch `develop` a partir da `main`.

---

### 🚀 3. Criando uma Feature (nova funcionalidade)

> Exemplo: “Tela de cadastro de cliente”

#### Com Git Flow CLI
```bash
git flow feature start cadastro-cliente
```

> Isso cria e muda automaticamente para a branch `feature/cadastro-cliente`.

Faça suas alterações e commits:
```bash
git add .
git commit -m "feat: implementar tela de cadastro de cliente"
```

Quando terminar a feature:
```bash
git flow feature finish cadastro-cliente
```

> Isso mescla a feature na `develop` e apaga a branch local.

Se quiser enviar ao repositório remoto antes de finalizar:
```bash
git push origin feature/cadastro-cliente
```

---

### 🧪 4. Criando uma Release (preparar versão para produção)

Quando a `develop` estiver estável e pronta para virar uma versão:
```bash
git flow release start 1.0.0
```

Faça ajustes finais, correções e commits:
```bash
git add .
git commit -m "chore: ajustes finais para versão 1.0.0"
```

Finalize a release:
```bash
git flow release finish 1.0.0
```

👉 O que acontece:
- O Git Flow faz **merge da release em `main`** e **em `develop`**.
- Cria uma **tag `v1.0.0`** (ou `1.0.0`, se você deixou o prefixo vazio).

Por fim:
```bash
git push origin main develop --tags
```

---

### 🔥 5. Criando um Hotfix (correção urgente em produção)

Quando há um bug grave **em produção**, não espere a próxima release!

Crie o hotfix:
```bash
git flow hotfix start v1.0.1
```

Corrija o problema e faça o commit:
```bash
git add .
git commit -m "fix: corrigir erro de login em produção"
```

Finalize:
```bash
git flow hotfix finish v1.0.1
```

👉 Isso:
- Faz merge do hotfix na `main` (produção).
- Faz merge também na `develop` (para manter o código igual).
- Cria uma tag `v1.0.1`.

Depois:
```bash
git push origin main develop --tags
```

---

### 🧰 6. Fluxo Resumido com Git Flow CLI

| Etapa | Comando | Resultado |
|--------|----------|-----------|
| Iniciar fluxo | `git flow init` | Configura `main`, `develop`, etc |
| Nova funcionalidade | `git flow feature start nome` | Cria `feature/nome` |
| Finalizar feature | `git flow feature finish nome` | Mescla em `develop` |
| Criar release | `git flow release start 1.0.0` | Cria `release/1.0.0` |
| Finalizar release | `git flow release finish 1.0.0` | Mescla em `main` + tag |
| Criar hotfix | `git flow hotfix start v1.0.1` | Cria `hotfix/v1.0.1` |
| Finalizar hotfix | `git flow hotfix finish v1.0.1` | Mescla em `main` + `develop` + tag |

---

### 🌍 7. Enviando para o repositório remoto

Após finalizar qualquer etapa:
```bash
git push origin main develop --tags
```

Durante o desenvolvimento de uma feature ou release:
```bash
git push origin feature/nome
# ou
git push origin release/1.0.0
```

---

### 🧭 8. Dica de fluxo no GitHub

Mesmo com Git Flow, muitos times usam **Pull Requests (PRs)** para revisão de código.  
Você pode combinar os dois:

1. Criar a feature com:
   ```bash
   git flow feature start nome
   ```
2. Fazer commits, depois:
   ```bash
   git push origin feature/nome
   ```
3. Criar um **Pull Request** da branch `feature/nome` → `develop`.
4. Após aprovação, fazer o `finish` localmente ou via merge no GitHub.

---

### 🧩 9. Exemplo visual simplificado

```
main
 ├── v1.0.0
 ├─── hotfix/v1.0.1
 │     └── v1.0.1
develop
 ├── feature/login
 ├── feature/cadastro
 └── release/1.1.0
       └── v1.1.0
```

---

### 🏁 10. Dica bônus — Convenções de commits

Use [Conventional Commits](https://www.conventionalcommits.org/pt-br/v1.0.0/):

| Tipo | Descrição | Exemplo |
|------|------------|---------|
| `feat` | nova funcionalidade | `feat: adicionar cadastro de usuário` |
| `fix` | correção de bug | `fix: corrigir erro de validação de email` |
| `chore` | manutenção, build, configs | `chore: atualizar dependências` |
| `refactor` | melhoria sem mudar comportamento | `refactor: simplificar método de login` |

---

📘 **Dica:** adicione este arquivo ao repositório como `GIT_FLOW_TUTORIAL.md` ou `docs/gitflow.md` para referência da

### 📚 Documentação

> Fonte: [Alura - Git Flow: o que é, como e quando utilizar](https://www.alura.com.br/artigos/git-flow-o-que-e-como-quando-utilizar?srsltid=AfmBOopzMECBzXZi4B-MMtz8-B8bNHIHBJoJKSa13qdjOf5RextEvvSo)
---

## 🧩 Convenção de Commits

A padronização dos commits facilita:

- Leitura e entendimento do histórico;

- Automação de changelogs;

- Rastreamento rápido de alterações.

### 📜 Estrutura
```bash
<prefixo>: <descrição breve>
```

---

### 🧱 Prefixos mais utilizados
Prefixo	Descrição	Exemplo
| Prefixo    | Descrição                        | Uso                                       | Exemplo                                     |
|------------|---------------------------------|-------------------------------------------|---------------------------------------------|
| `feat:`    | Nova funcionalidade             | Adicionar uma nova feature                 | `feat: implementar cadastro de clientes`   |
| `fix:`     | Correção de bug                | Ajustes que resolvem problemas             | `fix: corrigir cálculo de desconto`         |
| `docs:`    | Alteração em documentação      | Modificar arquivos de documentação         | `docs: atualizar instruções de instalação`  |
| `style:`   | Alteração estética             | Formatação, espaçamento, remoção warnings | `style: padronizar identação do módulo`     |
| `refactor:`| Refatoração do código          | Melhorar código sem alterar funcionalidade | `refactor: separar lógica da camada de UI`  |
| `perf:`    | Melhoria de performance        | Otimizar desempenho                         | `perf: otimizar consulta de filmes`         |
| `test:`    | Adição/alteração de testes    | Criar ou modificar testes                   | `test: adicionar teste unitário`             |
| `chore:`   | Manutenção/Tarefas administrativas | Atualizações que não afetam sistema       | `chore: atualizar dependências`              |
| `build:`   | Alterações no build            | Ajustes em compilação e empacotamento      | `build: configurar webpack para produção`   |
| `ci:`      | Integração contínua            | Mudanças em pipelines CI/CD                  | `ci: adicionar etapa de teste no GitHub`    |
| `revert:`  | Reversão de commit            | Desfazer commits                             | `revert: desfaz alteração que quebrou cadastro` |
| `hotfix:`  | Correção urgente em produção  | Resolver problemas críticos rapidamente     | `hotfix: corrigir falha de autenticação`    |
| `release:` | Preparação/publicação de versão| Versões e lançamentos                        | `release: versão 2.0.0`                      |
| `wip:`     | Trabalho em andamento (Work In Progress) | Alteração não finalizada                      | `wip: implementação inicial da tela de relatórios` |
| `deps:`    | Alteração de dependências     | Adicionar, remover ou atualizar libs        | `deps: atualizar versão do JUnit`           |
| `security:`| Correções/melhorias de segurança | Aumentar segurança do sistema                | `security: corrigir vulnerabilidade SQLi`   |
| `config:`  | Alterações em configurações   | Modificar arquivos de config (`.env`, etc) | `config: atualizar variáveis de ambiente`   |
| `breaking:`| Mudança que quebra compatibilidade | Quebra mudanças que exigem adaptação        | `breaking: remover campo idade do cadastro` |

---

## 🐙 Uso de Issues (GitHub)

As issues são utilizadas para registrar:

- Bugs 🐞

- Melhorias ✨

- Novas funcionalidades 🚀

- Tarefas e ajustes técnicos 🧩

### 🔹 Passo a passo

1. Acesse a aba "Issues" no repositório.

2. Leia ou crie uma issue nova com título e descrição claros.

3. Comente se for assumir a tarefa:
```
“Vou assumir esta issue para resolver o problema.”
```

4. Crie uma branch relacionada à issue:
```bash
git checkout -b feature/nome-da-issue
```

5. Implemente e faça commits referenciando a issue:

```bash
git commit -m "fix: corrigir listagem incorreta de produtos (#5)"
```

6. Suba a branch e abra um Pull Request (PR):

```bash
git push origin feature/nome-da-issue
```

7. No corpo da PR, adicione:
```
Closes #5
```

Isso fecha automaticamente a issue ao fazer o merge.

### 🧾 Exemplo de Issue Bem Escrita

```
**Título:** [Clientes] Erro ao salvar novo cadastro

**Descrição detalhada:**
Ocorre um erro ao tentar salvar novos clientes, exibindo a mensagem "Campo obrigatório ausente".

**Passos para reproduzir:**
1. Acessar o módulo de clientes
2. Clicar em "Novo cliente"
3. Preencher todos os campos
4. Clicar em "Salvar"

**Comportamento esperado:**
O cliente deve ser cadastrado com sucesso.

**Comportamento observado:**
Mensagem de erro é exibida.

**Evidência:**
![print do erro](url-da-imagem)

**Ambiente:**
- Windows 10  
- Java 17  
- MySQL 8.0
```

---

### 🧠 Boas Práticas de Versionamento

✅ Sempre crie uma branch por feature ou bugfix.

✅ Mantenha a main estável — sem commits diretos.

✅ Commits pequenos e descritivos.

✅ Evite mensagens genéricas:

❌ update files → ✅ feat: adicionar validação no cadastro

✅ Sempre vincule commits a issues.

✅ Use Pull Requests para revisão antes do merge.

✅ Adote tags de versão para facilitar rollback e histórico (v1.0.0, v1.1.0, etc.).

✅ Use rebase para manter histórico limpo:

```
git pull --rebase origin develop
```

## 🚀 Exemplo de Pull Request

### Titulo:
```
feat: implementar busca de produtos por nome
```

### Descrição
```
Implementa a funcionalidade de busca por nome no módulo de produtos.
Inclui validações, testes unitários e integração com o banco de dados.

Closes #7 -> número da issue que ira fechar
```

---

## 🏁 Conclusão

Seguindo este guia:

- O histórico do projeto será limpo e compreensível;

- As versões terão rastreabilidade clara;

- As contribuições seguirão um padrão profissional.

💙 Mantenha o fluxo, escreva bons commits e versionar será seu melhor aliado!
