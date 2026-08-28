# Procedimentos Armazenados (Stored Procedures)

Uma **Stored Procedure (Procedimento Armazenado)** é um conjunto compilado de instruções SQL armazenado diretamente no servidor do banco de dados, capaz de receber parâmetros, executar regras de negócio complexas, loops, condicionais e retornar dados ou manipular tabelas.

---

## Vantagens das Stored Procedures

1. **Redução de Tráfego de Rede:** Em vez de enviar dezenas de instruções SQL pela rede, a aplicação envia apenas o comando de chamada (`CALL`).
2. **Centralização de Regras de Negócio:** Se a regra mudar, a atualização é feita em um único ponto no banco.
3. **Segurança:** Permite conceder aos usuários privilégio de execução (`EXECUTE`) na procedure, sem dar permissão de acesso direto às tabelas subjacentes.

---

## Regras de Nomenclatura e Delimitador

- O comando `DELIMITER $$` altera temporariamente o caractere de término de instrução (que por padrão é `;`), permitindo que a procedure contenha múltiplos comandos terminados com `;` em seu corpo interno sem interromper a compilação.
- Nomes de procedures devem ser únicos no schema e podem conter letras, números, `_` e `$`.

---

## Tipos de Parâmetros

| Tipo | Descrição |
| :--- | :--- |
| **`IN`** (Padrão) | Parâmetro de entrada: recebe um valor da aplicação/chamador. |
| **`OUT`** | Parâmetro de saída: retorna um valor calculado de volta para o chamador. |
| **`INOUT`** | Parâmetro bidirecional: entra com um valor e pode ser modificado e retornado. |

---

## Exemplos Práticos de Criação

### 1. Procedure Simples com Parâmetros de Entrada e Saída

```sql
DELIMITER $$

CREATE PROCEDURE CalcularFaturamentoCliente (
    IN  p_cliente_id INT,
    OUT p_total_gasto DECIMAL(10, 2)
)
BEGIN
    -- Atribuindo o resultado da consulta diretamente ao parâmetro OUT
    SELECT COALESCE(SUM(inf.quantidade * inf.preco), 0.00)
    INTO p_total_gasto
    FROM notas_fiscais nf
    INNER JOIN itens_notas_fiscais inf ON nf.numero = inf.numero
    WHERE nf.cliente_id = p_cliente_id;
END$$

DELIMITER ;

-- Executando a procedure e capturando a saída em uma variável de sessão:
CALL CalcularFaturamentoCliente(101, @total);
SELECT @total AS faturamento_cliente;
```

---

### 2. Atribuição com `SELECT INTO` e Tratamento de Exceções (`HANDLER`)

O MySQL permite declarar tratadores de erro (*handlers*) para interceptar violações de chave estrangeira, duplicidade ou códigos de erro específicos:

```sql
DELIMITER $$

CREATE PROCEDURE CriarReservaHospedagem (
    IN p_aluguel_id VARCHAR(50),
    IN p_cliente_nome VARCHAR(100),
    IN p_hospedagem_id VARCHAR(50),
    IN p_data_inicio DATE,
    IN p_data_final DATE,
    IN p_preco_unitario DECIMAL(10, 2)
)
BEGIN
    DECLARE v_cliente_id VARCHAR(50);
    DECLARE v_dias INT DEFAULT 0;
    DECLARE v_preco_total DECIMAL(10, 2);
    DECLARE v_mensagem VARCHAR(255);

    -- Tratamento de exceção para Erro 1452 (Violação de Chave Estrangeira)
    DECLARE EXIT HANDLER FOR 1452
    BEGIN
        SET v_mensagem = 'Erro: Chave estrangeira não encontrada.';
        SELECT v_mensagem AS status_execucao;
    END;

    -- Localizando o ID do cliente a partir do nome
    SELECT cliente_id INTO v_cliente_id 
    FROM clientes 
    WHERE nome = p_cliente_nome 
    LIMIT 1;

    -- Calculando o número de diárias e preço total
    SET v_dias = DATEDIFF(p_data_final, p_data_inicio);
    SET v_preco_total = v_dias * p_preco_unitario;

    -- Inserindo o novo registro de reserva
    INSERT INTO reservas (aluguel_id, cliente_id, hospedagem_id, data_inicio, data_final, preco_total)
    VALUES (p_aluguel_id, v_cliente_id, p_hospedagem_id, p_data_inicio, p_data_final, v_preco_total);

    SET v_mensagem = 'Reserva inserida com sucesso!';
    SELECT v_mensagem AS status_execucao;
END$$

DELIMITER ;
```

---

## Gerenciamento de Procedures

```sql
-- Excluindo uma procedure existente
DROP PROCEDURE IF EXISTS CriarReservaHospedagem;

-- Visualizando o código-fonte de uma procedure
SHOW CREATE PROCEDURE CriarReservaHospedagem;
```
