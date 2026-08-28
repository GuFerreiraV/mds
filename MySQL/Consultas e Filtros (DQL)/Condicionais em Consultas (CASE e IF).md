# Condicionais em Consultas (`CASE` e `IF`)

O SQL permite aplicar lógicas condicionais dinâmicas dentro de consultas `SELECT`, atribuindo valores, classificações e rótulos com base em regras de negócio.

---

## 1. A Estrutura `CASE WHEN`

A expressão `CASE` avalia uma lista de condições e retorna um resultado correspondente à primeira condição verdadeira.

### Sintaxe Pesquisada (Searched CASE)

```sql
CASE 
    WHEN condicao1 THEN resultado1
    WHEN condicao2 THEN resultado2
    ELSE resultado_padrao
END
```

### Exemplo 1: Categorização de Status de Horas

```sql
SELECT 
    login,
    total_horas,
    CASE 
        WHEN total_horas >= 184 THEN 'Meta Atingida'
        WHEN total_horas >= 160 THEN 'Em Andamento'
        ELSE 'Horas Faltantes'
    END AS status_meta,
    CASE 
        WHEN total_horas >= 184 THEN 0
        ELSE 184 - total_horas
    END AS saldo_horas_restantes
FROM (
    SELECT 
        login,
        SUM(horas_trabalhadas) AS total_horas
    FROM tb_apontamentos_jira
    GROUP BY login
) AS resumo_horas;
```

### Exemplo 2: Classificação de Clientes por Faixa de Preço

```sql
SELECT 
    nome_do_produto,
    preco_de_lista,
    CASE 
        WHEN preco_de_lista >= 12.00 THEN 'Produto Premium'
        WHEN preco_de_lista >= 7.00 THEN 'Produto Médio'
        ELSE 'Produto Econômico'
    END AS faixa_preco
FROM tabela_de_produtos
ORDER BY preco_de_lista DESC;
```

---

## 2. A Função `IF()`

Para testes binários rápidos (equivalente ao operador ternário `condicao ? val1 : val2`), o MySQL fornece a função `IF`:

```sql
-- Sintaxe: IF(condicao, valor_se_verdadeiro, valor_se_falso)
SELECT 
    nome,
    limite_de_credito,
    IF(limite_de_credito >= 50000, 'VIP', 'Padrão') AS categoria_cliente
FROM tabela_de_clientes;
```
