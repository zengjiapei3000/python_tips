# Classes and functions

This section describes in depth the API of unittest.

## reference

<https://docs.python.org/3/library/unittest.html?highlight=unittest#classes-and-functions>

## Test cases

(Too many to omit, only list the class name.)

### `class unittest.TestCase(methodName='runTest')`

Instances of the `TestCase` class represent the logical test units in the `unittest` universe. This class is intended to be used as a base class, with specific tests being implemented by concrete subclasses. This class implements the interface needed by the test runner to allow it to drive the tests, and methods that the test code can use to check for and report various kinds of failure.

Each instance of `TestCase` will run a single base method: the method named *methodName*. In most uses of `TestCase`, you will neither change the *methodName* nor reimplement the default *runTest()* method.

*Changed in version 3.2:* TestCase can be instantiated successfully without providing a *methodName*. This makes it easier to experiment with `TestCase` from the interactive interpreter.

`TestCase` instances provide three groups of methods: one group used to run the test, another used by the test implementation to check conditions and report failures, and some inquiry methods allowing information about the test itself to be gathered.

Methods in the first group (**running the test**) are:

`setUp()`
`tearDown()`
`setUpClass()`
`tearDownClass()`
`run(result=None)`
`skipTest(reason)`
`subTest(msg=None, **params)`
`debug()`

The `TestCase` class provides several assert methods to **check for and report failures**. The following table lists the most commonly used methods (see the tables below for more assert methods):

| **Method**                  | **Checks that**      | **New in** |
|-----------------------------|----------------------|------------|
| `assertEqual(a, b)`         |`a == b`              |            |
| `assertNotEqual(a, b)`      |`a != b`              |            |
| `assertTure(x)`             |`bool(x) is True`     |            |
| `assertFalse(x)`            |`bool(x) is False`    |            |
| `assertIs(a, b)`            |`a is b`              | 3.1        |
| `assertIsNot(a, b)`         |`a is not b`          | 3.1        |
| `assertIsNone(x)`           |`x is None`           | 3.1        |
| `assertIsNotNone(x)`        |`x is not None`       | 3.1        |
| `assertIn(a, b)`            |`a in b`              | 3.1        |
| `assertNotIn(a, b)`         |`a not in b`          | 3.1        |
| `assertIsInstance(a, b)`    |`isinstance(a, b)`    | 3.2        |
| `assertNotIsInstance(a. b)` |`not isinstance(a, b)`| 3.2        |

All the assert methods accept a msg argument that, if specified, is used as the error message on failure (see also [`longMessage`](https://docs.python.org/3/library/unittest.html?highlight=unittest#unittest.TestCase.longMessage)). Note that the msg keyword argument can be passed to `assertRaises()`, `assertRaisesRegex()`, `assertWarns()`, `assertWarnsRegex()` only when they are used as a context manager.
`assertEqual(first, second, msg=None)`
`assertNotEqual(first, second, msg=None)`
`assertTrue(expr, msg=None)`
`assertFalse(expr, msg=None)`

---

It is also possible to **check the production of exceptions, warnings, and log messages** using the following methods:

| **Method**                                    | **Checks that**                                                           | **New in** |
|-----------------------------------------------|---------------------------------------------------------------------------|------------|
| assertRaises(exc, fun, *args, **kwds)         | `fun(*args, **kwds)` raises *exc*                                         |            |
| assertRaisesRegex(exc, r, fun, *args, **kwds) | `fun(*args, **kwds)` raises *exc* <br/>and the message matches regex *r*  | 3.1        |
| assertWarns(warn, fun, *args, **kwds)         | `fun(*args, **kwds)` raises *warn*                                        | 3.2        |
| assertWarnsRegex(warn, r, fun, *args, **kwds) | `fun(*args, **kwds)` raises *warn* <br/>and the message matches regex *r* | 3.2        |
| assertLogs(logger, level)                     | The `with` block logs on *logger* with <br/>minimum *level*               | 3.4        |
| assertNoLogs(logger, level)                   | The `with` block does not log on <br/>*logger* with minimum *level*       | 3.10       |

`assertRaises(exception, callable, *args, **kwds)`
`assertRaises(exception, *, msg=None)`

`assertRaisesRegex(exception, regex, callable, *args, **kwds)`
`assertRaisesRegex(exception, regex, *, msg=None)`

`assertWarns(warning, callable, *args, **kwds)`
`assertWarns(warning, *, msg=None)`

`assertWarnsRegex(warning, regex, callable, *args, **kwds)`
`assertWarnsRegex(warning, regex, *, msg=None)`

`assertLogs(logger=None, level=None)`
`assertNoLogs(logger=None, level=None)`

---

There are also other methods used to perform **more specific checks**, such as:

| **Method**                   | **Checks that**                                                                        | **New in** |
|------------------------------|----------------------------------------------------------------------------------------|------------|
| `assertAlmostEqual(a, b)`    | `round(a-b, 7) == 0`                                                                   |            |
| `assertNotAlmostEqual(a, b)` | `round(a-b, 7) != 0`                                                                   |            |
| `assertGreater(a, b)`        | `a > b`                                                                                | 3.1        |
| `assertGreaterEqual(a, b)`   | `a >= b`                                                                               | 3.1        |
| `assertLess(a, b)`           | `a < b`                                                                                | 3.1        |
| `assertLessEqual(a, b)`      | `a <= b`                                                                               | 3.1        |
| `assertRegex(s, r)`          | `r.search(s)`                                                                          | 3.1        |
| `assertNotRegex(s, r)`       | `not r.search(s)`                                                                      | 3.2        |
| `assertCountEqual(a, b)`     | *a* and *b* have the same elements in <br/>the same number, regardless of their order. | 3.2        |

`assertAlmostEqual(first, second, places=7, msg=None, delta=None)`
`assertNotAlmostEqual(first, second, places=7, msg=None, delta=None)`

`assertGreater(first, second, msg=None)`
`assertGreaterEqual(first, second, msg=None)`
`assertLess(first, second, msg=None)`
`assertLessEqual(first, second, msg=None)`

`assertRegex(text, regex, msg=None)`
`assertNotRegex(text, regex, msg=None)`

`assertCountequal(first, second, msg=None)`

`addTypeEqualityFunc(typeobj, function)`

---

The list of **type-specific methods** automatically used by `assertEqual()` are summarized in the following table. Note that it’s usually not necessary to invoke these methods directly.

| **Method**                   | **Used to compare** | **New in** |
|------------------------------|---------------------|------------|
| `assertMultiLineEqual(a, b)` | strings             | 3.1        |
| `assertSequenceEqual(a, b)`  | sequences           | 3.1        |
| `assertListEqual(a, b)`      | lists               | 3.1        |
| `assertTupleEqual(a, b)`     | tuples              | 3.1        |
| `assertSetEqual(a, b)`       | sets or frozensets  | 3.1        |
| `assertDictEqual(a, b)`      | dicts               | 3.1        |

`assertMultiLineequal(first, second, msg=None)`
`assertSequenceEqual(first, second, msg=None)`
`assertListEqual(first, second, msg=None)`
`assertTupleEqual(first, second, msg=None)`
`assertDictEqual(first, second, msg=None)`

---

Finally the `TestCase` provides the following **methods and attributes**:

`fail(msg=None)`

`failureException`

`longMessage`

`maxDiff`

Testing frameworks can use the following methods to collect information on the test:

`countTestCases()`

`defaultTestResult()`

`id()`

`shortDescription()`

`addCleanup(function, /, *args, **kwargs)`

`doCleanups()`

`classmethod addClassCleanup(function, /, *args, **kwargs)`

`classmethod doClassCleanups()`


### `class unittest.IsolatedAsyncioTestCase(methodName='runTest')`


`coroutine asyncSetUp()`

`coroutine asyncTearDown()`

`addAsyncCleanup(function, /, *args, **kwargs)`

`run(result=None)`


### `class unittest.FunctionTestCase(testFunc, setUp=None, tearDown=None, description=None)`

This class provides an API similar to `TestCase` and also accepts coroutines as test functions.

This class implements the portion of the `TestCase` interface which allows the test runner to drive the test, but does not provide the methods which test code can use to check and report errors. This is used to create test cases using legacy test code, allowing it to be integrated into a unittest-based test framework.

### Deprecated aliases

For historical reasons, some of the `TestCase` methods had one or more aliases that are now deprecated. The following table lists the correct names along with their deprecated aliases:

| **Method Name**          | **Deprecated alias**  | **Deprecated alias**   |
|--------------------------|-----------------------|------------------------|
| `assertEqual()`          | failUnlessEqual       | assertEquals           |
| `assertNotEqual()`       | failIfEqual           | assertNotEquals        |
| `assertTrue()`           | failUnless            | assert_                |
| `assertFalse()`          | failIf                |                        |
| `assertRaises()`         | failUnlessRaises      |                        |
| `assertAlmostEqual()`    | failUnlessAlmostEqual | assertAlmostEquals     |
| `assertNotAlmostEqual()` | failIfAlmostEqual     | assertNotAlmostEquals  |
| `assertRegex()`          |                       | assertRegexpMatches    |
| `assertNotRegex()`       |                       | assertNotRegexpMatches |
| `assertRaisesRegex()`    |                       | assertRaisesRegexp     |

*Deprecated since version 3.1:* The fail* aliases listed in the second column have been deprecated.


*Deprecated since version 3.2:* The assert* aliases listed in the third column have been deprecated.

*Deprecated since version 3.2:* assertRegexpMatches and assertRaisesRegexp have been renamed to assertRegex() and assertRaisesRegex().

*Deprecated since version 3.5:* The assertNotRegexpMatches name is deprecated in favor of assertNotRegex().

## Grouping tests

### `class unittest.TestSuite(tests=())`

This class represents an aggregation of individual test cases and test suites. The class presents the interface needed by the test runner to allow it to be run as any other test case. Running a `TestSuite` instance is the same as iterating over the suite, running each test individually.

If *tests* is given, it must be an iterable of individual test cases or other test suites that will be used to build the suite initially. Additional methods are provided to add test cases and suites to the collection later on.

`TestSuite` objects behave much like `TestCase` objects, except they do not actually implement a test. Instead, they are used to aggregate tests into groups of tests that should be run together. Some additional methods are available to add tests to `TestSuite` instances:

`addTest(test)`

`addTests(tests)`

`TestSuite` shares the following methods with `TestCase`:

`run(result)`

`debug()`

`countTestCases()`

`__iter__()`

In the typical usage of a `TestSuite` object, the `run()` method is invoked by a `TestRunner` rather than by the end-user test harness.

## Loading and running tests

### `class unittest.TestLoader`

The `TestLoader` class is used to create test suites from classes and modules. Normally, there is no need to create an instance of this class; the `unittest` module provides an instance that can be shared as `unittest.defaultTestLoader`. Using a subclass or instance, however, allows customization of some configurable properties.

`TestLoader` objects have the following **attributes**:

`errors`

`TestLoader` objects have the following **methods**:

`loadTestsFromTestCase(testCaseClass)`
`loadTestsFromModule(module, pattern=None)`
`loadTestsFromName(name, module=None)`
`loadTestsFromNames(names, module=None)`
`getTestCaseNames(testCaseClass)`
`discover(start_dir, pattern='test*.py', top_level_dir=None)`
``

The following **attributes** of a `TestLoader` can be **configured** either by subclassing or assignment on an instance:

`testMethodPrefix`
`sortTestMethodsUsing`
`suiteClass`
`testNamePatterns`

### `class unittest.TestResult`

This class is used to compile information about which tests have succeeded and which have failed.

A `TestResult` object stores the results of a set of tests. The `TestCase` and `TestSuite` classes ensure that results are properly recorded; test authors do not need to worry about recording the outcome of tests.

Testing frameworks built on top of `unittest` may want access to the `TestResult` object generated by running a set of tests for reporting purposes; a `TestResult` instance is returned by the `TestRunner.run()` method for this purpose.

`TestResult` instances have the following **attributes** that will be of interest when inspecting the results of running a set of tests:

`errors`
`failures`
`skipped`
`expectedFailures`
`unexpectedSuccesses`
`shouldStop`
`testsRun`
`buffer`
`failfast`
`tb_locals`
`wasSuccessful()`
`stop()`

The following methods of the `TestResult` class are used to maintain the internal data structures, and may be extended in subclasses to support additional reporting requirements. This is particularly useful in building tools which support interactive reporting while tests are being run.

`startTest(test)`
`stopTest(test)`
`startTestRun()`
`stopTestRun()`
`addError(test, err)`
`addFailure(test, err)`
`addSuccess(test)`
`addSkip(test, reason)`
`addExpectedFailure(test, err)`
`addUnexpectedSuccess(test)`
`addSubTest(test, subtest, outcome)`

### `class unittest.TextTestResult(stream, descriptions, verbosity)`

A concrete implementation of `TestResult` used by the `TextTestRunner`.

*New in version 3.2:* This class was previously named `_TextTestResult`. The old name still exists as an alias but is deprecated.

`unittest.defaultTestLoader`

Instance of the TestLoader class intended to be shared. If no customization of the TestLoader is needed, this instance can be used instead of repeatedly creating new instances.

### `class unittest.TextTestRunner(stream=None, descriptions=True, verbosity=1, failfast=False, buffer=False, resultclass=None, warnings=None, *, tb_locals=False)`

A basic test runner implementation that outputs results to a stream. If stream is `None`, the default, `sys.stderr` is used as the output stream. This class has a few configurable parameters, but is essentially very simple. Graphical applications which run test suites should provide alternate implementations. Such implementations should accept `**kwargs` as the interface to construct runners changes when features are added to unittest.

By default this runner shows `DeprecationWarning`, `PendingDeprecationWarning`, `ResourceWarning` and `ImportWarning` even if they are ignored by default. Deprecation warnings caused by deprecated unittest methods are also special-cased and, when the warning filters are 'default' or 'always', they will appear only once per-module, in order to avoid too many warning messages. This behavior can be overridden using Python’s -Wd or -Wa options (see [Warning control](https://docs.python.org/3/using/cmdline.html#using-on-warnings)) and leaving warnings to `None`.

*Changed in version 3.2:* Added the `warnings` argument.

*Changed in version 3.2:* The default stream is set to `sys.stderr` at instantiation time rather than import time.

*Changed in version 3.5:* Added the tb_locals parameter.

`_makeResult()`
`run(test)`

`unittest.main(module='__main__', defaultTest=None, argv=None, testRunner=None, testLoader=unittest.defaultTestLoader, exit=True, verbosity=1, failfast=None, catchbreak=None, buffer=None, warnings=None)`

---

### load_tests Protocol

*New in version 3.2.*

Modules or packages can customize how tests are loaded from them during normal test runs or test discovery by implementing a function called `load_tests`.

If a test module defines `load_tests` it will be called by `TestLoader.loadTestsFromModule()` with the following arguments:

`load_tests(loader, standard_tests, pattern)`

where *pattern* is passed straight through from `loadTestsFromModule`. It defaults to `None`.

It should return a `TestSuite`.

*loader* is the instance of `TestLoader` doing the loading. *standard_tests* are the tests that would be loaded by default from the module. It is common for test modules to only want to add or remove tests from the standard set of tests. The third argument is used when loading packages as part of test discovery.

A typical `load_tests` function that loads tests from a specific set of `TestCase` classes may look like:

```python
test_cases = (TestCase1, TestCase2, TestCase3)

def load_tests(loader, tests, pattern):
    suite = TestSuite()
    for test_class in test_cases:
        tests = loader.loadTestsFromTestCase(test_class)
        suite.addTests(tests)
    return suite
```

If discovery is started in a directory containing a package, either from the command line or by calling `TestLoader.discover()`, then the package `__init__.py` will be checked for `load_tests`. If that function does not exist, discovery will recurse into the package as though it were just another directory. Otherwise, discovery of the package’s tests will be left up to `load_tests` which is called with the following arguments:

```python
load_tests(loader, standard_tests, pattern)
```

This should return a `TestSuite` representing all the tests from the package. (`standard_tests` will only contain tests collected from `__init__.py`.)

Because the pattern is passed into `load_tests` the package is free to continue (and potentially modify) test discovery. A ‘do nothing’ `load_tests` function for a test package would look like:

```python
def load_tests(loader, standard_tests, pattern):
    # top level directory cached on loader instance
    this_dir = os.path.dirname(__file__)
    package_tests = loader.discover(start_dir=this_dir, pattern=pattern)
    standard_tests.addTests(package_tests)
    return standard_tests
```

*Changed in version 3.5*: Discovery no longer checks package names for matching *pattern* due to the impossibility of package names matching the default pattern.

