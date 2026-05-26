---
name: peticao-inicial-execucao
description: >
  PETICAO-INICIAL-EXECUCAO — Gera peticao inicial de execucao de titulo
  extrajudicial conforme CPC arts. 319, 798-805. Le contexto da sessao
  produzido por analise-titulo-executivo, competencia-territorial,
  competencia-funcional e calculo-atualizacao-monetaria. Aplica CDC se
  contexto marcou consumo. Inclui requerimentos de citacao, penhora,
  arresto, e medidas de cooperacao. BLOQUEADA se Tiers 1-2 nao foram
  rodadas. Use quando o usuario confirmar acao executiva apos analise.
---

# PETICAO-INICIAL-EXECUCAO — Inicial Executiva Completa

## 1. PRE-REQUISITOS BLOQUEANTES

Antes de gerar, valide que rodaram NESTA sessao:

- [ ] `analise-titulo-executivo` (decidiu execucao como acao cabivel)
- [ ] `competencia-territorial` (foro escolhido)
- [ ] `competencia-funcional` (JEC ou Comum)
- [ ] `notificacao-extrajudicial-mora` se contexto exigiu (ex_persona)
- [ ] `calculo-atualizacao-monetaria` (memoria de calculo pronta)

Se faltar **qualquer** item: PARE e indique ao usuario qual skill rodar
antes.

---

## 2. ESTRUTURA OBRIGATORIA DA INICIAL DE EXECUCAO

### 2.1 Endereçamento

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DA [Vara] DA COMARCA DE
[cidade] / ESTADO DE [UF]

[OU se JF: EXCELENTISSIMO SENHOR DOUTOR JUIZ FEDERAL DA [N] VARA FEDERAL
DA [Secao Judiciaria] / ESTADO DE [UF]]

[OU se JEC: EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DO JUIZADO
ESPECIAL CIVEL DA COMARCA DE [cidade] / ESTADO DE [UF]]
```

### 2.2 Qualificacao das partes (CPC art. 319 II, IV)

```
[NOME EXEQUENTE], [nacionalidade], [estado civil], [profissao], inscrito
no CPF/CNPJ sob n. [XXX.XXX.XXX-XX], com endereco profissional/residencial
em [endereco completo], por meio de seu(s) advogado(s) que esta(o)
firmando esta peticao (procuracao anexa), vem, respeitosamente, perante
V.Exa, ajuizar a presente

AÇÃO DE EXECUCAO DE TITULO EXTRAJUDICIAL

em face de

[NOME EXECUTADO], [qualificacao completa], inscrito no CPF/CNPJ sob n.
[XXX], com endereco em [completo], pelas razoes de fato e fundamentos
de direito a seguir expostos.
```

### 2.3 Dos fatos

Narrativa enxuta (3-8 paragrafos):
- Origem da divida (contrato/titulo)
- Vencimento e inadimplemento
- Tentativas de cobranca / notificacao extrajudicial (citar o
  documento gerado pela skill `notificacao-extrajudicial-mora`)
- Atualizacao apurada (citar memoria de calculo)

### 2.4 Do direito

Bloco fundamentado:

```markdown
1. **Titulo executivo extrajudicial** — O documento que sustenta a
   presente acao se enquadra perfeitamente no rol do art. 784 do CPC
   (inciso I/II/III/etc., conforme o caso), preenchendo todos os
   requisitos exigidos pela legislacao especifica
   ([Lei do Cheque 7.357/85 / LUG e Decreto 2.044/08 / Lei das
   Duplicatas 5.474/68 / etc.]).

2. **Liquidez, certeza e exigibilidade** — O titulo apresenta valor
   determinado, beneficiario identificado, data de vencimento ja
   transcorrida, e mora constituida [automaticamente nos termos do
   art. 397 caput CC / mediante notificacao extrajudicial protocolada
   em [data], conforme documento anexo].

3. **Competencia** — A presente acao e proposta no foro de [comarca]
   com fundamento em [CPC art. 781 I/II/III / CDC art. 101 I / clausula
   de eleicao art. 63 CPC], conforme analise estruturada anexa.

4. **Atualizacao do credito** — A divida foi atualizada conforme
   memoria de calculo anexa, aplicando-se [tabela oficial do TJ-X /
   CJF / etc.] no periodo de [data inicial] ate [data limite], com
   juros de mora de [taxa] e [multa de N%, se houver].

[Se CDC aplicavel:]
5. **Relacao de consumo** — Aplicam-se os arts. 6º VIII, 42 e 51 IV do
   CDC, com observancia ao foro do consumidor (art. 101 I) e veda-se
   qualquer cobranca vexatoria.
```

### 2.5 Dos requerimentos (CPC art. 798)

```markdown
Diante do exposto, REQUER-SE:

a) A CITACAO do executado para, no prazo de **3 (tres) dias**,
   efetuar o pagamento da divida acrescida dos honorarios advocaticios
   (CPC art. 829);

b) Em caso de pagamento integral no prazo, a fixacao dos honorarios
   advocaticios em **10%** sobre o valor da divida (CPC art. 827 §1º);

c) Em caso de NAO pagamento no prazo, a PENHORA E AVALIACAO de tantos
   bens quantos bastem para garantir a execucao (CPC art. 829 §1º),
   priorizando:
   - Dinheiro em deposito ou aplicacao financeira (CPC art. 854 —
     SISBAJUD)
   - Veiculos automotores (RENAJUD)
   - Imoveis (CCS-Bacen e SREI)
   - Outros bens conforme art. 835 CPC

d) Caso a citacao seja frustrada, a expedicao de ARRESTO sobre tantos
   bens do executado quanto bastem para garantir a execucao (CPC
   art. 830 e 831), com posterior conversao em penhora apos efetivada
   a citacao;

e) A condenacao do executado ao pagamento das CUSTAS processuais e
   HONORARIOS sucumbenciais em **20%** sobre o valor da execucao
   (CPC art. 85 §2º), majorados em caso de embargos (CPC art. 827 §2º);

f) Em caso de localizacao de bens, a expedicao dos competentes
   mandados/ordens nos sistemas eletronicos SISBAJUD, RENAJUD,
   INFOJUD, CNIB.

[Se houver pedido de tutela de urgencia (arresto, indisponibilidade):
g) Os pedidos especificos do skill `pedido-tutela-urgencia`.]
```

### 2.6 Das provas

```markdown
Junta-se a presente:

1. Procuracao
2. Comprovantes de pagamento de custas (ou requerimento de gratuidade)
3. Titulo executivo extrajudicial original ou copia autenticada
4. Demonstrativo do debito atualizado (memoria de calculo)
5. Notificacao extrajudicial protocolada e respectivo comprovante
   (se aplicavel)
6. Documentos de identificacao das partes
7. Certidoes negativas/positivas conforme o caso
8. Demais documentos relevantes
```

### 2.7 Do valor da causa

```
Da-se a causa o valor de **R$ [valor da divida atualizada]**,
correspondente ao montante atualizado da execucao ate [data].
```

### 2.8 Fechamento

```
Termos em que,
Pede deferimento.

[cidade], [data].

________________________________________
[NOME DO ADVOGADO]
OAB/[UF] [numero]
```

---

## 3. ADAPTACOES POR TIPO DE TITULO

### Cheque
- Citar Lei 7.357/85 explicitamente.
- Anexar cheque original ou copia frente-verso.
- Comprovar protesto ou apresentacao bancaria com recusa.

### Nota Promissoria
- Citar LUG (Decreto 57.663/66) + Decreto 2.044/08.
- Verificar requisitos formais (denominacao, data, lugar, beneficiario,
  assinatura).

### Duplicata
- Lei 5.474/68. Se sem aceite: protesto + comprovante de entrega.

### Contrato com testemunhas
- CPC art. 784 III. Confirmar 2 testemunhas qualificadas.

---

## 4. APOS GERAR A INICIAL

**Auto-disparar `protocolo-p4-execucao`** para auditoria de excelencia
antes de entregar ao usuario.

Output final inclui aviso:

```
⚠️ REVISAR ANTES DE PROTOCOLAR:
- Conferir indices da memoria de calculo contra tabela oficial atual
- Conferir endereco completo das partes (validar via CPF/CNPJ)
- Anexar TODOS os documentos listados
- Conferir clausula de eleicao se aplicavel
- Validacao final humana e obrigatoria (CFR. licenca do plugin)
```

---

## 5. PROIBICOES

1. Nao gerar inicial se Tiers 1-2 nao rodaram nesta sessao.
2. Nao inventar artigo do CPC. Em duvida, deixar placeholder.
3. Nao chutar valor ou indice — sempre da memoria de calculo.
4. Nao omitir aviso final de revisao humana.
5. Nao bipassar `protocolo-p4-execucao`.
