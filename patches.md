# Patches Control

Track all patches submitted to emacs-devel and their statuses.

---

## markdown-ts-mode

### 1. Fix 'fill-paragraph' respecting list items, code blocks, and tables

'fill-paragraph' (M-q) was merging adjacent list items into a
single paragraph.  Uses tree-sitter to identify list items and
narrows to each item before filling.  Skips code blocks and tables.

- https://debbugs.gnu.org/cgi/bugreport.cgi?bug=80613
- Status: **Reviewing**

### 2. Dedicated faces, clickable links, and new fontification

Add dedicated 'markdown-ts-*' faces for all fontified elements so
every face is individually customizable.  Links and image descriptions
are clickable buttons.  New fontification for strikethrough, task
lists, autolinks, pipe tables, inline HTML, setext underlines, and
backslash escapes.  Markup hiding for delimiters and link destinations.

- https://debbugs.gnu.org/cgi/bugreport.cgi?bug=80625
- Status: **Waiting for Review**

### 3. Fix font-lock leaking in 'markdown-ts-mode'

Language modes' range settings (e.g., jsdoc from js-ts-mode,
Doxygen from c-ts-mode) created global parsers that leaked
font-lock rules into the entire Markdown buffer.

- Not yet submitted
- Status: **Not yet submitted**

### 4. Improve link handling in 'markdown-ts-mode'

Add support for reference links (full, collapsed, shortcut),
email autolinks, link reference definition fontification, and
parenthesis-style ordered list markers.

- Not yet submitted
- Status: **Not yet submitted**


## Eglot

### 1. Eldoc documentation rendering

Provides a way of switching renderers on eldoc to
markdown-ts-mode, so that LSP hover documentation is displayed
with proper markdown fontification instead of raw markup.

- https://debbugs.gnu.org/cgi/bugreport.cgi?bug=80127
- Status: Reviewing by Joao
