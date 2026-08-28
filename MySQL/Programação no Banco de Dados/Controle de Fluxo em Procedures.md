# Controle de Fluxo e Estruturas de Repetição em Procedures

No corpo de *Stored Procedures* do MySQL, podemos utilizar estruturas condicionais (`IF`, `CASE`) e estruturas de repetição (*loops* como `WHILE`, `REPEAT`, `LOOP`) para implementar lógicas procedurais completas.

---

## 1. Estrutura Condicional `IF ... ELSEIF ... ELSE`

```sql
DELIMITER $$

CREATE PROCEDURE AvaliarDescontoCliente (
    IN  p_valor_compra DECIMAL(10, 2),
    OUT p_percentual_desconto DECIMAL(5, 2)
)
BEGIN
    IF p_valor_compra >= 5000.00 THEN
        SET p_percentual_desconto = 0.20; -- 20% de desconto
    ELSEIF p_valor_compra >= 2000.00 THEN
        SET p_percentual_desconto = 0.10; -- 10% de desconto
    ELSEIF p_valor_compra >= 500.00 THEN
        SET p_percentual_desconto = 0.05; -- 5% de desconto
    ELSE
        SET p_percentual_desconto = 0.00; -- Sem desconto
    END IF;
END$$

DELIMITER ;
```

---

## 2. Estrutura Condicional `CASE`

```sql
DELIMITER $$

CREATE PROCEDURE ObterDescricaoStatus (
    IN  p_status_codigo CHAR(1),
    OUT p_descricao VARCHAR(50)
)
BEGIN
    CASE p_status_codigo
        WHEN 'P' THEN SET p_descricao = 'Pendente de Pagamento';
        WHEN 'A' THEN SET p_descricao = 'Aprovado / Pago';
        WHEN 'C' THEN SET p_descricao = 'Cancelado';
        WHEN 'E' THEN SET p_descricao = 'Enviado para Transporte';
        ELSE SET p_descricao = 'Status Desconhecido';
    END CASE;
END$$

DELIMITER ;
```

---

## 3. Estruturas de Repetição (Loops)

### A. Loop `WHILE` (Testa no Início)
Executa o bloco enquanto a condição for verdadeira:

```sql
DELIMITER $$

CREATE PROCEDURE InserirSequenciaWhile (IN p_limite INT)
BEGIN
    DECLARE v_contador INT DEFAULT 1;
    
    WHILE v_contador <= p_limite DO
        INSERT INTO tb_numeros (numero) VALUES (v_contador);
        SET v_contador = v_contador + 1;
    END WHILE;
END$$

DELIMITER ;
```

---

### B. Loop `REPEAT` (Testa no Final)
Executa ao menos uma vez e repete até que a condição seja verdadeira (*UNTIL*):

```sql
DELIMITER $$

CREATE PROCEDURE InserirSequenciaRepeat (IN p_limite INT)
BEGIN
    DECLARE v_contador INT DEFAULT 1;
    
    REPEAT
        INSERT INTO tb_numeros (numero) VALUES (v_contador);
        SET v_contador = v_contador + 1;
    UNTIL v_contador > p_limite
    END REPEAT;
END$$

DELIMITER ;
```

---

### C. Loop Genérico com Rótulos e `LEAVE` / `ITERATE`

- **`LEAVE rotulo`:** Encerra o loop (equivalente ao `break`).
- **`ITERATE rotulo`:** Salta para a próxima iteração (equivalente ao `continue`).

```sql
DELIMITER $$

CREATE PROCEDURE ProcessarComLoopRotulado ()
BEGIN
    DECLARE v_contador INT DEFAULT 0;
    
    meu_loop: LOOP
        SET v_contador = v_contador + 1;
        
        -- Salta iterações pares
        IF MOD(v_contador, 2) = 0 THEN
            ITERATE meu_loop;
        END IF;
        
        INSERT INTO tb_impares (valor) VALUES (v_contador);
        
        -- Condição de saída
        IF v_contador >= 10 THEN
            LEAVE meu_loop;
        END IF;
    END LOOP meu_loop;
END$$

DELIMITER ;
```
