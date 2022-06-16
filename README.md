Olá Sou a Thamyres
*/
DROP DATABASE IF EXISTS  aula_banco;

CREATE DATABASE aula_banco; -- criando a base de dados

USE  aula_banco;

CREATE TABLE estado(
id INT NOT NULL AUTO_INCREMENT,
nome VARCHAR(200) NOT NULL UNIQUE , -- CONSTRAINT INLINE 
sigla CHAR(2) NOT NULL UNIQUE,
ativo CHAR(1)  NOT NULL DEFAULT 'S',
data_cadastro datetime  NOT NULL DEFAULT CURRENT_TIMESTAMP,
-- CHECK (ativo IN ('S','N'))  -- CONSTRAINT OUT OF LINE - regra sem nome 
CONSTRAINT coluna_ativo_deve_ser_S_ou_N CHECK (ativo IN ('S','N')), -- regra com nome
CONSTRAINT pk_estados PRIMARY KEY (id)
);

INSERT INTO estado (id,nome,sigla,ativo,data_cadastro) VALUES ('1','GOIÁS','GO','S','2022-06-16');
INSERT INTO estado (id,nome,sigla,ativo,data_cadastro) VALUES ('2','PARANÁ','PR','S','2022-06-16');
INSERT INTO estado (id,nome,sigla,ativo,data_cadastro) VALUES ('3','SÃO PAULO','SP','S','2022-06-16');

-- Definição automática 

INSERT INTO estado (nome,sigla) VALUES ('AMAPÁ','AP');
INSERT INTO estado (nome,sigla) VALUES ('Rio Grande Do Sul','RS');

SELECT id,nome,sigla,ativo,data_cadastro FROM estado;
