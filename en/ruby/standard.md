# Ruby Style Guide
**References**:
- https://github.com/rubocop-hq/ruby-style-guide
- https://github.com/github/rubocop-github/blob/master/STYLEGUIDE.md
- https://github.com/framgia/coding-standards/blob/master/eng/ruby/standard.md

-----

### Source Code Layout

-----

* Use only spaces for indentation. No hard tabs.

* Use two spaces per indentation level (soft tabs).

```ruby
# bad - four spaces
def some_method
    do_something
end

# good
def some_method
  do_something
end
```

* Indent `when` as deep as `case`.

```ruby
# bad
case user.name
  when "Nara"
    puts "Hi Nara!"
  when "Jang"
    puts "Hi jang!"
  else
    puts "Hi!"
end

# good
case user.name
when "Nara"
  puts "Hi Nara!"
when "Jang"
  puts "Hi jang!"
else
  puts "Hi!"
end
```

* When assigning the result of a conditional expression to a variable, preserve the usual alignment of its branches.

```ruby
# bad
kind = case year
when 1..5 then "small"
when 6..10 then "medium"
else "large"
end

result = if some_cond
  calc_something
else
  calc_something_else
end

# good
kind = case year
       when 1..5 then "small"
       when 6..10 then "medium"
       else "large"
       end

result = if some_cond
           calc_something
         else
           calc_something_else
         end

# good
kind =
  case year
  when 1..5 then "small"
  when 6..10 then "medium"
  else "large"
  end

result =
  if some_cond
    calc_something
  else
    calc_something_else
  end
  ```

* Limit lines to **80** characters.

  If it is a string of methods, break line before dot `.` and let the dot `.` be the start of new line

```ruby
some_method.some_long_method(arg)
  .other_long_method(arg1)
  .other_long_method_2(arg2)
```

* Avoid trailing whitespace.

* End each file with a newline.

* Don’t use `;` to terminate statements and expressions.

```ruby
# bad
puts "it is bad";

# good
puts "it is good"
```

* Use one expression per line.

```ruby
# bad
puts 'foo'; puts 'bar' # two expressions on the same line

# good
puts 'foo'
puts 'bar'
```

* Use spaces around operators, after commas `,`, colons `:`.

```ruby
sum = 1 + 2
a, b = 1, 2
1 > 2 ? true : false
```

* Use spaces around `{` and before `}`.

```ruby
[1, 2, 3].each { |e| puts e }
```

* But with interpolated expressions, there should be no padded-spacing inside the braces.

```ruby
# bad
"From: #{ user.first_name }, #{ user.last_name }"

# good
"From: #{user.first_name}, #{user.last_name}"
```

* No spaces after `(`, `[` or before `]`, `)`.

```ruby
some(arg).other
[1, 2, 3].length
```

* No space inside range literals.

```ruby
# bad
1 .. 3
'a' ... 'z'

# good
1..3
'a'...'z'
```

* No spaces after `!`.

```ruby
!array.include?(element)
```

* Add 1 space after arguments.

```ruby
# bad
arr.each{ |elem|puts elem }

# good
arr.each{ |elem| puts elem }
```

* Add 1 space between `do` and argument.

```ruby
# bad
arr.each do|elem|
  puts elem
end

# good
arr.each do |elem|
  puts elem
end
```

* Use spaces around the `=` operator when assigning default values to method parameters:

```ruby
# bad
def some_method(arg1=:default, arg2=nil, arg3=[])
  # do something...
end

# good
def some_method(arg1 = :default, arg2 = nil, arg3 = [])
  # do something...
end
```

* There is no  spaces between method name and arguments.

```ruby
# bad
total (3 + 2) + 1

# good
total(3 + 2) + 1
```

* Add 1 space after comment out character `#`.

```
#this is a bad comment

# this is a good comment
```

* Use empty lines between method definitions and also to break up methods into logical paragraphs internally.

```ruby
def some_method
  logic_1

  logic_2

  result
end

def other_method
  result
end
```

* Don’t use several empty lines in a row.

```ruby
# bad
def some_method
  logic


  result
end

# goof
def some_method
  logic

  result
end
```

* Use empty lines around access modifiers.

```ruby
# bad
class Foo
  attr_reader :foo
  def foo
    # do something...
  end
end

# good
class Foo
  attr_reader :foo

  def foo
    # do something...
  end
end
```

* Don’t use empty lines around method, class, module, block bodies.

```ruby
# bad
class Foo

  def foo

    begin

      do_something do

        something

      end

    rescue

      something

    end

  end

end

# good
class Foo
  def foo
    begin
      do_something do
        something
      end
    rescue
      something
    end
  end
end
```

### Syntax

-----

* Do not use `()` in method definition.

```ruby
def some_method
  # some proccesses
end

def other_method arg1, arg2
  # some proccesses
end
```

* Do not use `()` when calling method.

* Do not use `for`

```ruby
arr = [1, 2, 3]

# bad
for elem in arr do
  puts elem
end

# good
arr.each{ |elem| puts elem }
```

* Do not use `then`

```ruby
# bad
if some_condition then
  # some proccesses
end

# goof
if some_condition
  # some proccesses
end
```

* Avoid multi-line `?:` (the conditional operator), use `if/unless` instead.

```ruby
# bad
name = user.actived? ?
  'Nara'
  :
  'Jang'

# good
weather = user.actived? ? 'Nara' : 'Jang'
```

* Do not use nested conditional operators.

```ruby
# bad
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

# goof
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
```

* Use short style for `if/unless` when it is possible to write less than 80 characters in a line.

```ruby
# bad
if some_condition
  do_something
end

# good
do_something if some_condition
```

* Never use `unless` with `else`.
```ruby
# bad
unless success?
  puts "failure"
else
  puts "success"
end

# good
if success?
  puts "success"
else
  puts "failure"
end
```

* Do not use `!` in `if` conditional clause (if necessary use `unless`). However we can still use `!` with `&&` or `||`.

```ruby
# bad
if !user.nil?
  user.greeting
end

# good
unless user.nil?
  user.greeting
end

# better
if user
  user.greeting
end

# better
user.greeting if user

# OK
if !user.nil? && !user.suspended?
  user.greeting
end
```

* Use `&&` and `||` instead of `and` and `or` if possible.

* Do not use () in conditional clause of if/unless/while
```ruby
# bad
if (x > 10)
  # body omitted
end

# good
if x > 10
  # body omitted
end
```

* Prefer `{...}` over `do...end` for single-line blocks. Avoid using `{...}` for multi-line blocks. Always use `do...end` for "control flow" and "method definitions". Avoid `do...end` when chaining.

```ruby
names = ["Jang", "Nara", "Jangnara"]

# good
names.each { |name| puts name }

# bad
names.each do |name|
  puts name
end

# good
names.select { |name| name.start_with?("J") }.map { |name| name.upcase }

# bad
names.select do |name|
  name.start_with?("J")
end.map { |name| name.upcase }
```

* Avoid return where not required.

```ruby
# bad
def some_method(some_arr)
  return some_arr.size
end

# good
def some_method(some_arr)
  some_arr.size
end
```

* Use `_` for unused block parameters.

```ruby
# bad
result = hash.map { |k, v| v + 1 }

# good
result = hash.map { |_, v| v + 1 }
```

* Use `%w( )` to create array of strings

```ruby
# bad
STATES = ['draft', 'open', 'closed']

# good
STATES = %w(draft open closed)
```

* When write **key** of hash, use **symbol** instead of **characters** if possible.

```ruby
# bad
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# good
hash = { one: 1, two: 2, three: 3 }
```

* Use the Ruby 1.9 syntax for hash literals when all the keys are symbols:

```ruby
# bad
user = {
  :login => "nara",
  :name => "Jang Nara"
}

# good
user = {
  login: "nara",
  name: "Jang Nara"
}
```

* Use the 1.9 syntax when calling a method with Hash options arguments or named arguments:

```ruby
# bad
user = User.create(:login => "nara")
link_to("Account", :controller => "users", :action => "show", :id => user)

# good
user = User.create(login: "nara")
link_to("Account", controller: :users, action: :show, id: user)
```

* If you have a hash with mixed key types, use the **legacy hashrocket style** to avoid mixing styles within the same hash:

```ruby
# bad
hsh = {
  user_id: 55,
  "followers-count" => 1000
}

# good
hsh = {
  :user_id => 55,
  "followers-count" => 1000
}
```

* When combine variables into a string, follow below rules:

```ruby
# bad
email_with_name = user.name + ' <' + user.email + '>'

# good
email_with_name = "#{user.name} <#{user.email}>"
```

* Use `"` for strings.

```ruby
# bad
name = 'Jang Nara'

# good
name = "Jang Nara"
```

### Naming

-----

* Name identifiers in English.

```ruby
# bad - identifier using non-ascii characters
заплата = 1_000

# good
salary = 1_000
```


* Use **snake_case** for symbols, methods and variables.

```ruby
# bad
:someSymbol

someVar = 5

def someMethod
  # some code
end

# good
:some_symbol

some_var = 5

def some_method
  # some code
end
```

* Do not separate numbers from letters on symbols, methods and variables.

```ruby
# bad
:some_sym_1

var_10 = 10

def some_method_1
  # some code
end

# good
:some_sym1

var10 = 10

def some_method1
  # some code
end
```


* Use **CamelCase** for classes and modules.

```ruby
# bad
class Someclass
  # some code
end

# good
class SomeClass
  # some code
end
```


* Use **snake_case** for naming directories, e.g. `lib/hello_world/hello_world.rb`.

* Use **snake_case** for naming files, e.g. `hello_world.rb`.

* One class/module per source file. Name the file name as the class/module, but replacing **CamelCase** with **snake_case**.


* Use **SCREAMING_SNAKE_CASE** for other constants.

```ruby
# bad
SomeConst = 5

# good
SOME_CONST = 5
```


* The names of predicate methods (methods that return a boolean value) should end in a question mark `?` (i.e. `Array#empty?`).

* Avoid prefixing predicate methods with the auxiliary verbs such as **is**, **does**, or **can**.

```ruby
# bad
class Person
  def is_tall?
    true
  end

  def can_play_basketball?
    false
  end

  def does_like_candy?
    true
  end
end

# good
class Person
  def tall?
    true
  end

  def basketball_player?
    false
  end

  def likes_candy?
    true
  end
end
```

* **Destroy method** or **dangerous method** should add `!` at the end, such as `Array#flatten! `When define destroy method, un-destroy method like `Array#flatten` should be defined as well.


### Classes

-----

* Avoid using class variables @@ unless it is really necessary

```ruby
class Parent
  @@class_var = 'parent'

  def self.print_class_var
    puts @@class_var
  end
end

class Child < Parent
  @@class_var = 'child'
end

Parent.print_class_var # => output "child"
```

* Use def `self.method`to define singleton methods.

```ruby
class TestClass
  # bad
  def TestClass.some_method
    # body omitted
  end

  # good
  def self.some_other_method
    # body omitted
  end
end
```

* When need to compare between a variable and a value like a number or a constant, write variable on the right side.

```ruby
greeting = "Hello!"

# bad
if greeting == "Hola!"
  ...
end

# good
if "Hola!" == greeting
  ...
end
```

* When define a method or a class macro, use `class << self`.

```ruby
class TestClass
  class << self
    attr_accessor :per_page
    alias_method :nwo, :find_by_name_with_owner

    def some_method
      # body omitted
    end

    def other_method
      # body omitted
    end
  end
end
```

* With a block of **public** methods, no need to declare public before like **private/protected** block below.
* Write **protected** methods before **private** methods.
* When define **protected** methods, **private** methods, indent the methods to be the same as **public** methods
* Add an empty line above **protected** methods, **private** methods, do not add an empty line below.

```ruby
class SomeClass
  def public_method
    # ...
  end

  protected
  def protected_method
    # ...
  end

  private
  def private_method
    # ...
  end
end
```

* Avoid explicit use of `self` as the recipient of internal class or instance messages unless to specify a method shadowed by a variable.

```ruby
class SomeClass
  attr_accessor :message

  def greeting(name)
    message = "Hi #{name}" # local variable in Ruby, not attribute writer
    self.message = message
  end
end
```

### Exceptions

-----

* Do not use exception to control the flow. Exceptions which can be avoided should be avoided.

```ruby
# bad
begin
  n / d
rescue ZeroDivisionError
  puts "Cannot divide by 0!"
end

# good
if d.zero?
  puts "Cannot divide by 0!"
else
  n / d
end
```

* Rescue specific exceptions, not StandardError or its superclasses.

```ruby
# bad
begin
  # an exception occurs here
rescue
  # exception handling
end

# still bad
begin
  # an exception occurs here
rescue Exception
  # exception handling
end

# good
begin
  # an exception occurs here
rescue ActiveRecord::RecordInvalid
  # exception handling
end
```
