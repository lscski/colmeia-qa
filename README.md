# Colmeia QA — Testes Funcionais

Projeto desenvolvido como parte da avaliação técnica para a posição de **Analista de Testes / QA**.

## Objetivo

Realizar testes exploratórios e funcionais na aplicação fornecida, identificando comportamentos inesperados, inconsistências e possíveis defeitos.

## Escopo

Os testes realizados contemplam:

* Autenticação
* Sessão
* Navegação
* Dashboard
* Campanha
* Banco de Dados
* Colmeia Forms
* Recuperação de senha
* Validação de campos
* Exclusão de registros
* Arquivamento de registros
* Persistência de dados
* Análise de requisições HTTP

## Bugs e comportamentos identificados

| ID      | Área                 | Descrição                                                              | Status       |
| ------- | -------------------- | ---------------------------------------------------------------------- | ------------ |
| BUG-001 | Banco de Dados       | Registro é salvo sem nome mesmo com validação de campo obrigatório     | Confirmado   |
| BUG-002 | Sessão               | Possibilidade de retornar ao sistema utilizando histórico do navegador | Investigação |
| BUG-003 | Recuperação de senha | Funcionalidade "Esqueci minha senha" não funciona                      | Investigação |
| BUG-004 | Arquivamento         | Item arquivado não aparece na lista de arquivados                      | Investigação |

## Documentação

O relatório detalhado dos testes está disponível em:

`docs/test-report.md`

## Estrutura

```text
colmeia-qa/
├── docs/
│   └── test-report.md
├── evidence/
├── tests/
└── README.md
```

## Ferramentas

* Google Chrome
* Chrome DevTools
* Git
* GitHub

## Próximas etapas

* Finalizar a investigação dos comportamentos identificados;
* Criar casos de teste estruturados;
* Implementar testes automatizados;
* Executar os testes;
* Gerar relatório de execução.
