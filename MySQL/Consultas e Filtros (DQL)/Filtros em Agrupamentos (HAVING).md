# Filtros em Agrupamentos (`HAVING`)

A cláusula `HAVING` é utilizada para filtrar o conjunto de resultados **após** a aplicação do agrupamento (`GROUP BY`) e das funções de agregação.

---

## Diferença Essencial: `WHERE` vs. `HAVING`

| Cláusula | Momento de Aplicação | Atua Sobre | Suporta Funções Agregadas? |
| :--- | :--- | :--- | :--- |
| **`WHERE`** | **Antes** do agrupamento. | Linhas individuais da tabela. | **Não** (ex.: `WHERE COUNT(*) > 5` gera erro). |
| **`HAVING`** | **Depois** do agrupamento. | Grupos sumarizados gerados pelo `GROUP BY`. | **Sim** (`HAVING COUNT(*) > 5`, `HAVING SUM(valor) >= 1000`). |

---

## Sintaxe

```sql
SELECT coluna_agrupada, FUNCAO_AGREGACAO(coluna)
FROM tabela
WHERE condicao_filtra_linhas_individuais
GROUP BY coluna_agrupada
HAVING FUNCAO_AGREGACAO(coluna) condicao_filtra_grupos;
```

---

## Exemplos Práticos

### 1. Filtrando Embalagens com Preço Máximo Superior a R$ 5,00

```sql
SELECT 
    embalagem, 
    MAX(preco_de_lista) AS preco_maximo, 
    MIN(preco_de_lista) AS preco_minimo 
FROM tabela_de_produtos
GROUP BY embalagem 
HAVING MAX(preco_de_lista) >= 5.00;
```

---

### 2. Clientes com Volume Expressivo de Compras em 2016

```sql
SELECT 
    cpf, 
    COUNT(*) AS total_notas_emitidas 
FROM notas_fiscais
WHERE data_venda BETWEEN '2016-01-01' AND '2016-12-31'
GROUP BY cpf 
HAVING COUNT(*) > 2000;
```
