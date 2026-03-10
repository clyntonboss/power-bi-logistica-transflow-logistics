# Documentação das Medidas - Projeto TransFlow Logistics
# Projeto Logística — TransFlow Logistics

Este documento lista todas as medidas criadas no modelo Power BI, suas regras de negócio, dependências e retornos esperados.

---

## Medidas de Contagem

### quantidade_pedidos
```DAX
VAR Resultado = COUNTROWS('fLogistica')
RETURN COALESCE(Resultado, 0)
```
Descrição: Total de pedidos registrados na tabela fLogistica.

### quantidade_produtos
```DAX
VAR Resultado = SUM('fLogistica'[quantidade_itens])
RETURN COALESCE(Resultado, 0)
```
Descrição: Total de produtos registrados na tabela fLogistica.

### quantidade_motoristas
```DAX
VAR Resultado = DISTINCTCOUNT('fLogistica'[nome_motorista])
RETURN COALESCE(Resultado, 0)
```
Descrição: Quantidade distinta de motoristas registrados.

---

## Medidas de Devolução

### devolucao_arrependimento
```DAX
VAR Resultado = CALCULATE([quantidade_pedidos], 'fLogistica'[motivo_devolucao] = "Arrependimento")
RETURN COALESCE(Resultado, 0)
```
Descrição: Quantidade de pedidos devolvidos por motivo de arrependimento.

### devolucao_danificado
```DAX
VAR Resultado = CALCULATE([quantidade_pedidos], 'fLogistica'[motivo_devolucao] = "Danificado")
RETURN COALESCE(Resultado, 0)
```
Descrição: Quantidade de pedidos devolvidos por motivo Danificado.

### devolucao_produto_errado
```DAX
VAR Resultado = CALCULATE([quantidade_pedidos], 'fLogistica'[motivo_devolucao] = "Produto Errado")
RETURN COALESCE(Resultado, 0)
```
Descrição: Quantidade de pedidos devolvidos por motivo Produto Errado.

### sem_devolucao
```DAX
VAR Resultado = CALCULATE([quantidade_pedidos], 'fLogistica'[motivo_devolucao] = "Sem Devolução")
RETURN COALESCE(Resultado, 0)
```
Descrição: Quantidade de pedidos sem devolução.

### produtos_devolvidos
```DAX
VAR Resultado = SUM('fLogistica'[quantidade_devolucao])
RETURN COALESCE(Resultado, 0)
```
Descrição: Total de produtos devolvidos.

---

## Medidas de Entregas

### entregas_prazo
```DAX
VAR Resultado = CALCULATE([quantidade_pedidos], 'fLogistica'[status] = "No Prazo")
RETURN COALESCE(Resultado, 0)
```
Descrição: Quantidade de pedidos entregues dentro do prazo.

---

## Medidas de Faturamento

### faturamento
```DAX
VAR Resultado = SUM('fLogistica'[valor_faturamento])
RETURN COALESCE(Resultado, 0)
```
Descrição: Soma do valor faturado de todos os pedidos.

---

## Medidas de Percentual

### percentual_arrependimento
```DAX
VAR Resultado = DIVIDE([devolucao_arrependimento], [quantidade_pedidos])
RETURN COALESCE(Resultado, 0)
```
Descrição: Percentual de pedidos devolvidos por arrependimento.

### percentual_danificado
```DAX
VAR Resultado = DIVIDE([devolucao_danificado], [quantidade_pedidos])
RETURN COALESCE(Resultado, 0)
```
Descrição: Percentual de pedidos devolvidos por motivo Danificado.

### percentual_produto_errado
```DAX
VAR Resultado = DIVIDE([devolucao_produto_errado], [quantidade_pedidos])
RETURN COALESCE(Resultado, 0)
```
Descrição: Percentual de pedidos devolvidos por Produto Errado.

### percentual_entregas_prazo
```DAX
VAR Resultado = DIVIDE([entregas_prazo], [quantidade_pedidos])
RETURN COALESCE(Resultado, 0)
```
Descrição: Percentual de pedidos entregues dentro do prazo.

### percentual_produtos_devolvidos
```DAX
VAR Resultado = DIVIDE([produtos_devolvidos], [quantidade_produtos])
RETURN COALESCE(Resultado, 0)
```
Descrição: Percentual de produtos devolvidos.

### percentual_sem_devolucao
```DAX
VAR Resultado = DIVIDE([sem_devolucao], [quantidade_pedidos])
RETURN COALESCE(Resultado, 0)
```
Descrição: Percentual de pedidos sem devolução.

