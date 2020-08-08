# Banco de Dados - MySQL
> Autor: Lucas Joshua Pires

## 1. Acessando o serviço
Inicie o serviço
~~~
sudo service postgresql start
~~~

Acesse o terminal com qualquer um dos 3 seguintes comandos:
~~~
sudo -u postgres psql
~~~
~~~
sudo su - postgres
psql
~~~
~~~
sudo psql -Upostgres
~~~

## 2. Criando um banco de dados

~~~ postgresql
CREATEDB name_of_db;
~~~
~~~ postgresql
CREATE ROLE nomeDoUser WITH CREATEDB LOGIN PASSWORD 'senhaDoUser';   
~~~

## 3. Executando uma query SQL

## Select
~~~ postgresql
SELECT select_list
FROM table_name;
~~~

## Insert
~~~ postgresql
INSERT INTO table_name (column_list)
VALUES
    (value_list_1),
    (value_list_2)
RETURNING * | output_expression;
~~~

## Update
~~~ postgresql
UPDATE table_name
SET column1 = value1,
    column2 = value2
WHERE condition;
~~~

## Delete
~~~ postgresql
DELETE FROM table_name
WHERE condition;
~~~