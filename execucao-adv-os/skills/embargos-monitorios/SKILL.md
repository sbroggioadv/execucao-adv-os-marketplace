---
name: embargos-monitorios
description: >
  EMBARGOS-MONITORIOS — Defesa do requerido em acao monitoria, oposta
  nos PROPRIOS AUTOS (nao incidente). Aplica CPC art. 702 e Sum. 292
  STJ. Prazo: 15 dias uteis da citacao. Sem garantia do juizo. Use
  quando o usuario representar o REQUERIDO em monitoria. NAO confundir
  com embargos-execucao (incidente em execucao, regime diferente) nem
  com embargos-declaracao (recurso).
---

# EMBARGOS-MONITORIOS — Defesa em Monitoria

## 1. NATUREZA — NAO E EXECUCAO

Diferente dos embargos a execucao, os embargos monitorios:
- Sao **oferecidos nos proprios autos** da monitoria (CPC art. 702).
- **NAO exigem garantia do juizo.**
- Suspendem **automaticamente** a eficacia do mandado monitorio
  (art. 702 §4º).
- Tem amplitude probatoria ampla — qualquer materia de defesa do
  procedimento comum.

**Prazo:** 15 dias uteis da citacao (CPC art. 702 caput).

## 2. MATERIAS CABIVEIS

Qualquer materia de defesa do procedimento comum (CPC art. 702 §1º):

- Inexistencia/inexigibilidade da obrigacao
- Pagamento
- Prescricao / decadencia
- Compensacao
- Transacao
- Nulidade da obrigacao
- Coacao, dolo, erro, fraude
- Impugnacao da prova escrita apresentada
- Incompetencia / impedimento / suspeicao
- Excesso (com memoria contestando o calculo)

## 3. ESTRUTURA

### 3.1 Endereçamento

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DA [Vara Civel] DA
COMARCA DE [cidade] — Acao Monitoria n. [numero]
```

### 3.2 Qualificacao + tipo

```
[NOME EMBARGANTE/REU], ja qualificado nos autos da monitoria em
epigrafe, vem oferecer

EMBARGOS MONITORIOS

em face de [NOME EMBARGADO/AUTOR], pelas razoes a seguir.
```

### 3.3 Tempestividade

```
**Da Tempestividade** — Citacao em [data], prazo de 15 dias uteis
(CPC art. 702), encerrando-se em [data]. **TEMPESTIVOS.**
```

### 3.4 Preliminares (se aplicavel)

- Incompetencia
- Inepcia da inicial
- Falta de pressuposto processual

### 3.5 Materia de fundo

```markdown
### Da [defesa especifica]

[Exposicao dos fatos]

[Fundamentacao legal — CPC art. 702 e materia substantiva aplicavel]

[Citacao de jurisprudencia se houver — usar plugin juris-adv-os para
validar]
```

### 3.6 Requerimentos

```markdown
REQUER-SE:

a) Recebimento dos embargos com SUSPENSAO automatica da eficacia do
   mandado monitorio (CPC art. 702 §4º);

b) PROCEDENCIA dos embargos para julgar IMPROCEDENTE a pretensao
   monitoria, com:
   i) [pedidos especificos: declaracao de inexistencia,
   inexigibilidade, prescricao, pagamento, etc.];

c) Condenacao do embargado em honorarios sucumbenciais (CPC art. 85
   §11 — majoracao em embargos rejeitados / acolhidos);

d) Producao de todas as provas em direito admitidas, em especial
   testemunhal, pericial e depoimento pessoal.
```

## 4. EFEITOS DA SENTENCA

| Cenario | Efeito |
|---------|--------|
| Embargos **procedentes** | Acao monitoria julgada improcedente; honorarios devidos ao embargante |
| Embargos **improcedentes** | Mandado monitorio se converte em **titulo executivo judicial** (CPC art. 702 §8º), seguindo direto pra cumprimento de sentenca |
| Embargos parciais procedentes | Conversao parcial — divida reduzida vira titulo executivo |

## 5. RECURSO

A sentenca dos embargos monitorios e impugnavel por **apelacao**
(CPC art. 1.009) — direcionar ao skill `apelacao`.

## 6. PROIBICOES

1. Nao confundir prazo (15 dias monitorios) com 3 dias da execucao.
2. Nao exigir garantia — monitoria nao tem.
3. Nao pular preliminares quando cabiveis.
4. Auto-disparar `protocolo-p4-execucao`.
