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

CREATE TABLE Estoque (
    id_estoque INT PRIMARY KEY,
    id_produto INT,
    id_funcionario INT,
    quant_produto INT,
    FOREIGN KEY (id_produto) REFERENCES Produtos(id_produto),
    FOREIGN KEY (id_funcionario) REFERENCES Funcionarios(id_funcionario)
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

CREATE TABLE Funcionarios_Clientes (
    id_funcionario INT,
    id_cliente INT,
    PRIMARY KEY (id_funcionario, id_cliente),
    FOREIGN KEY (id_funcionario) REFERENCES Funcionarios(id_funcionario),
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente)
);

CREATE TABLE Funcionarios_Estoque (
    id_funcionario INT,
    id_estoque INT,
    PRIMARY KEY (id_funcionario, id_estoque),
    FOREIGN KEY (id_funcionario) REFERENCES Funcionarios(id_funcionario),
    FOREIGN KEY (id_estoque) REFERENCES Estoque(id_estoque)
);

CREATE TABLE Produtos_Vendas (
    id_produto INT,
    id_venda INT,
    quantidade INT,
    PRIMARY KEY (id_produto, id_venda),
    FOREIGN KEY (id_produto) REFERENCES Produtos(id_produto),
    FOREIGN KEY (id_venda) REFERENCES Vendas(id_compra)
);
```


