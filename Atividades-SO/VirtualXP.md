# Instalação do Windows XP no Oracle VM VirtualBox

Este guia descreve, de forma estruturada, o processo de instalação do Windows XP em uma máquina virtual utilizando o Oracle VM VirtualBox.

---

## 1. Pré-requisitos

Antes de iniciar, certifique-se de possuir:

- O software de virtualização :contentReference[oaicite:0]{index=0} instalado
- Um arquivo ISO do sistema operacional :contentReference[oaicite:1]{index=1}

---

## 2. Criação da Máquina Virtual

1. Abra o VirtualBox
2. Clique em **“Novo”**
3. Configure:
   - **Nome:** Windows XP
   - **Tipo:** Microsoft Windows
   - **Versão:** Windows XP (32-bit)

---

## 3. Configuração de Memória (RAM)

- Defina entre **512 MB e 1024 MB** de memória RAM  
- Essa quantidade é suficiente para o funcionamento estável do sistema

---

## 4. Criação do Disco Rígido Virtual

1. Selecione **Criar disco rígido virtual agora**
2. Escolha:
   - **Tipo:** VDI (VirtualBox Disk Image)
   - **Alocação:** Dinamicamente alocado
   - **Tamanho:** mínimo de 10 GB

---

## 5. Inserção do Arquivo ISO

1. Acesse **Configurações** da máquina virtual
2. Vá até a aba **Armazenamento**
3. Clique no ícone de CD vazio
4. Selecione o arquivo ISO do Windows XP

---

## 6. Inicialização da Máquina Virtual

- Clique em **Iniciar**
- O instalador do Windows XP será carregado automaticamente

---

## 7. Processo de Instalação

Durante a instalação:

1. Pressione **Enter** para iniciar
2. Aceite os termos de licença (**F8**)
3. Selecione o disco virtual criado
4. Escolha o sistema de arquivos:
   - Recomendado: **NTFS**
5. Aguarde a cópia de arquivos e reinicialização automática

---

## 8. Configuração Inicial do Sistema

Após reiniciar, configure:

- Idioma e região
- Nome do usuário
- Chave do produto (se necessário)
- Configurações de rede

---

## 9. Primeiro Acesso ao Sistema

- Após a conclusão, o Windows XP será inicializado
- O ambiente gráfico estará disponível para uso

---

## 10. Instalação do Guest Additions (Opcional)

Para melhorar a experiência:

1. No menu do VirtualBox, clique em:
   - **Dispositivos → Inserir imagem de CD dos Adicionais para Convidado**
2. Execute o instalador dentro da máquina virtual

### Benefícios:

- Melhor resolução de tela
- Integração do mouse
- Melhor desempenho geral

---

## Considerações Finais

A virtualização do Windows XP permite executar aplicações legadas em ambientes modernos, mantendo isolamento e segurança. Recomenda-se evitar conexão com a internet para reduzir riscos, devido à descontinuação de suporte do sistema.
