# Ordenação de Resultados (`ORDER BY`)

A cláusula `ORDER BY` é utilizada para classificar e ordenar o conjunto de registros retornado por uma consulta `SELECT`.

---

## Sentidos de Ordenação

- **`ASC` (Ascendente / Padrão):** Do menor para o maior (numérico: 0 a 9; texto: A a Z; datas: mais antigas para mais recentes).
- **`DESC` (Descendente):** Do maior para o menor (numérico: 9 a 0; texto: Z a A; datas: mais recentes para mais antigas).

---

## Exemplos Práticos

### 1. Ordenação Simples

```sql
-- Ordena produtos do menor para o maior preço
SELECT nome_do_produto, preco_de_lista 
FROM tabela_de_produtos 
ORDER BY preco_de_lista ASC;

-- Ordena produtos do mais caro para o mais barato
SELECT nome_do_produto, preco_de_lista 
FROM tabela_de_produtos 
ORDER BY preco_de_lista DESC;
```

---

### 2. Ordenação por Múltiplas Colunas

É possível combinar diferentes colunas com direções independentes de ordenação:

```sql
-- Ordena primeiro pela quantidade decrescente; havendo empate, pelo preço decrescente
SELECT codigo_do_produto, quantidade, preco 
FROM itens_notas_fiscais 
WHERE codigo_do_produto = '1101035' 
ORDER BY quantidade DESC, preco DESC;
```

---

### 3. Ordenação com Expressões e Apelidos

```sql
-- Ordena pelo total calculado da linha
SELECT 
    numero_nota,
    quantidade,
    preco,
    (quantidade * preco) AS faturamento_linha
FROM itens_notas_fiscais
ORDER BY faturamento_linha DESC;
```
