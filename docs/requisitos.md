# Requisitos iniciais — ERP SaaS

**Status:** levantamento preliminar. Este documento não autoriza implementação.

## Visão
Construir um ERP SaaS multiempresa com cadastros, estoque, vendas, caixa, financeiro e relatórios.

## Perfis e acesso (propostos)
- Administrador da plataforma.
- Administrador de empresa.
- Usuário com papéis e permissões configuráveis.

## Requisitos funcionais candidatos
- **RF-001:** cadastrar e administrar empresas, conforme permissões.
- **RF-002:** cadastrar usuários e vincular papéis/permissões.
- **RF-003:** cadastrar pessoas e classificá-las como clientes, fornecedores, colaboradores ou vendedores.
- **RF-004:** cadastrar produtos e controlar movimentações de estoque.
- **RF-005:** registrar vendas com itens e formas de pagamento.
- **RF-006:** registrar recebimentos e pagamentos, inclusive parciais.
- **RF-007:** controlar movimentações de caixa.
- **RF-008:** cancelar vendas com tratamento consistente de estoque e financeiro.
- **RF-009:** emitir relatórios operacionais e gerenciais.
- **RF-010:** manter trilha de auditoria para operações críticas.

## Requisitos não funcionais candidatos
- **RNF-001:** impedir acesso a dados de outra empresa.
- **RNF-002:** autenticar usuários e autorizar operações por permissão.
- **RNF-003:** proteger credenciais e dados sensíveis.
- **RNF-004:** garantir consistência transacional em operações críticas.
- **RNF-005:** possuir testes automatizados e revisão humana de mudanças.
- **RNF-006:** prever backup, recuperação e observabilidade.

## Regras de negócio a validar
- Venda a prazo gera obrigação no contas a receber.
- Pagamento parcial reduz saldo aberto sem duplicar receita.
- Cancelamento de venda exige reversão coerente de estoque e movimentos financeiros.
- Registros financeiros precisam manter rastreabilidade mesmo após estornos.
- Unicidade de cadastros deve considerar o contexto empresarial quando aplicável.

## Critérios de aceite da primeira entrega técnica (a definir)
- Contratos e validações revisados.
- Testes de permissões e isolamento multiempresa.
- Testes de sucesso, erro e concorrência das operações relevantes.
- Nenhuma migração ou deploy em produção sem autorização.

## Fora do escopo desta etapa
Implementação de API, frontend, banco de dados, workflows e deploy.

## Questões abertas
- Qual será o MVP?
- Quais perfis e permissões serão necessários?
- Quais exigências fiscais e integrações serão atendidas primeiro?
- Qual será o modelo de cobrança e contratação SaaS?
- Qual o modelo de tenant e a estratégia de hospedagem?
