# HashDiff

Deep comparison of Ruby Hash objects

## Installation

Add this line to your application's Gemfile:

    gem 'hash_diff'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install hash_diff

## Usage

Easily find the differences between two Ruby hashes.

```ruby
  left = { 
    foo: 'bar',  
    bar: 'foo',  
    nested: { 
      foo: 'bar',  
      bar: { 
        one: 'foo1' 
      } 
    }, 
    num: 1 
  }

  right = { 
    foo: 'bar2', 
    bar: 'foo2', 
    nested: { 
      foo: 'bar2', 
      bar: { 
        two: 'foo2' 
      } 
    }, 
    word: 'monkey' 
  }

  hash_diff = HashDiff::Comparison.new( left, right )
```

Comparion#diff returns the left and right side differences

```ruby
  hash_diff.diff # => { foo: ["bar", "bar2"], bar: ["foo", "foo2"], nested: { foo: ["bar", "bar2"], bar: { one: ["foo1", nil], two: [nil, "foo2"] } }, num:  [1, nil], word: [nil, "monkey"] }
```

Comparison#left_diff returns only the left side differences

```ruby
  hash_diff.left_diff # => { foo: "bar2", bar: "foo2", nested: { foo: "bar2", bar: { one: nil, two: "foo2" } }, num:  nil, word: "monkey" }
```

Comparison#right_diff returns only the right side differences

```ruby
  hash_diff.right_diff # => { foo: "bar", bar: "foo", nested: { foo: "bar", bar: { one: "foo1", two: nil } }, num:  1, word: nil }
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request