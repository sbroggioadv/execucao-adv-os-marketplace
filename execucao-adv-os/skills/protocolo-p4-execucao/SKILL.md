---
name: protocolo-p4-execucao
description: >
  PROTOCOLO-P4-EXECUCAO — Auditoria Suprema Corte R1-R4 obrigatoria
  antes de qualquer peca final do plugin sair (inicial, defesa,
  recurso). Quatro rounds estruturados: R1 Coleta (premissas), R2
  Base Juridica (lei + jurisprudencia + sumulas), R3 Tese (alinhamento
  fato-direito-pedido), R4 Completude (checklist de itens
  obrigatorios). Emite SELO P4 com nivel APROVADA / REVISAR /
  BLOQUEADA. Auto-disparada por TODAS as skills geradoras de peca.
---

# PROTOCOLO-P4-EXECUCAO — Auditoria de Excelencia (R1-R4)

## 1. POR QUE EXISTE

Mitigacao integrada dos 7 cenarios do pre-mortem. Esta skill e o
filtro de qualidade FINAL — toda peca passa por ela antes de chegar
no advogado.

E o mesmo padrao Suprema Corte da familia Adv-OS, adaptado para
execucao/cobranca.

## 2. INPUT

A peca completa gerada pela skill anterior + contexto da sessao
(yaml de `analise-titulo-executivo`, `competencia-*`, etc.).

## 3. OS 4 ROUNDS

### ROUND 1 — COLETA (Premissas)

Verifica se os PRESSUPOSTOS estao presentes na peca:

```markdown
✅/⚠️/🔴 **R1 — COLETA**

- [ ] Tipo de acao identificado e adequado (do `analise-titulo-executivo`)
- [ ] Natureza da relacao (consumo/civil/empresarial) declarada
- [ ] Prazo prescricional verificado (nao prescrita)
- [ ] Mora constituida (ex re automatica OU notificacao comprovada)
- [ ] Calculo de atualizacao com formula + fonte indicada
- [ ] Foro indicado coerente com `competencia-territorial` (rank 1-3)
- [ ] Juizo correto coerente com `competencia-funcional`
- [ ] Qualificacao completa das partes (CPF/CNPJ, endereco)
```

### ROUND 2 — BASE JURIDICA (Lei + Jurisprudencia)

Confere se a fundamentacao legal e robusta:

```markdown
✅/⚠️/🔴 **R2 — BASE JURIDICA**

- [ ] Todos os artigos do CPC citados estao corretos (verificar inciso/
      paragrafo)
- [ ] Lei especial aplicavel citada (Cheque/Duplicata/LUG/CDC/Locacao
      conforme caso)
- [ ] Sumulas STJ aplicaveis citadas (especialmente 247, 282, 299, 384,
      503, 504, 531 para monitorias)
- [ ] Sumulas STF aplicaveis citadas (282, 356, 636, 640 para
      RE/recursos superiores)
- [ ] Pre-questionamento expresso se peca for prelim. de REsp/RE
- [ ] Jurisprudencia citada (se houver) tem URL/fonte validavel
      (cross-check com plugin juris-adv-os se disponivel)
```

### ROUND 3 — TESE (Alinhamento fato-direito-pedido)

Verifica alinhamento interno:

```markdown
✅/⚠️/🔴 **R3 — TESE**

- [ ] Narrativa dos fatos suporta CADA pedido formulado
- [ ] Fundamentacao juridica explica POR QUE o pedido cabe
- [ ] Pedidos estao expressos, claros e CERTOS (CPC art. 322)
- [ ] Valor da causa coerente com pedido (CPC art. 291)
- [ ] Cumulacao de pedidos (se houver) respeita compatibilidade
      (CPC art. 327)
- [ ] Reconvencao (se houver) tem pedido proprio e valor
- [ ] Producao de provas requerida de forma generica E especifica
- [ ] Honorarios sucumbenciais pedidos no patamar correto (10-20%
      regra; 5% pagamento monitorio cumprido; menores em JEC 1o grau)
```

### ROUND 4 — COMPLETUDE (Checklist obrigatorio)

```markdown
✅/⚠️/🔴 **R4 — COMPLETUDE**

ITENS OBRIGATORIOS DA PECA:

- [ ] Endereçamento correto (juizo + comarca + UF)
- [ ] Identificacao das partes COMPLETA
- [ ] Tipo da acao mencionado no titulo da peca
- [ ] Tempestividade demonstrada (se recurso/defesa)
- [ ] Preliminares antes do merito (se aplicavel)
- [ ] Bloco de fatos
- [ ] Bloco de direito
- [ ] Bloco de pedidos
- [ ] Valor da causa indicado
- [ ] Lista de documentos anexos
- [ ] Local e data
- [ ] Assinatura do advogado + OAB
- [ ] Aviso de revisao humana obrigatoria (no output final)
```

## 4. VEREDITO P4

Cada round recebe um status:

| Status | Quando |
|--------|--------|
| ✅ APROVADO | Todos os checks passaram |
| ⚠️ REVISAR | 1-3 checks com ressalvas |
| 🔴 BLOQUEADO | 4+ checks falhos OU 1 critico falho |

**Verdito final consolidado:**

| Combinação | Selo P4 final |
|------------|---------------|
| R1-R4 todos ✅ | ✅ APROVADA — pronta para revisao humana final |
| R1-R4 com 1-2 ⚠️ | 📝 REVISAR — corrigir antes de protocolar |
| R1-R4 com qualquer 🔴 OU 3+ ⚠️ | 🚫 BLOQUEADA — pendente ajuste antes de novo P4 |

## 5. OUTPUT FINAL

Sempre devolva, ao fim da peca:

```markdown
---

## ⚖️ SELO P4 — Auditoria Suprema Corte

| Round | Status | Observacoes |
|-------|--------|-------------|
| R1 — Coleta | ✅/⚠️/🔴 | [pontos especificos se nao ✅] |
| R2 — Base Juridica | ✅/⚠️/🔴 | [pontos especificos] |
| R3 — Tese | ✅/⚠️/🔴 | [pontos especificos] |
| R4 — Completude | ✅/⚠️/🔴 | [pontos especificos] |

**VEREDITO FINAL:** ✅ APROVADA | 📝 REVISAR | 🚫 BLOQUEADA

[Se ✅:]
Pronta para revisao humana final. Conferir documentos anexos +
calculos + clausulas contratuais especificas. Validar em fonte
oficial os dispositivos legais citados.

[Se 📝:]
Pontos a corrigir antes de protocolar:
- [item especifico]
- [item especifico]

[Se 🚫:]
Bloqueios criticos:
- [item bloqueador]
- [item bloqueador]

NAO PROTOCOLAR sem nova passagem pelo P4.

---

⚠️ **AVISO LEGAL:** Esta auditoria e assistida por IA. A conferencia
humana final, especialmente do calculo, clausulas contratuais,
documentos anexos e pertinencia ao caso concreto, e responsabilidade
exclusiva do advogado antes de protocolar.
```

## 6. PROIBICOES

1. NAO emitir ✅ APROVADA se faltar qualquer item critico de R1 ou R3.
2. NAO ocultar 🔴 — sinalize destacado no relatorio.
3. NAO autoaprovar — sempre fazer os 4 rounds explicitamente.
4. NAO esquecer do aviso legal final.
