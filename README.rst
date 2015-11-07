PyExecJS
========

Run JavaScript code from Python.

PyExecJS is a porting of ExecJS from Ruby. PyExecJS **automatically**
picks the best runtime available to evaluate your JavaScript program.

A short example:

::

    >>> import execjs
    >>> execjs.eval("'red yellow blue'.split(' ')")
    ['red', 'yellow', 'blue']
    >>> ctx = execjs.compile("""
    ...     function add(x, y) {
    ...         return x + y;
    ...     }
    ... """)
    >>> ctx.call("add", 1, 2)
    3

The pros of PyExecJS is that you do not need take care of JavaScript
environment. Especially, it works in Windows environment without
installing extra libraries.

One of cons of PyExecJS is performance. PyExecJS communicate JavaScript
runtime by text and it is slow. The other cons is that it does not fully
support runtime specific features.

`PyV8 <https://code.google.com/p/pyv8/>`__ might be better choice for
some use case.

Installation
============

::

    $ pip install PyExecJS

or

::

    $ easy_install PyExecJS

Details
=======

PyExecJS supports these runtimes:

-  `PyV8 <http://code.google.com/p/pyv8/>`__ - A python wrapper for
   Google V8 engine,
-  `Node.js <http://nodejs.org/>`__
-  Apple JavaScriptCore - Included with Mac OS X
-  `Mozilla SpiderMonkey <http://www.mozilla.org/js/spidermonkey/>`__
-  `Microsoft Windows Script
   Host <http://msdn.microsoft.com/en-us/library/9bbdkx3k.aspx>`__
   (JScript)
-  `SlimerJS <http://slimerjs.org/>`__
-  `PhantomJS <http://phantomjs.org/>`__

If ``EXECJS_RUNTIME`` environment variable is specified, PyExecJS pick
the JavaScript runtime as a default:

::

    >>> #execjs.get().name # this value is depends on your environment.
    >>> os.environ["EXECJS_RUNTIME"] = "Node"
    >>> execjs.get().name
    'Node.js (V8)'

You can choose JavaScript runtime by ``execjs.get()``:

::

    >>> default = execjs.get() # the automatically picked runtime
    >>> default.eval("1 + 2")
    3
    >>> jscript = execjs.get("JScript")
    >>> jscript.eval("1 + 2")
    3
    >>> node = execjs.get("Node")
    >>> node.eval("1 + 2")
    3

License
=======

Copyright (c) 2012 Omoto Kenji. Copyright (c) 2011 Sam Stephenson and
Josh Peek.

Released under the MIT license. See ``LICENSE`` for details.

Changes
=======

1.1.0
-----

-  Supported Python 3.4
-  Supported SlimerJS as runtime
-  Supported PhantomJS as runtime
-  Fixed JScript runtime on Windows 8

1.0.5
-----

-  Supported Python 3.3
-  Fixed file handle leaking
-  Fixed issue with passenger-nginx-4.0

1.0.4
-----

-  Removed "import execjs" (it prevent execution of setup.py by Python
   2.6)

1.0.3
-----

-  Javascript sources were embeded in **init**.py. 'which' command were
   reimplemented by pure python.

1.0.2
-----

-  Python 2.6.x was supported.

1.0.1
-----

-  Forgotten shell=True was added to Popen.

1.0.0
-----

-  First release.
