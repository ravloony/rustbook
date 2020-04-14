#Syntax features

##Last expression return


## Pattern matching

The following syntax features are based on pattern matching, where a variable is matched against a type. This feature can also be found in more functional languages like Haskell or Elixir. In Rust, it relies on having an type system with ADTs. As ADTs are formed by combining other types, pattern matching allows the programmer to check a value against several possible types: the components of the ADT in question.


### Match

`match` is Rust's syntax for full pattern matching. For each possible type in the ADT, one branch is executed if the value being matched is of that type.

Let's see an example:

```rust
    let matches = app.get_matches();
    match (matches.value_of(FILE_KEY)) {
        Some(file) => {
            Ok(file.name)
        }
        _ => Ok(''),
    }
```

As you can observe, the match takes the value, and compares its type to each branch, moving execution into the only branch that matches. Because this is an ADT, there can only be one. However, in the second and last case, we can see that there is a wildcard `_` which corresponds to "all remaining cases" which is convenient when you only want to actually do something about one or two of the cases, and / or execute the same action for the others.

The match also extracts the value from the matched type, allowing the programmer to use it in the statement.

In the event that you want to execute some action, but not necessarily return something when a value is of a certain type, Rust offers the `if let` construct.

### `if let`

This construct reads a bit strangely, but is very useful. Rust's syntax for partial pattern matching, it is basically a block scope that is entered if the condition matches a certain type. Whatever is in the block is then executed, but the syntax of the if condition allows the programmer to bind a variable (hence the `let`).

In the following example you can see that the `start_line` variable is bound for the scope of the block if the `maybe_line` variable is of the type Option::Some. To put it another way, the `let` is extracting the value held by the `Some` into the `start_line` variable, thereby making it available for the block.

```rust
if let Some(start_line) = maybe_line {
  chaser.line = Line(start_line.parse()?);
}
```

### `while let`

In a similar fashion, `while let` allows the programmer to match a value against a type. So long as the match is valid, the while condition evaluates to true an the content of the matched type is extracted to a variable which is made available within the while block.

### Destructuring

As you have no doubt noticed, the above constructs allow the programmer to extract the value in a type to a variable. This process is known as "destructuring" and also exists in a lot of function languages with strong type systems. You may recognize destructuring from languages like Javascript, where it is possible to take part of an object or an array into one or more variables. In rust, destructuring is part of pattern matching as it involves a type level part and a variable level part.
