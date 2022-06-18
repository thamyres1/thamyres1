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

CREATE TABLE cliente (
id INT ,
nome VARCHAR(200) NOT NULL,
ativo CHAR(1) NOT NULL DEFAULT 'S',
data_cadastro DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);


CREATE TABLE item_caixa(
id INT NOT NULL AUTO_INCREMENT
,nome VARCHAR(200) NOT NULL UNIQUE 
,preço VARCHAR(200) NOT NULL UNIQUE 
,por_quilo ENUM('SIM','NÃO') NOT NULL DEFAULT 'SIM'
,ativo ENUM('S','N') NOT NULL DEFAULT 'S'
,data_cadastro DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
,CONSTRAINT pk_item_caixa PRIMARY KEY (id)  
);


-- 1) Escreva o comando para inserir um registro da tabela estado com todas as colunas. 
INSERT INTO estado VALUES (NULL,'ACRE','AC','S','2021-05-01'); 
/* 
Como id é um campo com auto incremento, definimos NULL no comando.
Como estamos inserindo todas as colunas não precisamos informar a descrição das colunas. 
Porém, devemos informar os dados na sequência correta 
**/ 

-- 2) Escreva o comando para inserir um registro da tabela estado, definindo todos os dados, exceto a  chave primária que é auto incremento.  
INSERT INTO estado (nome,sigla,ativo,data_cadastro) 
VALUES ('ALAGOAS','AL','S','2021-05-02'); 
-- Como não estamos informando todos os dados, é necessário especificar de quais colunas são 

-- 3) Escreva o comando para inserir um registro da tabela estado, definindo somente os dados  necessários.  
INSERT INTO estado (nome,sigla) VALUES ('AMAPÁ','AP'); 
/** 
id → não precisa informar porque é auto incremento  
ativo e data_cadastro → não precisa informar porque possui o valor padrão  
**/ 

-- 4) Escreva o comando para inserir registros da tabela cidade das 3 formas apresentadas nos exercícios  anteriores.  
-- O registro de uma cidade requer a referência do estado (cidade é dependente  do estado). Assim, é necessário, primeiro, fazer a inserção dos estados. 
INSERT INTO cidade (id,nome,estado_id,ativo,data_cadastro) VALUES (NULL, 'ACRELANDIA',1,'S','2021-04-28'); 
INSERT INTO cidade (nome,estado_id,ativo,data_cadastro) VALUES ('ASSIS  BRASIL',1,'S','2021-03-14'); 
INSERT INTO cidade (nome,estado_id) VALUES ('BRASILEIA',1);

/*
AGORA É A SUA VEZ!!!! Para que você aprenda, é muito importante que não copie e cole,  digite os comandos e mentalize o que está fazendo na medida que digita cada comando. Uma dica  importante é que você digite primeiro no bloco de notas, com intuito de testar se realmente  consegue digitar os comandos sem a ajuda do IDE – depois teste os comandos. 
5. Escreva o comando para inserir 3 registros da tabela estado com todas as colunas. 
6. Escreva o comando para inserir 2 registros da tabela estado, definindo todos os dados, exceto a chave  primária que é auto incremento. 
7. Escreva o comando para inserir 2 registros da tabela estado, definindo somente os dados necessários. 
8. Escreva o comando para inserir registros da tabela cidade das 3 formas apresentadas nos exercícios  anteriores.  
9. Faça a inserção de 2 registros de cliente.  
10. DESAFIO!!! Tente fazer todas as inserções necessárias para que se tenha um item de caixa. Na medida  que esteja digitando o código, tente associar os dados inseridos com o contexto real.
*/

-- 05
INSERT INTO estado (id,nome,sigla,ativo,data_cadastro)
VALUES (4,'PARANÁ','PR','S','2022-04-18') , (5,'SÃO PAULO','SP','S','2022-04-18') , (6,'GOIÁS','GO','S','2022-04-18'); 
-- 06
INSERT INTO estado (id,nome,sigla,ativo,data_cadastro)
VALUES  (DEFAULT,'AMAZONAS','AM','S','2022-04-18') , (DEFAULT,'ESPÍRITO SANTO','ES','S','2022-04-18'); 
-- 07
INSERT INTO estado (nome,sigla) VALUES ('MATO GROSSO','MT') , ('RIO GRANDE DO SUL','RS') ; 
-- 08
INSERT INTO cidade (id,nome,ativo,data_cadastro,estado_id)
VALUES (4,'RIO BRANCO','S','2022-04-18',3) , (5,'CURITIBA','S','2022-04-18',4) , (6,'CAMPINAS','S','2022-04-18',5);

INSERT INTO cidade (id,nome,ativo,data_cadastro,estado_id)
VALUES  (DEFAULT,'POSSE','S','2022-04-18',6) , (DEFAULT,'MANAUS','S','2022-04-18',7); 

INSERT INTO cidade (nome,estado_id) VALUES ('SERRA','8') , ('SINOP','9') ; 
-- 09

INSERT INTO cliente (id,nome) VALUES (1,'SAUL') , (2,'PEDRO') ;
-- 10

INSERT INTO item_caixa (nome,preço) VALUES ('UVA','7,90'); 
INSERT INTO item_caixa (nome,preço) VALUES ('BANANA','2,90'); 
INSERT INTO item_caixa (nome,preço) VALUES ('MAÇA','7,78'); 
INSERT INTO item_caixa (nome,preço) VALUES ('LARANJA','10,90'); 
INSERT INTO item_caixa (nome,preço) VALUES ('PÊRA','3,90'); 
INSERT INTO item_caixa (nome,preço) VALUES ('KIWI','21,90'); 
INSERT INTO item_caixa (nome,preço) VALUES ('MELÃO','7,00'); 
INSERT INTO item_caixa (nome,preço) VALUES ('MAMÃO','6,60'); 
INSERT INTO item_caixa (nome,preço) VALUES ('MORANGO','23,33'); 
INSERT INTO item_caixa (nome,preço) VALUES ('CASTANHAS','23,99'); 

SELECT * FROM estado;
SELECT * FROM cidade;
SELECT * FROM cliente;
SELECT * FROM item_caixa;
