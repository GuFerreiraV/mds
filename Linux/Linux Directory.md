> Um diretório do Linux é simplesmente um arquivo, que é distribuído em forma de hierarquia. 

### Diferenças de diretórios entre Linux e Windows

- Suas diferenças estão no modo como eles foram desenvolvidos. O Windows surgiu na época dos microcomputadores, quando várias partições do disco rígido começaram a existir e ser usadas, como o `C:\` e `D:\`, e são inicializadas junto com o SO.
- Já o Linux, depende que suas [partições Linux](/2b5e4af651cd80819defc89012e01951) sejam criadas e ativadas, gerenciando o sistema “bootável”. Com essa flexibilidade e podendo ser ativado localmente, o Linux acaba sendo mais simples de entender e mexer.

---

## Principais diretórios do Linux

### (/) Root/Raiz

- É dentro deste diretório que todos os outros diretórios e comandos se localizam.
- Ele é o principal dentre a hierarquia de diretórios, sendo assim, somente o usuário com acesso administrador, poderá fazer modificações dentro dele.

### /bin

- Representa a localização de todos os arquivos binários, ou seja, comandos para executar funções do sistema.
- Somente com ele é possível explorar recursos de texto e rede do SO

### /sbin

- Parecido com o `/bin` , o `/sbin` também contempla os diretórios passíveis de execução, mas o admins da estrutura utilizam apenas para fazer alterações pontuais no sistema. 

### /usr

- A maioria dos aplicativos e softwares armazenados aqui estão disponiveis a todos os usuários, independentemente do nível de permissão.
- Este diretório pode ser executado em conjunto com os dois anteriores, dessa forma:
    - `/usr/bin`: que contém todos os arquivos binários (acionados pelo /bin), que podem ser vistos por qualquer usuário, não só pelo administrador;
    - `/usr/sbin`: mostra apenas os arquivos binários que são essenciais ao administrador, aos quais somente ele tem acesso.

### /etc

- Se precisar configurar qualquer arquivo ou software, as informações estarão neste diretório, até soluções para DNS.
- Caso queira interromper ou inicializar qualquer sistema através de scrips excluivos, basta procurar aqui.

### /lib

- Aqui é onde se encontram as bibliotecas de comandos.
- Parecido com o System32 do Windows.
