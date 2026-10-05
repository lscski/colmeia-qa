# Colmeia QA — Testes Funcionais

Projeto desenvolvido como parte de uma avaliação técnica para a posição de **Analista de Testes / QA**.

O objetivo do projeto é avaliar uma aplicação web fornecida para testes, identificar comportamentos inesperados e documentar os resultados de forma estruturada, incluindo casos de teste, evidências e análise dos defeitos encontrados.

---

## Objetivo

Realizar uma avaliação funcional e exploratória da aplicação, buscando identificar:

* falhas funcionais;
* inconsistências de validação;
* problemas de autenticação;
* problemas de controle de acesso;
* problemas de sessão;
* falhas de persistência;
* problemas de navegação;
* inconsistências de interface;
* problemas de usabilidade e acessibilidade.

Além dos testes funcionais, foram utilizadas ferramentas de desenvolvimento do navegador para analisar requisições HTTP, comportamento da aplicação e investigar a origem de alguns comportamentos identificados.

---

## Aplicação avaliada

**URL:** https://teste-colmeia-qa.colmeia-corp.com/

**Perfil utilizado:** QA

**Tipo de aplicação:** Web

**Navegador principal:** Google Chrome

---

## Escopo dos testes

Foram avaliadas as seguintes áreas:

* Login
* Autenticação
* Controle de acesso
* Sessão
* Recuperação de senha
* Dashboard
* Navegação
* Campanha
* Banco de Dados
* Criação de registros
* Validação de campos
* Exclusão de registros
* Arquivamento
* Pesquisa
* Persistência
* Colmeia Forms
* Interface
* Responsividade
* Acessibilidade

---

# Resultados

Durante a execução dos testes foram identificados comportamentos inesperados em diferentes áreas da aplicação.

### Principais problemas identificados

| ID      | Área                 | Descrição                                                      | Severidade  | Status     |
| ------- | -------------------- | -------------------------------------------------------------- | ----------- | ---------- |
| BUG-001 | Banco de Dados       | Registro sem nome pode ser salvo após nova tentativa           | Alta        | Confirmado |
| BUG-002 | Recuperação de senha | "Esqueceu a senha?" não executa nenhuma ação                   | Média       | Confirmado |
| BUG-003 | Autenticação         | Rotas internas podem ser acessadas sem autenticação            | Crítica     | Confirmado |
| BUG-005 | Sessão               | Não existe controle efetivo de sessão/logout                   | Alta        | Confirmado |
| BUG-006 | Banco de Dados       | Arquivar remove o registro em vez de arquivá-lo                | Alta        | Confirmado |
| BUG-007 | Banco de Dados       | Estado vazio não é atualizado corretamente após exclusão       | Média       | Confirmado |
| BUG-008 | Banco de Dados       | Atualização da página perde os registros criados               | Média       | Confirmado |
| BUG-009 | Banco de Dados       | Existe possibilidade de IDs duplicados                         | Média       | Confirmado |
| BUG-010 | Banco de Dados       | Botão de pesquisa não possui ação associada                    | Média       | Confirmado |
| BUG-011 | Persistência         | Registros não são persistidos após reload                      | Alta        | Confirmado |
| BUG-012 | Navegação            | Menu Campanha direciona para página sem conteúdo               | Média       | Confirmado |
| BUG-014 | Banco de Dados       | Lista de itens arquivados permanece vazia                      | Média       | Confirmado |
| BUG-015 | Login                | Mensagem informa login incorreto mesmo com credenciais válidas | Baixa/Média | Confirmado |
| BUG-016 | Interface            | Layout apresenta limitações em telas menores                   | Baixa       | Observado  |
| BUG-017 | Interface            | Interface apresenta mistura de português e inglês              | Baixa       | Observado  |

---

# Bugs de maior impacto

## BUG-003 — Acesso às rotas internas sem autenticação

Foi identificado que páginas internas da aplicação podem ser acessadas diretamente sem a realização de login.

Esse comportamento é considerado crítico por comprometer o controle de acesso da aplicação.

---

## BUG-001 — Validação inconsistente de campo obrigatório

A aplicação apresenta uma mensagem informando que o nome é obrigatório, porém permite a criação de um registro sem nome após uma nova tentativa.

O comportamento também foi reproduzido utilizando apenas espaços no campo.

---

## BUG-006 — Arquivamento remove o registro

A ação "Arquivar" remove o item da lista principal, porém o registro não aparece posteriormente na lista de itens arquivados.

Na prática, o comportamento se aproxima de uma exclusão em vez de um arquivamento.

---

## BUG-011 — Falta de persistência

Registros criados durante a utilização da aplicação desaparecem após a atualização da página.

Isso indica que os dados não estão sendo persistidos de forma permanente.

---

# Metodologia

A avaliação foi realizada utilizando uma abordagem de **teste exploratório**, combinada com casos de teste estruturados.

Durante a exploração foram utilizadas diferentes entradas e condições, incluindo:

* credenciais válidas;
* credenciais inválidas;
* campos vazios;
* campos contendo espaços;
* nomes longos;
* caracteres especiais;
* exclusão de registros;
* arquivamento;
* atualização da página;
* navegação direta por URL;
* navegação pelo histórico do navegador;
* utilização de janela anônima.

Após a identificação dos comportamentos inesperados, os cenários foram reproduzidos para confirmar sua consistência.

---

# Análise técnica

Além dos testes funcionais, foi utilizado o **Chrome DevTools** para investigar:

* requisições HTTP;
* Fetch/XHR;
* carregamento de recursos;
* comportamento das rotas;
* comportamento dos componentes;
* implementação dos fluxos envolvidos.

A análise técnica foi utilizada como evidência complementar e para auxiliar na identificação da origem de alguns comportamentos.

Por exemplo, durante a investigação foi possível identificar que determinadas funcionalidades possuem implementação incompleta ou comportamento diferente do esperado, como o fluxo de arquivamento e a ausência de controle de acesso nas rotas internas.

---

# Evidências

As evidências dos principais defeitos estão armazenadas em:

```text
evidence/
```

Exemplos:

```text
evidence/
├── BUG-001-empty-name.png
├── BUG-002-forgot-password.png
├── BUG-003-unauthenticated-access.png
├── BUG-006-before-archive.png
├── BUG-006-after-archive.png
├── BUG-011-before-reload.png
├── BUG-011-after-reload.png
├── BUG-012-campanha.png
├── BUG-014-archived-empty.png
└── BUG-015-valid-login-message.png
```

As screenshots foram utilizadas principalmente para documentar comportamentos classificados como `FAIL`.

---

# Casos de teste

Os casos de teste estão documentados em:

```text
docs/test-cases.md
```

Os cenários incluem:

* pré-condições;
* dados de teste;
* passos para reprodução;
* resultado esperado;
* resultado obtido;
* status;
* bug relacionado;
* prioridade.

Exemplo:

```text
TC-DB-007
Arquivar banco de dados

Resultado esperado:
O registro deve sair da lista ativa e aparecer nos itens arquivados.

Resultado obtido:
O registro desaparece da lista ativa e não aparece nos itens arquivados.

Status:
FAIL

Bug:
BUG-006
```

---

# Relatório de testes

O relatório consolidado está disponível em:

```text
docs/test-report.md
```

O documento apresenta:

* resumo da execução;
* bugs identificados;
* severidade;
* prioridade;
* passos para reprodução;
* resultado esperado;
* resultado obtido;
* testes que passaram;
* observações de qualidade;
* análise de rede;
* conclusão da avaliação.

---

# Estrutura do projeto

```text
colmeia-qa/
│
├── README.md
│
├── docs/
│   ├── test-report.md
│   └── test-cases.md
│
├── evidence/
│   ├── BUG-001-empty-name.png
│   ├── BUG-002-forgot-password.png
│   ├── BUG-003-unauthenticated-access.png
│   └── ...
│
└── tests/
    └── ...
```

A pasta `tests/` será utilizada para os testes automatizados desenvolvidos posteriormente.

---

# Ferramentas utilizadas

* Google Chrome
* Chrome DevTools
* Git
* GitHub
* Playwright — etapa de automação
* TypeScript — etapa de automação

---

# Próximas etapas

As próximas etapas do projeto são:

1. Configurar o ambiente de automação.
2. Implementar testes automatizados com Playwright.
3. Criar testes de autenticação.
4. Criar testes para o fluxo de Banco de Dados.
5. Automatizar cenários críticos identificados durante os testes manuais.
6. Executar os testes automatizados.
7. Registrar evidências de falhas de automação.
8. Integrar a execução dos testes ao projeto.

---

# Conclusão

A avaliação exploratória identificou problemas principalmente relacionados a **autenticação, controle de acesso, validação, persistência e gerenciamento dos registros**.

O objetivo deste projeto não foi apenas identificar falhas, mas demonstrar um processo de QA completo:

```text
Exploração
    ↓
Identificação do comportamento
    ↓
Reprodução
    ↓
Definição do resultado esperado
    ↓
Classificação do defeito
    ↓
Documentação
    ↓
Evidência
    ↓
Automação dos cenários relevantes
```

O projeto continuará sendo utilizado para demonstrar a evolução dos testes manuais para testes automatizados.
