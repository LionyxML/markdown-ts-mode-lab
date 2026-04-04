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
[example]: https://www.gnu.org

<!-- Link Reference Definitions: link_label handling -->
[Example Label]: https://www.gnu.org

<!-- Link Reference Definitions: link_destination (bare URL) -->
[bare-url]: https://www.gnu.org/path?query=1

<!-- Link Reference Definitions: link_destination (<angle-bracketed>) -->
<!-- [angle-url]: <https://www.gnu.org/path with spaces> -->

<!-- Link Reference Definitions: link_title ("double") -->
[with-double-title]: https://www.gnu.org "Double quoted title"

<!-- Link Reference Definitions: link_title ('single') -->
<!-- [with-single-title]: https://www.gnu.org 'Single quoted title' -->

<!-- Link Reference Definitions: link_title ((parenthesized)) -->
[with-paren-title]: https://www.gnu.org (Parenthesized title)

<!-- Link Reference Definitions: multi-line -->
[multi-line-def]:
  https://www.gnu.org/very/long/path
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
[Click here](https://www.gnu.org "Example Site")

<!-- Links: inline link without title -->
[Click here](https://www.gnu.org)

<!-- Links: full reference link -->
[Click here][example]

<!-- Links: collapsed reference link -->
[example][]

<!-- Links: shortcut link -->
[example]

<!-- Links: link text fontification -->
The text [inside these brackets](https://www.gnu.org) should be fontified.

<!-- Links: link destination fontification -->
[link](https://this-url-should-be-fontified.com)

<!-- Links: link title fontification -->
[link](https://www.gnu.org "This title should be fontified")

<!-- Links: clickable link buttons (browse-url) -->
[Open in browser](https://www.gnu.org)

<!-- Links: file path links (find-file) -->
[Open local file](./README.md)

<!-- Links: link destination hiding when markup is hidden -->
[Only this text visible when markup hidden](https://hidden-url.com)

<!-- Images: inline image -->
![Alt text for image](https://www.gnu.org/image.png "Image title")

<!-- Images: inline image without title -->
![Alt text](./local-image.png)

<!-- Images: full reference image -->
![Alt text][example]

<!-- Images: collapsed reference image -->
![example][]

<!-- Images: shortcut reference image -->
![example]

<!-- Images: image description fontification -->
![This description should be fontified](https://www.gnu.org/img.png)

<!-- Images: inline image preview -->
![Preview this image](https://www.gnu.org/photo.jpg)

<!-- Autolinks: URI autolink -->
Visit <https://www.gnu.org> for more info.

<!-- Autolinks: email autolink -->
Contact us at <user@gnu.org> for support.

<!-- Autolinks: fontification as clickable button -->
The autolink <https://www.gnu.org> should be clickable.

<!-- Autolinks: angle bracket hiding when markup is hidden -->
When markup is hidden, <https://www.gnu.org> should show without < >.

<!-- Naked URLs: bare URLs without angle brackets -->
<!-- These are not handled by the grammar; goto-address-mode is a candidate. -->
Visit https://www.gnu.org for more info.

Here is a URL in the middle of text https://www.gnu.org/path?query=1&foo=bar and text continues.

Also email addresses without angle brackets: user@gnu.org should ideally be recognized.

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

<!-- Entity References: named HTML entities (basic) -->
&amp; &lt; &gt; &quot; &apos; &copy; &reg; &trade; &nbsp;

<!-- Entity References: typographic punctuation -->
&ndash; &mdash; &hellip; &bull; &lsquo; &rsquo; &ldquo; &rdquo; &prime;
&Prime;

<!-- Entity References: arrows -->
&larr; &rarr; &uarr; &darr; &harr; &crarr;

<!-- Entity References: mathematical -->
&infin; &sum; &prod; &radic; &prop; &exist; &forall; &part; &nabla;
&isin; &notin; &empty; &ne; &equiv; &le; &ge; &asymp; &sim; &sub; &sup;
&sube; &supe; &oplus; &otimes; &perp;

<!-- Entity References: Greek letters -->
&Alpha; &Beta; &Gamma; &Delta; &Omega; &alpha; &beta; &gamma; &delta;
&omega; &pi; &sigma; &theta; &lambda;

<!-- Entity References: currency and symbols -->
&euro; &pound; &yen; &cent; &sect; &para; &deg; &plusmn; &micro; &fnof;
&loz;

<!-- Entity References: card suits -->
&spades; &clubs; &hearts; &diams;

<!-- Entity References: spacing -->
&ensp; &emsp; &thinsp;

<!-- Entity References: ligatures and accented -->
&OElig; &oelig; &Scaron; &scaron; &Yuml; &Agrave; &Eacute; &Ntilde;
&szlig; &AElig; &aelig;

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

<!-- LaTeX / Math: complex inline -->
$\sqrt{3x-1}+(1+x)^2$

<!-- LaTeX / Math: multi-line display with nested $ and \\ -->
$$
f(x)=
\begin{cases}
1/d_{ij} & \quad \text{when $d_{ij} \leq 160$}\\
0 & \quad \text{otherwise}
\end{cases}
$$

<!-- LaTeX / Math: inline math in list items -->
- $x + y$
- $x - y$
- $x \times y$
- $x \div y$
- $\dfrac{x}{y}$

<!-- Superscript / Subscript: NOT SUPPORTED by tree-sitter-markdown grammar.
     No EXTENSION_ build flag exists for this.  Pandoc/PHP Markdown Extra
     syntax like superscript^2^ or subscript~2~ will not be parsed. -->
superscript^2^ and subscript~2~ are NOT recognized.

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

```javascript some nice js block
let secondBlock = true;
```

More text between blocks.

```rust some nice rust block
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
This has **bold**, *italic*, ~~strike~~, `code`, and [links](https://www.gnu.org).
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

---

# Fill Paragraph Tests

## Fill on unnumbered lists

<!-- Test A: cursor on col 0 of the long "- three" line, M-q.
     Expected: only the long item wraps, others untouched. -->

- one is a short item that should not be touched at all
- two is another short item that should remain exactly as it is
- three is a very long list item that absolutely needs to be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width by a significant amount
- four is yet another short item that must stay on its own line

<!-- Test B: cursor on col 0 of the long "- two" line, M-q.
     Expected: only the long item wraps, others untouched. -->

- one is a short item
- two is a very long list item that should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it exceeds the fill-column width significantly and needs to be broken into multiple lines
- three is a short item
- four is a short item

<!-- Test C: cursor on col 0 of the long "- This is..." item, M-q.
     Expected: only the long item wraps, others untouched. -->

- This is a very long list item that should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it exceeds the fill-column width significantly.
- short item
- another short item

<!-- Test D: cursor on col 0 of the long "  - inner one" line, M-q.
     Expected: only the long inner item wraps, no merging across
     items or nesting levels. -->

- outer one
- outer two has some text here
  - inner one is a very long nested list item that should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width by a large margin
  - inner two is short
- outer three

## Fill in block quotes

<!-- Test E: cursor on col 0 of the long "> block quote" line, M-q.
     Expected: long line wraps with "> " prefix, no merging across
     different nesting levels. -->

> block quote that is a very long line and should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width by a significant amount
> > nested block quote
> >
> > - item
> > - item
> block quote

<!-- Test F: cursor on col 0 of the long "> This is..." line, M-q.
     Expected: long line wraps with "> " prefix.  "Short line" merges
     in because both lines form one paragraph (no blank line between). -->

> This is a very long block quote line that should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column.
> Short line.

<!-- Test G: cursor on col 0 of the long "> This is..." line, M-q.
     Expected: long line wraps with "> " prefix.  "Short line" stays
     separate because the blank "> " line creates a paragraph break. -->

> This is a very long block quote line that should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column.
>
> Short line.

## Fill in nested block quotes with blank separator

<!-- Test H: cursor on "nested block quote" line (line 2), M-q.
     Expected: text stays on its own line, the "> >" blank line is
     NOT merged into it.  The list items below are untouched. -->

> block quote
> > nested block quote
> >
> > - item
> > - item
> block quote

<!-- Test I: cursor on the long "> > nested..." line, M-q.
     Expected: long line wraps with "> > " prefix.  The blank "> >"
     line acts as a paragraph break — list items are not merged. -->

> block quote
> > nested block quote that is a very long line and should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width
> >
> > - item one
> > - item two
> block quote

## List promote/demote on ordered lists

<!-- Test J: cursor on "2. two" line, M-left or M-right.
     Expected: user-error "Ordered list items cannot be nested
     (grammar limitation)".  The item must NOT be indented. -->

1. one
2. two
3. three

<!-- Test K: cursor on "- bar" line, M-right then M-left.
     Expected: demote indents "- bar" under "- foo", promote
     dedents it back.  Both directions work for unordered lists. -->

- foo
- bar
- baz

## Fill in nested block quotes preserves prefix style

<!-- Test L: cursor on the long "> > nested..." line, M-q.
     Expected: long line wraps with "> > " prefix (spaced style)
     on continuation lines.  Blank "> >" is not merged. -->

> block quote
> > nested block quote that is a very long line and should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width
> >
> > - item
> block quote

<!-- Test M: cursor on the long ">> nested..." line, M-q.
     Expected: long line wraps with ">> " prefix (compact style)
     on continuation lines.  Blank ">>" is not merged. -->

> block quote
>> nested block quote that is a very long line and should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width
>>
>> - item
> block quote

<!-- Test N: cursor on the long ">>> deep..." line, M-q.
     Expected: long line wraps with ">>> " prefix (compact style)
     on continuation lines. -->

>>> deep block quote that is a very long line and should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width

<!-- Test O: cursor on the long "> > > deep..." line, M-q.
     Expected: long line wraps with "> > > " prefix (spaced style)
     on continuation lines. -->

> > > deep block quote that is a very long line and should be wrapped by fill-paragraph when you place your cursor on it and press M-q because it clearly exceeds the fill-column width

## Auto-continue lists (RET)

<!-- Test P: cursor at end of "- foo" line, RET.
     Expected: new line "- " inserted, cursor after "- ". -->

- foo
- bar
- baz

<!-- Test Q: cursor at end of "2. second" line, RET.
     Expected: new line "3. " inserted with incremented number. -->

1. first
2. second
3. third

<!-- Test R: cursor at end of "  - inner" line, RET.
     Expected: new line "  - " inserted at same nesting level. -->

- outer
  - inner
  - inner2
- outer2

<!-- Test S: cursor at end of "* one" line, RET.
     Expected: new line "* " inserted (star marker preserved). -->

* one
* two

<!-- Test T: cursor at end of "+ one" line, RET.
     Expected: new line "+ " inserted (plus marker preserved). -->

+ one
+ two

<!-- Test U: cursor at end of "2) beta" line, RET.
     Expected: new line "3) " inserted (parenthesis style). -->

1) alpha
2) beta

<!-- Test V: type "- " then some text, RET, type more text, then
     RET on an empty item (just "- " with no text).
     Expected: the empty "- " line is removed (org-mode convention). -->

- type here then RET
-

<!-- Test W: cursor at end of "    - deeply nested" line, RET.
     Expected: new line "    - " at same 4-space indent level. -->

- level 1
  - level 2
    - deeply nested
    - also nested

<!-- Test X: cursor at end of a paragraph (not in a list), RET.
     Expected: normal newline, no marker inserted. -->

This is just a paragraph, not a list item.

## List renumbering

<!-- Test Y: cursor anywhere in the list, C-c C-r.
     Expected: renumber from first item's number (41, 42, 43). -->

41. first
3. second
5. third

<!-- Test Z: cursor anywhere in the list, C-u 10 C-c C-r.
     Expected: renumber starting from 10 (10, 11, 12). -->

1. first
5. second
99. third

<!-- Test AA: nested unordered inside ordered, cursor on "- bar", C-c C-r.
     Expected: no-op (unordered list is not renumbered).
     Note: nested ordered lists don't work (parser limitation,
     see Commentary).  Only unordered lists nest correctly. -->

1. outer
   - foo
   - bar
2. outer two

<!-- Test AB: parenthesis style, C-c C-r.
     Expected: renumber from 5 (5, 6, 7). -->

5) alpha
1) beta
9) gamma

<!-- Test AC: unordered list, C-c C-r.
     Expected: no-op, unordered lists are not renumbered. -->

- one
- two
- three

---

# Round 6 Test Cases

## RET in block quotes (spurious list items)

<!-- Test: Place point at x and press RET.
     Expected: new "> " line, NOT a "- " item.
     Bug was: parser sees block_continuation, finds wrong list_item. -->

> block quote
> > nested block quote
> >
> > - item
> > - item
> block quote x
x

## RET in block-quoted list

<!-- Test: Place point at x and press RET.
     Expected: new "> > - " line with proper quote prefix. -->

> block quote
> > nested block quote
> >
> > - item x
> > - item
> block quote

## Empty list items preserved

<!-- Test: Place point after the empty "- " and press RET.
     Expected: new "- " below, empty item NOT deleted.
     "I'd prefer to keep empty list items." -->

- foo
-
- bar

1. first
2.
3. third

## RET in indented code block

<!-- Test: Place point at x and press RET.
     Expected: new line at same indentation (4 spaces). -->

    pre block x
    more pre block

## Fill short block-quoted list (no space removal)

<!-- Test: Place point inside item on last line and M-q.
     Expected: nothing changes, no space removed after ">".
     Bug was: "> > - item" became "> >- item". -->

> >
> > - item
> > - item

## Fill long block-quoted list (should wrap)

<!-- Test: Place point inside the long item and M-q.
     Expected: wraps with "> > " prefix and list alignment.
     Bug was: fill did nothing. -->

> > - item weofij wefoijw efoijw efoiwje foiwejf oiwejf oiwefj owiefj woiefj woeifj weoifj weofij weofij weofij wefoij wefoijw efoiwje foij
> > - item

## Renumber nested list (no extra indent)

<!-- Test: Place point on "1. bar" and C-c C-r.
     Expected: renumbers to 1, 2 without adding extra indentation.
     Bug was: indentation doubled. -->

- foo
  1. bar
  1. baz

## Renumber preserves tabs

<!-- Test: Place point in list and C-c C-r.
     Expected: tabs between number and text preserved.
     Bug was: tabs converted to spaces. -->

1.	alpha
2.	beta
3.	gamma

## Renumber with nested sublist

<!-- Test: Place point at x and C-c C-r.
     Known issue: may only renumber items in the same parser
     list node, depending on how the grammar splits the tree. -->

1. a
2. a
2. a
2. a
  - foo
    1. foo
    1. bar
2. a
2. a
2. a x

## Two separate lists

<!-- Test: Place point in second list at x and C-c C-r.
     Known issue: parser may merge both lists into one node,
     causing the second to continue numbering from the first. -->

 1. a
 2. a
 3. a
 4. a
 5. a
 6. a
 7. a
 8. a
 9. a
10. a

1. space
2. space
3. space x

## Inline Image Preview Test Cases

Toggle images with `C-c C-x C-v` (`markdown-ts-toggle-inline-images`).

### Local relative path (should display)

![Test image](test_image.png)

### Local absolute path (should display)

![Absolute](/Users/rmj/site-compiled/emacs/rahul/test_image.png)

### Tilde path (should display if file exists)

![Tilde](~/site-compiled/emacs/rahul/test_image.png)

### Nonexistent file (should skip)

![Missing](nonexistent.png)

### Non-image file (should skip)

![Not image](Makefile)

### Empty alt text (should display)

![](test_image.png)

### Image in a list item

- ![List image](test_image.png)
- Second item

### List of Images

- ![List image](test_image.png)
- ![List image](test_image.png)
- ![List image](test_image.png)
- ![List image](test_image.png)


### Image with spaces in path (should skip if file doesn't exist)

![Spaced](path with spaces.png)

### Images inside a paragraph

This is the GNU logo ![gnu](test_image.png), and this is the Emacs logo ![emacs](https://www.gnu.org/software/emacs/images/emacs.png) inline in text.

### Remote URL (should skip by default)

<!-- (setq-local markdown-ts-display-remote-inline-images 'download) -->

![Remote](https://www.gnu.org/software/emacs/images/emacs.png)

### Image in a block quote

> ![Quoted image](test_image.png)
