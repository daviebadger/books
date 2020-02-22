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

Strings
-------

Strings may be written in two ways (styles or also concepts) that are common
in YAML:

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

Use an integer value:

* positive:

  .. code:: yaml

     1

* negative:

  .. code:: yaml

     -1

Floating Points
---------------

Use a floating point (float) value:

* positive:

  .. code:: yaml

     1.0

* positive infinity:

  .. code:: yaml

     .inf

* negative:

  .. code:: yaml

     -1.0

* negative infinity:

  .. code:: yaml

     -.inf

.. tip::

   Since YAML version 1.2 is possible to use the scientific notation for writing
   too big or too small numbers like:

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

Use a boolean value:

* true:

  .. code:: yaml

     true

* false:

  .. code:: yaml

     false

.. note::

   Old YAML version 1.1 supports more values as boolean ones:

   * ``on`` / ``off``
   * ``yes`` / ``no``

   Capitalized, lowercased or uppercased variants are also valid. However, it
   may be ambiguous, especially the ``NO`` variant. Did I mean Norway (alpha-2
   country code) or the false value?

   That is why it is reduced in the YAML version 1.2 only to ``true`` or
   ``false``, like in JSON.

Null
----

Use a null (empty) value:

.. code:: yaml

   null

.. hint::

   In block mappings and sequences (collections), if a value is not defined
   (left empty), then it is interpreted as a null value. This way is not
   possible to use in flow collections. Therefore, it is better to use
   explicitly ``null``.

.. note::

   Alternatively, ``~`` is also interpreted as a null value, nevertheless
   ``null`` is 1:1 to JSON null value.


Collections
===========

Collections are in general data containers, which contain a collection of scalar
values or also a collection of data containers (collections inside collections).

They are represented by:

* mappings (also known as objects in JSON or dicts in Python)
* sequences (also known as arrays in JSON or lists in Python)

Mappings
--------

Sequences
---------



References
==========

* `Google Search - YAML Reference`__
* `Learn X in Y minutes - Learn yaml in Y Minutes`__
* `Stack Overflow - Is it .yaml or .yml?`__
* `Wikipedia - YAML`__
* `YAML - YAML Ain’t Markup Language (YAML™) Version 1.1`__
* `YAML - YAML Ain’t Markup Language (YAML™) Version 1.2`__

__ https://www.google.com/search?q=yaml+reference
__ https://learnxinyminutes.com/docs/yaml/
__ https://stackoverflow.com/questions/21059124/is-it-yaml-or-yml
__ https://en.wikipedia.org/wiki/YAML
__ https://yaml.org/spec/1.1/
__ https://yaml.org/spec/1.2/spec.html
