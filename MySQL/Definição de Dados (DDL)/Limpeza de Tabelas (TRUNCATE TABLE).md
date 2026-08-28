# Limpeza Rápida de Tabelas (`TRUNCATE TABLE`)

O comando `TRUNCATE TABLE` é uma operação DDL utilizada para esvaziar completamente uma tabela, removendo todos os seus registros de maneira rápida e eficiente ao desalocar suas páginas de armazenamento.

---

## Sintaxe

```sql
TRUNCATE TABLE nome_da_tabela;
```

---

## Diferença Fundamental: `TRUNCATE` vs. `DELETE`

| Critério | `TRUNCATE TABLE` | `DELETE FROM` |
| :--- | :--- | :--- |
| **Categoria SQL** | **DDL** (Definição de Dados) | **DML** (Manipulação de Dados) |
| **Velocidade** | Extremamente rápido (desaloca páginas). | Mais lento (exclui linha por linha registrando em logs). |
| **Cláusula `WHERE`** | Não suporta (sempre limpa a tabela inteira). | Suporta filtros pontuais. |
| **`AUTO_INCREMENT`** | Reinicia o contador para o valor inicial (geralmente `1`). | Mantém a sequência do último ID inserido. |
| **Gatilhos (`Triggers`)** | **Não** dispara triggers de exclusão (`BEFORE/AFTER DELETE`). | Dispara triggers para cada linha excluída. |
| **Transações** | No MySQL, causa um *implicit commit* na maioria dos cenários. | Pode ser revertido com `ROLLBACK` dentro de uma transação ativa. |

---

## Limitações e Cuidados

> [!warning] ⚠️ Restrição de Chave Estrangeira
> Se uma tabela for referenciada por uma **Chave Estrangeira (`FOREIGN KEY`)** de outra tabela ativa, o MySQL bloqueará a execução do `TRUNCATE TABLE`.
> Nesses casos, para esvaziar a tabela deve-se utilizar o comando `DELETE FROM nome_tabela` ou desabilitar temporariamente a checagem de chaves estrangeiras com:
> ```sql
> SET FOREIGN_KEY_CHECKS = 0;
> TRUNCATE TABLE nome_da_tabela;
> SET FOREIGN_KEY_CHECKS = 1;
> ```