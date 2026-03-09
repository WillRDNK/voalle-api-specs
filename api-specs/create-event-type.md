# Rota para Criar Tipo de Evento

## Descrição
Esta rota permite criar um novo tipo de evento para ser usado nos logs de contratos. Tipos de eventos centralizam as categorias de ações ou comunicações realizadas nos contratos, como campanhas de email, WhatsApp, pagamentos, etc.

## Endpoint
`POST /api/event-types`

## Parâmetros
Nenhum parâmetro de path ou query.

## Corpo da Requisição
```json
{
  "name": "Nome do tipo de evento (obrigatório, string, ex: 'Campanha de Email Enviada')",
  "description": "Descrição opcional do tipo de evento (string)",
  "category": "Categoria do evento (opcional, string, ex: 'comunicação', 'pagamento', 'bloqueio')"
}
```

## Resposta de Sucesso
- Status: 201 Created
- Corpo:
```json
{
  "success": true,
  "message": "Tipo de evento criado com sucesso",
  "eventType": {
    "id": "ID gerado para o tipo de evento",
    "name": "Nome do tipo",
    "description": "Descrição",
    "category": "Categoria",
    "createdAt": "Data de criação"
  }
}
```

## Resposta de Erro
- Status: 400 Bad Request (dados inválidos, como nome vazio)
- Status: 409 Conflict (tipo de evento com mesmo nome já existe)
- Status: 500 Internal Server Error (erro interno)

## Autenticação
Requer autenticação especifica de usuario integrador.

## Notas
- Os tipos de eventos são globais e podem ser reutilizados em múltiplos contratos.
- Exemplos de tipos: "Pagamento Recebido", "Campanha de Email Enviada", "Campanha de WhatsApp Enviada", "Bloqueio Aplicado".