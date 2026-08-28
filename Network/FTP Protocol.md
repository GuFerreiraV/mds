> File Transfer Protocol 

- Uma maneira de baixar e transferir dados entre computadores;
- Usando conexões TCP/IP, ele permite que usuários enviem e recebam arquivos de <u>**FTP servers**</u>. 

---

## *Como funciona*

- A conexão FTP precisa de **duas partes** para estabelecer e se comunicar na rede. 
- Existem dois canais de comunicação para se estabelecer uma conexão usando FTP: 
    1. <u>**Canal de comando**</u>, que é onde se inicia a instrução e a resposta.
    2. <u>**Canal de dados**</u>, onde ocorre a distribuição de dados.

---

- Caso queira baixar ou transferir um arquivo, um usuário terá que usar o protocolo para solicitar a criação de mudanças no servidor, em troca, o servidor vai garantir esse acesso. 
- Essa seção é conhecida como “modo de conexão ativa”.

- O <u>**modo passivo**</u> é usado caso esse problema ocorrer. Neste modo, o usuário estabelece tanto o canal de comando quanto o de dados.

---

## *Como usar*

Existem três abordagens para estabelecer uma conexão FTP: 

Um método simples é usando um FTP em linha de comando (CMD ou terminal do Mac e Linux);

É possível também usar o navegador para se comunicar com o servidor FTP (Usado com frequência quando os usuários querem acessar grandes diretórios no servidor);

Cliente FTP é o mais comum na hora de se usar um FTP; ==Oferece mais liberdade se comparado a uma linha de comando e a um navegador, também é mais fácil de gerenciar e mais poderoso==.
