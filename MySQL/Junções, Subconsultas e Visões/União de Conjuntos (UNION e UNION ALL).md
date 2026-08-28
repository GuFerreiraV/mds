# União de Conjuntos (`UNION` e `UNION ALL`)

Os operadores `UNION` e `UNION ALL` combinam verticalmente os conjuntos de resultados retornados por duas ou mais consultas `SELECT` em uma única tabela de saída.

---

## Requisitos Obrigatórios para Uso

> [!tip] 💡 Regras Estruturais
> 1. Todas as instruções `SELECT` devem possuir a **mesma quantidade de colunas**.
> 2. As colunas correspondentes devem possuir **tipos de dados compatíveis**.
> 3. Os nomes das colunas de saída serão herdados do **primeiro `SELECT`**.

---

## Diferença entre `UNION` e `UNION ALL`

| Operador | Tratamento de Duplicatas | Desempenho |
| :--- | :--- | :--- |
| **`UNION`** | Remove automaticamente linhas idênticas (executa um `DISTINCT` implícito). | Mais lento, devido à ordenação e remoção de duplicatas. |
| **`UNION ALL`** | Mantém todas as linhas, inclusive repetições. | Mais rápido, pois apenas concatena os resultados. |

---

## Exemplos Práticos

### 1. `UNION` (Sem Duplicatas)

```sql
-- Retorna bairros únicos onde residem clientes ou atuam vendedores
SELECT bairro FROM tabela_de_clientes
UNION 
SELECT bairro FROM tabela_de_vendedores;
```

---

### 2. `UNION ALL` (Com Todas as Ocorrências)

```sql
-- Retorna todos os lançamentos consolidados de receitas e despesas
SELECT 
    data_movimento, 
    descricao, 
    valor, 
    'Receita' AS tipo_operacao 
FROM tb_contas_a_receber

UNION ALL

SELECT 
    data_movimento, 
    descricao, 
    valor * -1, 
    'Despesa' AS tipo_operacao 
FROM tb_contas_a_pagar
ORDER BY data_movimento DESC;
```
