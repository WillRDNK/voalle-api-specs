# Rota de Desbloqueio de Contrato

## Descrição
Esta rota permite desbloquear um contrato de forma independente, sem seguir as regras de negócio de desbloqueio por confiança ou quantidade mensal de desbloqueios.

## Endpoint
`POST /api/contracts/{contractId}/unblock`

## Parâmetros
- `contractId` (path): ID do contrato a ser desbloqueado (obrigatório, string ou integer dependendo do sistema)

## Corpo da Requisição
Não requer corpo adicional, ou opcionalmente:
```json
{
  "reason": "Motivo do desbloqueio (opcional)",
}
```

## Resposta de Sucesso
- Status: 200 OK
- Corpo:
```json
{
  "success": true,
  "message": "Contrato desbloqueado com sucesso",
  "contractId": "{contractId}",
  "status": "active"
}
```

## Resposta de Erro
- Status: 400 Bad Request (se contractId inválido)
- Status: 404 Not Found (se contrato não encontrado)
- Status: 409 Conflict (se contrato já está desbloqueado)
- Status: 500 Internal Server Error (erro interno)

## Autenticação
Requer autenticação especifica de usuario integrador.

## Notas
- Esta rota é independente da lógica de desbloqueio por confiança.
- O desbloqueio é imediato e não conta para limites mensais.