> Código que a máquina entende : Código binário 010110 (**Código de máquina**)

- Em um computador, o ‘0‘ e ‘1’ é chamada de **bit (Binary Digit)**,** **como bit é uma unidade pequena, costuma-se trabalhar com grupos de 8 bits e essa quantidade de bits é chamada de **Byte. **
- Um arquivo de 200MB é um arquivo com 200 milhões de bytes. 
- Uma Internet com velocidade de 20Mbps transfere **20 milhões de bits** por segundo ou **2,5 milhões de bytes** por segundo.

# Tradutores de códigos 

## Compilador

- Execução rápida.
- Contexto completo antes de precisar executar.
- Verifica erros antes de executar.
- Tempo extra para executar.
- Executa em uma máquina.

Linguagens compiladores: C, Go, R

## Interpretador

- Execução lenta
- Interpretação + execução (em tempo real)
- Só verifica erros executando 
- Começa a executar na hora
- Executa em diferentes máquinas

Linguagens interpretadoras : JavaScript, Python, Ruby, PHP

---

# Memórias secundárias

## HD

> Hard Disk ou Disco Rígido

1. Vantagem:
    1. Grande capacidade
2. Desvantagem:
    2. Lento
    3. Frágil


## SSD 

> Solid State Drive ou Unidade de Estado Sólido

3. Vantagem:
    1. Menores
    2. Rápidos
4. Desvantagem:
    3. Caros
    4. Limitação de escrita



# Memória de trabalho 

### Memória RAM 

> Random Access Memory ou Memória de acesso aleatório

- Guarda os dados que o computador está lendo no momento atual;
- Memória volátil/temporária; 
- Dados são apagados após desligar o computador;



### Memória ROM 

> Read Only Memory ou Memória de apenas leitura

- É responsável pelo armazenamento dos dispositivos e de suas informações.
- É um tipo de memória não volátil com baixo armazenamento.
- Seus modelo são projetados para serem apenas lidos, então, não é esperado que o usuário escreva informações na memória ROM.
- Quando o computador é inicializado, as primeiras informações que ele irá buscar estarão na ROM (exemplo: BIOS - Basic Input/Ouput System)

### CPU 

> Central Process Unit ou Unidade Central de Processamento

5. Parte: Recebimento de informações
    1. Chama-se Unidade de controle, ela analisa as instruções repassadas (bit - 0101010110);
6. Parte: Unidade Lógico Aritmética
    2. Executa e manipula os dados;
    3. Recebe sinais elétricos (instruções)
7. Parte: Registradores
    4. Responsáveis pela memória do computador;
    5. Guarda a instrução atual;
    6. Guarda a posição da instrução;
    7. Guarda valores intermediários;

---

### Processador

As instruções do computador serão executadas em uma sequência especifica. 

8. Buscar a instrução
9. Decodificar a instrução
10. Executar a instrução
- Frequência de processador (velocidade, clock)
- Core: O core é o núcleo do processador (É possível possuir até 4 cores).
- Cache: É um tipo de memória auxiliar, que faz diminuir o tempo de transmissão de informações entre o processador e outros componentes.

## Entrada e saída ou I/O 

- Entrada → Periféricos (mouse, keyboard, camera, etc.)
- Saída → Vídeo saindo do monitor, Audio, impressora.   

> Esses dispositivos são responsáveis pela iteração entre usuário e computador.


## GPU 

> Graphics Processing Unit ou placa de vídeo

- É a unidade responsável pela renderização dos pixels na tela do computador.
- Algoritmos de machine learning e ciência de dados utilizam a alta capacidade de processamento numérico da GPU para acelerar seus cálculos. Isso é chamado de computação acelerada via GPU.

## TPU

> Tensor Processing Unit ou Unidade de Processamento de Tensores.

- Elas aumentam a performance nessas aplicações, em relação à GPU, e é usada em grandes empresas de tecnologia.

---

## Memória cache: Melhorando a performance 

### DRAM

- Há dois tipos de memória, a memória RAM e ela é construída  por um material que se chama DRAM (Dynamic RAM ou RAM dinâmica), 
11. Vantagem → Esse tipo de memória RAM é mais barata e consegue armazenar grandes quantidades de memória na escala de GB.
12. Desvantagem → Ela é lenta para buscar informações.

### SRAM

- Por outro lado , tem o segundo tipo de memória, chamada SRAM (static RAM ou RAM estática).
13. Vantagem → É mais rápida que a DRAM
14. Desvantagem → Mais cara

---

### Princípio da localidade 

15. Localidade temporal
    1. Acessar um local, e ele ficará salvo sempre

16. Localidade Espacial
    1. Acessar o local vizinho em breve 

---

## Processador de 32 ou 64 bits 

> Tamanho de informação que pode ser processada na CPU em um ciclo de clock.

### Processador de 64 bits

- Possui uma performance melhor, processa mais de uma só vez;
- Sua otimização é mais complexas;  

> Um processador de 32 bits possui apenas 4GB

---

## Codificadores UTF-8 | UTF-16 | UTF-32

> Representam os vários caracteres do sistema Unicode.

- Todos os três sistemas conseguem codificar todos os caracteres do Unicode. Apenas a quantidade de bits que serão usadas é o que muda

### UTF-8

- Representa os caracteres em pedaços de 8bits, e sua vantagem é manter os textos codificados apenas em ASCII intactos.
- Essa é a codificação mais comum na web

### UTF-16

- Representa os caracteres em pedaços de 16bits, por isso, não é mais compatível com ASCII e ocupa o dobro de memória em textos com apenas caracteres da língua inglesa. 
- Sua vantagem é ocupar menos espaço quando os textos possuem muitos caracteres asiáticos.

### UTF-32

- Representa os caracteres em pedaços de 32bits, e não é compatível com ASCII e ocupa 4 vezes mais espaço em textos que utilizam ASCII.
- Sua vantagem é que ele tem um tamanho fixo.  