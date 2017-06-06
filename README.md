# Elixir

## 1 Primeiros Passos

### 1.1 Instalando Elixir

O curso em questão usará máquinas Ubuntu 14.04.
para instalar você deve abrir o terminal e digitar os comandos:

Adicionando o Erlang Solutions repo:
`wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && sudo dpkg -i erlang-solutions_1.0_all.deb`

`sudo apt-get update`

Instalando o Erlang e suas aplicações:
`sudo apt-get install esl-erlang`

Por fim, a instalação do Elixir:
`sudo apt-get install elixir`

As instruções de instalação para os demais sistema operacional poderá ser encontradas em [Elixir-lang.org](https://elixir-lang.org/) na aba [Install](https://elixir-lang.org/install.html).

### 1.2 Modo Interativo

Elixir vem com IEx, um console interativo, que nos permite avaliar expressões em Elixir.
Para iniciar, executamos `iex`:

![alt text](https://github.com/ohashijr/elixir/blob/master/img/modointerativo.png "Modo interativo do Elixir")


## 1.3 Aridade de funções

Aridade em linguagem funcionais corresponde ao número de argumentos que uma determinada função recebe.
No próprio terminal, voce pode consultar o `IEx.Helpers` (O módulo interativo de ajuda com o Elixir) que oferece auxílios durante o desenvolvimento e torna o terminal do Elixir mais prazeroso para o trabalho :smile:

Então, após execultar o comando `iex` digite um simples `h` que o IEX.Helpers explica:

* `b/1           - prints callbacks info and docs for a given module`
* `c/1           - compiles a file into the current directory`
* `c/2           - compiles a file to the given path`
* `cd/1          - changes the current directory`
* `clear/0       - clears the screen`
* `flush/0       - flushes all messages sent to the shell`
* `h/0           - prints this help message`
* `h/1           - prints help for the given module, function or macro`
* `i/1           - prints information about the data type of any given term`
* `import_file/1 - evaluates the given file in the shell's context`
* `l/1           - loads the given module's BEAM code`
* `ls/0          - lists the contents of the current directory`
* `ls/1          - lists the contents of the specified directory`
* `nl/2          - deploys local BEAM code to a list of nodes`
* `pid/1         - creates a PID from a string`
* `pid/3         - creates a PID with the 3 integer arguments passed`
* `pwd/0         - prints the current working directory`
* `r/1           - recompiles the given module's source file`
* `recompile/0   - recompiles the current project`
* `respawn/0     - respawns the current shell`
* `s/1           - prints spec information`
* `t/1           - prints type information`
* `v/0           - retrieves the last value from the history`
* `v/1           - retrieves the nth value from the history`


## 2 Coleções
### 2.1 Listas

Listas  são  um  tipo  de  coleção  de  elementos  e  podem conter diversos outros tipos dentro dela. Uma lista pode conter valores númericos, Strings e booleans, por exemplo.

Listas em Elixir, jamais podem ser comparadas  com  arrays  de Java ou PHP,  porque  não  os conceitos não são iguais. O conceito  aqui  é  que listas podem ter `head` (cabeça) e `tail` (cauda). A cabeça contém o  valor  e  a  cauda  por  si  mesma  é  a  lista  inteira.  Por  causa  dessa implementação, elas podem ser percorridas facilmente.

```elixir
iex> [3.14, :okgoogle, "AppleStore", true, 2]
[3.14, :okgoogle, "AppleStore", true, 2]
```

Elixir implementa listas como listas encadeadas. Isso significa que acessar a profundidade da lista é uma operação O(n). Por essa razão, é normalmente mais rápido inserir um elemento no início do que no final.

```elixir
iex> lista = [3.14, :pie, "Apple"]
[3.14, :pie, "Apple"]
iex> ["π"] ++ lista
["π", 3.14, :pie, "Apple"]
iex> lista ++ ["Cherry"]
[3.14, :pie, "Apple", "Cherry"]
```


#### Concatenação de listas

A concatenação de listas usa o operador ++/2.

```elixir
iex> [1, 2] ++ [3, 4, 1]
[1, 2, 3, 4, 1]
```

#### Subtração de listas

O suporte para subtração é provido pelo operador --/2; é seguro subtrair um valor que não existe:

```elixir
iex> ["foo", :bar, 42] -- [42, "bar"]
["foo", :bar]
```


Existem diversas funções para trabalhar com listas, você deve consultar  a  [documentação  oficial](https://elixir-lang.org/docs.html)  a  cada  atualização  da  linguagem para ficar por dentro de todas as novidades. :smile:

```elixir
iex> lista = [1,2,3]
[1,2,3]
iex> hd lista #acessando o head
1
iex> List.first lista #buscando a primeira posicao da lista
1
iex> newLista = List.insert_at lista, 3, 4 #inserindo o valor 4 na posição 3 da lista, salvando em uma nova lista
[1,2,3,4]
iex> newLista ++ lista #concatenando as duas listas
[1,2,3,4,1,2,3]
```

#### Lazy Evaluation


### 2.2 Tuplas

As tuplas são similares as listas porém são armazenadas de maneira contígua em memória. Isto permite acessar a sua profundidade de forma rápida porém sua modificação é custosa. A nova tupla deve ser armazenada inteira na memória. As tuplas são definidas com chaves.

```elixir
iex> {3.14, :okgoogle, "AppleStore", true, 2}
{3.14, :okgoogle, "AppleStore", true, 2}
```


Existem diversas funções para trabalhar com tuplas, você deve consultar  a  [documentação  oficial](https://elixir-lang.org/docs.html)  a  cada  atualização  da  linguagem para ficar por dentro de todas as novidades. :smile:

```elixir
iex> tupla = {3.14, :okgoogle, "AppleStore", true, 2}
{3.14, :okgoogle, "AppleStore", true, 2}
iex> tuple_size tupla #verificando o tamanho da tupla
5
iex> elem tupla, 2 #acessando o elemento no indice 2
"AppleStore"
iex> elem tupla, 4 #acessando o elemento no indice 4
2
iex> put_elem tupla, 0, 3 #atualizando o valor do indice zero
{3, :okgoogle, "AppleStore", true, 2}
```

### 2.3 Maps
Mapas são uma coleção de chave/valor e são similares a tuplas, exceto  quando adicionamos um sinal  de  % (porcentagem)  na frente das chaves.

```elixir
iex> map = %{:foo => "bar", "hello" => :world}
%{:foo => "bar", "hello" => :world}
iex> map[:foo]
"bar"
iex> map["hello"]
:world
```

Em Elixir 1.2, variáveis são permitidas como chaves do mapa:

```elixir
iex> key = "hello"
"hello"
iex> %{key => "world"}
%{"hello" => "world"}
```

Se um elemento duplicado é inserido no mapa, este sobrescreverá o valor anterior;

```elixir
iex> %{:foo => "bar", :foo => "hello world"}
%{foo: "hello world"}
```

Como podemos ver na saída anterior, há uma sintaxe especial para os mapas que contem átomos como chaves:

```elixir
iex> %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}
```

```elixir
iex> %{foo: "bar", hello: "world"} == %{:foo => "bar", :hello => "world"}
true
```


Outra propriedade interessante de mapas é que eles têm sua própria sintaxe para atualizar e acessar átomos como chaves:
```elixir
iex> map = %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}
iex> %{map | foo: "baz"}
%{foo: "baz", hello: "world"}
iex> map.hello
"world"
```


## 3 Patthern Matching

Em Elixir, o operador `=` é na verdade o nosso operador match, comparável ao sinal de igualdade da matemática. Quando usado, a expressão inteira se torna uma equação e faz com que Elixir combine os valores do lado esquerdo com os valores do lado direito da expressão. Se a comparação for bem sucedida, o valor da equação é retornado. Se não, um erro é lançado. Vejamos a seguir:

```elixir
iex> x = 5
5
```
Agora vamos tentar a simples correspondência:

```elixir
iex> 5 = x
5
iex> 2 = x
** (MatchError) no match of right hand side value: 5
```

Vamos tentar isso com algumas das coleções que nós conhecemos:

```elixir
# Listas
iex> list = [1, 2, 3]
iex> [1, 2, 3] = list
[1, 2, 3]
iex> [] = list
** (MatchError) no match of right hand side value: [1, 2, 3]


# Tuplas
iex> {:ok, value} = {:ok, "Successful!"}
{:ok, "Successful!"}
iex> value
"Successful!"
iex> {:ok, value} = {:error}
** (MatchError) no match of right hand side value: {:error}


# Situação-problema
iex> {:moto, modelo} = {:moto, "Suzuky"}
{:moto, "Suzuky"}
iex> modelo
"Suzuky"
iex> {:moto, modelo} = {:carro, "Suzuky"}
** (MatchError) no match of right hand side value: {:carro, "Suzuky"}
```

E podemos  fazer match  pulando  valores  que  não nos interessam. Vamos supor que queremos pegar sempre o segundo ou terceiro  valor,  não importando  quais  sejam  o  primeiro  ou  o segundo. Para isso, podemos usar um simples `_`(underscore).

```elixir
iex> {_, numero} = {"bla bla bla", 404}
{"bla bla bla", 404}
iex> numero
404
iex> {_,_,_,x} = {1,2,3,4}
{1,2,3,4}
iex> x
4
```

## 4 Funções
Em linguagens funcionais como o **elixir** as funções são cidadãos de primeira classe.

Funções podem ser criadas dentro de um modulo, utilizando a paralavra def em seguida o nome da função e seus argumentos. Também podem ser criadas sem argumentos e, até mesmo sem nomes.
Aprenderemos a seguir qual a diferença, como usar funções e tipos de funções em elixir.  

### 4.1 Nomeadas
Funções nomeadas são criadas dentro de um modulo, utilizando a palavra `def`  em seguida o nome da função e seus argumentos. Podemos definir esse tipo de função para mencionar a elas futuramente.

```elixir
iex(1)> defmodule Media do
...(1)>   def notas(n1,n2,n3,n4) do
...(1)>      (n1+n2+n3+n4)/4
...(1)> end
...(1)> end
iex(2)> Media.notas(8,9,7,6)
7.5
```

Se tentarmos definir a função fora de um modulo será gerado um erro, como veremos a seguir:

```elixir
iex(3)>   def notas(n1,n2,n3,n4) do
...(3)>      (n1+n2+n3+n4)/4             
...(3)> end
** (ArgumentError) cannot invoke def/2 outside module
    (elixir) lib/kernel.ex:4436: Kernel.assert_module_scope/3
    (elixir) lib/kernel.ex:3433: Kernel.define/4
    (elixir) expanding macro: Kernel.def/2
             iex:3: (file)
iex(3)>
```

Podemos reduzir o corpo da nossa função ainda mais com `do:`:

```elixir
iex(1)> defmodule Media do
...(1)>   def notas(n1,n2,n3,n4), do: (n1+n2+n3+n4)/4
...(1)> end
```

Podemos explorar ainda mais recursos de funções nomeadas, usando nossos conhecimentos sobre `patthern matching`.

```elixir
defmodule Contador do
    def contar([]), do: 0
    def contar([ _ | tail]), do: 1 + contar(tail)
end
```

Podemos reutizar funções definidas dentro de modulos em outros modulos, isso é singularmente útil na construção de blocos em elixir:

```elixir
iex(1)> defmodule Media do
...(1)>   def notas(n1,n2,n3,n4) do
...(1)>      (n1+n2+n3+n4)/Contador.contar [n1,n2,n3,n4]
...(1)> end
...(1)> end
iex(2)> Media.notas 8,8,8,8
8.0
iex(3)>
```
Observe não foi preciso colocar os parênteses para chamar a função.

### 4.2 Privadas
As funções privadas só podem ser chamadas de dentro do módulo no qual foram declaradas. Bem parecido com que acontece em outras linguagens.

No exemplo que irá ser criado, será declarada um função com `defp` em de `def`. significa que se trata de uma função restrita somente para chamadas internas.

```elixir
defmodule Media do
  def notas(n1,n2,n3,n4), do: soma(n1,n2,n3,n4)/4
    defp soma(n1,n2,n3,n4), do: n1 + n2 + n3 + n4         
end

iex(7)> Media.notas 9,8,9,10
9.0
```
Agora tente executar fora do módulo a função privada `soma`. Observe o resultado:

```elixir
iex(8)> Media.soma 2,3,4,5  
** (UndefinedFunctionError) function Media.soma/4 is undefined or private
    Media.soma(2, 3, 4, 5)
```
Como podemos observar é gerado o seguinte erro: A função Media.soma/4 é indefinida ou privada.

### 4.3 Anônimas
Como nome já diz, uma função anônima não tem nome. São frequentemente passadas para outras funções.

Em elixir ela é criada da seguinte forma: usando a palavra chave `fn` e `end`, acrescentando os argumentos e um `->` que representa o corpo da função. A função é ligada por meio de `match` a uma variável que servirá para execultá-la futuramente.

```elixir
iex(1)> soma = fn (a,b) -> a + b end
#Function<12.118419387/2 in :erl_eval.expr/5>
iex(2)> soma.(8,10)
18
iex(3)> media = fn (a,b) -> soma.(a,b)/2 end
#Function<12.118419387/2 in :erl_eval.expr/5>
iex(4)> media.(2,2)
2.0
iex(5)>  
```
Atente que, ao chamar uma função anônima através de uma variável, usamos um ".()" ponto e parênteses, os mesmos são obrigatórios. Percebe-se a diferença entre funções anônimas e nomeadas.

Se tentar chamar a função sem o ponto ou sem o parêntese, ocorrerá um erro.

```elixir
iex(5)> soma(8,10)                          
** (CompileError) iex:5: undefined function soma/2

iex(5)> soma.8,10  
** (SyntaxError) iex:5: syntax error before: 8

iex(5)> soma. 8,10
** (SyntaxError) iex:5: syntax error before: 8

iex(5)> soma 8,10
** (CompileError) iex:5: undefined function soma/2

iex(5)>
```
### A & taquigrafia
Em elixir é muito comum a criação de funções anonimas, por isso que desenvolvedores resolveram criar um atalho para elas. Para usar o atalho, basta utilizar o `&` seguindo de parênteses com o o corpo da função. Os argumentos são nomeados a seguinte forma: &1, &2, ... &n.

```elixir
iex(1)> soma = &(&1 + &2)
&:erlang.+/2
iex(2)> soma.(8,5)
13
iex(3)> media = &((&1+&2)/2)
#Function<12.118419387/2 in :erl_eval.expr/5>
iex(4)> media.(2,2)
2.0
iex(5)> media.(8,8)
8.0
iex(6)> mutilica_e_soma = &(&1 * &2 + &3)
#Function<18.118419387/3 in :erl_eval.expr/5>
iex(7)> multiplica_e_soma = &(&1 * &2 + &3)
#Function<18.118419387/3 in :erl_eval.expr/5>
iex(8)> multiplica_e_soma.(2,5,10)         
20
iex(9)>
```

## Guards


## 5 Modulo

Os módulos são a melhor maneira de organizar as funções em um namespace. Além de agrupar funções, eles permitem definir funções nomeadas e privadas que cobrimos nas lições passadas. Para isso, basta utilizar a palavra reservada defmodule seguida do nome do módulo, por exemplo, defmodule Multiplicacao.

No código de exemplo, você cria um módulo com uma função dentro dele que multiplica seus argumentos. Para criar uma função, basta usarmos a palavra reserva  def, seguida do nome da função e seus argumentos.

```elixir
defmodule Multiplicacao do
  def multiplique(a, b) do
    a * b
  end
end

iex> Multiplicacao.multiplique 2, 6
12
iex> Multiplicacao.multiplique 5, 4
20
```

### 5.1 Compilação

Na maioria das vezes é conveniente escrever módulos em arquivos para que eles possam ser compilados e reutilizados. Vamos supor que temos um arquivo multiplicacao.ex com o seguinte conteúdo:

```elixir
defmodule Multiplicacao do
  def multiplique(a, b) do
    a * b
  end
end
```

Este arquivo pode ser compilado usando elixirc:

```elixir
$ elixirc multiplicacao.ex
```

Isso gerará um arquivo chamado Elixir.Math.beam contendo o bytecode para o módulo definido. Se iexcomeçarmos novamente, a definição do nosso módulo estará disponível (desde que iexseja iniciado no mesmo diretório em que o arquivo bytecode esteja):

```elixir
iex> Multiplicacao.multiplique(1, 3)
3
```

Os projetos Elixir geralmente são organizados em três diretórios:

* `ebin - contém o bytecode compilado`
* `lib - contém elixir code contém o codigo elixir (geralmente arquivos .ex)`
* `test - contém os testes (geralmente arquivos .exs)`

Ao mixtrabalhar em projetos reais, a ferramenta de construção chamada será responsável por compilar e configurar os caminhos adequados para você. Para fins de aprendizagem, Elixir também oferece suporte a um modo de script que é mais flexível e não gera nenhum artefato compilado.

## 6 Structs

Structs são mapas especiais com um conjunto definido de chaves e valores padrões. Ele deve ser definido dentro de um módulo, no qual leva o nome dele. É comum para um struct ser a única coisa definido dentro de um módulo.

Para definir um struct nós usamos `defstruct` juntamente com uma lista de palavra-chave de campos e valores padrões:

```elixir
defmodule Example.User do
  defstruct name: "Sean", roles: []
end
```

Vamos criar algumas estruturas:

```elixir
iex> %Example.User{}
%Example.User{name: "Sean", roles: []}
```

```elixir
iex> %Example.User{name: "Steve"}
%Example.User{name: "Steve", roles: []}
```

```elixir
iex> %Example.User{name: "Steve", roles: [:admin, :owner]}
%Example.User{name: "Steve", roles: [:admin, :owner]}
```
Podemos atualizar nosso struct apenas como se fosse um mapa:

```elixir
iex> steve = %Example.User{name: "Steve", roles: [:admin, :owner]}
%Example.User{name: "Steve", roles: [:admin, :owner]}
iex> sean = %{steve | name: "Sean"}
%Example.User{name: "Sean", roles: [:admin, :owner]}
```
Mais importante, você pode associar estruturas contra mapas:

```elixir
iex> %{name: "Sean"} = sean
%Example.User{name: "Sean", roles: [:admin, :owner]}
```
## 7 Operador pipe
O operador pipe |> é um grande auxiliador na hora de construir seu código em Elixir. O seu uso é simples de se entender. Ele pega o resultado da expressão da esquerda e aponta para o primeiro argumento da função a sua direita e assim segue.O objetivo é destacar os dados que estão sendo transformados por uma série de funções, e você pode tornar o seu código limpo.

```elixir
foo(bar(baz(new_function(other_function()))))
```

Aqui, nós estamos passando o valor other_function/1 para new_function/1, e new_function/1 para baz/1, baz/1 para bar/1, e finalmente o resultado de bar/1 para foo/1.

Aplicando o pipe

```elixir
other_function() |> new_function() |> baz() |> bar() |> foo()
```


Vamos aos exemplos. O primeiro segue sem a ultilização e em seguida o mesmo codigo porém utilizando pipe para as devidas comparações.

```elixir
iex> Enum.join(Enum.map(String.split("olá, sr mundo!", " "), &String.capitalize/1), " ")
"Olá, Sr Mundo!"

iex> "olá, sr mundo" |> String.split(" ") |> Enum.map(&String.capitalize/1) |> Enum.join
"Olá,SrMundo"
```


Digamos que voce queira montar um serviço de vendas de smartphones. E nesse sistema voce precise mapear, descontar, somar e filtrar os aparelhos. Daremos 30% de desconto para cada smartphone e selecionar apenas os que tem valor superior a mil reais e somar o resultado para finalizar a compra.


```elixir
iex> carrinho = [%{smartphone: "Moto G4 Plus", valor: 1099.00}, %{smartphone: "Galaxy S8", valor: 3999.00 }, %{smartphone: "iPhone 7", valor: 4299.99 }, %{smartphone: "Galaxy J7", valor: 897.00 }, %{smartphone: "Xperia XA", valor: 1649.00}]

iex> carrinho |> Enum.map(&(Float.round(&1.valor - &1.valor * 0.3, 2))) |> Enum.filter(&(&1 > 1000.00)) |> Enum.sum
6963.59

```

## 8 Composição
Acima apredemos criar modulos e struct, agora iremos aprender a adcionar uma funcionalidade exitente neles, por meio da compisição. Veremos que `elixir` oferece vastas maneiras direntes para interagir com outros módulos.

 * **alias**

 Sua função é criar criptônimos ou pode-se dizer "apelidos", alias  sãos muito usadas em código elixir.

 ```elixir
 defmodule Sayings.Greetings do
   def basic(name), do: "Hi, #{name}"
 end

 defmodule Example do
   alias Sayings.Greetings

   def greeting(name), do: Greetings.basic(name)
 end

 # Sem alias

 defmodule Example do
   def greeting(name), do: Sayings.Greetings.basic(name)
 end
 ```
 * import
 * require
 * use

## 9 Recursividade


## 0 Mix
