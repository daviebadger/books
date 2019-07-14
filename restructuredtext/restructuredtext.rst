==================
 reStructuredText
==================
---------------------------------------------------------
 Lightweight Markup Language for Technical Documentation
---------------------------------------------------------

:Author: `Davie Badger`_
:Contact: davie.badger@gmail.com
:Copyright: `Creative Commons Attribution 4.0 International Public License`_

:Abstract:
   `reStructuredText`_ (RST or also reST) is heavily used in Python community
   for writing technical documentation, both Python docstrings and standalone
   documents. Other notable projects using |RST| for documentation are Blender_,
   CMake_ or `Linux Kernel`_.

   Unlike `Markdown`_, |RST| covers officially many advanced markup, for example
   document metadata, automatic table of contents, tables and semantic text. It
   has also a standardized way for writing custom extensions (directives and
   interpreted text roles) via `Docutils`_ library written in Python.

   |RST| is commonly used with `Sphinx`_, which is a documentation generator
   originally developed for official `Python documentation`_, but now it is
   independent from projects using a different programming language or none at
   all.

   :Filename extension: ``.rst``
   :Reference documentation: http://docutils.sourceforge.net/rst.html#reference-documentation
   :Online editor: http://rst.ninjs.org (unmaintained)

.. contents::

.. sectnum::
   :depth: 3
   :suffix: .

.. _Blender: https://docs.blender.org/manual/en/latest/
.. _CMake: https://cmake.org/cmake/help/latest/
.. _Creative Commons Attribution 4.0 International Public License: https://creativecommons.org/licenses/by/4.0/
.. _Davie Badger: https://github.com/daviebadger
.. _Docutils: http://docutils.sourceforge.net/
.. _Linux Kernel: https://www.kernel.org/doc/html/latest/
.. _Markdown: https://daringfireball.net/projects/markdown/
.. _Python documentation: https://docs.python.org
.. _reStructuredText: http://docutils.sourceforge.net/rst.html
.. _Sphinx: http://www.sphinx-doc.org



Markup
======

Markup is a set of special characters within text. Parsers thanks to them know,
how to transform the given text in a document to other text or file formats, for
example HTML or PDF.


Sections
--------

Sections headers are a single line of text with an underline or an underline and
an overline of non-alphanumeric characters (adornment), which are at least as
long as the text:

.. code:: rst

   *************
   Section Title
   *************

   ...

Although there are many non-alphanumeric characters, none of them is associated
with a specific heading level. Therefore, it is very important to be consistent
with heading levels through a document.

Python documentation has the following convention (with analogous heading levels
in HTML), which may be followed:

* ``#`` with overline and centered title text using 2 spaces at the left edge,
  for parts (H1 in master documents in Sphinx) [#]_

  .. code:: rst

     ##################
       Document Title
     ##################

* ``*`` with overline, for chapters (H1 in ordinary documents)

  .. code:: rst

     **************
     Document Title
     **************

* ``=`` for sections (H2)

  .. code:: rst

     Section Title
     =============

* ``-`` for subsections (H3)

  .. code:: rst

     Subsection Title
     ----------------

* ``^`` for subsubsections (H4)

  .. code:: rst

     Subsubsection Title
     ^^^^^^^^^^^^^^^^^^^

* ``"`` for paragraphs (H5)

  .. code:: rst

     Paragraph Title
     """""""""""""""

For standalone documents out of documentation, if there is a need to use a
document title with a subtitle, then the following adornment style is
recommended by |RST|:

.. code:: rst

   ================
    Document Title
   ================
   ----------
    Subtitle
   ----------

   Section Title
   =============

.. note::

   When a document has a lot of text within sections and scrolling is needed in
   that document, then it may easily get you lost unless you use a |RST| plugin
   with quick table of contents.

   Python documention has mention about generous using blank lines, but nothing
   concrete, how many should be used. In generous, it makes sense to use more
   than one blank line between sections with body elements.

   The following numbers may be used:

   * 3 blank lines between sections (H2)
   * 2 blank lines between subsections (H3)
   * 1 blank line between subsubsections (H4)

.. tip::

   There may exist a |RST| plugin to your editor, which can speed up creating
   section headers by highlighting a section title and applying a keyboard
   shortcut for a specific heading level.

.. _The Python documentation: https://devguide.python.org/documenting/#sections


Paragraphs
----------

Paragraphs are chunks of text aligned at the left edge and separated by a blank
line:

.. code:: rst

   This is a paragraph over
   three lines, but the line breaks
   will not be preserved.

   This is another paragraph.

To preserve line breaks in paragraphs, a vertical bar ("|") with a space must be
used at the left edge of each line with a line break in order to create line
blocks:

.. code:: rst

   | First line
   | Second line
   | Third line
   |
   | Fifth line

   ...

It is also possible to join lines if they are left-aligned with text at a line
containing a line break:

.. code:: rst

   | A really long line
     which continues over
     another lines

   ...

.. tip::

   Python documentation uses maximally 80 characters per line except a few
   special cases (tables, hyperlinks, code samples), when it is allowed to
   exceed this limit.


Text Styles
-----------

Text in paragraphs and other body elements [#]_ is normal by default (no text
style), unless some parts of text need to be emphasized. One asterisk ("*")
around a word(s) indicates emphasis (italics), whereas two asterisks indicate
strong emphasis (boldface):

.. code:: rst

   *This part of text will be rendered in italics*,
   **while this one in bold**.

|RST| is pretty smart when to not use italics or boldface, if there are spaces
or asterisks inside a word:

.. code:: rst

   1 * 1 is 1. 2*2 is 4. 3 ** 3 is 27.

However, if there is a need to emphasis characters inside a word, then around
asterisks must be spaces escaped:

.. code:: rst

   thisis\ **one**\ word (thisisoneword with "one" in bold)

Escaping can be also used with asterisks or any other special markup found later
in this book:

.. code:: rst

   Explicitly: \*italics\* (twice)
   Implicitly: \**bold** (once)

Besides emphasis, text may be monospaced, which is used for inline code samples.
Each character inside double backquotes ("``") is preserved:

.. code:: rst

   To emphesasize text, you need to use ``*`` around a word, e.g. ``*italics*``.

.. note::

   Because both emphasis and strong emphasis use asterisks, it is not possible
   to use italics and boldface at the same time.


Lists
-----

|RST| has oficially five types of lists, namely:

* bulleted
* numbered (also enumerated)
* definition
* field
* option

Bulleted and numbered lists are classic lists. Definition lists are rather
dictionaries (glossary). Field and option lists are rather special tables.

Bulleted Lists
^^^^^^^^^^^^^^

Bulleted lists consists of a bullet point character, usually an asterisk (like
in Python documentation) followed by one space and an item:

.. code:: rst

   * first item
   * second item
   * third item

Items may continue on the next lines like pagraphs with line breaks or have
other body elements inside text:

.. code:: rst

   * first item over
     two lines
   * second item with two paragraphs

     This is the **second** pagagraph.

Bulleted lists may be also nested, if the inner lists are surrounded by blank
lines and left-aligned with text at the previous line:

.. code:: rst

   * first item
     over two lines

     * first subitem

       * first subsubitem

     * second subitem
     * third subitem

   * second item

Numbered Lists
^^^^^^^^^^^^^^

Numbered (enumerated) lists consists of a number and a formatting type, usually
a period (like in Python documentation) followed by one space and an item:

.. code:: rst

   1. first item
   2. second item over
      two lines
   3. third item

Items may be automatically numbered for greater convenience:

.. code:: rst

   #. item
   #. item
   #. item

Both bulleted and enumerated lists may be combined:

.. code:: rst

   * first outer bulleted item

     1. first numbered item

        * first inner bulleted item

     2. second numbered item

   * second outer bulleted item
   * third outer bulleted item

Definition Lists
^^^^^^^^^^^^^^^^

Definitions lists consists of a term and a definition for that term starting at
the next line with indentation and separated by a blank line from other terms:

.. code:: rst

   RST
      A shortcut for reStructuredText markup language.

   HTML
      Hypertext Markup Language for creating web pages.

Definitions may contain more than one paragraph or other body elements:

.. code:: rst

   Term
      This term cannot be *briefly* explained.

      It requires **two** paragraphs for its definition.

.. tip::

   Python documentation uses 3 spaces for indentation in |RST| documents
   (mainly due to Directives, described later in his book).

Field Lists
^^^^^^^^^^^

Field lists are actually two-column tables, where each row has a header (field)
in the first column and content (field body) in the second column:

.. code:: rst

   :Shortcut: RST or reST
   :Filename extension: ``.rst``
   :Reference documentation: www

Field bodies may contain more than one paragraph or other body elements:

.. code:: rst

   :Body elements:
      * paragraphs
      * lists

      etc.

.. note::

   If a field list is used right after a document title or a subtitle, then
   the field list is supposed to be a bibliographic field list (metadata about
   the document):

   .. code:: rst

      **************
      Document Title
      **************

      :Author: Davie Badger

   Tbere are special bibliographic fields, which are rendered differently than
   other fields:

   * ``:Abstract:`` - body elements are allowed
   * ``:Address:`` - a multi-line address with preserved newlines
   * ``:Author:``
   * ``:Authors:`` - a bulleted list of authors
   * ``:Contact:``
   * ``:Copyright:``
   * ``:Date:``
   * ``:Dedication:`` - body elements are allowed
   * ``:Organization:``
   * ``:Status:``
   * ``:Version:``

Option Lists
^^^^^^^^^^^^

Option lists are two-column tables, where each row has an option(s) in the first
column and a description for that option in the second column which is separated
by at least two spaces:

.. code:: rst

   -v               Verbose
   -h, --help       Display help message
                    and exit
   -n number        Provide a number
   -h, --host=host  Host to connect

It is possible to use body elements in descriptions, but they must be
left-aligned with the previous lines. The longer options, the more indentations
is needed for the body elements on the next lines:

.. code:: rst

   -n number  Provide a number.

              Allowed formats:

              * integer
              * float

.. note::

   If |RST| documents are written inside Sphinx, then it is better to use its
   directives for documenting command-line programs and options, because they
   more scalable, easier to maintain and better rendered in other formats.

.. tip::

   There may exist a |RST| plugin to your editor which support automatic
   alignment in option lists by highlighting an option list and applying a
   keyboard shortcut.


Hyperlinks
----------

Hyperlinks point to internal or external location. The most easiest way to
create a hyperlink target is to place an URI into text:

.. code:: rst

   Python documentation is located on https://docs.python.org/.

Alternatively, URIs may be embedded (surrounded by angle brackets "<>") within
a hyperlink text inside backquotes (also backticks "`") followed by an
underscore:

.. code:: rst

   Python documentation is `HERE <https://docs.python.org/>`_.

Nevertheless, in |RST| philosophy, hyperlink targets should be placed away of
text due to readability. Possible places are the end of a section or a whole
document. Hyperlinks within text should reference to these targets.

Hyperlink references may be single words followed by an underscore or several
words inside backqoutes also followed by an underscore, which are associated
with hyperlink targets leading to URIs:

.. code:: rst

   Python_ has `official documentation`_

   .. _Python: https://www.python.org/
   .. _official documentation: https://docs.python.org/

Within hyperlink targets it is possible to group several targets and point to
single location or point from one hyperlink target to another hyperlink
reference:

.. code:: rst

   Python_, `Python 3`_, `Python 3.7`_, all point to the same location_.

   .. _Python:
   .. _Python 3:
   .. _Python 3.7: https://www.python.org/
   .. _location: Python_

Hyperlinks can be anonymous (not named), which may be handy in cases when same
hyperlink text need to target two different locations. They may be also used in
a list with hyperlinks. Anonymous hyperlinks require two trailing underscores:

.. code:: rst

   References
   ==========

   * link__
   * `long link`__

   .. __: www for link
   .. __: www for long link

The anonymous hyperlink targets may be shortened:

.. code:: rst

   References
   ==========

   * link__
   * `long link`__

   __ www for link
   __ www for long link

.. note::

   If hyperlink references contain colons, then they must be escaped or
   backquoted within hyperlink targets:

   .. code:: rst

      `Link: with colon`_ or `Another link: with colon`_

      .. _`Link: with colon`: ...
      .. _Another link\: with colon: ...

.. tip::

   Sections in documents may be also hyperlinked according to their titles:

   .. code:: rst

      Section A
      =========

      See `Section B`_ below.

      Section B
      =========

   Other body elements may be also hyperlinked, if they have an internal
   hyperlink reference in the prior paragraph:

   .. code:: rst

      .. _List of shortcuts:

      * rst / RST
      * reST

      reST has a few shortcuts, see `List of shortcuts`_ (above).


Tables
------

|RST| has two builtin types of tables, simple and grid. Other advanced table
types use `Directives`_ notation.

Simple Tables
^^^^^^^^^^^^^

Simple tables are tables without row or column spans (only in headers), in which
are equal signs ("=") used as an adornment style for table headers and for
ending a table. Each column must be separated by two spaces:

.. code:: rst

   This is a simple table:

   =========  ========  ======  ===
   Firstname  Lastname  Gender  Age
   =========  ========  ======  ===
   Davie      Badger    Male    24
   Jacob      Badger    Male    19
   =========  ========  ======  ===

All columns except the last one must be adorned as long as the widest cell in
that column. Within these long columns, table headers may be centered:

.. code:: rst

   =======  =======  ===
      A        B      C
   =======  =======  ===
   Value A  Value X  Value 1
   Value B  Value Y  Value 2
   Value C  Value Z  Value 3
   =======  =======  ===

.. note::

   Although simple tables enable to use column spans in table headers or empty
   cells via single backward slash ("\") in that cells, it is better to use
   `Grid Tables`_ for these features and leave simple tables to be just simple
   tables.

.. tip::

   There may exist a |RST| plugin to your editor, which can speed up modifying
   simple tables by highlighting a table and applying a keyboard shortcut for
   extending / shortering adornment and realigning text within that table.

Grid Tables
^^^^^^^^^^^

Grid tables are tables with full suport for row spans, column spans, empty cells
and body elements inside cells. However, these features come at cost, because
grid tables are really cumbersome to design without a |RST| plugin in an editor.

Grid tables consists of plus signs ("+") as corners, vertical bars ("|") as
column separators, minus signs ("-") as row separators and equal signs ("=") as
separator between table headers and other rows:

.. code:: rst

   This is a grid table:

   +------------+--------------------+----------+
   | Header A   | Header B           | Header C |
   +============+====================+==========+
   | A1         | B1 + C1 (column span)         |
   +------------+--------------------+----------+
   | A2 + A3    | * first item       | C2       |
   | (row span) | * second item      |          |
   |            | * third item       |          |
   |            +--------------------+----------+
   |            | C3 is **empty**    |          |
   +------------+--------------------+----------+

.. note::

   If vertical bars are used inside cells, for example in inline code samples,
   then it is really important, where are the vertical bars located in that
   cells.

   |RST| may be confused, if a vertical bar is placed right in a place, which
   indicates column separation. Therefore a blank line on the next line is
   needed in this case to signal |RST| that the vertical bar has a different
   purpose:

   .. code:: rst

      +--------------+----------+-----------+-----------+
      | row 1, col 1 | column 2 | column 3  | column 4  |
      +--------------+----------+-----------+-----------+
      | row 2        | Use the command ``ls | more``.   |
      |              |                                  |
      +--------------+----------+-----------+-----------+
      | row 3        |          |           |           |
      +--------------+----------+-----------+-----------+

.. tip::

   |RST| provides directives for simplier work with tables, which will be
   covered later in this book.


Code Samples
------------

Code samples are indented pieces of code, which begin with a special unindented
paragraph containing only two colons followed by a blank line:

.. code:: rst

   Example from Python:

   ::

      def hello(name="World"):
          print(f"Hello {name}")


      hello()
      hello("Davie")

The two colons may appear at the end of text followed by a space:

.. code:: rst

   Example from Python: ::

      hello()

Both previous examples may be even further shortened, when |RST| will left one
colon instead of two colons at the end of the paragraph which will look exactly
like in the first example:

.. code:: rst

   Example from Python::

      hello()

Short Python code samples without blank lines may be also written like
interactive interpreter (no need to indent code):

.. code:: rst

   Example from Python:

   >>> print("Hello World")
   Hello World

.. note::

   Code samples using ``::`` markup are not highlighted at all, except the
   Python interactive examples. There are special directives for this case
   (either in |RST| or Sphinx).


Block Quotes
------------

Block quotes are just indented paragraphs, which may be nested, if text is
left-aligned with the previous lines and the indentations are keeped:

.. code:: rst

   This is a ordinary paragraph.

      This is a **quoted** paragraph.

         This is a *nested* quoted paragraph.

      This is another quoted paragraph
      over two lines.

Several block quotes may be separated from each other either by another ordinary
paragraphs or using two periods as a separator (empty comment):

.. code:: rst

   Famoues quotes from X Y:

      First quote.

   ..

      Second quote.

   ..

      Third quote.

At the end of block quotes, it is possible to give attribution to a specific
author of that quotes, if before name are two hyphens:

.. code:: rst

   This is a ordinary paragraph.

      This is a super quote.

      -- X Y


Comments
--------

Comments are hidden pagraphs, which starts with two periods followed by a space
and other lines are left-aligned to this indentation:

.. code:: rst

   .. This is a comment
      over two lines.

      This is another paragraph inside this single comment.


Footnotes
---------

Footnotes consits of numbers (indexes) inside square brackets followed by an
underscore in text and descriptions (footnote) for that indexes usually at the
end of documents:

.. code:: rst

   ``#`` with overline is used as an adornment style for document titles in
   master documents in Sphinx [1]_.

   .. [1] Master documents are special ``index.rst`` files with a TOC.

For short documents may be explicit numbers enough, but if a document is long or
regularly changed, it is better to use auto-numbered footnotes to save time with
overriding:

.. code:: rst

   ``#`` with overline is used as an adornment style for document titles in
   master documents in Sphinx [#]_.

   .. [#] Master documents are special ``index.rst`` files with a TOC.

Long footnotes may continue on another lines with other body elements if they
are left-aligned with the left square bracket:

.. code:: rst

   .. [#] Master documents are special ``index.rst``
      files with a TOC.

      They are stored in each directory (group of documents).

.. note::

   Each footnote is automatically hyperlinked to itself. It is possible in
   rendered |RST| documents to click on an index in text, see a footnote at the
   end of a document, click on the index next to the footnote and be back in
   text where I had been previously.

.. tip::

   To insert another footnote between existing auto-numebered footnotes requires
   only to find a previous or next occurence of ``[#]_`` to know where to
   properly place the new footnote.


Horizontal Lines
----------------

Horizontal lines are at least four same successive punctuation characters
surrounded by blank lines between paragraphs:

.. code:: rst

   This is a paragraph.

   ----

   This is another paragraph.

Python documentation has no convention for the horizontal lines. Propably
they are not used at all. However, documentation for |RST| uses hyphens in all
examples.

.. note::

   The purpose of horizontal lines is to signal a change in a subject between
   paragraphs in literature. In |RST| documents, the horizontal lines are rather
   used at the end of files with footnotes.

   If your editor allows you to quickly insert 80 hyphens at once, then you may
   use them instead of four hyphens:

   .. code:: rst

      ...

      --------------------------------------------------------------------------------

      .. [#] Footnote A
      .. [#] Footnote B
      .. [#] Footnote C


Substitutions
-------------

Substitions are words inside vertical bars ("|"), which will be during rendering
substituted with other words according to the given inline directive, which was
used, e.g. a directive for replacing text:

.. code:: rst

   |RST| is really long to type, so it is better to use a shorcut via
   substitutions.

   Also |PY 3| is mentioned a lot of times within a document, so it is better to
   replace it with a specific version.

   .. |RST| replace:: reStructuredText
   .. |PY 3| replace:: Python 3.7.

Other possible inline directives and directives in general are covered in the
`Directives`_ section.

.. note::

   Like in text styles, if a substituion is needed inside a word, then it needs
   spaces around (espaced) in order to be working:

   .. code:: rst

      Thisis\ |one|\ word

      .. |one| replace:: single

.. tip::

   Substitutions may be combined with hyperlinks:

   .. code:: rst

      |RST|_ is really long to type, so it is better to use a shorcut via
      substitutions.

      .. |RST| replace:: reStructuredText
      .. _RST: http://docutils.sourceforge.net/rst.html



Directives
==========

Directives are the primary extension mechanism of |RST| (the secondary are
`Interpreted Text Roles`_), how to extend or modify documents. Syntax is similar
to `Hyperlinks`_, `Footnotes`_ or `Substitutions`_.

They consists of two periods followed by a space, name of directive, two colons,
optionally arguments for that directive and optionally block of content for the
directive:

.. code:: rst

   .. directive-name:: argument

   or

   .. directive-name::

      Long content over
      multiple lines with a blank line
      before this block.

      Python documentation uses that way.

Each directive may have options (configuration for that directive) via a field
list inside the directive. There are two common options, ``class`` and
``name``:

.. code:: rst

   .. directive-name:: argument
      :class: a b c
      :name: Human name for this directive

      Long content over
      two lines.

The ``class`` option allows to define one or more classes separated by a space
for HTML elements and may be additionally styled via CSS, if output of a
document will be HTML page.

The ``name`` allows to add custom human-readable name to directives. The name is
then used like an ID attribute in HTML. This means that each directive with the
name option may be referenced (hyperlinked):

.. code:: rst

   .. directive-name:: content
      :name: Super name

   See also `Super name`_.

.. important::

   When using the ``name`` option inside directives, the name (text) must be
   unique across a document, otherwise a |RST| parser may raise an error.


Image Directives
----------------

Image Directive
^^^^^^^^^^^^^^^

Add an image:

.. code:: rst

   Local image:

   .. image:: path/to/image.png

   Remote image:

   .. image:: www.example.com/image.png

The image directive supports these options:

* ``alt``

  * alternate text, when the image cannot be rendered or for impaired users

* ``height``

  * height of the image, e.g. 100 (default is original height)

* ``width``

  * width of the image, e.g. 100 (default is original width)

* ``scale``

  * scale the image in % (bigger, smaller) with respect to ``height`` or
    ``width`` values, e.g. ``50 %`` (default is 100 %)

* ``align``

  * align the image left or right (both set float and change text flow around)
    or center (default is no alignment)

* ``target``

  * make the image clickable, either to an internal hyperlink target using
    ``Link_`` syntax or to an external link

Figure Directive
^^^^^^^^^^^^^^^^

Add an image with caption (optional):

.. code:: rst

   .. figure:: path/to/image.png
      :alt: alternate text

      Caption for the image.

Figures may also have a legend defined after a caption using common body
elements:

.. code:: rst

   .. figure:: path/to/image.png
      :alt: alternate text

      Caption for the image.

      Legend for the image with a grid table.

The figure directive supports same options like for `Image Directive`_, except
for the ``align`` option (now aligns the figure, not only image), plus these
options:

* ``figwidth``

  * width of the image and caption in overall

* ``figclass``

   * set class attributes on the figure (by default the ``:class:`` option adds
     classes only to the image)


Table Directives
----------------

Advanced directives for tables. Each of these directives supports these options:

* ``align``

  * align a table ``left`` (default), ``center`` or ``right`` in a document

* ``widths``

  * ``auto`` according to text in columns, ``grid`` for more flexible columns or
    comma-separated fixed numbers (ratio) for columns starting from the left
    (columns from the right may be omitted), e.g. ``15, 10, 30``

Table Directive
^^^^^^^^^^^^^^^

Add a title (optional) to simple or grid tables:

.. code:: rst

   .. table:: Users

      =========  ========  ======  ===
      Firstname  Lastname  Gender  Age
      =========  ========  ======  ===
      Davie      Badger    Male    24
      Jacob      Badger    Male    19
      =========  ========  ======  ===

Align a table and set proportionally size of columns via table options:

.. code:: rst

   Below is a table with proportionally set size for each column except for
   the last one:

   .. table::
      :align: center
      :widths: 10, 10, 5

      =========  ========  ======  ===
      Firstname  Lastname  Gender  Age
      =========  ========  ======  ===
      Davie      Badger    Male    24
      Jacob      Badger    Male    19
      =========  ========  ======  ===

List-table Directive
^^^^^^^^^^^^^^^^^^^^

Create a table via a list style without headers, column or row span (not
allowed at all):

.. code:: rst

   Below is a table without a table title:

   .. list-table::

      * - Davie
        - Badger
        - Male
        - 24
      * - Jacob
        - Badger
        - Male
        - 19

List tables may have either headers in the first row using a ``header-rows``
option or on the left in the first column, like in `Option Lists`_, using a
``stub-columns`` option:

.. code:: rst

   .. list-table:: Table with headers in the first row
      :header-rows: 1

      * - Firstname
        - Lastname
        - Gender
        - Age
      * - Davie
        - Badger
        - Male
        - 24

   .. list-table:: Table with headers in the first column
      :stub-columns: 1

      * - Name
        - reStructuredText
      * - Shortcut
        - rst
      * - Parser
        - Docutils

.. tip::

   If in a row is a list item without content, then it is considered as an empty
   cell:

   .. code:: rst

      .. list-table:: Example with an empty cell

         * - A
           - B
           - C
         * - 1
           -
           - 3

Csv-table Directive
^^^^^^^^^^^^^^^^^^^

Create a table using CSV format:

.. code:: rst

   .. csv-table:: CSV table without headers

      "David", "Badger", "Male", 24
      "Jacob", "Badger", "Male", 19

   .. csv-table:: CSV table with headers
      :header: "Firstname", "Lastname", "Gender", "Age"

      "David", "Badger", "Male", 24
      "Jacob", "Badger", "Male", 19

CSV tables may be loaded relatively from local files or externally from an URL
address, in which case there may be headers in rows, columns or not at all:

.. code:: rst

   .. csv-table:: CSV table without headers
      :file: data.csv

   .. csv-table:: CSV table with headers in the first row
      :file: data.csv
      :header-rows: 1

   .. csv-table:: Remote CSV table with headers in the first column
      :url: www.example.com/data.csv
      :stub-columns: 1

Usually CSV tables are comma-separated values with double quoted values, which
contain commas. Howoever, if a CSV table uses different delim character or
quotes, then the ``csv-table`` directive must know about it via set options:

* ``delim``

  * any character, e.g. ``;``, but default is ``,``, other allowed values are
    ``space`` or ``tab``

* ``quote``

  * quote for string values, default ``"``

* ``escape``

  * escape character for quotes, default ``""``

.. note::

   Options such as ``delim``, ``quote`` and ``escape`` may contain Unicode
   codes, for example ``0x09`` for tabs.


Substitution Directives
-----------------------

Directives suited for substitutions and nothing else.

Replace Directive
^^^^^^^^^^^^^^^^^

Replace text in substitutions:

.. code:: rst

   .. |RST| replace:: reStructuredText

   |RST| is really long to type.

.. note::

   Substitutions may be defined wherever in a document (before or after
   replacement text).

Unicode Directive
^^^^^^^^^^^^^^^^^

Convert unicode numbers to characters:

.. code:: rst

   .. |copy| unicode:: 0xA9

   Copyright |copy| Davie Badger 2019.

Unicode numbers can be followed by a comment, which will not be rendered:

.. code:: rst

   .. |copy| unicode:: 0xA9 .. copyright sign

   Copyright |copy| Davie Badger 2019.

.. note::

   Special symbols should be always used via unicode substitutions, if they are
   impossible to type via a keyboard.

.. tip::

   The unicode directive allows to use trim options as flags (no content for
   the trim fields):

   * ``:ltrim:`` - remove left whitespaces after a substitution
   * ``:rtrim:`` - remove right whitespaces after a substitution
   * ``:trim:`` - remove left and right whitespaces after a substitution

   .. code:: rst

      Davie Badger |TM| will be rendered like ``Davie Badger^TM``.

      .. |TM| unicode:: U+2122
         :ltrim:

Date Directive
^^^^^^^^^^^^^^

Format datetime using Python `time.strftime`_ function (default format is
``%Y-%m-%d``, which is ISO 8601 date):

.. code:: rst

   .. |date| date::
   .. |time| date:: %H:%M:%S

   This document was generated on |date| at |time|.

.. _time.strftime: https://docs.python.org/3/library/time.html#time.strftime


Body Element Directives
-----------------------

Directives to extend existing body elements.

Code Directive
^^^^^^^^^^^^^^

Add a code sample with syntax highlightning:

.. code:: rst

   .. code:: py

      print("Hello World")

Optionally, line numbers may be turned on:

.. code:: rst

   .. code:: py
      :number-lines:

      print("Hello World")

.. note::

   Code examples are highligted via Pygments_ syntax highlighter, unless |RST|
   documents are parsed in different parsers (not using Docutils at all).

   List of supported languages (lexers) is in `Pygments documentation`_.

.. _Pygments: http://pygments.org/
.. _Pygments documentation: http://pygments.org/docs/lexers/

Math Directive
^^^^^^^^^^^^^^

Add a mathematical formula using LaTeX math syntax including AMS extensions:

.. code:: rst

   .. math::

      f(x) = x^2

Rubric Directive
^^^^^^^^^^^^^^^^

Add an informal heading, which is not part of the table of contents:

.. code::

   .. rubric:: Footnotes

   .. [#] text

Topic Directive
^^^^^^^^^^^^^^^

Add a topic container with a title to express a self-contained idea separated
from the flow of a document without a need to create another sections:

.. code:: rst

   Section Title
   =============

   Bla bla bla

   .. topic:: Idea

      Foo bar baz

Highlights Directive
^^^^^^^^^^^^^^^^^^^^

Add a summary at the end of a section:

.. code:: rst

   .. highlights::

      A summary of the story:

      * a
      * b
      * c


Admonition Directives
---------------------

Directives for semantic text (additional topic information for readers). |RST|
has the following admonitions:

* ``admonition`` (generic)
* ``attention``
* ``caution``
* ``danger``
* ``error``
* ``hint``
* ``important``
* ``note``
* ``tip``
* ``warning``

Some of these admonitions are almost overlaping (attention, caution, danger), so
the last four admonitions are usually used (important, note, tip, warning).

Important Directive
^^^^^^^^^^^^^^^^^^^

Create an important admonition:

.. code:: rst

   .. important::

      This is really important.

Note Directive
^^^^^^^^^^^^^^

Create a note admonition:

.. code:: rst

   .. note::

      This is a note.

Tip Directive
^^^^^^^^^^^^^

Create a tip admonition:

.. code:: rst

   .. tip::

      This tip saves your life.

Warning Directive
^^^^^^^^^^^^^^^^^

Create a warning admonition:

.. code:: rst

   .. warning::

      Take this warning seriously.


Document Directives
-------------------

Directives about documents, either a document itself or other documents.

Contents Directive
^^^^^^^^^^^^^^^^^^

Generate a table of contents (TOC) from all sections except for a document title
or a subtitle) using a default title ``Contents`` for the TOC:

.. code:: rst

   .. contents::

Alternatively, a different title may be set for the TOC:

.. code:: rst

   .. contents:: Table of Contents

To restrict section levels listed in the TOC, a ``depth`` option must be used:

.. code:: rst

   .. contents::
      :depth: 2

   The table of contents above will show only sections and subsections.

.. tip::

   If a document has a table of contents and it is rendered for example to a
   HTML format, then entries in the TOC and section headers in the document are
   hyperlinked to each other.

Sectnum Directive
^^^^^^^^^^^^^^^^^

Automatically number sections headers in a document:

.. code:: rst

   .. sectnum::

   Sections headers will look like:

   * 1 Section Title
   * 1.1 Subsection Title
   * 1.1.1 Subsubsection Title
   * 2 Section Title

Add a prefix to each numbered section headers:

.. code:: rst

   .. sectnum::
      :suffix: .

   Sections headers will look like:

   * 1. Section Title
   * 1.1. Subsection Title
   * 1.1.1. Subsubsection Title
   * 2. Section Title

It is also possible to limit section headers, which will be numbered, using a
``depth`` option, like in `Contents Directive`_:

.. code:: rst

   .. sectnum::
      :depth: 2

   Sections headers will look like:

   * 1. Section Title
   * 1.1. Subsection Title
   *        Subsubsection Title
   * 2. Section Title

Include Directive
^^^^^^^^^^^^^^^^^

Include relatively another |RST| documents into a current document:

.. code:: rst

   .. include:: file.rst

   .. include:: directory/file.rst

In general, other document types may be also included, however they should be
rendered as code samples (either highlighted or not):

.. code:: rst

   Below will be included a code sample without syntax highlighting:

   .. include:: test.py
      :literal:

   Below will be included a code sample with syntax highlighting:

   .. include:: examples/test.py
      :code: py

.. note::

   Be aware, where is the ``include`` directive used, either at the left edge or
   inside body elements. If it is the first option (edge), then section headers
   are allowed in included documents, otherwise not.

.. warning::

   |RST| parsers may ignore the ``include`` directive, if it is configured that
   way or passed as an option to document convertors.

Raw Directive
^^^^^^^^^^^^^

Paste raw text, which will be used in another document type after rendering:

.. code:: rst

   .. raw:: html

      <script>console.log('Hello World')</script>

Like in `Include Directive`_, it is also possible to include raw documents from
local disk or even from remote websites:

.. code:: rst

   .. raw:: html
      :file: local.html

   or

   .. raw:: html
      :url: www.example.com/file.html

.. important::

   Use wisely the ``raw`` directive, because |RST| will not parse its content
   and the content will be placed as it is. It may represent a potential
   security hole.

.. warning::

   |RST| parsers may ignore the ``raw`` directive, if it is configured that way
   or passed as an option to document convertors.


HTML Directives
---------------

Directives specially for HTML output.

Title Directive
^^^^^^^^^^^^^^^

Set a document meta title, which will be visible in the browser tab, if a
document title is not enough:

.. code:: rst

   **************
   Document Title
   **************

   .. title:: Different Document Title

   The document meta title above will be rendered in HTML head as::

      <title>Different Document Title</title>

Meta Directive
^^^^^^^^^^^^^^

Add HTML metadata, if a document will be converted to HTML and metadata is
desired:

.. code:: rst

   .. meta::
      :author: Davie Badger
      :description: reStructuredText is a markup language used for documentation.
      :keywords: rst, reST, reStructuredText

The meta directive supports out of box meta tags with name attributes in field
lists and content for these fields. The previous code sample would be rendered
as:

.. code:: rst

   <meta name="author" content="Davie Badger">
   <meta name="description" content="reStructuredText is a markup language used for documentation.">
   <meta name="keywords" content="rst, reST, reStructuredText">

Other meta tags and attributes may be supported (not all of them, e.g. charset)
via ``attr=value`` syntax within field names (values may be inside quotes):

.. code:: rst

   This metadata:

   .. meta::
      :description lang="cs": reStructuredText je značkovacý jazyk používaný v dokumentaci.
      :http-equiv=Content-Type: text/html; charset=ISO-8859-1

   would be rendered as::

      <meta name="description" lang="cs" xml:lang="cs" content="reStructuredText je značkovacý jazyk používaný v dokumentaci.">
      <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">

Class Directive
^^^^^^^^^^^^^^^

Add HTML class attributes to the following non-comment element right after this
class directive:

.. code:: rst

   .. class:: super heading

   Section Title With Classes
   ==========================

   .. class:: special

   This is a paragraph with "special" class.

If |RST| elements are nested in the class directive, then classes are applied to
all nested elements:

.. code:: rst

   .. class:: wow

      This paragraph has the "wow" class.

      This paragraph has also the "wow" class.

   Unfortunately, this paragraph has not the "wow" class.

.. note::

   If the class directive is intended to be used before block quotes, then
   immediately after the class directive must follow a comment, otherwise the
   block quote will not have the class attributes (will be misinterpreted as
   paragrahs inside the directive):

   .. code:: rst

      .. class:: not-paragraph
      ..

         This is a block quote.



Interpreted Text Roles
======================

Interpreted text roles are the second standardized way of the extension
mechanism in |RST| how to extend inline markup. By roles is possible to style
inline text, create quickly and easily a hyperlink pointing to a specific domain
or transform the text in a different way.

The syntax of roles consists of a role name without whitespaces surrounded by
colons and immediately followed by role content surrounded by single backquotes:

.. code:: rst

   :role-name:`role-content`

Depending on where are roles used in a sentence, they may require spaces around
role markup, either hard-typed or escaped a backslash. It mainly goes for roles
used inside a single word or wherever inside a sentence, not at the edge.

Examples of using roles in practice:

#. a role used at the edge of a sentence (single space is needed only left or
   right depending on whether it is the start or the end of the sentence):

   .. code:: rst

      It is too :strong:`hot`.

#. a role inside a sentence (spaces must be naturally around the role):

   .. code:: rst

      Do :strong:`not` forget to make your bed!

#. a role inside a word (spaces must be escaped):

   .. code:: rst

      Thisis\ :strong:`one`\ word, where the word "one" will be formatted as bold text.


Built-in Roles
--------------

|RST| has notably these built-in roles:

* ``literal``
* ``math``
* ``sub``
* ``sup``
* ``title``
* ``PEP``
* ``RFC``

Other roles exist just for illustrative reasons, namely ``emphasis`` and
``strong``, which are equivalents of italics and bold text styles.

Finally, there are two special roles, a ``code`` role and a ``raw`` role, which
cannot be used individually, but only in conjunction with a ``role`` directive.

Literal Role
^^^^^^^^^^^^

Create an inline code sample which respects escaped characters with backslashes,
notably backquotes, unlike inline literal markup where backslashes are
preserved:

.. code:: rst

   The text inside enclosed double backquotes (:literal:`\`\`...\`\``) is treated as an inline code sample.

.. attention::

   The previous example is not possible to create via inline literal markup like
   :literal:`\`\`\`\`...\`\`\`\``, because the Docutils parser would have a
   problem to find out where is the start and the end of the inline code sample.
   The same goes for a single backquote like :literal:`\`\`\``.

   In general, if an inline code sample requires using backquotes, then it is
   safer to use the literal role to avoid an unwanted rendered result.

Math Role
^^^^^^^^^

Create an inline mathematical formula in LaTeX_ format without a need to enclose
formulas either into ``\(...\)`` (LaTeX) or ``$...$`` (TeX):

.. code:: rst

   Create a graph of a function :math:`f(x) = x^2`.

.. _LaTeX: https://en.wikibooks.org/wiki/LaTeX/Mathematics

Sub Role
^^^^^^^^

Create a subscript, where the characters are displayed in a smaller size below
a normal line of text:

.. code:: rst

   H\ :sub:`2`\ O is one of the famous chemical formulas.

.. tip::

   Subscripts are ideal candidates for substitutions for improving text
   readability. The previous example could be also written as:

   .. code:: rst

      |H2O| is one of the famous chemical formulas.

      .. |H2O| replace:: H\ :sub:`2`\ O

Sup Role
^^^^^^^^

Create a superscript, where the characters are displayed in a smaller size above
a normal line of text:

.. code:: rst

   E=mc\ :sup:`2` is one of the famous physics formulas.

.. tip::

   Superscripts are also ideal candidates for substitutions. The previous
   example could be also written as:

   .. code:: rst

      |E=mc2| is one of the phyhics phyhics formulas.

      .. |E=mc2| replace:: E=mc\ :sup:`2`

Title Role
^^^^^^^^^^

Create a title of a work, which may be a book, a chapter or any other text
material or even artwork:

.. code:: rst

  `title:`How to Title My Book` is the most selling book in the world.

.. note::

   The title role is the only role which may be used implicitly without
   specifying a role like :literal:`\`How to Title My Book\``. It is due to a
   ``default-role`` directive, which is by default set to the title role:

   .. code:: rst

      .. default-role:: title

   If the ``default-role`` directive is set differently, then it is not safe to
   use the title role implicitly. That is why it is always better to use roles
   explicitly.

PEP Role
^^^^^^^^

Create a link to a specific `PEP`_ (**P**\ ython **E**\ nhancement
**P**\ roposal) [#]_:

.. code:: rst

   See :PEP:`8` for Python style guide.

.. note::

   The previous example could be also written as:

   .. code:: rst

      See `PEP 8`_ for Python style guide.

      .. _PEP 8: https://www.python.org/dev/peps/

.. _PEP: https://www.python.org/dev/peps/

RFC Role
^^^^^^^^

Create a link to a specific `RFC`_ (**R**\ equest **F**\ or **C**\ comments)
[#]_:

.. code:: rst

   See :RFC:`3339` for standard date and time formats.

.. note::

   The previous example could be also written as:

   .. code:: rst

      See `RFC 3339`_ for standard date and time formats.

      .. _RFC 3339: https://tools.ietf.org/rfc/index

.. _RFC: https://tools.ietf.org/rfc/index


Custom Roles
------------

Custom roles may be created in two ways:

#. via the ``role`` directive
#. via programming

The first setup is quick and pretty straightforward, but it is very limited in
creating new roles. It may be used either for styling role content or in
conjunction with the ``code`` role or the ``raw`` role.

The second setup is relatively hard, but it offers technically speaking
unlimited options in comparison with the first way. It requires knowledge about
the Docutils library and programming skills in Python to program new roles.

.. hint::

   Look at already existing roles, either in |RST| or in Sphinx, before creating
   new ones (do not reinvent the wheel).

Custom Roles via the Role Directive
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Examples of creating roles via the role directive:

#. a dummy role only for styling purposes:

   .. code:: rst

      .. role:: strikethrough

      I do :strikethrough:`not` like reStructuredText.

      ----

      HTML & CSS:

      <p>
        I do
        <span class="strikethrough">not</span>
        like reStructuredText.
      </p>

      .strikethrough {
        text-decoration: line-through;
      }

#. an overloaded ``code`` role with a specific language for inline syntax
   highlighting (language names are same as for the ``code`` directive):

   .. code:: rst

      .. role:: python(code)
         :language: python

      Have you ever tried to run :python:`import this` in your Python interpreter?

#. an overloaded ``raw`` role for a specific output format (|RST| recommends
   using a ``raw-`` prefix):

   .. code:: rst

      .. role:: raw-html(raw)
         :format: html

      I do :raw-html:`<del>not</del>` like reStructuredText.

.. caution::

   Use wisely the overloaded ``raw-*`` roles, just like the ``raw`` directive.

.. tip::

   In general, roles may be aliased like the ``sup`` role, which is a shortcut
   of a ``superscript``, by the overloading mechanism:

   .. code:: rst

      .. role:: strikethrough
      .. role:: strike(strikethrough)

      I do :strike:`not` like reStructuredText.

   If it is an alias to an already existing built-in role, then it is fine to
   have only one style rule for the long name. However, when it is an alias to a
   completely new role from the |RST| perspective, then each role name must be
   covered in styles:

   .. code:: css

      .strikethrough, .strike {
        text-decoration: line-through;
      }

Custom Roles via Programming
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

TODO



Glossary
========

|RST| uses officially the following terminology for markup syntax:

Citations
   `Footnotes`_ with alphanumeric characters plus hyphens, underscores and
   periods instead of numbered indexes, e.g. ``[label123]_``.

   Citations are rarely used, footnotes are much more prefered.
Doctest Blocks
   `Code Samples`_ with interactive Python interpreter.
Inline Markup
   `Text Styles`_ plus markup inside paragraphs, like `Hyperlinks`_,
   `Footnotes`_ and `Substitutions`_ without parts inside ``..`` constructs.
Literal Blocks
   `Code Samples`_
Transitions
   `Horizontal Lines`_



References
==========

* `Python Developer's Guide - Documenting Python`__
* `reStructuredText`__
* `reStructuredText - Directives`__
* `reStructuredText - Interpreted Text Roles`__
* `reStructuredText - Markup Specification`__
* `Sphinx - Getting Started`__
* `Sphinx - reStructuredText Primer`__
* `Wikipedia - reStructuredText`__
* `Wikipedia - Sphinx (documentation generator)`__

__ https://devguide.python.org/documenting/
__ reStructuredText_
__ http://docutils.sourceforge.net/docs/ref/rst/directives.html
__ http://docutils.sourceforge.net/docs/ref/rst/roles.html
__ http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html
__ https://www.sphinx-doc.org/en/master/usage/quickstart.html
__ http://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html
__ https://en.wikipedia.org/wiki/ReStructuredText
__ https://en.wikipedia.org/wiki/Sphinx_(documentation_generator)

--------------------------------------------------------------------------------

.. rubric:: Footnotes

.. [#] Special ``index.rst`` files which serves as a welcoming page with a table
   of contents.
.. [#] Body elements are markup inside sections (paragraphs, lists, tables
   etc.).
.. [#] PEPs_ are documents about enhancing the Python language (such as style
   guides, syntax, evaluations, protocols, plans) reviewed by the Python's
   `Steering Council`_.
.. [#] RFCs_ are documents about Internet standards (such as specifications,
   formats or protocols) ratified by the IETF_ community.

.. _IETF: https://www.ietf.org/about/who/
.. _PEPs: https://www.python.org/dev/peps/
.. _RFCs: https://tools.ietf.org/rfc/index
.. _Steering Council: https://www.python.org/dev/peps/pep-0013/#current-steering-council

.. |RST| replace:: reStructuredText
