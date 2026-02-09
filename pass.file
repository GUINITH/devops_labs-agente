Perfeito, Guilherme. Aqui está um **README.md completo** documentando o fluxo no Power Automate para editar um arquivo no GitHub, localizar uma linha específica (`- resourcename.yaml`), inserir logo abaixo uma nova linha (`- novo-arquivo.yaml`), e salvar de volta no repositório.

```markdown
# Fluxo Power Automate – Atualizar arquivo no GitHub

Este fluxo automatiza a atualização de um arquivo YAML em um repositório GitHub.  
Ele baixa o arquivo, insere uma nova linha após um conteúdo específico e salva de volta no repositório.

---

## 🔎 Objetivo
Adicionar uma linha `- novo-arquivo.yaml` logo após a linha que contém `- resourcename.yaml`.

---

## 🛠️ Passo a passo

### 1. HTTP GET – Obter arquivo do GitHub
- **Ação:** HTTP
- **Método:** `GET`
- **URL:**
  ```
  `https://api.github.com/repos/{org}/{repo}/contents/{path}` [(api.github.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fapi.github.com%2Frepos%2F%257Borg%257D%2F%257Brepo%257D%2Fcontents%2F%257Bpath%257D")
  ```
- **Cabeçalhos:**
  ```
  Authorization: Bearer SEU_TOKEN
  Accept: application/vnd.github.v3+json
  ```
- **Saída:** JSON com `content` (Base64) e `sha`.

---

### 2. Compose – Decodificar conteúdo
- **Nome da ação:** Compose – Decodificar
- **Expressão:**
  ```plaintext
  base64ToString(body('HTTP_GET')?['content'])
  ```
- **Resultado:** conteúdo do arquivo como texto.

---

### 3. Compose – Inserir nova linha após referência
- **Nome da ação:** Compose – Atualizar
- **Expressão:**
  ```plaintext
  replace(
    outputs('Compose_Decodificar'),
    '- resourcename.yaml',
    concat('- resourcename.yaml', '\n  - novo-arquivo.yaml')
  )
  ```
- **Resultado:** arquivo atualizado com a nova linha logo abaixo da referência.

---

### 4. Compose – Converter para Base64
- **Nome da ação:** Compose – Base64
- **Expressão:**
  ```plaintext
  base64(outputs('Compose_Atualizar'))
  ```

---

### 5. HTTP PUT – Atualizar arquivo no GitHub
- **Ação:** HTTP
- **Método:** `PUT`
- **URL:**
  ```
  https://api.github.com/repos/{org}/{repo}/contents/{path}
  ```
- **Cabeçalhos:**
  ```
  Authorization: Bearer SEU_TOKEN
  Accept: application/vnd.github.v3+json
  Content-Type: application/json
  ```
- **Corpo:**
  ```json
  {
    "message": "Adiciona novo arquivo YAML na lista de resources",
    "content": "@{outputs('Compose_Base64')}",
    "sha": "@{body('HTTP_GET')?['sha']}"
  }
  ```

---

## ✅ Resultado
- O fluxo baixa o arquivo do GitHub.
- Decodifica para texto.
- Localiza a linha `- resourcename.yaml`.
- Insere `- novo-arquivo.yaml` logo abaixo.
- Converte para Base64.
- Faz o commit no GitHub com o arquivo atualizado.

---

## 📂 Estrutura de ações no Designer
1. **HTTP – GET arquivo GitHub**
2. **Compose – Decodificar**
3. **Compose – Atualizar**
4. **Compose – Base64**
5. **HTTP – PUT arquivo GitHub**
```

---

👉 Esse README já serve como documentação para o repositório e pode ser usado como guia para replicar o fluxo. Quer que eu monte também um **exemplo visual com prints simulados da tela do Power Automate Designer** (nomes das ações e expressões preenchidas), para deixar ainda mais didático?
