---
name: agravo-instrumento
description: >
  AGRAVO-INSTRUMENTO — Recurso contra DECISOES INTERLOCUTORIAS (nao
  contra sentenca) em Justica Comum (CPC art. 1.015). Cabivel apenas
  nas hipoteses do art. 1.015 + tema 988 STJ (rol mitigado). Prazo:
  15 dias uteis. Endereçado direto ao Tribunal. Use quando houver
  decisao interlocutoria que cause prejuizo nao reparavel ao final.
---

# AGRAVO-INSTRUMENTO — Recurso contra Interlocutorias

## 1. CABIMENTO — ROL DO ART. 1.015 + TEMA 988 STJ

CPC art. 1.015 lista hipoteses TAXATIVAS:

I — tutelas provisorias
II — merito do processo (resolve parte da causa antes da sentenca)
III — rejeicao da alegacao de convencao de arbitragem
IV — incidente de desconsideracao da personalidade juridica
V — rejeicao do pedido de gratuidade ou acolhimento do pedido de revogacao
VI — exibicao ou posse de documento ou coisa
VII — exclusao de litisconsorte
VIII — rejeicao do pedido de limitacao do litisconsorcio
IX — admissao ou inadmissao de intervencao de terceiros
X — concessao, modificacao ou revogacao de efeito suspensivo aos embargos
XI — redistribuicao do onus da prova
XII — converter acao individual em coletiva
XIII — outros casos expressamente referidos em lei
XIV (par. unico) — decisoes interlocutorias proferidas na fase de
liquidacao/cumprimento de sentenca, processo de execucao ou inventario

**TEMA 988 STJ (REsp 1.704.520/MT):** o rol e MITIGADO — admite-se
agravo fora do rol quando a decisao for **urgente** e **nao podera
ser eficazmente reexaminada no recurso da sentenca** (causa pre­juizo
imediato). Sempre justificar a urgencia/inutilidade do reexame no
recurso de apelacao.

## 2. PRAZO

**15 dias UTEIS** (CPC art. 1.003 §5º + 1.070).

## 3. ENDEREÇAMENTO

Direto ao **Tribunal competente** (Tribunal de Justica do Estado, ou
TRF) — NAO ao juiz a quo (diferente da apelacao).

## 4. ESTRUTURA

### 4.1 Endereçamento

```
EGREGIO TRIBUNAL DE JUSTICA DO ESTADO DE [UF]
COLENDA [Camara ou "DISTRIBUICAO"]
```

### 4.2 Qualificacao + tipo

```
[NOME AGRAVANTE], ja qualificado nos autos do processo n. [numero]
em tramite na [Vara] da Comarca de [cidade], em face de [AGRAVADO],
vem interpor

AGRAVO DE INSTRUMENTO

contra a r. decisao interlocutoria proferida em [data], pelas razoes
a seguir.
```

### 4.3 Tempestividade

```
**Da Tempestividade** — Decisao publicada em [data]. Prazo de 15 dias
uteis (CPC art. 1.003 §5º) terminaria em [data]. **TEMPESTIVO.**
```

### 4.4 Cabimento

Bloco DEDICADO. Critico, pois a primeira coisa que o Tribunal analisa
e o cabimento (pode rejeitar liminarmente).

```markdown
## Do Cabimento

A decisao interlocutoria agravada [versa sobre tutela provisoria /
merito do processo / OUTRA HIPOTESE], hipotese expressamente prevista
no inciso [N] do art. 1.015 do CPC.

[Se fora do rol: invocar Tema 988 STJ + justificar:
- urgencia da decisao
- inutilidade pratica do reexame na apelacao
- prejuizo imediato e irreparavel]
```

### 4.5 Documentos obrigatorios — CPC art. 1.017

```markdown
## Das Pecas Obrigatorias

Acompanham este agravo (CPC art. 1.017):

I — Copia da peticao inicial
II — Copia da contestacao
III — Copia da peticao que ensejou a decisao agravada
IV — Copia da decisao agravada
V — Copia da certidao da intimacao
VI — Procuracao do agravante e do agravado (se ja constituida)
VII — Demais pecas indicadas em lei ou que o agravante considere uteis

[Se autos eletronicos: ja consta nos autos — declarar conforme
art. 1.017 §5º]
```

### 4.6 Razoes

```markdown
## I — Sintese

[Breve relato do processo e da decisao recorrida.]

## II — Razoes de Reforma

### 1. [Materia A]
[Exposicao detalhada]

### 2. [Materia B]
[...]
```

### 4.7 Tutela recursal (se necessario suspensivo)

```markdown
## III — Do Efeito Suspensivo / Antecipacao da Tutela Recursal

Requer-se ATRIBUICAO DE EFEITO SUSPENSIVO ao presente recurso (CPC
art. 1.019 I), demonstrando-se:

a) Fumus boni iuris — [fundamentar verossimilhança das razoes];

b) Periculum in mora — [demonstrar dano irreparavel da execucao
   imediata da decisao impugnada].
```

### 4.8 Pedidos

```markdown
REQUER-SE:

a) CONHECIMENTO e PROVIMENTO do recurso;

b) ATRIBUICAO de efeito suspensivo (se aplicavel) ate o julgamento
   final;

c) REFORMA da decisao agravada para [pedido especifico];

d) Apos contrarrazoes, julgamento de merito do recurso pela Camara
   competente;

e) Em ultimo caso, em sendo o agravo de retencao, sua reiteracao
   nas razoes da apelacao.
```

## 5. CONTRARRAZOES

Apos intimacao do agravado, prazo de 15 dias uteis para apresentar.
Mesma estrutura, defendendo a decisao.

## 6. AGRAVO INTERNO

Diferente do agravo de instrumento. Cabe contra decisoes monocraticas
do relator no Tribunal (CPC art. 1.021). Prazo: 15 dias uteis. NAO e
escopo desta skill — caso necessario, gerar peca propria.

## 7. PROIBICOES

1. Nao apresentar agravo fora do rol sem invocar Tema 988 STJ +
   justificar urgencia.
2. Nao esquecer pecas obrigatorias do art. 1.017 — sob pena de
   rejeicao liminar.
3. Nao endereçar ao juizo a quo — vai direto ao Tribunal.
4. Nao confundir com agravo interno (regime diferente).
5. Auto-disparar `protocolo-p4-execucao`.
