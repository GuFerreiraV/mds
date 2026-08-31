## Descrição do Problema

Sintoma: O jogo encerra imediatamente ao iniciar, retornando o código de saída return code: 1280 (wait status: 5).

**Mensagem de Erro**:
```
Fontconfig error: "/etc/fonts/fonts.conf", line 86: out of memory
Fontconfig error: "/etc/fonts/fonts.conf", line 91: out of memory
Fontconfig error: Cannot load config file from /etc/fonts/fonts.conf
```

**Causa Raiz**

Corrupção ou dessincronização no cache do Fontconfig: O parser XML da biblioteca fontconfig encontrou entradas inválidas, corrompidas ou geradas em arquiteturas incompatíveis no cache local/sistema de fontes.

**Comportamento do Wine/UMU**: Ao tentar carregar as definições de fontes do host para renderizar o ambiente do jogo (processo 32-bit DP.exe), a falha de alocação/leitura no parser emitiu o erro falso-positivo out of memory e abortou o subprocesso antes da criação da janela gráfica.

Solução Aplicada
Regeneração forçada do cache de fontes do sistema e do usuário:

```Bash
# Limpa e regenera o cache global do sistema
sudo fc-cache -r -v

# Limpa e regenera o cache do usuário atual
fc-cache -r -v
```

**Parâmetros**:

***-r (--really-force)***: Apaga os arquivos de cache existentes (*.cache-7, etc.) antes de reescaneá-los.

***-v (--verbose)***: Exibe o progresso de indexação dos diretórios de fontes.

**Soluções Alternativas / Plano de Mitigação (Caso reincida)**

Limpeza manual de diretórios de cache:

```Bash
rm -rf ~/.cache/fontconfig/*
sudo rm -rf /var/cache/fontconfig/*
fc-cache -fv
```
**Ajuste de runner no Lutris**: Trocar executores baseados em Proton/UMU por runners Wine dedicados (wine-ge-custom / lutris-GE) para binários 32-bit legados.

**Isolamento de prefixo**: Configurar o prefixo Wine em modo win32 isolado para evitar o mapeamento direto de tabelas de fontes complexas do host.