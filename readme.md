# Shopify Liquid Functions

I hate repeating myself in shopify liquid, so to abide by the [Don't repeat yourself](http://en.wikipedia.org/wiki/Don't_repeat_yourself) (DRY) principle of software development, I created a spec for creating reusable functions in Shopify Liquid.

I've been using a technique for a little while now to create functions in shopify. With it's own sort of spec. I've been making them more and more, this repo will be dedicated to housing them.

## Example Function

Here's an example of a function that will check if a string (`string`) contains another string (`query`).

This would be in a file called `function.string_contains.liquid`.

```
{% assign return = false %}
{% if query %}
{% if string %}
  {% assign replaced = string | remove: query %}  
  {% if string != replaced %}
    {% assign return = true %}
  {% endif %}
{% endif %}
{% endif %}
```

Things to note:

* `return` is the return value of the function
* each argument started with `pass_` (depricated?)
* `return` is assigned to false at the beginning of each funciton file
* the value of `return` changes somewhere in the funciton
* there is no support for returning multiple variables
* wrap the whole function in `if` statment per outside argument.
* up for debate should set any `assign`ed variables to `null` at the end of a function `{% assign replaced = null %`?

## Example Usage

```
{% assign query = '5"x7"' %}
{% assign string = 'hello world 5"x7"' %}
{% include "function.string_contains" %}
{% assign contains_query = return %}
```

Things to note:

* `assign` the arguments
* `include` the function file
* re-`assign` the return value