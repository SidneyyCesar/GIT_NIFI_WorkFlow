PROCESSAMENTO - LAUDO DE AMOSTRA

CONSUMEAMQP:
FLUXO 1

LaudoComprasQueue

EXECUTESQL
FROM PROP_COMPRAS A
WHERE PROPRIEDADE = '00180'
AND (PEDIDO = '${CodigoPedido}' OR PEDIDO = REPLACE('${CodigoPedido}','A',''))


FLUXO 2
LaudoQualidadeQueue

EXECUTESQL

UPDATE A SET A.VALOR_PROPRIEDADE = '${status}'
FROM PROP_COMPRAS A
WHERE PROPRIEDADE = '00178'
AND (PEDIDO = '${CodigoPedido}' OR PEDIDO = REPLACE('${CodigoPedido}','A',''))

VARIAVEIS

EvaluatesJsonPath
  $.CodigoPedido
  $.status
  UPDATE A SET A.VALOR_PROPRIEDADE = '${status}'
