# Criação de Tabelas (`CREATE TABLE`)

O comando `CREATE TABLE` é a instrução DDL (*Data Definition Language*) utilizada para estruturar e criar uma nova tabela no banco de dados ativo.

---

## Sintaxe Geral

```sql
CREATE TABLE [IF NOT EXISTS] nome_da_tabela (
    nome_coluna1 tipo_de_dado [restricoes],
    nome_coluna2 tipo_de_dado [restricoes],
    ...,
    [restricoes_de_tabela]
) [ENGINE = InnoDB] [DEFAULT CHARSET = utf8mb4];
```

---

## Restrições Mais Comuns de Coluna

- **`PRIMARY KEY`:** Identifica unicamente cada registro da tabela.
- **`AUTO_INCREMENT`:** Incrementa automaticamente o valor numérico a cada novo `INSERT`.
- **`NOT NULL`:** Impede que a coluna receba valores vazios/nulos.
- **`UNIQUE`:** Garante que não existam dois registros com o mesmo valor nessa coluna.
- **`DEFAULT valor`:** Atribui um valor padrão caso nenhum seja fornecido.
- **`CHECK (condicao)`:** Valida se o dado atende a uma regra lógica específica.

---

## Exemplo Prático Completo

```sql
-- Criando uma tabela de itens de notas fiscais
CREATE TABLE IF NOT EXISTS itens_notas_fiscais (
    item_id INT NOT NULL AUTO_INCREMENT,
    numero_nota INT NOT NULL,
    codigo_do_produto VARCHAR(50) NOT NULL,
    quantidade INT NOT NULL DEFAULT 1,
    preco_unitario DECIMAL(10, 2) NOT NULL,
    data_criacao DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (item_id),
    CONSTRAINT chk_quantidade CHECK (quantidade > 0),
    CONSTRAINT chk_preco CHECK (preco_unitario >= 0)
) ENGINE = InnoDB DEFAULT CHARSET = utf8mb4;
```