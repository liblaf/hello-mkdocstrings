This demo demonstrate the bug when using [mkdocstrings](https://github.com/mkdocstrings/mkdocstrings) with [lazy-loader](https://github.com/scientific-python/lazy-loader).

## Description

[mkdocstrings](https://github.com/mkdocstrings/mkdocstrings) cannot find anything when the documented package is using [lazy-loader](https://github.com/scientific-python/lazy-loader), even when `force_inspection: true`.

`lazy_loader.attach_stub(...)` loads imports from the stub and override module `__getattr__`, `__dir__`, `__all__`. In this example, `foo` is a module that uses [lazy-loader](https://github.com/scientific-python/lazy-loader) to load function `hello(...)` from the stub.
However, [mkdocstrings](https://github.com/mkdocstrings/mkdocstrings) cannot find the function `hello(...)` in the module `foo`, even when `force_inspection: true`.
You can find the documentation workflow [here](https://github.com/liblaf/hello-mkdocstrings/actions/workflows/docs.yaml).

`::: foo` outputs nothing.

`::: foo.hello` produces an error:

```log
ERROR   -  mkdocstrings: foo.hello could not be found
ERROR   -  Error reading page 'README.md':
ERROR   -  Could not collect 'foo.hello'
```

## Outputs of [mkdocstrings](https://github.com/mkdocstrings/mkdocstrings)

```markdown
::: foo
```

::: foo
