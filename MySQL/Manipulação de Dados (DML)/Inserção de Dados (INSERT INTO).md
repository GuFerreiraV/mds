# Inserção de Dados (`INSERT INTO`)

O comando `INSERT INTO` é a instrução DML (*Data Manipulation Language*) utilizada para adicionar uma ou mais novas linhas de dados a uma tabela existente.

---

## 1. Inserção de Registro Único

Especificando as colunas e os valores correspondentes:

```sql
INSERT INTO tb_produtos (
    codigo_produto,
    nome_produto,
    embalagem,
    tamanho,
    sabor,
    preco_lista
) VALUES (
    '1078680',
    'Frescor do Verão - 470 ml - Manga',
    'Lata',
    '470 ml',
    'Manga',
    5.18
);
```

> [!tip] 💡 Boa Prática
> Sempre declare explicitamente a lista de colunas no comando `INSERT`. Isso evita erros caso novas colunas sejam adicionadas à tabela no futuro.

---

## 2. Inserção Múltipla (Bulk Insert / Em Lote)

Inserir múltiplos registros em um único comando melhora significativamente a performance em relação a múltiplos `INSERT` isolados:

```sql
INSERT INTO tb_produtos (codigo_produto, nome_produto, embalagem, preco_lista) VALUES 
('1000889', 'Sabor da Montanha - 700 ml - Uva', 'Garrafa', 6.31),
('1004327', 'Videira do Campo - 1,5 Litros - Melancia', 'PET', 19.51),
('1013793', 'Suco de Laranja da Fazenda - 350 ml', 'Lata', 2.40);
```

---

## 3. Inserção a partir de Consulta (`INSERT INTO ... SELECT`)

Permite copiar e transformar dados de uma tabela para outra de forma direta:

```sql
-- Criando uma cópia de produtos em promoção
INSERT INTO tb_produtos_promocao (codigo_produto, nome_produto, preco_promocional)
SELECT 
    codigo_produto, 
    nome_produto, 
    preco_lista * 0.80 -- Aplicando 20% de desconto
FROM tb_produtos
WHERE preco_lista > 10.00;
```
