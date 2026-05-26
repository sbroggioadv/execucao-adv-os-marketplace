# CLAUDE.md — plugin-execucao (interno do source)

> Regras internas do source `plugin-execucao/`. Plugin alvo:
> `execucao-adv-os`. Familia Adv-OS.

---

## Identidade

- **Plugin name (slug):** `execucao-adv-os`
- **Marketplace publico:** `https://github.com/sbroggioadv/execucao-adv-os-marketplace`
- **Source privado:** `https://github.com/sbroggioadv/execucao-adv-os`
- **Modelo comercial:** ORDER BUMP Kirvano — R$ 29,80
- **Posicionamento:** overdelivery proposital — 22 skills end-to-end
  no preco de order bump.

## Filosofia do plugin

**Anti-foro-errado + anti-calculo-alucinado por design.** As 2 mitigações
centrais:

1. `competencia-territorial` SEMPRE produz tabela ranqueada de
   foros, nunca resposta unica. (Cenario 1 do pre-mortem.)
2. `calculo-atualizacao-monetaria` NUNCA gera valor final com
   indices hardcoded — so formula + fonte. (Cenario 2 do pre-mortem.)

## Skill map (22 + orquestrador)

- Tier 0: `execucao-master` (orquestrador)
- Tier 1: `analise-titulo-executivo`, `competencia-territorial`,
  `competencia-funcional`
- Tier 2: `notificacao-extrajudicial-mora`, `calculo-atualizacao-monetaria`
- Tier 3: `peticao-inicial-execucao/-monitoria/-cobranca`
- Tier 4: `embargos-execucao/-monitorios`, `contestacao-cobranca`
- Tier 5: `embargos-declaracao`, `apelacao`, `recurso-inominado-jec`,
  `agravo-instrumento`
- Tier 6: `recurso-especial-stj`, `recurso-extraordinario-stf`
- Transversais: `protocolo-p4-execucao`, `gestao-prazo-recursal`,
  `pedido-tutela-urgencia`, `cumprimento-sentenca`

## Auto-chains criticas

- TODA peca final → auto-dispara `protocolo-p4-execucao`
- `analise-titulo-executivo` → propaga contexto pra TODAS as outras
- `peticao-inicial-*` → BLOQUEADA se Tier 1+2 nao rodou
- `apelacao` → BLOQUEADA se contexto e JEC (redireciona pra `recurso-inominado-jec`)
- Recursos → BLOQUEADOS se `gestao-prazo-recursal` indicou intempestivo

## Cross-link

- `juris-adv-os` (order bump irmao) e complementar opcional para
  buscar/validar jurisprudencia atualizada. Mencionar no README mas
  NAO declarar dependencia hard.
- `jurisprudencia-estrategica` do plugin-mae (`ia-combativa-adv-os`)
  trata de INTEGRACAO estrategica — complementar.
- `calculosjudiciais-adv-os` (plugin irmao em desenvolvimento) pode
  complementar com calculos avancados. Mencao soft no README.

## Pre-mortem (7 cenarios mitigados)

Detalhe no plano do agent-cto. Mitigacoes aplicadas em design:

1. Foro errado → `competencia-territorial` arvore 6 niveis + tabela
   ranqueada
2. Calculo desatualizado → `calculo-atualizacao-monetaria` zero
   hardcoded
3. Notificacao invalida → `notificacao-extrajudicial-mora` classifica
   mora ex re/persona, email proibido como unica via
4. Confusao executavel vs monitoria → `analise-titulo-executivo`
   matriz de decisao explicita
5. Recurso intempestivo JEC vs Comum → `apelacao` tem gate JEC,
   `recurso-inominado-jec` separada
6. Embargos confundidos → 3 skills com nomes inequivocos
7. CDC ignorado → flag obrigatoria de natureza_relacao no Tier 1

## Padroes de codigo

1. Stock first (WebSearch + WebFetch nativos).
2. Auto-chains so onde fazem sentido (busca → valida; peticao → P4).
3. Saida estruturada (markdown com blocos, tabelas, yaml de contexto).
4. Aviso legal em cada peca final + em outputs criticos.
5. Skill folder = SO SKILL.md (regra dura da familia).
6. plugin.json minimal (4 campos canonicos).

## Roadmap pos-v0.1.0

- `excecao-pre-executividade` (defesa endoprocessual sem garantia)
- `penhora-sisbajud-detalhada` (workflow especifico de penhora online)
- `leilao-judicial` (acompanhamento da fase de leilao)
- `desconsideracao-personalidade-juridica` (incidente do art. 133-137)

Nao implementar sem demanda real.
