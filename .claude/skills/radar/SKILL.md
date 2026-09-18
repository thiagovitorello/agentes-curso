---
name: radar
description: Roda o radar do dia com o time de agentes, na ordem pesquisador, verificador, redator, guarda (e o agente do dono, se existir), e depois grava o dia no repositório com um commit. Use quando alguém pedir para rodar o radar ou quando a rotina das 7h disparar.
---

# Radar do dia

Você coordena o time. Não pesquisa, não escreve o briefing e não julga notícia — cada
agente faz a sua parte e você garante que a fila ande na ordem.

Antes de começar, descubra a data de hoje. Ela nomeia todos os arquivos do dia, no
formato `AAAA-MM-DD`. Leia `RADAR.md` e `CLAUDE.md`: as regras do radar estão lá.

**Uma etapa por vez, na ordem. Não pule nenhuma e não junte duas.**

## 1. Pesquisador

Acione o agente `pesquisador`.

Quando ele terminar, abra `fontes/AAAA-MM-DD.md` e confira que tem **pelo menos três
itens**. Se tiver menos, ou se não houver nada novo no dia, **siga mesmo assim** — dia
fraco é resposta válida, e o briefing vai sair curto. Registre quantos itens vieram.

Se o arquivo não existir, o pesquisador falhou. Pare e diga isso.

## 2. Verificador

Acione o agente `verificador`.

Quando ele terminar, abra `verificacao/AAAA-MM-DD.md` e confira que existe e traz a
contagem no fim. Anote quantos ficaram CONFERE.

## 3. Redator

Acione o agente `redator`.

Quando ele terminar, confira que existem os dois arquivos: `diario/AAAA-MM-DD.md` e
`index.html`. Confira que o `index.html` não tem marcador `{{...}}` sobrando.

## 4. O agente do dono, se existir

Olhe `.claude/agents/`. Se houver algum agente **além** de `pesquisador`, `verificador`,
`redator` e `guarda`, acione ele agora e inclua o que ele devolver **no fim do briefing**,
numa seção com o nome dele.

Duas condições:

- O que ele devolver entra como texto no briefing. Nada mais.
- Se o trabalho desse agente for mandar alguma coisa para fora — e-mail, mensagem,
  publicação —, **não deixe ele enviar**. Esta Skill não envia nada. Rode o que ele produzir
  como texto, mostre para o dono e diga que o envio ficou parado, esperando um pedido
  explícito dele.

Se não houver agente extra, pule esta etapa e diga que pulou.

## 5. Guarda

Acione o agente `guarda`.

Leia a última linha do relatório:

- **`NÃO PUBLIQUE`** → **pare aqui.** Mostre o relatório inteiro. **Não faça commit.**
  Não tente consertar o briefing por conta própria — quem corrige é o redator, numa rodada
  nova que o dono pede.
- **`PODE PUBLICAR`** → siga para a etapa 6.

## 6. Gravar no repositório

Só chegue aqui com `PODE PUBLICAR`.

1. `git add -A`
2. `git commit -m "radar de AAAA-MM-DD"`
3. Se houver remoto configurado, `git push`. Se não houver, pare no commit e diga isso.

**Se o push falhar, diga o motivo e pare.** Não tente outro caminho, não force, não mude
de branch, não crie um repositório novo. Falha de login é assunto do dono, no navegador.

## 7. O relato final

Três linhas, no máximo:

- a **primeira linha do briefing**, copiada como está;
- quantos itens **conferiram**, de quantos anotados;
- quantos **agentes rodaram**, e se algum foi pulado.

Se a fila parou no meio, diga em qual etapa parou e por quê.

## Nunca

- **Nunca envie nada a ninguém.** O único jeito de o radar sair daqui é o commit e o push.
  Sem e-mail, sem mensagem, sem post.
- **Nunca use chave nem senha.** Se alguma etapa pedir credencial, pare e diga.
- **Nunca pule uma etapa** porque o dia parece fraco ou porque a etapa anterior foi rápida.
- **Nunca faça commit com o guarda em `NÃO PUBLIQUE`.**
- **Nunca reescreva o trabalho de um agente.** Se o resultado veio ruim, relate — não
  conserte por cima.
