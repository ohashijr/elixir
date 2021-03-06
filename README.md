## Elixir

“Elixir é uma linguagem dinâmica e funcional projetada para construir aplicações escaláveis e de fácil manutenção.” — [Elixir-lang.org](https://elixir-lang.org/)

Elixir aproveita a massivamente testada máquina virtual do Erlang para construir sistemas distribuídos e tolerantes a falhas com baixa latência.

Características | Função
--------------- | ---------------
Escalável       | habilidade de manipular uma porção crescente de trabalho de forma uniforme
Tolerante a falhas | existe como reiniciar partes do seu sistema quando algo estiver em declínio, e iniciar do estado que garante o funcionamento
Programação funcional | basicamente é tornar uma visao explícita das partes complexas do seu sistema
Extensível      | permite adicionar novas construções como se fossem parte da própria linguagem Elixir


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


## 2 Tipos e Operações Básicas

 Nessa parte, Elixir também é semelhante as diversas linguagens de programação existentes, possuindo tipos numéricos, Strings, booleanos e coleções(veremos esse assunto no próxmio módulo). Entretanto ela também nos trás algumas caracteristicas de suporte para estruturas binárias, hexais e octais e a novas estruturas, como atoms(equivalente aos Símbolos em Ruby).

 Abra o shell e execute o comando `iex` para começar a brincadeira.

### 2.1 Tipos Numéricos

* Inteiros
Podemos escrever os números inteiros de duas formas, na primeira apenas digitando o número como: 99 ou utilizando underline/underscore para facilitar na leitura do número quando existem muitos zeros.

```elixir
iex> 99
99

iex> 2_00
200

iex> 3_000
3000

iex> 9_000_000
9000000
```

* Pontos Flutuantes:
Em Elixir, os números de ponto flutuante requerem um decimal depois de pelo menos um dígito; estes possuem uma precisão de 64 bits.

```elixir
iex> 1.0
1.0

iex> 3.14
 3.14

iex> .14
** (SyntaxError) iex:2: syntax error before: '.'
```

### 2.2 Binários, Hexadecimais e Octais

Em Elixir, existem diferentes prefixos para a conversão de determinado numero para outra base numérica. Iremos converter para decimal, e precisamos acrescentar o prefixo `0b`.

```elixir
iex> 0b1110
14

iex> 0b1111
15

iex> 0b10000
16
```

Para a conversão de números Hexadecimais, temos o prefixo `0x`.

```elixir
iex> 0xd
13

iex> 0xe
14

iex> 0xf
15
```

Por fim, de Octais para decimais `0o`.

```elixir
iex> 0o12
10

iex> 0o13
11

iex> 0o14
12
```
### 2.3 Atoms

Um Átomo é uma constante cujo o nome é seu valor. em Elixir ele é representado por : (dois pontos) em seguida um texto. Geralmente atoms são mais comuns para sinalizar alguma mensagem como de erro ou sucesso.

```elixir
iex> :sucess
:sucess

iex> :error404
:error404

iex> :paiDegua
:paiDegua
```

### 2.4 Booleanos

Elixir apresenta três maneiras de expressões booleans: `true`, `false` e `nil`(avaliado como false em contextos booleanos).

```elixir
iex> true
true

iex> false
false

iex> nil
nil
```

### 2.5 Strings

As strings em Elixir são codificadas em UTF-8 e são representadas com aspas duplas:

```elixir
iex> "Elixir"
"Elixir"

iex> "égüà"
"égüà"
```

### 2.6 Operações Básicas

* Aritimética:

Elixir suporta os operadores básicos `+, -, *,` e `/` como era de esperar. É importante ressaltar que `/` sempre retornará um número ponto flutuante:

```elixir
iex> 7 + 7
14

iex> 14 - 1
13

iex> 20 * 5
100

iex> 10 / 2
5.0
```

Se você necessita de uma divisão inteira ou o resto da divisão, Elixir vem com duas funcionalidades úteis para isto:

```elixir
iex> div(10, 5)
2
iex> rem(10, 3)
1
```

* Expressões booleanas:


Entrada  | Saída
-------- | ----------------------------------------------
a or b	 |	 true se	a	é	true;	caso contrário, b.
a	and	b  |		false	se a é false;	caso contrário, b.
not a	   |	 	 false se	a	é	true;	caso contrário, true.
a	&& b	 |	 	 b se	a	é true;	caso contrário,	a.


Entrada         | Exemplo          |  Saída
--------------- | ---------------- | ------------
a	 	!==	 	b	 |	  	1	!==	1.0	  | 		 	true	 
a	 	==	 	b	 |	 		1	==	1.0	  | 	 	true	 
a	 	!=	 	b	 |	 		1	!=	1.0	  |	 	false

Entrada       | Saída
------------- | ---------------------------
a	 	>	 	b	 |	 		se	a	é	maior	do	que	b.
a	 	>=	 	b|		se	a	é	maior	ou	igual	a	b.
a	 	<	 	b	 |	 se	a	é	menor	do	que	b.
a	 	<=	 	b	| 		se	a	é	menor	ou	igual	a	b.

## 3 Coleções
### 3.1 Listas

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


#### 3.1.1 Concatenação de listas

A concatenação de listas usa o operador ++/2.

```elixir
iex> [1, 2] ++ [3, 4, 1]
[1, 2, 3, 4, 1]
```

#### 3.1.2 Subtração de listas

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


### 3.2 Tuplas

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

### 3.3 Maps

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


## 4 Patthern Matching

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

## 5 Estruturas de Controle

* If e unless:

Existem chances de que você já tenha encontrado `if` antes, e caso você tenha utilizado Ruby você é familiarizado com `unless`. Em Elixir eles trabalham praticamente da mesma forma.

```elixir

iex> if String.valid?("Ola") do
...>   "String válida!"
...> else
...>   "String inválida."
...> end
"String válida!"
```
Usar unless é bem parecido o uso do if porém trabalhando de forma negativa:

```elixir

iex> unless true do
...>   "Essa linha nunca será impressa"
...> end
nil
```

* Case:

Caso seja necessário combinar multiplos padrões nós poderemos utilizar `case`:

```elixir

iex> case :elixir do
...> :java -> "Isso nao combina com :elixir"
...> :php -> "Isso menos"  
...> 1     -> "Tambem nao"
...> :elixir -> "Tudo certo! Casou :elixir com :elixir"
end
"Tudo certo! Casou :elixir com :elixir"


iex> case 90 do
...> 50 -> "Some mais 40 que é 90"  
...> 40  -> "Falta muito pra 90"
...> _    -> "Underline/Underscore nao é 90, mas é um coringa que casa com tudo!"
end
"Underline/Underscore nao é 90, mas é um coringa que casa com tudo!"
```

* Cond:

Quando necessitamos associar condições, e não valores, nós podemos recorrer ao `cond`; Isso é semelhante ao else if ou elseif de outras linguagens:

```elixir
iex> cond do
...>   2 + 2 == 5 ->
...>     "Isso ai nao é verdade."
...>   2 * 2 == 3 ->
...>     "Nada disso tambem..."
...>   1 + 1 == 2 ->
...>     "Acertou a cond!"
...> end
"Acertou a cond!"
```


## 6 Funções
Em linguagens funcionais como o **elixir** as funções são cidadãos de primeira classe.

Funções podem ser criadas dentro de um modulo, utilizando a paralavra `def` em seguida o `nome da função` e seus `argumentos.` Também podem ser criadas sem argumentos e, até mesmo sem nomes.
Aprenderemos o conceito de aridades de funções e em seguida quais são os tipos de funções, a diferença e como usar funções em elixir.  


## 6.1 Aridade de funções

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


### 6.2 Nomeadas
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

### 6.3 Privadas
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

### 6.4 Anônimas
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
### 6.5 A & taquigrafia
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


## 7 Modulo

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

### 7.1 Compilação

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

## 8 Structs

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
## 9 Operador pipe
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

## 10 Composição
Acima apredemos criar modulos e struct, agora iremos aprender a adcionar uma funcionalidade exitente neles, por meio da compisição. Veremos que `elixir` oferece vastas maneiras direntes para interagir com outros módulos.

 * **alias**

   Sua função é criar criptônimos ou pode-se dizer "apelidos", alias  sãos muito usadas em código elixir.

 ```elixir
#criação do modulo soma
defmodule Soma do
        def numero(a,b,c,d), do: a+b+c+d
end

#modulo com alias
defmodule Media do                                       
  alias Soma #alias do modulo soma                                          
  def notas(n1,n2,n3,n4), do: Soma.numero(n1,n2,n3,n4)/4
end

#Exemplo
iex> Media.notas 5,5,5,5
5.0

 # Sem alias
 defmodule Media do
   def notas(name), do: Soma.numero(n1,n2,n3,n4)/4
 end
 ```

 Em caso de algum conflito com alias ou simplesmente queira criar um outro apelido completamente diferente, usa-se o `:as`.

 O exemplo a seguir criará um apelido para o alias Soma.

 ```elixir
 #apelido para o alias
 defmodule Media do                                       
   alias Soma, as: Somar                                          
   def notas(n1,n2,n3,n4), do: Somar.numero(n1,n2,n3,n4)/4
 end
 ```
 Também pode ser criados aplidos para multiplos módulos de uma só vez, observe:

 ```elixir


 ```

 * **import**

  Usa-se import sempre que quisermos acessar facilmente funções ou macros de outros módulos, sem a necessidade de usar o nome completo.

  Vamos ver um exemplo bem silmples, vamos criar um modulo com as seguintes funções: soma, subtração, multiplicação e divisão.

  ```elixir
  defmodule Operacoes do                          
     def soma(n1,n2,n3,n4), do: n1+n2+n3+n4         
     def subtracao(n1,n2,n3,n4), do: n1-n2-n3-n4    
     def multiplicacao(n1,n2,n3,n4), do: n1*n2*n3*n4
     def divisao(n1,n2,n3,n4), do: n1/n2/n3/n4      
  end  
  ```
  Agora quero usar as funções de dentro do módulo Operacoes sem ter que escrever Operacoes.soma, Operacoes.subtracao e etc.

  ```elixir
  import Operacoes

  soma 2,3,4,5,6
  17

  subtracao 2,4,2,8  
  -12

  multiplicacao 2,2,2,2
  16

  divisao 10,2,2,2
  1.25  
  ```
  **Filtrando**

  Perceba que quando executar o comando `import soma`, todas as funções e macros são importadas. Pode ser filtrado usando as opções `only` e `except`.

  Digamos quero importar apenas a função soma do módulo Operacoes, usamos o only.

  ```elixir
  import Operacoes, only: [soma: 4]    
  ```
  Observe que soma foi improtada da seguinte forma [soma: 4], esse "4" tem haver com a aridade da função soma. Teste importar sem o :4 e verifique o que acontece.  

  Se tentar usar as outras funções do modulo Algebricas, será gerado erro:

  ```elixir
  iex(6)> divisao 2,2,2,2  
  ** (CompileError) iex:6: undefined function divisao/4  
  ```
  Agora quero todas as funções do modulo Operacoes, menos a "soma". Para isso acontecer usamos o except:

  ```elixir
  iex(6)> import Operacoes, except: [soma: 4]
  Operacoes
  iex(7)> soma 2,2,3,4
  ** (CompileError) iex:7: undefined function soma/4
  iex(8)> subtracao 2,2,2,2
  -4
  iex(9)> divisao 10,2,1,1
  5.0
  iex(10)>  
  ```
  Analisando o exemplo acima, percebe-se que quando tento usar a função soma do módulo Algebricas e gerado um erro.

  Ainda existe dois átomos ou atom especiais que são, :function e :macros, que tem como objetico importar apenas funções e macros, repectativamente.        

 * **require**

 Elixir fornece `macros` como mecanismo de meta-programação (código de escrita que gera código).
 As macros são expandidas em tempo de compilação.

As funções públicas em módulos estão disponíveis globalmente, mas para usar `macros`,
você precisa optar por entrar, exigindo que o módulo esteja definido.

```elixir
#Verifica se o número é par
iex> Integer.is_even(4)
** (UndefinedFunctionError) function Integer.is_even/1 is undefined or private. However there is a macro with the same name and arity. Be sure to require Integer if you intend to invoke this macro
   (elixir) Integer.is_even(4)


iex> require Integer
Integer


iex> Integer.is_even(4)
true
```

Em Elixir, Ineger.is_even é definido como uma `macro`.
Isso significa que, para invocar `Integer.is_even / 1`, precisamos primeiro exigir o módulo Integer.

 * **use**

 Quando você chama o `use` em seu módulo, é chamado o macro `__using__` dos módulos em que o desenvolvedor pode gerar qualquer código que eles desejem.
Ele também possui uma lista de argumentos.

```elixir

defmodule LibraryGithubElixir do
  defmacro __using__(_) do
    quote do
      def print(s), do: IO.puts(s)
    end
  end
end
```
Aqui nós definimos um módulo  `__using__` macro.
Injetamos uma função `print / 1` que, quando chamada, imprime o que for passado para ela.

```elixir

defmodule MyLib do
  use LibraryGithubElixir
end

iex> MyLib.print("Hello Elixir")
Hello Elixir
:ok
```

## 11 Recursividade
A recursividade é a definição de uma sub-rotina (função ou método) que pode invocar a si mesma, até que uma condição seja atingida e resolva um determinado problema.
+No exemplo a seguir, o modulo `Repetir` imprime uma msg 10x:

```elixir
defmodule Repetir do
  def imprimir_varias_vezes(msg, n) when n <= 1 do
    IO.puts msg
end

def imprimir_varias_vezes(msg, n) do
    IO.puts msg
    imprimir_varias_vezes(msg, n - 1)
  end
end

iex>Repetir.imprimir_varias_vezes("Elixir", 10)
```

## 0 Mix
A funcionalidade do `MIX` é construir projetos, gerenciar dependências e execução de tarefas.

Com essa interface de linha de comando, além de criar projetos com toda a estrutura de pastas predefinidas, pode-se também customizar tarefas.

O `MIX` por padrão já vem instalado juntamente como o `Elixir`. E a melhor maneira de entendermos o `Mix` é utilizando, vamos a prática. Será criado um projeto novo, faremos a analise de cada arquivo e pasta que vair ser gerado.

Para criar um projeto basta digitar no terminal mix new <nome do projeto>, esse comando gerará toda a estrutura do projeto e todas as pastas necessárias para executá-lo.

```Elixir
$ mix new app
* creating README.md
* creating .gitignore
* creating mix.exs
* creating config
* creating config/config.exs
* creating lib
* creating lib/app.ex
* creating test
* creating test/test_helper.exs
* creating test/app_test.exs

Your Mix project was created successfully.
You can use "mix" to compile it, test it, and more:

    cd app
    mix test

Run "mix help" for more commands.
```
No exemplo acima foi criado um projeto chamado app, observe que depois de executar o comando, o terminal mostra as pastas que foram ciradas e informa que é possível utilizar o Mix também para compilar e testar o projeto. Agora será feita uma breve explicação sobre a estrutura.

### README
Este arquivo é usado por sistema de controle de versão, como o GIT. Ele descreve o que o projeto faz, como ele faz e informações necessárias para executá-lo.

//README.md

```elixir
# App

**TODO: Add description**

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `app` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [{:app, "~> 0.1.0"}]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/app](https://hexdocs.pm/app).
```

O README também informa que o projeto pode ser incluido no HEX, que é o gerenciador de dependências do Elixir, serve para mostrar a outros desenvolvedores como colocar seu projeto como uma dependência externa.

###MIX.EXS
Esse arquivo é um módulo, que gerencia todas as dependências do projeto. Nele é possível incluir dependências necessárias para o projeto carregar e informa a versão do elixir necessária para executá-lo.

//mix.exs

```elixir
defmodule App.Mixfile do
  use Mix.Project

  def project do
    [app: :app,
     version: "0.1.0",
     elixir: "~> 1.4",
     build_embedded: Mix.env == :prod,
     start_permanent: Mix.env == :prod,
     deps: deps()]
  end

  # Configuration for the OTP application
  #
  # Type "mix help compile.app" for more information
  def application do
    # Specify extra applications you'll use from Erlang/Elixir
    [extra_applications: [:logger]]
  end

  # Dependencies can be Hex packages:
  #
  #   {:my_dep, "~> 0.3.0"}
  #
  # Or git/path repositories:
  #
  #   {:my_dep, git: "https://github.com/elixir-lang/my_dep.git", tag: "0.1.0"}
  #
  # Type "mix help deps" for more examples and options
  defp deps do
    []
  end
end
```

A função `application` do módulo `mix.exs` carrega dependências externas necessárias para carregar a aplicação principal. Em quanto que a função `deps` carrega e faz download de todas as dependências.

### TESTS
Essa pasta contém todos os testes do seu projeto. tudo que for teste será criado aqui nessa pasta.

//app_test.exs

```elixir
defmodule AppTest do
  use ExUnit.Case
  doctest App

  test "the truth" do
    assert 1 + 1 == 2
  end
end
```

### LIB
Nessa pasta ficará todos os arquivos para execução do seu projeto. Até o momento, só existe um módulo com o mesmo nome do projeto "app".

//app.ex

```elixir
defmodule App do
  @moduledoc """
  Documentation for App.
  """

  @doc """
  Hello world.

  ## Examples

      iex> App.hello
      :world

  """
  def hello do
    :world
  end
end
```
Por convenção cria-se novos módulos dentro de uma pasta com o mesmo nome do projeto, dentro da pasta lib.
Exemplo: lib/app/modulo.ex.

Para fixar melhor ciremos uma pasta app, dentro da pasta lib, em seguida crie um módulo chamado hello.ex, dentro da pasta que criou na pasta lib, ficará assim: lib/app/hello.ex. O nome do módulo se chamará App.Hello, evitando assim conflito com nome, poderia ser qualquer outro nome.

//hello.ex

```elixir
defmodule App.Hello do
   def say(str) do
       str
   end
end
```
Vamos executar o projeto, para isso entre na pasta dele e digite `iex -S mix`. Esse comando compila e execita o projeto.

`$ iex -S mix`

```elixir
iex> App.Hello.say "Frank"  
"Frank"
```

### CONFIG

Essa pasta contém todas as configurações do projeto. O arquivo config.ex contém informações básicas de configuração.

```elixir
# This file is responsible for configuring your application
# and its dependencies with the aid of the Mix.Config module.
use Mix.Config

# This configuration is loaded before any dependency and is restricted
# to this project. If another project depends on this project, this
# file won't be loaded nor affect the parent project. For this reason,
# if you want to provide default values for your application for
# 3rd-party users, it should be done in your "mix.exs" file.

# You can configure for your application as:
#
#     config :elixir, key: :value
#
# And access this configuration in your application as:
#
#     Application.get_env(:elixir, :key)
#
# Or configure a 3rd-party app:
#
#     config :logger, level: :info
#

# It is also possible to import configuration files, relative to this
# directory. For example, you can emulate configuration per environment
# by uncommenting the line below and defining dev.exs, test.exs and such.
# Configuration from the imported file will override the ones defined
# here (which is why it is important to import them last).
#
#     import_config "#{Mix.env}.exs"
```

Este arquivo poder ser usado para passar argumentos para aplicação toda, muito útil para verificar se a aplicação está em ambiente de teste ou de produção.

Vamos criar uma configuração personalizada e acessar dentro da aplicação que criamos anteriormente. Para isso, basta chamar a macro `config`, seguida dos argumentos que queremos utilizar.

//config.exs
```elixir
use Mix.config

config :app, prefix: "Hello "

```

Agora utilizamos esta configuração em nossa aplicação, concatenando a configuração com o argumetno da função, para visualizar o retorno.   

//hello.ex
```elixir
defmodule App.Hello do
  def say(str) do
    Aplication.get_env(:app, :prefix) <> str
  end
end
```

$iex -S mix

```elixir
iex> App.Hello.say "LCA"
"Hello LCA"
```
Ter que chamar Apllication.get_env(:app, :prefix) é uma coisa grande e repetitiva, para solucionar o problema, podemos criar uma variável no escopo do módulo. Estas variáveis podem ser ciradas em qualquer módulo e são pré-fixadas com @.

```elixir
defmodule App.Hello do

  @prefix Application.get_env(:app, :prefix)

  def say(str) do
    @prefix <> str
  end
end
```
$ iex -S mix

```elixir
iex> App.Hello.say "LCA"
"Hello LCA"
```

Podemos usar três argumentos na macro `config`, o primeiro continua sendo o nome da aplicação, já o segundo é o nome do módulo que queremos configurar, e o terceiro é o prefixo com a configuração que já vimos anteriormente.

//config.exs
```elixir
use  Mix.Config

config :app, App.Hello, prefix: "Hello "
```

Agora chamamos a configuração da seguinte forma: precisa iformar o nome da aplicação, seguida do nome do módulo e uma lista com o nome da configuração. Pode-se utilizar a variável `__MODULE__` que contém o nome do módulo atual, `__MODULE__` = App.Hello.

//hello.ex

```elixir
defmodule App.Hello do
  @prefix Application.get_env(:app, __MODULE__)[:prefix]

  def say(str) do
    @prefix <> str
  end
end
```

$ iex -S mix

```elixir
iex> App.Hello.say "LCA"
"Hello LCA"
```
### Configurando aplicação para executar em difere ambientes.

Faremos um exemplo criado configurações separadas para cada um deles: ambiente testes, ambiente de desenvolvimento e outra para o de produção.

Crie na pasta config os seguintes arquivos `test.exs, dev.exs e prod.exs`. faça as seguintes configurações para cada um:

```elixir
//	test.exs
use	Mix.Config
config	:app,	App.Hello,	prefix:	"Test:	"
//	dev.exs
use	Mix.Config
config	:app,	App.Hello,	prefix:	"Dev:	"
//	prod.exs
use	Mix.Config
config	:app,	App.Hello,	prefix:	"Prod:	"
```

Remova a configuração anterior que foi criada no arquivo principal, para não conflitar com as novas configurações. Descomente a seguinte  linha `import_config "#{Mix.env}.exs"`, para que o Mix possa importar as configurações personalizadas.

Vamos executar, é simples, basta executar o Mix passando como argumento o ambiente em que ele será executado.

$MIX_ENV = test iex -S mix

```elixir
iex>	App.Hello.say	"LCA"
"Test:	LCA"

$	MIX_ENV=dev	iex	-S	mix
iex>	App.Hello.say	"LCA"
"Dev:	LCA"
```

BUILD esse pasta contém todos os arquivos compilados que serão executados pela máquina virtual.
