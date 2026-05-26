---
name: contestacao-cobranca
description: >
  CONTESTACAO-COBRANCA — Defesa do reu em acao de cobranca ordinaria
  (procedimento comum) ou JEC. Aplica CPC arts. 335-342. Prazo: 15
  dias uteis no comum (a partir da audiencia de conciliacao ou
  protocolo nos casos do art. 335 II-III), regime de prazos do JEC
  se Lei 9099. Inclui preliminares + materia de defesa + reconvencao
  se aplicavel. Use quando o usuario representar REU em acao de
  cobranca ordinaria.
---

# CONTESTACAO-COBRANCA — Defesa em Cobranca Comum/JEC

## 1. PRAZO E REGIME

| Procedimento | Prazo da contestacao | Inicio |
|--------------|----------------------|--------|
| Comum (CPC) | 15 dias uteis | Conforme CPC art. 335 (audiencia de conciliacao, protocolo do desinteresse, ou demais hipoteses) |
| JEC (Lei 9099) | Apresentada em audiencia (escrita ou oral) | Audiencia designada |

Veja contexto da sessao (`competencia-funcional`) para saber qual.

## 2. ESTRUTURA — PROCEDIMENTO COMUM

### 2.1 Endereçamento

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ DE DIREITO DA [Vara] DA COMARCA DE
[cidade] — Processo n. [numero]
```

### 2.2 Qualificacao + tipo

```
[NOME REU/CONTESTANTE], ja qualificado nos autos da acao em epigrafe,
vem oferecer

CONTESTAÇÃO

pelas razoes de fato e fundamentos de direito a seguir expostos.
```

### 2.3 Tempestividade

```
**Da Tempestividade** — [citar marco inicial e calculo].
```

### 2.4 Preliminares (CPC art. 337)

Identifique e desenvolva as cabiveis:

- Inepcia da inicial (art. 330)
- Incompetencia absoluta ou relativa
- Litispendencia / coisa julgada / perempção
- Conexao / continencia (pode determinar reuniao de processos)
- Incorrecao do valor da causa
- Indevida concessao de gratuidade de justica
- Falta de pressuposto processual
- Convencao de arbitragem
- Falta de interesse processual
- Defeito de representacao/capacidade

### 2.5 Merito

```markdown
### Dos fatos

[Versao do reu sobre os fatos — refutar ponto a ponto a inicial]

### Do direito

1. **Inexistencia / inexigibilidade da divida** — [se for o caso,
   fundamentar]

2. **Pagamento** — [se houve, anexar comprovantes]

3. **Prescricao / decadencia** — [se aplicavel, contar prazos
   conforme CC arts. 205-211]

4. **Compensacao / transacao / novacao** — [se aplicavel]

5. **Excesso de cobranca** — [se valor cobrado e indevido em parte,
   apresentar memoria de calculo correta]

6. **Limitacao por CDC** — [se relacao de consumo, invocar art. 51
   IV, art. 42 (cobranca vexatoria), inversao do onus art. 6º VIII]

7. **Nulidade de clausula contratual** — [se houver clausula abusiva]
```

### 2.6 Reconvencao (se aplicavel)

Pode ser apresentada NA propria contestacao (CPC art. 343):

```markdown
### Da Reconvencao

Em conformidade com o art. 343 do CPC, vem o reu apresentar
RECONVENCAO pelos seguintes motivos:

[pedido reconvencional fundamentado — ex: dano moral por cobranca
vexatoria do CDC art. 42 par. unico, restituicao em dobro, etc.]
```

### 2.7 Provas

```markdown
**Provas requeridas:**

a) Documental ja juntada;
b) Documental superveniente (se necessario);
c) Testemunhal — [rol em momento oportuno];
d) Pericial [se aplicavel];
e) Depoimento pessoal do autor;
f) [Outras].
```

### 2.8 Requerimentos

```markdown
REQUER-SE:

a) Acolhimento das PRELIMINARES suscitadas, com extincao do processo
   sem resolucao de merito;

b) Caso ultrapassadas, IMPROCEDENCIA da acao, com:
   i) [pedidos especificos por materia];

c) Acolhimento da RECONVENCAO [se apresentada] para [pedidos
   reconvencionais];

d) Condenacao do autor em honorarios sucumbenciais (CPC art. 85);

e) Producao de todas as provas requeridas.
```

## 3. ESTRUTURA — JEC

- **Forma:** pode ser oral em audiencia, mas o ideal e escrita
  protocolada antes para organizacao.
- **Conteudo:** mesma materia de defesa, mas com **linguagem mais
  simples** e fundamentacao mais enxuta.
- **Reconvencao:** Lei 9099 art. 31 — admite "pedido contraposto" mais
  amplo que a reconvencao do CPC, mas mais limitado em complexidade
  probatoria.

## 4. JURISPRUDENCIA APLICAVEL — REFERENCIAS

Use plugin `juris-adv-os` (order bump complementar) para buscar
jurisprudencia atualizada sobre:
- Limitacao de juros pactuados em consumo (Sum. 539 STJ)
- Cobranca de divida prescrita (Sum. 297 STJ aplicavel por analogia)
- Inversao do onus (CDC art. 6º VIII)
- Cobranca vexatoria (CDC art. 42)

## 5. PROIBICOES

1. Nao confundir prazo da contestacao do CPC com o do JEC.
2. Nao omitir preliminares se cabiveis — devem ser arguidas na
   contestacao sob pena de preclusao (CPC art. 337 §5º, salvo as
   absolutas).
3. Toda reconvencao deve ter pedido CLARO e VALOR atribuido.
4. Auto-disparar `protocolo-p4-execucao`.
