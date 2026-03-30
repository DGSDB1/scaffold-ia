---
agent: "agent"
description: "Gera a estrutura completa de AI-Driven Development para qualquer projeto"
---

# Scaffold: Estrutura AI-Driven Development

Você é um engenheiro de software sênior especialista em AI-Driven Development, Prompt Engineering e Repository Instruction Design para GitHub Copilot.

## Objetivo

Criar a estrutura completa de **AI-Driven Development** para o projeto atual, gerando todos os arquivos de configuração, instruções, templates e workflows necessários para que o desenvolvimento assistido por IA seja maximamente eficaz.

## Etapa 1 — Análise do Projeto

Antes de gerar qualquer arquivo, analise o projeto atual para mapear:

### 1.1 Stack Tecnológica
- Linguagem principal (Java, TypeScript, Python, Go, etc.)
- Framework(s) (Spring Boot, Next.js, Django, etc.)
- Build tool (Maven, Gradle, npm, pip, etc.)
- Ferramentas de teste (JUnit, Jest, pytest, etc.)
- ORM / acesso a dados (JPA, Prisma, SQLAlchemy, etc.)
- Banco(s) de dados

### 1.2 Estrutura Existente
- Arquitetura do projeto (camadas, módulos, monolito, microsserviços)
- Estrutura de diretórios e pacotes
- Convenções de nomenclatura já em uso
- Documentação de engenharia existente (se houver)

### 1.3 Padrões Identificados
- Padrões de código recorrentes (injeção de dependência, DTOs, etc.)
- Estilo de testes (AAA, BDD, TDD)
- Convenções de API (REST, GraphQL, gRPC)
- Configurações de CI/CD existentes

### 1.4 Diagnóstico Operacional Local (obrigatório)
- Comandos reais de execução local por stack detectada (start/build/validate)
- Diferença entre runtime no PATH e runtime usado pelo build tool
- Dependências externas exigidas para startup (config server, DB, fila, cache, serviços internos, VPN/proxy)
- Mecanismos reais de configuração encontrados no projeto (`application*`, `bootstrap*`, `.env*`, arquivos de config por framework)
- Possíveis cenários de fallback local quando integrações externas estiverem indisponíveis

**Apresente um resumo da análise antes de prosseguir.**

## Etapa 2 — Gerar Estrutura

Após a análise, crie os seguintes diretórios e arquivos:

### 2.1 Diretório `.github/`

```
.github/
├── copilot-instructions.md              # Instruções globais (~100 linhas, enxuto)
├── README.md                            # Índice do diretório
├── copilot/                             # Guias técnicos de referência
│   ├── README.md
│   ├── ai-development.md               # Fluxo de trabalho com IA
│   ├── [stack]-standards.md             # Padrões da stack (ex: java-spring-standards.md)
│   ├── rest-api-guidelines.md           # Se aplicável: diretrizes REST
│   ├── [stack]-code.instructions.md     # Instruction file com applyTo para código
│   └── testing.instructions.md          # Instruction file com applyTo para testes
├── prompts/                             # Prompt Files nativos do Copilot
│   ├── plan-task.prompt.md              # Fase 1: Planejamento
│   ├── implement-task.prompt.md         # Fase 2: Implementação
│   ├── validate-task.prompt.md          # Fase 3: Validação
│   ├── review-code.prompt.md            # Code Review
│   └── implement-local-environment.prompt.md   # Setup local pós-scaffold
└── rules/                               # Regras de engenharia
    ├── README.md
    ├── pull-request.md                  # Regras de PR e commits
    └── testing-practices.md             # Práticas de testes
```

### 2.2 Diretório `tasks/`

```
tasks/
├── README.md                            # Guia do workflow de tasks
├── templates/
│   ├── _task-template.md                # Template para features (14 seções)
│   └── _task-template-bugfix.md         # Template para bugs (19 seções)
├── examples/                            # Exemplo de task preenchida
├── backlog/
│   └── README.md
├── active/
│   └── README.md
└── done/
    └── README.md
```

### 2.3 Diretório `docs/`

```
docs/
├── architecture-onboarding.md          # Documento de arquitetura para onboarding
├── architecture-onboarding-summary.md  # Resumo executivo de arquitetura
└── developer-guide.md                  # Guia do desenvolvedor (first steps)
```

> Se `docs/architecture-onboarding.md`, `docs/architecture-onboarding-summary.md` ou `docs/developer-guide.md` já existirem, atualize-os ao invés de sobrescrever.

## Etapa 3 — Regras de Geração de Conteúdo

### `copilot-instructions.md` (Ponto de Entrada)
- **Máximo ~100 linhas** — regras essenciais e compactas
- caso ja exista um `copilot-instructions.md`, proponha um merge ao invés de sobrescrever
- Inclui: contexto do projeto, regras de nomenclatura, princípios de código, checklist
- Referencia os guias detalhados via tabela de links
- Referencia os Prompt Files para execução de tasks
- **NÃO** inclui exemplos de código (esses ficam nos guias detalhados)

### Instruction Files (`.instructions.md`)
- Usar frontmatter `applyTo` para aplicação automática por padrão de arquivo
- Máximo ~15 linhas — regras diretas e referências aos guias completos
- Um por tipo de arquivo relevante (código de produção, testes)

### Prompt Files (`.prompt.md`)
- Usar frontmatter `mode: "agent"` e `description`
- Cada prompt é autossuficiente — contém instruções completas para a fase
- Referenciam as diretrizes do projeto para consulta durante execução
- 5 prompts obrigatórios: plan-task, implement-task, validate-task, review-code, implement-local-environment
- `implement-local-environment.prompt.md` deve instruir explicitamente:
    - criação/atualização de `scripts/setup-local.ps1`, `scripts/run-local.ps1`, `scripts/validate-local.ps1`;
    - adaptação por stack (Java e não-Java), reaproveitando a detecção da Etapa 1;
    - atualização de `docs/LOCAL_SETUP.md` com seção **Exemplo validado de execução** contendo comandos reais:
        - comando de start local;
        - comando de validação local;
        - resultado esperado dos endpoints principais (ex.: health/openapi/swagger, quando aplicável).
    - validação de pelo menos 1 cenário funcional com execução real (não apenas comandos sugeridos).
    - documentação de cenário padrão e cenário fallback quando houver dependências externas opcionais.

### Guias Técnicos (`copilot/*.md`)
- Detalhados, com exemplos de código da stack do projeto
- `[stack]-standards.md` — padrões completos com exemplos bom/ruim
- `ai-development.md` — princípios de prompt engineering e workflow
- `rest-api-guidelines.md` — se o projeto tiver APIs REST

### Regras (`rules/*.md`)
- `pull-request.md` — convenções de branch, commits (Conventional Commits), tamanho de PR, checklist
- `testing-practices.md` — pirâmide de testes, padrão AAA, cobertura, flakiness

### Templates de Tasks (`tasks/templates/`)
- Feature template deve ser criado **exatamente** com o mesmo conteúdo e estrutura de `task_template/_task-template.md` (mesmos títulos, ordem, bullets e textos-base), sem variações, sem renomear seções e sem adicionar/remover seções.
- Bugfix template deve ser criado **exatamente** com o mesmo conteúdo e estrutura de `task_template/_task-template-bugfix.md` (mesmos títulos, ordem, bullets e textos-base), sem variações, sem renomear seções e sem adicionar/remover seções.

### `tasks/README.md`
- Documenta o workflow: `backlog/ → active/ → done/`
- Explica as 3 fases com IA via Prompt Files
- Inclui boas práticas e convenções de nomenclatura

### Documento de arquitetura para onboarding (`docs/architecture-onboarding.md`)
- Gerar ou atualizar com base na análise da Etapa 1.
- Deve conter:
    - **Contexto do serviço**: propósito, domínio de negócio e responsabilidades principais;
    - **Visão arquitetural**: tipo de arquitetura (monolito, microsserviço, etc.) e padrões utilizados (camadas, hexagonal, etc.);
    - **Componentes principais**: módulos, pacotes e responsabilidades;
    - **Mapa de integrações**: serviços externos, filas, bancos de dados, caches;
    - **Fluxo de dados**: sequência principal de uma requisição/evento ponta a ponta;
    - **Diagrama Mermaid de entidades**: mapa de entidades/tabelas centrais e seus relacionamentos;
    - **Diagrama Mermaid de fluxo**: fluxo ponta a ponta com componentes reais do projeto;
    - **Diagrama Mermaid de sequência**: `sequenceDiagram` com atores/sistemas reais e trocas principais;
    - **Stack tecnológica**: linguagem, frameworks, ferramentas e versões relevantes;
    - **Decisões arquiteturais relevantes**: ADRs ou decisões de design que não são óbvias.
- Linguagem: português brasileiro; nomes técnicos e de código em inglês.

### Resumo executivo de arquitetura (`docs/architecture-onboarding-summary.md`)
- Gerar ou atualizar uma versão resumida e operacional da arquitetura para leitura rápida.
- Deve conter:
    - **O que é o sistema**;
    - **Arquitetura em uma frase**;
    - **Mapa rápido das pastas**;
    - **Fluxo crítico de negócio (1 exemplo real)**;
    - **Persistência e integrações principais**;
    - **Riscos principais para mudanças**;
    - **Regras práticas para contribuir com segurança**;
    - **Arquivos para abrir primeiro**.
- Deve incluir obrigatoriamente:
    - 1 diagrama Mermaid de entidades centrais (versão compacta);
    - 1 diagrama Mermaid de fluxo crítico (versão compacta);
    - 1 diagrama Mermaid de sequência crítica (versão compacta).
- Linguagem: português brasileiro; nomes técnicos e de código em inglês.

### Guia do desenvolvedor (`docs/developer-guide.md`)
- Gerar ou atualizar com base na análise da Etapa 1.
- Deve conter:
    - **Primeiros passos**: pré-requisitos, configuração do ambiente local (referência para `docs/LOCAL_SETUP.md`);
    - **Estrutura do projeto**: mapeamento dos principais diretórios e pacotes;
    - **Fluxo de desenvolvimento**: como criar uma task, implementar, testar e abrir PR (referência aos Prompt Files);
    - **Convenções de código**: nomenclatura, formatação, idioma de classes/métodos/atributos vs. API;
    - **Estratégia de testes**: tipos de teste, como rodar, onde ficam;
    - **Dicas e armadilhas comuns**: padrões específicos do projeto que confundem newcomers;
    - **Links úteis**: repositórios relacionados, documentação externa, runbooks.
- Deve incluir obrigatoriamente:
    - 1 diagrama Mermaid de entidades/domínio para onboarding rápido;
    - 1 diagrama Mermaid de fluxo de implementação (request → use case → facade → testes/PR);
    - 1 diagrama Mermaid de sequência de implementação (task → código → validação → PR).
- Linguagem: português brasileiro; exemplos de código em inglês.

### Guia de setup local (`docs/LOCAL_SETUP.md`)
- Se o projeto expuser aplicação executável localmente, gerar ou atualizar `docs/LOCAL_SETUP.md`.
- O guia deve conter uma seção obrigatória **Exemplo validado de execução** com comandos e saídas esperadas.
- Para projetos sem API HTTP, substituir validação de endpoints por validação equivalente da stack.

## Etapa 3.1 — Padrão obrigatório de qualidade (anti-resumo)

Para evitar documentação superficial, aplique obrigatoriamente as regras abaixo:

- Não gerar documentos com texto genérico, placeholders ou listas curtas sem contexto do projeto.
- Sempre usar nomes reais de módulos/pacotes/entrypoints detectados na Etapa 1.
- Para cada documento, incluir exemplos concretos de fluxo (endpoint/use case/job/evento) com caminho de arquivos.
- Se não houver informação suficiente no repositório, registrar explicitamente "Não identificado" e listar onde foi feita a busca.
- Priorizar atualização por merge quando já existir conteúdo relevante, preservando contexto histórico.

### Template obrigatório — `docs/architecture-onboarding.md`

Gerar seguindo esta estrutura mínima (ordem obrigatória):

1. Visão Geral do Sistema
2. Estrutura do Repositório
3. Arquitetura da Aplicação
4. Fluxo de Inicialização da Aplicação
5. Fluxo de Requisição (com exemplo real)
6. Fluxos de Negócio Importantes
7. Camada de Persistência
8. Integrações Externas
9. Observabilidade e Operação
10. Segurança e Controle de Acesso
11. Decisões Arquiteturais Relevantes
12. Riscos Técnicos e Pontos de Atenção

Requisitos de conteúdo:

- Incluir ao menos 3 diagramas Mermaid obrigatórios:
    - arquitetura em camadas;
    - entidades/tabelas centrais;
    - fluxo ponta a ponta;
    - sequência ponta a ponta (`sequenceDiagram`).
- Referenciar arquivos/pacotes reais do projeto em cada seção crítica.
- Explicar dependências externas e impacto operacional.
- Profundidade mínima: conteúdo equivalente ao padrão de `exemplo/architecture-onboarding.md`.

### Template obrigatório — `docs/architecture-onboarding-summary.md`

Gerar seguindo esta estrutura mínima:

1. O que é este sistema
2. Arquitetura em uma frase
3. Mapa rápido das pastas
4. Fluxo crítico (exemplo real)
5. Persistência
6. Integrações que impactam operação
7. Inicialização e configuração
8. Riscos principais para quem vai alterar código
9. Regras práticas para contribuir com segurança
10. Arquivos para abrir primeiro

Requisitos de conteúdo:

- Deve ser curto e executivo, porém específico ao projeto.
- Não repetir texto integral do documento completo; sintetizar com foco operacional.
- Incluir 3 diagramas Mermaid obrigatórios: entidades (compacto) + fluxo crítico (compacto) + sequência crítica (compacta).
- Profundidade mínima: conteúdo equivalente ao padrão de `exemplo/architecture-onboarding-summary.md`.

### Template obrigatório — `docs/developer-guide.md`

Gerar seguindo esta estrutura mínima (ordem obrigatória):

1. Entrypoints principais do sistema
2. Serviços/UseCases centrais
3. Fluxos de negócio mais utilizados
4. Pontos ideais para implementar novas features
5. Roteiro de primeira feature
6. Estratégia de testes no projeto
7. Checklist de PR técnico
8. Troubleshooting para desenvolvedor

Requisitos de conteúdo:

- Incluir caminhos reais de arquivos para acelerar onboarding.
- Incluir ao menos 1 roteiro prático passo a passo (ex.: primeira feature em 1h).
- Referenciar `docs/LOCAL_SETUP.md` nos primeiros passos.
- Incluir 3 diagramas Mermaid obrigatórios: entidades/domínio + fluxo de implementação + sequência de implementação.
- Profundidade mínima: conteúdo equivalente ao padrão de `exemplo/developer-guide.md`.

## Etapa 4 — Adaptações por Stack

Adapte **todo o conteúdo** à stack detectada na Etapa 1:

| Aspecto | Exemplo Java/Spring | Exemplo Node/TypeScript | Exemplo Python/Django |
|---------|--------------------|-----------------------|----------------------|
| Standards | `java-spring-standards.md` | `typescript-node-standards.md` | `python-django-standards.md` |
| Instruction applyTo | `**/*.java` | `**/*.ts` | `**/*.py` |
| Test applyTo | `**/*Test.java` | `**/*.spec.ts` / `**/*.test.ts` | `**/test_*.py` |
| Injeção de dependência | Via construtor | Via módulos/DI container | Via Django DI |
| Testes | JUnit 5 + Mockito + AssertJ | Jest/Vitest | pytest |
| Build | Maven/Gradle | npm/pnpm | pip/poetry |
| Ordem implementação | Entity→Repo→Service→Controller | Model→Service→Route→Controller | Model→View→Serializer→URL |

## Etapa 5 — Validação

Após gerar todos os arquivos, valide:

- [ ] `copilot-instructions.md` existe e tem ~100 linhas
- [ ] Todos os links internos entre arquivos estão corretos
- [ ] Instruction files têm frontmatter `applyTo` válido para a stack
- [ ] Prompt files têm frontmatter `mode: "agent"` e `description`
- [ ] `implement-local-environment.prompt.md` foi gerado e inclui instruções de setup local adaptável por stack
- [ ] Compatibilidade legada mantida para nomes antigos sem sufixo `.prompt.md`, quando já existirem no repositório
- [ ] Templates de tasks têm todas as seções obrigatórias
- [ ] `tasks/templates/_task-template.md` foi reproduzido exatamente para tasks de feature (mesmos títulos, ordem, bullets e textos-base; sem adicionar/remover/renomear seções)
- [ ] `tasks/templates/_task-template-bugfix.md` foi reproduzido exatamente para tasks de bugfix (mesmos títulos, ordem, bullets e textos-base; sem adicionar/remover/renomear seções)
- [ ] README de cada diretório serve como índice navegável
- [ ] Workflow de tasks documenta o fluxo `backlog → active → done`
- [ ] Conteúdo adaptado à stack real do projeto (não genérico)
- [ ] `docs/architecture-onboarding.md` gerado/atualizado com todas as seções obrigatórias (contexto, visão arquitetural, componentes, integrações, fluxo de dados, stack, decisões)
- [ ] `docs/architecture-onboarding.md` segue o template obrigatório de 12 seções e contém Mermaid de arquitetura + entidades + fluxo + sequência
- [ ] `docs/architecture-onboarding-summary.md` foi gerado/atualizado e segue o template executivo obrigatório
- [ ] `docs/architecture-onboarding-summary.md` contém Mermaid de entidades (compacto), fluxo crítico (compacto) e sequência crítica (compacta)
- [ ] `docs/developer-guide.md` gerado/atualizado com todas as seções obrigatórias (primeiros passos, estrutura, fluxo de dev, convenções, testes, dicas, links)
- [ ] `docs/developer-guide.md` segue o template obrigatório com exemplos práticos e caminhos reais
- [ ] `docs/developer-guide.md` contém Mermaid de entidades/domínio, fluxo de implementação e sequência de implementação
- [ ] `docs/LOCAL_SETUP.md` contém seção "Exemplo validado de execução" (quando aplicável)
- [ ] Diagnóstico operacional local (Etapa 1.4) foi realizado e refletido nos artefatos gerados
- [ ] Pelo menos 1 cenário de execução local foi validado com execução real
- [ ] Quando aplicável, cenário fallback sem dependência externa opcional foi documentado e validado
- [ ] Documentação em português brasileiro
- [ ] Nomes técnicos e exemplos de código em inglês
- [ ] Profundidade dos documentos de arquitetura e guia é equivalente ao padrão da pasta `exemplo`

## Regras Gerais

- Documentação e READMEs em **português brasileiro**
- Código e nomenclatura técnica em **inglês**
- Não gere conteúdo genérico — adapte à stack e convenções reais do projeto
- Se já existir documentação de engenharia, integre-a (não descarte)
- Se já existir `.github/copilot-instructions.md`, proponha merge ao invés de sobrescrever
- Modo execução direta (arquivo isolado): apresente a análise (Etapa 1) e aguarde aprovação antes de gerar arquivos
- Modo orquestrado (quando chamado por `bootstrap-project.prompt.md`): após apresentar a análise da Etapa 1, prossiga automaticamente sem aguardar aprovação intermediária
