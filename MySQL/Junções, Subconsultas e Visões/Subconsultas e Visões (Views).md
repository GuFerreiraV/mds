# Subconsultas e Visões (Views)

Subconsultas e Visões são recursos avançados que permitem encapsular, reaproveitar e abstrair lógicas complexas de consulta.

---

## 1. O que é uma Visão (`VIEW`)?

Uma **View** é uma tabela virtual cujo conteúdo é definido dinamicamente por uma consulta SQL pré-armazenada.

![[Untitled 486.png]]

### Vantagens das Views:
- **Reaproveitamento de Lógica:** Evita reescrever JOINs e regras de negócio repetitivas.
- **Segurança e Abstração:** Permite conceder acesso a apenas certas colunas/linhas sem expor a tabela original inteira.

```sql
-- Criando uma View com os maiores preços por embalagem
CREATE OR REPLACE VIEW vw_maiores_embalagens AS 
SELECT 
    embalagem, 
    MAX(preco_de_lista) AS maior_preco 
FROM tabela_de_produtos 
GROUP BY embalagem;

-- Consultando a View como se fosse uma tabela comum
SELECT * 
FROM vw_maiores_embalagens 
WHERE maior_preco >= 10.00;

-- Combinando a View com outras tabelas usando JOIN
SELECT 
    p.nome_do_produto, 
    p.embalagem, 
    p.preco_de_lista, 
    vw.maior_preco 
FROM tabela_de_produtos AS p
INNER JOIN vw_maiores_embalagens AS vw 
  ON p.embalagem = vw.embalagem;
```

---

## 2. O que é uma Subconsulta (Subquery)?

Uma **Subconsulta** é uma instrução `SELECT` aninhada dentro de outra instrução SQL (`SELECT`, `INSERT`, `UPDATE` ou `DELETE`).

### Tipos de Subconsultas

1. **Subconsulta Escalar (Linha Única / Valor Único):**
   ```sql
   -- Localiza o cliente com o CPF especificado
   SELECT * FROM tabela_de_clientes
   WHERE cpf = (SELECT cpf FROM tabela_de_clientes WHERE cpf = '1471156710');
   ```

2. **Subconsulta de Múltiplas Linhas (`IN`, `ANY`, `ALL`):**
   ```sql
   -- Clientes que moram nos bairros presentes no estado de São Paulo
   SELECT nome, estado, bairro 
   FROM tabela_de_clientes
   WHERE bairro IN (SELECT DISTINCT bairro FROM tabela_de_clientes WHERE estado = 'SP');
   ```

3. **Subconsulta como Tabela Derivada (no `FROM`):**
   ```sql
   SELECT 
       codigo_do_produto, 
       nome_do_produto, 
       AVG(preco_de_lista) AS media_preco
   FROM tabela_de_produtos 
   GROUP BY codigo_do_produto, nome_do_produto
   HAVING AVG(preco_de_lista) < (
       SELECT MAX(media) 
       FROM (
           SELECT AVG(preco_de_lista) AS media 
           FROM tabela_de_produtos 
           GROUP BY codigo_do_produto
       ) AS sub_medias
   )
   ORDER BY codigo_do_produto;
   ```

4. **Subconsulta Correlacionada:**
   > Faz referência a colunas da consulta externa, sendo avaliada uma vez para cada linha retornada pela query principal.
