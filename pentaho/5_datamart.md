# 

## Metodoss de armazenamento

OLAP - On-Line Analytical Processing (Processamento Analítico On-Line)

**ROLAP** (OLAP Relacional): Os dados são armazenados de forma relacional.
**MOLAP** (OLAP Multidimensional): Os dados são armazenados de forma multidimensional.
**HOLAP** (OLAP Híbrido): Uma combinação dos métodos ROLAP e MOLAP.
**DOLAP** (OLAP Desktop): O conjunto de dados multidimensionais deve ser criado no servidor e transferido para o desktop. Permite portabilidade aos usuários OLAP que não possuem acesso direto ao servidor.


## OLAP

OLAP é um conceito de interface com o usuário que proporciona a capacidade de ter idéias sobre os dados, permitindo analisá-los profundamente em diversos ângulos. As funções básicas do OLAP são:

- Visualização multidimensional dos dados;
- Exploração;
- Rotação;
- Vários modos de visualização.

## Data Mart

- estructura multidimensional lógica, para melhorar performance do datawarehouse.

[grande banco] -> [pequenos bancos]
datawarehouse -> Data Mart

### exemplo datamart da presidencia

|   |  Tempo | Cliente | Produto | Fabrica | Vendas |
| :-- | :--: | :--: | :--: | :--: | :--: |
| faturamento em R$ (dados diarios)-(001) | X | X | X | X | X |
| Custo de frete R$ (dados diarios)-(002) | X | X | X | X | X |
| Imposto em R$ (dados diarios)-(001) | X | X | X | X | X |
| Custo fixo em R$ (dados Mensais)-(003) | X | X | X | X | X |
| Custo Variavel em R$ (dados diarios)-(001) | X | X | X | X | X |
| Unidades Vendidas em litros (dados diarios)-(001) | X | X | X | X | X |
| Meta de Faturamento em R$ (dados Mensais)-(004) | X | X | X | X | X |
| Meta de Custos em R$ (dados Mensais)-(005) | X | X | X | X | X |


## script sql datamart

```sql
USE DMPRESIDENCIA;

CREATE TABLE Dim_Organizacional (
    ID_Vendedor INT NOT NULL,
    Cod_Vendedor NVARCHAR(50) NOT NULL,
    Desc_Vendedor NVARCHAR(250) NOT NULL,
    Cod_Gerente NVARCHAR(50) NOT NULL,
    Desc_Gerente NVARCHAR(250) NOT NULL,
    Cod_Diretor NVARCHAR(50) NOT NULL,
    Desc_Diretor NVARCHAR(250) NOT NULL,
    PRIMARY KEY (ID_Vendedor)
);

CREATE TABLE Dim_Produto (
    ID_Produto INT NOT NULL,
    Cod_Produto NVARCHAR(50) NOT NULL,
    Desc_Produto NVARCHAR(250) NOT NULL,
    Cod_Marca NVARCHAR(50) NOT NULL,
    Atr_Tamanho NVARCHAR(250) NOT NULL,
    Atr_Sabor NVARCHAR(250) NOT NULL,
    Cod_Categoria NVARCHAR(50) NOT NULL,
    Desc_Marca NVARCHAR(250) NOT NULL,
    Desc_Categoria NVARCHAR(250) NOT NULL,
    PRIMARY KEY (ID_Produto)
);

CREATE TABLE Dim_Cliente (
    ID_Cliente INT NOT NULL,
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
    PRIMARY KEY (ID_Cliente)
);

ALTER TABLE Dim_Cliente COMMENT 'Tabela da dimensĂ£o cliente';

CREATE TABLE Dim_Tempo (
    ID_Tempo INT NOT NULL,
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
    PRIMARY KEY (ID_Tempo)
);

CREATE TABLE Dim_Fabrica (
    ID_Fabrica INT NOT NULL,
    Cod_Fabrica NVARCHAR(50) NOT NULL,
    Desc_Fabrica NVARCHAR(250) NOT NULL,
    PRIMARY KEY (ID_Fabrica)
);

CREATE TABLE Fato_Presidencia (
    ID_Tempo INT NOT NULL,
    ID_Fabrica INT NOT NULL,
    ID_Vendedor INT NOT NULL,
    ID_Cliente INT NOT NULL,
    ID_Produto INT NOT NULL,
    Faturamento DOUBLE PRECISION NOT NULL,
    Unidade_Vendida DOUBLE PRECISION NOT NULL,
    Quantidade_Vendida DOUBLE PRECISION NOT NULL,
    Imposto DOUBLE PRECISION NOT NULL,
    Custo_Variavel DOUBLE PRECISION NOT NULL,
    Custo_Frete DOUBLE PRECISION NOT NULL,
    Custo_Fixo DOUBLE PRECISION NOT NULL,
    Meta_Faturamento DOUBLE PRECISION NOT NULL,
    Meta_Custo DOUBLE PRECISION NOT NULL,
    PRIMARY KEY (ID_Tempo, ID_Fabrica, ID_Vendedor, ID_Cliente, ID_Produto)
);

ALTER TABLE Fato_Presidencia ADD CONSTRAINT dim_organizacional_fato_presidencia_fk
FOREIGN KEY (ID_Vendedor)
REFERENCES Dim_Organizacional (ID_Vendedor)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_Presidencia ADD CONSTRAINT produto_fato_presidencia_fk
FOREIGN KEY (ID_Produto)
REFERENCES Dim_Produto (ID_Produto)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_Presidencia ADD CONSTRAINT cliente_fato_presidencia_fk
FOREIGN KEY (ID_Cliente)
REFERENCES Dim_Cliente (ID_Cliente)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_Presidencia ADD CONSTRAINT tempo_fato_presidencia_fk
FOREIGN KEY (ID_Tempo)
REFERENCES Dim_Tempo (ID_Tempo)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE Fato_Presidencia ADD CONSTRAINT dim_fabrica_fato_presidencia_fk
FOREIGN KEY (ID_Fabrica)
REFERENCES Dim_Fabrica (ID_Fabrica)
ON DELETE NO ACTION
ON UPDATE NO ACTION;
```
