## Descrição do Problema e Erros Observados
Durante a tentativa de executar o jogo X-Men Origins: Wolverine (Unreal Engine 3 / DirectX 9) via Lutris no CachyOS (Arch Linux), o executável falhou em inicializar, resultando em encerramento precoce e falhas em cascata nas ferramentas de compatibilidade.

**Erro 1: Ausência de Prefixo Wine Configurado**

Mensagem de Erro:

```Plaintext
ValueError: No Wine prefix path given
File "/usr/lib/python3.14/site-packages/lutris/runners/commands/wine.py", line 107, in create_prefix raise ValueError("No Wine prefix path given")
```
**Causa Raiz**: O jogo foi adicionado manualmente ao Lutris sem a definição de um diretório para o Wine prefix na aba Game options. Sem um prefixo associado, o Lutris e o utilitário Winetricks não conseguiram instanciar o ambiente Windows virtual (drive_c, registros e bibliotecas base).

**Erro 2: Falha de Inicialização do Binário e Incompatibilidade de Runtime Containerizado**

Mensagem de Erro:

```Plaintext
Fontconfig error: "/etc/fonts/fonts.conf", line 86: out of memory
Fontconfig error: Cannot load config file from /etc/fonts/fonts.conf
[umu.umu_run:744] DEBUG: Child 16775 exited with wait status: 5
Monitored process exited.
Initial process has exited (return code: 1280)
```

**Causa Raiz**: Incompatibilidade com o Wrapper UMU: A seleção de runners do Steam (GE-Proton) fora do ecossistema Steam acionou o umu-run (Unified Memory Architecture / Steam Runtime container). O ambiente isolado falhou no carregamento do fontconfig e no tratamento de chamadas legadas do jogo.

**Ausência de Runtimes Legados (PhysX / DirectX 9 / VC++)**: Jogos baseados em Unreal Engine 3 exigem bibliotecas redistribuíveis que não acompanham prefixos Wine limpos (como o driver de física PhysX e módulos do D3D9/D3DCompiler). Sem essas DLLs carregadas na memória, o processo era abortado no boot com return code: 1280.

## Soluções Aplicadas e Justificativas Técnicas

### Criação e Mapeamento do Prefixo Wine Dedicado
**Ação**: Definição explícita do caminho do prefixo (ex.: /home/ferreira/Games/wolverine-prefix) e arquitetura de 64 bits nas opções do jogo.

**Explicação**: Fornece a estrutura de arquivos e chaves de registro do Windows isoladas para a aplicação, permitindo a persistência de configurações, saves e instalação de bibliotecas sem poluir outros jogos.

### Instalação das Dependências do Sistema via Winetricks
**Ação**: Instalação manual dos componentes: physx (NVIDIA/Ageia PhysX Legacy Software)d3dx9, d3dcompiler_43, d3dcompiler_47, vcrun2005, vcrun2008, vcrun2010

**Explicação**: O X-Men Origins: Wolverine utiliza intensamente efeitos de desmembramento e regeneração via PhysX. Sem o runtime instalado e registrado no Wine, a inicialização é bloqueada de imediato por falta de bibliotecas como PhysXLoader.dll.

As bibliotecas DirectX 9 / D3DCompiler garantem que as chamadas gráficas da Unreal Engine 3 sejam traduzidas corretamente para a API Vulkan via DXVK/D9VK. Os runtimes Visual C++ contêm as rotinas básicas de C/C++ requeridas pelo código compilado do jogo.

### Ajuste do Runner para lutris-GE-Proton-11.3
**Ação**: Configuração da versão do Wine para um runner otimizado (lutris-GE-Proton) que opera sem encapsulamento forçado em containers legados incompatíveis.

**Explicação**: Versões mantidas pelo projeto Lutris com patches GloriousEggroll (GE) trazem correções nativas de sincronização (Fsync/Esync/Nsync), gerenciamento de threads de áudio e compatibilidade estendida para jogos legados de 32/64 bits rodando sob o Wayland e drivers AMDGPU modernos.