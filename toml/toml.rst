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



Values
======


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
