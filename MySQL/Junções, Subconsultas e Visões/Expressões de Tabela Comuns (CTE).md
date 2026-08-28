# Expressões de Tabela Comuns (`CTE` - *Common Table Expressions*)

Uma **CTE (Common Table Expression)** é um conjunto de resultados temporário e nomeado, definido dentro do escopo de execução de uma única instrução (`SELECT`, `INSERT`, `UPDATE` ou `DELETE`) usando a cláusula **`WITH`**.

Introduzidas a partir do **MySQL 8.0**, as CTEs substituem subconsultas aninhadas complexas com muito mais legibilidade e elegância.

---

## Vantagens em Relação a Subconsultas Tradicionais

1. **Legibilidade Superior:** A consulta é lida de cima para baixo em sequência lógica.
2. **Reutilização:** Uma mesma CTE pode ser referenciada múltiplas vezes na consulta principal.
3. **Manutenção Simplificada:** Facilita isolar blocos lógicos e regras de negócio.

---

## Sintaxe Geral

```sql
WITH nome_cte AS (
    SELECT coluna1, coluna2
    FROM tabela
    WHERE condicao
)
SELECT * 
FROM nome_cte
WHERE condicao_adicional;
```

---

## Exemplos Práticos

### 1. Simplificando Cálculos de Média de Vendas

```sql
WITH ResumoVendasVendedor AS (
    SELECT 
        v.matricula,
        v.nome,
        COUNT(nf.numero) AS total_pedidos,
        SUM(inf.quantidade * inf.preco) AS faturamento_total
    FROM tabela_de_vendedores AS v
    INNER JOIN notas_fiscais AS nf ON v.matricula = nf.matricula
    INNER JOIN itens_notas_fiscais AS inf ON nf.numero = inf.numero
    GROUP BY v.matricula, v.nome
)
SELECT 
    matricula,
    nome,
    total_pedidos,
    faturamento_total,
    ROUND(faturamento_total / total_pedidos, 2) AS ticket_medio
FROM ResumoVendasVendedor
WHERE faturamento_total > 50000.00
ORDER BY faturamento_total DESC;
```

---

### 2. Múltiplas CTEs Encadeadas

```sql
WITH 
ClientesSP AS (
    SELECT cpf, nome, bairro 
    FROM tabela_de_clientes 
    WHERE estado = 'SP'
),
VendasSP AS (
    SELECT nf.cpf, SUM(inf.quantidade * inf.preco) AS total_gasto
    FROM notas_fiscais nf
    INNER JOIN itens_notas_fiscais inf ON nf.numero = inf.numero
    GROUP BY nf.cpf
)
SELECT 
    c.nome,
    c.bairro,
    COALESCE(v.total_gasto, 0.00) AS total_compras
FROM ClientesSP c
LEFT JOIN VendasSP v ON c.cpf = v.cpf
ORDER BY total_compras DESC;
```

---

## Referência Oficial
- [Documentação Oficial do MySQL 8.4 - WITH (Common Table Expressions)](https://dev.mysql.com/doc/refman/8.4/en/with.html)
