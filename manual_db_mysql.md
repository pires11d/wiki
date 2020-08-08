# Banco de Dados - MySQL
> Autor: Lucas Joshua Pires

## 1. Acessando o serviço
Inicie o serviço
~~~
sudo service mysqld start
~~~

Acesse o terminal
~~~
mysqld –u root –p
~~~

## 2. Criando um banco de dados

Criar banco de dados (ou schema):
~~~ sql
CREATE nome_do_banco
~~~

~~~ sql
USE nome_do_schema
~~~

Criar tabela:
~~~ sql
CREATE TABLE tarefas (
    id          INTEGER AUTO_INCREMENT PRIMARY KEY,
    nome        VARCHAR(20) NOT NULL,
    descricao   TEXT,
    prazo       DATE,
    prioridade  INTEGER(1),
    concluida   BOOLEAN
);
~~~

Inserindo colunas adicionais:
~~~ sql
ALTER TABLE tarefas ADD coluna_7 TEXT NULL;
~~~

## 3. Executando uma query SQL

## SELECT
~~~ sql
SELECT 
    nome, 
    descricao
FROM
    tarefas
WHERE
    concluida = TRUE
ORDER BY RAND()
LIMIT 1;
~~~

## INSERT
~~~ sql
INSERT INTO tarefas
(nome, descricao, prioridade)
VALUES
('Estudar PHP', 'Continuar meus estudos de PHP e MySQL', 1)
~~~

## UPDATE
~~~ sql
UPDATE tarefas
SET prioridade = 3
WHERE id = 2 
~~~

## DELETE
~~~ sql
DELETE FROM tarefas
WHERE concluida = TRUE 
~~~

# 4. phpMyAdmin
Criar usuário **admin**:

Tarefas > Privilégios > Adicionar Usuário