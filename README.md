# VOA + Voalle

Este repositório centraliza propostas de integração para reduzir o esforço operacional e técnico nas rotinas mais comuns envolvendo o ERP Voalle.

Hoje, grande parte das dores de integração com o Voalle aparece quando precisamos executar ações importantes de forma simples, rastreável e previsível, mas acabamos dependendo de fluxos manuais, regras de negócio pouco flexíveis ou ausência de endpoints claros para determinados casos de uso. A proposta deste projeto é organizar essas necessidades em especificações objetivas, facilitando a conversa entre times de produto, operação, desenvolvimento e parceiros de integração.

## Objetivo

Documentar, de forma prática, quais capacidades de integração seriam mais valiosas para o nosso contexto de operação com o Voalle, priorizando fluxos que:

- reduzam atividades manuais;
- deem mais autonomia para sistemas integradores;
- centralizem o histórico operacional no contrato do cliente;
- melhorem a auditabilidade das ações executadas;
- permitam automações seguras e reaproveitáveis.

## Principais dores que o projeto busca resolver

As especificações deste repositório foram pensadas para endereçar problemas recorrentes como:

- dificuldade para bloquear e desbloquear contratos de maneira direta, sem depender de regras paralelas que nem sempre atendem o cenário da operação;
- ausência de um padrão simples para registrar eventos relevantes no histórico do contrato;
- necessidade de criar trilhas de auditoria para campanhas, pagamentos, contatos e ações automatizadas;
- necessidade de gerar cobranças pontuais, como recargas ou serviços adicionais, com confirmação confiável de pagamento;
- falta de um material consolidado que traduza necessidades reais de negócio em requisitos claros de integração.

## Como este projeto ajuda

Em vez de tratar cada demanda de integração de forma isolada, este repositório propõe uma base organizada de contratos de API e fluxos desejados. Isso ajuda a:

- alinhar expectativa entre negócio e tecnologia;
- acelerar discussões com times internos e com a Voalle;
- transformar dores operacionais em requisitos concretos;
- servir como referência para futuras implementações, provas de conceito e validações.

## Escopo atual

Atualmente, o projeto cobre cenários como:

- bloqueio de contrato;
- desbloqueio de contrato;
- criação de tipos de evento;
- registro de eventos em contrato;
- geração de link de pagamento com confirmação via webhook.

Esses fluxos representam capacidades essenciais para operações que precisam integrar comunicação, cobrança, histórico de relacionamento e ações administrativas dentro do ciclo de vida do contrato.

## Estrutura do repositório

As especificações estão organizadas no diretório [`api-specs`](./api-specs):

- [`api-specs/block-contract.md`](./api-specs/block-contract.md): proposta de rota para bloqueio direto de contrato;
- [`api-specs/unblock-contract.md`](./api-specs/unblock-contract.md): proposta de rota para desbloqueio direto de contrato;
- [`api-specs/create-event-type.md`](./api-specs/create-event-type.md): criação de tipos de eventos reutilizáveis;
- [`api-specs/create-contract-event.md`](./api-specs/create-contract-event.md): registro de eventos vinculados ao contrato;
- [`api-specs/payment-link-generation.md`](./api-specs/payment-link-generation.md): fluxo de geração de link de pagamento e recebimento de webhook;
- [`api-specs/README.md`](./api-specs/README.md): visão geral das especificações.

Também existe o diretório [`api-gaps`](./api-gaps) para registrar APIs que já existem, mas ainda possuem limitações funcionais, técnicas ou de usabilidade para integração:

- [`api-gaps/README.md`](./api-gaps/README.md): visão geral da pasta;
- [`api-gaps/template.md`](./api-gaps/template.md): modelo para documentar problemas e lacunas em APIs existentes.

## Contexto da documentação oficial

Como referência de contexto, a Voalle disponibiliza uma coleção pública no Postman chamada `API's para Terceiros - ERPVoalle`, publicada em 3 de janeiro de 2025:

- documentação: [Postman Documenter](https://documenter.getpostman.com/view/16282829/TzzBqFw1#intro);
- foco: APIs para integrações de terceiros com o ERP Voalle;
- autenticação: realizada em ambiente separado do ERP;
- requisito: o usuário deve ser configurado como `Usuário integrador`;
- rastreabilidade: as ações executadas via API ficam registradas em nome do usuário autenticado.

Essa coleção atualmente está organizada em módulos como:

- Autenticação;
- Suite;
- CRM Voalle;
- Service Desk;
- ISP | Telecom;
- Faturamento;
- Financeiro;
- Faturamento Terceiro/Cofaturamento.

## O que a documentação oficial já cobre

A documentação oficial já apresenta endpoints para diversos fluxos operacionais relevantes, como:

- autenticação e refresh token;
- cadastro e atualização de pessoas;
- consultas e aberturas de solicitações;
- operações de CRM e contratos;
- atualização de conexão e consultas no contexto ISP;
- geração de contrato e aprovação de contrato;
- desbloqueio de contrato;
- boletos, liquidação, PIX e renegociação;
- webhook e confirmação em fluxos de faturamento de terceiros.

Isso mostra que já existe uma base importante de integração exposta pela Voalle, principalmente para processos transacionais e operacionais já consolidados

## Importante

As rotas, endpoints, parâmetros e estruturas descritos neste repositório representam necessidades e propostas de integração. Elas não devem ser tratadas como documentação oficial do Voalle sem validação prévia.

Ou seja:

- este material expressa o que precisamos ou gostaríamos de consumir;
- a implementação real deve ser adaptada conforme a documentação oficial disponível;
- qualquer adoção prática depende de alinhamento técnico e funcional com a Voalle e com os sistemas envolvidos.

## Próximos passos

Este repositório pode evoluir para cobrir outros pontos críticos da integração, como:

- consultas operacionais mais completas;
- automações financeiras;
- sincronização de status entre sistemas;
- webhooks adicionais;
- padronização de autenticação, erros e idempotência.

O objetivo final é construir uma base clara de integração que torne o ecossistema Voalle mais previsível, integrável e aderente às necessidades reais da operação.
