# Variáveis Locais e de Sessão

No MySQL, as variáveis são utilizadas para armazenar temporariamente valores de controle, contadores, flags e resultados intermediários. Existem três tipos principais de variáveis:

---

## 1. Variáveis Locais (`DECLARE`)

- **Escopo:** Existem exclusivamente dentro do bloco `BEGIN ... END` de uma *Stored Procedure* ou *Stored Function*.
- **Ciclo de Vida:** São criadas no início da execução do bloco e destruídas ao final dele.
- **Declaração:** Devem ser obrigatoriamente declaradas no início do bloco antes de qualquer outro comando executável.

```sql
-- Sintaxe de declaração
DECLARE nome_variavel TIPO_DE_DADO [DEFAULT valor_inicial];

-- Exemplo prático dentro de um bloco BEGIN...END
DECLARE v_total_pedidos INT DEFAULT 0;
DECLARE v_cliente_nome VARCHAR(100);
DECLARE v_saldo DECIMAL(10, 2) DEFAULT 0.00;

-- Atribuindo valores
SET v_total_pedidos = 10;
SELECT nome INTO v_cliente_nome FROM clientes WHERE cliente_id = 1;
```

---

## 2. Variáveis de Usuário / Sessão (`@`)

- **Escopo:** Definidas pelo usuário com o prefixo `@`. Existem durante toda a sessão de conexão do cliente ativo.
- **Ciclo de Vida:** Permanecem na memória até que a conexão seja encerrada ou sejam sobrescritas. Não são visíveis para outras conexões.
- **Declaração:** Não requerem declaração prévia de tipo.

```sql
-- Definindo com o comando SET
SET @desconto_padrao = 0.15;
SET @usuario_ativo = 'gustavo';

-- Definindo e atribuindo diretamente em uma consulta com :=
SELECT @maior_preco := MAX(preco_de_lista) FROM tabela_de_produtos;

-- Usando a variável em consultas subsequentes
SELECT nome_do_produto, preco_de_lista 
FROM tabela_de_produtos 
WHERE preco_de_lista = @maior_preco;
```

---

## 3. Variáveis Globais e de Sistema (`@@`)

- Controlam o funcionamento e configuração do servidor MySQL (ex.: `@@autocommit`, `@@sql_mode`, `@@time_zone`).

```sql
-- Consultando variáveis globais de sistema
SELECT @@autocommit, @@version;
```
