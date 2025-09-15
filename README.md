# azure-vm-terraform

Proyecto Terraform para aprovisionar una VM Linux en Azure.

## Requisitos
- Terraform >= 1.6
- Azure CLI (`az`) autenticado (`az login`)

## Estructura
- `versions.tf`: versiones de Terraform y provider.
- `providers.tf`: configuración del provider y variables sensibles.
- `variables.tf`: parámetros del despliegue.
- `main.tf`: recursos (RG, VNet, Subnet, NSG, IP, NIC, VM).
- `outputs.tf`: salidas útiles.

## Uso (un solo entorno)
1. Crea un archivo `dev.tfvars` con tus valores (no se necesita subscription_id porque está configurado en el provider):
   ```hcl
   admin_password  = "CambiaEstaPasswordSegura123!"
   location        = "eastus2"
   project_name    = "ingesoft"
   environment     = "dev"
   resource_group_name = "rg-ingesoft-dev"
   allowed_ssh_source_cidrs = ["0.0.0.0/0"]
   ```

2. Inicializa y valida:
   ```bash
   terraform init
   terraform validate
   ```

3. Planifica y aplica:
   ```bash
   terraform plan -var-file=dev.tfvars -input=false
   terraform apply -var-file=dev.tfvars -auto-approve -input=false
   ```

4. Salidas:
   ```bash
   terraform output
   ```

5. Destruir (opcional):
   ```bash
   terraform destroy -var-file=dev.tfvars -auto-approve -input=false
   ```

## Notas de seguridad
- La VM permite autenticación por contraseña para SSH (22). 

