# Tabelas Temporárias (`CREATE TEMPORARY TABLE`)

Uma **Tabela Temporária** é uma tabela especial no MySQL que existe exclusivamente durante a **sessão de conexão atual** do cliente ou durante a execução de uma rotina de processamento.

---

## Características Principais

1. **Escopo Isolado:** Cada cliente/conexão só enxerga as suas próprias tabelas temporárias. Dois clientes distintos podem criar uma tabela temporária com o mesmo nome sem conflito.
2. **Destruição Automática:** Quando a conexão com o banco de dados é encerrada, o MySQL descarta e desaloca automaticamente todas as tabelas temporárias criadas nessa sessão.
3. **Alto Desempenho:** Ideais para armazenar resultados intermediários de cálculos complexos, relatórios e processamento em lote em *Stored Procedures*.

---

## Sintaxe e Criação

```sql
CREATE TEMPORARY TABLE [IF NOT EXISTS] nome_tabela_temp (
    coluna1 tipo_de_dado,
    coluna2 tipo_de_dado
);
```

---

## Exemplo Prático com *Stored Procedure*

```sql
-- Remove a tabela temporária caso já exista na sessão
DROP TEMPORARY TABLE IF EXISTS temp_nomes;

-- Cria a tabela temporária de apoio
CREATE TEMPORARY TABLE temp_nomes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL
);

-- Inserindo dados temporários
INSERT INTO temp_nomes (nome) VALUES 
('Anna Luiza'),
('Gustavo Ferreira'),
('Thiago Esteves');

-- Consultando os dados da tabela temporária
SELECT * FROM temp_nomes;

-- Excluindo explicitamente antes do fim da sessão (opcional)
DROP TEMPORARY TABLE temp_nomes;
```