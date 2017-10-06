# Elixir Documentation

### Table of Contents
- Pattern Matching


### Pattern Matching
To understand pattern matching, first lets look at the assignment operator in Elixir and how it is different from the conventional programmming languages we use.
#### Assignment Operator
``` elixir
iex> a = 1      # This is not a regular assignment, though it appears that way.
1
iex> a + 3
4
iex> 2 = a      # Results in a error as matching can't be done.
** (MatchError) no match of right hand side value: 1
```
Here assignment operator is like an asserion. It succeeds only if there is way to match the left side of the assignment operator to the right side. Elixir calls `=` match operator. In the above example, elixir matches 1 to a (binds the value of 1 to a). `2 = a` fails as the value 1 in a can't be binded to 2.

##### Some more examples of pattern matching with `=` operator.
[1,2,3] represents a list in elixir and the list has 3 elements. A list in elixir is heterogenuous.
``` elixir
iex> list = [1, 2, [ 3, 4, 5 ] ]
[1, 2, [3, 4, 5]]
iex> [a, b, c ] = list
[1, 2, [3, 4, 5]]
iex> a
1
iex> b
2
iex> c
[3, 4, 5]
``` 

``` elixir
iex> list = [1, 2, 3]
[1, 2, 3]
iex> [a, 1, b ] = list
** (MatchError) no match of right hand side value: [1, 2, 3]
```

##### Wildcard operator
``` elixir
iex> [1, _, _] = [1, 2, 3]
[1, 2, 3]
iex> [1, _, _] = [1, "cat", "dog"]
[1, "cat", "dog"]
```

`_` accepts any value. It acts like a wild card.

#### Pin operator 
Forced elixir to use the existing value of the variable.
``` elixir
iex> a = 1
1
iex> a = 2
2
iex> ^a = 1
** (MatchError) no match of right hand side value: 1
```

### Immutability in Elixir
In Elixir, all values are immutable. Lets consider a list `a = [1,2,3]`. When `4` is appended to the list, a new list is formed instead of the old one being modified. The original list remains as is but a new list is formed with the added element.


### Elixir basics
##### Atoms
Atoms are constants. An atom's name is its value. Two atoms with the same value will always compare as being equal even if they were created by different applications on different computers. We write them using a leading colon `:`. We will use atoms a lot to tag values.
``` elixir
:fred 
:is_binary? 
:var@2
```
#### Ranges
Ranges are represented as ```start..end```, where start and end are integers.

#### Regular Expressions

#### PIDs and Ports
A PID is a reference to a local or remote process and port is a reference to a resource that you will be reading or writing to. The PID of the current process is available by calling `self`. A new PID is created when a process is spawned.

#### Collection Types
#####Tuples
A tuple is an ordered collection of values. As with all Elixir data structures, once created a tuple cannot be modified. You write a tuple between braces, separating the elements with commas.
``` elixir
{ 1, 2 } 
{ :ok, 42, "next" } 
{ :error, :enoent }
```

##### Lists
The list in elixir is not like an array in conventional programming languages. Instead list is linked data structure. Some operators on lists : 
``` elixir
iex> [ 1, 2, 3 ] ++ [ 4, 5, 6 ] # concatenation
[1, 2, 3, 4, 5, 6]
iex> [1, 2, 3, 4] -- [2, 4] # difference
[1, 3]
iex> 1 in [1,2,3,4] # membership
true
iex> "wombat" in [1, 2, 3, 4]
false
```

##### Keyword Lists
They are simple lists of key/value pairs.
``` elixir
[ name: "Dave", city: "Dallas", likes: "Programming" ]
```
Elixir converts it into a list of two-value tuples:
``` elixir
[ {:name, "Dave"}, {:city, "Dallas"}, {:likes, "Programming"} ]
```

##### Maps
A map is a collection of key/value pairs. A map literal looks like this.
``` elixir
%{ key => value, key => value }
```

``` elixir
iex> states = %{ "AL" => "Alabama", "WI" => "Wisconsin" }
%{"AL" => "Alabama", "WI" => "Wisconsin"}
iex> responses = %{ { :error, :enoent } => :fatal, { :error, :busy } => :retry }
%{{:error, :busy} => :retry, {:error, :enoent} => :fatal}
iex> colors = %{ :red => 0xff0000, :green => 0x00ff00, :blue => 0x0000ff }
%{blue: 255, green: 65280, red: 16711680}
```
Maps allow only one entry for a particular key, whereas keyword lists allow the key to be repeated

To access elements in a map :
``` elixir
iex> states = %{ "AL" => "Alabama", "WI" => "Wisconsin" }
%{"AL" => "Alabama", "WI" => "Wisconsin"}
iex> states["AL"]
"Alabama"
iex> states["TX"]
nil
iex> response_types = %{ { :error, :enoent } => :fatal,
...> { :error, :busy } => :retry }
%{{:error, :busy} => :retry, {:error, :enoent} => :fatal}
iex> response_types[{:error,:busy}]
:retry
```

If keys are atoms, you can use the dot notation.
``` elixir
iex> colors = %{ red: 0xff0000, green: 0x00ff00, blue: 0x0000ff }
%{blue: 255, green: 65280, red: 16711680}
iex> colors[:red]
16711680
iex> colors.green
65280
```

### Operators
##### Truth
Elixir has three special values related to Boolean operations: true, false, and nil. nil is treated as false in Boolean contexts.
(A bit of trivia: all three of these values are aliases for atoms of the same name, so true is the same as the atom :true.)
In most contexts, any value other than false or nil is treated as true. We sometimes refer to this as truthy as opposed to true.

##### Comparision Operators
``` elixir
a === b # strict equality (so 1 === 1.0 is false)
a !== b # strict inequality (so 1 !== 1.0 is true)
a == b # value equality (so 1 == 1.0 is true)
a != b # value inequality (so 1 != 1.0 is false)
a > b # normal comparison
a >= b # :
a < b # :
a <= b # :
```

##### Boolean Operators
``` elixir
a or b # true if a is true, otherwise b
a and b # false if a is false, otherwise b
not a # false if a is true, true otherwise
```

##### Relaxed Boolean Operators.
``` elixir
a || b # a if a is truthy, otherwise b
a && b # b if a is truthy, otherwise a
!a # false if a is truthy, otherwise true
```

##### Arithmetic Operators
``` elixir
+ - * / div rem
```
Integer division yields a floating-point result. Use div(a,b) to get an integer. rem is the remainder operator. It is called as a function (rem(11, 3) => 2).

##### Join Operators
``` elixir
binary1 <> binary2 # concatenates two binaries (later we'll
# see that binaries include strings)
list1 ++ list2 # concatenates two lists
list1 -- list2 # removes elements of list2 from a
# copy of list 1
```

##### The in operator
``` elixir
a in enum # tests if a is included in enum (for example,
# a list, a range, or a map). For maps, a should
# be a {key, value} tuple
```

### Variable Scope
Elixir is lexically scoped. The basic unit of scoping is the function body. Variables defined in a function (including its parameters) are local to that function. In addition, modules define a scope for local variables, but these are only accessible at the top level of that module, and not in functions defined in the module.

##### The with expression
The with expression serves double duty. First, it allows you to define a local scope for variables: if you need a couple of temporary variables when calculating something, and don’t want those variables to leak out into the wider scope, use with. Second, it gives you some control over pattern matching failures.

For example, the /etc/passwd file contains lines such as :
```
_installassistant:*:25:25:Install Assistant:/var/empty:/usr/bin/false
_lp:*:26:26:Printing Services:/var/spool/cups:/usr/bin/false
_postfix:*:27:27:Postfix Mail Server:/var/spool/postfix:/usr/bin/false
```

This code finds the values of the _lp_ user.
``` elixir
content = "Now is the time"
lp = with {:ok, file} = File.open("/etc/passwd"),
                        content = IO.read(file, :all),
                        :ok = File.close(file),
                        [_, uid, gid] = Regex.run(~r/_lp:.*?:(\d+):(\d+)/, content)
do
  "Group: #{gid}, User: #{uid}"
end
IO.puts lp #=> Group: 26, User: 26
IO.puts content #=> Now is the time
```
The with expression lets us work with what are effectively temporary variables as we open the file, read its content, close it, and search for the line we want. The value of the with is the value of its do parameter. The inner variable content is local to the with, and does not affect the variable in the outer scope.

##### with and Pattern Matching
In the previous example, the head of the with expression used = for basic pattern matches. If any of these had failed, a MatchError exception would be raised. But perhaps we’d want to handle this case in a more elegant way. That’s where the <- operator comes in. If you use <- instead of = in a with expression, it performs a match, but if it fails it returns the value that couldn’t be matched.

``` elixir
iex> with [a|_] <- [1,2,3], do: a
1
iex> with [a|_] <- nil, do: a
nil
```
We can use this to let the with in the previous example return nil if the user can’t be found, rather than raising an exception.

``` elixir
result = with {:ok, file} = File.open("/etc/passwd"),
                            content = IO.read(file, :all),
                            :ok = File.close(file),
                            [_, uid, gid] <- Regex.run(~r/xxx:.*?:(\d+):(\d+)/, content)
do
  "Group: #{gid}, User: #{uid}"
end
IO.puts inspect(result) #=> nil
```

### Anonymous Functions
An anonymous function is created using the fn keyword.
``` elixir
fn
  parameter-list -> body
  parameter-list -> body ...
end
```
Think of fn…end as being a bit like the quotes that surround a string literal, except here we’re returning a function as a value, not a string. We can pass that function value to other functions. We can also invoke it, passing in arguments.

At its simplest, a function has a parameter list and a body, separated by ->. For example, the following defines a function, binding it to the variable sum, and then calls it:

``` elixir
iex> sum = fn (a, b) -> a + b end
#Function<12.17052888 in :erl_eval.expr/5>
iex> sum.(1, 2)
3
```
The dot indicates the function call, and the arguments are passed between parentheses. We don't use . for named functions.

##### One function, Multiple bodies
A single function definition lets you define different implementations, depending on the type and contents of the arguments passed. You cannot select based on the number of arguments—each clause in the function definition must have the same number of parameters.

At its simplest, we can use pattern matching to select which clause to run. In the example that follows, we know the tuple returned by File.open has :ok as its first element if the file was opened, so we write a function that displays either the first line of a successfully opened file or a simple error message if the file could not be opened.

``` elixir
iex> handle_open = fn
...> {:ok, file} -> "Read data: #{IO.read(file, :line)}"
...> {_, error} -> "Error: #{:file.format_error(error)}"
...> end
#Function<12.17052888 in :erl_eval.expr/5>
iex> handle_open.(File.open("code/intro/hello.exs")) # this file exists
"Read data: IO.puts \"Hello, World!\"\n"
iex> handle_open.(File.open("nonexistent")) # this one doesn't
"Error: no such file or directory"
```

##### Functions can return functions
```
iex> fun1 = fn -> fn -> "Hello" end end
#Function<12.17052888 in :erl_eval.expr/5>
iex> fun1.()
#Function<12.17052888 in :erl_eval.expr/5>
iex> fun1.().()
"Hello"
```

#####  Functions remmeber their original environment.
``` elixir
iex> greeter = fn name -> (fn -> "Hello #{name}" end) end
#Function<12.17052888 in :erl_eval.expr/5>
iex> dave_greeter = greeter.("Dave")
#Function<12.17052888 in :erl_eval.expr/5>
iex> dave_greeter.()
"Hello Dave"
```

This works because functions in Elixir automatically carry with them the bindings of variables in the scope in which they are defined. In our example, the variable name is bound in the scope of the outer function. When the inner function is defined, it inherits this scope and carries the binding of name around with it. This is a closure—the scope encloses the bindings of its variables, packaging them into something that can be saved and used later. 

##### Passing functions as arguments.
``` elixir
iex> times_2 = fn n -> n * 2 end
#Function<12.17052888 in :erl_eval.expr/5>
iex> apply = fn (fun, value) -> fun.(value) end
#Function<12.17052888 in :erl_eval.expr/5>
iex> apply.(times_2, 6)
12
```
We use the ability to pass functions around pretty much everywhere in Elixir code. For example, the built-in Enum module has a function called map. It takes two arguments: a collection and a function. It returns a list that is the result of applying that function to each element of the collection.

``` elixir
iex> list = [1, 3, 5, 7, 9]
[1, 3, 5, 7, 9]
iex> Enum.map list, fn elem -> elem * 2 end
[2, 6, 10, 14, 18]
iex> Enum.map list, fn elem -> elem * elem end
[1, 9, 25, 49, 81]
iex> Enum.map list, fn elem -> elem > 6 end
[false, false, false, true, true]
```
##### The & Notation.
``` elixir
iex> add_one = &(&1 + 1) # same as add_one = fn (n) -> n + 1 end
#Function<6.17052888 in :erl_eval.expr/5>
iex> add_one.(44)
45
iex> square = &(&1 * &1)
#Function<6.17052888 in :erl_eval.expr/5>
iex> square.(8)
64
iex> speak = &(IO.puts(&1))
&IO.puts/1
iex> speak.("Hello")
Hello
:ok
```

``` elixir
iex> divrem = &{ div(&1,&2), rem(&1,&2) }
#Function<12.17052888 in :erl_eval.expr/5>
iex> divrem.(13, 5)
{2, 3}
```

### Modules and Named Functions
Elixir code can be broken down into functions and these functions can be organized into modules.
``` elixir
defmodule Times do
  def double(n) do
    n * 2
  end
end
```

The functions body is a block. The do…end block is one way of grouping expressions and passing them to other code. They are used in module and named function definitions, control structures…any place in Elixir where code needs to be handled as an entity.

However, do…end is not actually the underlying syntax. The actual syntax looks like this:
``` elixir
def greet(greeting, name), do: (
  IO.puts greeting
  IO.puts "How're you doing, #{name}?"
  )
```

##### Function calls and Pattern Matching
we saw how anonymous functions use pattern matching to bind their parameter list to the passed arguments. The same is true of named functions. The difference is that we write the function multiple times, each time with its own parameter list and body.

When you call a named function, Elixir tries to match your arguments with the parameter list of the first definition (clause). If it cannot match them, it tries the next definition of the same function (remember, this must have the same arity) and checks to see if it matches. It continues until it runs out of candidates.

``` elixir
defmodule Factorial do
  def of(0), do: 1
  def of(n), do: n * of(n-1)
end
```

##### Gaurd Clauses
We’ve seen that pattern matching allows Elixir to decide which function to invoke based on the arguments passed. But what if we need to distinguish based on their types or on some test involving their values? For this, you use guard clauses. These are predicates that are attached to a function definition using one or more when keywords. When doing pattern matching, Elixir first does the conventional parameter-based match and then evaluates any when predicates, executing the function only if at least one predicate is true.

``` elixir
defmodule Guard do
  def what_is(x) when is_number(x) do
    IO.puts "#{x} is a number"
  end
  def what_is(x) when is_list(x) do
    IO.puts "#{inspect(x)} is a list"
  end
  def what_is(x) when is_atom(x) do
    IO.puts "#{x} is an atom"
  end
end
Guard.what_is(99) # => 99 is a number
Guard.what_is(:cat) # => cat is an atom
Guard.what_is([1,2,3]) # => [1,2,3] is a list
```

##### Gaurd Clause Limitations
You can write only a subset of Elixir expressions in guard clauses.
- Comparision Operators  :  ==, !=, ===, !==, >, <, <=, >=
- Boolean and negation operators  : or, and, not, !. Note that || and && are not allowed.
- Arithmetic Operators  : +, -, /
- Join Operators  : <> and ++, as long as the left side is a literal.
- The in Operator : 
- Type-check functions  : is_atom is_binary is_bitstring is_boolean is_exception is_float is_function is_integer is_list is_map is_number is_pid is_port is_record is_reference is_tuple
- Other functions : abs(number) bit_size(bitstring) byte_size(bitstring) div(number,number) elem(tuple, n) float(term) hd(list) length(list) node() node(pid|ref|port) rem(number,number) round(number) self() tl(list) trunc(number) tuple_size(tuple)

##### Default Parameters
``` elixir
defmodule Example do
  def func(p1, p2 \\ 2, p3 \\ 3, p4) do
    IO.inspect [p1, p2, p3, p4]
  end
end
Example.func("a", "b") # => ["a",2,3,"b"]
Example.func("a", "b", "c") # => ["a","b",3,"c"]
Example.func("a", "b", "c", "d") # => ["a","b","c","d"]
```

##### The Amazing Pipe Operator: |>
filing = DB.find_customers
          |> Orders.for_customers
          |> sales_tax(2016)
          |> prepare_filing
          
The |> operator takes the result of the expression to its left and inserts it as the first parameter of the function invocation to its right. So the list of customers the first call returns becomes the argument passed to the for_customers function. The resulting list of orders becomes the first argument to sales_tax, and the given parameter, 2016, becomes the second.

`you should always use parentheses around function parameters in pipelines.`

### Modules
Modules provide namespace for things you define. They encapsulate named functions and they also act as wrappers for macros, structs, protocols and other modules.
``` elixir
defmodule Mod do
  def func1 do
    IO.puts "in func1"
  end
  def func2 do
    func1
    IO.puts "in func2"
  end
end
Mod.func1
Mod.func2
```
Nested modules are also allowed in elixir
```elixir
defmodule Outer do
  defmodule Inner do
    def inner_func do
    end
  end
  def outer_func do
    Inner.inner_func
  end
end
Outer.outer_func
Outer.Inner.inner_func
```

#### Directives for Modules
Elixir has three directives that simplify working with modules. All three are executed as your program runs, and the effect of all three is lexically scoped—it starts at the point the directive is encountered, and stops at the end of the enclosing scope. This means a directive in a module definition takes effect from the place you wrote it until the end of the module; a directive in a function definition runs to the end of the function.

###### The import directive
The import directive brings a module’s functions and/or macros into the current scope. If you use a particular module a lot in your code, import can cut down the clutter in your source files by eliminating the need to repeat the module name time and again.

``` elixir
defmodule Example do
  def func1 do
    List.flatten [1,[2,3],4]
  end
  def func2 do
    import List, only: [flatten: 1]
    flatten [5,[6,7],8]
  end
end
```

###### The alias directive
The alias directive creates an alias for a module. One obvious use is to cut down on typing.
``` elixir
defmodule Example do
  def compile_and_go(source) do
    alias My.Other.Module.Parser, as: Parser
    alias My.Other.Module.Runner, as: Runner
    source
    |> Parser.parse()
    |> Runner.execute()
  end
end
```

###### The require directive
You require a module if you want to use any macros it defines. This ensures that the macro definitions are available when your code is compiled.

#### The Module attributes
Elixir modules each have associated metadata. Each item of metadata is called an attribute of the module and is identified by a name. Inside a module, you can access these attributes by prefixing the name with an at sign (@). You give an attribute a value using the syntax

``` elixir
@name value
```

This works only at the top level of a module—you can’t set an attribute inside a function definition. You can, however, access attributes inside functions.
``` elixir
defmodule Example do
  @author "Dave Thomas"
  def get_author do
    @author
  end
end
IO.puts "Example was written by #{Example.get_author}"
```
These attributes are not variables in the conventional sense. Use them for configuration and metadata only.

#### Calling a function in Erlang library
The Erlang conventions for names are different—variables start with an uppercase letter and atoms are simple lowercase names. So, for example, the Erlang module timer is called just that, the atom timer. In Elixir we write that as :timer. If you want to refer to the tc function in timer, you’d write :timer.tc.

### Lists and Recursion
A list may either be empty or consist of a head and a tail. The head contains a value and the tail is itself a list. This is a recursive definition. We’ll represent the empty list like this: \[\].
Let’s imagine we could represent the split between the head and the tail using
a pipe character, |. The single element list we normally write as \[3\] can be
written as the value 3 joined to the empty list:
`[ 3 | [] ]`

``` elixir
iex> [a, b, c ] = [ 1, 2, 3 ]
[1, 2, 3]
iex> a
1
iex> b
2
iex> c
3
```

``` elixir
iex> [ head | tail ] = [ 1, 2, 3 ]
[1, 2, 3]
iex> head
1
iex> tail
[2, 3]
```

Recursive function to find the length of a list
``` elixir
defmodule MyList do
  def len([]), do: 0
  def len([head|tail]), do: 1 + len(tail)
end
```

function map takes a list, function and returns a new list containing the result of
applying that function to each element in the original.
```elixir
def map([], _func), do: []
def map([ head | tail ], func), do: [ func.(head) | map(tail, func) ]
```

##### Keeping track of values during recursion
``` elixir
defmodule MyList do
  def sum([], total), do: total
  def sum([ head | tail ], total), do: sum(tail, head+total)
end
```

``` elixir
defmodule MyList do
  def sum(list), do: _sum(list, 0)
  # private methods
  defp _sum([], total), do: total
  defp _sum([ head | tail ], total), do: _sum(tail, head+total)
end
```

##### List of lists
Let’s imagine we had recorded temperatures and rainfall at a number of weather stations. Each reading looks like this:
```[ timestamp, location_id, temperature, rainfall ]```
Our code is passed a list containing a number of these readings, and we want to report on the conditions for one particular location, number 27.
```elixir
defmodule WeatherHistory do
  def for_location_27([]), do: []
  def for_location_27([ [time, 27, temp, rain ] | tail]) do
    [ [time, 27, temp, rain] | for_location_27(tail) ]
  end
  def for_location_27([ _ | tail]), do: for_location_27(tail)
end
```
Our function is specific to a particular location, which is pretty limiting. We’d like to be able to pass in the location as a parameter. We can use pattern matching for this.
``` elixir
defmodule WeatherHistory do
  def for_location([], _target_loc), do: []
  def for_location([ [time, target_loc, temp, rain ] | tail], target_loc) do
    [ [time, target_loc, temp, rain] | for_location(tail, target_loc) ]
  end
  def for_location([ _ | tail], target_loc), do: for_location(tail, target_loc)
end
```

More improvement
``` elixir
defmodule WeatherHistory do
  def for_location([], _target_loc), do: []
  def for_location([ head = [_, target_loc, _, _ ] | tail], target_loc) do
    [ head | for_location(tail, target_loc) ]
  end
  def for_location([ _ | tail], target_loc), do: for_location(tail, target_loc)
end
```

##### The List Module
```elixir
#
# Concatenate lists
#
iex> [1,2,3] ++ [4,5,6]
[1, 2, 3, 4, 5, 6]
#
# Flatten
#
iex> List.flatten([[[1], 2], [[[3]]]])
[1, 2, 3]
#
# Folding (like reduce, but can choose direction)
#
iex> List.foldl([1,2,3], "", fn value, acc -> "#{value}(#{acc})" end)
"3(2(1()))"
iex> List.foldr([1,2,3], "", fn value, acc -> "#{value}(#{acc})" end)
"1(2(3()))"
#
# Updating in the middle (not a cheap operation)
#
iex> list = [ 1, 2, 3 ]
[ 1, 2, 3 ]
iex> List.replace_at(list, 2, "buckle my shoe")
[1, 2, "buckle my shoe"]
#
# Accessing tuples within lists
#
iex> kw = [{:name, "Dave"}, {:likes, "Programming"}, {:where, "Dallas", "TX"}]
[{:name, "Dave"}, {:likes, "Programming"}, {:where, "Dallas", "TX"}]
iex> List.keyfind(kw, "Dallas", 1)
{:where, "Dallas", "TX"}
iex> List.keyfind(kw, "TX", 2)
{:where, "Dallas", "TX"}
iex> List.keyfind(kw, "TX", 1)
nil
iex> List.keyfind(kw, "TX", 1, "No city called TX")
"No city called TX"
iex> kw = List.keydelete(kw, "TX", 2)
[name: "Dave", likes: "Programming"]
iex> kw = List.keyreplace(kw, :name, 0, {:first_name, "Dave"})
[first_name: "Dave", likes: "Programming"]
```

### Enum - Processing collections
- Convert any collection into a list
``` elixir
iex> list = Enum.to_list 1..5
[1, 2, 3, 4, 5]
```
- Concatenate collections
``` elixir
iex> Enum.concat([1,2,3], [4,5,6])
[1, 2, 3, 4, 5, 6]
iex> Enum.concat [1,2,3], 'abc'
[1, 2, 3, 97, 98, 99]
```
- Create collections whose elements are some function of the original
``` elixir
iex> Enum.map(list, &(&1 * 10))
[10, 20, 30, 40, 50]
iex> Enum.map(list, &String.duplicate("*", &1))
["*", "**", "***", "****", "*****"]
```
- Select elements by postion or criteria
``` elxir
iex> Enum.at(10..20, 3)
13
iex> Enum.at(10..20, 20)
nil
iex> Enum.at(10..20, 20, :no_one_here)
:no_one_here
iex> Enum.filter(list, &(&1 > 2))
[3, 4, 5]
iex> require Integer # to get access to is_even
nil
iex> Enum.filter(list, &Integer.is_even/1)
[2, 4]
iex> Enum.reject(list, &Integer.is_even/1)
[1, 3, 5]
```

- Sort and compare elements
``` elixir
iex> Enum.sort ["there", "was", "a", "crooked", "man"]
["a", "crooked", "man", "there", "was"]
iex> Enum.sort ["there", "was", "a", "crooked", "man"],
...> &(String.length(&1) <= String.length(&2))
["a", "was", "man", "there", "crooked"]
iex(4)> Enum.max ["there", "was", "a", "crooked", "man"]
"was"
iex(5)> Enum.max_by ["there", "was", "a", "crooked", "man"], &String.length/1
"crooked"
```

- Split a collection
``` elixir
iex> Enum.take(list, 3)
[1, 2, 3]
iex> Enum.take_every list, 2
[1, 3, 5]
iex> Enum.take_while(list, &(&1 < 4))
[1, 2, 3]
iex> Enum.split(list, 3)
{[1, 2, 3], [4, 5]}
iex> Enum.split_while(list, &(&1 < 4))
{[1, 2, 3], [4, 5]}
```

- Join a collection
``` elixir
iex> Enum.join(list)
"12345"
iex> Enum.join(list, ", ")
"1, 2, 3, 4, 5"
```

- Predicate operations
``` elixir
iex> Enum.all?(list, &(&1 < 4))
false
iex> Enum.any?(list, &(&1 < 4))
true
iex> Enum.member?(list, 4)
true
iex> Enum.empty?(list)
false
```
- Merge collections
``` elixir
iex> Enum.zip(list, [:a, :b, :c])
[{1, :a}, {2, :b}, {3, :c}]
iex> Enum.with_index(["once", "upon", "a", "time"])
[{"once", 0}, {"upon", 1}, {"a", 2}, {"time", 3}]
```

- Fold elements into a single value
``` elixir
iex> Enum.reduce(1..100, &(&1+&2))
5050
iex> Enum.reduce(["now", "is", "the", "time"],fn word, longest ->
...>    if String.length(word) > String.length(longest) do
...>      word
...>    else
...>      longest
...>    end
...> end)
"time"
```

### Control Flow

##### if and unless
``` elixir
iex> if 1 == 1 do
...>  "true part"
...> else
...>  "false part"
...> end
true part
```

unless is similar
``` elixir
iex> unless 1 == 1, do: "error", else: "OK"
"OK"
iex> unless 1 == 2, do: "OK", else: "error"
"OK"
iex> unless 1 == 2 do
...>  "OK"
...> else
...>  "error"
...> end
"OK"
```

