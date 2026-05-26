---
name: calculo-atualizacao-monetaria
description: >
  CALCULO-ATUALIZACAO-MONETARIA — Estrutura a memoria de calculo da
  divida para fins judiciais. NUNCA gera valores finais com indices
  hardcoded (anti-halucinacao por design). Identifica tabela aplicavel
  (TJSP, TJPR, TJRS, TJ-X, CJF para Justica Federal, STJ), termo
  inicial e final, composicao (correcao + juros mora + multa contratual
  + honorarios), e gera planilha estruturada com FORMULA pronta. O
  advogado preenche indices da tabela oficial atual. Use sempre que
  for necessario quantificar divida judicialmente.
---

# CALCULO-ATUALIZACAO-MONETARIA — Memoria de Calculo Estruturada

## 1. REGRA DURA — ZERO INDICE HARDCODED

**Nao gere valores finais usando indices que voce "lembra".** Voce
tem cutoff de Janeiro/2026; qualquer indice posterior e alucinacao.
Mesmo indices anteriores podem ter sido revisados.

A skill produz **estrutura + formula + fontes oficiais a consultar**.
O advogado preenche.

Mitigacao do cenario 2 do pre-mortem (cliente perdeu R$ 80k em
calculo errado).

---

## 2. INPUT NECESSARIO

Do contexto + perguntar:

1. **Tipo da acao** (do `analise-titulo-executivo`).
2. **Valor principal nominal e data do principal** (ex: R$ 100.000 em
   15/03/2022).
3. **Termo inicial da mora** (do `notificacao-extrajudicial-mora` ou
   ex re).
4. **Data ate quando atualizar** (geralmente data prevista de
   ajuizamento ou hoje).
5. **Existe multa contratual?** Percentual e momento de incidencia.
6. **Juros pactuados ou legais?** Se pactuados, qual percentual ao mes?
7. **Tribunal de destino** (TJSP, TJPR, TJRS, TJ-X, JF, STJ etc.) —
   define tabela a aplicar.

---

## 3. COMPOSICAO DO CALCULO

Calculo judicial tipico = 5 elementos:

1. **Principal** (valor original nominal)
2. **Correcao monetaria** (perda do poder de compra — indice oficial)
3. **Juros de mora** (sancao pelo atraso)
4. **Multa contratual** (se houver clausula)
5. **Honorarios advocaticios** (sucumbenciais — fixados em sentenca,
   nao no calculo do credor)

### 3.1 Indices de correcao monetaria — tabelas oficiais

| Tribunal/Juizo | Tabela aplicavel | Onde consultar |
|----------------|------------------|----------------|
| TJSP | Tabela pratica do TJSP | tjsp.jus.br/PaginaInicial/Tabela/Calculo |
| TJPR | Tabela do CGJ-PR | tjpr.jus.br |
| TJRS | Tabela do TJRS (URV / IGPM / IPCA-E) | tjrs.jus.br |
| TJMG | Tabela do TJMG | tjmg.jus.br |
| TJRJ | Tabela do TJRJ | tjrj.jus.br |
| Justica Federal | Tabela do CJF (Conselho da Justica Federal) | cjf.jus.br |
| STJ / multas STJ | Tabela do STJ | stj.jus.br |
| Trabalhista (CLT) | Tabela do CSJT | csjt.jus.br |

### 3.2 Juros de mora — base legal

| Caso | Taxa |
|------|------|
| Pactuado em contrato (capitalizacao mensal vedada se nao pactuada — Sum. 539 STJ em consumo bancario) | Conforme contrato |
| Nao pactuado, civis (CC art. 406) | Taxa SELIC (entendimento dominante STJ — EREsp 1.207.197) |
| Em obrigacoes civis pre-CC/02 | 0,5% ao mes (CC/16) ou 1% ao mes (regra geral) |
| Em consumo abusivo | Limitacao (CDC art. 51 IV) |

### 3.3 Multa contratual

Se houver clausula penal: percentual sobre o valor principal corrigido
(usualmente 2-10%). Para clausulas penais excessivas, juiz pode
reduzir (CC art. 413).

---

## 4. OUTPUT — PLANILHA ESTRUTURADA (zero indice hardcoded)

```markdown
## Memoria de calculo — [identificacao do caso]

**Atencao:** este calculo apresenta a ESTRUTURA + FORMULA. Os indices
numericos devem ser preenchidos pelo advogado a partir da **tabela
oficial vigente do tribunal de destino**. Esta skill nao tem acesso
a indices posteriores a Jan/2026, e mesmo periodos anteriores podem
ter sido revistos por norma do CNJ/CJF.

---

### Premissas

| Campo | Valor |
|-------|-------|
| Tipo da acao | [execucao / monitoria / cobranca] |
| Tribunal de destino | [TJSP / TJPR / TJRS / etc.] |
| Tabela aplicavel | [link/nome] |
| Principal nominal | R$ [valor] em [data] |
| Termo inicial mora | [data] |
| Termo final calculo | [data] |
| Juros pactuados? | [sim, X% am / nao] |
| Multa contratual? | [sim, X% / nao] |

---

### Tabela 1 — Atualizacao do principal

| Periodo (mes/ano) | Indice [TABELA] | Acumulado | Valor corrigido |
|-------------------|-----------------|-----------|-----------------|
| [mes inicial] | _________ | 1,000000 | R$ [principal] |
| [mes seguinte] | _________ | _________ | _________ |
| ... | _________ | _________ | _________ |
| [mes final] | _________ | _________ | **R$ ___** |

**Formula:** principal_corrigido = principal × (acumulado_final / acumulado_inicial)

**FONTE OBRIGATORIA:** [URL da tabela oficial do tribunal]

---

### Tabela 2 — Juros de mora

| Periodo | Meses | Taxa | Juros do periodo |
|---------|-------|------|------------------|
| [data inicio mora] -> [data fim] | [N] | [X% am ou SELIC mensal] | R$ ___ |

**Formula simples (juros nao capitalizados):**
juros = principal_corrigido × taxa_mensal × meses

**Formula composta (apenas se pactuada — Sum. 539 STJ):**
juros = principal_corrigido × ((1+taxa)^meses - 1)

**FONTE OBRIGATORIA SELIC:** receita.fazenda.gov.br / bcb.gov.br

---

### Tabela 3 — Multa contratual (se houver)

multa = principal_corrigido × [percentual_clausula] / 100

Observacao: se clausula penal exceder 10%, considerar reducao judicial
(CC art. 413).

---

### Totalizacao

| Verba | Valor |
|-------|-------|
| Principal corrigido | R$ ___ |
| Juros de mora | R$ ___ |
| Multa contratual | R$ ___ |
| **TOTAL ATE [data]** | **R$ ___** |

Valor sera atualizado ate a data do efetivo pagamento.

---

### Anexos exigidos pela peticao

1. Esta memoria de calculo (planilha)
2. Tabela oficial do tribunal de destino (impressao ou referencia)
3. Demonstrativo bancario SELIC do periodo (se aplicavel)
4. Comprovante do contrato/titulo com clausulas de juros e multa
```

---

## 5. AVISOS OBRIGATORIOS NO OUTPUT FINAL

```
⚠️ VALIDACAO OBRIGATORIA ANTES DE PROTOCOLAR:

1. Conferir indices contra a tabela OFICIAL ATUAL do tribunal
   [link especifico] — esta skill NAO tem acesso a indices
   posteriores a Janeiro/2026.

2. Conferir taxa SELIC mensal contra publicacao do Bacen
   ou tabela CJF — taxa flutua mensalmente.

3. Se relacao de consumo: revisar juros e multa contra CDC art. 51 IV
   (clausulas abusivas).

4. Se contrato bancario: revisar capitalizacao contra Sum. 539 STJ
   e contra clausula contratual expressa.

5. O calculo final tem efeito vinculante na execucao
   (CPC art. 524). Excesso pode gerar embargos por excesso de
   execucao (CPC art. 525 §1º V), com possibilidade de redirecionamento
   de honorarios contra o exequente.
```

---

## 6. PROIBICOES

1. **NUNCA gerar valor final.** So formula + fonte.
2. **NUNCA citar indice especifico numerico** (ex: "IPCA-E de
   julho/2025 = 0,28%"). Sempre placeholder `_____`.
3. **NUNCA assumir capitalizacao composta sem clausula expressa.**
4. **NUNCA omitir o aviso de validacao final** (item 5 acima).
