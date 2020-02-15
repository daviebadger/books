======
 YAML
======
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

Booleans
--------

Use a boolean value:

#. true:

   .. code:: yml

      true

#. false:

   .. code:: yml

      false

.. note::

   Old YAML version 1.1 supports more values as boolean ones:

   * ``on`` / ``off``
   * ``yes`` / ``no``

   Both lowercased and uppercased variants are valid. However, it may be
   ambiguous, especially the ``NO`` variant. Did I mean Norway (alpha-2 countr
   code) or the false value?

   That is why it is reduced in the YAML version 1.2 only to ``true`` or
   ``false``, like in JSON.



Collections
===========

Mappings
--------

Sequences
---------



References
==========

* `Google Search - YAML Reference`__
* `Learn yaml in Y Minutes`__
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
