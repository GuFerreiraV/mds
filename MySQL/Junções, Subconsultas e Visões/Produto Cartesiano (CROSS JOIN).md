# Produto Cartesiano (`CROSS JOIN`)

O `CROSS JOIN` produz o **produto cartesiano** entre duas ou mais tabelas. Isso significa que **cada linha da primeira tabela é combinada com todas as linhas da segunda tabela**.

Se a Tabela A possuir $N$ linhas e a Tabela B possuir $M$ linhas, o resultado conterá $N \times M$ linhas.

---

## Sintaxe

```sql
SELECT colunas
FROM tabela_a
CROSS JOIN tabela_b;

-- Sintaxe alternativa equivalente (vírgula no FROM sem WHERE):
SELECT colunas
FROM tabela_a, tabela_b;
```

---

## Exemplo Prático: Gerando Combinações de Produtos e Tamanhos

```sql
-- Gerando a matriz completa de combinações entre sabores e tamanhos
CREATE TEMPORARY TABLE temp_sabores (sabor VARCHAR(50));
INSERT INTO temp_sabores VALUES ('Manga'), ('Laranja'), ('Maracujá');

CREATE TEMPORARY TABLE temp_tamanhos (tamanho VARCHAR(50));
INSERT INTO temp_tamanhos VALUES ('Lata 350ml'), ('Garrafa 500ml'), ('PET 2L');

-- Produto cartesiano (3 sabores x 3 tamanhos = 9 combinações)
SELECT 
    s.sabor, 
    t.tamanho,
    CONCAT(s.sabor, ' - ', t.tamanho) AS descricao_produto
FROM temp_sabores AS s
CROSS JOIN temp_tamanhos AS t;
```

---

## Cuidados com Performance

> [!warning] ⚠️ Atenção ao Volume de Dados
> Em tabelas grandes, o produto cartesiano cresce exponencialmente (ex.: 10.000 linhas $\times$ 10.000 linhas = 100.000.000 de registros), podendo travar o servidor se executado sem filtro ou limite.
