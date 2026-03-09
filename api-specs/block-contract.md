# Rota de Bloqueio de Contrato

## Descrição
Esta rota permite bloquear um contrato de forma independente, sem seguir as regras de negócio de desbloqueio por confiança ou quantidade mensal de desbloqueios.

## Endpoint
`POST /api/contracts/{contractId}/block`

## Parâmetros
- `contractId` (path): ID do contrato a ser bloqueado (obrigatório, string ou integer dependendo do sistema)

## Corpo da Requisição
Não requer corpo adicional, ou opcionalmente:
```json
{
  "reason": "Motivo do bloqueio (opcional)",
}
```

## Resposta de Sucesso
- Status: 200 OK
- Corpo:
```json
{
  "success": true,
  "message": "Contrato bloqueado com sucesso",
  "contractId": "{contractId}",
  "status": "blocked"
}
```

## Resposta de Erro
- Status: 400 Bad Request (se contractId inválido)
- Status: 404 Not Found (se contrato não encontrado)
- Status: 500 Internal Server Error (erro interno)

## Autenticação
Requer autenticação especifica de usuario integrador.

## Notas
- Esta rota é independente da lógica de desbloqueio por confiança.
- O bloqueio é imediato e não conta para limites mensais.