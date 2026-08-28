# Junção à Esquerda (`LEFT JOIN`)

O `LEFT JOIN` (ou `LEFT OUTER JOIN`) retorna **todos os registros da tabela à esquerda** (primeira tabela declarada), juntamente com os registros correspondentes da tabela à direita.

> [!note] 📌 Registros Não Correspondentes
> Quando não houver linha correspondente na tabela da direita, as colunas dessa tabela virão preenchidas como **`NULL`**.

<!-- Column 1 -->
![[Untitled 490.png]]

<!-- Column 2 -->
![[Untitled 491.png]]

![[Untitled 492.png]]

---

## Sintaxe

```sql
SELECT colunas 
FROM tabela_esquerda AS a
LEFT JOIN tabela_direita AS b 
  ON a.chave = b.chave;
```

---

## Exemplos Práticos

### 1. Todos os Clientes e Suas Notas Emitidas

```sql
SELECT DISTINCT 
    c.cpf, 
    c.nome, 
    nf.numero AS numero_nota
FROM tabela_de_clientes AS c
LEFT JOIN notas_fiscais AS nf 
  ON c.cpf = nf.cpf;
```

---

### 2. Identificando Registros Órfãos / Sem Correspondência

Para localizar registros da tabela à esquerda que **não possuem nenhum relacionamento** na tabela à direita, combinamos o `LEFT JOIN` com `WHERE tabela_direita.chave IS NULL`:

```sql
-- Localiza clientes que NUNCA realizaram nenhuma compra
SELECT 
    c.cpf, 
    c.nome
FROM tabela_de_clientes AS c
LEFT JOIN notas_fiscais AS nf 
  ON c.cpf = nf.cpf
WHERE nf.cpf IS NULL;
```
