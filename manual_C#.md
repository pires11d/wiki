# C# - Noções básicas de orientação a objeto


## 1. Tipos de objetos 
~~~c#
// tipos principais:
int indice;
double numero;
string texto;
bool booleana;

// objeto genérico:
var objeto = new Objeto();

// objeto de uma classe (ex. Conta):
Conta c = new Conta();

// arrays:
int[] inteiros = new int[n];
double[] doubles = new double[n];
string[] strings = new string[n];
bool[] strings = new bool[n];
Conta[] contas = new Conta[n];

// listas:
List<Conta> lista = new List<Conta>(); 

// conjuntos:
HashSet<Conta> conjunto1 = new HashSet<Conta>();
SortedSet<Conta> conjunto2 = new SortedSet<Conta>();

// dicionários:
Dictionary<string,double> dict1 = new Dictionary<string,double>();
SortedDictionary<string,double> dict2 = new SortedDictionary<string,double>();
~~~

#

## 2. Loops
* com índices:
~~~c#
for(int i = 0; i < contas.Length; i++)
{
	Console.Write(contas[i].Saldo);
}
~~~

* sem índices:
~~~c#
foreach(Conta c in contas)
{
	Console.Write(contas[i].Saldo);
}
~~~

* em dicionários:
~~~c#
foreach(KeyValuePair<string,double> par in dict)
{
	Console.Write(par.Key + ":" + par.Value);
}
~~~

#

## 3. Getters e Setters de uma classe
Podemos adicionar uma propriedade com *get* e *set* a uma classe de duas maneiras, como no exemplo a seguir:

Dentro de um arquivo nomeado `Conta.cs`, escreva:

~~~c#
public class Conta
{
	private int numero;
	public int Numero
	{
		get
		{
			// codigo para ler a propriedade
			return this.numero;
		}
		set
		{
			// codigo para escrever na propriedade
			this.numero = value;
		}
	}

}
~~~
De maneira muito mais simplificada, seria:

~~~c#
public class Conta
{
	public int Numero { get; set; }
}
~~~

Criamos um objeto da classe *Conta* em `Program.cs` e assim podemos fazer o uso dos métodos *get* e *set*!
~~~c#
Conta c = new Conta()

// uso do get
c.Numero = 12345;

// uso do set
Console.Write(c.Numero);
~~~

#

## 4. Construtores de uma classe
No arquivo `Cliente.cs`, criamos o construtor que receberá dois argumentos:
~~~c#
class Cliente 
{
	public string Nome { get; set; }
	public int Idade { get; set; }

	// construtor que recebe o nome e a idade
	public Cliente (string nome, int idade)	{
		this.Nome = nome;
		this.Idade = idade;
	}
}
~~~
Podemos também deixar a escolha de preenchimento dos argumentos no construtor da classe *Cliente* ser **opcional**, como a seguir:
~~~c#
class Cliente 
{
	public string Nome { get; set; }
	public int Idade { get; set; }

	// construtor que recebe o nome e a idade
	public Cliente (string nome, int idade)	{
		this.Nome = nome;
		this.Idade = idade;
	}
	// construtor que não recebe argumentos
	public Cliente () {	}
}
~~~
Assim podemos instanciar objetos da classe *Cliente* de duas maneiras, no arquivo `Program.cs`:
~~~c#
Cliente c1 = new Cliente();

Cliente c2 = new Cliente("Lucas", 26);
~~~

#

## 5. Métodos de uma classe
No arquivo `Conta.cs`, temos a classe *Conta* que possui os métodos *Saca* e *Deposita*:
~~~c#
public class Conta 
{
	public int Numero { get; set;}
	public double Saldo { get; private set; }
	public Cliente Titular { get; set; }

	// metodo responsável pela realização de um saque
	public void Saca(double valor)
	{
		this.Saldo -= valor;
	}

	// metodo responsável pela realização de um depósito
	public void Deposita(double valor)
	{
		this.Saldo += valor;
	}
}
~~~
Note que ambos os métodos alteram o valor da propriedade *Saldo*!


#

## 6. Classe abstrata
Podemos tornar a classe *Conta* abstrata:

No arquivo `Conta.cs`, criamos o método ***virtual*** *Saca*:
~~~c#
public abstract class Conta  
{
	public virtual void Saca(double valor)
	{
		this.Saldo -= valor;
	}
	
}
~~~

Isto permite que outra classe qualquer herde todos os métodos e propriedades da classe pai (*Conta*) sem ter que reescrevê-los. 

#

## 5. Herança

Classes herdam todos os atributos e propriedades da classe pai, **EXCETO** seu construtor!

Podemos fazer com que os outros tipos de conta sempre tenham um pai comum, a classe abstrata *Conta*.

Aí, no arquivo `ContaPoupanca.cs`, quando formos implementar o método *Saca* (da seção anterior) de maneira exclusiva para a classe *ContaPoupanca*, precisamos usar o ***override***, alterando portanto o método padrão *Saca* da classe pai *Conta*:
~~~c#
public class ContaPoupanca : Conta
{
	public override void Saca(double valor)
	{
		this.Saldo -= (valor + 0.10);
	}
	
}
~~~
Outra maneira seria:
~~~c#
public class ContaPoupanca : Conta
{
	public override void Saca(double valor)
	{
		base.Saca(valor + 0.10);
	}
	
}
~~~

#

## 6. Interfaces
No arquivo `ITributavel.cs`
~~~c#
public interface ITributavel
{
	double CalculaTributo();
}
~~~
No arquivo `ContaPoupanca.cs`
~~~c#
public class ContaPoupanca : Conta, ITributavel
{
	public double CalculaTributo() // sem a necessidade de override!
	{
		return this.Saldo * 0.02;
	}
}
~~~

#

## 7. Métodos estáticos
No arquivo `ContaCorrente.cs`, podemos criar o atributo estático *totalDeContas* que terá um valor inicial de 0 para todos os objetos da classe *ContaCorrente*, usando a palavra ***static***:
~~~c#
public class ContaCorrente : Conta
{
	private static int totalDeContas = 0;
	
	// método que adiciona +1 ao valor de totalDeContas, cada vez que for criada uma nova ContaCorrente
	public ContaCorrente
	{
		ContaCorrente.totalDeContas++;
	}
}
~~~

#

## 8. Namespaces
O Diretório `Contas/` poderia conter o arquivo `Contas.cs`:
~~~c#
namespace Contas
{
	public class Conta
	{
		//...
	}
	public class ContaCorrente : Conta 
	{
		//...
	}
	public class ContaPoupanca : Conta 
	{
		//...
	}
}
~~~
Ou poderia conter cada classe separada em múltiplos arquivos:
- `Contas/Conta.cs` 
	~~~c#
	namespace Contas
	{
		public class Conta
		{
			//...
		}
	}
	~~~
- `Contas/ContaCorrente.cs`
	~~~c#
	namespace Contas
	{
		public class ContaCorrente : Conta 
		{
			//...
		}
	}
	~~~
- `Contas/ContaPoupanca.cs`
	~~~c#
	namespace Contas
	{
		public class ContaPoupanca : Conta 
		{
			//...
		}
	}
	~~~

E assim, podemos fazer referência ao namespace criado, importando-o no arquivo `Program.cs`:
~~~c#
using Contas;
~~~

#

## 9. Exceções

No arquivo `Conta.cs` temos um método qualquer como exemplo: 
~~~c#
public void MyMethod(){
	if (condicao1){
		throw new Exception();
	}
	else if (condicao2) {
		throw new SpecialException();
	}
	else {
		// ação padrão do método
		//...
	}
}
~~~

E no arquivo `Program.cs`, podemos utilizar um *try/catch* para executar este método, evitando erros de compilação:
~~~c#
Conta c = new Conta();

try {
	c.MyMethod();
}
catch (Exception ex){
	// tratamento para exceções default
	//...
}
catch (SpecialException ex){
	// tratamento para exceções especiais
	//...
}
~~~

E ainda podemos criar um arquivo com exceções customizadas, como por exemplo `MyExceptions.cs`:
~~~c#
public class SpecialException : Exception {
	//...
}
~~~

#

## 10. Métodos de string

- Metodos mais comuns (a string original nunca eh modificada!):
~~~c#
string maiusculo = conteudo.ToUpper();
string minusculo = conteudo.ToLower();
string lista = conteudo.Split(",");
string textonovo = conteudo.Replace("","\n");
string finaldotexto = conteudo.Substring(conteudo.IndexOf(" "));
~~~

- Sobrescrevendo métodos:
~~~c#
public override string ToString()
{
	//...
}
~~~

- Exemplo de uma funcionalidade "Find & Replace":
~~~c#
// botao "Find and Replace"
private void botaoReplace_Click(object sender, EventArgs e)
{
	string conteudoNovo = textoNovo.Text;
	int inicioSelecao = textoConteudo.SelectionStart;
	int tamanhoSelecao = textoConteudo.SelectionLength;
	string textoSelecionado = textoConteudo.Text.Substring(inicioSelecao,tamanhoSelecao);
	string antes = textoConteudo.Text.Substring(0,inicioSelecao);
	string depois = textoConteudo.Text.Substring(inicioSelecao + tamanhoSelecao);
	textoConteudo.Text = antes + conteudoNovo + depois;
}
~~~

#

## 11. Extensões de uma classe 
Exemplo: Adicionando a extensão "Pluralize" para uma string:
~~~c#
public static class StringExtensions
{
	public static string Pluralize(string texto)
	{
		if(texto.EndsWith("s"))
		{
			return texto;
		}
		else
		{
			return texto + "s";
		}
	}
}
~~~

# 

## 12. LINQ (Language INtegrated Query)
~~~c#
// filtrando uma consulta
var filtradas = contas.Where((Conta c) => {return c.Saldo > 2000;});
//...ou
var filtradas = contas.Where(c => {return c.Saldo > 2000;});
//...ou
var filtradas = contas.Where(c => c.Saldo > 2000;);

// funcao anonima (lambda)
(Conta c) => {return c.Saldo > 2000;};

// metodos matemáticos padrão
double totalSaldo = contas.Sum(c => c.Saldo);
double mediaSaldo = contas.Average(c => c.Saldo);
double minimoSaldo = contas.Sum(c => c.Saldo);
double maximoSaldo = contas.Sum(c => c.Saldo);
int numero = contas.Count();

// consultando com SQL-like queries
var filtradas = from c in contas
				where c.Saldo > 2000;
				orderby c.Titular.Nome descending;
				select c;
~~~

#

## 13. Biblioteca System.IO

- Lendo um arquivo texto
~~~c#
using System.IO;
string arquivo = "arquivo.txt";

if (File.Exists(filename))
{
	Stream entrada = File.Open(arquivo, FileMode.Open);
	StreamReader leitor = new StreamReader(entrada);
	string linha = leitor.ReadLine();
	while(linha != null)
	{
		linha = leitor.ReadLine()
		Console.Write(linha)
	}
	leitor.Close();
	entrada.Close();
}
~~~

- Escrevendo um arquivo texto:
~~~c#
using System.IO;
string arquivo = "arquivo.txt";

Stream saida = File.Open(arquivo, FileMode.Create);
StreamWriter escritor = new StreamWriter(saida);
escritor.WriteLine("texto a ser escrito")
escritor.Close();
saida.Close();
~~~

- Escolhendo um diretório:
~~~c#
string pasta = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

string caminho = Path.Combine(pasta, "arquivo.txt");
~~~

- Utilizando "using" para qualquer interface *IDisposable*:
~~~c#
using System.IO;
string arquivo = "arquivo.txt";

using(Stream arquivoStream = File.Open(arquivo, FileMode.Open))
{
	// o arquivo apenas ficara aberto aqui dentro
};

using(StreamReader leitor = new StreamReader(arquivo))
{
    // aqui dentro voce pode utilizar tanto o leitor quanto o arquivo
};

using(StreamWriter escritor = new StreamWriter(arquivo))
{
    // aqui dentro voce pode utilizar tanto o escritor quanto o arquivo
};
~~~

#

## 14. Biblioteca System.Data.SqlClient


Namespaces necessários:
~~~c#
using System.Data;
using System.Data.SqlClient;
~~~

Construindo a string de conexão:
~~~c#
// informações principais
string server = "localhost";
string username = "usuario";
string password = "senha";
string database = "banco de dados";

// montagem da string de conexão
string connectionString = "Data Source=" + server + ";";
connectionString += "User ID=" + username + ";";
connectionString += "Password=" + password + ";";
connectionString += "Initial Catalog=" + database;
~~~
E a string da query SQL:
~~~c#
string commandString = "SELECT * FROM contas";
~~~

Criando uma instância do objeto SqlConnection com a string de conexão como argumento:
~~~c#
SqlConnection con = null;
SqlCommand cmd = null;
try
{
	// conexão com o banco
	con = new SqlConnection(connectionString);
    con.Open();
	// comando SQL
	cmd = new SqlCommand(commandString, con);	
	// execução do comando
	SqlDataReader dr = cmd.ExecuteReader(); 
	// lendo o que a consulta retornou
	while (dr.Read())
	{
		//...
	}
}
catch (Exception Ex)
{
	MessageBox.Show(Ex.Message);
}
finally
{
    if (null != com);
        cmd.Dispose();
    if (null != con)
        con.Dispose();
}
~~~

Ou de maneira simplificada, com o *using*:
~~~c#
// conexão com o banco
using (SqlConnection con = new SqlConnection(connectionString))
{
	// comando SQL
    using (SqlCommand cmd = new SqlCommand(commandString, con))
    {
        con.Open();		
		
		SqlDataReader dr = cmd.ExecuteReader();

		while (dr.Read())
		{
			//...
		}
	}
}
~~~

>**OBS**: As Classes *SqlConnection* e *SqlCommand* implementam a interface *IDisposable* e isto significa que eles podem usar recursos não gerenciados e liberar tais recursos é trabalho do desenvolvedor, de forma que depois de usar estas classes temos que chamar o método *Dispose*(). Se ocorrer uma exeção no acesso ao banco de dados temos que ter certeza que o *Dispose*() foi chamado, e este é um motivo para usar a palavra reservada ***using***.

Possíveis estados de uma conexão com o banco (*SqlConnection.State*):
- Broken
- Closed
- Connecting
- Executing
- Fetching
- Open


