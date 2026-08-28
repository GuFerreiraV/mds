---

---
# *Protocolo WEP*

- WEP (Wired Equivalent Privacy) é o protocolo de segurança de Wi-Fi mais antigo e comum. Um conjunto de padrões técnicos que tinha o objetivo de fornecer uma rede local sem fio (WLAN) com um nível de segurança comparável a uma rede local com fio (LAN).
- WEP tem sofrido ao longo dos anos com muitas falhas de segurança. Apesar dos esforços para melhorar o WEP, ele ainda é vulnerável a falhas de segurança. A Wi-Fi Alliance aposentou oficialmente o WEP em 2004.

---

# *Protocolo WPA*

- O WPA (Wi-Fi Protected Access) é um protocolo de segurança de rede sem fio lançado para resolver as crescentes vulnerabilidades de seu antecessor, o WEP. O protocolo Wi-Fi do WPA é mais seguro que o WEP, porque usa uma chave de **256 bits** para criptografia, que é um grande aumento em relação às chaves de **64 e 128 bits usadas pelo sistema WEP**.
- O WPA também usa o <u>**Temporal Key Integrity Protocol (TKIP)**</u>, que ==gera dinamicamente uma nova chave para cada pacote ou unidade de dados==. O TKIP é muito mais seguro do que o sistema de chave fixa usado pelo WEP.

---

# *Protocolo WPA2*

- O WPA2 (Wi-Fi Protected Access 2) é a segunda geração do protocolo de segurança de rede sem fio WPA. Como o antecessor, o WPA2 foi projetado para proteger redes Wi-Fi. 
- O WPA2 garante que os dados enviados ou recebidos pela rede sem fio sejam criptografados e somente as pessoas com a senha de rede tenham acesso a eles.
- Um benefício do sistema WPA2 foi introduzir o <u>**Advanced Encryption System (AES)**</u> ==para substituir o sistema TKIP mais vulnerável usado no protocolo WPA original==. Usado pelo governo dos EUA para proteger dados confidenciais, o AES fornece **criptografia forte**.

![[Untitled 87.png]]

### *WPA2 Personal*

- Personal é o modo mais comumente usado em redes **wi-fi domésticas**. Também conhecido como modo ==Pre-Shared Key (====**PSK**====)==, ele ==utiliza uma senha compartilhada que deve ser inserida tanto no dispositivo cliente quanto no ponto de acesso.==

### *WPA2 Enterprise*

- É normalmente **usado em ambientes empresariais ou institucionais**. Ele utiliza o ==Extensible Authentication Protocol (====**EAP**====)== em conjunto com um servidor de autenticação centralizado, permitindo que cada usuário ou dispositivo faça login com credenciais exclusivas.

---

## *WPA3*

- ==WPA3 (Wi-Fi Protected Access 3)== é o mais novo protocolo de segurança sem fio, projetado para criptografar dados com mais segurança e proteger sessões anteriores, mesmo que uma senha seja comprometida posteriormente, um recurso chamada como ==Perfect Forward Secrecy.==
- WPA3 é mais seguro que o WPA2.
- WPA3 utiliza o ==AES-GCMP (Galois/Counter Mode Protocol)==, um modo de criptografia de alto desempenho que aumenta a segurança e a velocidade. Comparado ao modo AES-CCMP usado no WPA2, o **GCMP oferece melhor integridade de dados e eficiência geral**.