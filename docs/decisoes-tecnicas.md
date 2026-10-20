# Registro de decisões técnicas (ADRs)

**Status:** decisões pendentes. Este documento registra propostas, não aprovações automáticas.

## ADR-001 — Stack inicial
- **Proposta:** ASP.NET Core (.NET 8+), PostgreSQL, EF Core e Flutter Web/Desktop.
- **Motivo:** separar API, persistência e clientes; permitir testes e evolução.
- **Status:** proposta; validar versão LTS adotada e restrições de implantação.

## ADR-002 — Organização do backend
- **Proposta:** Clean Architecture com Domain, Application, Infrastructure e Api.
- **Consequência:** dependências orientadas para o domínio e contratos explícitos.
- **Status:** proposta.

## ADR-003 — Isolamento multiempresa
- **Alternativas:** banco por empresa; schema por empresa; tabelas compartilhadas com tenant_id e controles complementares.
- **Critérios:** segurança, custo, operação, backup, migrações e escala.
- **Status:** pendente; nenhuma alternativa selecionada.

## ADR-004 — Fluxo de desenvolvimento assistido por IA
- **Proposta:** agente arquiteto consultivo; futuras implementações somente após aprovação específica; branches por tarefa; pull requests e revisão humana.
- **Restrições:** sem merge automático, sem acesso irrestrito à produção e sem segredos no repositório.
- **Status:** proposta operacional; proteções de branch ainda precisam ser configuradas.

## ADR-005 — Identidade e autorização
- **Alternativas:** ASP.NET Core Identity, provedor externo compatível com OIDC ou outra solução justificada.
- **Status:** pendente.

## Processo de decisão
1. Agente apresenta contexto, alternativas, riscos e recomendação.
2. Responsável aprova ou pede ajustes.
3. Decisão aprovada recebe data, motivação e consequências neste registro.
4. Implementação é autorizada separadamente e revisada via pull request.
