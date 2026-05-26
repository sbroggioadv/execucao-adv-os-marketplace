---
name: analise-titulo-executivo
description: >
  ANALISE-TITULO-EXECUTIVO — Skill fundacional do plugin execucao-adv-os.
  Classifica o documento trazido pelo advogado (cheque, nota promissoria,
  duplicata, contrato, NF, boleto, e-mail, multa contratual) cruzando com
  os requisitos do art. 784 CPC, lei especial aplicavel, prazo
  prescricional, e natureza da relacao (consumo/civil/empresarial/locaticia).
  Emite veredito triplo: acao cabivel (execucao / monitoria / cobranca
  ordinaria) + probabilidade de exito + alternativa. SEMPRE primeira skill
  acionada pelo execucao-master em cada caso novo. Use quando o usuario
  trouxer titulo, contrato, divida, ou pedir analise do caso.
---

# ANALISE-TITULO-EXECUTIVO — Classificacao e Roteamento Inicial

## 1. PAPEL NO PLUGIN

Esta skill **abre TODO caso** atendido pelo `execucao-adv-os`. Sua saida
alimenta o contexto da sessao que TODAS as outras skills vao ler:

- Tipo de acao recomendada (execucao / monitoria / cobranca)
- Natureza da relacao (consumo / civil / empresarial / locaticia)
- Prazo prescricional ativo
- Mora ex re ou ex persona
- Eventual relacao de consumo (acende CDC)

Sem esta skill rodada, nenhuma peca pode ser gerada. O orquestrador
`execucao-master` bloqueia avanco se faltar.

---

## 2. INPUT MINIMO OBRIGATORIO

Pergunte ao usuario (em UMA passagem, depois proceda):

1. **Documento(s) que sustenta(m) o credito.** Tipo + estado fisico
   (original / copia / digital / com firma / com testemunhas / sem).
2. **Valor da divida + data do vencimento.**
3. **Partes:** credor (PF/PJ, atividade), devedor (PF/PJ).
4. **Natureza da relacao** se nao for obvio (consumo, civil, empresarial,
   locaticia, trabalhista, etc.).
5. **Houve notificacao previa?** Se sim, comprovante.

Se o usuario nao tiver alguma info, registre como **lacuna**.

---

## 3. MATRIZ DE CLASSIFICACAO

### 3.1 Cheque

| Requisito | Verificacao |
|-----------|-------------|
| **Art. 784 I CPC** + Lei 7.357/85 | Cheque assinado, com data, valor, e prazo de apresentacao ja vencido |
| **Acao executiva** | Sim, ate **6 meses** apos prazo de apresentacao (30 dias mesma praca / 60 dias diferente) |
| **Acao monitoria** | Apos 6 meses do prazo de apresentacao ate 5 anos (Sum. 503 STJ) |
| **Acao de cobranca/locupletamento** | Apos 5 anos (art. 61 Lei do Cheque) |

### 3.2 Nota Promissoria (NP)

| Requisito | Verificacao |
|-----------|-------------|
| **Art. 784 I CPC** + Decreto 2.044/1908 + LUG | Assinada, com data, valor por extenso, identificacao do beneficiario e emitente |
| **Acao executiva** | Sim, prazo prescricional de **3 anos** do vencimento (LUG art. 70) |
| **Acao monitoria** | Apos 3 anos ate 5 anos (Sum. 504 STJ) |

### 3.3 Duplicata

| Requisito | Verificacao |
|-----------|-------------|
| **Art. 784 I CPC** + Lei 5.474/68 | Duplicata aceita (com aceite expresso) OU protestada com comprovante de entrega da mercadoria/servico |
| **Acao executiva** | Sim. Aceita: 3 anos. Nao aceita: 3 anos + protesto + comprovante entrega |
| **Acao monitoria** | Apos 3 anos OU duplicata sem aceite sem protesto |

### 3.4 Contrato

| Requisito | Verificacao |
|-----------|-------------|
| **Art. 784 III CPC** | Contrato particular assinado pelo devedor **+ 2 testemunhas** |
| **Acao executiva** | Sim, **se houver testemunhas**. Prescricao: CC art. 206 §5º I (5 anos divida liquida em instrumento publico/particular) |
| **Acao monitoria (Sum. 247 STJ)** | Contrato **sem testemunhas** mas com prova escrita da divida |
| **Acao de cobranca ordinaria** | Quando nao houver prova escrita suficiente |

### 3.5 Nota Fiscal + Boleto

| Requisito | Verificacao |
|-----------|-------------|
| **Sem aceite formal** | NAO e titulo executivo. NF isoladamente nao executa |
| **Acao monitoria** | Sim — NF + comprovante de entrega + boleto = prova escrita da divida |
| **Acao de cobranca** | Alternativa se faltar prova de entrega |

### 3.6 Multa Contratual

| Requisito | Verificacao |
|-----------|-------------|
| **Liquida e exigivel?** | Se contrato com clausula penal liquida + clausula que torna divida ipso facto: pode integrar execucao do proprio contrato |
| **Iliquida** | Acao de cobranca com liquidacao (arbitramento) |

---

## 4. ARVORE DE DECISAO — SAIDA OBRIGATORIA

Apos analisar o(s) documento(s), produza:

```markdown
## Classificacao do titulo — [tipo do documento]

**Documento trazido:** [descricao breve]
**Valor:** R$ [valor]
**Vencimento:** [data]
**Estado prescricional:** [vivo / em risco / prescrito — com data limite]

### Requisitos do art. 784 CPC

- [ ] (item especifico)
- [ ] (item especifico)
- [ ] (item especifico)

### Veredito

🥇 **ACAO RECOMENDADA:** [Execucao | Monitoria | Cobranca ordinaria]
   - **Probabilidade de exito processual:** [alta / media / baixa]
   - **Razao:** [explicacao em 2-4 linhas]

🥈 **ALTERNATIVA:** [se aplicavel]
   - **Quando vale:** [condicao]

🚫 **CAMINHOS DESCARTADOS:** [com motivo]

### Contexto que sera propagado para outras skills

```yaml
caso:
  tipo_acao: [execucao | monitoria | cobranca]
  natureza_relacao: [consumo | civil | empresarial | locaticia | trabalhista]
  cdc_aplicavel: [true | false]
  mora_tipo: [ex_re | ex_persona | iliquida]
  prescricao:
    prazo_anos: [N]
    data_limite: [YYYY-MM-DD]
    status: [vivo | em_risco | prescrito]
  legislacao_chave:
    - [CPC art. X]
    - [Lei Y]
    - [Sum. Z STJ]
```

### Proximo passo

[Se mora ex_persona e ainda nao notificou: rodar notificacao-extrajudicial-mora]
[Se mora ex_re ou ja notificou: pular pra competencia-territorial]
```

---

## 5. CASOS DE CONSUMO — REGRA CRITICA

Se a parte devedora for **pessoa fisica** e o credor for **empresa em
atividade habitual**, presuma relacao de consumo ate prova em contrario
(CDC art. 2º e 3º). Isso ativa:

- Foro do consumidor (CDC art. 101 I) — afeta `competencia-territorial`
- Inversao do onus (CDC art. 6º VIII)
- Vedacao cobranca vexatoria (CDC art. 42)
- Limitacao a juros pactuados (CDC art. 51 IV)

**Marque no contexto `cdc_aplicavel: true` para que `peticao-inicial-*`
ajuste a peca automaticamente.**

---

## 6. PROIBICOES ABSOLUTAS

1. **Nao recomendar execucao** se faltar requisito formal do art. 784. Em
   duvida, recomende monitoria (mais segura).
2. **Nao ignorar prescricao em risco.** Se faltam <90 dias para prescricao,
   marque ⚠️ destaque no veredito e priorize protocolo imediato.
3. **Nao classificar como NAO-CONSUMO** sem checar habitualidade do credor.
4. **Nao prosseguir** sem completar a saida estruturada (yaml de contexto).
5. **Nao sugerir** valor de honorarios ou estrategia comercial — foco
   tecnico apenas.
