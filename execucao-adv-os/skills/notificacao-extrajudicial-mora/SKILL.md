---
name: notificacao-extrajudicial-mora
description: >
  NOTIFICACAO-EXTRAJUDICIAL-MORA — Constitui o devedor em mora quando
  necessario (obrigacoes ex persona). Classifica os 3 regimes de mora
  (ex re / ex persona / iliquida) por CC arts. 394-401, define via valida
  de notificacao (cartorio TD, AR-MP, edital, plataforma eletronica
  oficial), e gera o instrumento com comprovacao obrigatoria. EMAIL
  SIMPLES e PROIBIDO como unica via. Use SEMPRE em casos onde mora nao
  e ex re (automatica por termo) — auto-disparada por analise-titulo-executivo
  quando o contexto exigir.
---

# NOTIFICACAO-EXTRAJUDICIAL-MORA — Constituicao Valida em Mora

## 1. POR QUE EXISTE

Sem mora constituida validamente, a execucao de titulo extrajudicial
pode ser **extinta sem resolucao de merito** (CPC art. 803 I) por
falta de pressuposto. Cenario 3 do pre-mortem.

A skill garante:
- Tipo de mora correto identificado
- Via de notificacao com comprovacao
- Instrumento juridicamente valido

---

## 2. OS 3 REGIMES DE MORA (CC arts. 394-401)

### REGIME 1 — Mora ex re (automatica)

**Quando:** obrigacao positiva, liquida, com termo certo
(data de vencimento determinada).

**Base legal:** CC art. 397 caput — *"O inadimplemento da obrigacao,
positiva e liquida, no seu termo, constitui de pleno direito em mora
o devedor."*

**Notificacao necessaria?** NAO. A mora e automatica no vencimento.

**Casos tipicos:**
- Cheque (mora desde a apresentacao)
- Nota promissoria com data certa de vencimento
- Boleto bancario com data de vencimento
- Aluguel com data de pagamento estipulada
- Duplicata com vencimento

→ Voce pode pular esta skill e ir direto pra peticao inicial.

### REGIME 2 — Mora ex persona (precisa interpelar)

**Quando:** obrigacao sem termo certo OU obrigacao negativa OU
divida iliquida que precisou ser apurada antes.

**Base legal:** CC art. 397 par. unico — *"Nao havendo termo, a mora
se constitui mediante interpelacao judicial ou extrajudicial."*

**Notificacao necessaria?** **SIM, obrigatoriamente.**

**Casos tipicos:**
- Contrato de prestacao continuada sem termo de inadimplencia automatica
- Reembolso/restituicao sem prazo fixo
- Multa contratual em obrigacao sem termo
- Comodato — devolucao do bem (precisa notificar)
- Honorarios pactuados sem prazo

### REGIME 3 — Mora em obrigacao iliquida (CC art. 405)

Em ato ilicito, a mora corre desde o evento danoso (Sum. 54 STJ — em
responsabilidade extracontratual). Em ilicitos contratuais, segue
regra do art. 397.

Para iliquido contratual: notificacao constitui em mora e fixa termo
para apuracao.

---

## 3. WORKFLOW DECISORIO

### Passo 1 — Classificar a mora aplicavel

Pergunte/extraia:
- Existe data certa de vencimento no titulo? Sim → ex re. Nao → ex persona.
- Obrigacao positiva (pagar) ou negativa (nao fazer)?
- Divida liquida (valor ja determinado) ou iliquida (depende de
  apuracao)?

**Output:**
```yaml
mora:
  tipo: [ex_re | ex_persona | iliquida_extracontratual | iliquida_contratual]
  necessita_notificacao: [true | false]
  termo_inicial_mora: [data — se ex_re | a definir — se ex_persona]
```

### Passo 2 — Se ex_re ou Sum.54: STOP, pular pra proxima skill

Se ja constituido em mora automaticamente, marca o contexto e roteia
para `calculo-atualizacao-monetaria` ou direto pra peticao.

### Passo 3 — Se ex_persona: escolher via valida

| Via | Quando usar | Comprovacao |
|-----|-------------|-------------|
| **Cartorio de Titulos e Documentos** (Lei 6.015/73) | Forma mais segura, foro de qualquer comarca | Certidao do oficial com data |
| **AR Mao-Propria (AR-MP)** | Quando ha endereco certo, mais barata | AR assinado pelo destinatario |
| **Edital** | Devedor em local incerto e ignorado | Publicacao em DJ + jornal local |
| **Plataforma eletronica oficial** | Onde houver previsao contratual ou cartoraria digital | Hash + log de envio |
| **Notificacao judicial** (CPC art. 726-729) | Quando se quer formalidade maxima ou em conjunto com tutela | Mandado cumprido + certidao oficial |

**🚫 PROIBIDO como UNICA via:** e-mail simples, WhatsApp, SMS, ligacao
telefonica. Podem **complementar** as vias acima, nunca substituir.

### Passo 4 — Gerar a notificacao

Modelo basico (adaptar ao caso):

```markdown
# NOTIFICACAO EXTRAJUDICIAL

**De:** [NOME DO CREDOR], [qualificacao completa], por meio de seu
advogado infrafirmado.

**Para:** [NOME DO DEVEDOR], [qualificacao completa], no endereco
[completo].

**Assunto:** Constituicao em mora — [Contrato X / Divida Y]

Pelo presente instrumento, vimos NOTIFICAR V.Sa., na forma do art. 397,
paragrafo unico, do Codigo Civil, e demais dispositivos aplicaveis, para
INFORMAR e EXIGIR o pagamento da divida abaixo discriminada, no prazo
de [N] dias contados do recebimento desta, sob pena das medidas
judiciais cabiveis:

### 1. Origem da obrigacao

[descricao do titulo/contrato/relacao juridica que gerou a divida —
identificacao precisa, data de celebracao, partes, objeto]

### 2. Valor devido

| Verba | Valor |
|-------|-------|
| Principal | R$ [valor] |
| Correcao monetaria ate [data] | R$ [valor] |
| Juros de mora ate [data] | R$ [valor] |
| Multa contratual | R$ [valor] |
| **TOTAL** | **R$ [valor]** |

Valor atualizavel ate a data do efetivo pagamento.

### 3. Forma de pagamento

[Banco / agencia / conta — OU instrucoes especificas]

### 4. Consequencias do nao pagamento

Decorrido o prazo sem pagamento, sera ajuizada a competente acao
[de execucao de titulo extrajudicial | monitoria | de cobranca],
acrescida de honorarios advocaticios sucumbenciais, custas processuais,
custas cartorarias de eventual protesto, e demais consectarios legais.

[cidade], [data].

________________________________________
[NOME DO ADVOGADO]
OAB/[UF] [numero]
```

### Passo 5 — Comprovacao obrigatoria

Output da skill inclui **plano de comprovacao**:

```yaml
comprovacao:
  via_principal: [cartorio_td | ar_mp | edital | plataforma | judicial]
  documento_comprovante: [especifico]
  prazo_estimado_resposta_devedor: [N dias]
  proximo_passo_se_silencio: [acao judicial]
```

---

## 4. AVISOS CRITICOS

1. **Email/WhatsApp/SMS como UNICA via** — nao geram presuncao de
   recebimento juridicamente robusta. Devedor pode alegar que nao
   recebeu. Sempre combine com via formal.
2. **Recusa do destinatario em receber** — em cartorio TD ou AR-MP, a
   recusa pode ser certificada e equivale a notificacao valida (Sum.
   404 STJ aplicada por analogia).
3. **Endereco incerto** — sempre edital + busca em sistemas oficiais
   (Bacenjud, SIEL, etc.) antes de presumir desconhecido.
4. Aguarde o prazo concedido na notificacao antes de ajuizar — ajuizar
   na vespera enfraquece a constituicao em mora.

---

## 5. PROIBICOES

1. Nao gerar notificacao sem identificar tipo de mora aplicavel.
2. Nao recomendar email/WhatsApp como unica via.
3. Nao omitir campo de comprovacao (vai prejudicar prova judicial).
4. Nao fechar a notificacao sem prazo razoavel (3-15 dias e o usual).
