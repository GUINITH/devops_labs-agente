# 🚀 Deploy de Arquivos Terraform via Copilot Studio + Power Automate + GitHub API

Este projeto mostra como automatizar o envio de arquivos Terraform (`provider.tf`, `variables.tf`, `main.tf`, `output.tf`, `terraform.tfvars`) para um repositório GitHub usando **Copilot Studio** e **Power Automate**, sem precisar rodar `git` manualmente.

---

## 🔑 1. Criar Personal Access Token (PAT) no GitHub
1. Vá em **Settings → Developer settings → Personal access tokens → Tokens (classic)**.  
2. Clique em **Generate new token**.  
3. Marque permissões: `repo` (para ler e escrever nos repositórios).  
4. Copie o token gerado (será usado no fluxo).

---

## ⚙️ 2. Configurar o Fluxo no Power Automate
1. Crie um fluxo com trigger **“Quando um agente chamar este fluxo”**.  
2. Defina os parâmetros de entrada:  
   - `fileName` → nome do arquivo (ex.: `provider.tf`).  
   - `fileContent` → conteúdo HCL gerado pelo Copilot Studio.  
3. Adicione uma ação **HTTP**:
   - Método: `PUT`  
   - URL:
     ```
     https://api.github.com/repos/SEU_USUARIO/SEU_REPOSITORIO/contents/@{triggerBody()['fileName']}
     ```
   - Cabeçalhos:
     ```
     Authorization: Bearer SEU_TOKEN
     Accept: application/vnd.github.v3+json
     ```
   - Corpo:
     ```json
     {
       "message": "Adiciona arquivo via Copilot Studio",
       "content": "@{base64(triggerBody()['fileContent'])}",
       "branch": "main"
     }
     ```

---

## 🤖 3. Ajustar o Copilot Studio
- Depois que o agente gerar cada arquivo Terraform, configure a ação **Chamar fluxo**.  
- Passe os parâmetros:
  - `fileName = "provider.tf"`  
  - `fileContent = <conteúdo gerado>`  

Repita para `variables.tf`, `main.tf`, `output.tf`, `terraform.tfvars`.

---

## 🧪 4. Testar
1. Execute a intenção no Copilot Studio.  
2. O agente gera o código.  
3. O fluxo chama a API do GitHub e cria/atualiza o arquivo no repositório.  
4. O commit aparece no GitHub com a mensagem definida.

---

## ✅ Resultado
- Todos os arquivos Terraform são enviados automaticamente ao GitHub.  
- Cada commit é registrado com mensagem clara.  
- O repositório fica pronto para rodar `terraform init && terraform apply`.

---
# 🚀 Deploy de Arquivos Terraform via Copilot Studio + Power Automate + GitHub API

Este projeto mostra como automatizar o envio de arquivos Terraform (`provider.tf`, `variables.tf`, `main.tf`, `output.tf`, `terraform.tfvars`) para um repositório GitHub usando **Copilot Studio** e **Power Automate**, sem precisar rodar `git` manualmente.

---

## 🔑 1. Criar Personal Access Token (PAT) no GitHub
1. Vá em **Settings → Developer settings → Personal access tokens → Tokens (classic)**.  
2. Clique em **Generate new token**.  
3. Marque permissões: `repo` (para ler e escrever nos repositórios).  
4. Copie o token gerado (será usado no fluxo).

---

## ⚙️ 2. Criar Repositório via API do GitHub
Endpoint:

 ```
{
  "id": 987654321,
  "name": "terraform-ec2",
  "full_name": "NOME_ORGANIZACAO/terraform-ec2",
  "private": true,
  "html_url": "https://github.com/NOME_ORGANIZACAO/terraform-ec2"
}
 ```
