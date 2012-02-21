PHP Parser
==========

This is a PHP 5.4 (and older) parser written in PHP. It's purpose is to simplify static code analysis and
manipulation.

Documentation can be found in the [`doc/`][1] directory.

***Note: This project is experimental, so the API is subject to change.***

In a Nutshell
-------------

Basically, the parser does nothing more than turn some PHP code into an abstract syntax tree. ("nothing
more" is kind of sarcastic here as PHP has a ... uhm, let's just say "not nice" ... grammar, which makes
parsing PHP very hard.)

For example, if you stick this code in the parser:

```php
<?php
echo 'Hi', 'World';
hello\world('foo', 'bar' . 'baz');
```

You'll get a syntax tree looking roughly like this:

```
array(
    0: Stmt_Echo(
        exprs: array(
            0: Scalar_String(
                value: Hi
            )
            1: Scalar_String(
                value: World
            )
        )
    )
    1: Expr_FuncCall(
        name: Name(
            parts: array(
                0: hello
                1: world
            )
        )
        args: array(
            0: Arg(
                value: Scalar_String(
                    value: foo
                )
                byRef: false
            )
            1: Arg(
                value: Expr_Concat(
                    left: Scalar_String(
                        value: bar
                    )
                    right: Scalar_String(
                        value: baz
                    )
                )
                byRef: false
            )
        )
    )
)
```

If you then stick that result into the pretty printer you'll get back PHP code again :)

This is useful for a variety of situations where you want to deal with code programmatically, like static
analysis, code preprocessing and code generation.

So, that's it, in a nutshell. You can find everything else in the [docs][1].

 [1]: https://github.com/nikic/PHP-Parser/tree/master/doc