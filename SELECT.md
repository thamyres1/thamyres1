DROP DATABASE IF EXISTS aula_banco; 
CREATE DATABASE aula_banco; 		
USE aula_banco;						

CREATE TABLE estado( 				
id INT NOT NULL AUTO_INCREMENT
,nome VARCHAR(200) NOT NULL UNIQUE  
,sigla CHAR(2) NOT NULL UNIQUE
,ativo ENUM('S','N') NOT NULL DEFAULT 'S'
,data_cadastro DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
,CONSTRAINT pk_estado PRIMARY KEY (id)  
);

CREATE TABLE cidade (				
id INT NOT NULL AUTO_INCREMENT
,nome VARCHAR(200)  NOT NULL
,ativo ENUM('S','N') NOT NULL DEFAULT 'S'
,data_cadastro DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
,estado_id INT NOT NULL 
,CONSTRAINT pk_cidade PRIMARY KEY (id)
,CONSTRAINT fk_cidade_estado FOREIGN KEY (estado_id) REFERENCES estado (id)
,CONSTRAINT cidade_unica UNIQUE(nome, estado_id)
);

INSERT INTO estado (nome,sigla) VALUES ('GOIÁS','GO');
INSERT INTO estado (nome,sigla) VALUES ('PARANA','PR');
INSERT INTO estado (nome,sigla) VALUES ('SÃO PAULO','SP');
INSERT INTO estado (nome,sigla) VALUES ('AMAPÁ','AP');
INSERT INTO estado (nome,sigla) VALUES ('RIO GRANDE DO SUL','RS');

INSERT INTO cidade (nome,estado_id) VALUES ('POSSE','1');
INSERT INTO cidade (nome,estado_id) VALUES ('CURITIBA','2');
INSERT INTO cidade (nome,estado_id) VALUES ('CAMPINAS','3');
INSERT INTO cidade (nome,estado_id) VALUES ('MACAPÁ','4');
INSERT INTO cidade (nome,estado_id) VALUES ('PORTO ALEGRE','5');


-- 1) Escreva o comando para seleccionar todos os registros da tabela estado com todas as colunas.
SELECT * 
FROM estado;

-- OU 
SELECT id, nome, sigla, ativo, data_cadastro 
FROM estado;

/*
O segundo comando é melhor na questão de legibilidade e desempenho
Quando colocamos * em SELECT (todas as colunas): 
(1)o SGBD não sabe quais colunas são da tabela.
Assim, ele terá que pesquisar no dicionário e descubrir;
(2) por muitas vezes, trabalhamos em muitos projetos nos quais, não conhecemos a estrutura do banco. 
Colocando os nomes das colunas na consulta fica fácil para qualquer pessoa entender.
*/

-- 2) Escreva o comando para seleccionar o nome e a sigla de todos os registros da tabela estado.

SELECT nome, sigla -- Basta especificar as colunas depois do select
FROM estado;

-- 3) Escreva o comando para seleccionar o nome e a sigla de todos os registros da tabela estado. Associe a tabela nas definições das colunas.

SELECT estado.nome, estado.sigla 
FROM estado;

/**
Em consultas, é muito comum que envolva varias tabelas. Associar a coluna com a tabela no qual pertence facilita a leitura do comando. 
Em consultas que envolve mais que uma tabela, nos quais, há colunas com o mesmo nome, é OBRIGATÓRIO especificar a tabela.
**/

-- 4) Escreva o comando para seleccionar o nome e a sigla de todos os registros da tabela estado.  Por meio da definição do apelido, associe a tabela nas definições das colunas. 

SELECT e.nome, e.sigla 
FROM estado e;

/*
SELECT estado.nome, estado.sigla 
FROM estado e; -- 
>>> ERRADO - na referência da tabela da coluna, deveria ser utilizado o apelido
SELECT estado.nome, e.sigla 
FROM estado e; 
>>> ERRADO - A referência da tabela da coluna nome (estado.nome), deveria ser utilizado o apelido (e.nome)
-- Pode-se definir o apelido para tabela, bastando apenas colocar o apelido logo depois da tabela. Isso reduz a escrita na associação da tabela na referência da coluna.
**/

-- 5) Escreva o comando para seleccionar o nome e a sigla de todos os registros da tabela estado.  Por meio da definição do apelido, associe a tabela nas definições das colunas.  Redefine a descrição da coluna nome para nome_estado e sigla para sigla estado.

SELECT e.nome AS nome_estado, e.sigla AS 'sigla estado' 
FROM estado e;
-- OU 
SELECT e.nome nome_estado, e.sigla AS 'sigla estado' FROM 
estado e;
-- OU 
SELECT e.nome nome_estado, e.sigla 'sigla estado' 
FROM estado e;

/**
Para redefinir a descrição das colunas, basta utilizar a palabra chave “as” e o nome que deseja. A palavra chave “as” é opcional. 
Quando o nome possui mais que uma palvra é necessário delimitar, colocando aspas no início e fim.
**/


/*
AGORA É A SUA VEZ!!!! Para que você aprenda, é muito importante que não copie e cole, digite os comandos e mentalize o que está fazendo na medida que digita cada comando. Uma dica importante é que você digite primeiro no bloco de notas, com intuito de testar se realmente consegue digitar os comandos sem a ajuda do IDE – depois teste os comandos.
6.	Escreva o comando para seleccionar todos os registros da tabela cidade com todas as colunas.
7.	Escreva o comando para seleccionar o nome de todos os registros da tabela cidade.
8.	Escreva o comando para seleccionar o nome de todos os registros da tabela cidade.  Associe a tabela nas definições das colunas.
9.	Escreva o comando para seleccionar o nome  de todos os registros da tabela cidade.  Por meio da definição do apelido, associe a tabela nas definições das colunas.
10.	Escreva o comando para seleccionar o nome de todos os registros da tabela cidade.  Por meio da definição do apelido, associe a tabela nas definições das colunas.  Redefine a descrição da coluna nome para nome_cidade.
11.	Escreva o comando para seleccionar o nome de todos os registros da tabela cidade.  Por meio da definição do apelido, associe a tabela nas definições das colunas.  Redefine a descrição da coluna nome para nome da cidade.
12.	DESAFIO!!! Elabore uma consulta bem legal de forma que utilize todos os conhecimentos que adquiriu nesta aula. Mentalize o resultado com o que está fazendo  e depois valide o resultado.
*/
-- 06 
SELECT * FROM cidade;
-- 07
SELECT nome,ativo,data_cadastro,estado_id FROM cidade;
-- 08
SELECT cidade.nome
,cidade.ativo
,cidade.data_cadastro
,cidade.estado_id
 FROM cidade;
-- 09
SELECT cidade.nome  'NOME DA CIDADE'
,cidade.ativo  'CIDADE ATIVA OU NÃO'
,cidade.data_cadastro  'QUE DIA FUNDOU'
,cidade.estado_id  'NUMERO DO ESTADO PERTECENTE '
 FROM cidade;
-- 10
SELECT cidade.nome  nome_cidade
,cidade.ativo  
,cidade.data_cadastro
,cidade.estado_id 
 FROM cidade;
-- 11
SELECT cidade.nome  'nome da cidade'
,cidade.ativo  
,cidade.data_cadastro
,cidade.estado_id 
 FROM cidade;
-- 12
SELECT cidade.nome  'MUNICÍPIO'
,cidade.ativo  'CIDADE VIVA OU NÃO'
,cidade.data_cadastro  'QUE DIA ACORDOU'
,cidade.estado_id  'NUMERO DO ESTADO PERTECENTE '
FROM cidade;
