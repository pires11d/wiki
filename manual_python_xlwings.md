# Python - xlwings
> Autor: Lucas Joshua Pires


## 1. Instalando o pacote xlwings
* Instale o pacote principal
~~~
pip install xlwings
~~~

Caso não funcione a instalação, é sinal de que algum pacote está faltando.
Instale o pacote recomendado pelo prompt e repita o comando, que agora deverá funcionar normalmente.

Exemplo: 
~~~
pip install pypiwin32
~~~

* Instale o Add-in do pacote xlwings
~~~
xlwings addin install
~~~
	
* Instale o RunPython do pacote xlwings
~~~
xlwings runpython install
~~~

## 2. Como criar uma planilha (vazia) vinculada a um arquivo Python
* Na pasta local que desejar criar o projeto, digite o comando
~~~
xlwings quickstart nome_do_projeto
~~~

Dois arquivos serão criados, no diretório que for escolhido pelo terminal, dentro da pasta de mesmo nome:

`nome_do_projeto.xlsm`

`nome_do_projeto.py`
	
## 3. Como vincular uma planilha existente ao xlwings

- Primeiro, abra o editor do Visual Basic (Alt+F11)
- Em Project - VBAProject, localizado na esquerda do editor, 
	clique com o botão direito e em **Import file...**
- Importe os arquivos **xlwings** e **xlwings_udfs**
- Feche o editor
- Agora, vá em **File > Options > Trust Center > Trust Center Settings > Macro Settings**
- Em **Developer Macro Settings**, habilite a opção:
  - `Trust access to the VBA project object model`
	
	
	
	