# Requisitos iniciais — ERP SaaS

**Status:** levantamento preliminar; requisitos candidatos, não aprovados para implementação.

## Visão
ERP SaaS multiempresa com cadastros, estoque, vendas, caixa, financeiro e relatórios.

## Papéis candidatos
- Administrador da plataforma (escopo global controlado).
- Administrador da empresa (escopo do próprio tenant).
- Usuário da empresa com papéis e permissões atribuídos.
A matriz exata de permissões ainda precisa ser aprovada.

## Requisitos funcionais candidatos
- **RF-001 — Empresas:** cadastrar, consultar, editar e ativar/desativar empresas; validar identificadores e impedir duplicidade conforme política a definir. Somente perfis autorizados podem administrar empresas.
- **RF-002 — Usuários e permissões:** cadastrar/convidar usuários, associar empresas e papéis, conceder/revogar permissões; operações negadas devem retornar erro de autorização.
- **RF-003 — Pessoas:** cadastrar, consultar e atualizar pessoas com papéis de cliente, fornecedor, colaborador e vendedor; definir unicidade por tenant.
- **RF-004 — Produtos e estoque:** cadastrar produtos, consultar saldo e registrar entradas/saídas com rastreabilidade.
- **RF-005 — Vendas:** registrar venda e itens, calcular totais, validar pagamento e manter consistência de estoque.
- **RF-006 — Financeiro:** gerar títulos a receber/pagar e registrar baixas totais ou parciais sem perder saldo residual.
- **RF-007 — Caixa:** abrir/fechar caixa e registrar entradas/saídas vinculadas à origem.
- **RF-008 — Cancelamento:** cancelar venda com reversão consistente de estoque e lançamentos financeiros, preservando trilha de auditoria.
- **RF-009 — Relatórios:** consultar relatórios por empresa e período, respeitando permissões.
- **RF-010 — Auditoria:** registrar ator, empresa, instante, operação e referência de eventos críticos.

## Requisitos não funcionais candidatos
- **RNF-001:** impedir leitura e alteração cruzada entre tenants.
- **RNF-002:** exigir autenticação e autorização no servidor, com privilégio mínimo.
- **RNF-003:** manter credenciais e dados sensíveis protegidos.
- **RNF-004:** preservar integridade transacional, inclusive sob falhas e concorrência.
- **RNF-005:** exigir testes automatizados, PR e revisão humana.
- **RNF-006:** definir e testar backup, recuperação e observabilidade.

## Critérios de aceite iniciais (exemplos para refinamento)
- **RF-001:** CNPJ inválido é rejeitado; duplicidade é bloqueada conforme regra aprovada; usuário sem permissão não cria/edita empresas; desativação não apaga histórico.
- **RF-002 / RNF-002:** operação sem autenticação é negada; usuário autenticado sem permissão recebe resposta de acesso negado; revogação de permissão impede operações posteriores.
- **RNF-001:** usuário de empresa A não consegue consultar, editar, exportar ou inferir dados da empresa B manipulando IDs.
- **RF-006:** pagamento parcial reduz saldo aberto pelo valor efetivamente recebido; pagamentos maiores que o saldo seguem regra explícita a definir.
- **RF-008:** cancelamento não deixa estoque ou financeiro divergentes, inclusive se uma etapa falhar.

## Proposta de MVP (ainda não aprovada)
**Fase 1:** empresas, identidade, usuários, papéis/permissões, pessoas e produtos básicos; autenticação, autorização e isolamento testados.
**Fase 2:** estoque, venda simples, caixa e contas a receber com pagamento parcial e cancelamento.
**Depois:** contas a pagar, relatórios avançados, integrações fiscais e automações, sujeitos à priorização.

A fase 1 deve ser validada como MVP mínimo útil; a proposta não afirma que ela seja suficiente para operação comercial.

## Regras de negócio pendentes
- Unicidade de CPF/CNPJ e produtos por empresa.
- Modelo de tenant, associação usuário-empresa e troca de empresa ativa.
- Venda a prazo, crédito, parcelamento, recebimento parcial, troco e estornos.
- Fiscalidade, emissão de documentos e regime tributário.
- Critérios de exclusão lógica, retenção de dados e auditoria.

## Fora do escopo desta PR
Implementar API, frontend, migrations, banco de dados, workflows ou deploy.

## Próxima validação com o responsável
Aprovar escopo do MVP, perfis, matriz de permissões e estratégia de isolamento antes da primeira implementação.
