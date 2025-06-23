# ☁️ Azure - Infraestrutura Web

Este projeto descreve a criação de maquinas virtuais para a implantação de uma aplicação web na nuvem Azure, com foco em **alta disponibilidade**, **escalabilidade** e **segurança**.

## 📋 Requisitos

- Alta disponibilidade
- Escalabilidade
- Armazenamento otimizado
- Segurança
- Documentação clara e estruturada

## 🔧 Recursos Criados

- Grupo de Recursos: `rg-webApplication-prod`
- Rede Virtual: `vnet-webApplication-prod`
- Subnet: `subnet-web`, `subnet-agw`
- 3 VMs em zonas diferentes (Ubuntu)
- Application Gateway com WAF (modo preventivo)
- VMSS com escalonamento horizontal
- Armazenamento Premium SSD
- Sem IP público nas VMs

## 🧰 Tecnologias

- Azure Virtual Machines
- Azure VNet
- Application Gateway + WAF
- Availability Zones
- VM Scale Sets

## Visão Geral

A arquitetura foi projetada para atender aos requisitos de alta disponibilidade, escalabilidade e segurança, usando os seguintes componentes principais:

| Componente | Função |
|-----------|--------|
| Grupo de Recursos | Agrupa todos os recursos sob `rg-webApplication-prod` |
| Rede Virtual | Conecta todas as máquinas e serviços internos |
| VMs Ubuntu | Hospedam a aplicação web |
| Application Gateway | Balanceador de carga com WAF |
| VMSS | Escala automática das VMs |
| Availability Zones | Garante alta disponibilidade |

## 📈 Escalonamento

O Azure VMSS aumenta ou reduz a quantidade de VMs com base no uso de CPU (>= 70%).

## Como Implementar

Veja o passo a passo completo na pasta `/docs/tutorial.md`.

## 📦 Repositório

Este projeto está no GitHub:
```bash
gh repo clone tdlima/project-webApplication-az104-dio
```

## 📁 Estrutura do Repositório

```bash
azure-cloud-architecture/
│
├── README.md                     ← Descrição geral do projeto
├── docs/
│   ├── tutorial.md               ← Passo a passo completo da implantação
│   ├── architecture.md           ← Detalhes da arquitetura
│   └── best-practices.md         ← Boas práticas e dicas extras
│
├── images/
│   └── architecture-diagram.png  ← Diagrama visual da arquitetura (gerado)
│
└── scripts/
    └── deploy.ps1                ← Exemplo de script PowerShell para criação de recursos
```

## 📚 Documentação Oficial

- [Máquinas Virtuais no Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/)
- [Web Application Firewall (WAF) no Application Gateway](https://learn.microsoft.com/en-us/azure/web-application-firewall/ag/ag-overview)
- [Conjuntos de Dimensionamento de Máquinas Virtuais](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/)
