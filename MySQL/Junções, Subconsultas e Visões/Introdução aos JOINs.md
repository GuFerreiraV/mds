# Introdução aos JOINs

As operações de **JOIN (Junções)** no SQL permitem combinar registros de duas ou mais tabelas em um único conjunto de resultados, baseando-se em colunas relacionadas (geralmente chaves primárias e estrangeiras).

---

## Tipos Principais de Junções

```
  ┌─────────────────────────────────────────────────────────────┐
  │                      TIPOS DE JOIN                          │
  ├──────────────────┬──────────────────────────────────────────┤
  │ INNER JOIN       │ Apenas registros com correspondência     │
  │                  │ em ambas as tabelas (interseção).        │
  ├──────────────────┼──────────────────────────────────────────┤
  │ LEFT JOIN        │ Todos da tabela à esquerda +             │
  │                  │ correspondentes da direita (ou NULL).    │
  ├──────────────────┼──────────────────────────────────────────┤
  │ RIGHT JOIN       │ Todos da tabela à direita +              │
  │                  │ correspondentes da esquerda (ou NULL).   │
  ├──────────────────┼──────────────────────────────────────────┤
  │ FULL JOIN        │ Todos os registros de ambas as tabelas   │
  │                  │ (emulado no MySQL via UNION).            │
  ├──────────────────┼──────────────────────────────────────────┤
  │ CROSS JOIN       │ Produto cartesiano (todas as combinações)│
  └──────────────────┴──────────────────────────────────────────┘
```

---

## Diagrama Conceitual de Conjuntos

- **INNER JOIN:** $A \cap B$ (apenas interseção).
- **LEFT JOIN:** $A$ completo + $(A \cap B)$.
- **RIGHT JOIN:** $B$ completo + $(A \cap B)$.
- **FULL JOIN:** $A \cup B$ (união total).
