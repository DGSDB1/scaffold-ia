---
agent: "agent"
description: "Setup e validação do ambiente local pós-scaffold"
---

# Implement Local Environment

Este é o arquivo canônico para setup local pós-scaffold, seguindo a nomenclatura padrão `*.prompt.md`.

## Objetivo

Configurar e validar o ambiente de desenvolvimento local do projeto, criando ou atualizando:

- `scripts/setup-local.ps1` — instalação de dependências e configuração inicial;
- `scripts/run-local.ps1` — inicialização da aplicação localmente;
- `scripts/validate-local.ps1` — validação de que o ambiente está funcionando.

## Regras obrigatórias

- Adaptar scripts à stack detectada (Java/Maven/Gradle, Node/npm/pnpm, Python/pip, etc.).
- Para projetos sem API HTTP, substituir validação de endpoints por validação equivalente da stack.
- Atualizar `docs/LOCAL_SETUP.md` com seção **Exemplo validado de execução** contendo:
    - comando de start local;
    - comando de validação local;
    - resultado esperado (endpoints de health/openapi/swagger quando aplicável).
- Reaproveitar detecção de stack já realizada em etapas anteriores.
- Não sobrescrever scripts existentes sem propor merge.

## Diagnóstico obrigatório de cenário (multi-stack)

Antes de propor os comandos finais de `setup-local`, `run-local` e `validate-local`, você deve identificar e registrar no output:

1. **Ferramenta de execução principal por stack**
    - Java: Maven/Gradle wrapper vs instalação global.
    - Node: npm/pnpm/yarn e comando de start disponível.
    - Python: venv/poetry/pipenv e comando de execução.
2. **Versão efetiva usada pela ferramenta**
    - Não validar só o runtime no PATH.
    - Validar a versão usada pela ferramenta de build/run (ex.: `mvn -v`, `gradle -v`, `npm -v`, `python -V`, `poetry --version`).
3. **Dependências externas de bootstrap/start**
    - Ex.: Config Server, banco, fila, cache, proxy/VPN, serviços de autenticação.
4. **Chaves reais de configuração do projeto**
    - Detectar no repositório quais propriedades/variáveis realmente controlam o comportamento (não assumir nomes genéricos).
    - Ex.: em Java/Spring, verificar `application*` e `bootstrap*`; em Node/Python, verificar `.env*`, arquivos de config e loaders usados.

## Estratégia obrigatória de comandos (padrão + fallback)

Os scripts e a documentação devem conter, no mínimo, dois cenários quando houver dependência externa opcional no startup:

- **Cenário padrão**: execução completa com dependências externas habilitadas.
- **Cenário fallback local**: execução sem dependência externa opcional, usando a chave real detectada no projeto.

Regras para fallback:

- Não inventar flags; usar somente chaves comprovadas na base.
- Se não houver chave para bypass, documentar explicitamente o bloqueio e o pré-requisito.
- Em scripts PowerShell, preferir parâmetro explícito (ex.: `-Disable...`) quando fizer sentido para reduzir erro operacional.

## Validação obrigatória antes de concluir

Você só pode concluir a tarefa de setup local se executar validações reais e registrar resultado:

1. **Validação de toolchain**: comando de versão da ferramenta principal e runtime efetivo.
2. **Validação do start**: executar ao menos um comando de startup funcional (padrão ou fallback).
3. **Validação de saúde da aplicação**:
    - API HTTP: health/openapi/swagger (ou equivalentes definidos no projeto).
    - Não HTTP: validação equivalente (CLI smoke test, job dry-run, script de sanity).

Se o cenário padrão falhar por indisponibilidade externa, registrar evidência e validar obrigatoriamente o fallback (quando disponível).