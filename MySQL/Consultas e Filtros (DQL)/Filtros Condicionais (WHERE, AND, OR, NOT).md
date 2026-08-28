# Filtros Condicionais (`WHERE`, `AND`, `OR`, `NOT`)

A cláusula `WHERE` é utilizada para filtrar e restringir registros, retornando apenas as linhas que atendem a um critério lógico especificado.

> [!note] 📌 Aplicação Geral
> O `WHERE` não é exclusivo do `SELECT`. Ele também é crucial em comandos de modificação de dados como `UPDATE` e `DELETE`.

---

## 1. Operadores de Comparação Básicos

```sql
-- Igualdade (=)
SELECT * FROM tb_clientes WHERE data_nascimento = '1995-01-13';

-- Diferente (<> ou !=)
SELECT * FROM tb_clientes WHERE estado <> 'SP';

-- Maior (>), Menor (<), Maior/Menor ou Igual (>=, <=)
SELECT * FROM tb_clientes WHERE idade >= 18;
```

---

## 2. Operador Lógico `AND`

Retorna o registro somente quando **todas** as condições associadas forem verdadeiras:

```sql
SELECT * 
FROM clientes 
WHERE pais = 'Brasil' 
  AND cidade = 'São Paulo' 
  AND limite_credito > 1000.00;
```

---

## 3. Operador Lógico `OR`

Retorna o registro quando **ao menos uma** das condições for verdadeira:

```sql
SELECT * 
FROM clientes 
WHERE estado = 'SP' OR estado = 'RJ';
```

---

## 4. Operador Lógico `NOT`

Inverte o resultado lógico da condição seguinte:

```sql
-- Todos os clientes, exceto os da Espanha
SELECT * FROM clientes WHERE NOT pais = 'Espanha';
```

---

## 5. Operadores Especiais de Filtragem

### `BETWEEN` (Intervalo de Valores)
```sql
-- Clientes com idade entre 18 e 30 anos (inclusivo)
SELECT * FROM clientes WHERE idade BETWEEN 18 AND 30;

-- Negação do intervalo
SELECT * FROM clientes WHERE idade NOT BETWEEN 18 AND 30;
```

### `IN` (Conjunto / Lista de Valores)
```sql
-- Produtos com sabores específicos
SELECT * FROM produtos WHERE sabor IN ('Manga', 'Uva', 'Laranja');

-- Clientes que NÃO moram nas cidades especificadas
SELECT * FROM clientes WHERE cidade NOT IN ('São Paulo', 'Curitiba');
```

---

## 6. Precedência e Agrupamento com Parênteses

Assim como na matemática, o operador `AND` possui precedência sobre o `OR`. Para garantir a lógica desejada, **sempre utilize parênteses**:

```sql
-- Busca clientes do RJ cujo nome começa com 'D' ou 'G'
SELECT * 
FROM clientes 
WHERE estado = 'RJ' 
  AND (nome LIKE 'D%' OR nome LIKE 'G%');
```
