# Linux - Comandos básicos no terminal
> Autor: Lucas Joshua Pires


command --help
	mostra todas as opções do comando específico
man command
	mostra o manual do comando específico

## Diretórios e Arquivos

* **pwd**	= mostra diretório atual
  
* **ls**	= lista os arquivos presentes no diretório
* **la** 	= lista todos os arquivos presentes no diretório (incluindo ocultos)
* **cd**	= mudar diretório onde o terminal está atuando para o caminho especificado
* **cp**	= copiar arquivo ou diretório
* **mv**	= mover arquivo ou diretório (caso +1 argumento for especificado, renomeia o arquivo)
* **rm**	= remover arquivo ou diretório
	* -r  remove recursivamente subdiretórios e arquivos
	* -f  forçar (ou --force)
	* -v  dá print em todos os nomes de arquivos (verbose mode)
* **mkdir**	= cria uma pasta no diretório atual
* **rmdir** 	= remove o diretório especificado
* **touch**	= cria um ou mais arquivos dentro do diretório atual
* **fold**	= encurta textos de linhas longas, para o número máximo de caracteres dado por:  
	* -w5 = 5 caracteres
* **whereis**	= mostra local do arquivo especificado
* **which** =  localiza o executável especificado na variável ambiente PATH
* **cat**	= printa o que estiver escrito dentro de um arquivo no terminal
* **less**	= mostra temporariamente o que estiver escrito dentro de um arquivo
* **head**	= printa as primeiras (-n) linhas do arquivo
* **tail**	= printa as ultimas (-n) linhas do arquivo
* **cut**	= printa as colunas (-f) delimitadas (-d) por algum separador (ex.: arquivo .csv)
* **grep**	= encontra e printa apenas a "palavra" que for especificada
	* -v faz o inverso!
* **uniq** 	= agrupa as palavras repetidas (-c) em um arquivo
* **echo**	= printa o texto escrito após o comando
	* Ex.: **echo "insert text here" > test.txt**
		
		substitui tudo o que estiver dentro do arquivo pelo texto	
	* Ex.: **echo "insert text here" >> test.txt**
		
		apenas adiciona o texto na última linha do arquivo
* **bash**	= Bourne-Again SHell, para abrir arquivos executáveis
* **ssh**	= Security SHell
* **su** 	= Super User, acessa o root
* **sudo**	= executa algum comando com o modo Super User
* **visudo** 	= edita o arquivo sudoers (controle de permissões p/ usuários)
* **gedit**	= abre o editor de texto do GNOME
* **nano**	= abre o editor via terminal

## Loops ##
* for variable in a b c; do echo $variable; done
  
* for file in $file_list; do echo $file; done
  
* for file in seasonal/*.csv; do grep -h 2017-07 $file; done


## Filesystem Hierarchy Standard (FHS)

* **/** = root directory
* **/root** = home of root user
* **/home** = home of users
* **/boot** = operating systems boot directory
* **/dev** = essential device files
* **/bin**	= essential binary files for all users
* **/sbin**	= essential system binaries
* **/lib**	= essential libraries for **/bin and **/sbin
* **/opt** = optional programs and applications
* **/run**	= Run-time variable data
* **/srv**	= site-specific data served by the system, web server scripts, version control systems
* **/media**	= mount points for removable media (CD/DVD/USB)
* **/mnt**	= temporary mounted filesystems
* **/sys**	= information about devices, drivers, some kernel features
* **/tmp**	= temporary files
* **/usr**	= 2nd hierarchy for read-only user data (multi-user utilities and apps)
* **/var** = variable files (temporary, logs)
* **/etc**	= specific system configuration files (Editable Text Configuration)


## Símbolos ##

- **$( )** = lê o interior do parênteses como um comando, e o assigna em uma variável 
- **|**	= faz o "piping" entre comandos, ligando o stdout do 1o com o stdin do 2o
- **>**	= trata o arquivo (a direita) como stdout, sobrescrevendo-o
- **>>**	= trata o arquivo (a direita) como stdout, adicionando algo no final (append)
- **<** = trata o arquivo (a direita) como stdin, lendo-o
- **./**	= executa um arquivo com permissão para ser executado (.run, .sh)


## Permissões Especiais ##

- **chown**	= adiciona permissão ao usuário para determinado arquivo
	* Ex.: **chown root:root test.txt**
- **chmod**	= habilita permissões para determinado arquivo
	* Ex.: **chmod +x test.txt**
- **umask**	= modifica as permissões para um arquivo/diretório
	* *+r* = readable
	* *+w* = writable
	* *+x* = executable
	* OBS.: *777* habilita todas as permissões!
- **useradd**	= adiciona novo usuário (ou adduser)
- **userdel**	= deleta o usuário
	* -r  deleta seu diretório recursivamente
- **passwd**	= modifica a senha do usuário
- **chsh**	= modifica a shell para o usuário
- **chfn**	= modifica informações sobre o usuário
- **type** 	= verifica o tipo do comando
- **cut -d: -f1 /etc/passwd** = acessa a lista de usuários do sistema
- **chattr +i path/to/file** = bloqueia arquivo
- **chattr -i path/to/file** = desbloqueia arquivo
- **chattr -i -R path/to/dir** = desbloqueia pasta
- **fuser**	= procura por todos os processos que estejam usando o arquivo
	* *-k*  elimina qualquer processo que esteja usando-o
- **fstab**		= configura o boot das partições do HD


## Navegação no prompt

* **set +o history** = modo incognito (ou **shopt -uo history**)

* **set -o history** = modo padrão
(ou **shopt -so history**)


## Internet ##

* **ping**		= envia um pacote a um servidor e conta o tempo até receber uma resposta

* **traceroute**	= mostra todos os checkpoints de tráfego de dados até o servidor
* **curl**		= acessa informações do link indicado
	Para fazer download de arquivos: 
		-o <filename.mp3> <link>
		<link> > <filename.mp3>
* **ifconfig**	= configura todas as redes de conexão
* **iwconfig**	= configura a rede de conexão wireless
* **ip addr**		= mostra os endereços de IP
* **netstat**		= mostra todas as portas abertas do sistema


## Pacotes ##
* **apt** = acessa o gerenciador de pacotes "aptitude"
	* *install*
	* *update*
	* *upgrade*
	* *remove*
	* *-y* = para todas as perguntas no prompt, responde YES
	* *-n* = para todas as perguntas no prompt, responde NO

	* Obs.: ***sources.list*** = configura os repositórios para o aptitude 

* **tar** = extrai arquivos .tar.gz
	* *f* = o argumento do comando será o nome do arquivo
	* *z* = descomprime
	* *x* = extrai para um diretório
	* *v* = dá print em todos os nomes de arquivos (verbose mode)

* **dpkg** = extrai arquivos .deb

* **gunzip** = extrai arquivos .run.gz


## Processos ##

* **ps**	= mostra os processos iniciados pelo usuário
  
* **ps aux**	= mostra um específico processo (junto com grep)
  * Ex.: **ps aux | grep apt**
  
* **pstree**	= mostra a árvore de processos


## Exemplos de Pipelines ##

* cut -d, -f2 seasonal/winter.csv | grep -v "Tooth" | sort -r
  
* cut -d, -f2 seasonal/*.csv | grep -v "Tooth" | sort | uniq -c

