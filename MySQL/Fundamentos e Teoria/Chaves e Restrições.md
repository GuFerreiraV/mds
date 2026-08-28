# Chaves e Restrições (Constraints)

As **chaves primárias** e **chaves estrangeiras** são os pilares fundamentais do modelo relacional, responsáveis por manter a **integridade dos dados**, unicidade dos registros e as relações lógicas entre tabelas.

---

## 1. Chave Primária (Primary Key)

Uma **Chave Primária (`PRIMARY KEY`)** é um identificador exclusivo para cada registro de uma tabela.
- Não pode conter valores nulos (`NOT NULL`).
- Garante que cada linha seja única.
- Uma tabela pode ter apenas uma chave primária (que pode ser composta por uma ou mais colunas).

![[Untitled 483.png]]

---

## 2. Chave Estrangeira (Foreign Key)

> [!tip] 💡 Conceito
> Uma **Chave Estrangeira (`FOREIGN KEY`)** é uma coluna ou conjunto de colunas que aponta para a chave primária de outra tabela, garantindo **integridade referencial**.

Isso impede que uma tabela filha aponte para um registro inexistente na tabela pai.

### Ações de Integridade Referencial (`ON DELETE` / `ON UPDATE`)

| Ação | Comportamento |
| :--- | :--- |
| **`CASCADE`** | Se o registro pai for excluído/atualizado, todos os registros filhos correspondentes são automaticamente excluídos/atualizados. |
| **`RESTRICT` / `NO ACTION`** | Impede a exclusão/atualização do registro pai se existirem registros filhos dependentes. |
| **`SET NULL`** | Define a coluna estrangeira na tabela filha como `NULL` se o registro pai for excluído/atualizado. |

---

## Exemplos Práticos de Código

### 1. Criando Chave Primária e Estrangeira no `CREATE TABLE`

```sql
-- Tabela Pai (Clientes)
CREATE TABLE clientes (
    cliente_id INT NOT NULL AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) NOT NULL UNIQUE,
    PRIMARY KEY (cliente_id)
);

-- Tabela Filha (Pedidos)
CREATE TABLE pedidos (
    pedido_id INT NOT NULL AUTO_INCREMENT,
    numero_pedido VARCHAR(50) NOT NULL,
    data_emissao DATE NOT NULL,
    cliente_id INT NOT NULL,
    valor_total DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (pedido_id),
    CONSTRAINT fk_pedidos_cliente 
        FOREIGN KEY (cliente_id) 
        REFERENCES clientes(cliente_id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);
```

---

### 2. Adicionando Chaves com `ALTER TABLE`

![[Untitled 484.png]]

```sql
-- Adicionando Chave Primária a uma tabela existente
ALTER TABLE produtos 
ADD PRIMARY KEY (codigo_produto);

-- Adicionando Chave Estrangeira a uma tabela existente
ALTER TABLE itens_pedido
ADD CONSTRAINT fk_itens_pedido_produto
FOREIGN KEY (codigo_produto) 
REFERENCES produtos(codigo_produto)
ON DELETE CASCADE
ON UPDATE CASCADE;
```

---

### 3. Removendo Chaves e Restrições

```sql
-- Removendo uma chave estrangeira pelo nome da restrição
ALTER TABLE itens_pedido 
DROP FOREIGN KEY fk_itens_pedido_produto;

-- Removendo uma chave primária
ALTER TABLE produtos 
DROP PRIMARY KEY;
```