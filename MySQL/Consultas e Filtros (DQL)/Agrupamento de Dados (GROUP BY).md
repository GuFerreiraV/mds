# Agrupamento de Dados (`GROUP BY`)

A cláusula `GROUP BY` agrupa linhas que possuem valores idênticos em colunas especificadas, consolidando os dados em linhas de resumo.

Geralmente é utilizada em conjunto com as **funções de agregação**:
- **`COUNT(*)` / `COUNT(coluna)`:** Conta a quantidade de registros.
- **`SUM(coluna)`:** Calcula a soma total dos valores numéricos.
- **`AVG(coluna)`:** Calcula a média aritmética dos valores.
- **`MIN(coluna)`:** Identifica o menor valor do grupo.
- **`MAX(coluna)`:** Identifica o maior valor do grupo.

---

## Sintaxe

```sql
SELECT coluna_agrupamento, FUNCAO_AGREGACAO(coluna_calculada)
FROM nome_da_tabela
[WHERE condicao_filtro_linhas]
GROUP BY coluna_agrupamento;
```

---

## Exemplos Práticos

### 1. Limite Máximo e Mínimo por Bairro (`MAX`, `MIN`)

```sql
SELECT 
    bairro, 
    MAX(limite_de_credito) AS limite_maximo, 
    MIN(limite_de_credito) AS limite_minimo 
FROM tabela_de_clientes 
GROUP BY bairro;
```

---

### 2. Quantidade de Clientes por Bairro (`COUNT`)

```sql
SELECT 
    bairro, 
    COUNT(*) AS total_clientes 
FROM tabela_de_clientes 
GROUP BY bairro;
```

---

### 3. Faturamento Total por Embalagem (`SUM`)

```sql
SELECT 
    embalagem, 
    SUM(preco_de_lista) AS soma_precos 
FROM tabela_de_produtos
WHERE sabor NOT IN ('Açaí', 'Laranja', 'Maracujá')
GROUP BY embalagem;
```

---

### 4. Média de Preço por Tipo de Embalagem (`AVG`)

```sql
SELECT 
    embalagem, 
    ROUND(AVG(preco_de_lista), 2) AS media_preco 
FROM tabela_de_produtos
GROUP BY embalagem;
```
