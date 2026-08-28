# Expressões Regulares (`REGEXP` / `RLIKE`)

As **Expressões Regulares (REGEX)** fornecem um mecanismo poderoso e flexível para correspondência avançada de padrões e validação de textos em consultas SQL.

No MySQL, podemos utilizar os operadores `REGEXP` (ou seu sinônimo `RLIKE`) e funções nativas introduzidas no MySQL 8.0+.

---

## Metacaracteres Mais Utilizados

| Metacaractere | Descrição |
| :--- | :--- |
| **`^`** | Início da string (ex.: `^A` busca quem começa com 'A'). |
| **`$`** | Fim da string (ex.: `a$` busca quem termina com 'a'). |
| **`.`** | Qualquer caractere individual. |
| **`[...]`** | Qualquer caractere contido dentro dos colchetes (ex.: `[aeiou]`). |
| **`[^...]`** | Qualquer caractere **não** contido nos colchetes. |
| **`[a-z]` / `[0-9]`** | Intervalos de caracteres ou números. |
| **`p1|p2`** | Alternância lógica (OU entre padrões). |
| **`*`** | Zero ou mais repetições do elemento anterior. |
| **`+`** | Uma ou mais repetições. |
| **`?`** | Zero ou uma ocorrência (opcional). |

---

## Exemplos Práticos

### 1. Cidades que Começam com Vogais

```sql
SELECT DISTINCT cidade 
FROM tb_estacoes
WHERE cidade REGEXP '^[AEIOUaeiou]'
ORDER BY cidade ASC;
```

---

### 2. Cidades que Terminam com Vogais

```sql
SELECT DISTINCT cidade 
FROM tb_estacoes
WHERE cidade REGEXP '[AEIOUaeiou]$'
ORDER BY cidade ASC;
```

---

### 3. Cidades que Começam E Terminam com Vogais

```sql
SELECT DISTINCT cidade 
FROM tb_estacoes
WHERE cidade REGEXP '^[AEIOUaeiou].*[AEIOUaeiou]$'
ORDER BY cidade ASC;
```

---

### 4. Negação: Cidades que NÃO Começam ou NÃO Terminam com Vogais

```sql
-- Não começam com vogais
SELECT DISTINCT cidade 
FROM tb_estacoes
WHERE cidade NOT REGEXP '^[AEIOUaeiou]'
ORDER BY cidade ASC;

-- Não começam OU não terminam com vogais
SELECT DISTINCT cidade 
FROM tb_estacoes
WHERE cidade NOT REGEXP '^[AEIOUaeiou]'
   OR cidade NOT REGEXP '[AEIOUaeiou]$'
ORDER BY cidade ASC;
```

---

## 5. Funções Avançadas do MySQL 8.0+

- **`REGEXP_LIKE(expr, pat)`:** Testa se a string satisfaz o padrão regex.
- **`REGEXP_INSTR(expr, pat)`:** Retorna a posição do padrão encontrado.
- **`REGEXP_SUBSTR(expr, pat)`:** Extrai o trecho do texto correspondente ao padrão.
- **`REGEXP_REPLACE(expr, pat, repl)`:** Substitui ocorrências do padrão.

### Exemplo: Extração e Soma de Horas Válidas

```sql
SELECT 
    servico AS categoria,
    COUNT(*) AS total_chamados,
    SUM(CASE 
            WHEN REGEXP_LIKE(horas_texto, '^[0-9]+(\.[0-9]+)?$') THEN CAST(horas_texto AS DECIMAL(10, 2)) 
            ELSE 0 
        END) AS total_horas_validas
FROM tb_chamados_jira
GROUP BY servico;
```
