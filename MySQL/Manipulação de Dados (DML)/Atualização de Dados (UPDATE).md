# Atualização de Dados (`UPDATE`)

O comando `UPDATE` é a instrução DML utilizada para modificar os valores de colunas em registros já existentes dentro de uma tabela.

---

## Sintaxe Básica

```sql
UPDATE nome_da_tabela 
SET coluna1 = novo_valor1, 
    coluna2 = novo_valor2 
WHERE condicao_especifica;
```

---

## Exemplo Prático

```sql
-- Atualizando o tipo de embalagem e o preço de um produto específico
UPDATE tb_produtos 
SET embalagem = 'Garrafa', 
    preco_lista = 6.20 
WHERE codigo_produto = '1078680';
```

---

## Cuidados Críticos com a Cláusula `WHERE`

> [!danger] 🚨 Perigo ao Omitir o `WHERE`
> Se a cláusula `WHERE` for omitida, **todos os registros da tabela serão atualizados** com o mesmo valor!

```sql
-- NUNCA EXECUTE SEM WHERE, A MENOS QUE QUEIRA ALTERAR A TABELA INTEIRA:
-- UPDATE tb_produtos SET preco_lista = 0.00;
```

---

## Modo Seguro do MySQL (*Safe Updates*)

Por padrão, ferramentas como o MySQL Workbench vêm configuradas com o modo **Safe Updates** ativo (`SQL_SAFE_UPDATES = 1`), impedindo que comandos `UPDATE` ou `DELETE` sejam executados sem uma chave primária ou índice no `WHERE`.

Caso seja necessário atualizar múltiplos registros sem chave primária em uma sessão controlada:

```sql
-- Desabilita temporariamente para a sessão
SET SQL_SAFE_UPDATES = 0;

UPDATE tb_produtos 
SET preco_lista = preco_lista * 1.10 
WHERE sabor = 'Manga';

-- Reabilita o modo seguro
SET SQL_SAFE_UPDATES = 1;
```
