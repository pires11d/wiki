# PHP
> Autor: Lucas Joshua Pires

http://php.net

## 1. Rodando o servidor
~~~
cd path/to/webapp
~~~
- localmente
~~~	
php -S localhost:8080
~~~
- em toda a rede
~~~
php -S 0.0.0.0:8080
~~~

## 2. Acessando o servidor
http://localhost:8080

## 3. Exemplo de código
>OBS.: Mudar o formato dos arquivos *html* para *php*!
~~~php
<?php print date('Y') - 1932;  ?>
...ou...
<?= date(‘Y’) - 1932; ?>
~~~

## 4. Inclusao de Header & Footer
~~~php
<body>
<?php include("cabecalho.php"); ?>
...
<?php include(“rodape.php”); ?>
</body>
~~~
>OBS.: O cabeçalho precisa ter a tag `<header>`, e o rodapé a tag `<footer>`!

## 5. Variáveis, Scripts e Links
~~~php
<?php $cabecalho_css = '<link	rel="stylesheet" href="css/produto.css">'; ?>
~~~

~~~php
<?php print @$cabecalho_css; ?>
~~~
>OBS.: o @ printa apenas se a variavel existir!

## 6. Criando um Formulário
~~~php
<input	type="hidden" name="nome" value="Fuzzy	Cardigan">
<input	type="hidden" name="preco" value="129,00">
<form	action="checkout.php" method="POST">
~~~

## 7. Criando uma Lista de Definições
~~~php
<h2>Sua compra</h2>
<dl>
	<dt>Produto</dt>
	<dd><?= $_POST['nome'] ?></dd>
	<dt>Preço</dt>
	<dd>R$ <?= $_POST['preco'] ?></dd>
</dl>
~~~