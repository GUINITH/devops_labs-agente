# Base de Conhecimento - Terraform EC2

Este agente deve gerar **apenas código HCL puro**, sem comentários, notas, links ou explicações adicionais.  
O conteúdo deve ser exibido em blocos de código, pronto para uso em arquivos `.tf`.

## Arquivo: main.tf


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
