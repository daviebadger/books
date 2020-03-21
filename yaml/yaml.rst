==========
 YAML 1.2
==========
------------------------------------------
 Human-Readable Data Serialization Format
------------------------------------------

:Author: `Davie Badger`_
:Contact: davie.badger@gmail.com
:Copyright:
   `Creative Commons Attribution-ShareAlike 4.0 International Public License`__

:Abstract:
   YAML is mostly used for user configuration where applications themself are
   already running and are about to read user settings before further
   processing. Some notable projects using it are various CI/CD services
   (`GitHub Actions`_, `GitLab CI/CD`_), tools for infrastructure automation
   (Ansible_, Salt_, Kubernetes_) or proxies (Envoy_).

   Unlike JSON_, YAML is even a more human-readable data serialization format.
   It has comments, multi-line strings, documents metadata, and supports reusing
   values. It may be easily converted to JSON because YAML is simply a superset
   of JSON.

   Downsides are a lot of features, either from YAML itself or libraries for
   reading and writing, you probably never use them all. Because YAML implicitly
   inherits data types, there may be surprises you would not expect if you do
   not know these catches.

   :Filename extension:
      ``.yaml``, but ``.yml`` is more common due to archaic maximal 3-letter
      extension limit
   :Documentation: https://yaml.org/spec/1.2/spec.html

.. contents::

.. sectnum::
   :suffix: .

__ https://creativecommons.org/licenses/by-sa/4.0/

.. _Ansible: https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html
.. _Davie Badger: https://github.com/daviebadger
.. _Envoy: https://www.envoyproxy.io/docs/envoy/latest/start/start
.. _GitHub Actions: https://help.github.com/en/actions/automating-your-workflow-with-github-actions/configuring-a-workflow
.. _GitLab CI/CD: https://docs.gitlab.com/ee/ci/#getting-started
.. _JSON: https://www.json.org/json-en.html
.. _Kubernetes: https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/
.. _Salt: https://docs.saltstack.com/en/latest/topics/yaml/index.html



Scalars
=======

Scalars are one of three basic primitives in YAML (in the sense of data
structures). They are not usually used alone but as values in collections.

They are represented by:

* strings
* integers
* floating points
* booleans
* null
* timestamps

Strings
-------

Strings (text) may be written in two ways (styles or also concepts) that are
common in YAML:

* flow style
* block style

In general, flow style means that values are written inline (before or after
may be indicators or other values within the same line), while in a block style,
values start on separate lines.

Flow Style Strings
^^^^^^^^^^^^^^^^^^

Strings in the flow style may be written in three possible styles:

#. plain style without quotes around, where is not possible to use escape
   characters at all:

   .. code:: yaml

      text

#. single-quoted style using a ``'`` indicator without the support for escape
   characters (the only possible way is to double single quotes if needed):

   .. code:: yaml

      'I''m David'

#. double-quoted style using a ``"`` indicator with the support for escape
   characters, such as ``\"`` or ``\n``:

   .. code:: yaml

      "Hello\nWorld"

.. hint::

   In all of the three flow styles is possible to write multi-line strings by
   continuing on the next lines like:

   .. code:: yaml

      'This is a long sentence
      over two lines.'

   However, it has some downsides, mostly aesthetics, when using quotes or in
   mappings where are indentation. Therefore it is better to use block style
   strings.

.. tip::

   It is better to use only the quoted styles for flow style strings to be
   consistent throughout a document and also to avoid pitfalls when using YAML
   indicators in the plain style strings by mistake which could cause a syntax
   error during parsing.

Block Style Strings
^^^^^^^^^^^^^^^^^^^

Strings in the block style may be written in two possible styles, where both do
not support escape characters (text is literally kept as is):

#. literal style using a ``|`` indicator, where non-empty lines are joined by
   newlines:

   .. code:: yaml

      |
        pwd
        ls
        touch file.txt

#. folded style using a ``>`` indicator, where non-empty lines are joined by
   spaces:

   .. code:: yaml

      >
        This is
        the first paragraph.

        This is the second paragraph
        after a line break.

Both literal and folded style strings end by default with a newline(s) after
deserialization. These final line breaks may be controlled by chomping
indicators used after block style indicators.

There are three ways (methods):

#. clip (no chomping indicator) - a string ends with a single newline (the
   default behavior)

   .. code:: yaml

      >-
        a
        b
        c

      # Deserialized string: "a b c\n"

#. strip (``-`` indicator) - a string does not end with a newline(s) at all:

   .. code:: yaml

      >-
        a
        b
        c

      # Deserialized string: "a b c"

#. keep (``+`` indicator) - a string ends with more newlines if the string has
   trailing line breaks (very rarely used):

   .. code:: yaml

      >+
        a
        b
        c

      # Deserialized string: "a b c\n\n"

.. tip::

   Although YAML does not have strictly set indentation levels in documents, it
   is common to use consistently two spaces as indentation. Most examples in the
   YAML reference guide use this level.


Integers
--------

Integers are either positive or negative without infinity:

* positive integer:

  .. code:: yaml

     1

* negative integer:

  .. code:: yaml

     -1

Floating Points
---------------

Floating points are numbers with a decimal point, including infinity:

* positive float:

  .. code:: yaml

     1.0

* positive infinity:

  .. code:: yaml

     .inf

* negative float:

  .. code:: yaml

     -1.0

* negative infinity:

  .. code:: yaml

     -.inf

Moreover, from YAML version 1.2 is possible to use the scientific notation for
writing too big or too small numbers like:

* ``1e+0`` (1.0)
* ``1.0e+1`` (10.0)
* ``-1e+0`` (-1.0)
* ``-1.0e+1`` (-10.0)
* ``1e-0`` (1.0)
* ``1.0e-1`` (0.1)

The E notation may be uppercased like in calculators, but it subjectively
blends in with numbers due to the same text size. Next, the plus sign may be
omitted.

Booleans
--------

Booleans are represented by true or false:

* true:

  .. code:: yaml

     true

* false:

  .. code:: yaml

     false

Previous YAML version 1.1 supports more values as boolean ones, namely:

* ``on`` / ``off``
* ``yes`` / ``no``

These booleans are also valid in capitalized or uppercased variants. However, it
may be ambiguous, especially the ``NO`` variant. Did I mean Norway (alpha-2
country code) as a string or the false value?

Despite that, there are still some popular YAML libraries, which support only
the 1.1 version, and this behavior may surprise someone. That is why it is
reduced in the version 1.2 only to ``true`` or ``false``, like in JSON.

.. note::

   Booleans also may be written as ``True`` / ``TRUE``, respectively ``False``
   / ``FALSE``. However, the lowercased ones are the go-to variants.

Null
----

Null is an empty value (also known as ``None`` in Python), which is represented
by the same name keyword:

.. code:: yaml

   null

YAML also has other variants of the null value you may ever encounter with. The
first variant is via a ``~`` indicator instead of the ``null`` keyword. The
second variant is just not using any value at all in block style collections
(empty list item or key).

.. note::

   The ``null`` keyword also may be written as ``Null`` or ``NULL``. However,
   the lowercased one is the go-to variant.

Timestamps
----------

Timestamps are represented by `ISO 8601`_ dates and datetimes (date and time)
or also by spaced datetimes, which are allowed according to :RFC:`3339`:

* ISO-formatted date:

  .. code:: yaml

     2020-02-20

* ISO-formatted datetime without optional microseconds and a time zone:

  .. code:: yaml

     2020-02-20T00:00:00

* ISO-formatted datetime with microseconds:

  .. code:: yaml

     2020-02-20T00:00:00.123

* ISO-formatted datetime with a time zone:

  .. code:: yaml

     2020-02-20T00:00:00+02:30

* ISO-formatted datetime with microseconds and a time zone:

  .. code:: yaml

     2020-02-20T00:00:00.123+02:30

* spaced datetime without optional microseconds and a time zone:

  .. code:: yaml

     2020-02-20 00:00:00

* spaced datetime with microseconds:

  .. code:: yaml

     2020-02-20 00:00:00.123

* spaced datetime with a time zone:

  .. code:: yaml

     2020-02-20 00:00:00 -1

* spaced datetime with microseconds and a time zone:

  .. code:: yaml

     2020-02-20 00:00:00.123 -1

.. note::

   Although timestamps are a part of scalars, they may not be easily converted
   to JSON like other YAML primitives, which have counterparts in JSON. This
   goes especially for Python, where timestamps are converted to special
   date(time) objects and which are not JSON serializable by default.

.. _ISO 8601: https://en.wikipedia.org/wiki/ISO_8601


Collections
===========

Collections are in general data containers, which contain a collection of scalar
values or also a collection of data containers (collections inside collections).

They are represented by:

* mappings (also known as objects in JSON or dicts in Python)
* sequences (also known as arrays in JSON or lists in Python)

Mappings
--------

Mappings may be written in two styles:

* flow style
* block style

In both styles, mappings are represented by keys and values for these keys. They
may have an "unlimited" number of keys, which should not be duplicated (some
libraries may fail when parsing). It does not matter if keys with values are
sorted or not, because mappings are unordered by default (some libraries may
still keep the order of keys as they are defined).

There is no standard for naming keys. It depends on an underlying programming
language, in which are YAML documents parsed. The language itself usually has
its naming conventions (case styles). Whether it is a snake case or a camel
case, all case styles are valid from a YAML point of view.

Flow Style Mappings
^^^^^^^^^^^^^^^^^^^

Flow style mappings are usually inline mappings, although they may span multiple
lines. They are using ``{}`` indicators as borders. Inside are keys, which are
separated from values by a ``:`` indicator followed by space. Key/value pairs
are separated from each other by a ``,`` indicator followed by space:

.. code:: yaml

   {x: 0, y: 1}

Because of their compatibility with JSON objects, keys also may be quoted,
though it is optional:

.. code:: yaml

   {"x": 0, "y": 1}

.. note::

   YAML is benevolent with spacing. They are not limited when using right after
   curly braces or before them. The same goes after key/value pairs:

   .. code:: yaml

      { x: 0,   y: 1 }

   Even the last key/value pair may end with a comma before the ending curly
   brace:

   .. code:: yaml

      { x: 0, y: 1, }

.. tip::

   Flow style mappings are ideally used with block style sequences, where their
   values are just inline mappings, which fit into a line length. It may look
   like a row-oriented table.

Block Style Mappings
^^^^^^^^^^^^^^^^^^^^

Block style mappings have keys starting on a new line, which also may be
indented. There are no curly braces or commas, only the ``:`` indicator for
separating keys from values:

.. code:: yaml

   boolean: true
   floating point: 1.0
   flow_string: "text"
   integer: 1
   NestedBlockMapping:
     blockString: |-
       text
     NestedFlowMapping: {x: 0, y: 1}
   null: null
   timestamp: 2020-02-20

.. note::

   YAML has a ``?`` indicator. If it is used before a key, then the key may be
   any primitive such as a sequence. Nevertheless, these special keys may not be
   supported in the targeted programming language. Therefore it is safe to use
   only a single word key ideally.


Sequences
---------

Sequences also may be written in two styles:

* flow style
* block style

In both styles, sequences are represented by an ordered list of values.

Flow Style Sequences
^^^^^^^^^^^^^^^^^^^^

Flow style sequences are usually inline sequences, although they may span
multiple lines. They are using ``[]`` indicators as borders. Inside are values,
which are separated by a ``,`` indicator followed by space:

.. code:: yaml

   [0, 1]

.. note::

   Like in flow style mapping, YAML is also benevolent with spacing in flow
   style sequences, including the support for a comma after the last item:

   .. code:: yaml

      [ 0,   1, ]

.. tip::

   Flow style sequences are also ideally used with block style sequences. For
   example, to create a two-dimensional list, where a block style list
   represents rows and a flow style list columns.

Block Style Sequences
^^^^^^^^^^^^^^^^^^^^^

Block style sequences have values starting on a new line, which also may be
indented. There are no square brackets or commas. There is only a ``-``
indicator followed by space at the beginning of a (un)indented line for starting
a value:

.. code:: yaml

   - false
   - -1.0
   - "text"
   - -1
   - flowSequence: [0, 1]
     NestedBlockMapping:
       block string: >-
         text
       blockSequence:
         - {x: 0, y: 1}
         - {x: 1, y: 2}
         - {x: 2, y: 3}
     NestedBlockSequence:
       -
         - a
         - b
         - c
   - null
   - 2020-02-20



References
==========

* `Google Search - YAML Reference`__
* `Learn X in Y minutes - Learn yaml in Y Minutes`__
* `Stack Overflow - Is it .yaml or .yml?`__
* `Wikipedia - YAML`__
* `YAML - Reference card`__
* `YAML - YAML Ain’t Markup Language (YAML™) Version 1.1`__
* `YAML - YAML Ain’t Markup Language (YAML™) Version 1.2`__

__ https://www.google.com/search?q=yaml+reference
__ https://learnxinyminutes.com/docs/yaml/
__ https://stackoverflow.com/questions/21059124/is-it-yaml-or-yml
__ https://en.wikipedia.org/wiki/YAML
__ https://yaml.org/refcard.html
__ https://yaml.org/spec/1.1/
__ https://yaml.org/spec/1.2/spec.html
