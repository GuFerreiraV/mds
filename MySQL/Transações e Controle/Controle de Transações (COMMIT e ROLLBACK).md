# Controle de Transações (`COMMIT` e `ROLLBACK`)

Uma **Transação** no MySQL é uma unidade lógica e indivisível de trabalho composta por uma ou mais operações SQL que devem ser executadas com sucesso total ou totalmente desfeitas, preservando a **integridade, consistência e confiabilidade dos dados**.

---

## As Propriedades ACID

- **Atomicidade (Atomicity):** Tudo ou nada. Se qualquer instrução falhar, todas as alterações anteriores da transação são revertidas.
- **Consistência (Consistency):** O banco passa de um estado válido para outro estado válido, respeitando todas as regras e restrições.
- **Isolamento (Isolation):** Transações simultâneas não interferem umas nas outras até que sejam confirmadas.
- **Durabilidade (Durability):** Uma vez confirmada a transação (`COMMIT`), seus dados persistem permanentemente no disco, mesmo em caso de falha de energia.

---

## Comandos Principais de Transação

1. **`START TRANSACTION` (ou `BEGIN`):** Inicia explicitamente uma nova transação e cria um ponto de estado.
2. **`COMMIT`:** Confirma e grava definitivamente todas as operações realizadas desde o início da transação.
3. **`ROLLBACK`:** Cancela e desfaz todas as alterações realizadas desde o início da transação, retornando o banco ao estado original.
4. **`SAVEPOINT nome_ponto`:** Define um ponto intermediário de salvamento na transação.
5. **`ROLLBACK TO SAVEPOINT nome_ponto`:** Desfaz apenas as alterações feitas após o savepoint indicado.

---

## Exemplos Práticos

### 1. Confirmando Alterações com Sucesso (`COMMIT`)

```sql
-- Exemplo: Aumentando a comissão dos vendedores em 15%
START TRANSACTION;

-- Verifica os dados antes da alteração
SELECT matricula, nome, comissao FROM tabela_de_vendedores;

-- Executa a modificação
UPDATE tabela_de_vendedores 
SET comissao = comissao * 1.15;

-- Confirma a alteração no banco de dados
COMMIT;
```

![[Untitled 502.png]]
![[Untitled 503.png]]

---

### 2. Desfazendo Alterações em Caso de Erro (`ROLLBACK`)

```sql
-- Iniciando a transação de teste
START TRANSACTION;

-- Executa alteração indevida ou em teste
UPDATE tabela_de_vendedores 
SET comissao = comissao * 1.15;

-- Cancela a modificação e restaura os valores originais
ROLLBACK;
```

![[Untitled 504.png]]

---

### 3. Utilizando Pontos de Salvamento (`SAVEPOINT`)

```sql
START TRANSACTION;

INSERT INTO clientes (nome, email) VALUES ('Carlos Souza', 'carlos@empresa.com');
SAVEPOINT sp_primeiro_cliente;

INSERT INTO clientes (nome, email) VALUES ('Ana Lima', 'ana@empresa.com');
-- Ocorreu um problema com o registro da Ana:
ROLLBACK TO SAVEPOINT sp_primeiro_cliente;

-- O Carlos é mantido e confirmado:
COMMIT;
```

---

## Controle de Autocommit no MySQL

Por padrão, a variável do sistema `autocommit` vem habilitada (`1`), o que faz com que todo comando isolado seja comitado automaticamente. Ao executar `START TRANSACTION`, o autocommit é temporariamente suspenso até o `COMMIT` ou `ROLLBACK`.

```sql
-- Consultar estado do autocommit
SELECT @@autocommit;

-- Desativar o autocommit para a sessão
SET autocommit = 0;
```
