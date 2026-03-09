# Resumo – Estrutura e Arquitetura de Sistemas Operacionais

Esta aula apresenta os principais conceitos relacionados à estrutura e arquitetura de um sistema operacional, explicando como ele organiza e controla os recursos de um computador.

## Componentes do Sistema Operacional

Um sistema operacional é composto por diferentes partes responsáveis por gerenciar o funcionamento do computador. Entre os principais componentes estão:

- **Kernel:** núcleo do sistema responsável por controlar recursos essenciais.
- **Gerenciamento de processos:** controla a execução de programas.
- **Gerenciamento de memória:** organiza e protege o uso da memória.
- **Sistema de arquivos:** organiza e armazena dados em diretórios.
- **Entrada e saída (I/O):** permite a comunicação com dispositivos externos.
- **Drivers de dispositivos:** módulos que permitem ao sistema operacional interagir com hardware específico.

O sistema operacional atua como intermediário entre o **hardware** (CPU, memória e dispositivos físicos) e as **aplicações** utilizadas pelo usuário.

## Kernel: o núcleo do sistema

O **kernel** é a parte central do sistema operacional. Ele é responsável por:

- gerenciar processos e threads
- controlar memória física e virtual
- gerenciar dispositivos e periféricos
- garantir comunicação entre hardware e software
- manter a segurança e proteção do sistema

## Modos de Execução

Os sistemas operacionais utilizam diferentes modos de execução para garantir segurança e estabilidade:

- **Modo Usuário:** onde os programas e aplicações são executados com acesso limitado ao hardware.
- **System Call:** mecanismo usado pelas aplicações para solicitar serviços do sistema operacional.
- **Modo Kernel:** onde o sistema operacional executa operações críticas com acesso total aos recursos do hardware.

Essa separação impede que erros ou programas maliciosos comprometam todo o sistema.

## Processos

Um **processo** é um programa em execução. Cada processo possui seu próprio espaço de memória e recursos atribuídos pelo sistema operacional.

Os principais componentes de um processo incluem:

- código executável
- dados do programa
- pilha de execução (stack)
- registradores do processador
- arquivos abertos e outros recursos

## Sistema de Arquivos

O sistema de arquivos organiza os dados armazenados em dispositivos de armazenamento em uma **estrutura hierárquica de diretórios**, facilitando a localização e o gerenciamento das informações.

## Entrada, Saída e Drivers

Os sistemas operacionais precisam se comunicar com diversos dispositivos de hardware. Isso é feito por meio de **drivers**, que funcionam como intermediários entre o sistema e o dispositivo.

Exemplos de dispositivos controlados pelo sistema operacional:

- teclado
- mouse
- discos de armazenamento
- rede
- impressoras

Os drivers abstraem as diferenças entre dispositivos, permitindo que o sistema operacional controle diferentes tipos de hardware.

## Reaproveitamento de Estrutura de Sistemas Operacionais

Muitos dispositivos não criam um sistema operacional totalmente novo. Em vez disso, utilizam **sistemas existentes como base**, adaptando-os ao hardware específico.

Entre as vantagens dessa abordagem estão:

- redução de custos de desenvolvimento
- maior estabilidade e segurança
- reutilização de tecnologias já testadas
- suporte e atualizações contínuas

Exemplos apresentados:

- **Raspberry Pi OS**, baseado no **Debian (Linux)**.
- **Orbis OS**, utilizado no **PlayStation 4**, baseado no **FreeBSD**.

## Conclusão

Os sistemas operacionais possuem uma estrutura organizada que permite controlar hardware, executar programas e garantir segurança e estabilidade. Além disso, muitos sistemas modernos são desenvolvidos a partir de sistemas existentes, aproveitando suas estruturas e tecnologias para criar soluções adaptadas a dispositivos específicos.
