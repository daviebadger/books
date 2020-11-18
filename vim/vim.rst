Glossary
========

buffer
   Loaded file content in memory. Empty buffers may be created.
buffer line
   A real line stored in a buffer.
logical line
   Folded buffer lines as a single logical line, usually with a summary of
   folded lines.
screen
   The whole painted area including a tab line, windows, a status line, and a
   command line.
screen line
   Window lines plus a tab line, a status line, a and command line.
window
   A view on a buffer. One buffer may be opened in multiple windows.
window line
   A mix of buffer and logical lines, plus wrapped lines (one window line may
   contain several screen lines), and placeholder lines rendered with ``~``.
