# Funções Matemáticas e Classificação

O MySQL possui um conjunto robusto de funções matemáticas para cálculos, arredondamentos e funções analíticas de janela (*Window Functions*) para ranqueamento de dados.

---

## 1. Funções Matemáticas e Arredondamento

```sql
-- Valor Absoluto (remove o sinal negativo)
SELECT ABS(-23.2); -- Retorna 23.2

-- Arredondamento para Cima (teto)
SELECT CEILING(23.10); -- Retorna 24

-- Arredondamento para Baixo (piso)
SELECT FLOOR(23.10); -- Retorna 23

-- Arredondamento Padrão com Casas Decimais
SELECT ROUND(23.10);    -- Retorna 23
SELECT ROUND(23.76);    -- Retorna 24
SELECT ROUND(23.456, 2);-- Retorna 23.46

-- Potência e Raiz Quadrada
SELECT POWER(2, 3); -- 2 elevado a 3 = 8
SELECT SQRT(64);    -- Raiz quadrada de 64 = 8

-- Resto da Divisão Inteira (Módulo)
SELECT MOD(10, 3); -- Retorna 1
```

---

## 2. Aplicação em Faturamento e Impostos

```sql
-- Calculando o faturamento total arredondado por item
SELECT 
    produto, 
    quantidade, 
    preco, 
    ROUND(quantidade * preco, 2) AS faturamento 
FROM itens_notas_fiscais;

-- Calculando a média arredondada de preço e quantidade por produto
SELECT 
    produto, 
    FLOOR(AVG(preco)) AS media_preco_piso, 
    ROUND(AVG(quantidade), 2) AS media_qtde 
FROM itens_notas_fiscais 
GROUP BY produto;
```

![[Untitled 512.png]]

```sql
-- Cálculo do imposto total sobre produtos vendidos em 2016
SELECT 
    YEAR(data_venda) AS ano_venda, 
    FLOOR(SUM(imposto * (quantidade * preco))) AS total_imposto_calculado
FROM notas_fiscais nf 
INNER JOIN itens_notas_fiscais inf ON nf.numero = inf.numero
WHERE YEAR(data_venda) = 2016
GROUP BY YEAR(data_venda);
```

![[Untitled 513.png]]

---

## 3. Funções de Classificação e Janela: `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`

Introduzidas no MySQL 8.0, as funções analíticas de janela permitem ranquear e ordenar partições sem a necessidade de colapsar as linhas em um `GROUP BY`.

### Diferença entre as Funções de Janela:

- **`RANK()`:** Em caso de empate, atribui a mesma posição e **pula** as posições seguintes correspondentes à quantidade de empates (ex.: 1º, 2º, 2º, 4º).
- **`DENSE_RANK()`:** Em caso de empate, atribui a mesma posição e **não pula** as posições seguintes (ex.: 1º, 2º, 2º, 3º).
- **`ROW_NUMBER()`:** Atribui um número sequencial exclusivo e estrito para cada linha do grupo (ex.: 1, 2, 3, 4).

### Exemplo: Ranqueando Vendas por Região

```sql
SELECT 
    vendedor,
    regiao,
    total_vendas,
    RANK() OVER (PARTITION BY regiao ORDER BY total_vendas DESC) AS rank_vendas,
    DENSE_RANK() OVER (PARTITION BY regiao ORDER BY total_vendas DESC) AS dense_rank_vendas
FROM vendas;
```
