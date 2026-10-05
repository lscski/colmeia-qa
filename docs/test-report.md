# Relatório de Testes — Colmeia QA

## 1. Informações gerais

**Aplicação:** Colmeia
**URL:** https://teste-colmeia-qa.colmeia-corp.com/
**Perfil utilizado:** QA
**Tipo de teste:** Testes exploratórios e funcionais
**Ambiente:** Web
**Navegador principal:** Google Chrome
**Ferramentas utilizadas:**

* Google Chrome
* Chrome DevTools
* Git
* GitHub
* Análise de requisições HTTP
* Inspeção de HTML/CSS/JavaScript

---

## 2. Objetivo

Avaliar o comportamento funcional da aplicação, identificando:

* comportamentos inesperados;
* falhas funcionais;
* inconsistências de validação;
* problemas de autenticação e sessão;
* problemas de persistência;
* problemas de navegação;
* problemas de usabilidade;
* possíveis problemas de acessibilidade.

Além da execução dos testes, foram realizadas análises complementares utilizando o DevTools para investigar requisições de rede, comportamento da aplicação e implementação dos componentes envolvidos.

---

## 3. Escopo

Foram avaliadas as seguintes áreas:

* Login
* Autenticação
* Recuperação de senha
* Sessão
* Navegação
* Dashboard
* Campanha
* Banco de Dados
* Criação de registros
* Validação de campos
* Exclusão de registros
* Arquivamento de registros
* Busca
* Atualização/reload
* Persistência dos dados
* Colmeia Forms
* Interface e acessibilidade

---

# 4. Resumo dos resultados

Durante os testes foram identificados problemas em diferentes níveis de severidade.

| ID      | Área                 | Problema                                                       | Severidade  | Status     |
| ------- | -------------------- | -------------------------------------------------------------- | ----------- | ---------- |
| BUG-001 | Banco de Dados       | Registro sem nome é salvo após segunda tentativa               | Alta        | Confirmado |
| BUG-002 | Recuperação de senha | Botão "Esqueceu a senha?" não executa nenhuma ação             | Média       | Confirmado |
| BUG-003 | Autenticação         | Rotas internas podem ser acessadas sem autenticação            | Crítica     | Confirmado |
| BUG-005 | Sessão               | Não existe logout/controle efetivo de sessão                   | Alta        | Confirmado |
| BUG-006 | Banco de Dados       | Arquivar remove o registro em vez de arquivá-lo                | Alta        | Confirmado |
| BUG-007 | Banco de Dados       | Estado vazio não é exibido corretamente após exclusão          | Média       | Confirmado |
| BUG-008 | Banco de Dados       | Atualizar a página perde os registros criados                  | Média       | Confirmado |
| BUG-009 | Banco de Dados       | IDs podem ser duplicados após exclusões                        | Média       | Confirmado |
| BUG-010 | Banco de Dados       | Botão de busca não possui comportamento associado              | Média       | Confirmado |
| BUG-011 | Persistência         | Dados criados não são persistidos após reload                  | Alta        | Confirmado |
| BUG-012 | Navegação            | Menu Campanha direciona para página sem conteúdo               | Média       | Confirmado |
| BUG-014 | Banco de Dados       | Lista de itens arquivados permanece vazia                      | Média       | Confirmado |
| BUG-015 | Login                | Mensagem informa login incorreto mesmo com credenciais válidas | Baixa/Média | Confirmado |
| BUG-016 | Interface            | Layout do login possui limitações em telas menores             | Baixa       | Observado  |
| BUG-017 | Interface            | Interface apresenta mistura de português e inglês              | Baixa       | Observado  |

> Observação: BUG-003 e BUG-005 estão relacionados. O problema de autenticação permite acesso direto às rotas internas e também impede que exista um controle efetivo de sessão.

---

# 5. Bugs críticos e de alta prioridade

## BUG-003 — Acesso às rotas internas sem autenticação

**Severidade:** Crítica
**Prioridade:** P0
**Área:** Autenticação / Segurança

### Descrição

É possível acessar diretamente páginas internas da aplicação sem realizar login.

### Pré-condição

Não estar autenticado na aplicação.

### Passos para reprodução

1. Abrir uma janela anônima do navegador.
2. Acessar diretamente uma rota interna do sistema.
3. Observar o comportamento da aplicação.

### Resultado esperado

O sistema deveria verificar a existência de uma sessão válida.

Caso o usuário não esteja autenticado, deveria:

* bloquear o acesso;
* redirecionar para a tela de login;
* impedir o acesso ao conteúdo protegido.

### Resultado obtido

A aplicação permite acessar páginas internas diretamente, sem autenticação.

### Impacto

Esse comportamento compromete o controle de acesso da aplicação, pois páginas que deveriam depender de autenticação podem ser acessadas diretamente.

### Evidência

Teste realizado em janela anônima e análise das rotas da aplicação.

---

## BUG-005 — Ausência de controle efetivo de sessão/logout

**Severidade:** Alta
**Prioridade:** P1
**Área:** Sessão / Autenticação

### Descrição

A aplicação não apresenta mecanismo efetivo de logout e não mantém um controle de sessão que impeça o acesso às páginas internas.

### Passos para reprodução

1. Realizar login.
2. Navegar para o dashboard.
3. Utilizar os controles de navegação do navegador.
4. Reabrir a URL interna diretamente.
5. Testar o acesso em uma janela anônima.

### Resultado esperado

O sistema deveria possuir uma sessão autenticada e controlar o acesso às rotas protegidas.

Ao realizar logout ou quando não houver sessão válida, o usuário deveria ser direcionado para o login.

### Resultado obtido

As páginas internas continuam acessíveis sem autenticação.

### Impacto

Pode permitir acesso não autorizado às áreas internas da aplicação.

---

## BUG-001 — Validação permite salvar registro sem nome

**Severidade:** Alta
**Prioridade:** P1
**Área:** Banco de Dados

### Descrição

O sistema apresenta uma mensagem informando que o nome é obrigatório, porém permite criar um registro sem nome após uma segunda tentativa.

### Passos para reprodução

1. Acessar "Banco de Dados".
2. Selecionar a opção para criar um novo item.
3. Deixar o campo de nome vazio.
4. Tentar salvar.
5. Observar a mensagem de validação.
6. Tentar salvar novamente sem preencher o campo.

### Resultado esperado

O sistema deveria impedir a criação enquanto o campo obrigatório estiver vazio.

### Resultado obtido

Na primeira tentativa é exibida uma mensagem de validação.

Na segunda tentativa, o registro é criado mesmo sem nome.

### Impacto

Permite a criação de dados inválidos e contradiz a regra de validação apresentada ao usuário.

### Variação testada

O mesmo comportamento foi observado utilizando apenas espaços no campo de nome.

---

## BUG-006 — Arquivar remove o registro

**Severidade:** Alta
**Prioridade:** P1
**Área:** Banco de Dados

### Descrição

A opção "Arquivar" remove o registro da lista principal, mas o item não aparece posteriormente na lista de itens arquivados.

### Passos para reprodução

1. Criar um banco de dados.
2. Localizar o registro criado.
3. Selecionar "Arquivar".
4. Abrir a área de itens arquivados.

### Resultado esperado

O registro deveria:

1. deixar de aparecer na lista de itens ativos;
2. permanecer armazenado;
3. aparecer na lista de itens arquivados.

### Resultado obtido

O registro desaparece da lista principal, porém não aparece na lista de arquivados.

### Impacto

A operação de arquivamento resulta, na prática, na remoção do registro.

---

## BUG-011 — Dados não são persistidos após atualização

**Severidade:** Alta
**Prioridade:** P1
**Área:** Persistência / Banco de Dados

### Descrição

Os registros criados desaparecem após atualizar a página.

### Passos para reprodução

1. Acessar "Banco de Dados".
2. Criar um novo registro.
3. Confirmar que o registro aparece na lista.
4. Atualizar a página.
5. Observar a lista novamente.

### Resultado esperado

Os registros deveriam permanecer disponíveis após a atualização da página.

### Resultado obtido

Os registros criados desaparecem.

### Impacto

O usuário pode interpretar que os dados foram salvos quando, na realidade, eles permanecem apenas no estado atual da aplicação.

---

# 6. Bugs de média prioridade

## BUG-002 — Recuperação de senha sem ação

**Severidade:** Média
**Prioridade:** P2

### Descrição

O link "Esqueceu a senha?" não executa nenhuma ação.

### Passos

1. Abrir a tela de login.
2. Clicar em "Esqueceu a senha?".

### Resultado esperado

O sistema deveria abrir um fluxo de recuperação de senha ou informar que a funcionalidade não está disponível.

### Resultado obtido

Nenhuma ação ocorre.

### Evidência

Não foi identificada requisição de rede associada ao clique.

---

## BUG-007 — Estado vazio incorreto após exclusão

**Severidade:** Média
**Prioridade:** P2

### Descrição

Após excluir registros, o estado da tela não é atualizado corretamente para representar que não existem mais itens.

### Resultado esperado

Quando não houver registros, deveria ser apresentada uma mensagem de estado vazio.

### Resultado obtido

O comportamento do estado vazio não é atualizado corretamente após determinadas exclusões.

---

## BUG-008 — Botão de atualização perde os dados

**Severidade:** Média
**Prioridade:** P2

### Descrição

Ao atualizar a página, os registros criados desaparecem.

### Resultado esperado

A atualização deveria apenas recarregar os dados existentes.

### Resultado obtido

Os dados criados são perdidos.

### Relação

Relacionado ao BUG-011, que trata da ausência de persistência dos dados.

---

## BUG-009 — Possibilidade de IDs duplicados

**Severidade:** Média
**Prioridade:** P2

### Descrição

A geração dos IDs dos registros depende da quantidade atual de itens.

### Cenário

1. Criar três registros.
2. Excluir o primeiro.
3. Criar outro registro.

O novo registro pode receber um ID já utilizado por outro item.

### Impacto

IDs duplicados podem provocar operações incorretas de edição, exclusão ou identificação de registros.

---

## BUG-010 — Botão de busca sem ação

**Severidade:** Média
**Prioridade:** P2

### Descrição

O campo de busca permite digitação, porém o botão visual de busca não possui comportamento associado.

### Resultado esperado

O botão deveria executar a pesquisa ou aplicar o filtro.

### Resultado obtido

Clicar no botão não produz ação observável.

---

## BUG-012 — Menu Campanha abre página sem conteúdo

**Severidade:** Média
**Prioridade:** P2

### Descrição

O menu "Campanha" direciona para uma página que não apresenta conteúdo funcional.

### Passos

1. Acessar o dashboard.
2. Abrir o menu "Campanha".
3. Selecionar a opção correspondente.

### Resultado esperado

A área selecionada deveria apresentar seu conteúdo.

### Resultado obtido

A página é carregada, porém o conteúdo esperado não é apresentado.

---

## BUG-014 — Lista de itens arquivados permanece vazia

**Severidade:** Média
**Prioridade:** P2

### Descrição

A aplicação apresenta a opção de visualizar itens arquivados, porém os registros arquivados não são exibidos.

### Resultado esperado

Itens arquivados deveriam aparecer nessa área.

### Resultado obtido

A lista permanece vazia.

### Relação

Relacionado ao BUG-006.

---

# 7. BUG-015 — Mensagem incorreta durante login válido

**Severidade:** Baixa/Média
**Prioridade:** P3

### Descrição

Ao utilizar credenciais válidas, a aplicação apresenta uma mensagem informando que o login está incorreto e pergunta se o usuário deseja continuar.

### Passos

1. Informar:

   * Usuário: `qa@test.com`
   * Senha: `123456`
2. Clicar em entrar.
3. Observar a mensagem apresentada.
4. Selecionar "Continuar".

### Resultado esperado

Credenciais válidas deveriam autenticar o usuário diretamente ou apresentar uma mensagem de confirmação coerente.

### Resultado obtido

O sistema informa que o login está incorreto, embora permita continuar e acessar o sistema.

### Impacto

Pode gerar confusão para o usuário e transmitir uma informação incorreta sobre o estado da autenticação.

---

# 8. Testes que passaram

Nem todos os testes apresentaram falhas.

## Login

* Credenciais válidas permitem acesso após confirmação.
* Senha incorreta não permite acesso.
* Usuário incorreto não permite acesso.
* Campos vazios não permitem login normal.
* Combinações inválidas de usuário/senha não concederam acesso.

## Banco de Dados

* Criação de registro com nome válido funciona.
* Registro criado aparece na lista.
* Exclusão remove o registro da lista.
* Após exclusão, o registro não reaparece simplesmente com um refresh da tela.
* Nomes longos são aceitos.
* Caracteres especiais são aceitos.

---

# 9. Observações de qualidade

Além dos defeitos funcionais, foram observados alguns pontos que podem ser considerados melhorias de qualidade.

### Interface

* Alguns elementos utilizam português e inglês simultaneamente.
* Existem elementos de interface sem indicação clara de acessibilidade.
* Alguns botões baseados apenas em ícones não possuem identificação textual evidente.
* O layout da tela de login utiliza uma estrutura fixa que pode apresentar problemas em telas menores.

### Formulários

* O campo de senha não apresenta opção evidente para visualizar/ocultar a senha.
* O formulário utiliza configurações de autocomplete que podem prejudicar a experiência do usuário.
* O botão de login permanece disponível mesmo quando os campos estão inválidos.

### Experiência do usuário

* O fechamento do modal pode descartar dados digitados sem confirmação.
* A exclusão não apresenta confirmação antes da operação.
* O sistema apresenta mensagens de erro que poderiam ser mais específicas.

Esses pontos foram classificados como observações de qualidade e não necessariamente como defeitos funcionais.

---

# 10. Análise de rede

O Chrome DevTools foi utilizado para observar o comportamento das requisições durante a execução dos testes.

Foram observados recursos como:

* `index.html`
* arquivos JavaScript
* arquivos CSS
* imagens
* fontes

Durante algumas ações, não foram observadas requisições `Fetch/XHR` correspondentes às operações esperadas.

Isso foi utilizado como evidência complementar para investigar comportamentos como:

* recuperação de senha;
* persistência dos registros;
* operações de banco de dados.

Um código HTTP `301` observado durante o carregamento da aplicação não foi classificado isoladamente como defeito, pois redirecionamentos HTTP podem ser comportamento esperado da infraestrutura.

---

# 11. Conclusão

A aplicação apresenta funcionalidades básicas que podem ser executadas, porém foram identificados problemas relevantes principalmente nas áreas de:

* autenticação;
* controle de acesso;
* persistência;
* validação;
* arquivamento;
* navegação.

O problema de maior impacto identificado é a possibilidade de acesso às rotas internas sem autenticação.

Também existem inconsistências importantes no gerenciamento dos registros, especialmente a possibilidade de salvar itens sem nome, a ausência de persistência após atualização e o comportamento incorreto da funcionalidade de arquivamento.

Os casos de teste detalhados utilizados durante a avaliação estão documentados em:

`docs/test-cases.md`

Os testes automatizados serão implementados utilizando Playwright e TypeScript na pasta:

`tests/`
