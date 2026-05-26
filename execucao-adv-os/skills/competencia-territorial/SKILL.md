---
name: competencia-territorial
description: >
  COMPETENCIA-TERRITORIAL — Define foro correto da acao executiva,
  monitoria ou de cobranca atraves de arvore de decisao em 6 niveis,
  cruzando CPC arts. 46-53, 63, 781, CDC art. 101, e Sumulas 33 e 130
  STJ. SEMPRE produz tabela ranqueada de 2-4 foros possiveis, NUNCA
  resposta unica. Mitigacao de risco-killer: foro errado gera
  prescricao intercorrente. Use SEMPRE apos analise-titulo-executivo
  e antes de qualquer peticao inicial.
---

# COMPETENCIA-TERRITORIAL — Arvore de Decisao em 6 Niveis

## 1. POR QUE ESTA SKILL EXISTE

Foro errado = prescricao intercorrente quando os autos viajam pra
juizo competente (CPC art. 924 III). E o **principal risco-killer**
do plugin (cenario 1 do pre-mortem).

**Regra dura:** voce produz TABELA com 2-4 foros possiveis ranqueados,
NUNCA emite resposta unica. Quem decide e o advogado.

---

## 2. INPUT NECESSARIO

Do contexto da sessao (`analise-titulo-executivo`) + perguntar:

1. **Existe clausula de eleicao de foro no titulo/contrato?** Se sim,
   onde? Em que termos (geral, especifico)?
2. **Tipo de relacao** (consumo/civil/empresarial/locaticia).
3. **Tipo da acao** (execucao/monitoria/cobranca).
4. **Domicilio do executado/devedor.** Se incerto, dizer.
5. **Local dos bens conhecidos do executado.**
6. **Local do cumprimento da obrigacao** (entrega/pagamento estipulado).
7. **Justica Federal envolvida** (art. 109 CF — Uniao, autarquia, empresa
   publica federal, ou interesse da Uniao)?

---

## 3. ARVORE DE DECISAO — 6 NIVEIS

Aplique nesta ORDEM. Cada nivel pode resolver, ou abrir alternativas.

### NIVEL 1 — Justica Federal?

Se Uniao, autarquia federal, empresa publica federal ou interesse da
Uniao -> **competencia da Justica Federal** (CF art. 109). Pare aqui
e roteie para `competencia-funcional`.

### NIVEL 2 — Relacao de consumo?

Se sim (`cdc_aplicavel: true` no contexto):
- **CDC art. 101 I:** foro do domicilio do **consumidor**, mesmo que
  o consumidor seja o reu (Sum. 130 STJ na duvida).
- Em acao do **fornecedor contra consumidor**: foro do consumidor
  prevalece sobre clausula de eleicao (Sum. 130 STJ). Clausula que
  obrigue consumidor a litigar em foro distinto e nula (CDC art. 51 IV).

### NIVEL 3 — Foro especial obrigatorio?

| Tipo | Foro |
|------|------|
| Alimentos | Domicilio do alimentando (CPC art. 53 II) |
| Locaticia (despejo/cobranca de alugueres) | Local do imovel (CPC art. 53 c + Lei 8.245/91) |
| Sucessoes / inventario | Domicilio do autor da heranca (CPC art. 48) |
| Reparacao de dano por ato ilicito | Local do ato OU domicilio do autor (CPC art. 53 IV b) |
| Pessoa juridica como autora | Local da sede para acoes de cobranca / execucao de contratos (CPC art. 53 III a) |

### NIVEL 4 — Foros alternativos da execucao (CPC art. 781)

Em execucao de titulo extrajudicial, o **exequente** pode escolher
entre:

- **Domicilio do executado** (regra geral CPC art. 46 + art. 781 I)
- **Local onde se encontrem os bens sujeitos a execucao** (CPC art. 781 II)
- **Local em que se deve cumprir a obrigacao** (CPC art. 781 III)
- **Local onde reside o fiador, se houver** (CPC art. 781 V)
- Eleicao de foro **valida** (se nao colidir com niveis 1-3)

Estes sao **cumulativos** — o exequente escolhe o mais conveniente.

### NIVEL 5 — Clausula de eleicao de foro

- **Valida** entre partes plenamente capazes em relacoes civis/empresariais
  paritarias (CC art. 78 e CPC art. 63).
- **Nula** se for relacao de consumo (Sum. 130 STJ) ou de adesao com
  prejuizo a parte (CPC art. 63 §3º).
- Em **execucao**, eleicao convive com os foros alternativos do art.
  781 — o exequente pode optar.

### NIVEL 6 — Regra residual

Se nenhum dos anteriores resolveu: **domicilio do reu/executado**
(CPC art. 46). Se domicilio incerto: foro do **lugar onde for
encontrado** (CPC art. 49). Se reu no exterior: foro do **autor**
(CPC art. 49 c/c art. 21 CPC).

---

## 4. OUTPUT OBRIGATORIO — TABELA RANQUEADA

```markdown
## Foros possiveis — caso [identificacao]

### Premissas analisadas

- Tipo de acao: [execucao/monitoria/cobranca]
- Natureza da relacao: [consumo/civil/empresarial/locaticia]
- Clausula de eleicao: [sim — comarca de X / nao]
- Domicilio do executado: [comarca de Y]
- Bens conhecidos: [comarca de Z]
- Cumprimento da obrigacao: [comarca de W]
- Justica Federal: [sim/nao]

### Tabela de foros

| Rank | Foro | Base legal | Vantagens | Riscos |
|------|------|------------|-----------|--------|
| 🥇 | [comarca] | CPC art. X / Sum. Y | [acesso a bens / domicilio executado / etc.] | [eventual contestacao baseada em Z] |
| 🥈 | [comarca] | [base legal] | [...] | [...] |
| 🥉 | [comarca] | [base legal] | [...] | [...] |

### Recomendacao final

Foro mais defensavel processualmente: **[comarca]** porque [3-4 linhas
de fundamentacao tecnica].

**Riscos do foro escolhido:**
- [risco 1] -> mitigacao: [...]
- [risco 2] -> mitigacao: [...]

### Avisos criticos

⚠️ **DECISAO DO ADVOGADO.** Esta skill ranqueou opcoes — escolha final
e tecnica do advogado em funcao de conveniencia processual (acesso a
bens, agilidade do tribunal, jurisprudencia local).

🚨 **RISCO DE PRESCRICAO INTERCORRENTE:** se foro escolhido for declarado
incompetente, autos viajam e podem prescrever. Em duvida, escolha foro
inquestionavel mesmo que menos conveniente.
```

---

## 5. PROIBICOES ABSOLUTAS

1. **Nao dar resposta unica.** Sempre tabela com 2-4 foros.
2. **Nao ignorar clausula de eleicao** quando partes sao plenamente
   capazes em relacao paritaria.
3. **Nao impor foro do consumidor** se nao houver relacao de consumo
   real (verifique habitualidade do fornecedor).
4. **Nao confundir foro alternativo do art. 781 com regra geral
   do art. 46.** Em execucao, exequente escolhe.
5. **Nao prosseguir** se faltar dado critico (domicilio do executado,
   eleicao de foro, etc.). Pergunte UMA vez antes de tabelar.
