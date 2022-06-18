DROP DATABASE IF EXISTS  aula_banco;

CREATE DATABASE aula_banco;

USE  aula_banco;

CREATE TABLE estado(
id INT NOT NULL AUTO_INCREMENT,
nome VARCHAR(200) NOT NULL UNIQUE , -- CONSTRAINT INLINE 
sigla CHAR(2) NOT NULL UNIQUE,
ativo CHAR(1)  NOT NULL DEFAULT 'S',
data_cadastro datetime  NOT NULL DEFAULT CURRENT_TIMESTAMP,
CONSTRAINT coluna_ativo_deve_ser_S_ou_N CHECK (ativo IN ('S','N')),
CONSTRAINT pk_estados PRIMARY KEY (id)
);

INSERT INTO estado (nome,sigla) VALUES ('PARANÁ','PR');
INSERT INTO estado (nome,sigla) VALUES ('SÃO PAULO','SP');
INSERT INTO estado (nome,sigla) VALUES ('MATO GROSSO','MT');
INSERT INTO estado (nome,sigla) VALUES ('SANTA CATARINA','SC');
INSERT INTO estado (nome,sigla) VALUES ('RIO GRANDE DO SUL','RS');

CREATE TABLE cliente (
id INT ,
nome VARCHAR(200) NOT NULL,
ativo CHAR(1) NOT NULL DEFAULT 'S',
data_cadastro DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE cidade (
id INT NOT NULL AUTO_INCREMENT,
nome VARCHAR(200) NOT NULL,
ativo CHAR(1) NOT NULL DEFAULT 'S',
data_cadastro DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
estado_id INT NOT NULL,
CONSTRAINT pk_cidade PRIMARY KEY (id),
CONSTRAINT fk_cidade_estado FOREIGN KEY (estado_id) REFERENCES estado (id),
CONSTRAINT cidade_ativo_deve_ser_S_ou_N CHECK (ativo IN ('S','N')),
CONSTRAINT cidade_unica UNIQUE(nome,estado_id)
);
INSERT INTO cidade (nome, estado_id) VALUES ('BAURU',2);
INSERT INTO cidade (nome, estado_id) VALUES ('MARINGÁ',1);
INSERT INTO cidade (nome, estado_id) VALUES ('GUARULHOS',2);
INSERT INTO cidade (nome, estado_id) VALUES ('CAMPINAS',2);
INSERT INTO cidade (nome, estado_id) VALUES ('FLORIANÓPOLIS',4);
INSERT INTO cidade (nome, estado_id) VALUES ('PARANAVAÍ',1);
INSERT INTO cidade (nome, estado_id) VALUES ('CUIABA',3);
INSERT INTO cidade (nome, estado_id) VALUES ('BALNEÁRIO CAMBORIÚ',4);
INSERT INTO cidade (nome, estado_id) VALUES ('LONDRINA',1);
INSERT INTO cidade (nome, estado_id) VALUES ('CASCAVEL',1);
INSERT INTO cidade (nome, estado_id) VALUES ('JOINVILLE',4);
INSERT INTO cidade (nome, estado_id) VALUES ('PORTO ALEGRE',5);
INSERT INTO cidade (nome, estado_id) VALUES ('BLUMENAL',4);
INSERT INTO cidade (nome, estado_id) VALUES ('BARRA DOS GARÇAS',3);
INSERT INTO cidade (nome, estado_id) VALUES ('CHAPECÓ',4);
INSERT INTO cidade (nome, estado_id) VALUES ('ITAJAÍ',4);

SELECT * FROM estado,cidade;
-- EXECÍCIO 01
UPDATE estado SET nome = 'PARANÁ' WHERE id = 57;
-- 	EXERCÍCIO 02
UPDATE estado SET nome = 'PARANÁ' WHERE id = 57;
-- 	EXERCÍCIO 03
-- eu não soube fazer
-- 	EXERCÍCIO 04
SELECT id FROM estado WHERE nome = 'PARANÁ';

UPDATE cidade SET
nome = 'MARINGÁ'
, estado_id = 15
, ativo = 'N'
, data_cadastro = '2020-11-15'
WHERE id = 97;

SELECT * FROM cidade WHERE id = 97;
-- 	EXERCÍCIO 05
DELETE FROM estado WHERE id = 57;
-- 	EXERCÍCIO 06
ALTER TABLE estado DROP COLUMN nome;
-- 	EXERCÍCIO 07
DROP TABLE cliente;
-- 	EXERCÍCIO 08
DELETE FROM estado WHERE id = 23;
