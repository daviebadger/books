============
 TOML 1.0.0
============
-----------------------------------
 Minimal Configuration File Format
-----------------------------------

:Author: `Davie Badger`_
:Contact: davie.badger@gmail.com
:Copyright:
   `Creative Commons Attribution-ShareAlike 4.0 International Public License`__

:Abstract:
   TODO

   :Filename extension: ``.toml``
   :Documentation: https://github.com/toml-lang/toml

.. contents::

.. sectnum::
   :suffix: .

__ https://creativecommons.org/licenses/by-sa/4.0/

.. _Davie Badger: https://github.com/daviebadger



Keys
====

Keys, respectively key/value pairs are the main building blocks in TOML, and so
there are many ways, how to write these keys. Also, there are special keys which
wraps other ones into so-called tables (collections of pairs).

Key/Value Pairs
---------------

A key/value pair according to its name consists of a key followed by a space,
an equal sign, another space, and a concrete value:

.. code:: toml

   key = "value"

Keys may be written in these formats:

* a bare format where ASCII letters, digits, underscores, and dashes are only
  allowed (even if it contains only digits, it is always interpreted as a
  string):

  .. code:: toml

     key-with-dashes = "value"
     key_with_underscores = "value"
     123 = "value"

* a quoted format using single or double quotes around and spaces inside or any
  other special characters, but should be used only when necessary (quotes are
  later explained in a standalone section covering string values):

  .. code:: toml

     "double quotes" = "value"
     'single quotes' = "value"

* a dotted format where dots create a nested structure of keys, but when used
  inside quotes, then this behavior is disabled:

  .. code:: toml

     properties.a = "value"
     properties.b = "value"
     properties."a.b" = "value"

     # in JSON:
     #
     # {
     #   "properties": {
     #     "a": "value",
     #     "b": "value",
     #     "a.b": "value",
     #   }
     # }

.. note::

   TOML has no standardization about key names. Basically, these rules are taken
   from a programming language in which is used. So for Python users, it is a
   ``snake_case``style. For Javascript users, it is a ``camelCase`` style, and
   so on.

.. warning::

   When using the dotted format, the user should be aware that is not possible
   to write a dotted key if a parent key already exists (trying to have a key
   with a specific value and then a dotted key with a different value):

   .. code:: toml

      # INVALID

      parent = 1
      parent.child = 2

Tables
------

TODO

Array of Tables
---------------

TODO



Values
======

Concrete data types which may be used as values in keys, namely:

* strings
* integers
* floats
* booleans
* date-times
* dates
* times
* inline tables
* arrays

The last two types hold other types from this list, even themselves.

Strings
-------

Strings may be divided into two groups, whether they support the escaping
mechanism or not. Each group may further exist in an inline or a multi-line
version:

* basic (escaping is allowed):

  * inline:

    .. code:: toml

       key = "I'm David"
       escaped = "\""

  * multi-line (the first newline is removed while other ones are untouched):

    .. code:: toml

       key = """
       This is a
       multi-line
       basic string"""

* literal (escaping is disallowed):

  * inline:

    .. code:: toml

       key = 'Cannot use single quotes inside'

  * multi-line (the first newline is removed while other ones are untouched):

    .. code:: toml

       key = '''
       This is a
       multi-line
       literal string'''

.. note::

   When using a literal string, it is not possible to use a single quote inside.
   The solution is to use a multi-line literal string, which also can be written
   like an inline string (the same goes for basic ones):

   .. code:: toml

      basic = """ " """    # <space>"<space>
      literal = ''' ' '''  # <scape>'<space>


Integers
--------

Integers are either positive or negative without infinity:

* positive integer:

  .. code:: toml

     key = 1

* negative integer:

  .. code:: toml

     key = -1

Underscores may be used after thousands for better readability:

* positive integer with underscores:

  .. code:: toml

     key = 1_000_000

* negative integer with underscores:

  .. code:: toml

     key = -1_000_000

Floats
------

Floats are numbers with a decimal point, including infinity. They also may be
written via scientific notation, if needed. Lastly, underscores are allowed too
like for integers:

* positive float:

  .. code:: toml

     key = 1.0

* positive infinity:

  .. code:: toml

     key = inf

* positive float with scientific notation:

  .. code:: toml

     key = 1e+0

* positive float with underscores:

  .. code:: toml

     key = 1.123_456_789

* negative float:

  .. code:: toml

     key = -1.0

* negative infinity:

  .. code:: toml

     key = -inf

* negative float with scientific notation:

  .. code:: toml

     key = -1e+0

* negative float with underscores:

  .. code:: toml

     key = -1.123_456_789

Booleans
--------

Booleans are represented by true or false:

* true:

  .. code:: toml

     key = true

* false:

  .. code:: toml

     key = false

Date-Times
----------

TOML has two variants of date-times.

The first one is recognized as a local date-time without information about a
time zone. The date-time notation is according to RFC 3339, where are allowed
both ``T`` and space delimiters (between date and time), and it is up to users
which delimiter choose:

* local date-time with ``T`` delimiter:

  .. code:: toml

     key = 2020-01-31T12:30:00

* local date-time with space delimiter:

  .. code:: toml

     key = 2020-01-31 12:30:00

The second variant is an offset date-time where a time zone play a role. The
notation is the same as for local date-times except appended ``Z`` delimiter for
a time zone. The default time zone is UTC if not specified.

  * offset date-time in UTC:

    .. code:: toml

       t = 2020-01-31T12:30:00Z
       space = 2020-01-31 12:30:00Z

  * offset date-time in a specific time zone:

    .. code:: toml

       t = 2020-01-31T12:30:00+01:30
       space = 2020-01-31 12:30:00+01:30

Dates
-----

Local dates use a ``YYYY-mm-dd`` format:

.. code:: toml

   key = 2020-01-31

Times
-----

Local times use a ``HH:MM:SS`` format:

.. code:: toml

   key = 12:30:00

Inline Tables
-------------

Inline tables are tables which fit only into a single line (compact version) to
decrease verbosity over classic tables. They may be used for group data.

In the sense of syntax, inline tables are similar to object notation in JSON
except for stringified keys, so at the start and the end are curly braces, and
keys with values are separated from others by commas:

.. code:: toml

   key = { name = "David", age = 25 }

   # is same as
   #
   # [table]
   # name = "David"
   # age = 25

.. note::

   According to the latest reference guide (not library implementation yet), it
   is not allowed to add new keys to an already existing inline table like
   ``key.gender = "male"``. Only standard tables may be extended.

Arrays
------

Arrays are containers, which contain multiple values. The values may be either
homogeneous (single data type) or heterogeneous (mixed data types).

In the sense of syntax, arrays are the same as arrays in JSON, so square
brackets are at the start and the end, and values are separated from others by
commas:

.. code:: toml

   integers = [ 1, 2, 3 ]
   floats = [ 0.0, 0.1 ]
   mixed = [ 1, 1.0 ]

Arrays also may be nested and may span multi-line if it helps readability (for
example, an array of inline tables):

.. code:: toml

   nested = [ [ 1, 2, 3 ], [ 4, 5, 6 ] ]
   inline_tables = [
     { x = 1, y = 2, z = 3 },
     { x = 4, y = 5, z = 6 },
   ]

.. note::

   About standardization:

   1. Spaces after the opening and ending square brackets are optional, but they
      are relatively very used in the TOML reference guide.
   2. Indentation is two spaces for the same reason as the first point.
   3. It is quite common to use a trailing comma at the end of the last value
      in a multi-line array, and TOML has the support for it.



Other
=====

Syntax, which is neither related to the keys nor the values.

Commnets
--------

There are two ways, how to write comments for explaining used values if it is
not clear at first sight:

* inline, where a comment starts at the end of a line after a value, with at
  least one space before a ``#``  (it may be two spaces like in Python):

  .. code:: toml

     key = "value"  # This is an inline comment.

* full-line, where a comment starts at the beginning of a (un)indented line:

  .. code:: toml

     # This is a full-line comment
     # over two lines.
     key = "value"

References
==========

* `GitHub - TOML Wiki`__
* `TOML`__
* `Wikipedia - TOML`__

__ https://github.com/toml-lang/toml/wiki
__ https://toml.io/en/latest
__ https://en.wikipedia.org/wiki/TOML
