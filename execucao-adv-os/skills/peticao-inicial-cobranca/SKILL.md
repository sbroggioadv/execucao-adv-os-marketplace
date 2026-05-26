---
name: peticao-inicial-cobranca
description: >
  PETICAO-INICIAL-COBRANCA — Gera inicial de acao de cobranca ordinaria
  (procedimento comum, CPC arts. 319-321) ou Juizado Especial Civel
  (Lei 9099). Rota residual quando nao cabe execucao (sem titulo
  executivo) nem monitoria (sem prova escrita suficiente). Le contexto
  produzido pelo Tier 1+2. Adapta procedimento por JEC ou Comum (do
  contexto de competencia-funcional). Use quando o usuario confirmar
  acao de cobranca ordinaria.
---

# PETICAO-INICIAL-COBRANCA — Procedimento Comum ou JEC

## 1. QUANDO COBRANCA EM VEZ DE EXECUCAO/MONITORIA

Quando:
- Nao ha titulo executivo (faltam requisitos do art. 784 CPC).
- Nao ha prova escrita suficiente para monitoria (Sum. 247 STJ).
- Credito precisa ser apurado em fase instrutoria (testemunhal,
  pericial).
- Cliente prefere amplitude probatoria mesmo tendo monitoria/execucao
  disponivel.

---

## 2. ESCOLHA DO PROCEDIMENTO

Pelo contexto de `competencia-funcional`:

| Caminho | Quando |
|---------|--------|
| **JEC (Lei 9099)** | Valor ate 40 SM + autor PF/MEI/ME/EPP + materia compativel |
| **Procedimento comum (CPC)** | Demais casos |

JEC tem peca **mais simples** (pode ser ate por reclamacao verbal,
mas nesta skill produzimos sempre escrita). Comum exige todos os
requisitos do CPC art. 319.

---

## 3. ESTRUTURA DA INICIAL — PROCEDIMENTO COMUM

### 3.1 Endereçamento

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DA [Vara Civel] DA
COMARCA DE [cidade] / ESTADO DE [UF]
```

### 3.2 Qualificacao + tipo da acao

```
[NOME] ajuiza a presente

AÇÃO DE COBRANÇA

em face de [NOME REU], [...].
```

### 3.3 Dos fatos

Narrativa 4-10 paragrafos com:
- Origem da relacao juridica
- Discriminacao da divida
- Tentativas de pagamento extrajudicial
- Notificacao se houve

### 3.4 Do direito

```markdown
1. **Obrigacao certa e exigivel** — Restou demonstrado nos
   documentos juntados que a parte requerida e devedora da quantia
   discriminada, decorrente de [contrato/prestacao de servico/etc.],
   regularmente acordada entre as partes [com previsao expressa de
   prazo, forma de pagamento, etc.].

2. **Inadimplemento** — Conforme [documento/notificacao/correspondencia],
   o requerido [foi notificado / esta em mora] e nao efetuou o
   pagamento, evidenciando o inadimplemento.

3. **Atualizacao do credito** — Aplicando-se [tabela do TJ-X], juros
   de mora de [taxa] e correcao monetaria desde [data], o valor
   atualizado da divida e R$ [valor].

4. **Competencia** — [conforme `competencia-territorial`].

[Se CDC aplicavel: bloco sobre relacao de consumo.]
```

### 3.5 Requerimentos (CPC art. 319 VI)

```markdown
Diante do exposto, REQUER-SE:

a) A CITACAO do requerido para, no prazo legal, contestar a presente
   acao, sob pena de revelia e confissao quanto a materia de fato
   (CPC art. 344);

b) A designacao de AUDIENCIA DE CONCILIACAO/MEDIACAO (CPC art. 334);

c) A produçao de TODOS os meios de prova em direito admitidos, em
   especial DOCUMENTAL, TESTEMUNHAL, PERICIAL E DEPOIMENTO PESSOAL
   do requerido (CPC art. 319 VI);

d) A PROCEDENCIA TOTAL da acao para condenar o requerido ao pagamento
   da quantia de **R$ [valor atualizado]**, acrescida de correcao
   monetaria e juros de mora ate o efetivo pagamento;

e) A condenacao do requerido ao pagamento das custas processuais e
   honorarios sucumbenciais em **10-20%** sobre o valor da condenacao
   (CPC art. 85 §2º);

f) Concessao de gratuidade de justica [se aplicavel].
```

### 3.6 Provas e valor da causa

```markdown
Junta-se:
1. Procuracao
2. Comprovantes/gratuidade
3. Documentos da relacao juridica
4. Memoria de calculo da divida atualizada
5. Notificacao extrajudicial (se houve)
6. [Outras provas pertinentes]

Da-se a causa o valor de **R$ [valor atualizado]**.
```

### 3.7 Fechamento

```
Termos em que,
Pede deferimento.

[cidade], [data].

________________________________________
[NOME DO ADVOGADO]
OAB/[UF] [numero]
```

---

## 4. ESTRUTURA DA INICIAL — JEC (LEI 9099)

Adaptacoes ao formato acima:

### 4.1 Endereçamento

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DO JUIZADO ESPECIAL CIVEL
DA COMARCA DE [cidade] / ESTADO DE [UF]
```

### 4.2 Simplificacoes (Lei 9099 art. 14)

- Linguagem mais simples, sem citacoes excessivas de artigos.
- Pode-se nominar como "RECLAMAÇÃO INICIAL" em vez de "AÇÃO DE COBRANÇA".
- Dispensavel longa fundamentacao doutrinaria.
- Audiencia ja designada **una de conciliacao + instrucao + julgamento**
  (Lei 9099 art. 27 e seguintes).

### 4.3 Requerimentos especificos do JEC

```markdown
REQUER-SE:

a) Citacao do reclamado;
b) Designacao de audiencia (Lei 9099 art. 18-19);
c) Em audiencia, conciliacao e, nao havendo acordo, oitiva das partes e
   producao de provas (Lei 9099 art. 27-29);
d) Procedencia para condenar o reclamado ao pagamento de R$ [valor];
e) Isencao de custas em 1o grau (Lei 9099 art. 54).
```

### 4.4 Atencao especial

- Prazo de defesa nos JEC e diferente (geralmente em audiencia).
- Prazo recursal: **10 dias CORRIDOS** (Lei 9099 art. 42), nao 15 uteis.
- Em caso de recurso, **honorarios e custas** sao devidos pelo
  recorrente vencido (Lei 9099 art. 55).

---

## 5. PEDIDO DE TUTELA DE URGENCIA

Em cobranca, tutela cabe em casos especificos:
- Risco de dilapidacao patrimonial pelo reu
- Necessidade de inscricao/desinscricao em cadastros
- Outras hipoteses excepcionais (CPC art. 300)

Se aplicavel, integrar com `pedido-tutela-urgencia`.

---

## 6. APOS GERAR

- Auto-disparar `protocolo-p4-execucao`.
- Aviso final de revisao humana.

---

## 7. PROIBICOES

1. Nao usar cobranca quando cabe execucao ou monitoria (perde
   eficiencia processual).
2. Nao confundir procedimento comum com JEC nas formalidades.
3. Nao omitir designacao de audiencia (art. 334 CPC) se procedimento
   comum.
4. Nao chutar prazo de defesa do reu — JEC tem regra propria.
