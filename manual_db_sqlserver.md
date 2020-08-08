# Banco de Dados - SQL Server
> Autor: Lucas Joshua Pires


## Select
~~~ sql server
SELECT *
FROM tblCliente
~~~

## Insert
~~~ sql server
INSERT
INTO tblCliente
VALUES('JOAO', 1900-01-20)
~~~

## Update
~~~ sql server
UPDATE tblCliente
SET Nome='joaozinho'
WHERE id = 5
~~~

## Delete
~~~ sql server
DELETE *
FROM tblCliente
WHERE Nome = 'JOAOZINHO'
~~~

## Join
~~~ sql server
SELECT tblPedido.id,
    tblPedido.id_produto,
    tblProduto.descricao
    tblPedido.id_cliente,
    tblCliente.nome,
    tblPedido.quantidade,
    tblPedido.valor
FROM tblPedido
JOIN tblCliente
ON tblPedido.id_cliente = tblCliente.id
JOIN tblProduto
ON tblPedido.id = tblProduto.id
~~~

