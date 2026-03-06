# Minhas Entregas

Registro de entregas e conquistas para avaliações de desempenho.

Execute `/entrega` para registrar uma nova entrega.

---

## 2025-H1 (Janeiro - Junho 2025)

_Nenhuma entrega registrada neste ciclo._

---

## 2025-H2 (Julho - Dezembro 2025)

_Nenhuma entrega registrada neste ciclo._

---

## 2026-H1 (Janeiro - Junho 2026)

### Reestruturação de Permissionamento AWS - Conta Leve
**Data:** 2026-02-06
**Ref:** AP-1302

**Contexto:** A conta AWS da área de Lending operava com permissões excessivas, incluindo usuário de deploy com acesso root, gerando riscos de segurança, compliance e dificuldades de auditoria.

**O que fiz:**
- Criei repositório centralizado (`loans.iam`) para gerenciar políticas e roles IAM de toda a área de Lending
- Reestruturei roles e policies seguindo o princípio do menor privilégio
- Coordenei com o time de Infra Sec a migração dos perfis de acesso dos engenheiros
- Desenvolvi documentação completa com guia de migração para autonomia dos times
- Liderei o planejamento de rollout junto aos times de Lending (Vendas InApp, OutApp, EP e Pós Vendas)
- Mapeei todas as permissões necessárias para o usuário de deploy, viabilizando a remoção do acesso root
- Executei a migração completa em todos os repositórios da área: com os times sem capacidade de priorizar, absorvi o escopo e realizei as migrações nos 7 repositórios restantes (além do `loan-core` já migrado como PoC), totalizando 8 serviços migrados
- Realizei a limpeza pós-migração: removi políticas e roles obsoletas de todos os repositórios após a adoção das roles unificadas, eliminando o legado e garantindo que a estrutura antiga não permanecesse como tech debt

**Impacto:**
- Negócio: Adequação a requisitos de compliance e auditoria; redução significativa de risco de segurança com eliminação de acesso root; migração concluída em 100% dos serviços da área de Lending
- Técnico:
  - **Antes:** ~157 roles individuais espalhadas em 8 repositórios, cada lambda/task com sua própria role e policies duplicadas
  - **Depois:** 14 roles especializadas e 114 policy documents centralizados em repositório único, cobrindo 8 serviços migrados — redução de 91% no número de roles com políticas granulares seguindo o princípio do menor privilégio
  - Melhoria na rastreabilidade de ações e estrutura de IAM organizada para toda a área

**Competências demonstradas (L5):**
- **Autonomia & Planejamento:** Naveguei entre 5 times diferentes (Infra Sec + 4 times de Lending) para resolver problema complexo de segurança, criando planejamento de migração coordenado; ao identificar que os times não conseguiriam priorizar, absorvi o escopo de execução e entreguei a migração completa por conta própria
- **Técnico & Qualidade:** Antecipei riscos de segurança e compliance, propondo e executando solução que mitiga vulnerabilidades críticas (acesso root) em toda a área
- **Influência & Liderança:** Garantia de entrega mesmo sob restrições de capacidade dos times — assumiu ownership total do problema até a conclusão; documentação e tech talk garantiram conhecimento disseminado para manutenção futura
- **Processos & Métricas:** Criei e implementei processo padronizado de gestão de IAM que impacta múltiplas equipes da área de Lending
- **Colaboração & Comunidade:** Organizei Tech Talk para disseminar conhecimento entre os times de Lending, garantindo alinhamento e capacidade de evolução autônoma

**Colaboração:** Infra Sec, Vendas InApp, Vendas OutApp, Vendas EP, Pós Vendas

**Visibilidade:**
- Tech Talk (2026-02-09): Apresentação para 2 ICs de cada time de Lending sobre o trabalho de reestruturação de permissionamento e próximos passos para conclusão
  - Participantes: ~8 engenheiros (2 por time)
  - Objetivo: Compartilhar conhecimento e alinhar o que cada time precisa fazer para concluir a migração
  - Gravação e transcrição: https://docs.google.com/document/d/1N8StEih0dLsvYvoWQV7iL8e1WEfTdGkXqs40llezbMw/edit?tab=t.jup1mjnpfz46

**Evidências:**
- Repositório centralizado: https://github.com/neon/loans.iam
- Guia de migração: https://github.com/neon/loans.iam/blob/feat/centralize-iam/docs/MIGRATION_GUIDE.md
- PR de estrutura: https://github.com/neon/loans.iam/pull/1
- PRs de migração e limpeza (14 PRs em 7 repositórios):
  - loans.loan-core: https://github.com/neon/loans.loan-core/pull/2042, https://github.com/neon/loans.loan-core/pull/2040, https://github.com/neon/loans.loan-core/pull/2089, https://github.com/neon/loans.loan-core/pull/2087
  - loans.banking-core: https://github.com/neon/loans.banking-core/pull/123, https://github.com/neon/loans.banking-core/pull/120, https://github.com/neon/loans.banking-core/pull/125
  - loans.hr-core: https://github.com/neon/loans.hr-core/pull/221, https://github.com/neon/loans.hr-core/pull/217
  - loans.credit-engine: https://github.com/neon/loans.credit-engine/pull/319, https://github.com/neon/loans.credit-engine/pull/315
  - loans.notification-core: https://github.com/neon/loans.notification-core/pull/65, https://github.com/neon/loans.notification-core/pull/62
  - loans.backoffice-core: https://github.com/neon/loans.backoffice-core/pull/218, https://github.com/neon/loans.backoffice-core/pull/221
  - loans.database-core: https://github.com/neon/loans.database-core/pull/820

---

### Documentação de Gestão de Certificados mTLS - Dataprev
**Data:** 2026-02-09

**Contexto:** A integração com Dataprev (e-Consignado) utiliza certificados mTLS que precisam ser renovados periodicamente. O conhecimento sobre o processo de atualização estava concentrado em uma pessoa que deixou a empresa sem documentar o procedimento, criando risco operacional para 3 aplicações críticas (dataprevproxy, dataprevproxy-inss, dataprevproxy-tombamento).

**O que fiz:**
- Documentei todo o processo de gestão de certificados mTLS no README da aplicação
- Detalhei o passo a passo: extração de certificado/chave do arquivo PFX, codificação base64, atualização no Vault
- Mapeei os paths do Vault para ambientes HML e PRD
- Identifiquei e documentei que 3 aplicações compartilham o mesmo certificado
- Compartilhei a documentação com times de Infra/Sec, Redes e demais times de Lending
- Criei script de automação para conversão .pfx → base64, eliminando etapas manuais propensas a erro
- Executei a renovação do certificado em HML e PRD antes do vencimento (2026-02-28), validando na prática o processo documentado

**Impacto:**
- Negócio: Mitigação de risco de indisponibilidade total da integração com Dataprev em caso de expiração de certificado; renovação executada com sucesso em HML e PRD antes do vencimento (2026-02-28)
- Técnico: Eliminação de conhecimento institucional concentrado (bus factor); redução de horas de investigação em cada renovação de certificado; autonomia para qualquer engenheiro executar o processo; script de automação elimina a etapa mais sujeita a erro humano (conversão .pfx → base64)

**Competências demonstradas (L5):**
- **Técnico & Qualidade:** Antecipei risco operacional, documentei processo crítico antes que se tornasse incidente e criei tooling de automação para eliminar a etapa mais sujeita a erros humanos — mitigando potencial indisponibilidade
- **Influência & Liderança:** Elevei o conhecimento técnico da área ao transformar conhecimento tácito em documentação acessível a todos, validada em produção na primeira renovação real
- **Processos & Métricas:** Criei processo padronizado e automatizado onde não existia, aumentando a efetividade operacional de múltiplas equipes

**Colaboração:** Infra/Sec, Redes, times de Lending

**Evidências:**
- Documentação: https://github.com/neon/loans.e-consignado/tree/main/src/econsignado/dataprev_proxy#certificate-management
- Script de automação e renovação do certificado: https://github.com/neon/loans.e-consignado/pull/1205

---

### Planejamento e Documentação de Ações para Redução de Taxa de Erro - Novo Consignado
**Data:** 2026-02-11
**Ref:** NC-2594 (Epic), NC-2595, NC-2604, NC-2578

**Contexto:** A área de Lending tinha como KPI de engenharia reduzir a taxa de erro das aplicações para abaixo de 0.10% e o p99 de latência para <= 1.0s. Os serviços do Novo Consignado (loans.e-consignado-bffmobile e dependências) apresentavam error rate acima da meta, impactando a jornada de vendas e a experiência do cliente.

**O que fiz:**
- Realizei análise profunda de observabilidade utilizando Datadog (logs, traces, métricas APM) para identificar causas raiz dos erros
- Mapeei toda a cadeia de dependências dos endpoints críticos (POST /simulation, GET /details-unified)
- Identifiquei as causas raiz principais:
  - **Dataprev (serviço externo):** responsável por ~50% dos erros (503, timeout, indisponibilidade)
  - **Timeout de 99999 (~27h!) no DatabaseServiceFactory do loan-core:** permitia conexões penduradas indefinidamente, causando traces de 29s-301s
  - **Ausência de timeouts configurados no bffmobile:** requests sem proteção contra downstream lento
  - **Lambda timeouts:** configuração de 60s sem circuit breaker
- Categorizei e priorizei os erros por impacto (Crítico, Alto, Médio, Baixo) com dados quantitativos
- Documentei especificações técnicas (SPECs) para cada solução, incluindo:
  - SPEC-001: Módulo de resiliência (retry + circuit breaker) - impacto estimado de -87% em erros transientes
  - SPEC-002/004: Configuração de timeouts por endpoint
  - SPEC-003: Integração de resiliência nos services existentes
  - Especificação completa para escalabilidade horizontal do Dataprev Proxy via Redis (estado compartilhado, rate limiting distribuído)
- Criei plano de ação detalhado com impacto estimado de cada ação e métricas de sucesso

**Impacto:**
- Negócio: Mapeamento completo das causas de falha na jornada de vendas do Novo Consignado, possibilitando redução de ~50% nos erros com implementação das ações priorizadas
- Técnico:
  - Identificação de débito técnico crítico (timeout de 27h!) que passava despercebido
  - Documentação técnica detalhada que permite execução autônoma pelos times
  - Roadmap priorizado de melhorias cobrindo 3 repositórios (bffmobile, loan-core, database-core)
  - Especificação de arquitetura para escalabilidade horizontal do Dataprev Proxy

**Competências demonstradas (L5):**
- **Técnico & Qualidade:** Fiz leitura situacional dos KPIs de engenharia do período, alavancando análise de impacto para antecipar movimentos necessários. Avaliei trade-offs de soluções complexas (retry vs circuit breaker, escalabilidade via Redis) com plano de mitigação de riscos
- **Autonomia & Planejamento:** Naveguei entre múltiplas fontes de dados (Datadog, código, infraestrutura) e times para construir diagnóstico completo. Criei planejamento priorizado orientado às metas da empresa
- **Processos & Métricas:** Realizei diagnóstico profundo baseado em métricas (error rate, latência p50/p95/p99, categorização de erros) e defini indicadores de sucesso claros para acompanhamento
- **Influência & Liderança:** Documentação detalhada eleva conhecimento técnico do time e permite execução autônoma das melhorias

**Colaboração:** Time de Vendas Lending (análises específicas dos endpoints), cross-lending (Dataprev Proxy que serve todos os times)

**Evidências:**
- Epic: https://neonpagamentos.atlassian.net/browse/NC-2594
- Análise POST /simulation: https://neonpagamentos.atlassian.net/browse/NC-2595
- Análise GET /details-unified: https://neonpagamentos.atlassian.net/browse/NC-2604
- Spec Escalabilidade Dataprev Proxy: https://neonpagamentos.atlassian.net/browse/NC-2578

---

### Eliminação de Single Point of Failure no Dataprev Proxy
**Data:** 2026-02-14
**Ref:** NC-2578

**Contexto:** O dataprev-proxy processava ~218.620 requests/dia mas operava com apenas 1 pod devido a limitações arquiteturais críticas: token OAuth armazenado em memória local e rate limiting local. Essa arquitetura gerava 6.968 erros 503 em 15 dias (taxa global de 0.212%), com impacto severo no bidreader (1.055% error rate), comprometendo a disponibilidade e confiabilidade do serviço de e-Consignado.

**O que fiz:**
- Implementei infraestrutura Redis distribuída com cliente e dependências, permitindo estado compartilhado entre múltiplos pods
- Migrei armazenamento do token OAuth de memória local para Redis com prefixo isolado por variante (normal, inss, tombamento)
- Criei sistema de feature flags para deploy incremental e rollback seguro das mudanças
- Implementei timeout configurável via header (X-Proxy-Timeout) com validação e conversão para milissegundos, aumentando flexibilidade operacional
- Adicionei instrumentação automática do Redis para observabilidade e monitoramento
- Documentei especificação técnica completa e decisões arquiteturais para autonomia do time

**Impacto:**
- Negócio: Eliminação efetiva do SPOF no serviço de e-Consignado; redução confirmada de +7.000 para apenas 3 erros 503/dia (-99,8% no total), com eliminação total de erros em 4 dos 5 serviços consumidores
- Técnico:
  - **Antes:** 1 pod único, impossibilidade de escalar horizontalmente, token OAuth perdido a cada deploy/restart
  - **Depois:** Serviço rodando com múltiplos pods com estado compartilhado via Redis, escalabilidade horizontal confirmada em produção, token OAuth persistido e resiliente a restarts
  - Observabilidade aprimorada com métricas automáticas do Redis
  - Base técnica para rate limiting distribuído futuro
- Resultados medidos pós-implementação (13-14/02/2026):

  | Serviço | 503s/dia (baseline) | 503s/dia (pós-impl) | Redução |
  |---|---|---|---|
  | loans.e-consignado-bidreader | 3.648 | 3 | -99,8% |
  | econsignado-employees-endpoint | 3.507 | 0 | -100% |
  | econsignado-proposals-endpoint | 16 | 0 | -100% |
  | proposal-events-endpoint | 15 | 0 | -100% |
  | finish-contract | 17 | 0 | -100% |
  | **TOTAL** | **+7.000** | **3** | **-99,8%** |

**Competências demonstradas (L5):**
- **Técnico & Qualidade:** Avaliei trade-offs arquiteturais complexos (Redis vs alternativas, feature flags vs deploy direto) e antecipei movimentos necessários para evitar degradação de serviço. Implementei solução que mitiga riscos críticos de disponibilidade
- **Autonomia & Planejamento:** Naveguei entre múltiplas áreas técnicas (infraestrutura Redis, OAuth, observabilidade, feature flags) para resolver problema arquitetural complexo que bloqueava escalabilidade do serviço
- **Processos & Métricas:** Realizei diagnóstico baseado em métricas do Datadog (error rate, distribuição de erros por serviço consumidor) para quantificar o problema e definir baseline para medição de sucesso pós-implementação
- **Influência & Liderança:** Documentação técnica detalhada eleva conhecimento do time sobre gestão de estado distribuído e permite evolução futura (rate limiting, observabilidade adicional)

**Colaboração:** Trabalho individual

**Evidências:**
- Card: https://neonpagamentos.atlassian.net/browse/NC-2578
- Especificação técnica: https://github.com/neon/loans.e-consignado/blob/main/docs/plans/nc-2578-redis-timeout/README.md
- Análise de baseline (métricas pré-implementação): https://github.com/neon/loans.e-consignado/blob/main/docs/metrics/nc-2578/baseline-collected.md
- PRs implementação:
  - Feature Flags: https://github.com/neon/loans.e-consignado/pull/1183
  - Timeout configurável: https://github.com/neon/loans.e-consignado/pull/1184
  - Redis Infrastructure: https://github.com/neon/loans.e-consignado/pull/1189
  - Token Store distribuído: https://github.com/neon/loans.e-consignado/pull/1192
- Notebook Datadog com resultados pós-implementação: https://app.datadoghq.com/notebook/13959161/nc-2578-%25E2%2580%2594-evid%25C3%25AAncia-redu%25C3%25A7%25C3%25A3o-de-erros-503-p%25C3%25B3s-redis-token-store _(link pode expirar — backup salvo em `evidencias/NC-2578-reducao-erros-503-pos-redis-token-store.pdf`)_

---

### Desativação de Ambientes de Dev/TST Obsoletos e Redução de Custo AWS
**Data:** 2026-02-25

**Contexto:** A conta AWS da área de Lending mantinha ambientes de desenvolvimento e remanescentes de TST inativos, gerando custo contínuo sem qualquer utilidade operacional.

**O que fiz:**
- Realizei levantamento dos maiores ofensores de custo na conta via CloudZero, identificando e categorizando os recursos obsoletos
- Desativei o ambiente de dev e recursos remanescentes do ambiente de TST que não estavam mais em uso
- Recursos eliminados:
  - **RDS** (database-core, loan-core, employee-core, metabase): ~$110/mês
  - **API Gateway** (loan-core, hr-core): ~$230/mês
  - **ECS**: ~$140/mês
  - **Load Balancer**: ~$80/mês

**Impacto:**
- Negócio: Redução estimada de **$500–$600/mês** (~16% do custo total da conta, que gira em torno de $3.000/mês)
- Técnico: Eliminação de ambientes sem uso que adicionavam complexidade operacional desnecessária; redução de superfície de atualização e gestão de infraestrutura

**Competências demonstradas (L5):**
- **Técnico & Qualidade:** Fiz leitura situacional dos custos da área, identifiquei recursos obsoletos com dados do CloudZero e antecipei a ação de desativação antes que o custo se tornasse ainda maior
- **Autonomia & Planejamento:** Naveguei de forma autônoma pelo inventário de infraestrutura da conta, priorizei e executei a limpeza orientado a impacto financeiro mensurável
- **Processos & Métricas:** Realizei diagnóstico baseado em métricas financeiras (CloudZero), quantificando o impacto por recurso e estimando a economia total — evidência para tomada de decisão orientada a dados

**Colaboração:** Trabalho individual

**Evidências:**
- Levantamento via CloudZero (evidência completa disponível após 1 mês de conta fechada)

---

### Redução de ~53% no P95 do Endpoint Compact Offer - Novo Consignado
**Data:** 2026-03-03
**Ref:** NC-2610

**Contexto:** O endpoint `compact offer` é um dos mais acessados na jornada do Novo Consignado (~300 mil requisições/dia), sendo responsável por direcionar o cliente para um dos fluxos disponíveis: Finalização, Revisão, Refinanciamento, Troca de Dívida ou New Loan. O p95 de resposta estava em ~1,5s, acima da meta de KPI de engenharia de latência da área.

**O que fiz:**
- Identifiquei que o endpoint realizava 3 chamadas HTTP separadas ao `database-core` para recuperar informações de tomada de decisão, gerando latência desnecessária
- Projetei e executei solução em 3 fases distribuídas em 3 repositórios distintos:
  - **Fase 1 — database-core:** Criei endpoint unificado `GET /api/v1/econsignado/offer-decision-data/{person_id}` que consolida as 3 chamadas em uma única requisição, usando `.only()` + `Prefetch` para minimizar overhead no banco de dados
  - **Fase 2 — database-service:** Implementei mixin `get_offer_decision_data` para expor o novo endpoint ao loan-core (versão 2.154.0)
  - **Fase 3 — loan-core:** Refatorei o `EConsignadoOfferDecisionService` com feature flag (`use_unified_offer_decision_endpoint`) para rollout gradual e seguro; corrigi bug identificado durante o rollout (crash por `UUID(None)` quando `person_id` não tinha usuário correspondente); removi feature flags após validação completa em produção; otimizei instâncias no `UserProductEventHelper` convertendo para singletons

**Impacto:**
- Negócio: 300 mil requisições/dia com melhoria perceptível de tempo de resposta; alinhamento com KPI de engenharia de latência da área; impacto em conversão ainda não mensurado
- Técnico: Redução de **~53% no p95** (1,5s → 700ms); redução de 3 chamadas HTTP para 1 por requisição ao `database-core`

**Competências demonstradas (L5):**
- **Técnico & Qualidade:** Fiz leitura situacional dos KPIs de engenharia do período, identifiquei o gargalo por análise de código e traces, e projetei solução multi-repositório com trade-offs bem avaliados — endpoint aditivo para zero breaking change, feature flag para rollout seguro, remoção de flags após validação em produção
- **Autonomia & Planejamento:** Planejei e executei de forma totalmente autônoma uma solução em 3 fases distribuída em 3 repositórios, incluindo estratégia de deploy incremental com feature flag e limpeza de código após rollout completo
- **Processos & Métricas:** Realizei diagnóstico baseado em métricas de latência (Datadog), quantifiquei o problema com baseline antes/depois e confirmei o resultado com evidência de observabilidade

**Colaboração:** Trabalho individual

**Evidências:**
- Card: https://neonpagamentos.atlassian.net/browse/NC-2610
- PRs:
  - database-core (Fase 1): https://github.com/neon/loans.database-core/pull/842
  - database-service (Fase 2): https://github.com/neon/loan.database-service/pull/125
  - loan-core (Fase 3): https://github.com/neon/loans.loan-core/pull/2116, https://github.com/neon/loans.loan-core/pull/2120, https://github.com/neon/loans.loan-core/pull/2122, https://github.com/neon/loans.loan-core/pull/2125
- Gráfico Datadog — p95 por versão no BFF (`loans.e-consignado-bffmobile`): `evidencias/NC-2610-p95-bff-por-versao.png`
  - `release-20260226` (antes): AVG 1,71s — `release-20260302` (após): AVG 0,79s / valor atual 0,74s
- Gráfico Datadog — latência multi-percentil no API Gateway (`GET /econsignado/...`, `api.somosleve.com.br`): `evidencias/NC-2610-latencia-api-gateway.png`
  - Queda visível em todos os percentis (p50→p99,9) após o deploy em produção
- Notebook Datadog com evidências pós-implementação: https://app.datadoghq.com/notebook/13997405/nc-2610-evidencia-reducao-de-53-no-p95-do-endpoint-compact-offer _(link pode expirar — backup salvo em `evidencias/NC-2610-p95-compact-offer.pdf`)_

---

### Automação de Execução de Migrations - database-core
**Data:** 2026-03-06
**Ref:** AI-593 (action item pós-crise)

**Contexto:** A execução de migrations no `database-core` era um processo totalmente manual, com dependência de pessoas específicas que detinham credenciais root do banco de dados. Além do risco de segurança, o processo gerava gargalo operacional e expunha a área a riscos em momentos críticos de deploy.

**O que fiz:**
- Implementei automação completa do ciclo de migrations no pipeline CI/CD (GitHub Actions) do `database-core`
- Ao fazer merge para `main`, após o job de `build-and-push`, um novo job verifica automaticamente se há migrations pendentes; caso contrário, o fluxo segue sem interrupção
- Se houver migrations, o pipeline dispara uma ECS task na conta AWS para executá-las, com step pendente de aprovação dos staffs antes de produção (mesmo fluxo de aprovação do deploy)
- Em homologação (QA), o processo ocorre automaticamente, sem necessidade de aprovação manual
- O deploy em produção só é liberado após a migration ser executada e validada em QA, garantindo sequenciamento seguro entre ambientes

**Impacto:**
- Negócio: Eliminação da dependência de pessoas específicas com credencial root para executar migrations; mitigação de risco operacional em deploys; qualquer staff autorizado pode aprovar e acompanhar o processo com total rastreabilidade
- Técnico: Remoção do acesso root manual ao banco de dados; processo padronizado, auditável e seguro; beneficia os 4 times que commitam no `database-core` sem necessidade de intervenção manual

**Competências demonstradas (L5):**
- **Técnico & Qualidade:** Antecipei risco operacional e de segurança identificado em crise anterior (AI-593), projetei e implementei solução automatizada com controle de aprovação, sequenciamento de ambientes (QA → PRD) e disparo de ECS task — eliminando pontos de falha humana sem comprometer a governança do processo
- **Autonomia & Planejamento:** Planejei e executei de forma autônoma solução que impacta múltiplas equipes da área, priorizando a entrega dentro do contexto de action item pós-crise
- **Processos & Métricas:** Criei processo padronizado e automatizado de execução de migrations que impacta positivamente mais de uma equipe — os 4 times que utilizam o `database-core` passam a ter um fluxo seguro, rastreável e sem dependência de pessoas

**Colaboração:** Trabalho individual — impacto cross para 4 times da área de Lending

**Evidências:**
- Jira (action item pós-crise): https://neonpagamentos.atlassian.net/browse/AI-593
- Esteira de exemplo: https://github.com/neon/loans.database-core/actions/runs/22728063143
- PR: https://github.com/neon/loans.database-core/pull/845
