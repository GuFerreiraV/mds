# Alteração de Tabelas (`ALTER TABLE`)

O comando `ALTER TABLE` é uma instrução DDL usada para modificar a estrutura de uma tabela já existente no banco de dados, sem a necessidade de recriá-la.

Com ele é possível:
- Adicionar, excluir e modificar colunas;
- Renomear colunas e tabelas;
- Adicionar ou remover restrições (*constraints*), como chaves primárias, estrangeiras e regras de unicidade.

---

## 1. Adicionando Colunas

```sql
-- Adicionar uma coluna simples
ALTER TABLE clientes
ADD COLUMN data_nascimento DATE;

-- Adicionar múltiplas colunas de uma só vez
ALTER TABLE clientes
ADD (
    telefone VARCHAR(20),
    limite_credito DECIMAL(10, 2) DEFAULT 0.00,
    status_cadastro VARCHAR(20) DEFAULT 'Ativo'
);
```

---

## 2. Excluindo Colunas

```sql
-- Excluir uma coluna
ALTER TABLE clientes
DROP COLUMN telefone;

-- Excluir múltiplas colunas
ALTER TABLE clientes
DROP COLUMN limite_credito,
DROP COLUMN status_cadastro;
```

---

## 3. Modificando Tipos de Dados e Definições de Colunas

- **`MODIFY COLUMN`:** Altera o tipo de dado ou atributos (como `NULL` / `NOT NULL`) de uma coluna existente.
- **`CHANGE COLUMN`:** Permite renomear a coluna e mudar seu tipo de dado simultaneamente.

```sql
-- Modificando o tipo da coluna
ALTER TABLE clientes
MODIFY COLUMN nome VARCHAR(150) NOT NULL;

-- Renomeando a coluna e alterando o tipo
ALTER TABLE clientes
CHANGE COLUMN data_nascimento dt_nascimento DATE NOT NULL;
```

---

## 4. Renomeando Colunas e Tabelas (MySQL 8.0+)

```sql
-- Renomear apenas a coluna
ALTER TABLE clientes
RENAME COLUMN dt_nascimento TO data_nascimento;

-- Renomear a tabela completa
ALTER TABLE clientes
RENAME TO tb_clientes;
```

---

## 5. Gerenciando Restrições (*Constraints*)

```sql
-- Adicionar uma Chave Primária
ALTER TABLE tb_clientes
ADD CONSTRAINT pk_cliente PRIMARY KEY (cliente_id);

-- Adicionar uma Restrição de Unicidade
ALTER TABLE tb_clientes
ADD CONSTRAINT uq_cliente_email UNIQUE (email);

-- Remover uma Restrição
ALTER TABLE tb_clientes
DROP INDEX uq_cliente_email;
```
