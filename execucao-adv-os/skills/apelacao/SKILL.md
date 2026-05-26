---
name: apelacao
description: >
  APELACAO — Recurso contra sentenca proferida em Justica COMUM (CPC
  arts. 1.009-1.014). Prazo: 15 dias uteis. **GATE OBRIGATORIO no
  inicio:** se o contexto indica JEC (competencia-funcional), STOP e
  ative recurso-inominado-jec. Apelacao NAO se aplica ao JEC. Aplica
  efeitos suspensivos e devolutivos amplos. Use quando houver sentenca
  da Justica Comum a recorrer.
---

# APELACAO — Recurso contra Sentenca (Justica Comum)

## 1. ⚠️ GATE BLOQUEADOR — JEC vs COMUM

**ANTES de qualquer linha desta skill:**

Verifique o contexto da sessao:
```yaml
competencia_funcional:
  juizo: ?
  recurso_sentenca: ?
```

Se `juizo == jec` OU `recurso_sentenca == recurso_inominado`:

> **🛑 STOP.** Apelacao NAO se aplica ao JEC. O recurso correto e
> RECURSO INOMINADO (Lei 9099 art. 41). Ative a skill
> `recurso-inominado-jec`. Esta skill foi interrompida.

Se nao houver contexto, **pergunte explicitamente ao usuario** se a
acao tramita em JEC ou Justica Comum.

Cenario 5 do pre-mortem — recurso intempestivo por confusao JEC.

## 2. CABIMENTO E PRAZO

- **Cabe:** contra sentenca terminativa ou definitiva em 1o grau
  (CPC art. 1.009).
- **Prazo:** **15 dias uteis** da intimacao (CPC art. 1.003 §5º +
  art. 219).
- Interposicao via peca propria endereçada ao **juizo de 1o grau**
  (mas razoes endereçadas ao **Tribunal**).

## 3. EFEITOS — REGRA GERAL: SUSPENSIVO + DEVOLUTIVO (CPC art. 1.012)

A apelacao tem, por regra, efeito SUSPENSIVO automatico — a sentenca
nao produz efeitos ate o julgamento. EXCECOES (sem suspensivo) — art.
1.012 §1º:

- Homologa divisao/demarcacao
- Condena pagamento de alimentos
- Confirma/concede/revoga tutela provisoria
- Decreta interdicao
- Sentenca arbitral
- Procedente pedido instituidor da arbitragem
- Concede divorcio

E o art. 1.012 §3º permite a parte requerer atribuicao de efeito
suspensivo a apelacoes que nao o tenham por lei.

## 4. ESTRUTURA

### 4.1 Peca de interposicao (1a peca, dirigida ao juizo a quo)

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DA [Vara] DA COMARCA DE
[cidade] — Processo n. [numero]

[NOME APELANTE], ja qualificado nos autos da [acao] em epigrafe, vem
INTERPOR

RECURSO DE APELAÇÃO

em face da r. sentenca de fls. [...], pelas razoes anexas, que devera
ser remetida ao Egregio Tribunal de Justica de [UF] para apreciacao.

REQUER-SE:
a) Recebimento do recurso em seu duplo efeito legal (CPC art. 1.012);
b) Em sendo o caso, atribuicao de efeito suspensivo (CPC art. 1.012
   §3º) — [fundamentar];
c) Apos contrarrazoes do apelado, remessa dos autos ao TJ.

[Local e data]
________________________________________
[NOME DO ADVOGADO]
OAB/[UF] [numero]
```

### 4.2 Razoes (peca anexa, dirigida ao TJ)

```markdown
EGREGIO TRIBUNAL DE JUSTICA DO ESTADO DE [UF]
COLENDA [CAMARA — se conhecida, ou "DISTRIBUICAO"]

Apelante: [NOME]
Apelado: [NOME]
Processo: [numero] — [Vara] de [comarca]

# RAZÕES DE APELAÇÃO

## I — Da Tempestividade
Sentenca publicada em [data]; prazo de 15 dias uteis terminaria em
[data]. **TEMPESTIVA.**

## II — Do Cabimento
Cabivel apelacao na forma do art. 1.009 do CPC, contra sentenca que
[julgou procedente / improcedente / extinguiu sem resolucao].

## III — Da Sintese da Demanda
[3-6 paragrafos resumindo a acao, principais argumentos, prova
produzida.]

## IV — Da Sintese da Sentenca Recorrida
[2-4 paragrafos com o que a sentenca decidiu e como fundamentou.]

## V — Das Razoes de Reforma

### 1. [Materia A — ex: Erro na valoracao da prova]

[exposicao detalhada]

[fundamentacao legal + jurisprudencia]

### 2. [Materia B — ex: Aplicacao indevida do CDC]

[...]

### 3. [Materia C — ex: Honorarios mal arbitrados]

[...]

[Pre-questionamento de materias federais/constitucionais para
eventual REsp/RE futuro — citar arts. 1.025 CPC e dispositivos
especificos.]

## VI — Pedidos

REQUER-SE:

a) CONHECIMENTO e PROVIMENTO do recurso para REFORMAR integralmente
   a r. sentenca recorrida, julgando-se:
   i) [pedido novo, conforme tese]
   ii) [pedidos subsidiarios se cabiveis]

b) SUBSIDIARIAMENTE, [se cabivel: reducao de honorarios, anulacao por
   nulidade, etc.];

c) Inversao dos onus sucumbenciais;

d) Producao das provas porventura necessarias na instancia recursal.

[Local e data]
________________________________________
[NOME DO ADVOGADO]
OAB/[UF] [numero]
```

## 5. CONTRARRAZOES

Se a parte for INTIMADA de apelacao adversa: prazo de 15 dias uteis
(CPC art. 1.010 §1º) para apresentar contrarrazoes. Mesma estrutura
da razao, mas defendendo a sentenca.

## 6. APELACAO PARCIAL VS TOTAL

- **Total:** ataca tudo da sentenca.
- **Parcial:** ataca so parte. Cuidar do trânsito em julgado parcial.

## 7. PROIBICOES

1. **NUNCA gerar apelacao se contexto e JEC** — recurso inominado.
2. Nao confundir prazo (15 uteis, comum) com 10 corridos (JEC).
3. Nao omitir pre-questionamento se ha pretensao de REsp/RE.
4. Nao usar apelacao contra interlocutoria — usar agravo de
   instrumento.
5. Auto-disparar `protocolo-p4-execucao`.
