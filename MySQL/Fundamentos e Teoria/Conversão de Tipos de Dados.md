# Conversão de Tipos de Dados

O MySQL permite realizar conversões de tipos de dados tanto de forma **implícita** (automática pelo interpretador) quanto **explícita** (usando funções dedicadas como `CAST` e `CONVERT`).

---

## 1. Conversão Implícita

O MySQL converte automaticamente valores quando os tipos são compatíveis em operações de concatenação ou comparações:

```sql
-- O CURRENT_TIMESTAMP retorna data/hora, mas é convertido implicitamente em texto no CONCAT
SELECT CONCAT("Data e hora atual: ", CURRENT_TIMESTAMP()) AS info_sistema;

-- Conversão numérica implícita em operações matemáticas
SELECT '100' + 50 AS resultado; -- Retorna 150 (número)
```

---

## 2. Conversão Explícita: `CAST` e `CONVERT`

Usadas para converter expressamente um valor de um tipo para outro:

```sql
-- Sintaxe do CAST
SELECT CAST('2026-08-28' AS DATE) AS data_formatada;
SELECT CAST(123.45 AS SIGNED) AS numero_inteiro; -- Retorna 123
SELECT CAST('45.67' AS DECIMAL(10, 2)) AS valor_decimal;

-- Sintaxe do CONVERT
SELECT CONVERT('2026-08-28 14:30:00', DATETIME) AS data_hora;
```

---

## 3. Formatação e Conversão de Datas e Horas

A função `DATE_FORMAT(data, formato)` permite formatar datas em texto legível personalizado.

```sql
-- Exemplo de formatação brasileira (Dia/Mês/Ano)
SELECT DATE_FORMAT(NOW(), '%d/%m/%Y') AS data_brasil; -- Ex.: 28/08/2026

-- Exemplo de formatação com hora completa
SELECT DATE_FORMAT(NOW(), '%d/%m/%Y %H:%i:%s') AS data_hora_completa;

-- Exemplo por extenso
SELECT DATE_FORMAT(NOW(), 'Hoje é %W, dia %d de %M de %Y') AS data_extenso;
```

---

## Tabela de Especificadores de Formato (`DATE_FORMAT`)

| Especificador | Descrição | Exemplo |
| :--- | :--- | :--- |
| `%d` | Dia do mês numérico (2 dígitos: `01` a `31`) | `28` |
| `%e` | Dia do mês numérico sem zero à esquerda (`1` a `31`) | `28` |
| `%m` | Mês numérico (2 dígitos: `01` a `12`) | `08` |
| `%c` | Mês numérico sem zero (`1` a `12`) | `8` |
| `%Y` | Ano com 4 dígitos | `2026` |
| `%y` | Ano com 2 dígitos | `26` |
| `%M` | Nome do mês completo em inglês | `August` |
| `%b` | Nome do mês abreviado | `Aug` |
| `%W` | Nome do dia da semana completo | `Friday` |
| `%a` | Nome do dia da semana abreviado | `Fri` |
| `%w` | Dia da semana numérico (`0` = Domingo a `6` = Sábado) | `5` |
| `%H` | Hora no formato 24 horas (`00` a `23`) | `15` |
| `%h` / `%I` | Hora no formato 12 horas (`01` a `12`) | `03` |
| `%i` | Minutos (`00` a `59`) | `45` |
| `%s` | Segundos (`00` a `59`) | `30` |
| `%p` | Indicador `AM` ou `PM` | `PM` |
| `%T` | Hora completa em 24h (`hh:mm:ss`) | `15:45:30` |
| `%f` | Microssegundos (`000000` a `999999`) | `123456` |
