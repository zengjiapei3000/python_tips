# Command-Line Interface/Test Discovery

unittest 模块的命令行接口比较简单.

1. 基础:

```bash
python -m unittest test_module1 test_module2          # module
python -m unittest test_module.TestClass              # class
python -m unittest test_module.TestClass.test_method  # method
python -m unittest tests/test_something.py            # module was specified by file path
```

1. 可以通过传入 -v 标志来运行更详细（更详细）的测试:

```bash
python -m unittest -v test_module
```

1. 当不带参数执行时，测试发现开始:

```bash
python -m unittest
```

## Command-line options

unittest支持以下命令行选项:

### `-b, --buffer`

标准输出和标准错误流被缓冲，在测试运行期间。通过测试期间的输出将被丢弃。输出在测试失败或错误时正常回显，并添加到失败消息中。

### `-c, --catch`

Control-C在测试运行期间等待当前测试结束，然后报告到目前为止的所有结果。再一秒钟 Control-C 引发一般的 `KeyboardInterrupt` 异常。

有关提供此功能的功能，请参阅 [信号处理](https://docs.python.org/3/library/unittest.html?highlight=unittest#signal-handling)。

### `-f, --failfast`

在第一个错误或失败时停止测试运​​行。

### `-k`

仅运行与 模式或子字符串 匹配的测试方法和类。此选项可以多次使用，在这种情况下，所有匹配任何给定模式的测试用例都包括在内。

包含通配符 (*) 的模式使用 `fnmatch.fnmatchcase()` 与测试名称匹配; 否则使用简单的区分大小写的子字符串匹配。

模式与测试加载器导入的完全限定测试方法名称相匹配。

For example, `-k foo` matches `foo_tests.SomeTest.test_something`, `bar_tests.SomeTest.test_foo`, but not `bar_tests.FooTest.test_something`.

### `--locals`

在回溯中显示局部变量。

New in version 3.2: The command-line options `-b`, `-c` and `-f` were added.

New in version 3.5: The command-line option `--locals`.

New in version 3.7: The command-line option `-k`.

The command line can also be used for test discovery, for running all of the tests in a project or just a subset.

---

## Test Discovery

3.2 版中的新功能。

Unittest supports simple test discovery. In order to be compatible with test discovery, all of the test files must be modules or packages (including namespace packages) importable from the top-level directory of the project (this means that their filenames must be valid identifiers).

Test discovery is implemented in [`TestLoader.discover()`](https://docs.python.org/3/library/unittest.html?highlight=unittest#unittest.TestLoader.discover), but can also be used from the command line. The basic command-line usage is:

```bash
cd project_directory
python -m unittest discover
```

> **Note**: As a shortcut, `python -m unittest` is the equivalent of `python -m unittest discover`. If you want to pass arguments to test discovery the `discover` sub-command must be used explicitly.

The `discover` sub-command has the following options:

### `-v, --verbose`

Verbose output

### `-s, --start-directory <directory>`

Directory to start discovery (`.` default)

### `-p, --pattern <pattern>`

Pattern to match test files (`test*.py` default)

### `-t, --top-level-directory <directory>`

Top level directory of project (defaults to start directory)

The `-s`, `-p`, and `-t` options can be passed in as positional arguments in that order. The following two command lines are equivalent:

```bash
python -m unittest discover -s project_directory -p "*_test.py"
python -m unittest discover project_directory "*_test.py"
```

As well as being a path it is possible to pass a package name, for example `myproject.subpackage.test`, as the start directory. The package name you supply will then be imported and its location on the filesystem will be used as the start directory.

**Caution:** Test discovery loads tests by importing them. Once test discovery has found all the test files from the start directory you specify it turns the paths into package names to import. For example `foo/bar/baz.py` will be imported as `foo.bar.baz`.

If you have a package installed globally and attempt test discovery on a different copy of the package then the import could happen from the wrong place. If this happens test discovery will warn you and exit.

If you supply the start directory as a package name rather than a path to a directory then discover assumes that whichever location it imports from is the location you intended, so you will not get the warning.

Test modules and packages can customize test loading and discovery by through the [load_tests protocol](https://docs.python.org/3/library/unittest.html?highlight=unittest#load-tests-protocol).

Changed in version 3.4: Test discovery supports [namespace packages](https://docs.python.org/3/glossary.html#term-namespace-package) for the start directory. Note that you need to specify the top level directory too (e.g. `python -m unittest discover -s root/namespace -t root`).