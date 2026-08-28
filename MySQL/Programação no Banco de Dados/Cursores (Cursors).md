# Cursores (`Cursors`)

Um **Cursor** no MySQL é um mecanismo procedural que permite navegar e processar um conjunto de resultados de uma consulta linha por linha (*row-by-row*), em uma ordem sequencial determinada.

---

## Ciclo de Vida de um Cursor

O trabalho com cursores segue obrigatoriamente 4 etapas sequenciais:

```
  ┌─────────────┐     ┌───────────┐     ┌───────────┐     ┌────────────┐
  │ 1. DECLARE  │ ──► │  2. OPEN  │ ──► │ 3. FETCH  │ ──► │  4. CLOSE  │
  │   Cursor    │     │  Cursor   │     │ (no loop) │     │   Cursor   │
  └─────────────┘     └───────────┘     └───────────┘     └────────────┘
```

1. **`DECLARE cursor_name CURSOR FOR ...`:** Declara o cursor e associa à consulta `SELECT`.
2. **`OPEN cursor_name`:** Executa a consulta e aloca a memória necessária.
3. **`FETCH cursor_name INTO var1, var2, ...`:** Lê a linha atual e avança o ponteiro para a próxima linha.
4. **`CLOSE cursor_name`:** Libera a memória ocupada pelo cursor.

---

## Tratamento de Término com `HANDLER FOR NOT FOUND`

Para saber quando o cursor chegou ao final do conjunto de dados e evitar erros, declaramos um *Handler* especial que altera o valor de uma variável de controle para `1` quando não houver mais linhas:

```sql
DECLARE fim_cursor INT DEFAULT 0;
DECLARE CONTINUE HANDLER FOR NOT FOUND SET fim_cursor = 1;
```

---

## Exemplo Prático Completo

O exemplo abaixo demonstra uma procedure que itera sobre os nomes de uma tabela temporária de usuários, formatando e processando cada registro individualmente:

```sql
DELIMITER $$

CREATE PROCEDURE ProcessarListaUsuarios ()
BEGIN
    -- 1. Variáveis locais de controle e armazenamento
    DECLARE v_fim_cursor INT DEFAULT 0;
    DECLARE v_nome_atual VARCHAR(255);
    DECLARE v_total_processados INT DEFAULT 0;
    
    -- 2. Declaração do Cursor
    DECLARE cursor_usuarios CURSOR FOR 
        SELECT nome FROM temp_nomes;
    
    -- 3. Declaração do Handler de Término
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET v_fim_cursor = 1;
    
    -- 4. Abertura do Cursor
    OPEN cursor_usuarios;
    
    -- Primeira leitura
    FETCH cursor_usuarios INTO v_nome_atual;
    
    -- Loop de iteração linha a linha
    WHILE v_fim_cursor = 0 DO
        -- Processamento individual de cada linha
        SET v_total_processados = v_total_processados + 1;
        
        -- Exibe ou processa o nome atual
        SELECT CONCAT('Processando usuário #', v_total_processados, ': ', UPPER(v_nome_atual)) AS log_processamento;
        
        -- Avança para a próxima linha
        FETCH cursor_usuarios INTO v_nome_atual;
    END WHILE;
    
    -- 5. Fechamento e liberação de recursos
    CLOSE cursor_usuarios;
    
    SELECT CONCAT('Total de usuários processados: ', v_total_processados) AS resultado_final;
END$$

DELIMITER ;
```

---

## Quando Usar Cursores?

> [!tip] 💡 Performance: Conjuntos vs. Linhas
> Bancos de dados relacionais são otimizados para operações baseadas em **conjuntos** (`INSERT INTO ... SELECT`, `UPDATE ... WHERE`).
> Cursores devem ser utilizados apenas quando a lógica procedural exigir chamadas de APIs externas, disparos condicionais complexos para cada linha ou rotinas que não possam ser resolvidas diretamente com uma instrução SQL relacional padrão.
