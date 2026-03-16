# Introdução à Virtualização — Resumo da Aula

## O que é Virtualização
Virtualização é uma tecnologia que permite executar **vários sistemas operacionais ao mesmo tempo em um único computador físico**. Isso é feito criando ambientes isolados que simulam hardware real, permitindo rodar diferentes sistemas sem interferir no sistema principal. :contentReference[oaicite:0]{index=0}

Essa técnica é muito utilizada em:
- Laboratórios de informática  
- Desenvolvimento de software  
- Testes de sistemas  
- Ambientes de produção

---

## Vantagens da Virtualização

**Economia de hardware**  
Permite executar vários servidores ou sistemas em uma única máquina física, reduzindo custos.

**Ambientes isolados**  
Cada sistema roda separado dos outros, evitando que erros ou falhas afetem o sistema principal.

**Facilidade para testes**  
É possível criar e restaurar configurações rapidamente usando snapshots.

**Execução de múltiplos sistemas**  
Permite rodar diferentes sistemas operacionais ao mesmo tempo, como Linux e Windows.

---

## Máquina Virtual

Uma **máquina virtual (VM)** é um computador simulado dentro de outro computador.

Ela possui três componentes principais:

- **Host (Sistema Hospedeiro)**  
  Sistema operacional principal da máquina física.

- **Camada de Virtualização**  
  Software responsável por simular o hardware.

- **Guest (Sistema Convidado)**  
  Sistema operacional instalado dentro da máquina virtual.

---

## Oracle VirtualBox

O **VirtualBox** é um software de virtualização utilizado para criar e gerenciar máquinas virtuais.

Características:
- Desenvolvido pela Oracle  
- Gratuito para uso educacional e pessoal  
- Código aberto  
- Funciona em Windows, Linux, macOS e Solaris  
- Muito utilizado em ambientes acadêmicos e de testes

---

## Interface do VirtualBox

Principais áreas da interface:

- **Painel Principal** – lista das máquinas virtuais criadas  
- **Configurações** – ajustes de CPU, memória, disco e dispositivos  
- **Armazenamento** – gerenciamento de discos virtuais e arquivos ISO  
- **Rede** – configuração de conexão e adaptadores de rede

---

## Criando uma Máquina Virtual

Passos básicos:

1. Criar uma nova VM no VirtualBox
2. Escolher o tipo e versão do sistema operacional
3. Definir a quantidade de memória RAM (recomendado: 2 GB ou mais)
4. Criar um disco virtual (normalmente entre 20 e 40 GB)

---

## Instalando um Sistema Operacional

Etapas:

1. **Baixar a ISO** do sistema operacional
2. **Montar a ISO** no armazenamento da VM
3. **Iniciar a máquina virtual**
4. **Seguir o processo normal de instalação do sistema**

---

## Exemplo de Sistema Leve

**Tiny Core Linux**

Características:
- Distribuição Linux extremamente leve
- ISO entre 17 MB e 248 MB
- Ideal para testes e virtualização
- Sistema modular e personalizável
- Baixo consumo de recursos

---

## Atividade da Aula

1. Instalar o VirtualBox  
2. Criar uma máquina virtual  
3. Instalar um Linux leve (Tiny Core, Lubuntu ou Xubuntu)  
4. Testar o sistema virtualizado  
5. Documentar todo o processo em forma de **manual** e salvar no repositório da disciplina

---

## Conclusão

A virtualização é uma tecnologia essencial na computação moderna, pois permite **testar sistemas, economizar recursos de hardware e criar ambientes isolados** de forma prática e segura.
