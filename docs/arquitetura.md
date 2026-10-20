# Arquitetura proposta — ERP SaaS

**Status:** rascunho; escolhas pendentes de aprovação técnica. Nenhuma implementação autorizada.

## Objetivo
Definir uma base evolutiva para um ERP SaaS multiempresa, com isolamento de dados, regras de negócio testáveis e revisão humana.

## Stack proposta
- C# / ASP.NET Core (.NET 8 ou superior; versão exata a decidir).
- PostgreSQL, Entity Framework Core e migrations revisadas.
- Flutter Web/Desktop.
- GitHub, branches por tarefa e pull requests.

## Projetos e direção de dependências
- **ERP.Domain:** entidades, objetos de valor e invariantes; não referencia Application, Infrastructure ou Api.
- **ERP.Application:** casos de uso, DTOs, contratos/portas e validações; referencia Domain, não Infrastructure.
- **ERP.Infrastructure:** implementa contratos da Application, persistência EF Core e integrações; referencia Application/Domain.
- **ERP.Api:** endpoints, autenticação, autorização e composição de dependências; referencia Application e Infrastructure na composição.
- **Frontend:** consome contratos HTTP versionados; não acessa diretamente o banco.

As regras de negócio devem ficar no Domain/Application, nunca em controllers ou widgets. Dependências externas são substituíveis por interfaces nas camadas internas.

## Identidade e autorização (pendente: ADR-005)
- Distinguir administrador da plataforma, administrador da empresa e usuários de cada empresa.
- Autenticar a identidade e validar autorização por operação no backend; ocultar botões no frontend não é controle de acesso.
- Definir associação usuário-empresa, seleção de empresa ativa e políticas de acesso antes de implementar endpoints.
- Negar por padrão operações sem permissão; auditar operações críticas.
- Avaliar ASP.NET Core Identity e provedores OIDC sem decidir prematuramente.

## Multiempresa (pendente: ADR-003)
Alternativas: banco por empresa, schema por empresa ou tabelas compartilhadas com tenant_id e controles complementares. A decisão deve considerar custo, escala, migrações, backup, isolamento e operação.

Requisitos independentes da alternativa:
- O tenant deve ser derivado de contexto autenticado/autorizado no servidor; não confiar apenas no EmpresaId recebido do cliente.
- Escopo de empresa obrigatório em consultas, gravações e índices únicos pertinentes.
- Validar a associação do usuário ao tenant e evitar acesso cruzado por IDs manipulados.
- Testar leituras, escritas, exportações, relatórios, jobs e operações administrativas entre tenants.
- Considerar controles adicionais no PostgreSQL, como Row-Level Security, após avaliar sua adequação; não substituir testes de autorização.

## Módulos candidatos (ordem ainda não aprovada)
1. Empresas, identidade, papéis e permissões.
2. Pessoas: clientes, fornecedores, colaboradores e vendedores.
3. Produtos e estoque.
4. Vendas, pagamentos e caixa.
5. Contas a receber e a pagar.
6. Relatórios e auditoria.

## Integridade e operação
- Usar transações consistentes nas operações de estoque, venda e financeiro.
- Cancelamentos devem registrar reversões/estornos rastreáveis; não apagar histórico financeiro indiscriminadamente.
- Segredos fora do repositório; privilégios mínimos, backups e restauração testada.
- Testes unitários, integração, autorização e isolamento multiempresa antes de merge.
- Migrations e deploys exigem revisão e autorização separadas.

## Questões em aberto
- Estratégia de tenant (ADR-003) e autenticação (ADR-005).
- MVP e primeira jornada ponta a ponta.
- Requisitos fiscais, emissão de documentos e integrações.
- Escala, disponibilidade, observabilidade, hospedagem e recuperação.
- Política de versionamento de API e compatibilidade com clientes Flutter.

As propostas acima não são decisões finais nem autorização para criar código.
