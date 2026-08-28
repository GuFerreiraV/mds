## O que é 

- É uma ferramenta com o objetivo de prover uma conexão segura para acessar servidores remotamente. 
- SSH foi criado para resolver a questão de segurança, permitindo a conexão e comunicação entre o cliente e o servidor de **forma segura**, através da **criptografia das informações**.
- SSH é ferramenta mais utilizada para **gerenciar servidores remotamente.** 

---

## Camadas

- É composto por três camadas: camada de transporte, camada de autenticação e a camada de sessão.

### *Camada de transporte* 

- Camada mais baixa do SSH e é responsável por estabelecer e gerenciar uma conexão segura entre o cliente e o servidor. 
- Criptografa todas as informações transmitidas, impedindo que qualquer pessoa intercepte e leia as informações.

---

### *Camada de autenticação*

- Camada intermediária do SSH e é responsável por verificar a identidade do usuário que está se conectando ao servidor. 
- Isso é feito através de uma autenticação de senha.

---

### *Camada de sessão*

- Responsável por gerenciar as sessões estabelecidas entre o cliente e o servidor.
- Permite que o usuário execute comandos e transfira arquivos.
- Além de permitir que o servidor envie informações de volta para cliente.

---

## *Criptografia* 

- É baseada em chaves públicas e privadas;
- Quando dois dispositivos se conectam pela primeira vez, eles trocam suas chaves públicas. 
- Após isso, ambos usam a chave pública do dispositivo remoto para criptografas os dados que serão transmitidos. 
- E a chave privada do dispositivo remoto para descriptografar esses dados. 
- O processo de autenticação é baseado em uma **chave pública pré-compartilhada** ou em **autenticação por senha**. 
- Uma vez autenticado, o canal de segurança é estabelecido e todos os dados transmitidos neste canal serão criptografados.