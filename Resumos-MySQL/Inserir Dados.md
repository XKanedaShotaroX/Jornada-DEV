
# Um pouco sobre inserção de dados em tabelas
### Isso foi utilizado em um Curso\Formação na Alura

|-----------------------------------------------------------------------------|

INSERT INTO - Insere dados na Tabela. O commando seria INSERT INTO tabela (CAMPO 1, CAMPO 2, etc...) VALUES (VALOR 1, VALOR 2, ETC...) (NOTA: A ordem dos dados a sere inseridos precisa ser a mesma dos campos. Caso contrário, dá erro.) Exemplos abaixo.

```
INSERT INTO PRODUTOS (CODIGO, DESCRITOR, SABOR , TAMANHO, EMBALAGEM, PRECO_LISTA)
VALUES ('1040107','Light - 350ml - Melancia', 'Melancia', '350ml', 'Lata', 4.56); 

INSERT INTO PRODUTOS (CODIGO, DESCRITOR, SABOR , TAMANHO, EMBALAGEM, PRECO_LISTA)
VALUES ('1040108','Light - 350ml - Graviola', 'Graviola', '350ml', 'Lata', 4.00); 

INSERT INTO PRODUTOS
VALUES ('1040110','Light - 350ml - Jaca', 'Jaca', '350ml', 'Lata', 6.00),
	   ('1040111','Light - 350ml - Manga', 'Manga', '350ml', 'Lata', 3.50);
       
INSERT INTO CLIENTES
VALUES ('19290992743','Fernando Cavalcante','R. Dois de Fevereiro','Água Santa','Rio de Janeiro', 'RJ', '22000000', '2000-02-12', 18 ,'M', 100000 , 20000 , 1),
       ('2600586709','César Teixeira','Rua Conde de Bonfim','Tijuca','Rio de Janeiro', 'RJ', '22020001', '2000-03-12', 18 ,'M', 120000 ,  22000 , 0);

```
O exemplo abaixo mostra como podemos utilizar uma consulta para adicionar dados a uma tabela. É um conceito um pouco mas complexo, mas útil. Nesse caso você utiliza INSERT INTO (Pesquisa utilizando SELECT) Exemplo abaixo.

Caso for utilizar uma alias, o alias precisa ter o mesmo nome da tabela de destino e tambem respeitar a mesma ordem dos campos e destino.
Exemplo abaixo.
```
SELECT * FROM CLIENTES;

SELECT * FROM sucos_vendas.tabela_de_produtos;

SELECT CODIGO_DO_PRODUTO AS CODIGO, NOME_DO_PRODUTO AS DESCRITOR, EMBALAGEM, TAMANHO, SABOR, PRECO_DE_LISTA AS PRECO_LISTA FROM sucos_vendas.tabela_de_produtos
WHERE CODIGO_DO_PRODUTO NOT IN (SELECT CODIGO FROM PRODUTOS); 

INSERT INTO PRODUTOS (SELECT CODIGO_DO_PRODUTO AS CODIGO, NOME_DO_PRODUTO AS DESCRITOR, SABOR, TAMANHO, EMBALAGEM, PRECO_DE_LISTA AS PRECO_LISTA FROM sucos_vendas.tabela_de_produtos
WHERE CODIGO_DO_PRODUTO NOT IN (SELECT CODIGO FROM PRODUTOS));

INSERT INTO CLIENTES (SELECT CPF, NOME, ENDERECO_1 AS ENDERECO, BAIRRO, CIDADE, ESTADO, CEP, DATA_DE_NASCIMENTO AS DATA_NASCIMENTO, IDADE, SEXO, LIMITE_DE_CREDITO AS LIMITE_CREDITO, VOLUME_DE_COMPRA AS VOLUME_COMPRA, PRIMEIRA_COMPRA FROM SUCOS_VENDAS.TABELA_DE_CLIENTES
WHERE CPF NOT IN (SELECT CPF FROM CLIENTES));

```
