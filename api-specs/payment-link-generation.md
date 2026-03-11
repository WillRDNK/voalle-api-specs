# Especificação de Geração de Link de Pagamento via Gateway Finee e Webhook de Confirmação

## Descrição Geral
Esta funcionalidade permite gerar links de pagamento para cobranças específicas (ex: recarga de MVNO) utilizando o gateway de pagamentos próprio da Voalle, o Finee. O ERP Voalle disponibiliza o checkout, e após a confirmação do pagamento, dispara um webhook para informar o recebimento. O valor é creditado apenas após confirmação, e o evento é registrado no contrato do cliente.

## Caso de Uso: Recarga de MVNO
- O cliente solicita recarga de crédito para seu plano MVNO.
- O sistema solicita ao ERP Voalle a geração de um link de checkout via Finee.
- O cliente paga diretamente no gateway da Voalle.
- Após pagamento confirmado, o ERP Voalle dispara webhook, creditando o valor e registrando o evento no contrato.

## Fluxo de Integração

### 1. Solicitação de Geração do Link de Pagamento
- **Método**: POST
- **Endpoint**: `/api/payments/generate-checkout` (API do ERP Voalle)
- **Parâmetros de Entrada**:
  ```json
  {
    "contractId": "ID do contrato (obrigatório)",
    "amount": "Valor da cobrança em centavos (ex: 5000 para R$50,00)",
    "description": "Descrição da cobrança (ex: 'Recarga MVNO - R$50,00')",
    "metadata": {
      "type": "recarga_mvno",
      "plan": "Nome do plano",
      "creditAmount": "Quantidade de crédito a ser adicionada"
    },
    "successUrl": "URL para redirecionar após pagamento bem-sucedido (opcional)",
    "cancelUrl": "URL para redirecionar se cancelado (opcional)"
  }
  ```
- **Resposta**:
  ```json
  {
    "checkoutUrl": "https://checkout.voalle.com/Finee/pay/abc123",
    "paymentId": "ID único da cobrança gerado pelo Finee",
    "expiresAt": "Data de expiração do link"
  }
  ```

### 2. Webhook de Confirmação de Pagamento
- **Método**: POST
- **Endpoint**: `/webhooks/voalle-payment-confirmation` (nosso endpoint para receber o webhook do ERP Voalle)
- **Cabeçalhos**: Incluir token de autenticação fornecido pela Voalle (ex: Authorization: Bearer <token>).
- **Corpo da Requisição**:
  ```json
  {
    "event": "payment.confirmed",
    "paymentId": "ID da cobrança",
    "contractId": "ID do contrato",
    "amount": 5000,
    "status": "paid",
    "metadata": {
      "type": "recarga_mvno"
    },
    "paidAt": "2023-10-01T12:00:00Z"
  }
  ```
- **Processamento**:
  - Verificar token de autenticação.
  - Confirmar que o `contractId` existe.
  - Registrar evento de "Pagamento Recebido" no contrato usando a rota `/api/contracts/{contractId}/events`.
  - Creditar o valor no saldo do cliente/MVNO.
  - Enviar notificação ou atualizar status.

## Requisitos Técnicos
- **Gateway Finee**: Utilizar o checkout fornecido pela Voalle, sem integração externa.
- **Segurança**: Webhooks com token de autenticação para validar origem.
- **Idempotência**: Garantir que webhooks duplicados não processem pagamentos múltiplas vezes (usar paymentId como chave).
- **Registro**: Todo pagamento confirmado gera um evento no contrato com tipo "Pagamento Recebido".
- **Fallback**: Em caso de falha no webhook, consultar status via API do ERP Voalle.

## Benefícios
- Integração direta com o ERP Voalle.
- Crédito apenas após confirmação oficial.
- Histórico centralizado no contrato.
- Suporte seguro para recargas de MVNO.
- **Flexibilidade para Outros Serviços**: Esta funcionalidade permite que a empresa disponibilize qualquer tipo de serviço unitário (recargas, adesões, complementos, etc.) com pagamento seguro e registro automático no ERP.
- **Centralização de Dados**: Todos os eventos de pagamento e transações ficam registrados no contrato, mantendo histórico completo e facilitando auditorias e análises.

## Notas
- Coordenar com a equipe da Voalle para configurar o webhook e obter credenciais.
- Testar em ambiente de homologação.
- Adaptar URLs e campos conforme documentação oficial do Finee.
- Usar o campo `metadata.type` para diferençar tipos de serviços (recarga_mvno, adésão_plano, complemento, etc).