# Sensibilidade a Maiúsculas e Minúsculas (Case Sensitivity)

No MySQL, o comportamento de diferenciação entre maiúsculas e minúsculas (*case sensitivity*) varia de acordo com o elemento consultado e o sistema operacional subjacente.

---

## 1. Palavras-Chave e Funções SQL
- **Não são sensíveis a maiúsculas/minúsculas:**
  - `SELECT`, `select`, `Select` são idênticos.
  - `COUNT()`, `count()`, `Count()` produzem o mesmo resultado.
  - *Boa prática:* Escrever palavras-chave SQL em **MAIÚSCULAS** para facilitar a leitura.

---

## 2. Nomes de Tabelas e Bancos de Dados
O comportamento depende da variável de sistema `lower_case_table_names` e do sistema operacional:

- **Linux / Unix:** O sistema de arquivos diferencia maiúsculas de minúsculas por padrão (`clientes` é diferente de `Clientes`).
- **Windows / macOS:** O sistema de arquivos padrão não é sensível a maiúsculas (`clientes` e `CLIENTES` referenciam o mesmo arquivo físico).

### Configuração `lower_case_table_names`

| Valor | Descrição |
| :--- | :--- |
| `0` | Nomes de tabelas são armazenados como especificados e as comparações são sensíveis a maiúsculas (padrão em Linux). |
| `1` | Nomes de tabelas são armazenados em minúsculas e as comparações não diferenciam maiúsculas (padrão em Windows). |
| `2` | Nomes são armazenados como especificados, mas comparados em minúsculas (padrão em macOS). |

---

## 3. Dados e Colunas (Collation)
A sensibilidade de texto nas consultas depende do **Collation** definido para a tabela ou coluna:

- **`_ci` (*Case Insensitive*):** Não diferencia maiúsculas de minúsculas (`'Maria'` é igual a `'maria'`). Exemplo: `utf8mb4_0900_ai_ci` ou `utf8mb4_unicode_ci`.
- **`_bin` ou `_cs` (*Case Sensitive / Binary*):** Diferencia maiúsculas de minúsculas (`'Maria'` é diferente de `'maria'`).

### Forçando Comparação Binária em Consultas:

```sql
-- Busca estrita diferenciando maiúsculas de minúsculas
SELECT * 
FROM usuarios 
WHERE BINARY login = 'Admin';
```