# Modelo para Documentar API Existente com Problemas ou Lacunas

Use este modelo para registrar APIs que ja existem, mas nao possuem um funcionamento adequado ou nao atendem totalmente a necessidade da integracao.

## Nome da API
Nome funcional da rota ou servico.

## Contexto
Explique onde essa API e usada hoje e qual processo depende dela.

## Endpoint Atual
`METHOD /path/{param}`

## Objetivo da API
Descreva o que essa API deveria permitir fazer do ponto de vista do negocio.

## Comportamento Atual
Descreva como a API funciona hoje na pratica.

## Problemas Identificados
- Liste os problemas observados.
- Exemplo: retorno incompleto.
- Exemplo: nao permite filtro necessario.
- Exemplo: nao respeita o fluxo operacional esperado.

## Impacto na Operacao ou na Integracao
Descreva o impacto real causado pelo problema.

## O que esta faltando
- Campos adicionais no retorno
- Novos filtros
- Melhor tratamento de erro
- Webhook
- Idempotencia
- Documentacao
- Ajuste de regra de negocio

## Comportamento Esperado
Descreva como a API deveria funcionar para atender o cenario corretamente.

## Exemplo de Requisicao Atual
```json
{}
```

## Exemplo de Resposta Atual
```json
{}
```

## Exemplo de Resposta Esperada
```json
{}
```

## Regras de Negocio Envolvidas
Liste regras, restricoes, validacoes ou dependencias conhecidas.

## Prioridade
`baixa | media | alta | critica`

## Observacoes
Informacoes adicionais, dependencias externas, alinhamentos pendentes ou links relevantes.
