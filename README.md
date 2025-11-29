# 📘 README — Banco de Dados `mydb`

Este arquivo descreve a estrutura do banco de dados **mydb**, gerado a partir de um modelo do **MySQL Workbench**. Ele contém tabelas relacionadas ao gerenciamento de clientes, veículos, pagamentos, funcionários, ordens de serviço e fornecedores.

---

## 📂 **Visão Geral do Banco de Dados**

O banco de dados representa um sistema de oficina mecânica, contendo informações sobre:

* Clientes
* Veículos
* Pagamentos
* Funcionários
* Ordens de Serviço
* Fornecedores
* Peças utilizadas nas ordens

As relações incluem chaves estrangeiras, cardinalidades 1:1 e 1:N e tabelas auxiliares.

---

## 🗂️ **Estrutura das Tabelas**

### 🔹 **1. Telefone**

Armazena telefones cadastrados.

* **id** (PK)
* telefone

---

### 🔹 **2. Cliente**

Contém dados dos clientes.

* **id** (PK)
* username
* email
* password
* Telefone_id (FK → Telefone.id)

🔗 Relação: **1 Cliente ↔ 1 Telefone**

---

### 🔹 **3. Pagamento**

Registra dados dos pagamentos.

* **id** (PK)
* username
* email
* data_pagamento
* valor_pago
* forma_pagamento (enum)
* status_pagamento (enum)

---

### 🔹 **4. Veículo**

Armazena veículos cadastrados.

* **id** (PK)
* placa
* modelo
* marca
* ano
* Cliente_id (FK → Cliente.id)

🔗 Relação: **Cliente 1:N Veículo**

---

### 🔹 **5. Funcionário**

Registra funcionários.

* **id** (PK)
* nome
* especialidade
* telefone

---

### 🔹 **6. Ordem de Serviço**

Tabela que registra ordens de serviço da oficina.

* Várias chaves compostas (id, pagamento, funcionário, veículo)
* tipo
* peças_utilizadas
* custo
* datas

FKs:

* Pagamento
* Veículo
* Funcionários (duas referências)

---

### 🔹 **7. Status de Pagamento**

Tabela auxiliar para status.

* cancelado
* pendente
* concluido
* recusado

(Obs.: tabela não possui chave primária.)

---

### 🔹 **8. Usuário**

Usuários do sistema.

* **id** (PK)
* email
* senha
* Cliente_id (FK)

---

### 🔹 **9. Fornecedor**

Armazena fornecedores de peças.

* **id** (PK)
* nome
* cnpj
* telefone
* email

---

### 🔹 **10. Peças**

Peças usadas em ordens de serviço.

* **id** (PK)
* nome_peca
* quantidade_estoque
* preco_unitario
* Ordem de Serviço_id (FK)
* Fornecedor_id (FK)

🔗 Relações:

* **1 Fornecedor ↔ N Peças**
* **1 Ordem de Serviço ↔ N Peças**

---

## 🔗 **Principais Relacionamentos**

| Tabela           | Relaciona com    | Tipo |
| ---------------- | ---------------- | ---- |
| Cliente          | Telefone         | 1:1  |
| Cliente          | Veículo          | 1:N  |
| Veículo          | Ordem de Serviço | 1:N  |
| Pagamento        | Ordem de Serviço | 1:N  |
| Funcionário      | Ordem de Serviço | 1:N  |
| Fornecedor       | Peças            | 1:N  |
| Ordem de Serviço | Peças            | 1:N  |

---

## ⚠️ **Observações Importantes**

* Algumas colunas usam DEFAULT CURRENT_TIMESTAMP em tipos incompatíveis (ex.: INT, VARCHAR). Pode causar erros.
* O nome da tabela **"Ordem de Serviço"** contém espaço; não é recomendado.
* Relacionamentos compostos e múltiplas referências a funcionários podem ser revisados.

---

## 📌 **Sugestões de Melhoria**

* Padronizar nomes das tabelas (sem espaços e acentos).
* Revisar chaves primárias compostas muito extensas.
* Ajustar tipos errados (ex.: Telefone_id como TIMESTAMP).

---

## 📎 **Licença**

Este script pode ser modificado livremente para estudos e melhorias no sistema.

---

