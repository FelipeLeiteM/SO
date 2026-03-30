# Conceitos de Sistemas Operacionais

## Introdução
Sistemas operacionais fornecem abstrações que permitem gerenciar os recursos do computador.  
Principais conceitos:
- Processos
- Memória (espaço de endereçamento)
- Arquivos
- Entrada/Saída
- Proteção
- Shell

---

## Processos
- Um processo é um programa em execução.
- Possui memória própria, registradores e recursos.
- O sistema mantém uma **tabela de processos** com seu estado.

### Características
- Podem ser pausados e retomados (preservando estado)
- Podem criar outros processos (estrutura em árvore)
- Podem se comunicar (IPC)

### Outros conceitos
- **Multiprogramação**: vários processos compartilham a CPU
- **Sinais**: notificações do sistema ao processo
- **UID/GID**: identificam usuário e grupo

---

## Memória e Espaço de Endereçamento
- Cada processo possui seu próprio espaço de memória.
- Pode ser maior que a memória física graças à **memória virtual**.

### Tipos de sistemas
- Monoprogramação: um programa por vez
- Multiprogramação: vários programas simultaneamente

### Proteção
- Impede interferência entre processos
- Controlada por hardware e SO

---

## Arquivos
- Abstração para armazenamento de dados
- Organizados em **diretórios hierárquicos**

### Operações principais
- Criar, abrir, ler, escrever, fechar, remover

### Conceitos importantes
- Caminho absoluto e relativo
- Descritor de arquivo (identificador numérico)
- Montagem (integra dispositivos externos)
- Pipes (comunicação entre processos)

---

## Entrada/Saída (E/S)
- Controla dispositivos como teclado, monitor e disco
- Usa:
  - Código genérico (independente de dispositivo)
  - Drivers específicos

---

## Proteção
- Garante segurança do sistema e dados

### Permissões (Unix)
- Representadas por `rwx`
- Divididas em:
  - Usuário
  - Grupo
  - Outros

---

## Shell
- Interface entre usuário e sistema operacional
- Interpreta comandos

### Funções
- Executar programas
- Redirecionar entrada/saída
- Executar processos em segundo plano

---

## Evolução Tecnológica
- Conceitos antigos frequentemente retornam com novas formas
- Exemplos:
  - Memória aumentou drasticamente ao longo do tempo
  - Microprogramação → RISC → máquinas virtuais (como Java)
  - Sistemas de arquivos evoluíram de simples para hierárquicos

---

## Conclusão
Os sistemas operacionais se baseiam em conceitos fundamentais como:
- Processos
- Memória
- Arquivos
- Comunicação
- Proteção

Esses conceitos evoluem com o hardware, mas continuam sendo a base de qualquer sistema moderno.
