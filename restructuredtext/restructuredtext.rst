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

.. contents::

.. sectnum::
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

Horizontal lines, respectively transitions are at least four same consecutive
punctuation characters (usually a hyphen), which are surrounded by a blank line
around:

.. code:: rst

   This is a paragraph.

   ----

   This is a completely different paragraph.

.. note::

   The purpose of transitions is to signal a change in a subject between
   paragraphs, and thus it is not possible to use them at the start or the end
   of a section.


Substitutions
-------------

Substitutions are usually word shortcuts without spaces surrounded by vertical
bars and used inline in text. Spaces are allowed, but cannot be used as the
first or the last character in substitution references:

.. code:: rst

   |RST| is really long to type, so it is better to use a word shortcut via
   substitutions.

These marked substitution references will be substituted with a text declared in
substitution definitions with the help of directives (will be covered in detail
later) during a document conversion to other output formats:

.. code:: rst

   .. |RST| replace:: reStructuredText

Substitution definitions may be defined either before substitution references or
after them. The latter is a better choice because they may be organized at the
end of a section or even better at the end of a document after footnotes and
hyperlink targets.

.. note::

   If a substitution reference is placed inside a word, then it must be wrapped
   with escaped spaces around or else it will not be replaced:

   .. code:: rst

      Thisis\ |one|\ word

      .. |one| replace:: single

.. tip::

   Substitution references may be combined with hyperlink references:

   .. code:: rst

      |RST|_ is really long to type, so it is better to use a word shortcut via
      substitutions.

      .. |RST| replace:: reStructuredText
      .. _RST: http://docutils.sourceforge.net/rst.html



Directives
==========

Directives are the first standardized way of the extension mechanism in |RST|
how to extend block markup. By directives is possible to better structure
documents, add metadata or advanced body elements or load and transform data
stored in other documents and files.

The syntax of directives consists of two periods followed by a space and a
directive name without whitespaces immediately followed by two colons on a
separate line. Directives may further contain arguments, options like field
lists or body elements after a blank line:

.. code:: rst

   .. directive-name:: optional-directive-arguments
      :optional-directive-option: optional-directive-option-value

      optional-directive-body-elements

Some examples of using directives in practice:

#. a directive without arguments, options and body elements:

   .. code:: rst

      .. contents::

#. a directive with an argument:

   .. code:: rst

      .. include:: path/to/file

#. a directive with an argument and an option without a value (interpreted as
   a boolean flag, where if the option is present, then it is enabled, else
   disabled):

   .. code:: rst

      .. include:: path/to/file
         :literal:

#. a directive with an argument and an option with a value:

   .. code:: rst

      .. image:: path/to/image
         :alt: Alternate text description

#. a directive with an argument, an option with a value and a body element:

   .. code:: rst

      .. figure:: path/to/image
         :scale: 50 %

         Image title rendered below the image

#. a directive with a body element:

   .. code:: rst

      .. tip::

         This tip helps you save your money.

.. topic:: Common Directive Options

   Most directives, notably who add new content to a document, support these two
   directive options:

   * ``class``

     * add one or more HTML class attributes separated by a space to a
       directive, which may be further styled via CSS, if output of a
       document will be HTML:

       .. code:: rst

          .. image:: path/to/image
             :class: rounded trasparent

   * ``name``

     * add a human-redable name to a directive, which may be further used as a
       hyperlink target (the name must be unique across a document otherwise RST
       parser raises an error):

       .. code:: rst

          See below `My picture`_:

          .. image:: path/to/image
             :name: My picture



Built-In Directives
-------------------

|RST| has a lot of built-in directives. Most of them are curated in these
thematic groups:

* images
* tables
* substitutions
* body elements
* admonitions
* documents
* HTML


Image Directives
^^^^^^^^^^^^^^^^

Images are not a part of markup by design, because directives provide better
power in the sense of potential configuration. There are two image directives:

* ``image``
* ``figure``

The two have common directive options:

* ``alt``

  * an alternate text which is displayed when the image is not still rendered
    or cannot be rendered or when it is read by an impaired user

* ``width``

  * new width in pixels for the image if the original width is unwanted

* ``height``

  * new height in pixels for the image if the original height is unwanted

* ``scale``

  * new proportional scale in percentages for the image if the original size is
    unwanted (default is ``100 %``)

* ``align``

  * align the image in the center using the ``center`` value (default is
    unaligned)

* ``target``

  * add a hyperlink target to the image and make it clickable

.. note::

   It is also possible to align an image ``left`` or ``right``, but it will
   change text flow around (make it float) which may not be desired.

Image Directive
"""""""""""""""

Add an image:

#. from a local filesystem using either an absolute or a relative (preferred)
   path:

   .. code:: rst

      .. image:: path/to/image.png

#. from a remote location (must be a valid URL address):

   .. code:: rst

      .. image:: www.example.com/image.jpg

.. note::

   The ``image`` directive also can be used in substitutions:

   .. code:: rst

      |img|

      .. |img| image:: path/to/image.jpeg

   However, it is better to use only text-replacing substitution directives.

Figure Directive
""""""""""""""""

Add an image with a caption, though it is optional:

.. code:: rst

   .. figure:: path/to/image.png

      Caption for the image.

The ``figure`` directive supports two extra options:

* ``figwidth``

  * width of an image and a caption in total (pixels)

* ``figclass``

  * add HTML class attributes to a figure as a whole (the ``class`` option
    adds classes only to an image)

.. hint::

   The ``figure`` directive supports any body elements after a caption, which
   are considered as a legend for an image:

   .. code:: rst

      .. figure:: path/to/image.svg

         Caption for the image.

         Legend:

         * a is a
         * b is b
         * c is c

   it is okay only, if the figure is not aligned otherwise it may break the
   legend visually. When the figure needs to be aligned, a legend should be
   placed after the directive as new block markup:

   .. code:: rst

      .. figure:: path/to/image.svg
         :align: center
         :name: img

         Caption for the image.

      Legend for the `img`_ figure:

      ...

.. note::

   In case of the ``figure`` directive, the ``align`` option aligns both an
   image and a caption.


Table Directives
^^^^^^^^^^^^^^^^

Directives for creating advanced and yet easy-to-design tables. There are three
table directives:

* ``table``
* ``list-table``
* ``csv-table``

Each of these tables supports table titles, which are optional to use. The same
goes for base table options:

* ``align``

  * align horizontally a table ``left`` (default), ``center`` or ``right``

* ``widths``

  * set column widths to ``auto`` mode according to text in columns (by default
    ``csv-table`` and ``list-table`` tables have column-equal widths whereas
    ``table`` tables not)

Table Directive
"""""""""""""""

Wrap either a simple or a grid table with an optional title or possible
directive options, as mentioned in the introduction to table directives:

.. code:: rst

   .. table:: Users

      =========  ========  ======  ===
      Firstname  Lastname  Gender  Age
      =========  ========  ======  ===
      Davie      Badger    Male    24
      Jacob      Badger    Male    19
      =========  ========  ======  ===

List-table Directive
""""""""""""""""""""

Add a list-like table using a bulleted list where each sublist must contain the
same number of list items:

#. without a table header:

   .. code:: rst

      .. list-table:: Users

         * - Davie
           - Badger
           - Male
           - 24
         * - Jacob
           - Badger
           - Male
           - 19

#. with a table header in the first row of a table:

   .. code:: rst

      .. list-table:: Users
         :header-rows: 1

         * - Firstname
           - Lastname
           - Gender
           - Age
         * - Davie
           - Badger
           - Male
           - 24
         * - Jacob
           - Badger
           - Male
           - 19

#. with a table header in the first column of a table:

   .. code:: rst

      .. list-table::
         :stub-columns: 1

         * - Name
           - reStructuredText
         * - Shortcut
           - rst
         * - Parser
           - Docutils

.. note::

   In list-like tables is not possible to span columns or rows at all.

.. tip::

   If a table cell cannot contain a sensible value, then it may be left empty
   to meet the ``list-table`` directive requirements:

   .. code:: rst

      .. list-table:: Example with an empty cell

         * - A
           - B
           - C
         * - 1
           -
           - 3

Csv-table Directive
"""""""""""""""""""

Add a table using CSV_ format:

#. embedded CSV table without a table header:

   .. code:: rst

      .. csv-table:: Users

         "David", "Badger", "Male", 24
         "Jacob", "Badger", "Male", 19

#. embedded CSV table with a table header:

   .. code:: rst

      .. csv-table:: Users
         :header: "Firstname", "Lastname", "Gender", "Age"

         "David", "Badger", "Male", 24
         "Jacob", "Badger", "Male", 19

#. external CSV table without a table header:

   .. code:: rst

      .. csv-table::
         :file: data.csv

      .. csv-table::
         :url: www.example.com/data.csv

#. external CSV table with a table header in the first row of a table:

   .. code:: rst

      .. csv-table::
         :file: data.csv
         :header-rows: 1

      .. csv-table::
         :url: www.example.com/data.csv
         :header-rows: 1

#. external CSV table with a table header in the first column of a table:

   .. code:: rst

      .. csv-table::
         :file: data.csv
         :stub-columns: 1

      .. csv-table::
         :url: www.example.com/data.csv
         :stub-columns: 1

The ``csv-table`` directive supports these options:

* ``delim``

  * a character for separating column values (Unicode characters are also
    supported), which is by default ``,``

* ``quote``

  * a quote for multi-word (string) values, where the ``delim`` character does
    not separate a value (default is ``"``)

* ``escape``

  * an escape character for the ``quote`` character used inside a string value
    (default ``""``)

.. note::

   Unlike strict list-style tables, the |RST| parser doest not strictly check,
   whether each row contain the same number of columns or not.

.. _CSV: https://en.wikipedia.org/wiki/Comma-separated_values


Substitution Directives
^^^^^^^^^^^^^^^^^^^^^^^

Special directives only for substitution definitions, which use a slightly
different syntax:

.. code:: rst

   .. |substitution| directive-name:: substituted-text

There are three text-replacing substitution directives:

#. ``replace``
#. ``unicode``
#. ``date``

.. note::

   The ``unicode`` directive is the only substitution directive which may
   contain a comment after a substituted text:

   .. code:: rst

      .. |substitution| unicode:: substituted-text .. comment

Replace Directive
"""""""""""""""""

Substitute a substitution for a text:

.. code:: rst

   .. |RST| replace:: reStructuredText

   |RST| is too long to type.

Unicode Directive
"""""""""""""""""

Substitute a substitution for a Unicode character using its hexadecimal value
with a prefix, such as ``0x`` or ``U+``:

#. substituting without trims (no trimming whitespace around):

   .. code:: rst

      .. |copy| unicode:: 0xA9 .. copyright sign

      Copyright |copy| Davie Badger 2019.

#. substituting with a left whitespace trim (``:ltrim:``) or a right whitespace
   trim (``:rtrim``) or both the left and the right trims (``:trim:``):

   .. code:: rst

      .. |TM| unicode:: U+2122
         :ltrim:

      Davie Badger |TM| will be rendered as ``Davie Badger^TM``.

.. attention::

   Comments for the ``unicode`` directive are optional. Nevertheless, it is
   better to use them for description, if a substitution is not
   self-descriptive.

Date Directive
""""""""""""""

Substitute a substitution for a date(time) using the same format string like for
the `time.strftime`_ function in Python:

.. code:: rst

   .. |date| date::
   .. |time| date:: %H:%M:%S

   Last update: |date| at |time|

.. note::

   The default format string is ``%Y-%m-%d`` (`ISO 8601`_ date).

.. _time.strftime: https://docs.python.org/3/library/time.html#time.strftime
.. _ISO 8601: https://www.iso.org/iso-8601-date-and-time-format.html


Body Element Directives
^^^^^^^^^^^^^^^^^^^^^^^

Directives which extend a collection of already existing body elements. There
are five body element directives:

* ``code``
* ``math``
* ``rubric``
* ``topic``
* ``highlights``

Code Directive
""""""""""""""

Add a code sample from a specific language with syntax highlighting:

.. code:: rst

   .. code:: py

      print("Hello World")

.. hint::

   Sphinx provides more powerful directives for code samples with a lot of
   features via directive options than this one.

.. note::

   Code examples are highlighted via Pygments_ syntax highlighter unless |RST|
   documents are parsed by a different parser (not using Docutils at all).

   List of supported languages (so-called lexers) is in the
   `Pygments documentation`_.

.. _Pygments: http://pygments.org/
.. _Pygments documentation: http://pygments.org/docs/lexers/

Math Directive
""""""""""""""

Add a mathematical formula using LaTeX_ math syntax, which also supports AMS_
extensions:

.. code:: rst

   .. math::

      f(x) = x^2

.. _AMS: http://www.ams.org/publications/authors/tex/amslatex

Rubric Directive
""""""""""""""""

Add an informal heading, which will not be a part of an official document
structure and thus not visible in a potential table of contents:

.. code::

   .. rubric:: Footnotes

   .. [#] text

Topic Directive
"""""""""""""""

Add a topic container with a title to develop a self-contained idea without a
need to create another (sub)section:

.. code:: rst

   Section Title
   =============

   ...

   .. topic:: Idea

      Blah blah blah

Highlights Directive
""""""""""""""""""""

Add a summary of a whole document or a section:

.. code:: rst

   .. highlights::

      A summary of the story:

      * a
      * b
      * c


Admonition Directives
^^^^^^^^^^^^^^^^^^^^^

Admonitions are specially styled semantic text with additional information to
readers. |RST| has namely the following admonitions:

* ``attention``
* ``caution``
* ``danger``
* ``hint``
* ``important``
* ``note``
* ``tip``
* ``warning``

Except for these built-in admonitions, there exists an option to create a custom
directive via an ``admonition`` directive, if needed.

Admonition Directive
""""""""""""""""""""

Add a custom admonition with the given title to a text:

.. code:: rst

   .. admonition:: See also

      www.example.com for more examples.

.. tip::

   Custom admonitions are easily accessible via their titles, which are
   specially parsed and used as HTML class attributes. The previous example
   would have an ``admonition-see-also`` class name.

   The parsing mechanism consists of:

   #. lowercasing all characters
   #. replacing non-alphanumeric characters with hyphens
   #. prefixing the parsed name with ``admonition-``

Attention Directive
"""""""""""""""""""

Add attentive information to a text (a user should notice something):

.. code:: rst

   .. attention::

      The previous example is not possible to create via inline literal markup.

Caution Directive
"""""""""""""""""

Add cautious information to a text (a user should be careful with something):

.. code:: rst

   .. caution::

      Use wisely the overloaded ``raw-*`` roles.

Danger Directive
""""""""""""""""

Add dangerous information to a text (a user should not do something at all):

.. code:: rst

   .. danger::

      Do not try this at home!

Hint Directive
""""""""""""""

Add a hint to a text (an indirect help for a user):

.. code:: rst

   .. hint::

      Look at already existing roles.

Important Directive
"""""""""""""""""""

Add important information to a text:

.. code:: rst

   .. important::

      Be consistent with heading levels through a document.

Note Directive
""""""""""""""

Add a note to a text:

.. code:: rst

   .. note::

      Code samples using ``::`` markup are not highlighted at all.

Tip Directive
"""""""""""""

Add a tip to a text (a direct help for a user):

.. code:: rst

   .. tip::

      Subscripts are ideal candidates for substitutions.

Warning Directive
"""""""""""""""""

Add a warning to a text (a user should be warned about a possible problem):

.. code:: rst

   .. warning::

      Do not exceed the recommended daily dose.


Document Directives
^^^^^^^^^^^^^^^^^^^

Directives about documents as a whole.

Contents Directive
""""""""""""""""""

Generate a table of contents (TOC) from sections and their nested subsections
in a document (a document title and a subtitle are ignored):

#. using a default title for the table of contents:

   .. code:: rst

      .. contents::

      ----

      Contents

      * Section A
        * Subsection AA
          * Subsubsection AAA
      * Section B

#. using a custom title for the table of contents:

   .. code:: rst

      .. contents:: Table of Contents

      ----

      Table of Contents

      * Section A
        * Subsection AA
          * Subsubsection AAA
      * Section B

#. limiting section levels rendered in the table of contents:

   .. code:: rst

      .. contents::
         :depth: 2

      ----

      Contents

      * Section A
        * Subsection AA
      * Section B

.. tip::

   In a rendered RST document with a table of contents, entries in the TOC lead
   to sections in a document, whereas the sections in the document lead back to
   the entries in the TOC after a click on a section title.

Sectnum Directive
"""""""""""""""""

Automatically number section titles in a document (including those in a table
of content):

#. without any directive options:

   .. code:: rst

      .. sectnum::

      ----

      * 1 Section A
      * 1.1 Subsection AA
      * 1.1.1 Subsubsection AAA
      * 2 Section B

#. with a suffix at the end of each number:

   .. code:: rst

      .. sectnum::
         :suffix: .

      ----

      * 1. Section A
      * 1.1. Subsection AA
      * 1.1.1. Subsubsection AAA
      * 2. Section B

#. with limited section levels to be numbered:

   .. code:: rst

      .. sectnum::
         :depth: 2

      ----

      * 1 Section A
      * 1.1 Subsection AA
      * 2 Section B

Include Directive
"""""""""""""""""

Load text from a file using an absolute or a relative (preferred) path to the
given place, where is the ``include`` directive located:

#. a |RST| document:

   .. code:: rst

      .. include:: path/to/file.rst

#. a file rendered as literal code without syntax highlighting:

   .. code:: rst

      .. include:: test.py
         :literal:

#. a file rendered as code with syntax highlighting (language code is needed):

   .. code:: rst

      .. include:: test.py
         :code: py

.. caution::

   When loading a |RST| file, if the ``include`` directive is used at the left
   edge, then section levels in the loaded file must match those in the current
   document's context otherwise the |RST| parser raises an error.

   The parser also raises an error, when the ``include`` directive with a |RST|
   file is indented inside a body element. In this case, the loaded file cannot
   contain sections at all.

   Overall, be aware of what you are loading.

.. tip::

   |RST| contains Unicode character sets with substitution definitions, which
   may be loaded and used for substitutions in very technical documents instead
   of writing custom ones:

   .. code:: rst

      .. include:: <isonum.txt>

      Copyright |copy| Davie Badger 2019.

   Take in mind that these substitution definitions cannot be overridden in the
   sense of substituting for one way and later the other way in a document.
   There may exist only one unique substitution definition.

   All the sets are listed here__.

__ http://docutils.sourceforge.net/docs/ref/rst/definitions.html#character-entity-sets

Raw Directive
"""""""""""""

Bypass parsing text for the given output formats separated by a space:

#. a text inside the ``raw`` directive:

   .. code:: rst

      .. raw:: html

         <iframe id="video-player" width="200" height="200" src="www"></iframe>

#. a text in a local file accessible via an absolute or a relative (preferred)
   path:

   .. code:: rst

      .. raw:: html
         :file: index.html

#. a text accessible via a URL address:

   .. code:: rst

      .. raw:: html
         :url: www.example.com/file.html

.. caution::

   Use wisely the ``raw`` directive, because |RST| will not parse its content
   and the content will be placed as it is. It may contain malicious data.


HTML Directives
^^^^^^^^^^^^^^^

Special directives only for HTML output, namely:

* ``title``
* ``meta``
* ``class``

Title Directive
"""""""""""""""

Set a different HTML document title for a browser tab, which will be used
instead of a document title:

.. code:: rst

   **************
   Document Title
   **************

   .. title:: Alternative Document Title

Meta Directive
""""""""""""""

Add HTML meta tags, where a directive option represents ``name`` attribute and
directive content ``content`` attribute:

.. code:: rst

   .. meta::
      :author: Davie Badger
      :description: reStructuredText is a markup language used for documentation.

.. note::

   The previous code sample would be rendered in the HTML ``head`` tag as:

   .. code:: rst

      <meta name="author" content="Davie Badger">
      <meta name="description" content="reStructuredText is a markup language used for documentation.">

Class Directive
"""""""""""""""

Add HTML classes separated by a space right to the immediately following
non-comment element(s):

#. a single element outside of the ``class`` directive:

   .. code:: rst

      .. class:: heading color-red

      Section Title
      =============

#. multiple elements inside of the ``class`` directive:

   .. code:: rst

      .. class:: blink

         This paragraph has the "blink" class.

         This another paragraph also has the "blink" class.

.. note::

   If the ``class`` directive is intended to be used before block quotes, then
   a comment must be placed right after the ``class`` directive otherwise the
   block quotes will be misinterpreted as paragraphs inside the directive:

   .. code:: rst

      .. class:: block-quote
      ..

         This is a block quote.

.. tip::

   Before adding HTML classes to elements, try to convert a document to HTML
   first, and then inspect tags with attributes whether the tags already contain
   useful classes for styling or not.

.. warning::

   Although it is possible to use the ``class`` directive inside nested body
   elements, e.g. bulleted lists, it is better to use them only at the left
   edge of a line (unindented) to avoid some unexpected behavior:

   .. code:: rst

      .. note::

         This is a note.

         .. class:: cls

      Unfortunately, this paragraph has the "cls" class by mistake.



Custom Directives
-----------------

TODO

.. hint::

   Look at already existing directives, either in |RST| or in Sphinx, before
   creating new ones (do not reinvent the wheel).




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


Built-In Roles
--------------

|RST| has notably these built-in roles:

* ``literal``
* ``math``
* ``sub``
* ``sup``
* ``title``
* ``PEP``
* ``RFC``

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

   :title:`How to Title My Book` is the most selling book in the world.

.. note::

   The title role is the only role by default which may be used implicitly
   without specifying a role like :literal:`\`How to Title My Book\``. It is
   thanks to a ``default-role`` directive:

   .. code:: rst

      .. default-role:: title

      `How to Title My Book` == `title:`How to Title My Book`

   If the ``default-role`` directive is set differently, then it is not safe to
   use the title role implicitly. That is why it is always better to use roles
   explicitly.

PEP Role
^^^^^^^^

Create a link to a specific `PEP`_ (**P**\ ython **E**\ nhancement
**P**\ roposal) [#]_:

.. code:: rst

   See :PEP:`8` for Python style guide.

.. Attention::

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

.. Attention::

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

#. a dummy role only for styling purposes (the role is not interpreted however
   is intended to be styled via CSS):

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
.. _LaTeX: https://en.wikibooks.org/wiki/LaTeX/Mathematics
.. _PEPs: https://www.python.org/dev/peps/
.. _RFCs: https://tools.ietf.org/rfc/index
.. _Steering Council: https://www.python.org/dev/peps/pep-0013/#current-steering-council

.. |RST| replace:: reStructuredText
