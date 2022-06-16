/**
Olá Sou a Thamyres
*/
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

INSERT INTO estado (nome,sigla) VALUES ('GOIÁS','GO');
INSERT INTO estado (nome,sigla) VALUES ('PARANÁ','PR');
INSERT INTO estado (nome,sigla) VALUES ('SÃO PAULO','SP');
INSERT INTO estado (nome,sigla) VALUES ('AMAPÁ','AP');
INSERT INTO estado (nome,sigla) VALUES ('Rio Grande Do Sul','RS');

SELECT id,nome,sigla,ativo,data_cadastro FROM estado;

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

INSERT INTO cidade (nome,estado_id) VALUES ('POSSE','1');
INSERT INTO cidade (nome,estado_id) VALUES ('Curitiba','2');
INSERT INTO cidade (nome,estado_id) VALUES ('Campinas','3');
INSERT INTO cidade (nome,estado_id) VALUES ('Macapá','4');
INSERT INTO cidade (nome,estado_id) VALUES ('Porto Alegre','5');


SELECT * FROM CIDADE;
