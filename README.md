# Execucao Adv-OS

> ## ⚖️ Este repositório NÃO é software livre
>
> O código fica visível para viabilizar a instalação no Claude/Cowork — não porque seja gratuito.
>
> **EXECUCAO ADV-OS — R$ 29,80, pagamento único** (sem assinatura, sem recorrência)
> 👉 **[Adquirir a licença](https://pay.kirvano.com/78f3f212-a847-4365-91ca-6f0edf8a78da)**
>
> **Ao forkar ou clonar este repositório você adere à [licença de uso](LICENSE)**, devendo efetuar o
> pagamento no link acima e enviar o comprovante para **luis@sbroggio.com.br**.
>
> Os forks são públicos no GitHub e são registrados pelo titular (data, conta e repositório).
>
> **Já comprou?** Nada a fazer — sua licença cobre o uso e o fork para instalação. Este aviso vale de
> 11/08/2026 em diante, para quem chega ao repositório sem ter adquirido.


> ## ⚖️ Este repositório NÃO é software livre
>
> O código fica visível para viabilizar a instalação no Claude/Cowork — não porque seja gratuito.
>
> **EXECUCAO ADV-OS — R$ 29,80, pagamento único** (sem assinatura, sem recorrência)
> 👉 **[Adquirir a licença](https://pay.kirvano.com/78f3f212-a847-4365-91ca-6f0edf8a78da)**
>
> **Ao forkar ou clonar este repositório você adere à [licença de uso](LICENSE)**, devendo efetuar o
> pagamento no link acima e enviar o comprovante para **luis@sbroggio.com.br**.
>
> Os forks são públicos no GitHub e são registrados pelo titular (data, conta e repositório).
>
> **Já comprou?** Nada a fazer — sua licença cobre o uso e o fork para instalação. Este aviso vale de
> 11/08/2026 em diante, para quem chega ao repositório sem ter adquirido.


Plugin Claude Code / Cowork para advogados que atuam em **execucao de
titulo extrajudicial + acao monitoria + acao de cobranca** — ponta-a-ponta.

> Anti-foro-errado + anti-calculo-alucinado por design.

---

## O que entrega

**22 skills end-to-end** em 7 tiers, mais 1 orquestrador (`execucao-master`)
que roteia automaticamente conforme o input do advogado.

### Tier 1 — Analise inicial
- `analise-titulo-executivo` — classifica cheque/NP/duplicata/contrato/NF/boleto, valida art. 784 CPC, decide acao cabivel (execucao/monitoria/cobranca), identifica natureza da relacao (CDC?), prazo prescricional
- `competencia-territorial` — arvore 6 niveis (eleicao/consumo/foros especiais/art. 781/domicilio), **tabela ranqueada** de 2-4 foros
- `competencia-funcional` — JEC vs Comum vs Federal vs Fazenda

### Tier 2 — Pre-processual
- `notificacao-extrajudicial-mora` — classifica mora (ex re/persona/iliquida), vias validas (cartorio TD, AR-MP, edital), email simples PROIBIDO como unica via
- `calculo-atualizacao-monetaria` — planilha + formula estruturada, **zero indice hardcoded** (advogado preenche da tabela oficial atual)

### Tier 3 — Peticoes iniciais
- `peticao-inicial-execucao` (CPC 798-805)
- `peticao-inicial-monitoria` (CPC 700-702 + Sum. 247/299/503/504/531 STJ)
- `peticao-inicial-cobranca` (procedimento comum ou JEC)

### Tier 4 — Defesa
- `embargos-execucao` (CPC 914-920 + materias do 917)
- `embargos-monitorios` (CPC 702 + Sum. 292 STJ)
- `contestacao-cobranca` (CPC 335-342 + reconvencao CPC 343)

### Tier 5 — Recursos ordinarios
- `embargos-declaracao` (CPC 1.022-1.026, interrompe prazo dos demais)
- `apelacao` (CPC 1.009-1.014) — **gate JEC obrigatorio**
- `recurso-inominado-jec` (Lei 9099 art. 41-46, **10 dias corridos**)
- `agravo-instrumento` (CPC 1.015 + Tema 988 STJ rol mitigado)

### Tier 6 — Instancias superiores
- `recurso-especial-stj` (CF art. 105 III + Sum. 5, 7, 83, 211, 282-284 STJ)
- `recurso-extraordinario-stf` (CF art. 102 III + repercussao geral + Sum. 282, 356, 636, 640 STF)

### Transversais
- `protocolo-p4-execucao` — **auditoria Suprema Corte R1-R4 obrigatoria** em toda peca final
- `gestao-prazo-recursal` — calculadora de prazos (uteis Comum vs corridos JEC)
- `pedido-tutela-urgencia` — arresto, indisponibilidade, SISBAJUD preventivo, RENAJUD
- `cumprimento-sentenca` — fechamento do ciclo (CPC 513-538, multa 10%)

---

## Como usar

```
/execucao [descricao do caso]
```

Exemplos:

- `/execucao Cheque devolvido em fevereiro 2025, valor R$ 50k`
- `/execucao Cliente foi citado em monitoria, vou apresentar embargos`
- `/execucao Vou apelar da sentenca, processo no TJSP`

O Claude vai:
1. Classificar a fase do caso
2. Rotear pelas skills corretas em sequencia
3. Auditar a peca final pelo Protocolo P4 (Suprema Corte R1-R4)
4. Devolver peca + selo P4 + checklist de anexos + aviso de revisao humana

---

## Como instalar

### Via UI Cowork (recomendado)

1. Cowork -> Settings -> Plugins -> Pessoal -> "+" -> Adicionar marketplace
2. Cola:
   ```
   https://github.com/sbroggioadv/execucao-adv-os-marketplace
   ```
3. Sincronizar -> Instalar -> `/execucao <seu caso>`

### Via CLI

```bash
claude plugin marketplace add https://github.com/sbroggioadv/execucao-adv-os-marketplace
claude plugin install execucao-adv-os@execucao-adv-os-marketplace
```

---

## Filosofia

**Stock-first:** funciona com `WebSearch` + `WebFetch` nativos do
Claude Code. Sem MCP externo obrigatorio.

**Anti-halucinacao por design** em dois pontos criticos:
- Competencia: tabela ranqueada (nunca resposta unica)
- Calculo: planilha+formula (nunca indice numerico hardcoded)

**Auto-chain inteligente:** P4 audita TODA peca final antes de sair.
JEC trava apelacao automaticamente (so recurso inominado).

---

## Complementos opcionais (cross-sell)

- **`juris-adv-os`** (R$ 29,80, order bump) — busca e valida
  jurisprudencia atualizada com fonte rastreavel. Util para
  fundamentar pecas com Sumulas e julgados recentes.
- **`ia-combativa-adv-os`** (R$ 498, plugin-mae) — onboarding
  completo do escritorio + 29 skills gerais.
- **`calculosjudiciais-adv-os`** (em desenvolvimento) — calculos
  avancados e contraditados.

---

## ⚠️ Aviso legal

Validacao automatica e **assistida por IA**. A conferencia humana
final do calculo, das clausulas contratuais, dos documentos anexos
e da pertinencia ao caso concreto e RESPONSABILIDADE EXCLUSIVA do
advogado antes de protocolar.

---

## Licenca

Uso licenciado mediante aquisição — ver [`LICENSE`](./LICENSE). As cópias obtidas até 11/08/2026 permanecem sob MIT; a partir dessa data o código é proprietário.

---

**Familia Adv-OS** — plugins juridicos modulares para Claude Code / Cowork.

[ia-combativa-adv-os](https://github.com/sbroggioadv/ia-combativa-adv-os-marketplace) ·
[juris-adv-os](https://github.com/sbroggioadv/juris-adv-os-marketplace) ·
[marketing-adv-os](https://github.com/sbroggioadv/marketing-adv-os-marketplace) ·
[previdenciario-adv-os](https://github.com/sbroggioadv/previdenciario-adv-os-marketplace) ·
[trabalhista-adv-os](https://github.com/sbroggioadv/trabalhista-adv-os-marketplace) ·
[tributario-societario-adv-os](https://github.com/sbroggioadv/tributario-societario-adv-os-marketplace) ·
[auditoria-contabil-os](https://github.com/sbroggioadv/auditoria-contabil-os-marketplace) ·
[licitacoes-adv-os](https://github.com/sbroggioadv/licitacoes-adv-os-marketplace) ·
[direito-medico-adv-os](https://github.com/sbroggioadv/direito-medico-adv-os-marketplace)
