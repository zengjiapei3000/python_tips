# Re-using old test code(not recommend)

## not recommend using `FunctionTestCase`

Some users will find that they have existing test code that they would like to run from `unittest`, without converting every old test function to a `TestCase` subclass.

For this reason, `unittest` provides a `FunctionTestCase` class. This subclass of `TestCase` can be used to wrap an existing test function. Set-up and tear-down functions can also be provided.

Given the following test function:

```python
def testSomething():
    something = makeSomething()
    assert something.name is not None
    # ...
```

one can create an equivalent test case instance as follows, with optional set-up and tear-down methods:

```python
testcase = unittest.FunctionTestCase(testSomething,
                                     setUp=makeSomethingDB
                                     tearDown=deleteSomethingDB)
```

> **Note:** Even though `FunctionTestCase` can be used to quickly convert an existing test base over to a unittest-based system, this approach is not recommended. Taking the time to set up proper `TestCase` subclasses will make future test refactorings infinitely easier.

In some cases, the existing tests may have been written using the `doctest` module. If so, `doctest` provides a `DocTestSuite` class that can automatically build `unittest.TestSuite` instances from the existing doctest-based tests.