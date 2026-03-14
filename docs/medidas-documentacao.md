# Documentação das Medidas: Projeto Logística — TransFlow Logistics

Este documento lista todas as medidas criadas no modelo Power BI, suas regras de negócio, dependências e retornos esperados.

---

## Medidas de Devolução (Absoluto)

### devolucao_arrependimento
```DAX
-- Medida: devolucao_arrependimento
-- Descrição: Quantidade de pedidos devolvidos por motivo de arrependimento
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Considera apenas registros onde motivo_devolucao = "Arrependimento"
-- Dependência:
--     [quantidade_pedidos]
-- Retorno:
--     Número inteiro de pedidos devolvidos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        'fLogistica'[motivo_devolucao] = "Arrependimento"
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Quantidade de pedidos devolvidos por motivo de arrependimento.

### devolucao_danificado
```DAX
-- Medida: devolucao_danificado
-- Descrição: Quantidade de pedidos devolvidos por motivo de produto danificado
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Considera apenas registros onde motivo_devolucao = "Danificado"
-- Dependência:
--     [quantidade_pedidos]
-- Retorno:
--     Número inteiro de pedidos devolvidos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        'fLogistica'[motivo_devolucao] = "Danificado"
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Quantidade de pedidos devolvidos por motivo Danificado.

### devolucao_produto_errado
```DAX
-- Medida: devolucao_produto_errado
-- Descrição: Quantidade de pedidos devolvidos por motivo de produto errado
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Considera apenas registros onde motivo_devolucao = "Produto Errado"
-- Dependência:
--     [quantidade_pedidos]
-- Retorno:
--     Número inteiro de pedidos devolvidos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        'fLogistica'[motivo_devolucao] = "Produto Errado"
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Quantidade de pedidos devolvidos por motivo Produto Errado.

### produtos_devolvidos
```DAX
-- Medida: produtos_devolvidos
-- Descrição: Total de produtos devolvidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Soma simples da coluna [quantidade_devolucao] da tabela fLogistica
-- Dependência:
--     'fLogistica'[quantidade_devolucao]
-- Retorno:
--     Número total de produtos devolvidos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    SUM(
        'fLogistica'[quantidade_devolucao]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Total de produtos devolvidos.

### sem_devolucao
```DAX
-- Medida: sem_devolucao
-- Descrição: Quantidade de pedidos sem devolução
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Considera apenas registros onde motivo_devolucao = "Sem Devolução"
-- Dependência:
--     [quantidade_pedidos]
-- Retorno:
--     Número inteiro de pedidos sem devolução
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        'fLogistica'[motivo_devolucao] = "Sem Devolução"
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Quantidade de pedidos sem devolução.

---

## Medidas de Devolução (Percentual)

### percentual_arrependimento
```DAX
-- Medida: percentual_arrependimento
-- Descrição: Percentual de pedidos devolvidos por arrependimento em relação ao total de pedidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Divide o número de pedidos devolvidos por arrependimento pela quantidade total de pedidos
-- Dependência:
--     [devolucao_arrependimento], [quantidade_pedidos]
-- Retorno:
--     Percentual (0 a 1) de pedidos devolvidos por arrependimento
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

VAR _Resultado =
    DIVIDE(
        [devolucao_arrependimento],
        [quantidade_pedidos]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Percentual de pedidos devolvidos por arrependimento.

### percentual_danificado
```DAX
-- Medida: percentual_danificado
-- Descrição: Percentual de pedidos devolvidos por motivo "Danificado" em relação ao total de pedidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Divide o número de pedidos devolvidos por dano pelo total de pedidos
-- Dependência:
--     [devolucao_danificado], [quantidade_pedidos]
-- Retorno:
--     Percentual (0 a 1) de pedidos devolvidos por motivo Danificado
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

VAR _Resultado =
    DIVIDE(
        [devolucao_danificado],
        [quantidade_pedidos]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Percentual de pedidos devolvidos por motivo Danificado.

### percentual_produto_errado
```DAX
-- Medida: percentual_produto_errado
-- Descrição: Percentual de pedidos devolvidos por motivo "Produto Errado" em relação ao total de pedidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Divide o número de pedidos devolvidos por motivo "Produto Errado" pelo total de pedidos
-- Dependência:
--     [devolucao_produto_errado], [quantidade_pedidos]
-- Retorno:
--     Percentual (0 a 1) de pedidos devolvidos por motivo Produto Errado
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

VAR _Resultado =
    DIVIDE(
        [devolucao_produto_errado],
        [quantidade_pedidos]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Percentual de pedidos devolvidos por Produto Errado.

### percentual_produtos_devolvidos
```DAX
-- Medida: percentual_produtos_devolvidos
-- Descrição: Percentual de produtos devolvidos em relação ao total de produtos vendidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Divide o total de produtos devolvidos pelo total de produtos vendidos
-- Dependência:
--     [produtos_devolvidos], [quantidade_produtos]
-- Retorno:
--     Percentual (0 a 1) de produtos devolvidos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

VAR _Resultado =
    DIVIDE(
        [produtos_devolvidos],
        [quantidade_produtos]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Percentual de produtos devolvidos.

### percentual_sem_devolucao
```DAX
-- Medida: percentual_sem_devolucao
-- Descrição: Percentual de pedidos sem devolução em relação ao total de pedidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Divide o número de pedidos sem devolução pelo total de pedidos
-- Dependência:
--     [sem_devolução], [quantidade_pedidos]
-- Retorno:
--     Percentual (0 a 1) de pedidos sem devolução
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

VAR _Resultado =
    DIVIDE(
        [sem_devolucao],
        [quantidade_pedidos]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Percentual de pedidos sem devolução.

## Medidas de Entregas

### entregas_prazo
```DAX
-- Medida: entregas_prazo
-- Descrição: Quantidade de pedidos entregues dentro do prazo
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Considera apenas registros onde status = "No Prazo"
-- Dependência:
--     [quantidade_pedidos]
-- Retorno:
--     Número inteiro de pedidos entregues no prazo
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        'fLogistica'[status] = "No Prazo"
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Quantidade de pedidos entregues dentro do prazo.

### percentual_entregas_prazo
```DAX
-- Medida: percentual_entregas_prazo
-- Descrição: Percentual de pedidos entregues dentro do prazo em relação ao total de pedidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Divide o número de pedidos entregues no prazo pelo total de pedidos
-- Dependência:
--     [entregas_prazo], [quantidade_pedidos]
-- Retorno:
--     Percentual (0 a 1) de pedidos entregues dentro do prazo
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

VAR _Resultado =
    DIVIDE(
        [entregas_prazo],
        [quantidade_pedidos]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Percentual de pedidos entregues dentro do prazo.

## Medidas de Faturamento

### faturamento
```DAX
-- Medida: faturamento
-- Descrição: Soma do valor faturado de todos os pedidos
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Soma simples da coluna [valor_faturamento] da tabela fLogistica
-- Dependência:
--     'fLogistica'[valor_faturamento]
-- Retorno:
--     Valor monetário total faturado
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    SUM(
        'fLogistica'[valor_faturamento]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Soma do valor faturado de todos os pedidos.


## Medidas de Contagem

### quantidade_motoristas
```DAX
-- Medida: quantidade_motoristas
-- Descrição: Quantidade distinta de motoristas registrados na tabela fLogistica
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Conta todos os motoristas distintos na coluna [nome_motorista]
-- Dependência:
--     'fLogistica'[nome_motorista]
-- Retorno:
--     Número inteiro de motoristas distintos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    DISTINCTCOUNT(
        'fLogistica'[nome_motorista]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Quantidade distinta de motoristas registrados.

### quantidade_pedidos
```DAX
-- Medida: quantidade_pedidos
-- Descrição: Total de pedidos registrados na tabela fLogistica
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Conta todas as linhas da tabela fLogistica, representando cada pedido
-- Dependência:
--     'fLogistica'
-- Retorno:
--     Número inteiro de pedidos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    COUNTROWS(
        'fLogistica'
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Total de pedidos registrados na tabela fLogistica.

### quantidade_produtos
```DAX
-- Medida: quantidade_produtos
-- Descrição: Total de produtos registrados na tabela fLogistica
-- Tabela origem: fLogistica
-- Regra de negócio:
--     Soma todos os itens de produtos na coluna [quantidade_itens] da tabela fLogistica
-- Dependência:
--     'fLogistica'[quantidade_itens]
-- Retorno:
--     Número total de produtos
-- Observação:
--     COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    SUM(
        'fLogistica'[quantidade_itens]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Total de produtos registrados na tabela fLogistica.

---

---

---

---



