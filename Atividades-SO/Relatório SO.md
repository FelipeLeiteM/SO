## 1. Introdução

A DevStore é uma startup de desenvolvimento de sites que enfrenta desafios críticos de escalabilidade, organização e segurança em sua infraestrutura de TI. Atualmente, a empresa opera com servidores locais sem padronização, o que dificulta o gerenciamento eficiente dos sistemas e compromete o crescimento sustentável do negócio. Além disso, o pipeline de desenvolvimento ocorre diretamente nas máquinas dos desenvolvedores, sem versionamento de código ou ambientes de testes formalizados.

---

## 2. Diagnóstico dos Problemas Atuais

| Problema | Impacto |
|---|---|
| Servidores locais sem padronização | Dificuldade de gerenciamento e replicação de ambientes |
| Desenvolvimento direto na máquina local | Risco de inconsistências entre ambientes dev/produção |
| Ausência de testes automatizados | Alta chance de bugs chegarem à produção |
| Falta de versionamento de código | Impossibilidade de rastrear mudanças e reverter falhas |
| Sem escalabilidade | Incapacidade de atender crescimento da demanda |
| Segurança não formalizada | Vulnerabilidades e riscos de violação de dados |

---

## 3. Arquitetura Proposta

A solução é organizada em quatro camadas complementares:

```
[ Máquina do Desenvolvedor ]
         ↓  Git + Docker (ambiente local padronizado)
[ Ambiente de Testes — VMs Isoladas ]
         ↓  Pipeline CI/CD (testes automatizados)
[ Ambiente de Homologação — Containers Docker ]
         ↓  Deploy automatizado
[ Produção — Nuvem AWS ]
```

### 3.1 Ambientes

**Desenvolvimento (Local)**  
Cada desenvolvedor trabalhará com um container Docker local, garantindo que o ambiente seja idêntico ao de produção. O código será versionado via Git com branches para cada funcionalidade.

**Testes (Virtualizado)**  
Máquinas virtuais (VMs) isoladas serão provisionadas para execução de testes de integração e segurança. O isolamento total das VMs protege o ambiente de produção de eventuais falhas durante os testes.

**Homologação (Containerizado)**  
Ambiente em containers Docker, espelhando a produção, onde a equipe valida as entregas antes do deploy final.

**Produção (Nuvem — AWS)**  
Hospedagem das aplicações na AWS, com alta disponibilidade, escalabilidade automática e redundância geográfica.

---

## 4. Planejamento de Virtualização

### 4.1 Finalidade

As máquinas virtuais serão utilizadas exclusivamente para ambientes de testes isolados, onde é necessário simular configurações de sistema operacional distintas (ex: diferentes versões de Linux ou Windows Server) sem impacto nos demais ambientes.

### 4.2 Tecnologia Sugerida

- **Hypervisor:** VirtualBox (desenvolvimento local) ou VMware ESXi (ambiente corporativo)
- **Sistema Operacional Guest:** Ubuntu Server 22.04 LTS

### 4.3 Configuração das VMs de Teste

| Parâmetro | Valor Recomendado |
|---|---|
| vCPUs | 2 |
| Memória RAM | 2 GB |
| Armazenamento | 20 GB (disco dinâmico) |
| Rede | NAT ou Host-Only (isolada) |
| Snapshot | Habilitado (antes de cada ciclo de testes) |

### 4.4 Controle de Consumo de Recursos

- Limitar CPUs e RAM via configuração do hypervisor por VM
- Monitorar uso com ferramentas como `htop`, `vmstat` e relatórios do hypervisor
- Desligar VMs automaticamente após conclusão dos testes (scripts de automação)

---

## 5. Planejamento de Containerização com Docker

### 5.1 Justificativa

A containerização oferece melhor desempenho e menor consumo de recursos em comparação com máquinas virtuais, sendo mais adequada para os ambientes de homologação e produção da DevStore. O Docker garante portabilidade e padronização dos ambientes.

### 5.2 Estrutura de Containers

```
devstore/
├── docker-compose.yml
├── services/
│   ├── frontend/          # Aplicação web (Node.js / React)
│   │   └── Dockerfile
│   ├── backend/           # API (ex: Node.js / Python)
│   │   └── Dockerfile
│   └── database/          # Banco de dados (PostgreSQL)
│       └── Dockerfile
└── nginx/                 # Proxy reverso
    └── Dockerfile
```

### 5.3 Controle de Recursos dos Containers

- Utilizar `--cpus` e `--memory` para limitar recursos por container
- Monitorar com `docker stats` em tempo real
- Integrar com Prometheus + Grafana para dashboards de métricas

---

## 6. Computação em Nuvem — AWS

### 6.1 Serviços AWS Propostos

| Serviço | Finalidade |
|---|---|
| **EC2** | Instâncias de servidores para hospedar os containers |
| **ECS / EKS** | Orquestração de containers em produção |
| **RDS** | Banco de dados gerenciado (PostgreSQL) |
| **S3** | Armazenamento de arquivos estáticos e backups |
| **CloudFront** | CDN para entrega rápida de conteúdo |
| **VPC** | Rede privada isolada para os serviços |
| **IAM** | Controle de acesso e permissões |
| **CloudWatch** | Monitoramento e alertas |
| **Auto Scaling** | Escalabilidade automática conforme demanda |

### 6.2 Configuração de Rede (VPC)

```
VPC: 10.0.0.0/16
├── Sub-rede Pública: 10.0.1.0/24   (load balancer, CloudFront)
├── Sub-rede Privada: 10.0.2.0/24   (servidores de aplicação)
└── Sub-rede de Dados: 10.0.3.0/24  (banco de dados RDS)
```

- **Security Groups:** regras de firewall por camada (web, app, banco)
- **NAT Gateway:** permite que sub-redes privadas acessem a internet sem exposição direta

### 6.3 Armazenamento

- **EBS:** volumes persistentes para as instâncias EC2
- **S3:** backups automáticos diários e armazenamento de assets
- **RDS Multi-AZ:** banco de dados com replicação em múltiplas zonas de disponibilidade

---

## 7. Segurança

### 7.1 Controle de Acesso

- Criação de grupos de usuários no **AWS IAM** com permissões mínimas necessárias (princípio do menor privilégio)
- Autenticação com MFA (Multi-Factor Authentication) para todos os usuários com acesso à console AWS
- Chaves SSH para acesso às instâncias EC2 (senhas desabilitadas)

### 7.2 Firewall e Redes

- **Security Groups AWS:** liberar apenas as portas necessárias (80, 443 para web; 5432 restrito à sub-rede privada para banco)
- **Network ACLs:** camada adicional de controle no nível de sub-rede
- Uso de HTTPS em todos os endpoints com certificado SSL via **AWS Certificate Manager**

### 7.3 Monitoramento Contínuo

- **AWS CloudWatch:** alertas de uso de CPU, memória, erros e latência
- **AWS CloudTrail:** auditoria completa de todas as ações realizadas na conta AWS
- **Logs centralizados:** agregação de logs de aplicação no CloudWatch Logs

---

## 8. Pipeline de Desenvolvimento Otimizado

```
Desenvolvedor → Git Push
      ↓
GitHub/GitLab (versionamento)
      ↓
CI/CD Pipeline (GitHub Actions / GitLab CI)
      ↓
Testes Automatizados (ambiente VM isolado)
      ↓
Build da imagem Docker
      ↓
Push para registro de imagens (ECR - AWS)
      ↓
Deploy em Homologação (containers)
      ↓
Aprovação Manual
      ↓
Deploy em Produção (AWS ECS/EKS)
```

**Ferramentas recomendadas:**
- Versionamento: Git + GitHub ou GitLab
- CI/CD: GitHub Actions ou GitLab CI
- Registro de imagens: Amazon ECR
- Orquestração: AWS ECS (Fargate) para início; migrar para EKS conforme escala

---

## 9. Papel do Sistema Operacional em Cada Camada

| Camada | Sistema Operacional | Papel |
|---|---|---|
| **Local (Dev)** | Ubuntu 22.04 / macOS / Windows + WSL2 | Hospeda o Docker Desktop e ferramentas de desenvolvimento |
| **VMs de Teste** | Ubuntu Server 22.04 LTS | Ambiente isolado para testes; o SO garante separação total de recursos |
| **Containers** | Linux (kernel compartilhado via Docker) | O SO do host é compartilhado entre containers; namespaces e cgroups garantem isolamento |
| **Nuvem (AWS EC2)** | Amazon Linux 2023 / Ubuntu Server | Gerencia recursos físicos, processos, rede e armazenamento das instâncias |

O sistema operacional é fundamental em todas as camadas: gerencia processos, memória, sistema de arquivos, rede e segurança — sendo a base sobre a qual virtualização, containers e serviços em nuvem operam.

---

## 10. Estratégias de Implantação, Manutenção e Expansão

### Implantação

1. Configurar repositório Git e definir política de branches (main, develop, feature/*)
2. Criar Dockerfiles e docker-compose para todos os serviços
3. Configurar pipeline CI/CD com testes automatizados
4. Provisionar infraestrutura AWS (VPC, EC2, RDS, S3)
5. Realizar deploy inicial com acompanhamento manual

### Manutenção

- Atualização de imagens Docker mensalmente (patches de segurança)
- Revisão de Security Groups e políticas IAM trimestralmente
- Backups diários automáticos no S3 com retenção de 30 dias
- Revisão de alertas do CloudWatch semanalmente
- Testes de recuperação de desastres semestralmente

### Expansão

- Ativar **Auto Scaling** no ECS para lidar com picos de demanda
- Migrar para **Kubernetes (EKS)** quando o número de microserviços justificar
- Adotar **Infrastructure as Code** com Terraform para replicar ambientes com agilidade
- Implementar **CDN (CloudFront)** para atender clientes internacionais com baixa latência
- Considerar **multi-região AWS** para alta disponibilidade geográfica quando necessário

---

## 11. Justificativas das Escolhas Técnicas

| Decisão | Justificativa |
|---|---|
| **Docker** em vez de apenas VMs | Menor consumo de recursos, portabilidade e rapidez de deployment |
| **VMs para testes** | Isolamento total necessário para testes que podem comprometer o SO |
| **AWS** como provedor cloud | Ampla documentação, serviços gerenciados robustos e escalabilidade comprovada |
| **Ubuntu Server** nas VMs | Estabilidade, suporte LTS, excelente compatibilidade com Docker e vasto ecossistema |
| **PostgreSQL** como banco | Open source, robusto, suportado pelo RDS e compatível com a stack proposta |
| **Git** para versionamento | Padrão da indústria, integração nativa com CI/CD e rastreabilidade completa |
| **Pipeline CI/CD** | Automatiza testes e reduz erros humanos no processo de entrega |

---

## 12. Conclusão

A arquitetura proposta para a DevStore combina virtualização, containerização e computação em nuvem de forma complementar, endereçando todos os desafios identificados: falta de padronização, ausência de testes, riscos de segurança e limitações de escalabilidade. A adoção gradual dessa infraestrutura — começando pela containerização local e evoluindo para a nuvem — permite que a empresa cresça de forma sustentável, com controle de custos e alta disponibilidade dos serviços.

---
