---
title: Code styling
date: 20200626
author: Lyz
---

# [Commit message guidelines](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)

I'm following the Angular commit convention that is backed up by
[python-semantic-release](https://python-semantic-release.readthedocs.io/en/latest/commit-log-parsing.html),
with the idea of implementing automatic [semantic
versioning](https://semver.org/) sometime in the future.

Each commit message consists of a header, a body and a footer. The header has
a defined format that includes a type, a scope and a subject:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

The *header* is mandatory and the *scope* of the header is optional.

Any line of the commit message cannot be longer 100 characters.

The *footer* should contain a [closing reference to an issue](https://help.github.com/articles/closing-issues-via-commit-messages/) if any.

Samples: (even more samples)

```
docs(changelog): update changelog to beta.5

fix(release): need to depend on latest rxjs and zone.js

The version in our package.json gets copied to the one we publish, and users need the latest of these.

docs(router): fix typo 'containa' to 'contains' (#36764)

Closes #36763

PR Close #36764
```

## Revert

If the commit reverts a previous commit, it should begin with `revert:` , followed
by the header of the reverted commit. In the body it should say: `This reverts
commit <hash>.`, where the hash is the SHA of the commit to revert.

## Type

Must be one of the following:

* `build`: Changes that affect the build system or external dependencies.
* `ci`: Changes to our CI configuration files and scripts.
* `docs`: Documentation changes.
* `feat`: A new feature.
* `fix`: A bug fix.
* `perf`: A code change that improves performance.
* `refactor`: A code change that neither fixes a bug nor adds a feature.
* `style`: Changes that do not affect the meaning of the code (white-space,
    formatting, missing semi-colons, etc).
* `test`: Adding missing tests or correcting existing tests.

## Subject

The subject contains a succinct description of the change:

* Use the imperative, present tense: "change" not "changed" nor "changes".
* Don't capitalize the first letter.
* No dot (.) at the end.

## Body

Same as in the subject, use the imperative, present tense: "change" not
"changed" nor "changes". The body should include the motivation for the change
and contrast this with previous behavior.

## Footer

The footer should contain any information about Breaking Changes and is also the
place to reference issues that this commit Closes.

Breaking Changes should start with the word `BREAKING CHANGE:` with a space or
two newlines. The rest of the commit message is then used for this.

## Pre-commit

To ensure that your project follows these guidelines, add the following
to your [pre-commit configuration](ci.md):

!!! note "File: .pre-commit-config.yaml"
    ```yaml
    - repo: https://github.com/commitizen-tools/commitizen
      rev: master
      hooks:
        - id: commitizen
          stages: [commit-msg]
    ```

To make your life easier, change your workflow to use
[commitizen](https://commitizen-tools.github.io/commitizen/).

In Vim, if you're using Vim fugitive [change the
configuration](https://vi.stackexchange.com/questions/3670/how-to-enter-insert-mode-when-entering-neovim-terminal-pane)
to:

```vimrc
nnoremap <leader>gc :terminal cz c<CR>
nnoremap <leader>gr :terminal cz c --retry<CR>

" Open terminal mode in insert mode
if has('nvim')
    autocmd TermOpen term://* startinsert
endif
autocmd BufLeave term://* stopinsert
```

If some pre-commit hook fails, make the changes and then use `<leader>gr` to
repeat the same commit message.

To automatically generate the changelog use `cz bump --changelog --no-verify`.
The `--no-verify` part is required [if you use pre-commit
hooks](https://github.com/commitizen-tools/commitizen/issues/164).

Whenever you want to release `1.0.0`, use `cz bump --changelog --no-verify
--increment MAJOR`.

# [Black code style](https://black.readthedocs.io)

[Black](black.md) is a style guide enforcement tool.

# [Flake8](https://flake8.pycqa.org/)

[Flake8](flake8.md) is another style guide enforcement tool.

# f-strings

[f-strings](https://realpython.com/python-f-strings/), also known as *formatted
string literals*, are strings that have an `f` at the beginning and curly braces
containing expressions that will be replaced with their values.

Introduced in Python 3.6, they are more readable, concise, and less prone
to error than other ways of formatting, as well as faster.

```python
>>> name = "Eric"
>>> age = 74
>>> f"Hello, {name}. You are {age}."
'Hello, Eric. You are 74.'
```

## Arbitrary expressions

Because f-strings are evaluated at runtime, you can put any valid Python
expressions in them. For example, calling a function or method from within.

```python
>>> f"{name.lower()} is funny."
'eric idle is funny.'
```

## Multiline f-strings

```python
>>> name = "Eric"
>>> profession = "comedian"
>>> affiliation = "Monty Python"
>>> message = (
...     f"Hi {name}. "
...     f"You are a {profession}. "
...     f"You were in {affiliation}."
... )
>>> message
'Hi Eric. You are a comedian. You were in Monty Python.'
```

# Reference

## Type hints

* [Bernat gabor article on the state of type hints in python](https://www.bernat.tech/the-state-of-type-hints-in-python/)
* [Real python article on type checking](https://realpython.com/python-type-checking/#type-systems)