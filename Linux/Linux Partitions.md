### O que são partições? (resumo)

- São simplesmente as divisões de um disco rígido.
- Esse particionamento de disco ocorre dentro da estrutura lógica do disco, ou seja, na parte **abstrata**. Com isso, a estrutura física do disco não sofre nenhuma alteração.
- Desse modo, cada partição do disco pode ser direcionada para uma finalidade, como ==armazenamento de dados, sistema operacional, memória Swap==.
- Obs: Quando há uma interferência em uma das partições, a outra não é afetada. Ex: Se a partição do SO é formatada, a partição de armazenamento de dados se mantém intacta.

---

- As partições do Linux podem ser subdivididas em duas categorias: partições de dados (arquivs que iniciam e executam o sistema) e partições de troca (expandem a memória física do computador, pois utilizam a partição como cache). 
- Enquanto a nomenclatura no Windows das unidades é **C, F ou D**, no Linux o disco rígido é nomeado como **/dev/sdb**, **/dev/sdc** entre outras.

---

### Tipos de partições

- **Primário**: Esse tipo de partição armazena sistema de arquivos. Portanto, geralmente trata-se de partições de sistemas operacionais.
- **Estendido:** Tipo de partição que abriga partições lógicas.
- **Lógico:** Esse tipo de partição está dentro de Estendido, e recebe sistemas de arquivos.

---

## Padrões de particionamento de disco

### MBR

- Padrão mais comum, suportado pela BIOS. Portanto, nos computadores mais antigos, é com o MBR que iremos nos deparar.
- Esse padrão apresenta limitações, por isso foi criado o GPT.
- ==Uma de suas limitações é não permitir a configuração de mais de 4 partições primárias e cada partição ser limitada a 2 TB.==

### GPT

- Padrão mais moderno, que suporta interface UEFI.
- ==Suporta até 128 partições primárias e que armazenam mais de 2 TB ==
