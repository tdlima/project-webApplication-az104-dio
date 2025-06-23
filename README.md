# ☁️ Azure - Infraestrutura Contoso Web

Este projeto descreve a criação de maquinas virtuais para a implantação de uma aplicação web na nuvem Azure, com foco em **alta disponibilidade**, **escalabilidade** e **segurança**.

## 📋 Requisitos

- Alta disponibilidade (Availability Zones)
- Escalabilidade horizontal (VMSS)
- Armazenamento otimizado (SSD Premium)
- Segurança (WAF, RBAC, Policy)
- Documentação clara e estruturada

## 🔧 Recursos Criados

- Grupo de Recursos: `rg-webApplication-prd`
- Rede Virtual: `vnet-webApplication-prd`
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

![Arquitetura Azure](../images/architecture-diagram.png)

A arquitetura foi projetada para atender aos requisitos de alta disponibilidade, escalabilidade e segurança, usando os seguintes componentes principais:

| Componente | Função |
|-----------|--------|
| Grupo de Recursos | Agrupa todos os recursos sob `rg-varejoonline-prod` |
| Rede Virtual | Conecta todas as máquinas e serviços internos |
| VMs Ubuntu | Hospedam a aplicação web |
| Application Gateway | Balanceador de carga com WAF |
| VMSS | Escala automática das VMs |
| Availability Zones | Garante alta disponibilidade |

## 📈 Escalonamento

O Azure VMSS aumenta ou reduz a quantidade de VMs com base no uso de CPU (>= 70%).

## 🛡 Segurança

- IPs públicos desativados
- Application Gateway com WAF
- RBAC e Policies aplicadas

## Como Implementar

Veja o passo a passo completo na pasta `/docs/tutorial.md`.

## 📦 Repositório

Este projeto está no GitHub:
```bash
gh repo clone tdlima/project-webApplication-az104-dio
```

## 📚 Documentação Oficial

- [Máquinas Virtuais no Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/)
- [Web Application Firewall (WAF) no Application Gateway](https://learn.microsoft.com/en-us/azure/web-application-firewall/ag/ag-overview)
- [Conjuntos de Dimensionamento de Máquinas Virtuais](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/)
