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

TODO

Key/Value Pairs
---------------

TODO

Tables
------

TODO

Array of Tables
---------------

TODO



Values
======

TODO

Strings
-------

TODO

Integers
--------

TODO

Floats
------

TODO

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

TODO

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
   `key.sex = "male"`. Only standard tables may be extended.

Arrays
------

TODO



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
