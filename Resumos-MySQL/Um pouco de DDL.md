# Um pouco sobre a estruturas de tabelas e comandos DDL
### Isso foi utilizado em um Curso\Formação na Alura

|-----------------------------------------------------------------------------|


CREATE DATABASE - Cria o banco de Dados

DROP DATABASE - Deleta o banco de Dados

CREATE DATABASE IF NOT EXISTS - Com o IF NOT EXISTS ele criará o Banco de Dados caso 
outro banco de dados não exista com esse nome.

DROP DATABASE IF EXISTS - IF EXISTS apagará um Banco de Dados, caso ele exista.

USE (Banco de Dados) - Utiliza o Banco de Dados selecionado.

CHARACTER SET - Define o tipo de caracteres que serão aceitos no Banco de dados. UTF-8 é o nosso podr ter acentuações.


```
CREATE DATABASE vendas_sucos;

CREATE DATABASE vendas_sucos2
CHARACTER SET = utf8;

CREATE DATABASE IF NOT EXISTS vendas_sucos2;

DROP DATABASE IF EXISTS vendas_sucos2;

USE VENDAS_SUCOS;

```

CREATE TABLE - Cria a tabela. E dentro dela precisamos nomear os campos, os tipos de dados que cada uma vai receber e outras configurações, como: PRIMARY KEY ou FOREIGN KEY, UNIQUE, AUTO_INCREMENT, NULL ou NOT NULL.

Alguns tipos de dados aceitos, são: 

VARCHAR() - Que aceita STRINGS, e dentro do parenteses, colocamos a quantidade de caracteres aceitos nesse campo.

FLOAT - Campo que aceita numeros com um ponto flutuante, não serão numeros inteiros.

INT  - Recebe numeros inteiros.

BIT - Campo binário. No exemplo abaixo, 1 é TRUE e 0 é FALSE

DATE - Aceita datas no formato "2023-10-17"

Como restrições nos campos:

PRIMARY KEY - Cria um campo único, no qual não pode ser copiado e pode ser utilizado para realizar consultas relacionais com outras tabelas.

FOREIGN KEY - Cria um campo que será recebido por outra tabela, tambem para realizar consultas relacionais. Quem irá receber seu campo dependerá da relação em que as tabelas possuem : 1 para 1, 1 para Muitos ou Muitos para Muitos.

AUTO_INCREMENT - Não necessita ser preenchido. Ele toma como ultimo dado o ultimo registro e adiciona mais 1. Você precisa apenas deixar como DEFAULT na hora de inserir o dado e o AUTO_INCREMENT faz seu trabalho. (CUIDADO: Essa sequência pode ser forçada a iniciar de um numero específico e a partir daí o MySQL, vai continuar dele. Por Exemplo: Se eu forço a sequência dele a iniciar de 100, meu próximo registro será 101, mesmo que eu preencha no próximo cadastro com o numero 2, meu proximo cadastro com AUTO_INCREMENT será 102 e não 3.)

NULL - Aceita campos vazios.

NOT NULL - Não aceita campos vazios.

UNIQUE - Criaa um campo único, similar ao PRIMARY KEY, contudo não pode ser usado para relacionamento entre tabelas.

```
CREATE TABLE PRODUTOS (
CODIGO VARCHAR(10) NOT NULL ,
DESCRITOR VARCHAR(100) NULL,
SABOR VARCHAR(50) NULL,
TAMANHO VARCHAR (50) NULL,
EMBALAGEM VARCHAR (50) NULL,
PRECO_LISTA FLOAT NULL,
PRIMARY KEY (CODIGO));

CREATE TABLE VENDEDORES(
MATRICULA VARCHAR (5) NOT NULL,
NOME VARCHAR (100) NULL,
BAIRRO VARCHAR (50) NULL,
COMISSAO FLOAT NULL,
DATA_ADMISSAO DATE NULL,
FERIAS BIT (1) NULL,
PRIMARY KEY(MATRICULA));

CREATE TABLE TABELA_DE_VENDAS(
NUMERO VARCHAR(5) NOT NULL,
DATA_VENDA DATE NULL,
CPF VARCHAR(11) NOT NULL,
MATRICULA VARCHAR(5) NOT NULL,
IMPOSTO FLOAT NULL,
PRIMARY KEY (NUMERO));

CREATE TABLE ITENS_NOTAS(
NUMERO VARCHAR (5) NOT NULL,
CODIGO VARCHAR (10) NOT NULL,
QUANTIDADE INT,
PRECO FLOAT,
PRIMARY KEY (NUMERO, CODIGO));

```
ALTER TABLE - Altera a estrutura da tabela. Após utilizar o ALTER TABLE precisa ser nomeado o que será mudado.

RENAME COLUMN - Muda o nome da coluna. O commando seria: RENAME COLUMN (CAMPO 1) to (CAMPO 2).

RENAME (Novo nome da tabela) - Exemplo ALTER TABLE tabela RENAME (Novo nome da tabela).

ADD CONSTRAINT - Adiciona uma constraint, no exemplo FOREIGN KEY, FK_nome da tabela, e o campo precisa ser referenciado com FOREIGN KEY (Campo) REFERENCES Tabela (CAMPO na tabela referenciada). Exemplo abaixo.

```
ALTER TABLE VENDEDORES
RENAME COLUMN ADIMISSAO TO ADMISSAO;

ALTER TABLE TABELA_DE_VENDAS
ADD CONSTRAINT FK_CLIENTES
FOREIGN KEY (CPF) REFERENCES CLIENTES (CPF);

ALTER TABLE tabela_de_vendas
ADD CONSTRAINT FK_VENDEDORES
FOREIGN KEY (MATRICULA) REFERENCES VENDEDORES (MATRICULA);

ALTER TABLE tabela_de_vendas
RENAME NOTAS; 

ALTER TABLE ITENS_NOTAS
ADD CONSTRAINT FK_NOTAS
FOREIGN KEY (NUMERO) REFERENCES NOTAS(NUMERO);

ALTER TABLE ITENS_NOTAS
ADD CONSTRAINT FK_PRODUTOS
FOREIGN KEY (CODIGO) REFERENCES PRODUTO(CODIGO);

```
