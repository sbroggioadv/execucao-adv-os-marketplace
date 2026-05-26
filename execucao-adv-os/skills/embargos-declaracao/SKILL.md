---
name: embargos-declaracao
description: >
  EMBARGOS-DECLARACAO — Recurso de aclaramento (CPC arts. 1.022-1.026)
  contra qualquer decisao em qualquer instancia para sanar OMISSAO,
  CONTRADICAO, OBSCURIDADE ou ERRO MATERIAL. Prazo: 5 dias uteis
  (Comum) / 5 dias corridos (JEC). Interrompe prazo dos demais recursos.
  Use quando a decisao for confusa, omissa, contraditoria ou tiver erro
  obvio.
---

# EMBARGOS-DECLARACAO — Recurso de Aclaramento

## 1. CABIMENTO (CPC art. 1.022)

Embargos cabem para sanar (taxativamente):

1. **Obscuridade** — decisao confusa, multiplos sentidos
2. **Contradicao** — fundamentos antagonicos entre si OU dispositivo
   incompativel com a fundamentacao
3. **Omissao** — ponto suscitado pela parte nao foi enfrentado
4. **Erro material** — equivocos obvios (nome trocado, data
   equivocada, valor incorreto)

**ATENCAO:** embargos NAO servem pra rediscutir o merito. Se a parte
quer mudar o que a decisao decidiu, e via inadequada — usar o recurso
proprio (apelacao, agravo, etc.).

## 2. PRAZO

| Procedimento | Prazo | Regime |
|--------------|-------|--------|
| Justica Comum (CPC) | **5 dias UTEIS** (art. 1.023) | CPC art. 219 |
| JEC (Lei 9099) | **5 dias CORRIDOS** | Lei 9099 art. 50 |

**Efeito critico:** embargos INTERROMPEM o prazo para os outros
recursos (apelacao, agravo, REsp/RE) — CPC art. 1.026. Apos
publicacao do julgamento dos embargos, prazo recursal **recomeça
do zero**.

## 3. ESTRUTURA

### 3.1 Endereçamento

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ/DESEMBARGADOR/MINISTRO
[orgao prolator da decisao] — Processo n. [numero]
```

### 3.2 Qualificacao + tipo

```
[NOME EMBARGANTE], ja qualificado nos autos em epigrafe, vem opor

EMBARGOS DE DECLARAÇÃO

com fundamento nos arts. 1.022 e seguintes do CPC, pelas razoes a seguir.
```

### 3.3 Tempestividade

```
**Da Tempestividade** — Intimacao da decisao publicada em [data]. Prazo
de 5 dias uteis terminaria em [data]. **TEMPESTIVOS.**
```

### 3.4 Vicio especifico identificado

Para CADA vicio alegado, monte bloco:

```markdown
### Da [Omissao / Obscuridade / Contradicao / Erro material]

**Trecho da decisao impugnado:**
> [transcricao literal do trecho]

**Vicio especifico:**
[explicar com precisao qual o vicio. Se omissao, indicar o ponto
arguido que NAO foi enfrentado. Se contradicao, mostrar os 2 trechos
incompativeis. Se obscuridade, mostrar a ambiguidade. Se erro
material, apontar o equivoco.]

**Consequencia processual:**
[por que isso prejudica a parte / impede a aplicacao da decisao /
viola o devido processo]
```

### 3.5 Pre-questionamento (se for preparar REsp/RE)

```markdown
### Do Pre-questionamento

Pretende-se, com a presente, suscitar e pre-questionar expressamente
para fins do art. 1.025 do CPC (eventual REsp/RE futuro), as seguintes
materias federais/constitucionais:

- [Artigo X da CF / Lei Y, art. Z]
- [Outro dispositivo]
```

### 3.6 Requerimentos

```markdown
REQUER-SE:

a) Conhecimento e PROVIMENTO dos embargos para SANAR o(s) vicio(s)
   apontado(s);

b) Em caso de aclaramento que altere o conteudo da decisao
   (excepcionalmente), atribuir efeitos modificativos (CPC art. 1.023
   §2º);

c) Suspensao/interrupcao do prazo dos demais recursos (CPC art. 1.026).
```

## 4. EFEITOS

| Cenario | Efeito |
|---------|--------|
| Acolhidos com aclaramento simples | Decisao integrada/esclarecida; prazo recursal recomeça |
| Acolhidos com efeitos modificativos | Alteracao do conteudo (excepcional, exige contraditorio) |
| Rejeitados | Decisao mantida; prazo recursal recomeça apos publicacao |
| **Manifestamente protelatorios** | Multa de 2% (1a vez) / ate 10% (reiteracao) — CPC art. 1.026 §2º |

## 5. NAO PROTELATORIO

CRITICO: embargos manifestamente protelatorios geram MULTA. Sinais que
o juiz pode considerar protelatorio:
- Repetir argumento ja enfrentado
- Pedir esclarecimento de ponto claro
- Tentar rediscutir merito sob fachada de aclaramento

Por isso, **so use quando ha vicio real**. Em duvida, melhor passar
direto para apelacao/agravo.

## 6. PROIBICOES

1. Nao usar embargos pra rediscutir merito.
2. Nao omitir transcricao literal do trecho impugnado.
3. Nao confundir com embargos a execucao ou embargos monitorios.
4. Se pre-questionar pra REsp/RE: ser EXPLICITO mencionando art. 1.025.
5. Auto-disparar `protocolo-p4-execucao`.
