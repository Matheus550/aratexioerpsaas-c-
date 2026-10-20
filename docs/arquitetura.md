# Arquitetura proposta — ERP SaaS

**Status:** rascunho inicial, sujeito à aprovação do responsável pelo projeto.

## Objetivo
Definir uma base evolutiva para um ERP SaaS multiempresa, com isolamento de dados, regras de negócio testáveis e revisão humana das alterações.

## Tecnologias propostas
- Backend: C# / ASP.NET Core (.NET 8 ou superior).
- Banco: PostgreSQL.
- ORM e migrations: Entity Framework Core.
- Frontend: Flutter para Web e Desktop.
- Versionamento e revisão: GitHub, branches de trabalho e pull requests.

Estas escolhas são propostas iniciais; a implementação ainda não foi iniciada.

## Camadas propostas
- **ERP.Domain:** entidades, invariantes, regras e contratos de domínio sem dependências de infraestrutura.
- **ERP.Application:** casos de uso, validações, DTOs e interfaces de serviços.
- **ERP.Infrastructure:** persistência, EF Core, integrações e implementação de interfaces.
- **ERP.Api:** endpoints HTTP, autenticação, autorização e composição de dependências.
- **Frontend:** cliente Flutter consumindo contratos versionados da API.

Fluxo esperado de dependências: Api e Infrastructure dependem de Application/Domain conforme necessário; Domain não depende das demais camadas.

## Multiempresa
- Definir uma estratégia de tenant antes de criar tabelas.
- Toda operação com dados empresariais deve validar contexto da empresa e permissões.
- Índices únicos e consultas devem considerar o escopo do tenant quando aplicável.
- Testar acesso cruzado entre empresas e impedir vazamento de dados.
- Nunca confiar somente no identificador de empresa enviado pelo frontend.

## Módulos candidatos (ordem ainda não aprovada)
1. Empresas e identidade.
2. Papéis, permissões e usuários.
3. Pessoas: clientes, fornecedores, colaboradores e vendedores.
4. Produtos e estoque.
5. Caixa, vendas e pagamentos.
6. Contas a receber e a pagar.
7. Relatórios e auditoria.

## Princípios de implementação
- Transações consistentes em vendas, estoque e financeiro.
- Cancelamentos e estornos com trilha de auditoria.
- Migrations revisadas, testadas e executadas somente com autorização.
- Testes unitários e de integração antes do merge.
- Segredos fora do repositório; privilégios mínimos por ambiente.
- Alterações propostas em branches separadas, sem merge automático.

## Pendências arquiteturais
- Confirmar estratégia de autenticação e autorização.
- Escolher modelo de isolamento multiempresa.
- Definir requisitos de emissão fiscal, integração com pagamentos e auditoria.
- Definir estratégia de deploy, observabilidade, backup e recuperação.
- Validar requisitos não funcionais e volume esperado de usuários.

Nenhuma destas pendências deve ser tratada como decisão tomada.
