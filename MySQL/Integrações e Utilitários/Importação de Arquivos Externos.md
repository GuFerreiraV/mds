# Importação de Arquivos Externos (CSV / TXT)

A importação de dados externos para tabelas do MySQL pode ser realizada tanto por assistentes visuais (como o MySQL Workbench) quanto por comandos SQL de alta performance (`LOAD DATA INFILE`).

---

## 1. Importação Visual pelo MySQL Workbench

Para importar dados de planilhas e arquivos `.csv` de forma gráfica:

1. No painel de navegação de esquemas (*Schemas*), clique com o botão direito sobre a tabela de destino e selecione a opção **`Table Data Import Wizard`**.
   ![[Untitled 514.png]]

2. Localize e selecione o arquivo `.csv` ou `.json` no seu computador.
3. Configure o mapeamento de colunas e selecione o formato de codificação correto (geralmente **`utf-8`**).
   ![[Untitled 515.png]]
4. Avance e aguarde a conclusão da carga dos registros.

---

## 2. Importação Nativa de Alta Velocidade: `LOAD DATA INFILE`

Para importar milhões de registros com máxima velocidade diretamente pelo SQL:

```sql
LOAD DATA INFILE 'C:/dados/clientes.csv'
INTO TABLE tb_clientes
CHARACTER SET utf8mb4
FIELDS TERMINATED BY ';'        -- Separador de colunas (vírgula, ponto e vírgula, tabulação '\t')
ENCLOSED BY '"'                 -- Caractere que envolve textos com aspas
LINES TERMINATED BY '\r\n'      -- Quebra de linha (Windows '\r\n', Linux '\n')
IGNORE 1 LINES                  -- Pula a primeira linha de cabeçalho
(codigo, nome, email, telefone);-- Mapeamento das colunas
```

---

## Dicas Importantes de Codificação e Formatos

- **Codificação de Caracteres:** Sempre utilize `utf8mb4` para evitar problemas com acentuação e caracteres especiais em português.
- **Formato de Datas:** O MySQL espera datas no padrão internacional `'AAAA-MM-DD'`. Caso seu arquivo CSV contenha datas brasileiras (`DD/MM/AAAA`), é possível converter na importação usando `STR_TO_DATE`:
  ```sql
  LOAD DATA INFILE 'C:/dados/pedidos.csv'
  INTO TABLE tb_pedidos
  FIELDS TERMINATED BY ','
  LINES TERMINATED BY '\n'
  IGNORE 1 LINES
  (numero_pedido, @data_br, valor)
  SET data_emissao = STR_TO_DATE(@data_br, '%d/%m/%Y');
  ```
