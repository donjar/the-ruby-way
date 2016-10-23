# Programming, the Ruby Way
(Many parts stolen from https://github.com/alexch/ruby_notes/blob/master/ruby-intro.md)

Ruby is a unique language! This document helps you to better transition to the ways of Ruby.

## Philosophy

Matz (Yukihiro Matsumoto), Ruby creator, says:
- I believe people want to express themselves when they program. They don't want to fight with the language.
- Programming languages must feel natural to programmers.
- I tried to make people enjoy programming and concentrate on the fun and creative part of programming when they use Ruby.
- For me the purpose of life is partly to have joy. Programmers often feel joy when they can concentrate on the creative side of programming, So Ruby is designed to make programmers happy.

Ruby favors readability a lot. Keep this in mind!

## Installing Ruby

This series of shell commands should get you up and running:
```bash
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.3.1
rvm use 2.3.1 --default
gem install bundler rails
```
Afterwards try opening `irb` in your terminal. You should see a prompt like: `2.3.1 :001 >` If it's not working, just use https://repl.it for this moment.

## Playing with Ruby
`irb` stands for Interactive RuBy. Try these on your irb shell, one line at a time:
```ruby
3 + 5 - 2
puts "Hello World!"
x = 2 ** 10000
x.even?
"Hi!".upcase
test = "NUSSU CommIT"
test.downcase!
puts test
'Ang,Desmond,Gilbert,Hangzhi,Indra'.split(',').count
```
From these simple experiments, some points can be made:
- `puts` prints to output
- `**` is the exponential operator. There is pretty much no limit to how big numbers can be in Ruby - try `3 ** 100000`!

Here are other fun Ruby stuff!

## Everything is an object
This means that everything in Ruby has instances and methods.
```ruby
> 2.class
=> Fixnum
> (2 ** 1000).class
=> Bignum
> 'asdf'.class
=> String
```

## Also, Ruby's standard library is HUGE
Check https://ruby-doc.org/core-2.3.1/String.html. These are some things that you can do with Ruby:
```ruby
> 'hello'.delete('l')
=> 'heo'
> 'Desmond'.end_with?('mond')
=> true
> 'Hello World'.upcase
=> 'HELLO WORLD'
> 'Abcd'[2]
=> 'c'
```
In Ruby, methods are named by a convention:
- Methods ending with a question mark (?) always returns true or false.
- Methods ending with a bang (!) mutates the variable. For example:
```ruby
> x = 'try'
=> 'try'
> x.upcase
=> 'TRY'
> x
=> 'try'
> x.upcase!
=> 'TRY'
> x
=> 'try'
```

## Some basic stuff
You can copy and paste these stuff to irb... You can also save it as a file (for example, `test.rb`) and run `ruby test.rb`.
```ruby
def div_by_7(n)
  if (n % 7 == 0)
    return 'divisible by 7'
  else
    return 'not divisible by 7'
  end
end
```
Functions start with `def` and if statements start with `if`. Pretty much everything ends with `end`.

But of course - parantheses are optional. What might be unexpected though is that `return` is also optional!
```ruby
def div_by_7 n
  if n % 7 == 0
    'divisible by 7'
  else
    'not divisible by 7'
  end
end
```
If Ruby does not find a return statement, it will just return the result of the last statement evaluated.

How about for or while loops? Avoid them - they are _not_ the Ruby way!

## Instead, we have these cool things called blocks
Why write something like this?
```c
for (int i = 0; i < 5; i++) {
    printf(i * i);
}
```
when you can write sentences!
```ruby
5.times { |i| puts i * i }
```
"Do this 5 times: for every `i`, print out `i * i`."

The braces create what we call a Ruby block, which is in many ways similar to a function: it takes arguments and do something with them. In this particular case, `times` is a method of 5, a Fixnum, that takes a block. The block takes one argument and does something with it. The argument will be automatically incremented.

Another example is `select` on arrays:
```ruby
> [7, 2, 4, 1, 10, 9, 5].select { |num| return num.even? }
=> [2, 4, 10]
```
This is similar to:
```c
function get_even(int arr[], int size) {
    int[] result;
    int position = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] % 2 == 0) {
            result[position] = arr[i];
            position++;
        }
    }
    return result;
}
```
Look how nice Ruby is!

Another syntax you can use for blocks is `do...end`:
```ruby
[7, 2, 4, 1, 10, 9, 5].select do |num|
  num.even?
end
```
And yes, of course, you can get rid of the `return` statement.

## Some final stuff
### String interpolation
```ruby
> "I have #{3 + 5} apples in total!"
=> "I have 8 apples in total!"
> "The answer is #{2.even?}"
=> "The answer is true."
```
Note that for string interpolation you need double quotes.
### Comments
They start with `#`, except if it is inside a string.
```ruby
[2, 10, -3].map { |i| i * 2 } # multiplies all numbers by 2
```
### Ranges
```ruby
> (3..5).each { |num| puts num }
3
4
5
=> 3..5
> (3...5).each { |num| puts num }
3
4
=> 3...5
```
A range is just an array of consecutive numbers from a start number to end number.
### Symbols
```ruby
> :test
=> :test
> :test.to_s # converts to string
=> "test"
```
For now you can just assume that symbols are special strings.
### Hashes
Some languages call them "dictionaries". Example:
```ruby
{ 'Indra' => 'Technical', 'Desmond' => 'Marketing', 'Glenys' => 'Presidential' }
```
This is a hash with the newer syntax:
```ruby
{ username: 'herbert', fullname: 'Herbert Ilhan Tanujaya', cell: 'Technical' }
```
This is equivalent to:
```ruby
{ :username => 'herbert', :fullname => 'Herbert Ilhan Tanujaya', :cell => 'Technical' }
```
## Time for some practice!
https://github.com/vikingeducation/learn_ruby
