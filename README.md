# 🛒 E-Commerce Database

Este projeto apresenta o **modelo de banco de dados relacional** de um sistema de E-Commerce.  
O objetivo é representar de forma organizada as entidades envolvidas em um processo de compra e venda online, incluindo **clientes (PF e PJ)**, **pedidos**, **produtos**, **fornecedores**, **estoques**, **pagamentos** e **entregas**.

---

## 📊 Estrutura Geral

O banco de dados foi modelado para garantir **normalização**, **consistência referencial** e **flexibilidade** no cadastro de informações de clientes, produtos e pedidos.

### Principais Entidades

| Entidade | Descrição |
|-----------|------------|
| **Cliente** | Representa o comprador. Pode ser Pessoa Física (PF) ou Jurídica (PJ). |
| **Cliente_PF** | Especialização de Cliente para pessoa física, contendo CPF. |
| **Cliente_PJ** | Especialização de Cliente para pessoa jurídica, contendo CNPJ e Razão Social. |
| **Produto** | Itens disponíveis para venda, com categoria, descrição e valor. |
| **Fornecedor** | Entidades responsáveis pelo fornecimento de produtos. |
| **Estoque** | Locais onde os produtos estão armazenados, com controle de quantidade. |
| **Pedido** | Registra cada compra feita por um cliente, contendo descrição, status e frete. |
| **Produto/Pedido** | Relação N:N entre produtos e pedidos, com quantidade solicitada. |
| **FormaPagamento** | Tipos de pagamento disponíveis (cartão, PIX, boleto, etc). |
| **Pedido_Pagamento** | Relação N:N entre pedidos e formas de pagamento, permitindo múltiplos pagamentos. |
| **Entrega** | Informações de rastreio, status e datas da entrega do pedido. |
| **Terceiro_Vendedor** | Vendedores parceiros, podendo associar produtos e quantidades vendidas. |
| **Fornecedor/Produto** | Relação entre fornecedor e produto. |
| **Produto_has_Estoque** | Controle de quantidades de produtos em diferentes estoques. |

---

## 🔧 Melhorias Implementadas

### 1️⃣ Cliente PF e PJ
- Criadas tabelas especializadas `Cliente_PF` e `Cliente_PJ` ligadas à tabela principal `Cliente`.
- Um cliente pode ser **Pessoa Física** ou **Pessoa Jurídica**, **nunca ambas**.

### 2️⃣ Pagamento Múltiplo
- Criada a tabela `FormaPagamento` e a tabela intermediária `Pedido_Pagamento`.
- Permite que um mesmo pedido tenha **diversas formas de pagamento** (ex: parte em cartão, parte em PIX).

### 3️⃣ Entrega com Rastreamento
- Criada a tabela `Entrega` para vincular o **status**, **código de rastreio** e **datas** ao pedido.

---

## 🧠 Modelo Lógico (Visão Simplificada)

```text
Cliente
 ├── Cliente_PF
 ├── Cliente_PJ
 └── Pedido ──< Entrega
         └── Pedido_Pagamento >── FormaPagamento
         └── Produto/Pedido >── Produto
Produto >── Produto_has_Estoque >── Estoque
Produto >── Fornecedor/Produto >── Fornecedor
Produto >── Vendedor/Produto >── Terceiro_Vendedor
