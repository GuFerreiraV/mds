# História do SQL e do MySQL

Na década de 1970, a **IBM** desenvolveu o **System R**, um projeto de pesquisa pioneiro que tinha como objetivo criar um sistema de gerenciamento de banco de dados relacional baseado nos trabalhos teóricos de Edgar F. Codd. 

O System R foi pioneiro ao introduzir conceitos fundamentais da computação moderna, como:
- **Tabelas e Tuplas** (linhas e colunas);
- A linguagem estruturada de consultas **SEQUEL** (que posteriormente evoluiu para **SQL** - *Structured Query Language*);
- Mecanismos de integridade e transações.

Em meados dos anos 1990, os desenvolvedores Michael Widenius ("Monty"), David Axmark e Allan Larsson criaram o **MySQL**, com foco em alta performance, simplicidade de uso e suporte para ambientes web em rápida expansão (a clássica pilha LAMP: Linux, Apache, MySQL, PHP).

---

## Características Principais do SQL / MySQL

> [!note]+ Características Arquiteturais
> - **Arquitetura Cliente-Servidor:** Os clientes enviam consultas SQL e o servidor MySQL processa e retorna os resultados.
> - **Portabilidade:** Funciona de forma consistente em Windows, Linux, macOS e sistemas Unix.
> - **Multithread:** Suporta conexões e operações concorrentes em múltiplos núcleos de CPU.
> - **Motores de Armazenamento Pluggáveis:** Suporta diferentes engines como **InnoDB** (transacional, ACID, chaves estrangeiras) e **MyISAM** (focado em leituras rápidas).
> - **Segurança e Controle de Acesso:** Gerenciamento granular de privilégios de usuários.
> - **Mecanismos de Logs:** Binlog, General Log, Slow Query Log e Error Log para recuperação e diagnóstico.

---

## Vantagens e Desafios

### Vantagens
- **Curva de Aprendizado Agradável:** Sintaxe declarativa intuitiva e padronizada.
- **Portabilidade:** Padrão ANSI/ISO amplamente adotado em diferentes SGBDs.
- **Comunidade Ativa:** Ecossistema gigantesco de bibliotecas, ferramentas de administração (Workbench, DBeaver) e documentação.
- **Confiabilidade e Longevidade:** Décadas de maturidade em produção empresarial.

### Desafios / Considerações
- **Estruturação Rígida:** Alterações em esquemas muito volumosos exigem planejamento prévio de migração.
- **Escalabilidade Horizontal:** Bancos relacionais tradicionalmente escalam verticalmente, embora hoje suportem particionamento, replicação master-replica e clusters.
