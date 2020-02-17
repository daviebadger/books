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



Syntax
======


Scalars
-------

Strings
^^^^^^^

Flow Style
""""""""""

Use a string value:

* plain style without the support for escape characters:

  .. code:: yaml

     text

* single-quoted style without the support for escape characters (the only way is
  to double single quotes):

  .. code:: yaml

     'I''m David'

* double-quoted style with the support for escape characters, such as ``\"``
  or ``\n``:

  .. code:: yaml

     "Hello\nWorld"


Numbers
^^^^^^^

Integers
""""""""

Use an integer value:

* positive:

  .. code:: yaml

     1

* negative:

  .. code:: yaml

     -1

Floating Points
"""""""""""""""

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
^^^^^^^^

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
^^^^

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
-----------

Mappings
^^^^^^^^

Sequences
^^^^^^^^^



References
==========

* `Google Search - YAML Reference`__
* `Learn X in Y minutes - Learn yaml in Y Minutes`__
* `Stack Overflow - Is it .yaml or .yml?`__
* `Wikipedia - YAML`__
* `YAML`__
* `YAML -  YAML Ain’t Markup Language (YAML™) Version 1.1`__
* `YAML -  YAML Ain’t Markup Language (YAML™) Version 1.2`__

__ https://www.google.com/search?q=yaml+reference
__ https://learnxinyminutes.com/docs/yaml/
__ https://stackoverflow.com/questions/21059124/is-it-yaml-or-yml
__ https://en.wikipedia.org/wiki/YAML
__ https://yaml.org/
__ https://yaml.org/spec/1.1/
__ https://yaml.org/spec/1.2/spec.html
