# source_code_encoding

## main

  By default, Python source files are treated as encoded in UTF-8. In that encoding, characters of most languages in the world can be used simultaneously in string literals, identifiers and comments — although the standard library only uses ASCII characters for identifiers, a convention that any portable code should follow. To display all these characters properly, your editor must recognize that the file is UTF-8, and it must use a font that supports all the characters in the file.

  To declare an encoding other than the default one, a special comment line should be added as the first line of the file. The syntax is as follows:

```python
# -*- coding: encoding -*-
```

where encoding is one of the valid [codecs][docs.python.org:codecs] supported by Python.

For example, to declare that Windows-1252 encoding is to be used, the first line of your source code file should be:

```python
# -*- coding: cp1252 -*-
```

One exception to the first line rule is when the source code starts with a [UNIX “shebang” line][docs.python.org:unix shebang]. In this case, the encoding declaration should be added as the second line of the file. For example:

```python
#!/usr/bin/env python3
# -*- coding: cp1252 -*-
```

[docs.python.org:codecs]: https://docs.python.org/3/library/codecs.html#module-codecs
[docs.python.org:unix shebang]: https://docs.python.org/3/tutorial/appendix.html#tut-scripts
