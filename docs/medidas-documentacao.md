# Documentação das Medidas: Projeto Logística — TransFlow Logistics

Este documento lista todas as medidas criadas no modelo Power BI, suas regras de negócio, dependências e retornos esperados.

---

## Medidas de Devolução (Absoluto)

### devolucao_arrependimento
```DAX
devolucao_arrependimento = 

-- Medida:
--      devolucao_arrependimento
--
-- Descrição:
--      Quantidade de pedidos devolvidos por motivo de arrependimento
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Considera apenas registros onde motivo_devolucao = "Arrependimento"
--
-- Dependência:
--      [quantidade_pedidos]
--
-- Retorno:
--      Número inteiro de pedidos devolvidos
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        fPedidos_Realizados[id_motivo]="1"
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
devolucao_danificado = 

-- Medida:
--      devolucao_danificado
--
-- Descrição:
--      Quantidade de pedidos devolvidos por motivo de produto danificado
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Considera apenas registros onde motivo_devolucao = "Danificado"
--
-- Dependência:
--      [quantidade_pedidos]
--
-- Retorno:
--      Número inteiro de pedidos devolvidos
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        fPedidos_Realizados[id_motivo]="2"
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
devolucao_produto_errado = 

-- Medida:
--      devolucao_produto_errado
--
-- Descrição:
--      Quantidade de pedidos devolvidos por motivo de produto errado
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Considera apenas registros onde motivo_devolucao = "Produto Errado"
--
-- Dependência:
--      [quantidade_pedidos]
--
-- Retorno:
--      Número inteiro de pedidos devolvidos
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        fPedidos_Realizados[id_motivo]="3"
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
produtos_devolvidos = 

-- Medida:
--      produtos_devolvidos
--
-- Descrição:
--      Total de produtos devolvidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Soma simples da coluna [quantidade_devolucao] da tabela fPedidos_Realizados
--
-- Dependência:
--      'fPedidos_Realizados'[quantidade_devolucao]
--
-- Retorno:
--      Número total de produtos devolvidos
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    SUM(
        fPedidos_Realizados[quantidade_devolucao]
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
sem_devolucao = 

-- Medida:
--      sem_devolucao
--
-- Descrição:
--      Quantidade de pedidos sem devolução
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Considera apenas registros onde motivo_devolucao = "Sem Devolução"
--
-- Dependência:
--      [quantidade_pedidos]
--
-- Retorno:
--      Número inteiro de pedidos sem devolução
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        fPedidos_Realizados[id_motivo]="4"
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
percentual_arrependimento = 

-- Medida:
--      percentual_arrependimento
--
-- Descrição:
--      Percentual de pedidos devolvidos por arrependimento em relação ao total de pedidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Divide o número de pedidos devolvidos por arrependimento pela quantidade total de pedidos
--
-- Dependência:
--      [devolucao_arrependimento], [quantidade_pedidos]
--
-- Retorno:
--      Percentual (0 a 1) de pedidos devolvidos por arrependimento
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

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
percentual_danificado = 

-- Medida:
--      percentual_danificado
--
-- Descrição:
--      Percentual de pedidos devolvidos por motivo "Danificado" em relação ao total de pedidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Divide o número de pedidos devolvidos por dano pelo total de pedidos
--
-- Dependência:
--      [devolucao_danificado], [quantidade_pedidos]
--
-- Retorno:
--      Percentual (0 a 1) de pedidos devolvidos por motivo Danificado
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

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
percentual_produto_errado = 

-- Medida:
--      percentual_produto_errado
--
-- Descrição:
--      Percentual de pedidos devolvidos por motivo "Produto Errado" em relação ao total de pedidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Divide o número de pedidos devolvidos por motivo "Produto Errado" pelo total de pedidos
--
-- Dependência:
--      [devolucao_produto_errado], [quantidade_pedidos]
--
-- Retorno:
--      Percentual (0 a 1) de pedidos devolvidos por motivo Produto Errado
--
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
percentual_produtos_devolvidos = 

-- Medida:
--      percentual_produtos_devolvidos
--
-- Descrição:
--      Percentual de produtos devolvidos em relação ao total de produtos vendidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Divide o total de produtos devolvidos pelo total de produtos vendidos
--
-- Dependência:
--      [produtos_devolvidos], [quantidade_produtos]
--
-- Retorno:
--      Percentual (0 a 1) de produtos devolvidos
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

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
percentual_sem_devolucao = 

-- Medida:
--      percentual_sem_devolucao
--
-- Descrição:
--      Percentual de pedidos sem devolução em relação ao total de pedidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Divide o número de pedidos sem devolução pelo total de pedidos
--
-- Dependência:
--      [sem_devolução], [quantidade_pedidos]
--
-- Retorno:
--      Percentual (0 a 1) de pedidos sem devolução
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

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

---

## Medidas de Entregas

### entregas_prazo
```DAX
entregas_prazo = 

-- Medida:
--      entregas_prazo
--
-- Descrição:
--      Quantidade de pedidos entregues dentro do prazo
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Considera apenas registros onde status = "No Prazo"
--
-- Dependência:
--      [quantidade_pedidos]
--
-- Retorno:
--      Número inteiro de pedidos entregues no prazo
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    CALCULATE(
        [quantidade_pedidos],
        fPedidos_Realizados[id_status]="2"
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
percentual_entregas_prazo = 

-- Medida:
--      percentual_entregas_prazo
--
-- Descrição:
--      Percentual de pedidos entregues dentro do prazo em relação ao total de pedidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Divide o número de pedidos entregues no prazo pelo total de pedidos
--
-- Dependência:
--      [entregas_prazo], [quantidade_pedidos]
--
-- Retorno:
--      Percentual (0 a 1) de pedidos entregues dentro do prazo
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK() e divisão por zero

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

---

## Medida de Faturamento

### faturamento
```DAX
faturamento = 

-- Medida:
--      faturamento
--
-- Descrição:
--      Soma do valor faturado de todos os pedidos
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Soma simples da coluna [faturamento] da tabela fPedidos_Realizados
--
-- Dependência:
--      'fPedidos_Realizados'[faturamento]
--
-- Retorno:
--      Valor monetário total faturado
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    SUM(
        fPedidos_Realizados[faturamento]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Soma do valor faturado de todos os pedidos.

---

## Medidas de Contagem

### quantidade_motoristas
```DAX
quantidade_motoristas = 

-- Medida:
--      quantidade_motoristas
--
-- Descrição:
--      Quantidade de motoristas ativos na tabela dMotoristas
--
-- Tabela origem:
--      dMotoristas
--
-- Regra de negócio:
--      Conta todos os motoristas ativos na tabela dMotoristas
--
-- Dependência:
--      dMotoristas
--
-- Retorno:
--      Número inteiro de motoristas ativos
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    COUNTROWS(
        dMotoristas
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
quantidade_pedidos = 

-- Medida:
--      quantidade_pedidos
--
-- Descrição:
--      Total de pedidos registrados na tabela fPedidos_Realizados
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Conta todas as linhas da tabela fPedidos_Realizados, representando cada pedido
--
-- Dependência:
--      'fPedidos_Realizados'
--
-- Retorno:
--      Número inteiro de pedidos
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    COUNTROWS(
        fPedidos_Realizados
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
quantidade_produtos = 

-- Medida:
--      quantidade_produtos
--
-- Descrição:
--      Total de produtos transportados na tabela fPedidos_Realizados
--
-- Tabela origem:
--      fPedidos_Realizados
--
-- Regra de negócio:
--      Soma todos os itens de produtos na coluna [quantidade_itens] da tabela fPedidos_Realizados
--
-- Dependência:
--      'fPedidos_Realizados'[quantidade_itens]
--
-- Retorno:
--      Número total de produtos transportados
--
-- Observação:
--      COALESCE é utilizado para evitar retorno BLANK()

VAR _Resultado =
    SUM(
        fPedidos_Realizados[quantidade_itens]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```
Descrição: Total de produtos registrados na tabela fLogistica.
