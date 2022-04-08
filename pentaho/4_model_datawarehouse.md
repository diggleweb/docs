# Criar modelo usando power Architect

1) Abra o SQL Power Architect, indo em C:\treinamento\SQL Power Architect e executando o architect.exe.

2) Abra o projeto de criação do Data Warehouse.

3) Clique com o botão direito do mouse sobre a área vazia, à direita, do SQL Power Architect e selecione Nova Tabela. Crie uma tabela com os seguintes dados:

    ```
    Nome da Tabela Lógica: Tabela de Fato 001
    Nome da Tabela Física: Fato_001
    Nome da chave primária: Fato_001_pk
    Cor da tabela: Vermelho
    Cantos arredondados: Sim
    ```
4) Clique com o botão direito do mouse sobre a tabela criada acima e crie novas colunas, com as seguintes características:

    ```
    Nome Lógico	Nome Físico	Chave Primária	Tipo	Precisão	Permite nulos
    Código da Fábrica	Cod_Fabrica	Sim	NVARCHAR	50	Não
    Código do Tempo	Cod_Tempo	Sim	NVARCHAR	50	Não
    Código do Cliente	Cod_Cliente	Sim	NVARCHAR	50	Não
    Código Organizacional	Cod_Organizacional	Sim	NVARCHAR	50	Não
    Código do Produto	Cod_Produto	Sim	NVARCHAR	50	Não
    Faturamento	Faturamento	Não	DOUBLE	-	Não
    Quantidade Vendida	Quantidade_Vendida	Não	DOUBLE	-	Não
    Imposto	Imposto	Não	DOUBLE	-	Não
    Custo Variável	Custo_Variavel	Não	DOUBLE	-	Não
    ```
5) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Fabrica, da tabela Fabrica, com Cod_Fabrica, da tabela Fato_001.

6) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Tempo, da tabela Tempo, com Cod_Tempo, da tabela Fato_001.

7) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Cliente, da tabela Cliente, com Cod_Cliente, da tabela Fato_001.

8) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Organizacional, da tabela Cod_Organizacional, com Cod_Fabrica, da tabela Fato_001.

9) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Produto, da tabela Produto, com Cod_Produto, da tabela Fato_001.

10) Clique com o botão direito do mouse sobre a área vazia, à direita, do SQL Power Architect e selecione Nova Tabela. Crie uma tabela com os seguintes dados:

    ```
    Nome da Tabela Lógica: Tabela de Fato 002
    Nome da Tabela Física: Fato_002
    Nome da chave primária: Fato_002_pk
    Cor da tabela: Vermelho
    Cantos arredondados: Sim
    ```

11) Clique com o botão direito do mouse sobre a tabela criada acima e crie novas colunas, com as seguintes características:

    ```
    Nome Lógico	Nome Físico	Chave Primária	Tipo	Precisão	Permite nulos
    Código da Fábrica	Cod_Fabrica	Sim	NVARCHAR	50	Não
    Código do Tempo	Cod_Tempo	Sim	NVARCHAR	50	Não
    Código do Cliente	Cod_Cliente	Sim	NVARCHAR	50	Não
    Código do Produto	Cod_Produto	Sim	NVARCHAR	50	Não
    Custo do Frete	Custo_Frete	Não	DOUBLE	-	Não
    ```

12) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Fabrica, da tabela Fabrica, com Cod_Fabrica, da tabela Fato_002.

13) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Tempo, da tabela Tempo, com Cod_Tempo, da tabela Fato_002.

14) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Cliente, da tabela Cliente, com Cod_Cliente, da tabela Fato_002.

15) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Produto, da tabela Produto, com Cod_Produto, da tabela Fato_002.

16) Clique com o botão direito do mouse sobre a área vazia, à direita, do SQL Power Architect e selecione Nova Tabela. Crie uma tabela com os seguintes dados:

    ```
    Nome da Tabela Lógica: Tabela de Fato 003
    Nome da Tabela Física: Fato_003
    Nome da chave primária: Fato_003_pk
    Cor da tabela: Vermelho
    Cantos arredondados: Sim
    ```

17) Clique com o botão direito do mouse sobre a tabela criada acima e crie novas colunas, com as seguintes características:

    ```
    Nome Lógico	Nome Físico	Chave Primária	Tipo	Precisão	Permite nulos
    Código da Fábrica	Cod_Fabrica	Sim	NVARCHAR	50	Não
    Código do Tempo	Cod_Tempo	Sim	NVARCHAR	50	Não
    Custo Fixo	Custo_Fixo	Não	DOUBLE	-	Não
    ```

18) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Fabrica, da tabela Fabrica, com Cod_Fabrica, da tabela Fato_003.

19) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Tempo, da tabela Tempo, com Cod_Tempo, da tabela Fato_003.

20) Clique com o botão direito do mouse sobre a área vazia, à direita, do SQL Power Architect e selecione Nova Tabela. Crie uma tabela com os seguintes dados:

    ```
    Nome da Tabela Lógica: Tabela de Fato 004
    Nome da Tabela Física: Fato_004
    Nome da chave primária: Fato_004_pk
    Cor da tabela: Vermelho
    Cantos arredondados: Sim
    ```

21) Clique com o botão direito do mouse sobre a tabela criada acima e crie novas colunas, com as seguintes características:

    ```
    Nome Lógico	Nome Físico	Chave Primária	Tipo	Precisão	Permite nulos
    Código do Tempo	Cod_Tempo	Sim	NVARCHAR	50	Não
    Código do Cliente	Cod_Cliente	Sim	NVARCHAR	50	Não
    Código Organizacional	Cod_Organizacional	Sim	NVARCHAR	50	Não
    Código do Produto	Cod_Produto	Sim	NVARCHAR	50	Não
    Meta do Faturamento	Meta_Faturamento	Não	DOUBLE	-	Não
    ```

22) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Tempo, da tabela Tempo, com Cod_Tempo, da tabela Fato_004.

23) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Cliente, da tabela Cliente, com Cod_Cliente, da tabela Fato_004.

24) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Organizacional, da tabela Organizacional, com Cod_Organizacional, da tabela Fato_004.

25) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Produto, da tabela Produto, com Cod_Produto, da tabela Fato_004.

26) Clique com o botão direito do mouse sobre a área vazia, à direita, do SQL Power Architect e selecione Nova Tabela. Crie uma tabela com os seguintes dados:

    ```
    Nome da Tabela Lógica: Tabela de Fato 005
    Nome da Tabela Física: Fato_005
    Nome da chave primária: Fato_005_pk
    Cor da tabela: Vermelho
    Cantos arredondados: Sim
    ```

27) Clique com o botão direito do mouse sobre a tabela criada acima e crie novas colunas, com as seguintes características:

    ```
    Nome Lógico	Nome Físico	Chave Primária	Tipo	Precisão	Permite nulos
    Código do Tempo	Cod_Tempo	Sim	NVARCHAR	50	Não
    Código da Fábrica	Cod_Fabrica	Sim	NVARCHAR	50	Não
    Código do Produto	Cod_Produto	Sim	NVARCHAR	50	Não
    Meta do Custo	Meta_Custo	Não	DOUBLE	-	Não
    ```

28) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Tempo, da tabela Tempo, com Cod_Tempo, da tabela Fato_005.

29) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Fabrica, da tabela Fabrica, com Cod_Fabrica, da tabela Fato_005.

30) Com o mouse, clique na opção Novo Relacionamento identificado, no menu vertical à direita, e ligue o campo Cod_Produto, da tabela Produto, com Cod_Produto, da tabela Fato_005.

31) Salve o projeto.

32) Com o projeto finalizado escolha, no menu superior do SQL Power Architect, a opção Ferramentas --> Engenharia Reversa.

33) Crie na conexão Modelo de Dados, para o banco de dados MySQL e a sua base de dados. Se houver erros durante a geração dos comandos, pode ser que você tenha algum campo com nome inválido, por exemplo, um acento.

34) Copie os comandos MySQL que o SQL Power Architect gerou. Em seguida, vá no HeidiSQL, crie uma nova consulta, e cole os comandos.

35) Coloque, na primeira linha, o comando USE DWSUCOS;.

36) Execute os comandos para criação do Data Warehouse.

37) Os comandos a serem executados para criação do Data Warehouse são os seguintes:

```sql
USE DWSUCOS;

CREATE TABLE Dim_Organizacional (
    Cod_Organizacional NVARCHAR(50) NOT NULL,
    Desc_Organizacional NVARCHAR(250) NOT NULL,
    Cod_Pai NVARCHAR(50) NOT NULL,
    Esquerda INT NOT NULL,
    Direita INT NOT NULL,
    Nivel INT NOT NULL,
    PRIMARY KEY (Cod_Organizacional)
);

CREATE TABLE Dim_Categoria (
    Cod_Categoria NVARCHAR(50) NOT NULL,
    Desc_Categoria NVARCHAR(250) NOT NULL,
    PRIMARY KEY (Cod_Categoria)
);

CREATE TABLE Dim_Marca (
    Cod_Marca NVARCHAR(50) NOT NULL,
    Desc_Marca NVARCHAR(250) NOT NULL,
    Cod_Categoria NVARCHAR(50) NOT NULL,
    PRIMARY KEY (Cod_Marca)
);

CREATE TABLE Dim_Produto (
    Cod_Produto NVARCHAR(50) NOT NULL,
    Desc_Produto NVARCHAR(250) NOT NULL,
    Cod_Marca NVARCHAR(50) NOT NULL,
    Atr_Tamanho NVARCHAR(250) NOT NULL,
    Atr_Sabor NVARCHAR(250) NOT NULL,
    PRIMARY KEY (Cod_Produto)
);

CREATE TABLE Dim_Tempo (
    Cod_Tempo NVARCHAR(50) NOT NULL,
    Data DATE NOT NULL,
    Numero_Dia_Semana NVARCHAR(50) NOT NULL,
    Numero_Mes NVARCHAR(50) NOT NULL,
    Numero_Ano NVARCHAR(50) NOT NULL,
    Nome_Mes NVARCHAR(250) NOT NULL,
    Numero_Trimestre NVARCHAR(50) NOT NULL,
    Nome_Trimestre NVARCHAR(250) NOT NULL,
    Numero_Semestre NVARCHAR(50) NOT NULL,
    Nome_Semestre NVARCHAR(250) NOT NULL,
    PRIMARY KEY (Cod_Tempo)
);

CREATE TABLE Dim_Cliente (
    Cod_Cliente NVARCHAR(50) NOT NULL,
    Desc_Cliente NVARCHAR(250) NOT NULL,
    Cod_Cidade NVARCHAR(50) NOT NULL,
    Desc_Cidade NVARCHAR(250) NOT NULL,
    Cod_Estado NVARCHAR(50) NOT NULL,
    Desc_Estado NVARCHAR(250) NOT NULL,
    Cod_Regiao NVARCHAR(50) NOT NULL,
    Desc_Regiao NVARCHAR(250) NOT NULL,
    Cod_Segmento NVARCHAR(50) NOT NULL,
    Desc_Segmento NVARCHAR(250) NOT NULL,
    PRIMARY KEY (Cod_Cliente)
);

ALTER TABLE Dim_Cliente COMMENT 'Tabela da dimensão cliente';

CREATE TABLE Fato_004 (
    Cod_Produto NVARCHAR(50) NOT NULL,
    Cod_Organizacional NVARCHAR(50) NOT NULL,
    Cod_Cliente NVARCHAR(50) NOT NULL,
    Cod_Tempo NVARCHAR(50) NOT NULL,
    Meta_Faturamento DOUBLE PRECISION NOT NULL,
    PRIMARY KEY (Cod_Produto, Cod_Organizacional, Cod_Cliente, Cod_Tempo)
);

CREATE TABLE Dim_Fabrica (
    Cod_Fabrica NVARCHAR(50) NOT NULL,
    Desc_Fabrica NVARCHAR(250) NOT NULL,
    PRIMARY KEY (Cod_Fabrica)
);

ALTER TABLE Dim_Fabrica COMMENT 'Tabela de dimensão Fábrica';

CREATE TABLE Fato_005 (
    Cod_Produto NVARCHAR(50) NOT NULL,
    Cod_Tempo NVARCHAR(50) NOT NULL,
    Cod_Fabrica NVARCHAR(50) NOT NULL,
    Meta_Custo DOUBLE PRECISION NOT NULL,
    PRIMARY KEY (Cod_Produto, Cod_Tempo, Cod_Fabrica)
);

CREATE TABLE Fato_003 (
    Cod_Fabrica NVARCHAR(50) NOT NULL,
    Cod_Tempo NVARCHAR(50) NOT NULL,
    Custo_Fixo DOUBLE PRECISION NOT NULL,
    PRIMARY KEY (Cod_Fabrica, Cod_Tempo)
);

CREATE TABLE Fato_002 (
    Cod_Fabrica NVARCHAR(50) NOT NULL,
    Cod_Tempo NVARCHAR(50) NOT NULL,
    Cod_Cliente NVARCHAR(50) NOT NULL,
    Cod_Produto NVARCHAR(50) NOT NULL,
    Custo_Frete DOUBLE PRECISION NOT NULL,
    PRIMARY KEY (Cod_Fabrica, Cod_Tempo, Cod_Cliente, Cod_Produto)
);

CREATE TABLE Fato_001 (
    Cod_Fabrica NVARCHAR(50) NOT NULL,
    Cod_Tempo NVARCHAR(50) NOT NULL,
    Cod_Cliente NVARCHAR(50) NOT NULL,
    Cod_Organizacional NVARCHAR(50) NOT NULL,
    Cod_Produto NVARCHAR(50) NOT NULL,
    Faturamento DOUBLE PRECISION NOT NULL,
    Unidade_Vendida DOUBLE PRECISION NOT NULL,
    Quantidade_Vendida DOUBLE PRECISION NOT NULL,
    Imposto DOUBLE PRECISION NOT NULL,
    Custo_Variavel DOUBLE PRECISION NOT NULL,
    PRIMARY KEY (Cod_Fabrica, Cod_Tempo, Cod_Cliente, Cod_Organizacional, Cod_Produto)
);

ALTER TABLE Fato_001 ADD CONSTRAINT dim_organizacional_fato_001_fk
FOREIGN KEY (Cod_Organizacional)
REFERENCES Dim_Organizacional (Cod_Organizacional)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_004 ADD CONSTRAINT dim_organizacional_fato_004_fk
FOREIGN KEY (Cod_Organizacional)
REFERENCES Dim_Organizacional (Cod_Organizacional)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Dim_Marca ADD CONSTRAINT dim_categoria_dim_marca_fk
FOREIGN KEY (Cod_Categoria)
REFERENCES Dim_Categoria (Cod_Categoria)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Dim_Produto ADD CONSTRAINT dim_marca_dim_produto_fk
FOREIGN KEY (Cod_Marca)
REFERENCES Dim_Marca (Cod_Marca)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_001 ADD CONSTRAINT dim_produto_fato_001_fk
FOREIGN KEY (Cod_Produto)
REFERENCES Dim_Produto (Cod_Produto)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_002 ADD CONSTRAINT dim_produto_fato_002_fk
FOREIGN KEY (Cod_Produto)
REFERENCES Dim_Produto (Cod_Produto)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_004 ADD CONSTRAINT dim_produto_fato_004_fk
FOREIGN KEY (Cod_Produto)
REFERENCES Dim_Produto (Cod_Produto)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_005 ADD CONSTRAINT dim_produto_fato_005_fk
FOREIGN KEY (Cod_Produto)
REFERENCES Dim_Produto (Cod_Produto)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_001 ADD CONSTRAINT dim_tempo_fato_001_fk
FOREIGN KEY (Cod_Tempo)
REFERENCES Dim_Tempo (Cod_Tempo)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_002 ADD CONSTRAINT dim_tempo_fato_002_fk
FOREIGN KEY (Cod_Tempo)
REFERENCES Dim_Tempo (Cod_Tempo)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_003 ADD CONSTRAINT dim_tempo_fato_003_fk
FOREIGN KEY (Cod_Tempo)
REFERENCES Dim_Tempo (Cod_Tempo)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_004 ADD CONSTRAINT dim_tempo_fato_004_fk
FOREIGN KEY (Cod_Tempo)
REFERENCES Dim_Tempo (Cod_Tempo)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_005 ADD CONSTRAINT dim_tempo_fato_005_fk
FOREIGN KEY (Cod_Tempo)
REFERENCES Dim_Tempo (Cod_Tempo)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_001 ADD CONSTRAINT dim_clinete_fato_001_fk
FOREIGN KEY (Cod_Cliente)
REFERENCES Dim_Cliente (Cod_Cliente)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_002 ADD CONSTRAINT dim_clinete_fato_002_fk
FOREIGN KEY (Cod_Cliente)
REFERENCES Dim_Cliente (Cod_Cliente)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_004 ADD CONSTRAINT dim_clinete_fato_004_fk
FOREIGN KEY (Cod_Cliente)
REFERENCES Dim_Cliente (Cod_Cliente)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_001 ADD CONSTRAINT dim_fabrica_fato_001_fk
FOREIGN KEY (Cod_Fabrica)
REFERENCES Dim_Fabrica (Cod_Fabrica)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_002 ADD CONSTRAINT dim_fabrica_fato_002_fk
FOREIGN KEY (Cod_Fabrica)
REFERENCES Dim_Fabrica (Cod_Fabrica)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_003 ADD CONSTRAINT dim_fabrica_fato_003_fk
FOREIGN KEY (Cod_Fabrica)
REFERENCES Dim_Fabrica (Cod_Fabrica)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_005 ADD CONSTRAINT dim_fabrica_fato_005_fk
FOREIGN KEY (Cod_Fabrica)
REFERENCES Dim_Fabrica (Cod_Fabrica)
ON DELETE NO ACTION
ON UPDATE NO ACTION;
```