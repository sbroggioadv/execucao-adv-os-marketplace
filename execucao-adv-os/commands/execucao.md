---
description: Orquestrador do plugin execucao-adv-os. Analisa titulo, decide acao (execucao/monitoria/cobranca), competencia, notificacao, calculo, geracao de peca e defesa/recurso. Anti-foro-errado por design.
allowed-tools: Read, Write, Edit, WebFetch, WebSearch, Bash, Glob, Grep
argument-hint: [descricao do caso ou fase atual]
---

Voce foi acionado pelo comando `/execucao` do plugin Execucao-Adv-OS.

Argumento recebido: `$ARGUMENTS`

## PROTOCOLO

### 1. Ativar imediatamente a skill `execucao-master`

Use `Skill(skill="execucao-master")` passando o argumento + contexto.

A skill `execucao-master` ira:
- Classificar a fase do caso pelo input
- Rotear para as skills corretas (Tiers 1-7)
- Manter o contexto da sessao (yaml `caso:`)
- Garantir que upstream rodou antes de downstream
- Auto-disparar `protocolo-p4-execucao` em pecas finais

### 2. Casos novos (fluxo classico)

Se for um caso novo (cliente acabou de chegar com titulo):

1. `analise-titulo-executivo` (decide acao + propaga contexto)
2. `competencia-territorial` (tabela ranqueada de foros)
3. `competencia-funcional` (JEC ou Comum)
4. `notificacao-extrajudicial-mora` (se ex persona)
5. `calculo-atualizacao-monetaria` (planilha + formula)
6. `peticao-inicial-execucao` / `peticao-inicial-monitoria` /
   `peticao-inicial-cobranca`
7. `protocolo-p4-execucao` (auto)

### 3. Casos de defesa

Cliente foi citado:

1. `analise-titulo-executivo` (analisar o titulo da parte contraria)
2. `competencia-*` (validar foro escolhido pelo autor)
3. `embargos-execucao` / `embargos-monitorios` / `contestacao-cobranca`
4. `protocolo-p4-execucao` (auto)

### 4. Casos de recurso

Houve decisao desfavoravel:

1. `gestao-prazo-recursal` (validar tempestividade)
2. Conforme decisao + competencia_funcional:
   - `embargos-declaracao`
   - `apelacao` (Comum) | `recurso-inominado-jec` (JEC)
   - `agravo-instrumento` (interlocutoria)
   - `recurso-especial-stj` (STJ)
   - `recurso-extraordinario-stf` (STF)
3. `protocolo-p4-execucao` (auto)

### 5. Cumprimento

Sentenca transitou em julgado:

1. `cumprimento-sentenca`
2. `protocolo-p4-execucao` (auto)

## REGRAS DURAS

1. **NUNCA gerar peca** sem ter rodado Tier 1 + Tier 2 antes.
2. **NUNCA pular** o `protocolo-p4-execucao` em pecas finais.
3. **SEMPRE alertar prescricao em risco** com ⚠️ em destaque.
4. **JEC vs Comum** muda TUDO: prazos, recursos, capacidade
   postulatoria — checar competencia-funcional sempre antes de
   recursos.
