# Consultas Recursivas (`WITH RECURSIVE`)

A cláusula **`WITH RECURSIVE`** permite criar CTEs (Common Table Expressions) que referenciam a si mesmas de forma iterativa, comportando-se de forma análoga a uma função recursiva em linguagens de programação.

---

## Estrutura de uma CTE Recursiva

Uma consulta recursiva é obrigatoriamente dividida em duas partes unidas por `UNION ALL`:

1. **Caso Base (Membro Âncora / Não Recursivo):**
   > Inicializa a recursão, retornando o registro ou valor inicial de partida.
2. **Caso Recursivo (Membro Recursivo):**
   > Executa a próxima iteração referenciando a própria CTE e aplicando uma condição de parada no `WHERE`.

A recursão é executada continuamente até que a parte recursiva retorne um conjunto vazio.

---

## Sintaxe

```sql
WITH RECURSIVE nome_cte (colunas) AS (
    -- 1. Caso Base (Âncora)
    SELECT valores_iniciais
    
    UNION ALL
    
    -- 2. Caso Recursivo
    SELECT proximos_valores
    FROM nome_cte
    WHERE condicao_de_parada
)
SELECT * FROM nome_cte;
```

---

## Exemplos Práticos

### 1. Gerando uma Sequência Numérica de 1 a 10

```sql
WITH RECURSIVE sequencia AS (
    -- Caso base: inicia com o número 1
    SELECT 1 AS numero
    
    UNION ALL
    
    -- Caso recursivo: soma 1 até atingir 10
    SELECT numero + 1
    FROM sequencia
    WHERE numero < 10
)
SELECT * FROM sequencia;
```

---

### 2. Gerando Números Primos de 1 a 1000

```sql
WITH RECURSIVE sequencia(num) AS (
    SELECT 1 AS num
    UNION ALL
    SELECT num + 1
    FROM sequencia
    WHERE num < 1000
),
PrintNumPrimo AS (
    SELECT sq1.num * sq2.num AS Aux
    FROM sequencia AS sq1, sequencia AS sq2
    WHERE sq1.num <= sq2.num
      AND sq1.num * sq2.num > 1
      AND sq1.num * sq2.num <= 1000
    GROUP BY sq1.num * sq2.num
    HAVING COUNT(*) = 1
)
SELECT GROUP_CONCAT(Aux ORDER BY Aux SEPARATOR ' & ') AS numeros_primos
FROM PrintNumPrimo;
```

---

### 3. Navegação em Árvores e Organogramas Hierárquicos

```sql
-- Consultando a hierarquia de cargos / gerência
WITH RECURSIVE HierarquiaFuncionarios AS (
    -- Caso base: Presidente / Diretor Geral (sem gestor acima)
    SELECT funcionario_id, nome, cargo, gestor_id, 1 AS nivel
    FROM tb_funcionarios
    WHERE gestor_id IS NULL
    
    UNION ALL
    
    -- Caso recursivo: colaboradores subordinados ao nível anterior
    SELECT f.funcionario_id, f.nome, f.cargo, f.gestor_id, h.nivel + 1
    FROM tb_funcionarios f
    INNER JOIN HierarquiaFuncionarios h ON f.gestor_id = h.funcionario_id
)
SELECT * FROM HierarquiaFuncionarios 
ORDER BY nivel, gestor_id;
```
