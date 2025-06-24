
## 🔐 Boas Práticas de Segurança

- Nas VMs, use apenas IPs internos
- Habilitar backup das VMs
- Crie grupos de segurança (NSG) para permitir apenas as portas necessárias (80)
- Monitore com Azure Monitor e Log Analytics
- Use Tags:
  - `env=prod`
  - `owner=infra`
  - `project=ecommerce-web`

---

## Configurações de Segurança (RBAC e Policy)  

### ** RBAC: **  

   - Crie funções personalizadas para administradores, desenvolvedores e auditores.
   - Exemplo: função “Leitor de Máquinas” com permissão somente de visualização.
     

### ** Policy: **  

    - Use Azure Policy para impor regras como:
    - Somente discos SSD podem ser criados
    - Nomes de recursos devem seguir padrão (<tipo>-<nome>)
    - Máquinas só podem estar em Availability Zones
         
---     

> 📌 **Dica final:** Use Azure Resource Locks para proteger os recursos contra exclusão acidental.

---
