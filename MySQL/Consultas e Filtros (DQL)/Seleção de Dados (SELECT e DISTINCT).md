# Seleção de Dados (`SELECT` e `DISTINCT`)

O comando `SELECT` é a principal instrução DQL (*Data Query Language*) do SQL, utilizada para consultar, projetar e recuperar informações armazenadas nas tabelas do banco de dados.

---

## 1. Seleção Geral (`SELECT *`)

Extrai todas as colunas de uma tabela:

```sql
SELECT * FROM tb_produtos;
```

---

## 2. Seleção de Colunas Específicas

Recupera apenas os campos necessários, melhorando a performance de rede e memória:

```sql
SELECT codigo_do_produto, quantidade, preco 
FROM itens_notas_fiscais;
```

---

## 3. Apelidos de Coluna (`AS`)

Permite atribuir nomes temporários mais claros e amigáveis para as colunas no resultado:

```sql
SELECT 
    codigo_do_produto AS codigo, 
    quantidade AS qtde,
    preco AS valor_unitario
FROM itens_notas_fiscais;
```

---

## 4. Eliminação de Duplicatas com `DISTINCT`

A cláusula `DISTINCT` garante que apenas linhas com combinações de valores exclusivos sejam retornadas, omitindo repetições:

```sql
-- Retorna os bairros únicos onde existem clientes cadastrados
SELECT DISTINCT bairro 
FROM tabela_de_clientes;

-- Retorna pares exclusivos de Nome e Bairro no Rio de Janeiro
SELECT DISTINCT nome, bairro 
FROM tabela_de_clientes 
WHERE cidade = 'Rio de Janeiro';

-- Contagem de bairros distintos
SELECT COUNT(DISTINCT bairro) AS total_bairros_unicos 
FROM tabela_de_clientes;
```

---

## 5. Limitação e Paginação com `LIMIT`

A cláusula `LIMIT` restringe a quantidade de linhas retornadas pela consulta:

```sql
-- Retorna apenas os primeiros 5 registros
SELECT * FROM notas_fiscais 
LIMIT 5;

-- Paginação: pula 10 registros (offset) e retorna os próximos 5
SELECT * FROM notas_fiscais 
LIMIT 10, 5;
-- Sintaxe alternativa equivalente:
SELECT * FROM notas_fiscais 
LIMIT 5 OFFSET 10;
```
