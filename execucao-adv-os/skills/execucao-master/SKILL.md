---
name: execucao-master
description: >
  EXECUCAO-MASTER — Orquestrador central do plugin execucao-adv-os.
  Le o input do advogado (texto livre ou /execucao + argumentos),
  classifica a fase do caso, e ativa as skills corretas em sequencia.
  Mantem o contexto da sessao consistente entre skills (yaml caso{}).
  Roteia inputs por palavras-chave + estado do caso. Use SEMPRE como
  ponto de entrada do plugin OU quando o usuario disser "qual o
  proximo passo", "como prossigo", "ajude com execucao".
---

# EXECUCAO-MASTER — Orquestrador do Plugin

## 1. PAPEL

Esta skill e o **maestro**. Recebe input do advogado e:
1. Classifica a fase do caso (analise/notificacao/inicial/defesa/recurso/cumprimento)
2. Ativa a skill correta para essa fase
3. Garante que skills upstream (Tier 1+2) rodaram antes de skills downstream
4. Mantem o contexto da sessao (yaml `caso:`) coerente

## 2. ROTEAMENTO POR PALAVRA-CHAVE

| Input do usuario | Skill ativada |
|------------------|---------------|
| "tenho um cheque", "NP", "duplicata", "contrato", "boleto", "NF", "divida", "titulo", "analise", "qual acao cabivel" | `analise-titulo-executivo` |
| "competencia", "foro", "qual TJ", "onde ajuizar" | `competencia-territorial` |
| "JEC ou comum", "Justica Federal", "valor da causa", "qual juizo" | `competencia-funcional` |
| "notificar", "constituir em mora", "mora", "interpelar" | `notificacao-extrajudicial-mora` |
| "atualizar", "calculo", "juros", "correcao monetaria", "valor atualizado" | `calculo-atualizacao-monetaria` |
| "ajuizar execucao", "executar", "execucao de titulo" | `peticao-inicial-execucao` |
| "monitoria", "acao monitoria" | `peticao-inicial-monitoria` |
| "cobranca", "acao de cobranca" | `peticao-inicial-cobranca` |
| "embargar execucao", "fui executado", "embargos a execucao" | `embargos-execucao` |
| "embargar monitoria" | `embargos-monitorios` |
| "contestar cobranca", "contestacao" | `contestacao-cobranca` |
| "esclarecer sentenca", "omissao", "contradicao", "embargos declaracao" | `embargos-declaracao` |
| "apelar", "apelacao", "recurso" (em Justica Comum) | `apelacao` |
| "recurso JEC", "recurso inominado", "recurso na Lei 9099" | `recurso-inominado-jec` |
| "agravo", "interlocutoria" | `agravo-instrumento` |
| "REsp", "recurso especial", "STJ" | `recurso-especial-stj` |
| "RE", "recurso extraordinario", "STF", "repercussao geral" | `recurso-extraordinario-stf` |
| "penhora online", "arresto", "indisponibilidade", "tutela" | `pedido-tutela-urgencia` |
| "cumprir sentenca", "executar sentenca", "transito em julgado" | `cumprimento-sentenca` |
| "prazo do recurso", "ate quando recorro", "tempestividade" | `gestao-prazo-recursal` |
| "audita", "P4", "auditoria" | `protocolo-p4-execucao` |

## 3. ESTADOS DO CASO

A sessao mantem um `yaml` mental do estado do caso:

```yaml
caso:
  fase_atual: [analise | notificacao | calculo | inicial | defesa | recurso | cumprimento]
  tipo_acao: [execucao | monitoria | cobranca | nao_definido]
  natureza_relacao: [consumo | civil | empresarial | locaticia | trabalhista]
  cdc_aplicavel: [true | false]
  mora_tipo: [ex_re | ex_persona | iliquida]
  prescricao:
    prazo_anos: N
    data_limite: YYYY-MM-DD
    status: vivo | em_risco | prescrito
  legislacao_chave: [...]
  competencia_territorial:
    foros_ranqueados: [...]
    foro_escolhido: [...]
  competencia_funcional:
    juizo: [vara_civel | jec | jef | vara_federal | jefp]
    prazo_regime: [uteis | corridos]
  notificacao:
    necessaria: [true|false]
    realizada: [true|false]
    data: YYYY-MM-DD
  calculo:
    valor_atualizado: R$ ...
    data_atualizacao: YYYY-MM-DD
  peticoes_geradas:
    - tipo: ...
      data: ...
      selo_p4: APROVADA|REVISAR|BLOQUEADA
```

## 4. WORKFLOW DE ATIVACAO

### Cenario A: Caso novo (cliente acabou de chegar)

```
1. analise-titulo-executivo  (sempre)
   ↓ (preenche tipo_acao, natureza_relacao, mora_tipo)
2. competencia-territorial   (sempre)
   ↓ (preenche foros_ranqueados)
3. competencia-funcional     (sempre)
   ↓ (preenche juizo + prazo_regime)
4. Se mora_tipo == ex_persona e notificacao.realizada == false:
     notificacao-extrajudicial-mora
5. calculo-atualizacao-monetaria   (antes de qualquer peticao)
6. Conforme tipo_acao:
     peticao-inicial-execucao | peticao-inicial-monitoria |
     peticao-inicial-cobranca
   ↓ (auto-dispara `protocolo-p4-execucao`)
7. Output final com peca + selo P4 + checklist anexos
```

### Cenario B: Cliente vai responder a uma acao

```
1. analise-titulo-executivo  (mesmo do polo passivo — pra entender
   o titulo na maos da parte contraria)
2. competencia-territorial   (validar foro escolhido pelo autor)
3. competencia-funcional     (validar juizo)
4. Conforme tipo_acao em que ele e reu:
     embargos-execucao | embargos-monitorios | contestacao-cobranca
   ↓ (auto-dispara `protocolo-p4-execucao`)
5. Output
```

### Cenario C: Cliente vai recorrer

```
1. gestao-prazo-recursal  (calcular se ainda da tempo)
2. Conforme decisao + competencia_funcional:
     embargos-declaracao | apelacao | recurso-inominado-jec |
     agravo-instrumento | recurso-especial-stj |
     recurso-extraordinario-stf
   ↓ (auto-dispara `protocolo-p4-execucao`)
3. Output
```

### Cenario D: Ganhou e quer cumprir

```
1. cumprimento-sentenca
2. P4
3. Output
```

## 5. BLOQUEIOS UPSTREAM

| Skill | Bloqueada se NAO rodou |
|-------|------------------------|
| peticao-inicial-* | analise-titulo-executivo + competencia-* + calculo |
| embargos-* / contestacao | analise (pra entender o titulo da outra parte) |
| Qualquer recurso | gestao-prazo-recursal (validar tempestividade) |
| Qualquer peca final | protocolo-p4-execucao apos geracao |

Se faltar pre-requisito, **PARE** e ative a skill que falta antes
de prosseguir.

## 6. FORMATO DE INTERACAO

Quando o usuario faz uma pergunta livre:

```markdown
## Diagnostico inicial — execucao-master

**Input recebido:** "[copiar trecho relevante]"

**Fase do caso classificada:** [analise / inicial / defesa / recurso / etc.]

**Skills que serao acionadas em sequencia:**
1. [skill X] — [razao]
2. [skill Y] — [razao]
3. ...

**Estado atual do caso (preenchido na medida que avancarmos):**

```yaml
[yaml inicial]
```

Vamos comecar pela primeira skill...
```

## 7. PRINCIPIOS DA ORQUESTRACAO

1. **Nunca pule a fase de analise.** Mesmo se o advogado diz "ja sei
   que e execucao", rode `analise-titulo-executivo` para validar
   requisitos e propagar contexto.
2. **Sempre cheque competencia antes de gerar peticao.**
3. **Sempre P4 antes do output final** de qualquer peca.
4. **Sinalize prescricao em risco** com ⚠️ destaque em todas as
   skills.
5. **Em duvida sobre rotear**, pergunte UMA VEZ ao usuario.

## 8. PROIBICOES

1. Nao gerar peca sem ter rodado Tier 1 + Tier 2 no minimo.
2. Nao confundir cliente em polo ativo vs passivo na hora de
   escolher skills.
3. Nao bipassar `protocolo-p4-execucao`.
4. Nao perder o yaml de contexto entre skills da mesma sessao.
