---
name: pedido-tutela-urgencia
description: >
  PEDIDO-TUTELA-URGENCIA — Estrutura pedido de tutela de urgencia
  (CPC art. 300) acessorio a inicial de execucao, monitoria ou
  cobranca. Cabe arresto (art. 830), indisponibilidade de bens
  via SISBAJUD (art. 854), bloqueio de veiculos (RENAJUD),
  protesto extrajudicial preventivo. Exige FUMUS BONI IURIS +
  PERICULUM IN MORA. Use quando ha risco de dilapidacao
  patrimonial ou de prescricao iminente.
---

# PEDIDO-TUTELA-URGENCIA — Anti-dilapidacao

## 1. BASE LEGAL

- CPC art. 300 — tutela de urgencia (cautelar ou antecipada)
- CPC art. 830-831 — arresto em execucao
- CPC art. 854 — penhora online (SISBAJUD)
- Lei 6.830/80 — execucao fiscal (subsidiariamente)
- CC art. 591 — desconsideracao patrimonial preventiva

## 2. REQUISITOS — CPC ART. 300

Dois CUMULATIVOS:

### 2.1 Fumus boni iuris

Probabilidade do direito. Demonstrar:
- Titulo executivo formalmente valido (se execucao)
- Prova escrita robusta (se monitoria/cobranca)
- Direito documentalmente verificavel

### 2.2 Periculum in mora

Risco de dano grave ou de dificil reparacao. Tipos:
- Devedor com sinais de dilapidacao patrimonial (vendas suspeitas,
  desvio de bens, transferencias para terceiros)
- Devedor em mora ha muito tempo (risco de insolvencia consumada)
- Bens objeto da execucao em risco de perecimento ou desaparecimento
- Prescricao iminente ou nova lesao em curso
- Cadastros restritivos ja sinalizando dificuldade financeira

## 3. MEDIDAS POSSIVEIS

### 3.1 Arresto (CPC art. 830-831)

Em execucao, quando frustrada a citacao (executado nao encontrado),
juiz expede mandado de **arresto** sobre bens do executado em valor
suficiente para garantir o credito. Apos efetivada a citacao, o
arresto converte-se em penhora.

### 3.2 Penhora online (CPC art. 854 — SISBAJUD)

Sistema SISBAJUD permite bloqueio de ativos financeiros em conta-
corrente, poupança ou aplicacoes. Pode ser requerida **ANTES** da
citacao do executado (sigilo do art. 854 caput) para evitar
movimentacao de ativos. Em monitoria/cobranca, pode ser pedida em
sede de tutela de urgencia para garantir futuro adimplemento.

### 3.3 RENAJUD

Bloqueio de transferencia de veiculos automotores. Util quando o
devedor tem veiculos em seu nome — evita venda preventiva.

### 3.4 CCS-Bacen / SREI

Cadastro Central de Clientes do Sistema Financeiro Nacional (CCS) e
Sistema de Registro de Imoveis Eletronico (SREI) — instrumentos para
localizar bens.

### 3.5 Indisponibilidade especifica

Em casos de devedor com facetas de empresario, indisponibilidade
preventiva de quotas/acoes societarias.

### 3.6 Protesto extrajudicial preventivo

Inclui o devedor em cadastros restritivos (SPC/Serasa) antes mesmo do
trânsito em julgado — Sumula 372 STJ admite em sede de tutela
desde que tutela urgencia.

## 4. ESTRUTURA DO PEDIDO

Pode ir EMBUTIDO na inicial (caso mais comum) ou em peca avulsa
incidental.

### 4.1 No bloco "DA TUTELA DE URGENCIA"

```markdown
## Da Tutela de Urgencia (CPC art. 300)

Esta acao se faz acompanhada de **PEDIDO DE TUTELA DE URGENCIA**, com
base no art. 300 do CPC, pelos motivos a seguir:

### Fumus boni iuris

[Demonstrar probabilidade do direito — citar titulo executivo,
prova escrita, ou demais elementos]

### Periculum in mora

[Demonstrar risco — sinais de dilapidacao, prescricao iminente,
prejuizo nao reparavel ao final, etc.]

### Medidas requeridas

REQUER-SE, em sede de tutela de urgencia, INAUDITA ALTERA PARTE
(CPC art. 300 §2º):

a) **Arresto/Penhora online via SISBAJUD** sobre os ativos
   financeiros do executado em valor suficiente para garantir a
   execucao no montante de R$ [valor];

b) **Bloqueio RENAJUD** de eventual veiculo registrado em nome do
   executado;

c) **Indisponibilidade preventiva** de quotas/acoes societarias do
   executado (se PJ ou empresario);

d) [Outras medidas pertinentes]
```

### 4.2 Em peca avulsa (apos a inicial)

```
EXCELENTISSIMO SENHOR DOUTOR JUIZ [...] — Processo n. [numero]

[NOME REQUERENTE] vem requerer, nos autos em epigrafe,

TUTELA DE URGENCIA INCIDENTE

com fundamento no art. 300 do CPC, pelos motivos a seguir.

[...estrutura similar...]
```

## 5. CAUCAO

CPC art. 300 §1º permite ao juiz exigir caucao do requerente para
ressarcimento de eventual dano causado pela medida (caso seja
posteriormente revogada). Em execucao, geralmente dispensada quando
ha titulo extrajudicial valido.

## 6. RESPONSABILIDADE DO REQUERENTE

CPC art. 302: requerente responde objetivamente por dano causado
quando a tutela:
- For revertida em sentenca
- For revogada por mudanca de fato
- Houver dolo ou ma-fe

**Atencao:** sempre orientar o cliente sobre essa responsabilidade.

## 7. PROIBICOES

1. NUNCA pedir tutela sem demonstrar AMBOS os requisitos (fumus +
   periculum).
2. Nao confundir tutela ANTECIPADA (gera efeito da sentenca de
   merito) com CAUTELAR (apenas conservativa).
3. Nao omitir caucao se for o caso.
4. Auto-disparar `protocolo-p4-execucao` apos integrar a tutela na
   peca principal.
