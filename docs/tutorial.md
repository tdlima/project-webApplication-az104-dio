# ☁️ Tutorial Completo: Implantação de Arquitetura com Máquinas Virtuais, Application Gateway e WAF no Azure

Este guia ensina, passo a passo, como criar uma infraestrutura no Microsoft Azure composta por:

- Máquinas Virtuais Linux em 3 Zonas de Disponibilidade
- Application Gateway com WAF (Web Application Firewall)
- Rede Virtual e Sub-rede
- Armazenamento com discos gerenciados
- Escalabilidade horizontal

---

## 📌 1. Criar Grupo de Recursos

1. Acesse o [Portal do Azure](https://portal.azure.com)
2. No menu lateral esquerdo, clique em **"Grupos de recursos"**
3. Clique em **"Criar"**
4. Preencha os campos:
   - **Assinatura**: Selecione sua assinatura
   - **Nome do grupo de recursos**: `rg-webApplication-prod`
   - **Região**: `East US`
5. Clique em **"Revisar + criar"** e depois em **"Criar"**

---

## 🌐 2. Criar Rede Virtual (VNet) com Sub-redes

1. No menu superior, pesquise por **"Redes virtuais"** e clique em **"Criar"**
2. Selecione:
   - **Assinatura**: Sua assinatura
   - **Grupo de recursos**: `rg-webApplication-prod`
   - **Nome da VNet**: `vnet-web-prod`
   - **Região**: `East US`
3. Em **Endereçamento IP**, configure:
   - **Espaço de endereçamento**: `10.0.0.0/16`
   - **Sub-rede**:
     - Nome: `subnet-web`
     - Prefixo: `10.0.1.0/24`
4. Clique em **"Revisar + criar"** e depois em **"Criar"**

---

## 🖥 3. Criar Máquinas Virtuais (3 Zonas de Disponibilidade)

### Criar a primeira VM (Zone 1)

1. Acesse **"Máquinas virtuais" > Criar**
2. Aba **"Básico"**:
   - **Grupo de recursos**: `rg-webApplication-prod`
   - **Nome da VM**: `vm-web-01`
   - **Região**: `East US`
   - **Zona de disponibilidade**: `1`
   - **Imagem**: Ubuntu 22.04 LTS
   - **Tamanho**: Standard B2s
   - **Autenticação**: Chave SSH ou Senha
3. Aba **"Discos"**:
   - Tipo de disco: Premium SSD
4. Aba **"Rede"**:
   - VNet: `vnet-web-prod`
   - Sub-rede: `subnet-web`
   - IP Público: **Nenhum**
5. Clique em **"Revisar + criar"** e **"Criar"**

### Repita o processo para as outras duas VMs:

- `vm-web-02` – Zona 2
- `vm-web-03` – Zona 3

---

## 🧱 4. Criar Sub-rede para o Application Gateway

1. Acesse **"Redes virtuais" > `vnet-web-prod` > Sub-redes > + Sub-rede**
2. Nome: `subnet-agw`
3. Prefixo: `10.0.2.0/24`
4. Clique em **"Salvar"**

---

## 🛡 5. Criar Application Gateway com WAF

1. Pesquise por **"Application Gateway"** e clique em **"Criar"**
2. Aba **"Básico"**:
   - Nome: `agw-web-prod`
   - Região: `East US`
   - Tier: **WAF V2**
   - Zonas: Marque **1, 2 e 3**
   - Grupo de recursos: `rg-webApplication-prod`
3. Aba **"Frontends"**:
   - Tipo: IP Público
   - Criar novo IP público: `pip-agw-web`
4. Aba **"Backends"**:
   - Criar novo backend pool: `backend-vms`
   - Adicionar os **endereços IP privados** das VMs criadas (`vm-web-01`, `02`, `03`)
5. Aba **"Configuração de regras"**:
   - Criar regra de roteamento HTTP na porta 80
   - Path-based routing: Desativado
6. Aba **"WAF"**:
   - WAF Ativo
   - Modo: **Prevenção**
   - Policy: Usar padrão
7. Clique em **"Revisar + criar"** e depois **"Criar"**

---

## 📊 6. Configurar Escalabilidade Horizontal (opcional com VMSS)

> Se desejar usar um VM Scale Set ao invés de VMs separadas, siga:

1. Acesse **"Conjuntos de dimensionamento de máquinas virtuais"**
2. Clique em **"Criar"**
3. Configure:
   - Nome: `vmss-web-prod`
   - Região: `East US`
   - Zonas: 1, 2, 3
   - Imagem: Ubuntu 22.04 LTS
   - Instâncias: Mín 2 / Máx 6
   - VNet/Sub-rede: `vnet-web-prod` / `subnet-web`
4. Configure **escalonamento automático** com base em CPU > 70% por 10 minutos

---
