# QualiLLM: instruções dos juízes

Este repositório reúne as instruções dos juízes automáticos (LLM-as-a-judge) do **QualiLLM**
(Qualidade de Aplicações que Consomem LLMs). O QualiLLM é um framework de avaliação de
qualidade para aplicações que consomem LLMs via API, proposto no Trabalho de Conclusão de Curso
de Myrna Gabrielle Bastos de Castro (Ciência da Computação, UFOPA, 2026): *Teste de software em
sistemas que integram inteligência artificial generativa: limitações das técnicas tradicionais
e proposta de um framework de avaliação de qualidade*.

> [!WARNING]
> **Só os arquivos `nucleo.md` valem para qualquer aplicação.** Todo o resto foi escrito para o
> estudo de caso do TCC, um assistente de negociação de dívidas com RAG, e **precisa ser
> ajustado para a aplicação que você vai testar**:
> - os apêndices de domínio (`dominio_negociacao.md`);
> - as regras fixas (`exemplo_negociacao/regras_fixas.md`);
> - as duas instruções de tom (`prompts/tom/`).
>
> Esses arquivos começam com um comentário HTML que avisa isso. **Tire o comentário antes de
> enviar o texto ao juiz**: ele não fazia parte do que os juízes receberam no estudo de caso.

## Estrutura

```
prompts/
  equivalencia/  nucleo.md  dominio_negociacao.md
  fidelidade/    nucleo.md  dominio_negociacao.md
  groundedness/  nucleo.md  dominio_negociacao.md
  toxicidade/    nucleo.md  dominio_negociacao.md
  equidade/      nucleo.md  dominio_negociacao.md
  robustez/      nucleo.md  dominio_negociacao.md
  tom/           por_turno.md  por_sessao.md
exemplo_negociacao/
  regras_fixas.md
```

| Métrica | Categoria | Arquivos |
|---|---|---|
| Taxa de consistência, total e por pares | Confiabilidade | `prompts/equivalencia/` |
| Fidelidade factual | Factualidade | `prompts/fidelidade/` |
| *Groundedness* | Aderência ao contexto | `prompts/groundedness/` |
| Taxa sem toxicidade | Segurança | `prompts/toxicidade/` |
| Fração dos grupos sem tratamento desigual | Equidade | `prompts/equidade/` |
| Taxa de resistência | Robustez | `prompts/robustez/` |
| Nota de tom, por turno e por sessão | Dimensão da aplicação | `prompts/tom/` |

As instruções de tom são recurso da plataforma e não entraram nas rodadas do estudo de caso.

A taxa de vazamento não tem instrução própria, porque se decide por asserção determinística
sobre dados conhecidos de antemão.

## Como usar

**O núcleo vale para qualquer aplicação.** Ele define a pergunta, o vocabulário do veredito,
as regras de decisão e o formato da resposta, com a justificativa antes do veredito. O
apêndice de domínio diz o que conta como fato, regra ou dano na aplicação testada, e é
reescrito para cada uma.

**Como os dois se combinam.** A instrução enviada ao juiz é o núcleo seguido do apêndice:
1. o texto do núcleo, sem os espaços e quebras de linha do fim;
2. uma linha em branco;
3. o texto do apêndice, sem espaços e quebras de linha no começo e no fim;
4. uma quebra de linha final.

Sem apêndice, ou com apêndice vazio, vai só o núcleo. O núcleo vem primeiro porque é ele que
define a tarefa; o apêndice especializa o que já foi definido.

**As instruções de tom não se combinam.** Cada uma vai inteira, como está, porque o tom é
dimensão específica da aplicação e a régua vem toda do domínio.

**O ponto de corte da toxicidade e os limiares ficam fora da instrução.** O juiz devolve o
veredito, e quem aplica o framework define o que é aceitável.

### Material do juiz

Além da instrução, o juiz recebe o material do turno. Ele vem destas origens:

| Material do juiz | Origem na aplicação | Quando existe |
|---|---|---|
| Dados consultados | banco de dados e regras de negócio | quando a aplicação consulta dados |
| Trechos recuperados | base de conhecimento consultada por RAG | só em aplicações com RAG |
| Regras fixas | prompt de sistema da aplicação | sempre, com o conteúdo de cada aplicação |

**As regras fixas não vêm do RAG.** Elas saem do prompt de sistema da aplicação, porque a
aplicação as tinha à mão ao responder, com ou sem recuperação. Os trechos do RAG chegam ao
juiz à parte, no contexto do turno.

No estudo de caso, os juízes de fidelidade, *groundedness* e robustez recebem as regras
fixas. Elas vão no material do turno, não na instrução. `exemplo_negociacao/regras_fixas.md`
mostra a lista do assistente de negociação, com os valores das regras de negócio já
preenchidos (até 24 parcelas, mínimo de R$ 50,00). Outra aplicação tira as suas do próprio
prompt de sistema.

## O que não está aqui

- **As asserções determinísticas.** Dependem dos referentes de cada aplicação (os dados, as
  regras de negócio e o formato que ela deve seguir) e devem ser construídas e ajustadas por
  quem aplica o framework. Ver a seção "Quando e como aplicar" e o Apêndice D do TCC.
- **O código da aplicação** do estudo de caso, com os estímulos, as conversas gravadas e os
  rótulos humanos, que está em
  [gabriellebcastro/qualillm-chatbot](https://github.com/gabriellebcastro/qualillm-chatbot).

## Versão

Instrumento congelado do estudo de caso, tag `v1.0-tcc`. O hash das regras fixas é
`d6ba731f26e8`: os 12 primeiros caracteres do SHA-256 do texto das regras em UTF-8, sem o
comentário da primeira linha e sem a quebra de linha final.

Os textos são cópias dos arquivos usados no estudo de caso, sem nenhuma alteração além do
comentário de aviso. Os dados de exemplo são fictícios.

## Licença

[CC BY 4.0](LICENSE).

## Como citar

CASTRO, Myrna Gabrielle Bastos de. **Teste de software em sistemas que integram inteligência
artificial generativa**: limitações das técnicas tradicionais e proposta de um framework de
avaliação de qualidade. 2026. Trabalho de Conclusão de Curso (Bacharelado em Ciência da
Computação) – Universidade Federal do Oeste do Pará, Santarém, 2026.
