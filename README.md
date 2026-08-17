# Padrão AAA Universal

Manual de execução portátil para o Claude Code. Ele não diz **o que** construir — diz **quanto rigor**
cada tarefa merece, e **que evidência** prova que o rigor aconteceu.

Escrito em português. Nasceu de um workspace real, calibrado por erros que custaram sessões inteiras
de trabalho, e depois separado do projeto de origem para servir a qualquer um.

## O que ele traz

- **Três marchas de rigor** (Rápida / Padrão / AAA), escolhidas antes de ler código. A marcha que o
  agente escolhe é **piso, nunca teto**: se o projeto declara um mapa `caminho → marcha`, ele vence.
- **Oito lentes de inspeção distintas** — não oito cópias do mesmo revisor. Oito cópias acham o mesmo
  problema oito vezes; oito lentes acham oito classes de problema.
- **Inspeção cega A/B** com regra anti-teatro: achado sem `arquivo:linha` não conta como achado.
- **Convergência com teto**: duas rondas secas aprovam, três rondas é o limite, e conserto que quebra
  o conserto anterior manda parar de remendar.
- **Guarda-corpos** que impedem o rigor de virar estrago: achado fora de escopo vira registro, nunca
  correção; menor diff seguro; arquivo já modificado pertence a outra frente.
- **Gatilhos contáveis** de troca de chat, para o plano não passar a ser executado de memória.
- **O que um "pronto" precisa provar** — evidência fresca colada, e o que não rodou declarado.
- **Armadilhas de ambiente** que só se aprende apanhando: heredoc que come barra invertida e crase,
  encoding de hook em Windows, índice de git com CRLF, skill que não sobe de diretório.

## Instalação

```
/plugin marketplace add wendellmcs/padrao-aaa-universal
/plugin install padrao-aaa-universal@padrao-aaa-universal
```

Depois disso a skill carrega sozinha quando a tarefa corresponde ao gatilho.

> ⚠️ **Se você já tinha uma cópia em `~/.claude/skills/padrao-aaa-universal/`, remova-a após
> instalar.** Duas cópias com o mesmo nome é ambiguidade, e ambiguidade em manual de execução é pior
> que não ter manual.

## O adaptador — a parte que é sua

O manual é o procedimento; ele **não inventa fato sobre o seu projeto**. Todo valor concreto entra por
fatia, e as fatias aparecem no texto assim:

- `{{campo:X}}` — referência a um campo de configuração do projeto (comando de teste, arquivos
  intocáveis, quem decide). **Referência, nunca o valor**: comando muda, nome de campo não.
- `{{texto:X}}` — resposta de julgamento que varredura nenhuma responde (contra o que se compara, o
  que este produto não pode parecer, o que está fora de escopo).

Na primeira vez que rodar num projeto, a skill procura um adaptador. Não achando, ela **oferece
criar** — varre o repositório primeiro e depois faz as cinco perguntas que a varredura não responde:

| # | Pergunta |
|---|---|
| 1 | Este projeto é interno ou público? |
| 2 | Quais arquivos mandam de verdade, e em que ordem? |
| 3 | Qual comando prova que está pronto? |
| 4 | O que não se pode tocar? |
| 5 | Quem decide? |

**Sem adaptador ele ainda funciona** — em modo degradado, e *declarando* quais portões não consegue
verificar ali. O risco nunca foi a ausência do portão; é o silêncio sobre ela.

## O que ele NÃO é

- **Não é portão determinístico.** É texto que o agente lê e segue. Se você quer mecanismo que
  *bloqueia* em vez de instruir, isso é outro tipo de ferramenta — e as duas se complementam: o
  manual manda colar a evidência, um portão confere que colou.
- **Não é regra de negócio.** Ele não sabe nada do seu domínio, e não deve fingir que sabe.
- **Não julga se ficou bonito.** Sem uma régua declarada, a lente visual responde "vaza?" e não
  responde "está bom?".

## Convenções internas

Duas, e as duas existem por cicatriz:

1. **Referência por seção nomeada, nunca por número de linha.** Âncora de linha apodrece em silêncio:
   no projeto de origem, 9 de 9 âncoras haviam passado a apontar para linha vazia — numa skill cuja
   regra central é exigir evidência citada.
2. **Número medido vem com a forma de recontá-lo.** Número cravado envelhece; número com o comando ao
   lado se corrige sozinho.

## Licença

MIT. Ver [LICENSE](LICENSE).
