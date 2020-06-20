# Ruby

## Methods

`Comparable#clamp(min, max)`
    - [Ruby-doc](https://ruby-doc.org/core-2.6.3/Comparable.html#method-i-clamp)
    - Returns `min` if `obj <=> min` is less than zero, `max` if `obj <=> max` is greater than zero and `obj` otherwise.

## Regexes

The patterns `^` and `$` match the beginning and end of a line, respectively.

Similarly, the sequence `\A` matches the beginning of a string, and `\z` and `\Z` match the end of a string. (Actually, `\Z` matches the end of a string unless the string ends with `\n`, in which case it matches just before the `\n`.)

```ruby
str = "this is\nthe time"
show_regexp(str, /^the/) # => this is\n->the<- time
show_regexp(str, /is$/) # => this ->is<-\nthe time
show_regexp(str, / \A this/) # => ->this<- is\nthe time
show_regexp(str, / \A the/) # => no match
```

the patterns `\b` and `\B` match word boundaries and nonword boundaries, respectively. Word characters are ASCII letters, numbers, and underscores:

```ruby
show_regexp( "this is\nthe time" , / \b is/) # => this ->is<-\nthe time
show_regexp( "this is\nthe time" , / \B is/) # => th->is<- is\nthe time
```

## Bundler

tags = #bundler #tips 

You can list all outdated gems of a project using

```shell
bundle outdated
```

## IRB

- [Documentation](https://docs.ruby-lang.org/en/2.7.0/IRB.html)
- There are a few variables in every Irb session that can come in handy:
  - `_` : The value command executed, as a local variable
  - `__` : The history of evaluated commands
  - `__[line_no]` : Returns the evaluation value at the given line number, line_no. If line_no is a negative, the return value line_no many lines before the most recent return value.

## Rake

### Parameters

Pass parameters to a rake task

```ruby
task :my_task, [:arg1, :arg2] do |t, args|
  arg1, arg2 = args.values_at(:arg1, :arg2)
end
```

```shell
rake my_task[arg1,arg2]
```

### gotchas
With some shells (eg zsh), brackets need to be escaped, ie:

```shell
rake my_task\[arg1,arg2\]
```

## Rails

### Todos

Rails has a built-in rake task for showing todos in code

```shell
bundle exec rake notes:todo
```

It works for other forms of annotations too

```shell
bundle exec rake notes:todo ANNOTATION=FIXME
```

### Console

`my_object.method(:my_method_name).source_location` : full path of a method's file definition

`my_object.method(:my_method_name).source.display` : output a method's source code directly to the console

### Solargraph rails config

Les libs rails utilisent #rdoc et #solargraph se base sur #yard, cette tache créé une version #yard des docs et la cache (à réexécuter en cas de mise à jour)

`solargraph bundle`

2. Ajouter la version la plus récente de [ce fichier](https://gist.github.com/castwide/28b349566a223dfb439a337aea29713e) dans config/solargraph_definitions.rb (l'important est que ça soit un fichier Ruby dans le projet)

   - Contient une liste de directives #yard pour améliorer la comprehension qu'a #solargraph des classes de #rails
		
      - la directive `@!parse` expose à #solargraph des méthodes inaccessible par analyse statique parce qu'incluses au runtime

		```ruby
		    @!parse
		      class ActionController::Base
		        include ActionController::MimeResponds
		        ...
		      end
		```

      - la directive `@!override` permet d'injecter sa propre doc #yard à des méthodes externes, ce qui permet ici d'inférer les types retournés correctement

		```ruby
		    @!override ActiveRecord::FinderMethods#find
		      @overload find(id)
		        @param id [Integer]
		        @return [self]
		      @overload find(list)
		        @param list [Array]
		        @return [Array<self>]
		      @overload find(*args)
		        @return [Array<self>]
		        @return [self, Array<self>]
		```

