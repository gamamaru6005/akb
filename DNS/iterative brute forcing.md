## Iterative Brute Forcing

Source: http://www.room362.com/2014/02/iterative-dns-brute-forcing.html

Save this to brutelist.rb

```ruby
#!/usr/bin/env ruby

#
## Brute code stolen form: https://gist.github.com/petehamilton/4755855
#

def result?(sub)
  puts sub    
  1 == 2
end

def crack_yielding(chars)
  crack_yield(chars){ |p|
      return p if result?(p)
  }
end


def crack_yield(chars)
  chars.each { |c| yield c }

  crack_yield(chars) { |c|
      chars.each do |x|
          yield c + x
      end
  }
end

chars = ('a'..'z').to_a
(0..9).each {|x| chars << x.to_s} 

crack_yielding(chars)
```

then this:

```
ruby brutelist.rb | parallel -j100 dig +noall {}.microsoft.com +answer
```