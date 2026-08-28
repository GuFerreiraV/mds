# Junção à Direita (`RIGHT JOIN`)

O `RIGHT JOIN` (ou `RIGHT OUTER JOIN`) retorna **todos os registros da tabela à direita** (segunda tabela declarada no `FROM`), juntamente com os registros correspondentes da tabela à esquerda.

> [!note] 📌 Registros Não Correspondentes
> Quando não houver linha correspondente na tabela da esquerda, as colunas dessa tabela virão preenchidas como **`NULL`**.

<!-- Column 1 -->
![[Untitled 493.png]]

<!-- Column 2 -->
![[Untitled 494.png]]

![[Untitled 495.png]]

---

## Sintaxe

```sql
SELECT colunas 
FROM tabela_esquerda AS a
RIGHT JOIN tabela_direita AS b 
  ON a.chave = b.chave;
```

---

## Exemplo Prático

```sql
-- Retorna todos os clientes cadastrados e identifica quais não possuem notas associadas
SELECT DISTINCT 
    c.cpf, 
    c.nome, 
    nf.numero AS numero_nota
FROM notas_fiscais AS nf
RIGHT JOIN tabela_de_clientes AS c 
  ON c.cpf = nf.cpf
WHERE nf.cpf IS NULL;
```

> [!tip] 💡 Dica de Padronização
> Na prática da engenharia de software e SQL, o **`LEFT JOIN`** é amplamente preferido por padrão em relação ao `RIGHT JOIN`, pois torna a ordem de leitura das tabelas mais natural (da esquerda para a direita). Qualquer `RIGHT JOIN` pode ser reescrito como `LEFT JOIN` invertendo a posição das tabelas.
