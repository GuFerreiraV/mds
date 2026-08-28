# Funções de Manipulação de Texto (Strings)

O MySQL oferece um vasto conjunto de funções nativas para tratar, formatar, concatenar e extrair dados textuais.

---

## 1. Concatenação de Strings: `CONCAT` e `CONCAT_WS`

### `CONCAT(str1, str2, ...)`
Une duas ou mais cadeias de caracteres em uma única string:

```sql
-- Concatenação com separadores manuais
SELECT 
    nome, 
    CONCAT(endereco_1, ' - ', bairro, ' - ', cidade, '/', estado) AS endereco_completo 
FROM tabela_de_clientes;
```

![[Untitled 505.png]]
![[Untitled 506.png]]

---

### `CONCAT_WS(separador, str1, str2, ...)`
(*Concatenate With Separator*) Adiciona automaticamente o caractere delimitador entre cada termo:

```sql
SELECT 
    nome, 
    CONCAT_WS(' | ', endereco_1, bairro, cidade, estado) AS perfil_cliente 
FROM tabela_de_clientes;
```

![[Untitled 507.png]]

---

## 2. Extração e Posição de Texto: `SUBSTRING` e `FIND_IN_SET`

### `SUBSTRING(texto, inicio, tamanho)`
Extrai um trecho da string a partir da posição inicial (base 1 no SQL):

```sql
SELECT 
    nome, 
    SUBSTRING(nome, 4, 8) AS trecho_extraido 
FROM tabela_de_clientes;
```

![[Untitled 508.png]]

---

### `FIND_IN_SET(termo, lista_separada_por_virgula)`
Retorna o índice (posição) do elemento dentro de uma lista de valores separados por vírgula. Retorna `0` caso não encontre:

```sql
SELECT FIND_IN_SET('v', 'b,a,k,o,v,s,q,l') AS posicao_letra; -- Retorna 5
SELECT FIND_IN_SET('L', 's,q,l') AS posicao_letra;            -- Retorna 0 (não encontrado)
```

---

## 3. Tamanho e Contagem: `LENGTH` e `CHAR_LENGTH`

- **`LENGTH(str)`:** Retorna o tamanho em **bytes**.
- **`CHAR_LENGTH(str)`:** Retorna a quantidade de **caracteres** (ideal para acentuação UTF-8).

```sql
SELECT 
    nome, 
    CHAR_LENGTH(nome) AS quantidade_caracteres 
FROM tabela_de_clientes;
```

![[Untitled 509.png]]

---

## 4. Remoção de Espaços: `TRIM`, `LTRIM` e `RTRIM`

- **`TRIM(str)`:** Remove espaços em branco das duas extremidades.
- **`LTRIM(str)`:** Remove espaços à esquerda (*Left Trim*).
- **`RTRIM(str)`:** Remove espaços à direita (*Right Trim*).

```sql
SELECT LTRIM('           Gustavo') AS sem_espaco_esquerda;
SELECT RTRIM('Gustavo           ') AS sem_espaco_direita;
SELECT TRIM('    Gustavo Ferreira    ') AS texto_limpo;

-- Combinando TRIM com formatação
SELECT CONCAT(TRIM(nome), ' | E-mail: ', TRIM(contato)) AS contato_formatado 
FROM clientes;
```

---

## 5. Transformação de Caixa: `UPPER` e `LOWER`

```sql
SELECT 
    UPPER(nome) AS nome_maiusculo, 
    LOWER(email) AS email_minusculo 
FROM tabela_de_clientes;
```

---

## 6. Substituição e Preenchimento: `REPLACE`, `LPAD` e `RPAD`

```sql
-- Substituição de caracteres
SELECT REPLACE(nome_do_produto, 'Litro', 'L') AS produto_abreviado 
FROM tabela_de_produtos;

-- Preenchimento à esquerda com zeros (ex.: formatação de código com 6 dígitos)
SELECT LPAD(codigo_produto, 6, '0') AS codigo_formatado 
FROM tabela_de_produtos;
```
