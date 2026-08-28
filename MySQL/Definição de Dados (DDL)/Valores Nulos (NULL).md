# Valores Nulos (`NULL`)

No MySQL e no modelo relacional, um valor **`NULL`** representa a **ausência de valor**, dado desconhecido ou não aplicável.

> [!tip] 💡 Atenção
> `NULL` é totalmente diferente de zero (`0`) ou de uma sequência vazia (`""` ou espaço em branco). 
> `NULL` significa que nenhum valor foi atribuído ao campo.

---

## Características de Campos `NULL`

1. Se uma coluna não for marcada com `NOT NULL`, ela aceita valores `NULL` por padrão.
2. Qualquer operação aritmética envolvendo `NULL` resulta em `NULL` (ex.: `10 + NULL = NULL`).
3. Comparações tradicionais (`= NULL` ou `<> NULL`) **não funcionam**. Para testar nulidade, utiliza-se **`IS NULL`** ou **`IS NOT NULL`**.

---

## Exemplo Prático

```sql
-- Criando banco e tabela de alunos
CREATE DATABASE IF NOT EXISTS escola;
USE escola;

CREATE TABLE tbl_aluno (
    aluno_id INT NOT NULL AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NULL,
    telefone VARCHAR(20) NULL,
    PRIMARY KEY (aluno_id)
);

-- Inserindo registro com campos opcionais nulos
INSERT INTO tbl_aluno (nome, email, telefone) 
VALUES ('Mariana Silva', NULL, '11999998888');

-- Buscando alunos que NÃO possuem e-mail cadastrado
SELECT * 
FROM tbl_aluno 
WHERE email IS NULL;

-- Buscando alunos que possuem e-mail cadastrado
SELECT * 
FROM tbl_aluno 
WHERE email IS NOT NULL;
```

---

## Funções Úteis para Tratar `NULL`

- **`IFNULL(campo, valor_alternativo)`:** Substitui `NULL` por um valor padrão.
  ```sql
  SELECT nome, IFNULL(email, 'Não informado') AS email_contato 
  FROM tbl_aluno;
  ```
- **`COALESCE(valor1, valor2, ...)`:** Retorna o primeiro valor não nulo da lista.
  ```sql
  SELECT nome, COALESCE(telefone, email, 'Sem contato') AS contato_principal 
  FROM tbl_aluno;
  ```