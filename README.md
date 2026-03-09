# OCI Network Infrastructure with Terraform

![Terraform](https://img.shields.io/badge/Terraform-%3E%3D1.5-blue)
![OCI](https://img.shields.io/badge/Oracle-Cloud-red)
![IaC](https://img.shields.io/badge/Infrastructure-as%20Code-green)

Este repositorio implementa **Infraestructura como Código (IaC)** para desplegar una **arquitectura de red en Oracle Cloud Infrastructure (OCI)** utilizando **Terraform**.

La infraestructura está organizada utilizando **arquitectura modular**, permitiendo reutilización, mantenimiento sencillo y escalabilidad.

---

# Arquitectura

```
                Internet
                    │
            ┌───────────────┐
            │ Internet GW   │
            └───────┬───────┘
                    │
              ┌─────────┐
              │   VCN   │
              │10.0.0.0/16
              └───┬─────┘
                  │
        ┌─────────┴─────────┐
        │                   │
   Public Subnet       Private Subnet
   10.0.1.0/24         10.0.2.0/24
        │                   │
   Route Table         Route Table
        │                   │
   Internet GW           NAT GW
```

---

# Estructura del Proyecto

```
oci-network
│
├── main.tf
├── provider.tf
├── variables.tf
├── terraform.tfvars
├── outputs.tf
├── versions.tf
├── .gitignore
│
└── modules
    └── network
        ├── vcn.tf
        ├── subnets.tf
        ├── gateways.tf
        ├── routes.tf
        ├── nsg.tf
        ├── variables.tf
        └── outputs.tf
```

---

# Descripción de Archivos

## Root Module

| Archivo | Descripción |
|------|------|
| main.tf | Llama al módulo `network` |
| provider.tf | Configuración del provider OCI |
| variables.tf | Variables utilizadas por el proyecto |
| terraform.tfvars | Valores de variables |
| outputs.tf | Outputs expuestos |
| versions.tf | Versiones de Terraform y provider |

---

# Módulo Network

Ubicación:

```
modules/network
```

Este módulo contiene todos los recursos de red.

| Archivo | Descripción |
|------|------|
| vcn.tf | Crea la Virtual Cloud Network |
| subnets.tf | Define subredes |
| gateways.tf | Internet Gateway / NAT Gateway / Service Gateway |
| routes.tf | Route Tables |
| nsg.tf | Network Security Groups |
| variables.tf | Variables del módulo |
| outputs.tf | Outputs del módulo |

---

# Variables Principales

| Variable | Descripción | Ejemplo |
|------|------|------|
| compartment_id | OCID del compartment | ocid1.compartment... |
| vcn_cidr | CIDR de la VCN | 10.0.0.0/16 |
| public_subnet_cidr | CIDR subnet pública | 10.0.1.0/24 |
| private_subnet_cidr | CIDR subnet privada | 10.0.2.0/24 |
| region | Región OCI | us-ashburn-1 |

---

# Outputs

| Output | Descripción |
|------|------|
| vcn_id | ID de la VCN |
| public_subnet_id | ID de la subnet pública |
| private_subnet_id | ID de la subnet privada |
| internet_gateway_id | ID del Internet Gateway |

---

# Ejemplo terraform.tfvars

```
compartment_id = "ocid1.compartment.oc1..xxxxx"

region = "us-ashburn-1"

vcn_cidr = "10.0.0.0/16"

public_subnet_cidr = "10.0.1.0/24"

private_subnet_cidr = "10.0.2.0/24"
```

---

# Requisitos

- Terraform >= 1.5
- Cuenta en Oracle Cloud Infrastructure
- Credenciales OCI configuradas

---

# Inicializar Terraform

```bash
terraform init
```

---

# Validar Configuración

```bash
terraform validate
```

---

# Ver Plan

```bash
terraform plan
```

---

# Aplicar Infraestructura

```bash
terraform apply
```

---

# Destruir Infraestructura

```bash
terraform destroy
```

---

# Buenas Prácticas

Este proyecto implementa:

- Arquitectura modular
- Separación de recursos por tipo
- Variables reutilizables
- Outputs para integración con otros módulos
- Versionado de Terraform

---

# Archivos Ignorados

```
.terraform/
terraform.tfstate
terraform.tfstate.backup
*.tfstate
*.tfstate.*
```

Estos archivos contienen el **estado local de Terraform** y no deben subirse al repositorio.

---

# Mejoras Futuras

- Remote Backend con OCI Object Storage
- Separación por ambientes (`dev`, `qa`, `prod`)
- Integración CI/CD
- Naming convention estandarizado
- Automatización de seguridad

---

# Autor

Infraestructura desarrollada utilizando **Terraform + Oracle Cloud Infrastructure**.
