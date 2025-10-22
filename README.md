# 🧭 Padrões de Versionamento e Contribuição

Este documento define o **guia oficial de versionamento, commits, issues e Pull Requests** do projeto.  
Seguir este padrão garante **organização, rastreabilidade e colaboração eficiente** entre todos os desenvolvedores.

---

## 📦 Estrutura de Branches (Git Flow)

O projeto utiliza o **modelo Git Flow** para organizar o ciclo de vida do código.

### 🌱 Branches principais

| Branch | Função | Observação |
|--------|--------|-------------|
| `main` | Código estável e pronto para produção | Recebe merges das releases e hotfixes |
| `develop` | Código em desenvolvimento | Integra as features antes de ir para produção |

### 🌿 Branches secundárias

| Tipo | Origem | Objetivo | Exemplo |
|------|---------|-----------|----------|
| `feature` | `develop` | Nova funcionalidade | `feature/cadastro-cliente` |
| `release` | `develop` | Preparar versão para produção | `release/1.0.0` |
| `hotfix` | `main` | Correção urgente em produção | `hotfix/corrigir-login` |

---

## 🔄 Fluxo Git Flow na Prática

### Imagem na prática

<img width="905" height="380" alt="image" src="https://github.com/user-attachments/assets/a36c4d8c-ff7b-454b-ab95-626e48b6a3bd" />

---

### 💡 Exemplo de fluxo completo

```bash
# 1. Criar branch de feature
git checkout develop
git checkout -b feature/cadastro-cliente

# 2. Fazer commits
git add .
git commit -m "feat: implementar tela de cadastro de clientes"

# 3. Subir branch para o repositório remoto
git push origin feature/cadastro-cliente

# 4. Abrir Pull Request no GitHub
# Título: feat: implementar cadastro de cliente
# Descrição: Closes #12

# 5. Após aprovação
git checkout develop
git merge feature/cadastro-cliente
git push origin develop

# 6. Criar release quando estiver pronto para deploy
git checkout -b release/1.0.0
git push origin release/1.0.0

# 7. Testar, corrigir e publicar versão estável
git checkout main
git merge release/1.0.0
git tag -a v1.0.0 -m "Versão estável 1.0.0"
git push origin main --tags
```

---

### 📚 Documentação

> Fonte: [Alura - Git Flow: o que é, como e quando utilizar](https://www.alura.com.br/artigos/git-flow-o-que-e-como-quando-utilizar?srsltid=AfmBOopzMECBzXZi4B-MMtz8-B8bNHIHBJoJKSa13qdjOf5RextEvvSo)
>  
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
