# Exclusão de Dados (`DELETE`)

O comando `DELETE` é a instrução DML utilizada para remover uma ou mais linhas existentes em uma tabela, de acordo com as condições especificadas na cláusula `WHERE`.

---

## Sintaxe Básica

```sql
DELETE FROM nome_da_tabela 
WHERE condicao_especifica;
```

---

## Exemplos Práticos

### 1. Excluindo um Registro Único por Chave Primária

```sql
-- Exclui o produto com código '1078680'
DELETE FROM tb_produtos 
WHERE codigo_produto = '1078680';
```

### 2. Excluindo Múltiplos Registros por Condição

```sql
-- Exclui pedidos cancelados e antigos
DELETE FROM tb_pedidos 
WHERE status_pedido = 'Cancelado' 
  AND data_emissao < '2023-01-01';
```

### 3. Excluindo com Limite de Linhas (`LIMIT`)

O MySQL permite usar a cláusula `LIMIT` no comando `DELETE` para remover um número máximo controlado de registros:

```sql
-- Remove no máximo os 10 primeiros logs antigos
DELETE FROM tb_logs_acesso 
WHERE data_evento < DATE_SUB(NOW(), INTERVAL 90 DAY)
LIMIT 10;
```

---

## Cuidados Críticos

> [!danger] 🚨 Exclusão sem `WHERE`
> Se você executar `DELETE FROM nome_tabela;` sem a cláusula `WHERE`, **todas as linhas da tabela serão excluídas**!
> Se a intenção for realmente limpar a tabela por completo com melhor performance, utilize `TRUNCATE TABLE`.

---

## `DELETE` com Chaves Estrangeiras

Se a linha a ser excluída for referenciada por outra tabela via `FOREIGN KEY`:
- **`ON DELETE RESTRICT` / `NO ACTION`:** O MySQL impedirá a exclusão e retornará um erro de violação de integridade.
- **`ON DELETE CASCADE`:** As linhas filhas correspondentes serão excluídas automaticamente junto com o registro pai.
- **`ON DELETE SET NULL`:** Os campos estrangeiros nas tabelas filhas serão definidos como `NULL`.
