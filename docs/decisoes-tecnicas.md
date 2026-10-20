# Registro de decisões técnicas (ADRs)

**Status geral:** propostas para análise. Nenhuma ADR foi aprovada nesta PR.

## Convenção de ADR
Cada decisão deve registrar: identificador, título, contexto, alternativas, recomendação, riscos, consequências, status, responsável e data da decisão. Status possíveis: proposta, aprovada, rejeitada ou substituída. A data só deve ser preenchida quando a decisão ocorrer; não inventar aprovações.

## ADR-001 — Stack inicial
- **Contexto:** ERP SaaS com API, persistência e clientes Web/Desktop.
- **Alternativas:** stack C#/.NET + Flutter; outras stacks exigiriam avaliação específica.
- **Recomendação:** ASP.NET Core (.NET 8+), PostgreSQL, EF Core e Flutter Web/Desktop.
- **Riscos/consequências:** manutenção de duas linguagens; verificar versão .NET com suporte e capacidade da equipe.
- **Status:** proposta.
- **Responsável/data:** pendentes.

## ADR-002 — Organização do backend
- **Contexto:** reduzir acoplamento de regras a banco e HTTP.
- **Alternativas:** arquitetura em camadas tradicional; Clean Architecture.
- **Recomendação:** Domain, Application, Infrastructure e Api com dependências voltadas para o domínio.
- **Riscos/consequências:** mais projetos e abstrações; evitar complexidade sem necessidade.
- **Status:** proposta.
- **Responsável/data:** pendentes.

## ADR-003 — Isolamento multiempresa
- **Contexto:** clientes distintos compartilharão uma plataforma SaaS.
- **Alternativas:** banco por empresa; schema por empresa; tabelas compartilhadas com tenant_id e controles adicionais.
- **Critérios:** segurança, custo, escalabilidade, backup/restauração, operação e migrações.
- **Recomendação:** pendente de comparação e validação.
- **Riscos/consequências:** vazamento entre tenants se consultas, permissões ou jobs não aplicarem isolamento corretamente.
- **Status:** proposta em avaliação, sem alternativa selecionada.
- **Responsável/data:** pendentes.

## ADR-004 — Fluxo de desenvolvimento supervisionado por IA
- **Contexto:** vários agentes poderão propor e implementar mudanças.
- **Alternativas:** alterações diretas; branches e PRs com revisão humana.
- **Recomendação:** agente arquiteto consultivo, autorização por escopo e nível, branches por tarefa, testes e PRs; merge/deploy com autorização separada.
- **Riscos/consequências:** instruções de agente não garantem bloqueio técnico; configurar permissões e proteção de branch.
- **Status:** proposta operacional; proteções ainda não configuradas.
- **Responsável/data:** pendentes.

## ADR-005 — Identidade e autorização
- **Contexto:** usuários podem pertencer a empresas com diferentes papéis.
- **Alternativas:** ASP.NET Core Identity; provedor externo OIDC; outra solução justificada.
- **Recomendação:** avaliar integração com políticas de autorização por tenant e operação antes da escolha.
- **Riscos/consequências:** elevação de privilégio, sessão em tenant errado, revogação ineficaz.
- **Status:** proposta em avaliação.
- **Responsável/data:** pendentes.

## Processo de aprovação
1. Vincular a ADR aos IDs RF/RNF relevantes.
2. Agente apresenta alternativas, trade-offs, impactos e testes.
3. Responsável aprova ou rejeita explicitamente a decisão.
4. Registrar responsável, data, motivação e consequências.
5. Autorizar implementação separadamente, em branch e PR.
6. Exigir outra autorização para merge, migrations e deploy.

Nenhuma proposta escrita aqui equivale à aprovação da arquitetura ou da implementação.
