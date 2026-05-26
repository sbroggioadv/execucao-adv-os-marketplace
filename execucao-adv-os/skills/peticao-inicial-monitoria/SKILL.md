---
name: peticao-inicial-monitoria
description: >
  PETICAO-INICIAL-MONITORIA — Gera peticao inicial de acao monitoria
  conforme CPC arts. 700-702, aplicando Sumulas 247, 282, 299, 384,
  503, 504, 531 STJ. Cabivel quando ha prova escrita da divida sem
  forca executiva (contrato sem testemunhas, NF + comprovante de
  entrega, cheque prescrito, NP prescrita, etc.). Le contexto produzido
  pelo Tier 1+2. BLOQUEADA se analise-titulo-executivo nao indicou
  monitoria. Use quando o usuario confirmar acao monitoria.
---

# PETICAO-INICIAL-MONITORIA — Inicial Monitoria Completa

## 1. QUANDO MONITORIA EM VEZ DE EXECUCAO

Monitoria cabe quando o credor tem **prova escrita sem eficacia
executiva** (CPC art. 700). Casos tipicos:

| Documento | Razao |
|-----------|-------|
| Cheque apos 6 meses do prazo de apresentacao | Sum. 503 STJ |
| Nota promissoria apos 3 anos do vencimento | Sum. 504 STJ |
| Contrato **sem 2 testemunhas** | Sum. 247 STJ |
| NF + comprovante entrega de mercadoria/servico | Sum. 299 STJ |
| Cheque prescrito | Sum. 299 STJ |
| Documento gerado por instituicao financeira sem assinatura | Conforme prova escrita |

Pre-requisito: `analise-titulo-executivo` recomendou monitoria.

---

## 2. ESTRUTURA DA INICIAL MONITORIA

### 2.1 Endereçamento

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DA [Vara Civel] DA
COMARCA DE [cidade] / ESTADO DE [UF]
```

### 2.2 Qualificacao

Mesmo padrao da inicial de execucao, ajustando para:

```
ajuizar a presente

AÇÃO MONITORIA

em face de [...]
```

### 2.3 Dos fatos

Narrativa em 3-6 paragrafos:
- Origem da relacao juridica que gerou a divida
- Documentos que comprovam a divida (prova escrita)
- Inadimplemento e atualizacao
- Por que monitoria e nao execucao (citar sumula aplicavel)

### 2.4 Do direito

```markdown
1. **Cabimento da monitoria (CPC art. 700)** — A presente acao se
   funda em prova escrita sem eficacia executiva, na forma do art. 700
   do CPC. [Citar sumula aplicavel: Sum. 247/282/299/384/503/504/531
   STJ conforme o caso].

2. **Prova escrita da divida** — Junta-se [descricao especifica dos
   documentos], que demonstram cabalmente a existencia da obrigacao
   pecuniaria devida pelo requerido.

3. **Liquidez e exigibilidade** — A divida e liquida, no valor de
   R$ [valor], conforme memoria de calculo anexa, e exigivel desde
   [data do vencimento ou da notificacao].

4. **Competencia** — [conforme analise da skill `competencia-territorial`].

[Se CDC aplicavel: bloco sobre relacao de consumo.]
```

### 2.5 Dos requerimentos (CPC art. 701)

```markdown
Diante do exposto, REQUER-SE:

a) A EXPEDICAO de mandado de pagamento (CPC art. 701) ordenando ao
   requerido que, no prazo de **15 (quinze) dias**, efetue o pagamento
   da quantia de **R$ [valor atualizado]**, acrescida de honorarios
   advocaticios de 5%, podendo, no mesmo prazo:
   - **Cumprir o mandado** (pagar) — isencao de custas e honorarios
     reduzidos (CPC art. 701 §1º);
   - **Opor embargos monitorios** — defesa nos proprios autos
     (CPC art. 702);
   - **Manter-se silente** — constituicao DE PLENO DIREITO do titulo
     executivo judicial (CPC art. 701 §2º).

b) Em caso de cumprimento, a fixacao dos honorarios em 5% sobre o
   valor da divida;

c) Em caso de silencio do requerido, a CONVERSAO automatica do mandado
   monitorio em titulo executivo judicial (CPC art. 701 §2º), com
   prosseguimento direto na fase de cumprimento de sentenca (art. 513);

d) A condenacao do requerido ao pagamento das custas e honorarios
   sucumbenciais em **10-20%** sobre o valor da causa (CPC art. 85
   §2º), majoradas em caso de embargos rejeitados (art. 85 §11);

e) Concessao de gratuidade de justica [se aplicavel] OU recolhimento
   das custas anexo.
```

### 2.6 Provas e valor da causa

```markdown
Junta-se:
1. Procuracao
2. Comprovantes/gratuidade
3. **Prova escrita da divida** (documento principal — descrito)
4. Memoria de calculo
5. Notificacao extrajudicial (se aplicavel)
6. Demais documentos pertinentes

Da-se a causa o valor de **R$ [valor atualizado]**.
```

### 2.7 Fechamento

```
Termos em que,
Pede deferimento.

[cidade], [data].

________________________________________
[NOME DO ADVOGADO]
OAB/[UF] [numero]
```

---

## 3. SUMULAS STJ A APLICAR CONFORME O CASO

| Sumula | Conteudo |
|--------|----------|
| 247 STJ | "O contrato de abertura de credito em conta-corrente,
   acompanhado do demonstrativo de debito, constitui documento habil
   para o ajuizamento da acao monitoria." |
| 282 STJ | "Cabe a citacao por edital em acao monitoria." |
| 299 STJ | "E admissivel a acao monitoria fundada em cheque prescrito." |
| 384 STJ | "Cabe acao monitoria para haver saldo remanescente oriundo
   de venda extrajudicial de bem alienado fiduciariamente em garantia." |
| 503 STJ | "O prazo para ajuizamento da acao monitoria em face do
   emitente de cheque sem forca executiva e quinquenal, a contar do
   dia seguinte a data de emissao estampada na cartula." |
| 504 STJ | "O prazo para ajuizamento de acao monitoria em face do
   emitente de nota promissoria sem forca executiva e quinquenal, a
   contar do dia seguinte ao vencimento do titulo." |
| 531 STJ | "Em acao monitoria fundada em cheque prescrito ajuizada
   contra o emitente, e dispensavel a mencao ao negocio juridico
   subjacente a emissao da cartula." |

---

## 4. EFEITOS DA SENTENCA MONITORIA

Tres rotas possiveis apos a citacao do requerido:

1. **Pagamento no prazo** — extincao com o credor recebendo (CPC art.
   701 §1º).
2. **Embargos monitorios** — instaura-se contraditorio. Apos sentenca
   final, ou se transitada favoravel ao credor, vira titulo
   executivo judicial.
3. **Silencio** — constituicao DE PLENO DIREITO do titulo executivo
   judicial (CPC art. 701 §2º), seguindo direto pra cumprimento.

---

## 5. APOS GERAR

- Auto-disparar `protocolo-p4-execucao` para auditoria.
- Aviso final padrao de revisao humana.

---

## 6. PROIBICOES

1. Nao gerar monitoria se `analise-titulo-executivo` indicou execucao.
2. Nao confundir prova escrita com titulo executivo extrajudicial.
3. Nao omitir sumula STJ aplicavel.
4. Nao chutar prazos — sao 15 dias (Cprc art. 701), nao confundir
   com prazos de execucao (3 dias).
