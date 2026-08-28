# Junção Completa (`FULL JOIN`)

O `FULL JOIN` (ou `FULL OUTER JOIN`) retorna **todos os registros de ambas as tabelas**, preenchendo com `NULL` nos lados onde não houver correspondência mútua.

<!-- Column 1 -->
![[Untitled 496.png]]

<!-- Column 2 -->
![[Untitled 497.png]]

![[Untitled 498.png]]

---

## O `FULL JOIN` no MySQL

> [!warning] ⚠️ Suporte no MySQL
> O MySQL **não possui** a sintaxe nativa direta `FULL OUTER JOIN`.
> A execução direta de `SELECT ... FROM tabA FULL JOIN tabB` resultará em erro de sintaxe.

---

## Como Emular o `FULL JOIN` no MySQL

Para obter o comportamento exato de um Full Outer Join no MySQL, combinamos um **`LEFT JOIN`** e um **`RIGHT JOIN`** utilizando a instrução **`UNION`** (que já remove automaticamente linhas duplicadas):

![[Untitled 499.png]]

```sql
-- Parte 1: Todos os vendedores e clientes com mesmo bairro (LEFT JOIN)
SELECT 
    v.bairro AS bairro_vendedor, 
    v.nome AS nome_vendedor, 
    v.de_ferias,
    c.bairro AS bairro_cliente, 
    c.nome AS nome_cliente 
FROM tabela_de_vendedores AS v
LEFT JOIN tabela_de_clientes AS c 
  ON v.bairro = c.bairro

UNION

-- Parte 2: Todos os clientes e vendedores com mesmo bairro (RIGHT JOIN)
SELECT 
    v.bairro AS bairro_vendedor, 
    v.nome AS nome_vendedor, 
    v.de_ferias,
    c.bairro AS bairro_cliente, 
    c.nome AS nome_cliente 
FROM tabela_de_vendedores AS v
RIGHT JOIN tabela_de_clientes AS c 
  ON v.bairro = c.bairro;
```
