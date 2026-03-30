---
agent: "agent"
description: "Orquestra o bootstrap completo: scaffold AI-Driven + setup local pós-scaffold"
---

# Bootstrap completo do projeto (orquestrador)

Você deve executar, em sequência, os dois prompts existentes neste mesmo diretório:

1. `scaffold-ai-structure.prompt.md`
2. `implement-local-environment.prompt.md`

## Objetivo

Permitir uma execução única e ponta a ponta para:

- analisar a stack e estrutura do projeto;
- gerar a estrutura AI-Driven Development;
- preparar automações de ambiente local;
- documentar e validar execução local.

## Regras obrigatórias

- Não remover nem substituir os prompts originais.
- Manter `scaffold-ai-structure.prompt.md` e `implement-local-environment.prompt.md` intactos para execução individual.
- Reutilizar artefatos já existentes antes de criar novos.
- Aplicar adaptações por stack detectada (Java e não-Java).
- Em projetos sem API HTTP, não forçar Postman/Swagger; documentar validação equivalente.
- Garantir que a documentação de arquitetura e onboarding não seja resumida em excesso.
- Sempre gerar/atualizar documentação seguindo padrão semelhante aos arquivos da pasta `exemplo`.
- Exigir diagnóstico de cenário operacional local (dependências externas, variações de stack e fallback possível).
- Exigir validação executada de comandos antes de declarar sucesso do bootstrap.

## Fluxo de execução

### Etapa A — Executar scaffold AI-Driven

Execute integralmente o conteúdo de `scaffold-ai-structure.prompt.md`.

Durante esta execução via orquestrador, considere **modo orquestrado**: após apresentar a análise da Etapa 1, não interrompa o fluxo aguardando aprovação intermediária.

Resultado esperado da Etapa A:

- estrutura `.github`, `tasks` e documentação base geradas/atualizadas;
- prompts e instruções adaptados à stack detectada.
- `docs/architecture-onboarding.md` gerado/atualizado com profundidade adequada e seções obrigatórias.
- `docs/architecture-onboarding-summary.md` gerado/atualizado no formato executivo.
- `docs/developer-guide.md` gerado/atualizado com foco prático para onboarding.
- os três arquivos acima com padrão semelhante ao da pasta `exemplo`.

### Etapa B — Executar setup local pós-scaffold

Na sequência, execute integralmente o conteúdo de `implement-local-environment.prompt.md`.

Resultado esperado da Etapa B:

- scripts locais criados/atualizados (`setup-local`, `run-local`, `validate-local`);
- `docs/LOCAL_SETUP.md` atualizado com seção **Exemplo validado de execução**;
- cenários de execução **padrão** e **fallback** (quando aplicável) documentados com comandos reais;
- validações locais e artefatos auxiliares (quando aplicável).

## Critério de conclusão

Considere concluído apenas quando as duas etapas (A e B) tiverem sido finalizadas e os artefatos esperados estiverem presentes.

Checklist mínimo de conclusão:

- [ ] `docs/architecture-onboarding.md` existe e segue o template obrigatório do scaffold
- [ ] `docs/architecture-onboarding-summary.md` existe e segue o template executivo obrigatório
- [ ] `docs/developer-guide.md` existe e segue o template obrigatório do scaffold
- [ ] Profundidade e organização dos três documentos são semelhantes ao padrão dos arquivos da pasta `exemplo`
- [ ] `docs/LOCAL_SETUP.md` contém **Exemplo validado de execução** (quando aplicável)
- [ ] Comando de startup validado com execução real em pelo menos 1 cenário funcional
- [ ] Quando houver dependência externa opcional no startup, cenário fallback foi validado e documentado