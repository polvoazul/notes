# Coding & Style Guidelines Python DS & EXP

Para evitar o caos generalizado precisamos de um guia de estilo:

Roubei descaradamente muita coisa do Clean Code.

## 
## Concepts

1. Very important: **[Use good names](https://docs.google.com/document/d/17CHpgAqvSok6abg7L_wIEjYMSU1da0dINqaVhB28_ss/edit?usp=sharing)**
1. Newspaper metaphor for code organization in a file:
    * If you are building a runnable script, use `if __name__ == '__main__': main()` pattern to guarantee that main script is on top.
1. Comments and Docstrings: 
    1. Docstrings are for documenting modules/classes/functions usage. Use them for public functions or very important private functions.
    1. Comments are for indicating Caveats to a fellow programmer. Dont use comments to ‘comment out’ code. Delete unused code (VSV) before merging with master. 
    1. Don't use comments to explain what code is or does, for that use docstrings or better names. Use comments to explain WHY you are doing it in a unconvencional way. 
    1. ``# TODO:``comments are ok for small notes (ex.: ideas for optimizations). For big features use Jira 
1. Reduce scope as much as you can:
    1. Variable declarations inside methods should be as close as possible to their usages. Exception: `import` statements at the top of the file.
    1. Use small functions to avoid having lots of temporary variables
1. [Use Return guards](https://refactoring.guru/replace-nested-conditional-with-guard-clauses) to reduce [nested conditionals](https://medium.com/@scadge/if-statements-design-guard-clauses-might-be-all-you-need-67219a1a981a)
1. Follow Python case conventions: ![case conventions](https://i.imgur.com/snLDjq0.png) This is not Java, stop please! Also, [this](http://www.cs.kent.edu/~jmaletic/papers/ICPC2010-CamelCaseUnderScoreClouds.pdf).
1. Don't return error codes or booleans to indicate success. Throw exceptions instead.
1. Use list/set/dict/gen [comprehensions](https://www.pythonforbeginners.com/basics/list-comprehensions-in-python) instead of 'accumulator + for loops' if possible. If its too complex, extract method. Use for loops only when there's relevant state carried between each iteration.

## Formatting

1. Vertical Formatting:
    1. Avoid very long files (> 150 lines). (Except for tests, configuration, etc…)
    1. Functions should fit in one small splited screen ~ 15 lines
    1. Vertical Space is Valuable *(VSV)*, dont use extra blank lines! You will get used to it and it's good :smile:. If you feel like separating parts of your function's code, [Extract Method](https://refactoring.guru/extract-method).
    1. Methods, Classes should be separated by 1 and only 1 blank line.
    1. Related functions/constants/classes should be vertically near each other. We want to avoid making the reader hop around the code.
    1. Dependent Functions: If one function calls another, they should be vertically close, and the caller should be above the callee, if at all possible.
1. Horizontal Formatting:
    1. 4 spaces indentation. The data hath spoketh.
    2. Double identation for line continuation (8 spaces):
    ```python
    def main():
        very_long_function_call(argument1, argument2,
                argument3)
        function_2()
    ```
    3. Lines < 120 chars
    4. Dont forget single spaces after commas and between `+-*` operators.

## Tests

1. Write tests. Use pytest.
2. Write docker-compose/Dockerfile in your projects so that testing is  easily done inside docker. Create a script called `./bin/test.sh` that runs tests inside docker. A new person joining your project should be able to clone the project and just run `./bin/test.sh`.
3. Test classes should start with 'happy path' test cases. Then proceed to test edge cases, fallbacks and finally errors and validations.
4. Dont obsess! Usually less is more! Having too many tests makes code inflexible as any change breaks many tests. Prefer tests of functionality over implementation.
5. Dont un-obsess! Sometimes more is more! Put more tests in critical paths. Question yourself, if a deploy  breaks this part of the program will it affect end-users? How many? For how long? For what cost?
6. Test files don't need to follow strict formatting guidelines. We can use blank lines to separate tests functions into:
```python
def test_something():
    mocks/inits

    execute

    asserts
```

## Documentation

All projects must have a top level `README.md`

README must explain what the project is about and if there is some special setup to develop in it.

If the project is a reusable library the README needs to be much more detailed. Major Features should be listed. Any difficulties such as the need to ask for permissions or setups should be documented as well as you can. Use hyperlinks.\
Instead of: "you need to install libyaml for this to work"\
Do: "Setup Step 1: install libyaml \<link to libyaml setup>"\
Even better: "Setup Step 1: run `apt-get install libyaml5.2`"

We can have an auto-generated documentation from doc-strings using sphynx. Use gitlab-CI to publish it, and link it from README. See olx_bigdata


## Appendix:
[Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

[Refactoring](https://martinfowler.com/books/refactoring.html)

Zen of python: (just run) `python -c 'import this'`
