# 📚 Projeto: Sistema de Gestão de Livraria (PostgreSQL)

## 📖 Descrição
Este projeto implementa um **banco de dados em PostgreSQL** para a gestão de uma livraria.  
Inclui tabelas de **livros, clientes e pedidos**, além de consultas SQL para análise de vendas, estoque e clientes.

---

## 🗂 Estrutura do Banco de Dados

### 📘 Tabela: Books
| Coluna          | Tipo            | Descrição                |
|-----------------|-----------------|--------------------------|
| Book_ID         | SERIAL (PK)     | ID único do livro        |
| Title           | VARCHAR(100)    | Título do livro          |
| Author          | VARCHAR(100)    | Autor do livro           |
| Genre           | VARCHAR(50)     | Gênero literário         |
| Published_Year  | INT             | Ano de publicação        |
| Price           | NUMERIC(10,2)   | Preço do livro           |
| Stock           | INT             | Quantidade em estoque    |

### 👥 Tabela: Customers
| Coluna       | Tipo          | Descrição                |
|--------------|---------------|--------------------------|
| Customer_ID  | SERIAL (PK)   | ID único do cliente      |
| Name         | VARCHAR(100)  | Nome do cliente          |
| Email        | VARCHAR(100)  | E-mail do cliente        |
| Phone        | VARCHAR(15)   | Telefone                 |
| City         | VARCHAR(50)   | Cidade                   |
| Country      | VARCHAR(150)  | País                     |

### 🛒 Tabela: Orders
| Coluna        | Tipo          | Descrição                         |
|---------------|---------------|-----------------------------------|
| Order_ID      | SERIAL (PK)   | ID único do pedido                |
| Customer_ID   | INT (FK)      | Cliente que fez o pedido          |
| Book_ID       | INT (FK)      | Livro comprado                    |
| Order_Date    | DATE          | Data do pedido                    |
| Quantity      | INT           | Quantidade de livros comprados    |
| Total_Amount  | NUMERIC(10,2) | Valor total do pedido             |

---

## 📥 Importação de Dados
Os dados foram carregados para as tabelas a partir de arquivos CSV utilizando o comando:

```sql
\copy Books FROM 'books.csv' DELIMITER ',' CSV HEADER;
\copy Customers FROM 'customers.csv' DELIMITER ',' CSV HEADER;
\copy Orders FROM 'orders.csv' DELIMITER ',' CSV HEADER;
📊 Consultas SQL de Exemplo
1. Listar todos os livros de gênero Fiction
sql
Copiar código
SELECT * FROM Books WHERE Genre = 'Fiction';
2. Encontrar livros publicados após 1950
sql
Copiar código
SELECT * FROM Books WHERE Published_Year > 1950;
3. Listar todos os clientes do Canadá
sql
Copiar código
SELECT * FROM Customers WHERE Country = 'Canada';
4. Mostrar pedidos realizados em novembro de 2023
sql
Copiar código
SELECT * FROM Orders
WHERE Order_Date BETWEEN '2023-11-01' AND '2023-11-30';
5. Calcular o valor total de vendas por cliente
sql
Copiar código
SELECT c.Name, SUM(o.Total_Amount) AS Total_Gasto
FROM Customers c
JOIN Orders o ON c.Customer_ID = o.Customer_ID
GROUP BY c.Name
ORDER BY Total_Gasto DESC;
6. Verificar o estoque de cada livro
sql
Copiar código
SELECT Title, Stock FROM Books ORDER BY Stock ASC;
7. Encontrar os 5 livros mais vendidos
sql
Copiar código
SELECT b.Title, SUM(o.Quantity) AS Total_Vendido
FROM Orders o
JOIN Books b ON o.Book_ID = b.Book_ID
GROUP BY b.Title
ORDER BY Total_Vendido DESC
LIMIT 5;
8. Clientes que compraram mais de 3 livros em um pedido
sql
Copiar código
SELECT c.Name, o.Quantity
FROM Orders o
JOIN Customers c ON o.Customer_ID = c.Customer_ID
WHERE o.Quantity > 3;
9. Média de preço dos livros por gênero
sql
Copiar código
SELECT Genre, AVG(Price) AS Media_Preco
FROM Books
GROUP BY Genre;
10. Número de clientes por país
sql
Copiar código
SELECT Country, COUNT(*) AS Numero_Clientes
FROM Customers
GROUP BY Country
ORDER BY Numero_Clientes DESC;
🚀 Como Executar
Criar o banco de dados no PostgreSQL:

sql
Copiar código
CREATE DATABASE livraria;
Executar os scripts SQL fornecidos (create_tables.sql, insert_data.sql, queries.sql).

Importar os CSVs para popular as tabelas.

Rodar as consultas para análise.

📌 **Tecnologias Utilizadas**  
- PostgreSQL  
- SQL  
- Git (controle de versão)  
- GitHub (versionamento remoto e portfólio)  
- PgAdmin (administração e testes)  
- CSV (importação de dados)  
- Markdown (documentação no README)  
👤 Autor
Projeto desenvolvido por Osvaldo Machado 🚀
Se gostou, deixe uma ⭐ no repositório!
