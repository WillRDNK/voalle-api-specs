# Rota para Registrar Evento em Contrato

## Descrição
Esta rota permite registrar um novo evento em um contrato específico, criando um log de ações ou comunicações realizadas. Isso centraliza informações como pagamentos recebidos, campanhas enviadas, tentativas de contato, etc.

## Endpoint
`POST /api/contracts/{contractId}/events`

## Parâmetros
- `contractId` (path): ID do contrato onde o evento será registrado (obrigatório, string ou integer)

## Corpo da Requisição
```json
{
  "eventTypeId": "ID do tipo de evento (obrigatório, string ou integer)",
  "details": "Detalhes adicionais do evento (opcional, string, ex: 'Email enviado para cliente@exemplo.com')",
}
```

## Resposta de Sucesso
- Status: 201 Created
- Corpo:
```json
{
  "success": true,
  "message": "Evento registrado com sucesso no contrato",
  "event": {
    "id": "ID gerado para o evento",
    "contractId": "{contractId}",
    "eventTypeId": "ID do tipo",
    "eventTypeName": "Nome do tipo de evento",
    "details": "Detalhes",
    "createdBy": "ID do usuário",
    "createdAt": "Data de criação"
  }
}
```

## Resposta de Erro
- Status: 400 Bad Request (dados inválidos, como eventTypeId inexistente)
- Status: 404 Not Found (contrato ou tipo de evento não encontrado)
- Status: 500 Internal Server Error (erro interno)

## Autenticação
Requer autenticação especifica de usuario integrador.

## Notas
- Eventos são imutáveis após criação.
- Permite rastrear histórico completo de interações com o contrato.
- Exemplos: registrar "Pagamento Recebido" automaticamente ao processar pagamento, ou "Campanha de WhatsApp Enviada" ao enviar mensagem.