---
name: gestao-prazo-recursal
description: >
  GESTAO-PRAZO-RECURSAL — Calcula e alerta prazos recursais cumprindo
  CPC art. 219 (uteis) vs Lei 9099 (corridos). Da intimacao ate o
  recurso correto: embargos declaracao (5 dias), apelacao/recurso
  inominado (15 uteis / 10 corridos), agravo (15 uteis), REsp/RE (15
  uteis), agravo em REsp/RE (15 uteis). Calcula interrupcao por
  embargos. Use SEMPRE que houver pergunta sobre prazo de recurso.
---

# GESTAO-PRAZO-RECURSAL — Calculadora de Prazos

## 1. REGIMES

| Procedimento | Regime |
|--------------|--------|
| Justica Comum (CPC) | UTEIS (CPC art. 219) |
| JEC (Lei 9099) | CORRIDOS (art. 12-13) |
| JEF (Lei 10.259) | Aplica subsidiariamente Lei 9099 — corridos |
| JEFP (Lei 12.153) | Aplica Lei 9099 — corridos |

**Critico:** confundir uteis com corridos gera **recurso intempestivo**
e transito em julgado. Cenario 5 do pre-mortem.

## 2. PRAZOS DOS RECURSOS

| Recurso | Comum (uteis) | JEC (corridos) |
|---------|---------------|----------------|
| Embargos de declaracao | 5 (art. 1.023) | 5 (Lei 9099 art. 50) |
| Apelacao / Recurso inominado | 15 (art. 1.003 §5º) | 10 (Lei 9099 art. 42) |
| Agravo de instrumento | 15 (art. 1.003 §5º) | — (nao cabe em regra no JEC) |
| Agravo interno | 15 (art. 1.021) | 5 corridos (turma recursal) |
| Recurso especial | 15 (art. 1.003 §5º) | — (NAO CABE — Sum. 203 STJ) |
| Recurso extraordinario | 15 (art. 1.003 §5º) | 15 (Sum. 640 STF — cabe RE no JEC se materia constitucional) |
| Agravo em REsp/RE | 15 (art. 1.042) | 15 |

## 3. INTERRUPCAO POR EMBARGOS DE DECLARACAO

**CPC art. 1.026:** embargos INTERROMPEM o prazo dos demais recursos.

Apos publicacao do julgamento dos embargos:
- Prazo dos demais recursos **REINICIA do zero** (nao "soma o que faltava")
- Aplica-se tanto em Comum quanto em JEC

## 4. WORKFLOW

### Passo 1 — Identificar marco inicial

Pergunte:
1. Qual a decisao impugnada? (sentenca / acordao / interlocutoria /
   embargos de declaracao decididos)
2. Qual a data da intimacao/publicacao?
3. O processo tramita em Comum ou JEC?

### Passo 2 — Identificar recurso cabivel

Cruze com a skill correspondente (apelacao, agravo, REsp, RE,
inominado etc.).

### Passo 3 — Calcular o prazo

#### Regra util (CPC art. 219):
- Conta-se a partir do dia util seguinte a intimacao
- Excluem-se sabados, domingos e feriados
- Suspende-se em recesso (CPC art. 220 — 20/12 a 20/01)

#### Regra corrida (Lei 9099):
- Conta-se a partir do dia seguinte
- Nao se exclui sabado/domingo/feriado para contagem
- Apenas se o ULTIMO dia cair em dia nao util, prorroga-se para o
  proximo dia util (art. 12)

### Passo 4 — Verificar feriados forenses

- Feriados nacionais (CC, Lei 662/49)
- Feriados estaduais (legislacao estadual)
- Feriados forenses locais (portarias do TJ ou TRF)
- Recesso forense final de ano (CPC art. 220)

### Passo 5 — Output

```markdown
## Calculo de Prazo Recursal

**Decisao:** [sentenca / acordao / interlocutoria]
**Tipo de processo:** [Justica Comum / JEC]
**Data da intimacao/publicacao:** [DD/MM/YYYY]
**Recurso cabivel:** [apelacao / agravo / REsp / etc.]
**Prazo:** [N] dias [uteis / corridos]

### Calculo

| Item | Valor |
|------|-------|
| Inicio | [DD/MM/YYYY] |
| Termino | **[DD/MM/YYYY]** |
| Dias contabilizados | [N uteis / N corridos] |
| Feriados/recessos excluidos | [lista] |

### Embargos interrompem? Sim
Se opostos embargos antes do termino, prazo do recurso PRINCIPAL
REINICIARA apos a publicacao da decisao dos embargos.

### ⚠️ Margem de seguranca

Recomenda-se protocolar com pelo menos **3 dias uteis de antecedencia**
para evitar imprevistos sistemicos (PJe fora do ar, etc.).

**PROTOCOLAR ATE:** [data com margem de 3 dias]
```

## 5. PROIBICOES

1. NUNCA confundir uteis com corridos.
2. Nao esquecer suspensao por recesso forense (20/12 a 20/01).
3. Nao prometer prazo "exatos" sem verificar feriado estadual/local.
4. Sempre orientar margem de seguranca.
