# Avaliação Prática Banco de Dados

# ● 1- Cenário
  Você é um desenvolvedor apaixonado por música e foi contratado pela loja Retro Music que vende CDs e Vinis. Essa loja precisa de um software para auxiliar no gerenciamento do negócio, devido ao aumento da concorrência e a necessidade de acompanhar a modernização. Conversando com o dono da loja, foi apresentado algumas funções que esse software deve conter, como: gerenciar o estoque de CDs e Vinis, acompanhar e registrar as vendas, gerenciar cadastros de clientes e cadastrar seus funcionários. 


# ● 2- Modelagem Conceitual

![DER](https://github.com/herixcx/Avaliacao_Pratica_Banco_de_Dados/assets/162808394/475b319b-3dfb-4c60-9cf1-38dbdf691b17)


# ● 3- Modelagem Lógica

![DER (2)](https://github.com/herixcx/Avaliacao_Pratica_Banco_de_Dados/assets/162808394/3ea9c870-a794-4a5c-b9da-a34b4421019c)

# ● 4- Modelagem Física

```sql
    CREATE TABLE Funcionarios (
    id_funcionario INT PRIMARY KEY,
    nome VARCHAR(70),
    cargo VARCHAR(70),
    salario DECIMAL(20,2),
    data_contratacao DATE
);

CREATE TABLE Endereco (
    id_endereco INT PRIMARY KEY,
    rua VARCHAR(100),
    numero INT,
    cidade VARCHAR(50),
    estado VARCHAR(50),
    cep VARCHAR(10)
);

CREATE TABLE Email (
    id_email INT PRIMARY KEY,
    email VARCHAR(100)
);

CREATE TABLE Telefone (
    id_telefone INT PRIMARY KEY,
    telefone VARCHAR(15)
);

CREATE TABLE Clientes (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(70),
    id_endereco INT,
    id_email INT,
    id_telefone INT,
    FOREIGN KEY (id_endereco) REFERENCES Endereco(id_endereco),
    FOREIGN KEY (id_email) REFERENCES Email(id_email),
    FOREIGN KEY (id_telefone) REFERENCES Telefone(id_telefone)
);

CREATE TABLE Produtos (
    id_produto INT PRIMARY KEY,
    titulo VARCHAR(70),
    artista VARCHAR(70),
    genero VARCHAR(50),
    preco DECIMAL(10, 2),
    id_funcionario INT,
    FOREIGN KEY (id_funcionario) REFERENCES Funcionarios(id_funcionario)
);

CREATE TABLE Estoque (
    id_estoque INT PRIMARY KEY,
    id_produto INT,
    id_funcionario INT,
    quant_produto INT,
    FOREIGN KEY (id_produto) REFERENCES Produtos(id_produto),
    FOREIGN KEY (id_funcionario) REFERENCES Funcionarios(id_funcionario)
);

CREATE TABLE Vendas (
    id_compra INT PRIMARY KEY,
    id_cliente INT,
    id_produto INT,
    id_funcionario INT,
    data_compra DATE,
    valor_total DECIMAL(10, 2),
    quant_produto INT,
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente),
    FOREIGN KEY (id_produto) REFERENCES Produtos(id_produto),
    FOREIGN KEY (id_funcionario) REFERENCES Funcionarios(id_funcionario)
);
```
# ● 5- Inserção de Dados

```sql
INSERT INTO Endereco (id_endereco, rua, numero, cidade, estado, cep)
VALUES 
    (01, 'Rua A', 104, 'Franca', 'São Paulo', '14405-000'),
    (02, 'Rua B', 456, 'Franca', 'São Paulo', '14405-001'),
    (03, 'Rua C', 159, 'Franca', 'São Paulo', '14405-002'),
    (04, 'Rua D', 753, 'Franca', 'São Paulo', '14405-003'),
    (05, 'Rua E', 20, 'Franca', 'São Paulo', '14405-004'),
    (06, 'Rua F', 34, 'Franca', 'São Paulo', '14405-005'),
    (07, 'Rua G', 879, 'Franca', 'São Paulo', '14405-006'),
    (08, 'Rua H', 46, 'Franca', 'São Paulo', '14405-007'),
    (09, 'Rua I', 234, 'Franca', 'São Paulo', '14405-008'),
    (10, 'Rua J', 98, 'Franca', 'São Paulo', '14405-009'),
    (11, 'Rua K', 45, 'Franca', 'São Paulo', '14405-011'),
    (12, 'Rua L', 32, 'Franca', 'São Paulo', '14405-012'),
    (13, 'Rua M', 678, 'Franca', 'São Paulo', '14405-013'),
    (14, 'Rua N', 4567, 'Franca', 'São Paulo', '14405-014'),
    (15, 'Rua O', 3435, 'Franca', 'São Paulo', '14405-015'),
    (16, 'Rua P', 4567, 'Franca', 'São Paulo', '14405-016'),
    (17, 'Rua Q', 967, 'Franca', 'São Paulo', '14405-017'),
    (18, 'Rua R', 3456, 'Franca', 'São Paulo', '14405-018'),
    (19, 'Rua S', 5674, 'Franca', 'São Paulo', '14405-019'),
    (20, 'Rua T', 123, 'Franca', 'São Paulo', '14405-020');

INSERT INTO Email (id_email, email)
VALUES 
    (01, 'maria@exemplo.com'),
    (02, 'ana@exemplo.com'),
    (03, 'carlos@exemplo.com'),
    (04, 'joao@exemplo.com'),
    (05, 'patricia@exemplo.com'),
    (06, 'pedro@exemplo.com'),
    (07, 'luana@exemplo.com'),
    (08, 'rafael@exemplo.com'),
    (09, 'camila@exemplo.com'),
    (10, 'lucas@exemplo.com'),
    (11, 'bianca@exemplo.com'),
    (12, 'gustavo@exemplo.com'),
    (13, 'juliana@exemplo.com'),
    (14, 'thiago@exemplo.com'),
    (15, 'vanessa@exemplo.com'),
    (16, 'diego@exemplo.com'),
    (17, 'fernanda@exemplo.com'),
    (18, 'marcelo@exemplo.com'),
    (19, 'renata@exemplo.com'),
    (20, 'daniel@exemplo.com');


INSERT INTO Telefone (id_telefone, telefone)
VALUES 
    (01, '987654321'),
    (02, '998767432'),
    (03, '987154321'),
    (04, '998765632'),
    (05, '981654321'),
    (06, '998768432'),
    (07, '987654221'),
    (08, '998760432'),
    (09, '987354321'),
    (10, '948765432'),
    (11, '987658321'),
    (12, '998775432'),
    (13, '987634321'),
    (14, '968765432'),
    (15, '987653321'),
    (16, '998765442'),
    (17, '988654321'),
    (18, '998760432'),
    (19, '987664321'),
    (20, '998765430');



INSERT INTO Funcionarios (id_funcionario, nome, cargo, salario, data_contratacao)
VALUES 
     (1, 'João Silva', 'Gerente', 5000.00, '2023-01-15'),
     (2, 'Gabriela Santos', 'Vendedor', 3200.00, '2023-05-20'),
     (3, 'Thiago Costa', 'Atendente', 2800.00, '2021-09-10'),
     (4, 'Laura Pereira', 'Assistente de Estoque', 3000.00, '2020-11-30'),
     (5, 'Juliana Silva', 'Gerente de Vendas', 5000.00, '2023-02-25'),
     (6, 'Matheus Rodrigues', 'Vendedor', 3400.00, '2021-07-12'),
     (7, 'Camila Almeida', 'Atendente', 5000.00, '2022-08-05'),
     (8, 'André Souza', 'Assistente de Estoque', 3200.00, '2020-04-18'),
     (9, 'Mariana Lima', 'Vendedor', 3300.00, '2021-01-09'),
     (10, 'Felipe Martins', 'Gerente', 5000.00, '2022-10-30'),
     (11, 'Letícia Ribeiro', 'Atendente', 3000.00, '2023-04-15'),
     (12, 'Rafael Barbosa', 'Assistente de Estoque', 2900.00, '2021-06-20'),
     (13, 'Aline Gonçalves', 'Gerente de Vendas', 5200.00, '2020-09-05'),
     (14, 'Guilherme Cardoso', 'Vendedor', 3500.00, '2022-03-12'),
     (15, 'Fernanda Oliveira', 'Atendente', 2700.00, '2021-11-25'),
     (16, 'Henrique Costa', 'Assistente de Estoque', 3100.00, '2023-01-08'),
     (17, 'Beatriz Santos', 'Gerente', 5300.00, '2020-07-19'),
     (18, 'Letícia Silva', 'Vendedor', 3300.00, '2023-12-03'),
     (19, 'Vinícius Nunes', 'Atendente', 2800.00, '2021-02-28'),
     (20, 'Renata Pereira', 'Gerente de Vendas', 5300.00, '2023-05-10');

INSERT INTO Clientes (id_cliente, nome, id_endereco, id_email, id_telefone)
VALUES 
    (1, 'Maria Souza', 01, 01, 01),
    (2, 'Ana Santos', 02, 02, 02),
    (3, 'Carlos Oliveira', 03, 03, 03),
    (4, 'Joao Costa', 04, 04, 04),
    (5, 'Patricia Pereira', 05, 05, 05),
    (6, 'Pedro Rodrigues', 06, 06, 06),
    (7, 'Luana Almeida', 07, 07, 07),
    (8, 'Rafael Souza', 08, 08, 08),
    (9, 'Camila Lima', 09, 09, 09),
    (10, 'Lucas Martins', 10, 10, 10),
    (11, 'Bianca Ribeiro', 11, 11, 11),
    (12, 'Gustavo Barbosa', 12, 12, 12),
    (13, 'Juliana Gonçalves', 13, 13, 13),
    (14, 'Thiago Cardoso', 14, 14, 14),
    (15, 'Vanessa Fernandes', 15, 15, 15),
    (16, 'Diego Carvalho', 16, 16, 16),
    (17, 'Fernanda Gomes', 17, 17, 17),
    (18, 'Marcelo Nunes', 18, 18, 18),
    (19, 'Renata Pereira', 19, 19, 19),
    (20, 'Daniel Miranda', 20, 20, 20);

INSERT INTO Produtos (id_produto, titulo, artista, genero, preco, id_funcionario)
VALUES 
    (1, 'ARTPOP', 'LADY GAGA', 'Pop/EDM', 49.99, 1),
    (2, 'BRAT', 'Charli XCX', 'Pop', 59.99, 2),
    (3, 'Blue', 'iamwhoami', 'EDM', 39.99, 3),
    (4, 'CHROMATICA', 'LADY GAGA', 'Pop', 59.99, 4),
    (5, 'Crash', 'Charli XCX', 'Pop', 59.99, 5),
    (6, 'Noitada', 'Pabllo Vittar', 'Pop', 59.99, 6),
    (7, 'Artangels', 'Grimes', 'Pop', 39.99, 7),
    (8, 'Renaissance', 'Beyoncé', 'Pop', 59.99, 8),
    (9, 'The Fame Monster', 'LADY GAGA', 'Pop', 39.99, 9),
    (10, 'So Sad So Sexy', 'Lykke Li', 'Pop', 39.99, 10),
    (11, 'THE ALBUM', 'BLACKPINK', 'Kpop', 129.99, 11),
    (12, 'how i’m feeling now', 'Charli XCX', 'Pop', 49.99, 12),
    (13, 'Melodrama', 'Lorde', 'Pop', 49.99, 13),
    (14, 'Funk Generation', 'Anitta', 'Funk', 49.99, 14),
    (15, 'STARFUCKER', 'Slayyyter', 'Pop', 39.99, 15),
    (16, 'Slut Pop Miami', 'Kim Petras', 'Pop/EDM', 29.99, 16),
    (17, 'This is Acting', 'Sia', 'Pop', 39.99, 17),
    (18, 'Batuke Freak', 'Karol Conká', 'Hip Hop', 49.99, 18),
    (19, 'Pop 2', 'Charli XCX', 'Pop', 49.99, 19),
    (20, 'Dangerous Woman', 'Ariana Grande', 'Pop', 59.99, 20);


INSERT INTO Estoque (id_estoque, id_produto, id_funcionario, quant_produto)
VALUES 
    (1, 1, 1, 50),
    (2, 2, 2, 60),
    (3, 3, 3, 30),
    (4, 4,4, 40),
    (5, 5, 5, 55),
    (6, 6, 6, 20),
    (7, 7, 7, 40),
    (8, 8, 8, 25),
    (9, 9, 9, 40),
    (10,10, 10, 60),
    (11, 11, 11, 65),
    (12, 12, 12, 40),
    (13, 13, 13, 20),
    (14, 14, 14, 30),
    (15, 15, 15, 60),
    (16, 16, 16, 35),
    (17, 17, 17, 45),
    (18, 18, 18, 50),
    (19, 19, 19, 30),
    (20, 20, 20, 40);

INSERT INTO Vendas (id_compra, id_cliente, id_produto, id_funcionario, data_compra, valor_total, quant_produto)
VALUES 
    (1, 2, 3, 4, '2020-06-01', 39.99, 1),
    (2, 3, 4, 5, '2022-07-03', 59.99, 1),
    (3, 4, 5, 6, '2023-10-06', 59.99, 1),
    (4, 5, 6, 7, '2023-06-08', 59.99, 1),
    (5, 6, 7, 8, '2020-05-03', 39.99, 1),
    (6, 7, 8, 9, '2020-05-02', 59.99, 1),
    (7, 8, 9, 10, '2020-06-04', 39.99, 1),
    (8, 9, 11, 11, '2021-09-02', 39.99, 1),
    (9, 10, 11, 12, '2022-04-12', 129.99, 1),
    (10, 11, 12, 13, '2020-06-25', 49.99, 1),
    (11, 12, 13, 14, '2020-06-22', 49.99, 1),
    (12, 13, 14, 15, '2022-11-12', 49.99, 1),
    (13, 14, 15, 16, '2022-06-12', 39.99, 1),
    (14, 15, 16, 17, '2020-08-01', 29.99, 1),
    (15, 16, 17, 18, '2022-12-25', 39.99, 1),
    (16, 17, 18, 19, '2020-08-09', 49.99, 1),
    (17, 18, 19, 20, '2022-10-01', 49.99, 1),
    (18, 19, 20, 1, '2022-09-16', 49.99, 1),
    (19, 20, 1, 2, '2022-05-28', 29.99, 1),
    (20, 1, 2, 3, '2023-04-13', 49.99, 1);
```

# ● 6- CRUD
READ:
```sql
SELECT * FROM Funcionarios;
```
![Screenshot_16](https://github.com/herixcx/Avaliacao_Pratica_Banco_de_Dados/assets/162808394/ec9ca812-fdd4-46c7-968c-db25b082ab5f)
![Screenshot_17](https://github.com/herixcx/Avaliacao_Pratica_Banco_de_Dados/assets/162808394/fd5b0257-f02d-466c-a384-42709d339a12)
![Screenshot_18](https://github.com/herixcx/Avaliacao_Pratica_Banco_de_Dados/assets/162808394/d678c89f-81c5-4fc4-83c0-59cf1e38b446)





