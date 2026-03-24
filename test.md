---
title		: The Official 'markdown-ts-mode.el' Feature Test File
author		: Rahul Martim Juliato
date		: 2026-03-18
version		: 0.1.0
parsers needed	: markdown, markdown-inline, yaml, toml, html, c, javascript, python, rust
---

<!-- You need all the above mentionated parsers installed to read this
     document as intended or faces might be funny.  If you find some
     strange colors, please check all of them are installed first. -->

<!-- TOML header version (swap with YAML above to test):
+++
title = "Feature Test File"
author = "Rahul Martim Juliato"
date = "2026-03-18"
parsers = "markdown, markdown-inline, yaml, toml, html, c, javascript, python, rust"
+++
-->

<!-- ============================================================ -->
<!-- 1. Block-Level - CommonMark                                  -->
<!-- ============================================================ -->

<!-- Document Structure: `document` root node handling -->
<!-- This entire file is a document root node. -->

<!-- Document Structure: `section` grouping -->
<!-- Each heading below starts a section; nested headings create nested sections. -->

<!-- ATX Headings: levels 1-6, markers # through ###### -->
# Heading Level 1
## Heading Level 2
### Heading Level 3
#### Heading Level 4
##### Heading Level 5
###### Heading Level 6

<!-- ATX Headings: closing hashes -->
## Heading with Closing Hashes ##

<!-- ATX Headings: content parsed via inline parser -->
## Heading with *emphasis* and **bold** and `code`

<!-- Setext Headings: level 1 (=== underline) -->
Setext Heading Level 1
=======================

<!-- Setext Headings: level 2 (--- underline) -->
Setext Heading Level 2
-----------------------

<!-- Setext Headings: setext underline fontification -->
<!-- The === and --- lines above should be fontified as delimiters. -->

<!-- Setext Headings: multi-line setext heading content -->
This is a multi-line
setext heading
==============

<!-- Paragraphs: paragraph recognition -->
This is a simple paragraph. It contains multiple sentences.
This sentence is on the next line but is part of the same paragraph.

Another paragraph separated by a blank line.

<!-- Thematic Breaks: ***, ---, ___ -->
***

---

___

<!-- Thematic Breaks: with spaces -->
* * *

- - -

_ _ _

<!-- Block Quotes: recognition and fontification -->
> This is a block quote.

<!-- Block Quotes: marker (>) fontification -->
> The > marker should be fontified as a delimiter.

<!-- Block Quotes: nested block quotes -->
> Outer quote.
> > Inner nested quote.
> > > Triple nested quote.

<!-- Block Quotes: containing all block types -->
> ## Heading inside a block quote
>
> Paragraph inside a block quote.
>
> - List item inside a block quote.
>
> ```python
>    print("code block inside a quote")
> ```
>
>     indented code inside a block quote
>
> > Nested quote inside a quote.
>
> ---

<!-- Lists: unordered list marker: minus (-) -->
- Item with minus marker
- Another minus item

<!-- Lists: unordered list marker: plus (+) -->
+ Item with plus marker
+ Another plus item

<!-- Lists: unordered list marker: star (*) -->
* Item with star marker
* Another star item

<!-- Lists: ordered list marker: dot (1.) -->
1. First item
2. Second item
3. Third item

<!-- Lists: ordered list marker: parenthesis (1)) -->
1) First item with paren
2) Second item with paren
3) Third item with paren

<!-- Lists: ordered list starting from arbitrary number -->
42. Starting from forty-two
43. Forty-three
44. Forty-four

<!-- Lists: list item nesting via indentation -->
- Top level item
  - Nested item level 2
    - Nested item level 3
      - Nested item level 4

1. Ordered top
   1. Ordered nested
      1. Ordered deeply nested

- Mixed top
  1. Ordered inside unordered
     - Unordered inside ordered inside unordered

<!-- Lists: loose vs tight list distinction -->
<!-- Tight list (no blank lines between items): -->
- Tight item one
- Tight item two
- Tight item three

<!-- Loose list (blank lines between items): -->
- Loose item one

- Loose item two

- Loose item three

<!-- Lists: list items containing all block types -->
- Item with a paragraph.

  This is a continuation paragraph inside the same list item.

- Item with a block quote:

  > Quoted text inside a list item.

- Item with a code block:

  ```python
  def hello():
      print("inside a list item")
  ```

- Item with a thematic break below:

  ---

<!-- Fenced Code Blocks: backtick -->
```
plain fenced code block with backticks
no language specified
```

<!-- Fenced Code Blocks: tilde -->
~~~
plain fenced code block with tildes
no language specified
~~~

<!-- Fenced Code Blocks: info_string / language extraction -->
```python
def greet(name):
    return f"Hello, {name}!"
```

<!-- Fenced Code Blocks: code_fence_content fontification -->

```javascript
const x = 42;
console.log(`The answer is ${x}`);

```

<!-- Fenced Code Blocks: language-specific fontification -->
```c
#include <stdio.h>
int main(void) {
    printf("Hello, world!\n");
    return 0;
}
```

<!-- Fenced Code Blocks: language-specific indentation -->
```rust
fn main() {
    let x = vec![1, 2, 3];
    for item in &x {
	println!("{}", item);
    }
}
```

<!-- Fenced Code Blocks: non-tree-sitter mode fontification (elisp) -->
```elisp
(defun hello (name)
  "Greet the user by NAME."
  (message "Hello, %s!" name))

(hello "friend")
```

<!-- Fenced Code Blocks: opening/closing fence delimiter fontification -->
````markdown
You can use more backticks for the fence (4 here).
The opening and closing delimiters should be fontified.
````

<!-- Indented Code Blocks: recognition (4+ spaces) -->

    This is an indented code block.
    It requires 4 spaces of indentation.
    Each line is part of the same block.

<!-- Indented Code Blocks: fontification -->

    int x = 10;
    int y = 20;
    printf("%d\n", x + y);

<!-- HTML Blocks: type 1 (<pre>, <script>, <style>, <textarea>) -->
<pre>
This is preformatted text in an HTML block type 1.
</pre>

<script>
var x = 42;
</script>

<style>
body { color: red; }
</style>

<textarea>
Some text area content.
</textarea>

<!-- HTML Blocks: type 2 (comments) -->
<!-- This is an HTML comment block (type 2). -->

<!--
Multi-line
HTML comment
block.
-->

<!-- HTML Blocks: type 3 (<? processing instructions) -->
<?xml version="1.0" encoding="UTF-8"?>

<!-- HTML Blocks: type 4 (<! declarations) -->
<!-- BUG: uppercase <!DOCTYPE html> swallows entire document (parser bug,
     https://github.com/tree-sitter-grammars/tree-sitter-markdown/issues/233).
     Lowercase doesn't match type 4 start condition (needs uppercase after <!)
     so it parses differently and doesn't break the rest of the file. -->
<!doctype html>

<!-- HTML Blocks: type 5 (<![CDATA[) -->
<!-- NOTE: CDATA is valid CommonMark (HTML block type 5) but not valid
     HTML5 outside SVG/MathML.  The markdown block parser handles it
     correctly (html_block), but the embedded HTML parser produces
     (ERROR (UNEXPECTED '[')) - it doesn't recognize CDATA as valid
     markup.  No fontification is applied as a result.  Not a bug in
     markdown-ts-mode. -->
<![CDATA[
This is CDATA content in an HTML block.
]]>

<!-- HTML Blocks: standalone HTML without fence (html_block) -->
<p class="foo">This is a standalone HTML paragraph outside any fence.</p>

<nav id="main-nav">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>

<!-- HTML Blocks: type 6 (block-level HTML elements) -->
<div>
  <p>This is a block-level HTML element.</p>
</div>

<table>
  <tr><td>Cell</td></tr>
</table>

<!-- HTML Blocks: type 7 (complete open/close tag on its own line) -->
<custom-element>
  Custom element content here.
</custom-element>

<!-- Link Reference Definitions: recognition -->
[example]: https://www.example.com

<!-- Link Reference Definitions: link_label handling -->
[Example Label]: https://www.example.com

<!-- Link Reference Definitions: link_destination (bare URL) -->
[bare-url]: https://www.example.com/path?query=1

<!-- Link Reference Definitions: link_destination (<angle-bracketed>) -->
<!-- [angle-url]: <https://www.example.com/path with spaces> -->

<!-- Link Reference Definitions: link_title ("double") -->
[with-double-title]: https://www.example.com "Double quoted title"

<!-- Link Reference Definitions: link_title ('single') -->
<!-- [with-single-title]: https://www.example.com 'Single quoted title' -->

<!-- Link Reference Definitions: link_title ((parenthesized)) -->
[with-paren-title]: https://www.example.com (Parenthesized title)

<!-- Link Reference Definitions: multi-line -->
[multi-line-def]:
  https://www.example.com/very/long/path
  "Title on next line"


<!-- ============================================================ -->
<!-- 2. Inline-Level - CommonMark                                 -->
<!-- ============================================================ -->

<!-- Emphasis (Italic): star emphasis -->
This is *star emphasis* in a sentence.

<!-- Emphasis (Italic): underscore emphasis -->
This is _underscore emphasis_ in a sentence.

<!-- Emphasis (Italic): delimiter fontification / hiding -->
The *delimiters* around this word should be fontified and hideable.

<!-- Emphasis (Italic): nested emphasis -->
This has *nested _emphasis_ inside* star emphasis.

<!-- Strong Emphasis (Bold): star strong emphasis -->
This is **star bold** in a sentence.

<!-- Strong Emphasis (Bold): underscore strong emphasis -->
This is __underscore bold__ in a sentence.

<!-- Strong Emphasis (Bold): delimiter fontification / hiding -->
The **delimiters** around this word should be fontified and hideable.

<!-- Strong Emphasis (Bold): nested strong emphasis -->
This has **nested __strong__ inside** star bold.

And ***bold and italic together*** using three stars.

<!-- Code Spans: single backtick -->
This is `inline code` in a sentence.

<!-- Code Spans: multi-backtick -->
This is ``code with a ` backtick inside`` using double backticks.

Use double backticks to include a literal `` ` `` backtick in code.

<!-- Code Spans: delimiter fontification -->
The backticks around `this code` should be fontified as delimiters.

<!-- Code Spans: code span face -->
All of `this text` should use the code span face.

<!-- Links: inline link -->
[Click here](https://www.example.com "Example Site")

<!-- Links: inline link without title -->
[Click here](https://www.example.com)

<!-- Links: full reference link -->
[Click here][example]

<!-- Links: collapsed reference link -->
[example][]

<!-- Links: shortcut link -->
[example]

<!-- Links: link text fontification -->
The text [inside these brackets](https://example.com) should be fontified.

<!-- Links: link destination fontification -->
[link](https://this-url-should-be-fontified.com)

<!-- Links: link title fontification -->
[link](https://example.com "This title should be fontified")

<!-- Links: clickable link buttons (browse-url) -->
[Open in browser](https://www.gnu.org)

<!-- Links: file path links (find-file) -->
[Open local file](./README.md)

<!-- Links: link destination hiding when markup is hidden -->
[Only this text visible when markup hidden](https://hidden-url.com)

<!-- Images: inline image -->
![Alt text for image](https://www.example.com/image.png "Image title")

<!-- Images: inline image without title -->
![Alt text](./local-image.png)

<!-- Images: full reference image -->
![Alt text][example]

<!-- Images: collapsed reference image -->
![example][]

<!-- Images: shortcut reference image -->
![example]

<!-- Images: image description fontification -->
![This description should be fontified](https://example.com/img.png)

<!-- Images: inline image preview -->
![Preview this image](https://www.example.com/photo.jpg)

<!-- Autolinks: URI autolink -->
Visit <https://www.gnu.org> for more info.

<!-- Autolinks: email autolink -->
Contact us at <user@example.com> for support.

<!-- Autolinks: fontification as clickable button -->
The autolink <https://www.example.com> should be clickable.

<!-- Autolinks: angle bracket hiding when markup is hidden -->
When markup is hidden, <https://www.example.com> should show without < >.

<!-- Naked URLs: bare URLs without angle brackets -->
<!-- These are not handled by the grammar; goto-address-mode is a candidate. -->
Visit https://www.gnu.org for more info.

Here is a URL in the middle of text https://www.example.com/path?query=1&foo=bar and text continues.

Also email addresses without angle brackets: user@example.com should ideally be recognized.

<!-- Inline HTML: open tags with attributes -->
This is <span class="highlight" id="test"> inline HTML with attributes.

<!-- Inline HTML: closing tags -->
Some text </span> with a closing tag.

<!-- Inline HTML: self-closing tags -->
A line break <br /> using self-closing tag.

<!-- Inline HTML: inline HTML comments -->
This has <!-- an inline comment --> in the middle.

<!-- Inline HTML: inline processing instructions -->
Here is <?php echo "hello"; ?> a processing instruction inline.

<!-- Inline HTML: inline declarations -->
Here is <!ENTITY foo "bar"> an inline declaration.

<!-- Inline HTML: inline CDATA sections -->
Here is <![CDATA[some raw data]]> an inline CDATA section.

<!-- Hard Line Breaks: backslash before newline -->
This line has a hard break\
and continues on the next line.

<!-- Hard Line Breaks: trailing spaces (2+ spaces before newline) -->
This line has a hard break with trailing spaces
and continues on the next line.

<!-- Backslash Escapes: all ASCII punctuation -->
\! \" \# \$ \% \& \' \( \) \* \+ \, \- \. \/
\: \; \< \= \> \? \@
\[ \\ \] \^ \_ \`
\{ \| \} \~

<!-- Backslash Escapes: backslash hiding when markup is hidden -->
This shows \*literal asterisks\* not emphasis.

<!-- Entity References: named HTML entities -->
&amp; &lt; &gt; &quot; &apos; &copy; &reg; &trade; &nbsp;

<!-- Entity References: decimal numeric character references -->
&#65; &#66; &#67; &#8212; &#123; &#125;

<!-- Entity References: hexadecimal numeric character references -->
&#x41; &#x42; &#x43; &#x1F4A9; &#x2603; &#x2764;


<!-- ============================================================ -->
<!-- 3. GFM (GitHub Flavored Markdown) Extensions                 -->
<!-- ============================================================ -->

<!-- Strikethrough -->
This has ~~strikethrough text~~ in it.

<!-- Strikethrough: delimiter fontification / hiding -->
The ~~tildes~~ should be fontified as delimiters and hideable.

<!-- Strikethrough: face (:strike-through t) -->
~~This entire phrase should have a line through it.~~

<!-- Pipe Tables: recognition -->
| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Cell 1   | Cell 2   | Cell 3   |
| Cell 4   | Cell 5   | Cell 6   |

<!-- Pipe Tables: header row fontification -->
| This Header | Should Be Bold |
|-------------|----------------|
| data        | data           |

<!-- Pipe Tables: delimiter row recognition -->
| H1    | H2    |
|-------|-------|
| above | row   |

<!-- Pipe Tables: data row fontification -->
| H1             | H2                  |
|----------------+---------------------|
| This data cell | should be fontified |
|                |                     |

<!-- Pipe Tables: cell and delimiter cell fontification -->
| Header |
|--------|
| Cell   |

<!-- Pipe Tables: left alignment marker -->
| Left Aligned |
|:-------------|
| text         |

<!-- Pipe Tables: right alignment marker -->
| Right Aligned |
|--------------:|
|          text |

<!-- Pipe Tables: center alignment marker -->
| Centered    |
|:-----------:|
|   text      |

<!-- Pipe Tables: all alignment types together -->
| Left    | Center  | Right   | Default |
|:--------|:-------:|--------:|---------|
| L text  | C text  | R text  | D text  |

<!-- Pipe Tables: escaped pipes within cells -->
| Header           | Another     |
|------------------|-------------|
| cell with \| bar | normal cell |

<!-- Pipe Tables: table editing (create, align, add/remove rows/columns) -->
<!-- This is an editing feature, tested interactively. -->
| Edit Me | Add Cols | Remove Rows |
|---------|----------|-------------|
| data1   | data2    | data3       |

<!-- Task Lists: checked marker ([x] / [X]) -->
- [x] This task is done (lowercase x)
- [X] This task is also done (uppercase X)

<!-- Task Lists: unchecked marker ([ ]) -->
- [ ] This task is not done

<!-- Task Lists: checkbox fontification -->
- [x] Checked should be fontified
- [ ] Unchecked should be fontified

<!-- Task Lists: checkbox overlay (toggle interaction) -->
- [ ] Click to toggle this checkbox

<!-- Task Lists: nested task lists -->
- [ ] Parent task
  - [x] Child task completed
  - [ ] Child task pending
    - [x] Grandchild task completed


<!-- ============================================================ -->
<!-- 4. Other Extensions (Non-GFM)                                -->
<!-- ============================================================ -->

<!-- YAML Front Matter: see top of this file (--- delimited) -->
<!-- The YAML block at the top tests both recognition and fontification. -->

<!-- TOML Front Matter: would need a separate test file with +++ -->
<!-- Example (cannot coexist with YAML front matter):              -->
<!-- +++                                                           -->
<!-- title = "Test"                                                -->
<!-- date = 2026-03-18                                             -->
<!-- +++                                                           -->

<!-- LaTeX / Math: inline math -->
The equation $E = mc^2$ is famous.

<!-- LaTeX / Math: display math -->
$$
\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
$$

<!-- LaTeX / Math: delimiter fontification -->
The $delimiters$ around math should be fontified.

<!-- LaTeX / Math: content handling (no markdown processing inside) -->
This $*is not emphasis* inside math$ should be literal.

<!-- Wiki Links: basic -->
See [[SomePage]] for more information.

<!-- Wiki Links: with display text -->
See [[SomePage|click here]] for more information.

<!-- Wiki Links: fragment identifiers -->
See [[SomePage#section-two]] for that specific section.

<!-- Tags: hashtag-style -->
This note is about #emacs and #markdown and #tree-sitter.

<!-- Tags: tag fontification -->
The tag #gnu-emacs should be fontified as a tag.


<!-- ============================================================ -->
<!-- 5. Editing / Mode Features                                   -->
<!-- ============================================================ -->

<!-- Filling: fill-paragraph respecting list items -->
- This is a very long list item that should be filled properly when you press M-q and it should not merge with the next list item below it.
- This is a separate list item that should remain separate after filling the item above.

<!-- Filling: fill-paragraph skipping code blocks -->
```
This code block content should never be reflowed by fill-paragraph no matter how long the lines are in here because code formatting matters.
```

<!-- Filling: fill-paragraph skipping tables -->
| Column 1 with long text | Column 2 with long text | Column 3 with long text |
|-------------------------|-------------------------|-------------------------|
| data that should not    | be reflowed by          | fill-paragraph          |

<!-- Filling: fill-paragraph for HTML comments -->
<!-- This is a very long HTML comment that should be properly filled when pressing M-q and continuation lines should align with the text after the opening delimiter. -->

<!-- Filling: fill-region over multiple paragraphs -->
First paragraph for fill-region test. This paragraph has some long text that could be reflowed.

Second paragraph for fill-region test. This paragraph also has some long text that could be reflowed.

<!-- Filling: adaptive fill prefix for list items -->
- This list item has a long first line and when filled, continuation lines should be indented to align with the text after the marker, not the marker itself.

  1. This ordered list item should also have proper adaptive fill prefix where continuation lines align with the text, not the number.

<!-- Filling: auto-fill respecting markdown structure -->
<!-- Type a very long line here to test auto-fill-mode behavior. -->

<!-- Filling: filling inside code blocks in language mode -->
```python
# This comment inside a code block could potentially be filled
# according to the language mode's filling rules rather than markdown's.
```

<!-- Navigation: imenu support for headings -->
## Imenu Test Heading

Content under imenu test heading. Use M-x imenu to see headings.

<!-- Navigation: outline integration -->
### Outline Test Heading

Content for outline test. Use outline-minor-mode commands.

<!-- Navigation: navigate between headings (next/previous) -->
## First Heading for Navigation

Some content.

## Second Heading for Navigation

Some content.

## Third Heading for Navigation

Some content.

<!-- Navigation: navigate between code blocks (next/previous) -->

```python
first_block = True
```

Some text between blocks.

```javascript
let secondBlock = true;
```

More text between blocks.

```rust
let third_block = true;
```

<!-- List Editing: auto-continue lists (RET inserts next item marker) -->
- Press RET at the end of this line to auto-insert next marker
- This should appear after pressing RET above

<!-- List Editing: numbered list auto-increment -->
1. Press RET at end of this line
2. This number should auto-increment

<!-- List Editing: list promotion / demotion -->
- Promote this item (decrease indent)
  - Demote this item (increase indent)

<!-- List Editing: list reordering (move up/down) -->
- Item A (move down)
- Item B (move up)
- Item C

<!-- List Editing: list renumbering -->
1. First
3. Third (should renumber to 2)
5. Fifth (should renumber to 3)

<!-- Heading Editing: promotion / demotion -->
### Promote this to ## or demote to ####

<!-- Heading Editing: reordering (move up/down) -->
## Move This Section Down

Content of section to move down.

## Move This Section Up

Content of section to move up.

<!-- Block Editing: block quote wrapping / unwrapping -->
Wrap this paragraph in a block quote.

> Unwrap this block quote.

<!-- Block Editing: code block insertion (with language prompt) -->
<!-- Place cursor here and invoke code block insertion. -->

<!-- Block Editing: commenting/uncommenting in code blocks -->
```python
x = 42
y = 100
# Toggle comment on the lines above
```

<!-- Link Editing: link insertion helper -->
<!-- Invoke link insertion command here to create a link. -->

<!-- Link Editing: link/reference completion -->
<!-- Type [ and use completing-read to pick from existing references. -->
<!-- Available references: [example], [bare-url], [angle-url], etc. -->

<!-- Markup Visibility: toggle markup hiding -->
This has **bold**, *italic*, ~~strike~~, `code`, and [links](https://example.com).
Use M-x markdown-ts-toggle-hide-markup to hide/show delimiters.

<!-- Markup Visibility: horizontal rule overlay -->
---

Above should display as a horizontal rule overlay.

<!-- Other: comment support (HTML comments) -->
<!-- This HTML comment should be recognized by comment-start/comment-end. -->

<!-- Other: mode menu item -->
<!-- A "Markdown" menu should appear in the menu bar. -->

<!-- Other: markdown-aware kill/yank -->
```
Kill this code block as a unit.
Do not split across block boundaries.
```

> And this block quote as a unit.

<!-- Other: footnote support -->
This text has a footnote[^1] reference.

[^1]: This is the footnote content.

<!-- Other: table of contents generation from headings -->
<!-- Generate TOC from all headings in this document. -->

<!-- Other: theme support for markdown-ts faces -->
<!-- All markdown-ts-* faces should integrate with modus-themes, ef-themes, etc. -->

<!-- Other: tests for delicate features -->
<!-- Automated tests should cover filling, fontification, and navigation. -->

<!-- Other: export to HTML / preview -->
<!-- Export this document to HTML or preview in a browser. -->

<!-- Fenced Code Blocks: nroff conventional mode -->
```nroff
.\" Created from Texinfo source by yat2m 1.58
.TH GNUPG 7 2025-02-19 "GnuPG 2.4.9" "GNU Privacy Guard 2.4"
.SH NAME
.B GnuPG
\- The GNU Privacy Guard suite of programs
.SH DESCRIPTION
GnuPG is a set of programs for public key encryption and digital
signatures.
.SH SEE ALSO
\fBgpg\fP(1),
\fBgpgsm\fP(1)
```

<!-- Fenced Code Blocks: latex/tex -->
```latex
\documentclass{article}
\usepackage{amsmath}
\begin{document}
\section{Introduction}
The equation $E = mc^2$ is famous.

\begin{equation}
  \int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
\end{equation}
\end{document}
```

```tex
\begin{itemize}
  \item First item
  \item Second item
\end{itemize}
```

<!-- Fenced Code Blocks: recursive markdown fontification -->
```markdown
# H1
- a
- b
  - c
	- d
## H2
1. 1
2. 2
3. 3

This is **bold text**.
This is *italicized text*.
This is emphasized ***bold italicized text***.
This is strike through ~~text~~.
```
