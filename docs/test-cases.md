# Casos de Teste — Colmeia QA

## 1. Convenções

### Status

| Status  | Significado                           |
| ------- | ------------------------------------- |
| PASS    | Comportamento corresponde ao esperado |
| FAIL    | Comportamento diferente do esperado   |
| BLOCKED | Não foi possível executar o teste     |
| N/A     | Não aplicável                         |

### Prioridade

| Prioridade | Significado |
| ---------- | ----------- |
| P0         | Crítica     |
| P1         | Alta        |
| P2         | Média       |
| P3         | Baixa       |

---

# 2. Autenticação

## TC-LOGIN-001 — Login com credenciais válidas

**Prioridade:** P0
**Categoria:** Autenticação
**Status:** PASS

### Pré-condições

* Usuário não autenticado.
* Aplicação disponível.

### Dados

**Usuário:** `qa@test.com`
**Senha:** `123456`

### Passos

1. Acessar a tela de login.
2. Informar o usuário.
3. Informar a senha.
4. Clicar no botão de login.
5. Confirmar a continuação quando apresentada.

### Resultado esperado

O usuário deve conseguir acessar o sistema.

### Resultado obtido

O acesso foi realizado com sucesso após confirmação.

---

## TC-LOGIN-002 — Login com senha incorreta

**Prioridade:** P0
**Categoria:** Autenticação
**Status:** PASS

### Dados

Usuário válido com senha incorreta.

### Passos

1. Acessar a tela de login.
2. Informar um usuário válido.
3. Informar uma senha incorreta.
4. Tentar realizar o login.

### Resultado esperado

O sistema deve impedir o acesso.

### Resultado obtido

O acesso não foi concedido.

---

## TC-LOGIN-003 — Login com usuário incorreto

**Prioridade:** P0
**Categoria:** Autenticação
**Status:** PASS

### Passos

1. Informar um usuário inexistente.
2. Informar uma senha.
3. Tentar realizar o login.

### Resultado esperado

O acesso deve ser negado.

### Resultado obtido

O acesso não foi concedido.

---

## TC-LOGIN-004 — Login com campos vazios

**Prioridade:** P1
**Categoria:** Validação
**Status:** PASS

### Passos

1. Acessar a tela de login.
2. Não preencher os campos.
3. Tentar realizar o login.

### Resultado esperado

O sistema deve impedir o envio e apresentar validações apropriadas.

### Resultado obtido

O login não foi realizado.

---

## TC-LOGIN-005 — Recuperação de senha

**Prioridade:** P2
**Categoria:** Recuperação de senha
**Status:** FAIL
**Bug:** BUG-002

### Passos

1. Acessar a tela de login.
2. Clicar em "Esqueceu a senha?".

### Resultado esperado

O sistema deveria abrir um fluxo de recuperação de senha.

### Resultado obtido

Nenhuma ação ocorre.

---

# 3. Controle de acesso

## TC-AUTH-001 — Acesso direto ao dashboard sem autenticação

**Prioridade:** P0
**Categoria:** Segurança / Autenticação
**Status:** FAIL
**Bug:** BUG-003

### Pré-condições

* Usuário não autenticado.
* Janela anônima do navegador.

### Passos

1. Abrir uma janela anônima.
2. Acessar diretamente uma URL interna do dashboard.

### Resultado esperado

O sistema deveria redirecionar o usuário para a tela de login.

### Resultado obtido

A rota interna pode ser acessada sem autenticação.

---

## TC-AUTH-002 — Navegação pelo histórico após login

**Prioridade:** P1
**Categoria:** Sessão
**Status:** FAIL
**Bug:** BUG-005

### Passos

1. Realizar login.
2. Acessar o dashboard.
3. Utilizar o botão voltar do navegador.
4. Utilizar o botão avançar.
5. Acessar novamente uma rota interna.

### Resultado esperado

O sistema deveria manter o controle da sessão e bloquear acesso quando não houver autenticação válida.

### Resultado obtido

As páginas internas permanecem acessíveis.

---

# 4. Banco de Dados

## TC-DB-001 — Criar banco de dados com nome válido

**Prioridade:** P1
**Categoria:** CRUD
**Status:** PASS

### Passos

1. Acessar Banco de Dados.
2. Selecionar a opção de criação.
3. Informar um nome válido.
4. Confirmar a criação.

### Resultado esperado

O registro deve ser criado e aparecer na lista.

### Resultado obtido

Registro criado corretamente.

---

## TC-DB-002 — Criar banco de dados sem nome

**Prioridade:** P1
**Categoria:** Validação
**Status:** FAIL
**Bug:** BUG-001

### Passos

1. Acessar Banco de Dados.
2. Abrir o formulário de criação.
3. Deixar o nome vazio.
4. Clicar para criar.
5. Observar a mensagem.
6. Tentar novamente sem preencher o nome.

### Resultado esperado

O registro não deve ser criado enquanto o nome estiver vazio.

### Resultado obtido

A primeira tentativa apresenta validação, porém uma segunda tentativa permite criar um registro sem nome.

---

## TC-DB-003 — Criar banco de dados contendo apenas espaços

**Prioridade:** P1
**Categoria:** Validação
**Status:** FAIL
**Bug:** BUG-001

### Passos

1. Abrir o formulário de criação.
2. Informar somente espaços no campo de nome.
3. Tentar criar o registro.
4. Repetir a tentativa.

### Resultado esperado

O sistema deve considerar o valor inválido.

### Resultado obtido

O registro pode ser criado após nova tentativa.

---

## TC-DB-004 — Criar banco com caracteres especiais

**Prioridade:** P2
**Categoria:** Validação
**Status:** PASS

### Passos

1. Abrir o formulário de criação.
2. Informar nome contendo caracteres especiais.
3. Salvar.

### Resultado esperado

O registro deve ser criado corretamente caso os caracteres sejam permitidos.

### Resultado obtido

Registro criado.

---

## TC-DB-005 — Criar banco com nome longo

**Prioridade:** P2
**Categoria:** Validação
**Status:** PASS

### Passos

1. Informar um nome longo.
2. Salvar o registro.

### Resultado esperado

O sistema deve aceitar ou rejeitar o valor conforme limite definido.

### Resultado obtido

O valor foi aceito.

---

## TC-DB-006 — Excluir banco de dados

**Prioridade:** P1
**Categoria:** CRUD
**Status:** PASS

### Passos

1. Criar um registro.
2. Localizar o registro.
3. Selecionar a opção de exclusão.
4. Atualizar a página.
5. Verificar o registro.

### Resultado esperado

O registro excluído não deve continuar disponível.

### Resultado obtido

O registro foi removido.

### Observação

A aplicação não apresenta confirmação antes da exclusão. Esse comportamento foi registrado como observação de UX, não como defeito funcional confirmado.

---

## TC-DB-007 — Arquivar banco de dados

**Prioridade:** P1
**Categoria:** CRUD
**Status:** FAIL
**Bug:** BUG-006

### Passos

1. Criar um registro.
2. Selecionar "Arquivar".
3. Abrir a área de itens arquivados.

### Resultado esperado

O registro deve sair da lista ativa e aparecer nos itens arquivados.

### Resultado obtido

O registro desaparece da lista ativa e não aparece nos itens arquivados.

---

## TC-DB-008 — Persistência após atualização

**Prioridade:** P1
**Categoria:** Persistência
**Status:** FAIL
**Bug:** BUG-011

### Passos

1. Criar um registro.
2. Confirmar sua presença na lista.
3. Atualizar a página.
4. Verificar novamente a lista.

### Resultado esperado

O registro deve continuar disponível.

### Resultado obtido

O registro desaparece após o reload.

---

## TC-DB-009 — Atualização da lista

**Prioridade:** P2
**Categoria:** Interface / Persistência
**Status:** FAIL
**Bug:** BUG-008

### Passos

1. Criar um registro.
2. Utilizar a opção de atualização/reload.
3. Observar a lista.

### Resultado esperado

A lista deveria ser atualizada mantendo os dados persistidos.

### Resultado obtido

Os registros desaparecem.

---

## TC-DB-010 — IDs após exclusão

**Prioridade:** P2
**Categoria:** Integridade de dados
**Status:** FAIL
**Bug:** BUG-009

### Passos

1. Criar três registros.
2. Excluir o primeiro.
3. Criar um novo registro.
4. Verificar a identificação dos registros.

### Resultado esperado

Cada registro deve possuir identificador único.

### Resultado obtido

Existe possibilidade de reutilização de um ID já existente.

---

## TC-DB-011 — Pesquisa pelo campo de busca

**Prioridade:** P2
**Categoria:** Busca
**Status:** FAIL
**Bug:** BUG-010

### Passos

1. Criar dois ou mais registros.
2. Informar um termo no campo de pesquisa.
3. Observar o filtro.
4. Clicar no botão de pesquisa.

### Resultado esperado

O botão de pesquisa deveria executar/aplicar o filtro.

### Resultado obtido

O botão visual de pesquisa não apresenta ação observável.

---

# 5. Itens arquivados

## TC-ARCHIVE-001 — Visualizar itens arquivados

**Prioridade:** P2
**Categoria:** Arquivamento
**Status:** FAIL
**Bug:** BUG-014

### Passos

1. Acessar Banco de Dados.
2. Acessar a área de itens arquivados.

### Resultado esperado

Os itens arquivados deveriam ser listados.

### Resultado obtido

A área permanece sem registros.

### Relação

Relacionado ao BUG-006.

---

# 6. Navegação

## TC-NAV-001 — Acessar menu Campanha

**Prioridade:** P2
**Categoria:** Navegação
**Status:** FAIL
**Bug:** BUG-012

### Passos

1. Acessar o dashboard.
2. Abrir o menu Campanha.
3. Selecionar uma opção disponível.

### Resultado esperado

A opção selecionada deveria apresentar o conteúdo correspondente.

### Resultado obtido

A navegação ocorre, porém a página não apresenta o conteúdo esperado.

---

## TC-NAV-002 — Acessar Colmeia Forms

**Prioridade:** P2
**Categoria:** Navegação / Funcionalidade
**Status:** FAIL

### Passos

1. Abrir o menu Campanha.
2. Acessar Colmeia Forms.

### Resultado esperado

A página deveria apresentar a funcionalidade correspondente.

### Resultado obtido

A página é apresentada sem conteúdo funcional visível.

### Observação

Durante a investigação do código da aplicação, o componente correspondente também foi identificado como vazio. Portanto, o comportamento aparenta estar relacionado à implementação atual da aplicação.

---

# 7. Interface

## TC-UI-001 — Mensagem de login válido

**Prioridade:** P3
**Categoria:** UX
**Status:** FAIL
**Bug:** BUG-015

### Passos

1. Informar credenciais válidas.
2. Realizar login.
3. Observar a mensagem apresentada.

### Resultado esperado

A mensagem deveria indicar corretamente que as credenciais são válidas.

### Resultado obtido

É apresentada uma mensagem indicando que o login está incorreto, apesar de ser possível continuar para o sistema.

---

## TC-UI-002 — Responsividade da tela de login

**Prioridade:** P3
**Categoria:** Responsividade
**Status:** Observação

### Passos

1. Abrir a tela de login.
2. Reduzir a largura da janela.
3. Observar o comportamento do layout.

### Resultado esperado

O layout deveria se adaptar adequadamente a diferentes resoluções.

### Resultado obtido

Foi identificada uma estrutura de layout que pode apresentar limitações em telas menores.

---

## TC-UI-003 — Consistência de idioma

**Prioridade:** P3
**Categoria:** UX
**Status:** Observação

### Passos

1. Navegar pela interface.
2. Verificar textos, labels e botões.

### Resultado esperado

A interface deveria manter consistência no idioma.

### Resultado obtido

Foram identificados elementos em português e inglês na mesma interface.

---

# 8. Resumo de execução

| Categoria           | PASS | FAIL | Observação |
| ------------------- | ---: | ---: | ---------: |
| Login               |    4 |    1 |          0 |
| Autenticação/Sessão |    0 |    2 |          0 |
| Banco de Dados      |    5 |    6 |          0 |
| Arquivamento        |    0 |    1 |          0 |
| Navegação           |    0 |    2 |          0 |
| Interface           |    0 |    1 |          2 |

---

# 9. Critérios de encerramento

A avaliação exploratória foi considerada suficiente para iniciar a etapa de automação quando:

* os principais fluxos foram explorados;
* os comportamentos inconsistentes foram reproduzidos;
* os resultados esperados foram definidos;
* os defeitos foram classificados por prioridade;
* os principais cenários foram documentados.

Os cenários automatizáveis serão posteriormente implementados utilizando Playwright e TypeScript.

---

# 10. Próxima etapa

Os casos prioritários para automação são:

1. Login com credenciais válidas.
2. Login com credenciais inválidas.
3. Acesso direto ao dashboard sem autenticação.
4. Criação de banco de dados.
5. Validação de nome obrigatório.
6. Exclusão de banco de dados.
7. Arquivamento de banco de dados.
8. Persistência após reload.
9. Navegação entre áreas principais.
10. Recuperação de senha.
