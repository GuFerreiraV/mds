# Junção Interna (`INNER JOIN`)

O `INNER JOIN` retorna **apenas as linhas que possuem correspondência mútua** entre as tabelas envolvidas, com base na condição especificada na cláusula `ON`.

<!-- Column 1 -->
![[Untitled 487.png]]

<!-- Column 2 -->
![[Untitled 488.png]]

![[Untitled 489.png]]

---

## Sintaxe

```sql
SELECT colunas 
FROM tabela_a AS a
INNER JOIN tabela_b AS b 
  ON a.chave_estrangeira = b.chave_primaria;
```

---

## Exemplos Práticos

### 1. Contagem de Notas Fiscais por Vendedor

```sql
SELECT 
    v.matricula, 
    v.nome, 
    COUNT(nf.numero) AS total_notas_emitidas 
FROM tabela_de_vendedores AS v
INNER JOIN notas_fiscais AS nf 
  ON v.matricula = nf.matricula 
GROUP BY v.matricula, v.nome;
```

---

### 2. População de Cidades por Continente

```sql
-- População total das cidades na Ásia
SELECT SUM(cidade.population) AS total_populacao
FROM city AS cidade
INNER JOIN country AS pais 
  ON cidade.CountryCode = pais.Code
WHERE pais.Continent = 'Asia';

-- Média da população urbana por continente
SELECT 
    pais.Continent, 
    FLOOR(AVG(cidade.Population)) AS media_populacao
FROM country AS pais
INNER JOIN city AS cidade 
  ON pais.Code = cidade.CountryCode
GROUP BY pais.Continent;
```

---

### 3. Junção por Intervalo de Faixas (`BETWEEN`)

```sql
SELECT 
    CASE 
        WHEN g.grade >= 8 THEN s.name
        ELSE NULL
    END AS nome_estudante,
    g.grade AS nota_conceito,
    s.marks AS pontuacao_obtida
FROM students AS s 
INNER JOIN grades AS g 
  ON s.marks BETWEEN g.min_mark AND g.max_mark
ORDER BY g.grade DESC, s.name ASC, s.marks ASC;
```
