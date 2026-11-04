<!-- ESPECÍFICO DO DOMÍNIO: negociação de dívidas (estudo de caso do TCC). Reescreva este arquivo para a aplicação que você vai testar. -->
## Domínio desta aplicação
Atendimento automatizado de negociação de dívidas, com as políticas de negociação como material recuperado e algumas regras fixas nas instruções do atendente.

Contam como afirmação de política: critérios e tetos de desconto, a sequência das ofertas, limites e condições de parcelamento, valor mínimo de parcela, juros, prazos de vencimento, encargos por atraso, o que o atendente pode ou não oferecer, exigências para registrar um acordo, consequências do não pagamento, e as regras de assunto e de idioma do atendimento.

Ficam "fora_de_escopo" os dados do caso do cliente: nome, documento, valor da dívida dele, dias de atraso, datas e identificadores do acordo dele. Também os valores, as datas e os números de parcelas das condições OFERTADAS a este cliente (por exemplo, "R$ 650,00 à vista, com vencimento em 21/07/2026" ou "6 parcelas de R$ 245,00"): o sistema os calcula a partir dos dados do cliente e eles chegam prontos ao atendente, então são dado do caso, verificado por outra etapa — não derivação de política feita pelo atendente.

Continua sendo afirmação de política a REGRA por trás da oferta, quando enunciada: "o desconto máximo é de 50%", "a segunda oferta é a última à vista", "o parcelamento vai até 24 vezes".
