# Introdução ao MySQL

Um **Banco de Dados** é um repositório organizado que armazena dados digitais de forma estruturada, permitindo que sejam consultados, inseridos, atualizados e excluídos com eficiência e segurança.

Fisicamente, as informações ocupam espaço no disco rígido do servidor, sendo gerenciadas por um **SGBD** (Sistema de Gerenciamento de Banco de Dados), como o **MySQL**.

---

## Principais Entidades e Estruturas

Dentro de um banco de dados relacional, encontramos diversas entidades:

1. **Esquema (Schema / Database):**
   > Conjunto de tabelas, visões e objetos agrupados sob um determinado domínio de negócio (ex.: *Vendas*, *Estoque*, *RH*).

2. **Coleção de Tabelas (Tables):**
   > Estrutura bidimensional composta por linhas (registros/tuplas) e colunas (campos/atributos), similar a uma planilha estruturada.
   ![[Untitled 481.png]]

3. **Visões (Views):**
   > Tabelas virtuais baseadas no resultado de uma consulta (`SELECT`). Elas simplificam consultas complexas e adicionam uma camada de segurança sobre os dados reais.

4. **Gatilhos (Triggers):**
   > Procedimentos automáticos disparados antes ou depois de eventos de modificação de dados (`INSERT`, `UPDATE`, `DELETE`). Úteis para auditoria, validação e sincronização.

5. **Procedimentos e Funções (Stored Procedures e Functions):**
   > Blocos de código SQL compilados e armazenados no banco para executar lógicas de negócio e rotinas automatizadas.

---

## Tipos de Dados Básicos no MySQL

![[Untitled 482.png]]

| Categoria | Tipos Comuns | Descrição |
| :--- | :--- | :--- |
| **Numéricos Inteiros** | `TINYINT`, `SMALLINT`, `INT`, `BIGINT` | Armazenam números inteiros de diferentes faixas de valores. |
| **Numéricos Decimais** | `DECIMAL(M, D)`, `FLOAT`, `DOUBLE` | `DECIMAL` é ideal para valores monetários com precisão exata. |
| **Texto / Strings** | `VARCHAR(N)`, `CHAR(N)`, `TEXT` | `VARCHAR` possui tamanho variável, enquanto `CHAR` tem tamanho fixo. |
| **Data e Hora** | `DATE`, `TIME`, `DATETIME`, `TIMESTAMP` | Armazenam datas no padrão `'AAAA-MM-DD'` e horários. |
| **Booleanos** | `BOOLEAN` ou `TINYINT(1)` | Valores lógicos (`TRUE` = 1 / `FALSE` = 0). |

---

## Criação de Bancos de Dados / Schemas

No MySQL, as palavras `DATABASE` e `SCHEMA` são sinônimos.

```sql
-- Cria o banco de dados caso ele ainda não exista
CREATE DATABASE IF NOT EXISTS empresa_db
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;

-- Seleciona o banco de dados ativo para as próximas operações
USE empresa_db;
```