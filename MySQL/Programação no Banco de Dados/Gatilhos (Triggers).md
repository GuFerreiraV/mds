# Gatilhos (`Triggers`)

Um **Gatilho (Trigger)** é um objeto de banco de dados associado a uma tabela específica que é disparado e executado automaticamente quando ocorre um determinado evento de modificação de dados (**`INSERT`**, **`UPDATE`** ou **`DELETE`**).

---

## Principais Casos de Uso

- **Auditoria e Logs:** Registrar histórico de alterações (quem alterou, quando e qual era o valor antigo).
- **Consistência e Validação:** Impedir inserções inválidas disparando erros intencionais (`SIGNAL SQLSTATE`).
- **Sincronização e Resumos:** Atualizar tabelas de resumo e saldos consolidados automaticamente em tempo real.

---

## Momentos de Disparo e Qualificadores `NEW` e `OLD`

### Momentos de Execução:
- **`BEFORE`:** Executado **antes** da operação ser gravada no disco. Ideal para validação ou alteração prévia dos valores antes de salvar.
- **`AFTER`:** Executado **depois** que a operação foi concluída com sucesso. Ideal para logs, tabelas de resumo e sincronização.

### Acesso aos Registros:

| Evento | `OLD` (Valor Antigo) | `NEW` (Novo Valor) |
| :--- | :--- | :--- |
| **`INSERT`** | Indisponível | Contém os dados que estão sendo inseridos. |
| **`UPDATE`** | Contém os dados originais antes da alteração. | Contém os novos dados modificados. |
| **`DELETE`** | Contém os dados da linha que está sendo removida. | Indisponível |

---

## Sintaxe

```sql
DELIMITER $$

CREATE TRIGGER nome_do_trigger
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON nome_da_tabela
FOR EACH ROW
BEGIN
    -- Instruções SQL a serem executadas
END$$

DELIMITER ;
```

---

## Exemplos Práticos

### 1. Alimentando Automaticamente uma Tabela de Resumo Financeiro (`AFTER INSERT`)

```sql
-- 1. Tabela de resumo
CREATE TABLE resumo_aluguel (
    aluguel_id VARCHAR(50) NOT NULL,
    cliente_id VARCHAR(50) NOT NULL,
    valor_total DECIMAL(10, 2) NOT NULL,
    desconto_aplicado DECIMAL(10, 2) NOT NULL,
    valor_final DECIMAL(10, 2) NOT NULL,
    data_registro DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (aluguel_id, cliente_id)
);

-- 2. Criação do Trigger
DELIMITER $$

CREATE TRIGGER trg_apos_inserir_aluguel
AFTER INSERT ON alugueis
FOR EACH ROW
BEGIN 
    DECLARE v_desconto DECIMAL(10, 2) DEFAULT 0.00;
    DECLARE v_valor_final DECIMAL(10, 2);

    -- Regra: 10% de desconto para compras acima de R$ 2.000,00
    IF NEW.preco_total >= 2000.00 THEN
        SET v_desconto = NEW.preco_total * 0.10;
    END IF;

    SET v_valor_final = NEW.preco_total - v_desconto;

    -- Alimenta a tabela de resumo com o novo registro
    INSERT INTO resumo_aluguel (
        aluguel_id, 
        cliente_id, 
        valor_total, 
        desconto_aplicado, 
        valor_final
    ) VALUES (
        NEW.aluguel_id, 
        NEW.cliente_id, 
        NEW.preco_total, 
        v_desconto, 
        v_valor_final
    );
END$$

DELIMITER ;
```

---

### 2. Auditoria de Alteração de Preços (`BEFORE UPDATE`)

```sql
-- Tabela de auditoria
CREATE TABLE auditoria_precos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    codigo_produto VARCHAR(50),
    preco_antigo DECIMAL(10, 2),
    preco_novo DECIMAL(10, 2),
    data_modificacao DATETIME DEFAULT CURRENT_TIMESTAMP,
    usuario VARCHAR(100)
);

DELIMITER $$

CREATE TRIGGER trg_auditoria_preco_produto
BEFORE UPDATE ON tb_produtos
FOR EACH ROW
BEGIN
    -- Dispara apenas se o preço de fato mudou
    IF OLD.preco_lista <> NEW.preco_lista THEN
        INSERT INTO auditoria_precos (codigo_produto, preco_antigo, preco_novo, usuario)
        VALUES (OLD.codigo_produto, OLD.preco_lista, NEW.preco_lista, CURRENT_USER());
    END IF;
END$$

DELIMITER ;
```

---

## Gerenciamento de Triggers

```sql
-- Listar todos os triggers do banco de dados
SHOW TRIGGERS;

-- Remover um trigger
DROP TRIGGER IF EXISTS trg_apos_inserir_aluguel;
```
