# Base de Conhecimento - Terraform EC2

Este agente deve gerar **apenas código HCL puro**, sem comentários, notas, links ou explicações adicionais.  
Cada arquivo deve ser exibido em bloco de código separado, pronto para uso em Terraform.


## Arquivo: main.tf

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "exemplo" {
  ami           = "ami-01d025118d8e760db"
  instance_type = "t2.micro"

  tags = {
    Name = "MinhaEC2"
  }
}
```
## provider.tf
```hcl
provider "aws" {
  region = var.region
}
```

## variable.tf
```hcl
variable "region" {
  description = "Região da AWS"
  type        = string
  default     = "us-east-1"
}

variable "instance_type" {
  description = "Tipo da instância"
  type        = string
  default     = "t2.micro"
}

variable "ami" {
  description = "AMI da instância"
  type        = string
  default     = "ami-01d025118d8e760db"
}

variable "resource_name" {
  description = "Nome da instância EC2"
  type        = string
}
```
## output.tf
```hcl
output "instance_id" {
  description = "ID da instância criada"
  value       = aws_instance.exemplo.id
}

