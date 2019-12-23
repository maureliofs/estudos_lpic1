# Tópico 103 - Comandos GNU e Unix

## 103.1 - Trabalhando na linha de comando - shell, bash, echo e type

```shell
$ echo "texto"
```
> Escreve na tela, pode ser texto entre aspas caso tenha espaço ou conteúdo de uma variável.

```shell
ex.: echo $SHELL
```

Os comandos podem ser internos(já vem no bash), externo (instalado no linux) ou scripts.

```shell
$ type nomeComando
```
> Mostra o tipo do comando

```shell
ex.: $ type cd - echo is a shell builtin [comando interno]
     $ type clear - clear is hashed (/usr/bin/clear) [comando externo em cache]
     $ type tar - tar is /bin/tar [comando externo]
```

variável $PATH - mostra os diretórios onde os programas externos estão.

```shell
$ pwd - mostra o diretório local
```

## 103.1 - Trabalhando na linha de comando - Variáveis de ambiente

```shell
$NOME_VARIAVEL=valor [variável somente local]
```
> Declarando variáveis no shell

```shell
$ export NOME_VARIAVEL
```

> Tornar uma variável global (só funciona para
processos originados a partir do bash que você está no momento)

```shell
$ set - mostra todas as variáveis locais e exportadas
```

```shell
$ env - mostra somente as variáveis globais
```

```shell
$ unset NOME_VARIAVEL - remove a variável
```

Algumas variáveis do linux:

```shell
$HISTFILE - onde fica o arquivo de history
$HISTFILESIZE - tamanho máximo do arquivo
$HISTSIZE - número de linhas máximo do arquivo
$HOME - mostra o home do usuário
$HOSTNAME - nome da máquina
$LOGNAME - usuário que fez login no sistema
$PWD - guarda o diretório atual
$TERM - ambiente que tá logado (xterm, tty)
$USER - nome do usuário
$$ - PID do processo atual(shell atual)
$! - Último processo executado em background
$? - Código de retorno do último processo executado 
(se mostra 0 é sucesso, o resto é erro).
~ - home do usuário
PS1 - Aparência do prompt do shell
```

## 103.1 - Trabalhando na linha de comando - comandos sequenciais, history e man

Para executar vários comando ao mesmo tempo, basta separá-los por ; (sempre executa todos)

```shell
&& - Só executa o segundo se o anterior funcionar
|| - Só executa o segundo se o anterior n~
ao funcionar
$ history - Lista os últimos comando digitados
$ !! - Executa o último comando digitado
$ !numeroDoComando - Executa o comando referente ao número
$ history -c - Limpa o history
$ man nomeComando - O comando man mostra o manual dos comandos.
Caso seja um comando interno, n~
ao tem manual especı́fico, deve-se
chamar pelo $ man bash.
$ man -k "String" - procura comando que contém a string digitada.
$ info nomeComando - Funciona como o man de forma reduzida.
$ whatis nomeComando - mostra uma descriç~
ao do comando
$ apropos "String" - semelhante ao man -k
```

## 103.1 - Trabalhando na linha de comando - uname, alias, which

```shell
$ uname - Mostra informações do sistema
-a (all, mostra tudo),
-r (kernel-release mostra a versão do kernel)

$ alias - criar apelidos para chamar comandos
ex.: alias lt='ls /tmp' - toda vez que digitar lt, ele executará um
ls /tmp (só fica salvo durante a sessão)

$ which - localiza um comando
```

## 103.1 - Trabalhando na linha de comando - quoting
aspas duplas: Protege todos os caracteres exceto $ ‘ /
aspas simples: Portege todos os caracteres

### 103.1 Exercı́cios

1. Encontre as seguintes informações sobre a sua instalação Linux: O caminho completo do arquivo .bash history para o seu usuário;

```shell
echo $HISTFILE
/home/vagrant/.bash_history
```

O release do kernel instalado

```shell
uname -r
5.0.0-31-generic
```

Os diretórios incluı́dos em seu PATH

```shell
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:
/usr/local/games:/snap/bin
```

O hostname da máquina

```shell
hostname ou echo $HOSTNAME
ubuntu-disco
```

O PID da sua sessão shell atual

```shell
echo $$
2342
```

A localização do comando tar

```shell
which tar
/usr/bin/tar
```

2. Crie e exporte uma variável chamada ”NOME”que contenha o seu nome completo.
```shell
export NOME='Marco Aurélio Ferreira de Sousa'
```

3. Crie um comando que escreva na tela a seguinte frase: ”O Conteúdo da Variável $NOME é: Valor da Variável NOME ”

```shell
echo O Conteúdo da Variável '$NOME' é: $NOME
```

## 103.2 Aplicando filtros a textos e arquivos - cat, head, tail, sort, less, wc...

```shell
$ cat nomeArquivo.txt - mostra o conteúdo do arquivo.
-n - mostra todas as linhas numeradas
-b - mostra as linhas n~
ao brancas numeradas
-s - quando tem mais de uma linha em branco(enter) ele transforma
em um só enter.
-A - mostra caracteres especiais, fim de linha, tab, etc

$ tac nomeArquivo.txt - imprime o conteúdo do arquivo os contrário

$ head nomeArquivo.txt - mostra as primeiras 10 linhas de um arquivo
-n - mostra um número especı́fico de linhas. Ex. -n2 ou -2 mostra as
duas primeira linhas.
-c - mostra os primeiros bytes. Ex. -c50 mostra os 50 primeiros bytes

$ tail nomeArquivo.txt - mostra as últimas 10 linhas de um arquivo
-n - mostra um número especı́fico de linhas. Ex. -n2 ou -2 mostra as duas
últimas linhas.
-c - mostra os primeiros bytes. Ex. -c50 mostra os 50 primeiros bytes
-f - mostra o conteúdo do arquivo e atualiza em tempo real caso o arquivo
seja modificado. Muito usado para monitorar arquivos de log.

$ less nomeArquivo.txt - mostra o conteúdo do arquivo paginado.
seta para baixo e enter - se move entre as linhas
espaço - se move por página
/String - procure pela string especifica. apertando n busca a próxima ocorrência da string e N mostra a anterior.
Ctrl + G - mostra o status do arquivo, nome, tamanho, etc
q - sai do less

$ wc nomeArquivo.txt - mostra informaç~
oes sobre um determinado arquivo.
Em ordem, qtde de linhas, qtde de palavras, qtde de bytes e nome do arquivo
-l ou --lines - mostra somente a qtde de linhas
-w ou --words - mostra somente a qtde de palavras
-c ou --bytes - mostra somente a qtde de bytes
-m ou --chars - mostra somente a qtde de caracteres
wc * - mostra as informações de todos os arquivos no diretório e o total
de todas as informações.

$ nl nomeArquivo.txt - mostra as linhas n~
ao brancas numeradas, igual o cat -b

$ sort nomeArquivo.txt - mostra o arquivo ordenado em ordem crescente
-r - mostra de forma reversa
```

## 103.2 Aplicando filtros a textos e arquivos - uniq, od, paste, split

```shell
$ uniq - Mostra apenas uma vez cada palavra em um arquivo [caso tenha repetições] só mostra se tiver uma linha após a outra

$ sort arquivo.txt | uniq : Para retirar todas as ocorrências
-d - mostra somente as linhas que estão duplicadas
-c - mostra o numero de ocorrências repetidas de cada linha

$ od - [octal dump]mostra o conteúdo de um arquivo em formato octal
-tx - mostra em hexadeciamal

$ join - combina 2 arquivos através de um ı́ndice
ex.: join arq1.txt arq2.txt
-j2 - ordena de acordo com a segunda coluna por ex.

$ paste - combina as respectivas linhas de varios arquivos e mostra na tela.
ex.: paste arq1.txt arq2.txt

$ split - divide o arquivo em vários
-l - divide em numero de linhas
ex.: -l20 ou -20 - divide em varios arquivos de 20 linhas
-b - divide em bytes

$ tr substitui caracteres em um texto, deve ser usado em conjunto com o |
ou por redirecionamento de entrada.
ex.: $ cat alunos.txt | tr a-z A-Z # transforma tudo de a até z minusculo em A até Z maiusculo
-d - [delete] deleta os caracteres que passar para o par^
ametro
ex.: $ cat alunos.txt | tr -d A #apaga todos os A
$ cat alunos.txt | tr -d [:blank:] #apaga todos os espaços em branco

$ cut - recortar partes de texto
-c - recortar por caractere
ex.: cut -c1-5 alunos.txt #mostra os caracteres de 1 a 5 de cada linha
cut -c-3 alunos.txt #mostra os caracteres do inicio ate o 3
cut -c3- alunos.txt #mostra os caracteres de 3 pra frente
-b - recortar por bytes
-d - delimitador
-f - campos, usado em conjunto com o -d
ex.: cut -d" " -f1 alunos.txt # mostra o campo 1 usando como delimitador de campo um espaço.

$ sed - procurar um conteúdo e substituir ou deletar partes do texto
ex.: $ sed 's/Silva/Sousa' alunos.txt # s para substituir a primeira
# ocorrência de Silva por Sousa, para substituir todas as ocorrências
# deve se usar em /g. ex.: 's/Silva/Sousa/g'
ex.: $ sed '3,5 d' alunos.txt # apaga da linha 3 até a 5
ex.: $ sed '/Jose/d' alunos.txt # apaga as linhas q contem a palavras Jose
```

## 103.2 Aplicando filtros a textos e arquivos - xzcat, bzcat e zcat

Visualizar o conteúdo de um arquivo compactado

```shell
$ xzcat arquivo.txt.xz - Para arquivos.xz
$ bzcat arquivo.txt.bz2 - Para arquivos.bz2
$ zcat arquivo.txt.gz - Para arquivos.gz
```

## 103.2 Aplicando filtros a textos e arquivos - check-sums

Gerar um hash para fazer checksum de um determinado arquivo e verificar a autenticidade.

```shell
$ md5sum arquivo
$ sha256sum arquivo
$ sha512sum arquivo
```

Para comparar se o hash do arquivo é igual ao hash original em um arquivo de texto por exemplo (como uma iso do linux, por exemplo, arquivo SHA256SUMS) usa-se:

```shell
$sha256sum -c SHA256SUMS #compara sua iso com o arquivo de hash's originais[arquivos no mesmo diretório]
```

### 103.2 - Exercı́cios

4. O arquivo /etc/passwd contém a lista de usuários do Linux, os campos são separados pelo caractere :, o primeiro campo indica o nome do usuário e o terceiro o ID do usuário.
Escreva um comando que mostre os últimos 15 registros do arquivo, exibindo apenas o nome do usuário e seu ID, e que esteja ordenado pelo ID numérico. Por exemplo:
usuario1:10
usuario2:12
usuario3:1000

```shell
$ tail -n15 /etc/passwd | cut -d":" -f1,3 | sort -t ":" -k2 -g
```

5. Gere um comando, ou sequência deles, que mostre o número de linhas do arquivo /etc/passwd excluindo-se as linhas que contenham a palavra ”daemon”. O resultado do comando deve ser o número de linhas.

```shell
$ sed '/daemon/d' /etc/passwd | wc -l
```

## 103.3 Gerenciamento Básico de Arquivos - cd, ls, file

```shell
$ cd : muda de diretório
$ cd - : volta para o diretório que estava anteriormente
$ cd ~ : home do usuario
$ cd .. : volta um nı́vel de diretório
```

```shell
$ ls : Lista o conteúdo de um diretório
$ ls -a : mostra arquivos ocultos [--all]
$ ls -l : mostra os arquivos em formato de lista, além disso mostra os diretórios . e .. que se referem ao diretório atual e o anterior respectivamente.
As colunas do ls -l representam respectivamente o tipo do arquivo:
d para diretório, l pra link e - para arquivos normais, as permissões de rwx, número de hardlinks que apontam pra ele, nome do usuário que é dono do arquivo e grupo, tamanho do arquivo em bytes, data e hora da última alteração e nome do arquivo.
$ ls -lh : o parâmetro h é usado em conjunto com o l e mostra o tamanho do arquivo em bytes de um forma mais fácil de ler K para KB, M para MB [--human-readable]
$ ls -R : entra em cada subdiretório abaixo do atual e mostra os ls de tudo [--recursive]
Ex.: $ ls -l Aula1* : [asterisco significa nada ou algum caractere] mostra todos os arquivos que começa com Aula1 inclusive o próprio e mais alguma coisa pra frente.
$ ls -l Aula1? : [o interrogação significa algum caractere] mostra tudo que começa com Aula1, não incluso, e tem mais um caractere pra frente.
$ ls -l Aula[123] : associa a palavra Aula com cada um dos números nos colchetes, ou seja exibe somente Aula1, Aula2, Aula3. Pode ser usado o ! antes do 1 para negar e não exibir esses arquivos.
$ ls -l Aula[1-5]: mesma coisa do comando acima mas em forma de range, do 1 ao 5. Pode ser usado o ! para negar.
$ ls -l Aula{10,20,30}: mostra especificamente o Aula10, Aula20, Aula30.
```

```shell
$ file nomeArquivo: mostra o tipo do arquivo
```

## 103.3 Gerenciamento Básico de Arquivos - touch, cp, mv

```shell
$ cp - copia arquivos e diretórios sintaxe: 
$ cp arquivo destino Ex.: cp teste.txt /tmp/
-v : [--verbose] mostra o que foi feito
-i: [--interactive] pergunta se quer sobrescrever um arquivo caso ele ja exista no diretório
-r ou -R: [--recursive] copia diretórios e tudo dentro deles
-p : preserva as caracteristicas do arquivo, hora demodificação, usuario, etc.
```

```shell
$ mv - move ou renomea arquivos sintaxe: 
$ mv arquivo destino Ex.: mv texte.txt /tmp/
-v : [--verbose] mostra o que foi feito
-i: [--interactive] pergunta se quer sobrescrever um arquivo caso ele ja exista no diretório
```

```shell
$ touch - modifica a data e hora de um arquivo e cria arquivo em branco
$ touch arquivo.txt : cria o arquivo.txt
Caso use o touch em um arquivo que já exista e modifica a data da última alteração
-a : altera a data do último acesso
-m : altera a data da última modificação
-t : define a hora da alteração que a pessoa quiser AAAAMMDDHHMM.
Ex.: $ touch -t 201910211133 teste.txt
```

## 103.3 Gerenciamento Básico de Arquivos - rm, mkdir, rmdir, find

```shell
$ rm - Remove arquivos ou diretórios
sintaxe: $ rm nomeArquivo
-i : [--interactive] pergunta se quer remover um arquivo
-v : [--verbose] mostra o que foi removido
-r : [--recursive] remove diretório
```

```shell
$ mkdir nomeDiretório: cria diretório
-p : [--parents] cria diretórios e subdiretórios.
Ex. $ mkdir -p curso/linux/lpic1
```

```shell
$ rmdir : remove diretórios [somente diretórios vazios]
-p : [--parents] remove a estrutura de diretórios criado com mkdir -p [só se todos os diretórios estiverem vazios]
```

```shell
$ find - procura arquivos numa hierarquia de diretório
sintaxe: $ find diretorio parametro nomeArquivo.
Ex.: $ find / -name curso.txt
-name: procura pelo nome
-iname: no case sensitive
-user: arquivos de um determinado usuario
-ctime: data de modificação do arquivo.
Ex.: -ctime -1 arquivos que foram modificados num determinado periodo de tempo, no exemplo, 1 dia atrás.
```

## 103.3 Gerenciamento Básico de Arquivos - tar, gzip, bzip2, xz

```shell
$ tar - comando usado para compactar e descompactar arquivos
c : criar um arquivo de backup
x : extrair
t : listar quais arquivos estão no arquivo compactado
f : para indicar o nome do arquivo
p : preservar as opções = cp, mv
v : verbose
sintaxe ex.: $ tar cpvf backup.tar novo*
```
Algortimos de compactação
```shell
$ gzip backup.tar #compacta no formato gzip
$ gunzip backup.tar.gz # descompactar arquivo.gz ou gzip -d
-k : mantem o .tar e o .tar.gz
```

```shell
$ bzip2 -k backup.tar # -k [keep] para manter o .tar e .tar.bz2
$ bunzip2 backup.tar.bz2 # ou bzip2 -d
```

```shell
$ xz backup.tar
$ unxz backup.tar.xz # ou xz -d
```
Usando o tar em conjunto com os algoritmos de compactação, para agrupar e compactar ao mesmo tempo

```shell
z : gzip
j : bzip2
J : xz
ex.: $ tar zcvpf backup.tgz novo*
```
Para descompactar
```shell
$ tar zxvf backup.tgz # para gzip
```
## 103.3 Gerenciamento Básico de Arquivos - cpio, dd

```shell
$ cpio - copia files de e para archives, quase igual o tar os arquivos devem ser passado por meio de redirecionamento de saı́da para a entrada do cpio usando o find e redirecionar a saı́da do cpio para o arquivo.
ex.: $ find ./ -name "novo*" | cpio -o > backup.cpio
-i : descompactar o arquivo cpio
ex.: $ cpio -i < backup.cpio
```

```shell
$dd : copia uma partição inteira para outra, copiar uma partição para um arquivo ou um arquivo de imagem para uma partição.
Copia byte a byte
ex.: $ dd if=/dev/sda of=imagem.img
$ dd if=linux.iso of=/dev/sdb bs=8192;sync
```
### 103.3 Exercı́cios

6. No home de seu usuário, crie um diretório chamado LPI1, dentro dele crie Aulas, Exercicios e Exemplos.

```shell
$ mkdir -p LPI1/Aulas/Exercicios
$ mkdir -p LPI1/Aulas/Exemplos
```
7. Copie (não mova) todos os arquivos e diretórios existentes em /etc/network/ para HOME/LPI1/Exercicios/Network/. Mantenha as mesmas permissões.
```shell
$ mkdir /home/LPI1/Exercicios/Network
$ cp -rp /etc/network/* /home/LPI1/Exercicios/Network
```
8. Copie (não mova) todos os arquivos do diretório /etc, cujo nome termine com ”.conf” para HOME/LPI1/Exercicios/Config/
```shell
$ mkdir /home/LPI1/Exercicios/Config/
$ cp /etc/*.conf /home/LPI1/Exercicios/Config/
```
9. Em HOME/LPI1/Exercicios, crie um arquivo chamado arquivos-cron.tgz, compactado com o gzip, contendo todos os arquivos e diretórios do /etc que contenham a palavra ”cron”no nome.
```shell
$ cp -r /etc/*cron* /home/LPI1/Exercicios/
$ tar zcvpf arquivos-cron.tgz *
```
10. Descompacte conteúdo do arquivo arquivos-cron.tgz dentro do diretório HOME/LPI1/Exercicios/Descompactar/
```shell
$ tar zxvpf arquivos-cron.tgz -C Descompactar
```
11. Encontre todos os arquivos do diretório /var, cujo nome termine com ”.gz”e que foram modificados nas últimas 48 horas.
```shell
$ find /var -name "*.gz" -ctime -2