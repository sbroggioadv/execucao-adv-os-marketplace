---
name: embargos-execucao
description: >
  EMBARGOS-EXECUCAO — Defesa do executado em acao de execucao de titulo
  extrajudicial. Aplica CPC arts. 914-920, com materias do art. 917
  (nulidade citacao, inexigibilidade, ilegitimidade, excesso de execucao,
  causas modificativas/extintivas, incompetencia, etc.). Prazo: 15 dias
  uteis apos juntada do mandado citatorio. Aplica Sum. 393 STJ. Use
  quando o usuario representar o EXECUTADO (polo passivo da execucao).
---

# EMBARGOS-EXECUCAO — Defesa em Execucao

## 1. NATUREZA E PRAZOS

- **Acao incidente** ao processo executivo (CPC art. 914).
- **Prazo:** 15 dias uteis contados da juntada do mandado de citacao
  ou do arresto convertido (CPC art. 915).
- **Garantia do juizo:** NAO e mais requisito (CPC art. 914) salvo
  para suspender execucao (CPC art. 919 §1º).

## 2. MATERIAS DO ART. 917 — VEREDITO ESTRATEGICO

Analise quais materias se aplicam ao caso (pode ser mais de uma):

| Materia | Quando alegar |
|---------|---------------|
| **I — Inexigibilidade ou inexistencia do titulo** | Titulo nao preenche requisitos do 784, divida ja paga, novacao, etc. |
| **II — Penhora incorreta ou avaliacao erronea** | Bem impenhoravel, valor de avaliacao desproporcional |
| **III — Excesso de execucao ou cumulacao indevida** | Valor cobrado > devido (apresentar memoria de calculo correta — CPC art. 917 §3º) |
| **IV — Retencao por benfeitorias** | Em execucoes para entrega de coisa |
| **V — Incompetencia, impedimento, suspeicao** | Foro errado, juiz suspeito (CPC art. 144-148) |
| **VI — Qualquer materia que seria licito deduzir como defesa em processo de conhecimento** | Pagamento, prescricao, decadencia, compensacao, transacao, etc. |

**CRITICO — Excesso de execucao (art. 917 §3º):** se alegar, o
embargante deve declarar **o valor que entende devido** apresentando
memoria de calculo discriminada. Sem isso, parte do pedido vai ser
rejeitada liminarmente (CPC art. 917 §4º).

## 3. ESTRUTURA DA PEÇA

### 3.1 Endereçamento
```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DA [Vara] DA COMARCA DE
[cidade] — Processo de execucao n. [numero]
```

### 3.2 Qualificacao + tipo

```
[NOME EMBARGANTE], ja qualificado nos autos da execucao em epigrafe,
por meio de seu advogado infrafirmado, vem oferecer

EMBARGOS A EXECUÇÃO

em face de [NOME EMBARGADO/EXEQUENTE], pelas razoes a seguir.
```

### 3.3 Tempestividade

```
**Da Tempestividade**

A citacao foi juntada em [data]. O prazo de 15 dias uteis (CPC art.
915) terminaria em [data]. Os presentes embargos sao, portanto,
TEMPESTIVOS.
```

### 3.4 Fundamentacao por materia

Para CADA materia alegada, monte bloco fundamentado:

```markdown
### Da [Materia X — ex: inexigibilidade do titulo]

[Exposicao dos fatos especificos da defesa]

[Fundamentacao legal — citar artigo do CPC art. 917 e legislacao
substantiva aplicavel, alem de jurisprudencia relevante]

[Documentos que sustentam a alegacao]
```

### 3.5 Requerimentos

```markdown
REQUER-SE:

a) Recebimento dos embargos no efeito SUSPENSIVO (CPC art. 919 §1º)
   ate decisao final, demonstrando-se:
   i) Garantia do juizo (penhora/caucao);
   ii) Relevancia da fundamentacao;
   iii) Risco de dano de dificil ou impossivel reparacao;

b) PROCEDENCIA dos embargos para:
   [pedidos especificos por materia: declaracao de inexigibilidade,
   reducao do valor, anulacao da citacao, redesignacao para foro
   competente, etc.]

c) Condenacao do embargado em honorarios sucumbenciais (CPC art. 85);

d) Produçao de todas as provas em direito admitidas.
```

## 4. EFEITO SUSPENSIVO — REQUISITOS

CPC art. 919 §1º (TRES requisitos cumulativos):
1. Garantia do juizo (penhora ou caucao)
2. Relevancia da fundamentacao
3. Risco de dano grave

Sem os 3, embargos seguem **sem suspender** a execucao — penhora
prossegue, ate leilao.

## 5. PROIBICOES

1. Nao confundir embargos a execucao com embargos a sentenca ou
   embargos do CPC/73.
2. Excesso de execucao SEM memoria de calculo discriminada e rejeitada
   liminarmente (art. 917 §4º).
3. Nao omitir o pedido de efeito suspensivo se cabivel.
4. Auto-disparar `protocolo-p4-execucao` apos gerar.
