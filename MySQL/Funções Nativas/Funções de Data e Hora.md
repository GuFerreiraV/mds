# Funções de Data e Hora

O MySQL disponibiliza uma biblioteca completa de funções para manipulação, cálculo de intervalos, extração de partes e formatação temporal.

---

## 1. Obtendo a Data e Hora Atual do Sistema

```sql
-- Retorna a data atual (formato 'AAAA-MM-DD')
SELECT CURDATE(); -- ou CURRENT_DATE()

-- Retorna a hora atual (formato 'HH:MM:SS')
SELECT CURRENT_TIME(); -- ou CURTIME()

-- Retorna a data e a hora completas
SELECT NOW(); -- ou CURRENT_TIMESTAMP()
```

---

## 2. Extração de Partes de uma Data

```sql
-- Extraindo componentes individuais
SELECT 
    data_venda,
    DAY(data_venda) AS dia_do_mes,
    MONTH(data_venda) AS numero_mes,
    YEAR(data_venda) AS ano,
    DAYNAME(data_venda) AS nome_dia_semana,
    MONTHNAME(data_venda) AS nome_mes
FROM notas_fiscais;
```

![[Untitled 510.png]]

---

## 3. Cálculos de Diferença entre Datas: `DATEDIFF` e `TIMESTAMPDIFF`

### `DATEDIFF(data_final, data_inicial)`
Retorna o número total de dias entre duas datas:

```sql
-- Diferença em dias entre duas datas fixas
SELECT DATEDIFF('2026-08-28', '2026-08-01') AS diferenca_dias; -- Retorna 27

-- Total de dias hospedados agrupados por tipo
SELECT 
    h.tipo, 
    SUM(DATEDIFF(a.data_fim, a.data_inicio)) AS total_dias_hospedado,
    SUM(a.ativo) AS total_ativos
FROM alugueis AS a
INNER JOIN hospedagens AS h ON a.hospedagem_id = h.hospedagem_id
GROUP BY h.tipo;
```

![[image 66.png]]

---

### `TIMESTAMPDIFF(unidade, data_inicial, data_final)`
Calcula a diferença em unidades específicas (`YEAR`, `MONTH`, `DAY`, `HOUR`, `MINUTE`, `SECOND`):

```sql
-- Calculando a idade exata dos clientes em anos
SELECT 
    nome, 
    data_de_nascimento,
    TIMESTAMPDIFF(YEAR, data_de_nascimento, CURDATE()) AS idade_anos 
FROM tabela_de_clientes;
```

![[Untitled 511.png]]

---

## 4. Adição e Subtração de Intervalos: `DATE_ADD`, `DATE_SUB` e `ADDDATE`

```sql
-- Somando dias, meses e anos
SELECT 
    data_de_nascimento,
    ADDDATE(data_de_nascimento, INTERVAL 1 DAY) AS mais_um_dia,
    ADDDATE(data_de_nascimento, INTERVAL 1 MONTH) AS mais_um_mes,
    ADDDATE(data_de_nascimento, INTERVAL 1 YEAR) AS mais_um_ano
FROM tabela_de_clientes;

-- Subtraindo 30 dias de uma data
SELECT DATE_SUB(NOW(), INTERVAL 30 DAY) AS trinta_dias_atras;
```

---

## Tabela de Referência Rápida de Funções Temporais

| Função | Descrição |
| :--- | :--- |
| **`CURDATE()`** | Retorna a data atual. |
| **`NOW()`** | Retorna a data e hora atuais. |
| **`DATE(expr)`** | Extrai a parte da data de um valor datetime. |
| **`TIME(expr)`** | Extrai a parte do tempo de um valor datetime. |
| **`YEAR(data)`** | Retorna o ano (4 dígitos). |
| **`MONTH(data)`** | Retorna o mês (1 a 12). |
| **`DAY(data)`** | Retorna o dia do mês (1 a 31). |
| **`WEEK(data)`** | Retorna o número da semana no ano (0 a 53). |
| **`WEEKDAY(data)`** | Retorna o índice do dia da semana (0 = Segunda a 6 = Domingo). |
| **`DATEDIFF(d1, d2)`** | Retorna a diferença em dias ($d1 - d2$). |
| **`TIMEDIFF(t1, t2)`** | Retorna a diferença entre duas horas/datetimes. |
| **`DATE_FORMAT(d, fmt)`**| Formata a data de acordo com a máscara especificada. |
| **`STR_TO_DATE(str, fmt)`**| Converte uma string formatada em um tipo de dado `DATE` válido. |
