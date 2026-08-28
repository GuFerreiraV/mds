# Busca por Padrões (`LIKE` e Caracteres Coringa)

O operador `LIKE` é utilizado em conjunto com a cláusula `WHERE` para buscar correspondências parciais e padrões específicos em colunas de texto (strings).

---

## Caracteres Coringa (*Wildcards*) no MySQL

| Coringa | Significado |
| :--- | :--- |
| **`%`** | Representa **zero, um ou múltiplos caracteres** em qualquer posição. |
| **`_`** | Representa **exatamente um único caractere** naquela posição. |

---

## Padrões Mais Utilizados

### 1. Contém o Termo em Qualquer Posição (`%termo%`)

```sql
-- Localiza clientes com a letra ou sílaba 'silva' em qualquer parte do nome
SELECT * FROM clientes 
WHERE nome LIKE '%silva%';
```

---

### 2. Começa com Determinado Prefixo (`termo%`)

```sql
-- Localiza clientes cujo nome começa com a letra 'G'
SELECT * FROM clientes 
WHERE nome LIKE 'G%';
```

---

### 3. Termina com Determinado Sufixo (`%termo`)

```sql
-- Localiza clientes cujo nome termina com a letra 'a'
SELECT * FROM clientes 
WHERE nome LIKE '%a';
```

---

### 4. Começa e Termina com Padrões Específicos (`pref%suf`)

```sql
-- Começa com 'G' e termina com 'o' (ex.: Gustavo, Geraldo)
SELECT * FROM clientes 
WHERE nome LIKE 'G%o';
```

---

### 5. Posição Exata com Sublinhado (`_`)

```sql
-- Nomes com exatamente 2 caracteres terminados em 'a' (ex.: Za)
SELECT * FROM clientes 
WHERE nome LIKE '_a';

-- Nomes cuja SEGUNDA letra seja obrigatoriamente 'a'
SELECT * FROM clientes 
WHERE nome LIKE '_a%';

-- Nomes com a terceira letra sendo 'M'
SELECT * FROM clientes 
WHERE nome LIKE '__M%';
```

---

### 6. Negação com `NOT LIKE`

```sql
-- Clientes cujo nome NÃO começa com a letra 'A'
SELECT * FROM clientes 
WHERE nome NOT LIKE 'A%';
```
