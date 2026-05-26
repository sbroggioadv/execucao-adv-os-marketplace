---
name: competencia-funcional
description: >
  COMPETENCIA-FUNCIONAL — Decide se a acao tramita em Justica Estadual
  Comum, Justica Federal, Juizado Especial Civel (JEC, Lei 9099) ou
  Juizado Especial da Fazenda Publica. Aplica CF art. 109, Lei 9099,
  Lei 10.259/01 (JEF) e Lei 12.153/09 (JEFP). Marca contexto da sessao
  para que recursos da Tier 5 leiam (gate critico: prazos JEC sao
  CORRIDOS, recurso e inominado nao apelacao). Use SEMPRE apos
  competencia-territorial.
---

# COMPETENCIA-FUNCIONAL — JEC vs Comum vs Federal

## 1. POR QUE ESTA SKILL E CRITICA

Confundir JEC com Justica Comum gera **recurso intempestivo** (cenario
5 do pre-mortem). JEC tem regime proprio:
- Prazos **CORRIDOS** (Lei 9099 art. 12-13), nao uteis.
- Recurso e **inominado** (Lei 9099 art. 41), nao apelacao.
- Competencia recursal e **Turma Recursal**, nao TJ.
- Capacidade postulatoria dispensada ate 20 SM.

A skill marca o contexto da sessao com `competencia_funcional` que as
skills de recurso (Tier 5) LEEM antes de gerar peca.

---

## 2. INPUT NECESSARIO

Do contexto + perguntar:

1. **Valor da causa** (essencial para JEC: ate 40 SM — Lei 9099 art. 3º I).
2. **Partes:** PF? PJ? Microempreendedor? Massa falida? (algumas
   restricoes a serem PJ no JEC).
3. **Materia:** se executiva, se cobranca, se monitoria, se complexa
   probatoria.
4. **Uniao/autarquia federal/empresa publica federal envolvida?**
5. **Estado/municipio/autarquia estadual envolvida?**

---

## 3. ARVORE DE DECISAO

### Etapa 1 — Justica Federal? (CF art. 109)

| Parte/Materia | Resultado |
|---------------|-----------|
| Uniao, autarquia federal, empresa publica federal | JF (art. 109 I) |
| Causa fundada em tratado internacional | JF (art. 109 III) |
| Indigenas/disputa terras indigenas | JF (art. 109 XI) |
| Outros casos do art. 109 | JF |
| Nao se enquadra | **Justica Estadual** |

Se JF + valor ate 60 SM + causas listadas Lei 10.259/01 art. 3º →
**Juizado Especial Federal (JEF)**. Caso contrario, **Vara Federal**.

### Etapa 2 — JEC (Lei 9099)?

JEC pode quando TODOS os criterios:

- ✅ Valor da causa **ate 40 SM**
- ✅ Materia listada Lei 9099 art. 3º (cobranca em geral cabe; execucao
  de titulo extrajudicial de **ate 40 SM** tambem cabe — art. 3º §1º I)
- ✅ Autor e **pessoa fisica capaz** ou **microempreendedor individual**,
  **microempresa**, **empresa de pequeno porte** (Lei 12.126/09)
- ✅ Reu pode ser PF ou PJ (incluindo PJ de direito privado)
- ❌ Nao envolve massa falida, incapaz, presos, ou Fazenda Publica

**Atencao:** JEC e **opcional ate 40 SM, obrigatorio em alguns
casos específicos** (Lei 9099 art. 3º §3º).

### Etapa 3 — Juizado Especial da Fazenda Publica (Lei 12.153)?

Estado/Distrito/Municipio + valor ate 60 SM → **JEFP** estadual.

### Etapa 4 — Default: Vara Civel da Justica Estadual

Se nada acima — Vara Civel da Justica Comum estadual (com base no foro
ja definido em `competencia-territorial`).

---

## 4. OUTPUT OBRIGATORIO

```markdown
## Competencia funcional — caso [identificacao]

### Premissas

- Valor da causa: R$ [valor] (≈ [N] SM)
- Autor: [PF/PJ/ME/MEI/etc.]
- Reu: [PF/PJ/etc.]
- Materia: [cobranca/execucao/monitoria]
- Justica Federal: [sim/nao]

### Decisao

**JUIZO COMPETENTE:** [Vara Civel Comum / JEC / JEF / JEFP / Vara Federal]

**Base legal:** [Lei X art. Y / CF art. Z]

### Implicacoes processuais

| Item | Valor |
|------|-------|
| **Prazos** | Uteis (CPC art. 219) / **Corridos** (Lei 9099 art. 12-13) |
| **Recurso da sentenca** | Apelacao (CPC art. 1.009) / **Recurso Inominado** (Lei 9099 art. 41) |
| **Prazo recursal** | 15 dias uteis / **10 dias corridos** |
| **Capacidade postulatoria** | Advogado obrigatorio / **Dispensavel ate 20 SM no JEC** |
| **Custas iniciais** | Cobradas / **Isentas em 1o grau no JEC** |
| **Despesas em caso de derrota recursal** | Conforme CPC | Honorarios sucumbenciais Lei 9099 art. 55 |
| **Competencia recursal** | Tribunal de Justica | **Turma Recursal** |

### Contexto que sera propagado

```yaml
competencia_funcional:
  juizo: [vara_civel_comum | jec | jef | jefp | vara_federal]
  prazo_regime: [uteis | corridos]
  recurso_sentenca: [apelacao | recurso_inominado]
  prazo_recurso_dias: [15 | 10]
  capacidade_postulatoria: [obrigatoria | facultativa_ate_20_sm]
  tribunal_recursal: [tj | turma_recursal | trf]
```

### ⚠️ Avisos

- **JEC e opcao do autor.** Pode preferir Vara Comum mesmo se cabivel
  JEC (maior amplitude probatoria, recurso a TJ, advocacia obrigatoria).
- **Quem pode ser autor no JEC** e restrito (PF, MEI, ME, EPP). PJ
  comum (sociedade limitada de grande porte) NAO pode ajuizar no JEC.
- **Em execucao no JEC:** ate 40 SM. Acima, Vara Comum.
```

---

## 5. PROIBICOES

1. Nao recomendar JEC sem checar **valor + materia + parte legitimada**.
2. Nao confundir JEC com Vara Civel comum — regime processual e DIFERENTE.
3. Nao prosseguir sem marcar o contexto `competencia_funcional` que as
   skills de recurso vao ler.
4. Se duvida entre JEC e Vara Comum cabivel: explique o trade-off ao
   advogado, deixe a escolha com ele.
