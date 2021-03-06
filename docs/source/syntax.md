# Syntax Guide


```{note}
This documentation utilized the [Markedly Structured Text (MyST)](https://myst-parser.readthedocs.io/en/latest/index.html) syntax.
```

## Exercise Directive

An exercise directive can be included using the `exercise` pattern. The directive is enumerated by default and can take in an optional title argument. The following options are also supported:

* `label` : text

    A unique identifier for your exercise that you can use to reference it with `{ref}` and `{numref}`. Cannot contain spaces or special characters.
* `class` : text

    Value of the exercise’s class attribute which can be used to add custom CSS or JavaScript.
* `nonumber` : flag (empty)

    Turns off exercise auto numbering.

**Example**

```{exercise}
:label: my-exercise

Recall that $n!$ is read as "$n$ factorial" and defined as
$n! = n \times (n - 1) \times \cdots \times 2 \times 1$.

There are functions to compute this in various modules, but let's
write our own version as an exercise.

In particular, write a function `factorial` such that `factorial(n)` returns $n!$
for any positive integer $n$.
```

**MyST Syntax**

``````md
```{exercise}
:label: my-exercise

Recall that $n!$ is read as "$n$ factorial" and defined as
$n! = n \times (n - 1) \times \cdots \times 2 \times 1$.

There are functions to compute this in various modules, but let's
write our own version as an exercise.

In particular, write a function `factorial` such that `factorial(n)` returns $n!$
for any positive integer $n$.
```
``````

_Source:_ [QuantEcon](https://python-programming.quantecon.org/functions.html#Exercise-1)

### Referencing Exercises

You can refer to an exercise using the `{ref}` role like ```{ref}`my-exercise` ```, which will display the title of the exercise directive. In the event that directive does not have a title, the title will default to "Exercise" like so: {ref}`my-exercise`.

Enumerable directives can also be referenced through the `numref` role like ```{numref}`my-exercise` ```, which will display the number of the exercise directive. Referencing the above directive will display {numref}`my-exercise`. Furthermore, `numref` can take in three additional placeholders: _%s_ and _{number}_ which get replaced by the exercise number and _name_ by the exercise title.[^note]



<!-- You can refer to an exercise using the `{ref}` role like: ```{ref}`my-exercise` ```, which will replace the reference with the exercise number like so: {ref}`my-exercise`. When an explicit text is provided, this caption will serve as the title of the reference. -->

[^note]: If the exercise directive does not have a title, an `invalid numfig format` warning will be displayed during build if the user tries to use the _{name}_ placeholder.


## Solution Directive

A solution directive can be included using the `solution` pattern. It takes in the label of the directive it wants to link to as a required argument. Unlike the `exercise` directive, the solution directive is unenumerable. The following options are also supported:

* `label` : text

    A unique identifier for your solution that you can use to reference it with `{ref}`. Cannot contain spaces or special characters.
* `class` : text

    Value of the solution’s class attribute which can be used to add custom CSS or JavaScript.

```{note}
The title of the solution directive links directly to the referred directive.
```

**Example**

````{solution} my-exercise
:label: my-solution

Here's one solution.

```{code-block} python
def factorial(n):
    k = 1
    for i in range(n):
        k = k * (i + 1)
    return k

factorial(4)
```
````

**MyST Syntax**

``````md
````{solution} my-exercise
:label: my-solution

Here's one solution.

```{code-block} python
def factorial(n):
    k = 1
    for i in range(n):
        k = k * (i + 1)
    return k

factorial(4)
```
````
``````

_Source:_ [QuantEcon](https://python-programming.quantecon.org/functions.html#Exercise-1)


### Referencing Solutions

You can refer to a solution using the `{ref}` role like: ```{ref}`my-solution` ``` the output of which depends on the attributes of the linked directive. If the linked directive is enumerable, the role will replace the solution reference with the linked directive type and its appropriate number like so: {ref}`my-solution`.

In the event that the directive being referenced is unenumerable, the reference will display its title: {ref}`nfactorial-solution`. Click the toggle to see the supporting directives.

````{toggle}

```{exercise} $n!$ Factorial
:label: nfactorial
:nonumber:

Write a function `factorial` such that `factorial(int n)` returns $n!$
for any positive integer $n$.
```

```{solution} nfactorial
:label: nfactorial-solution

Here's a solution in Java.

```{code-block} java
static int factorial(int n){
    if (n == 0)
        return 1;
    else {
        return(n * factorial(n-1));
    }
}
```
````


If the title of the linked directive being reference does not exist, it will default to {ref}`nfactorial-notitle-solution`. Click the toggle to see the supporting directives.

````{toggle}

```{exercise}
:label: nfactorial-notitle
:nonumber:

Write a function `factorial` such that `factorial(int n)` returns $n!$
for any positive integer $n$.
```

```{solution} nfactorial-notitle
:label: nfactorial-notitle-solution

Here's a solution in Java.

```{code-block} java
static int factorial(int n){
    if (n == 0)
        return 1;
    else {
        return(n * factorial(n-1));
    }
}
```
````


## How to Hide Directives

Directives can be hidden using the `dropdown` class which is available through [Sphinx Book Theme](https://sphinx-book-theme.readthedocs.io/en/latest/index.html). For Sphinx projects, add `"sphinx_book_theme"` to your `html_theme` in the `conf.py` to activate the theme in your Sphinx configuration

```md
...
html_theme = "sphinx_book_theme"
...
```

Jupyter Book's default theme is Sphinx Book Theme; therefore, Jupyter Book projects can utilize `dropdown` without having to activate the theme in your Sphinx configuration.


To hide the directive, simply add `:class: dropdown` as a directive option.

**Example**

```{exercise}
:class: dropdown

Recall that $n!$ is read as "$n$ factorial" and defined as
$n! = n \times (n - 1) \times \cdots \times 2 \times 1$.

There are functions to compute this in various modules, but let's
write our own version as an exercise.

In particular, write a function `factorial` such that `factorial(n)` returns $n!$
for any positive integer $n$.
```

**MyST Syntax**:

````
```{exercise}
:class: dropdown

Recall that $n!$ is read as "$n$ factorial" and defined as
$n! = n \times (n - 1) \times \cdots \times 2 \times 1$.

There are functions to compute this in various modules, but let's
write our own version as an exercise.

In particular, write a function `factorial` such that `factorial(n)` returns $n!$
for any positive integer $n$.
```
````
