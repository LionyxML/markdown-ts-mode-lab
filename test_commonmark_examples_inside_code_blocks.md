# CommonMark Spec 0.31.2 Examples

Ref.: <https://spec.commonmark.org/0.31.2/>


# 1 Introduction

## 1.1 What is Markdown?

## 1.2 Why is a spec needed?

## 1.3 About this document

# 2 Preliminaries

## 2.1 Characters and lines

## 2.2 Tabs

#### Thus, for example, a tab can be used instead of four spaces in an indented code block. (Note, however, that internal tabs are passed through as literal tabs, not expanded to spaces.)

Example 1:
```markdown
	foo	baz		bim
```

Example 2:
```markdown

  	foo	baz		bim

```

Example 3:
```markdown
    a	a
    ὐ	a
```

#### In the following example, a continuation paragraph of a list item is indented with a tab; this has exactly the same effect as indentation with four spaces would:

Example 4:
```markdown
  - foo

	bar
```

Example 5:
```markdown
- foo

		bar
```

Example 6:
```markdown
>		foo
```

Example 7:
```markdown
-		foo
```

Example 8:
```markdown
    foo
	bar
```

Example 9:
```markdown
 - foo
   - bar
	 - baz
```

Example 10:
```markdown
#	Foo
```

Example 11:
```markdown
*	*	*	
```

## 2.3 Insecure characters

## 2.4 Backslash escapes

#### Any ASCII punctuation character may be backslash-escaped:

Example 12:
```markdown
\!\"\#\$\%\&\'\(\)\*\+\,\-\.\/\:\;\<\=\>\?\@\[\\\]\^\_\`\{\|\}\~
```

#### Backslashes before other characters are treated as literal backslashes:

Example 13:
```markdown
\	\A\a\ \3\φ\«
```

#### Escaped characters are treated as regular characters and do not have their usual Markdown meanings:

Example 14:
```markdown
\*not emphasized*
\<br/> not a tag
\[not a link](/foo)
\`not code`
1\. not a list
\* not a list
\# not a heading
\[foo]: /url "not a reference"
\&ouml; not a character entity
```

#### If a backslash is itself escaped, the following character is not:

Example 15:
```markdown
\\*emphasis*
```

#### A backslash at the end of the line is a hard line break:

Example 16:
```markdown
foo\
bar
```

#### Backslash escapes do not work in code blocks, code spans, autolinks, or raw HTML:

Example 17:
```markdown
`` \[\` ``
```

Example 18:
```markdown
    \[\]
```

Example 19:
```markdown
~~~
\[\]
~~~
```

Example 20:
```markdown
<https://example.com?find=\*>
```

Example 21:
```markdown
<a href="/bar\/)">
```

#### But they work in all other contexts, including URLs and link titles, link references, and info strings in fenced code blocks:

Example 22:
```markdown
[foo](/bar\* "ti\*tle")
```

Example 23:
```markdown
[foo]

[foo]: /bar\* "ti\*tle"
```

Example 24:
````markdown
``` foo\+bar
foo
```
````

## 2.5 Entity and numeric character references

#### Entity references consist of &amp; + any of the valid HTML5 entity names + ;. The document https://html.spec.whatwg.org/entities.json is used as an authoritative source for the valid entity references and their corresponding code points.

Example 25:
```markdown
&nbsp; &amp; &copy; &AElig; &Dcaron;
&frac34; &HilbertSpace; &DifferentialD;
&ClockwiseContourIntegral; &ngE;
```

Example 26:
```markdown
&#35; &#1234; &#992; &#0;
```

#### Hexadecimal numeric character references consist of &amp;# + either X or x + a string of 1-6 hexadecimal digits + ;. They too are parsed as the corresponding Unicode character (this time specified with a hexadecimal numeral instead of decimal).

Example 27:
```markdown
&#X22; &#XD06; &#xcab;
```

#### Here are some nonentities:

Example 28:
```markdown
&nbsp &x; &#; &#x;
&#87654321;
&#abcdef0;
&ThisIsNotDefined; &hi?;
```

#### Although HTML5 does accept some entity references without a trailing semicolon (such as &amp;copy), these are not recognized here, because it makes the grammar too ambiguous:

Example 29:
```markdown
&copy
```

#### Strings that are not on the list of HTML5 named entities are not recognized as entity references either:

Example 30:
```markdown
&MadeUpEntity;
```

#### Entity and numeric character references are recognized in any context besides code spans or code blocks, including URLs, link titles, and fenced code block info strings:

Example 31:
```markdown
<a href="&ouml;&ouml;.html">
```

Example 32:
```markdown
[foo](/f&ouml;&ouml; "f&ouml;&ouml;")
```

Example 33:
```markdown
[foo]

[foo]: /f&ouml;&ouml; "f&ouml;&ouml;"
```

Example 34:
````markdown
``` f&ouml;&ouml;
foo
```
````

#### Entity and numeric character references are treated as literal text in code spans and code blocks:

Example 35:
```markdown
`f&ouml;&ouml;`
```

Example 36:
```markdown
    f&ouml;f&ouml;
```

#### Entity and numeric character references cannot be used in place of symbols indicating structure in CommonMark documents.

Example 37:
```markdown
&#42;foo&#42;
*foo*
```

Example 38:
```markdown
&#42; foo

* foo
```

Example 39:
```markdown
foo&#10;&#10;bar
```

Example 40:
```markdown
&#9;foo
```

Example 41:
```markdown
[a](url &quot;tit&quot;)
```

# 3 Blocks and inlines

## 3.1 Precedence

#### Indicators of block structure always take precedence over indicators of inline structure. So, for example, the following is a list with two items, not a list with one item containing a code span:

Example 42:
```markdown
- `one
- two`
```

## 3.2 Container blocks and leaf blocks

# 4 Leaf blocks

## 4.1 Thematic breaks

#### A line consisting of optionally up to three spaces of indentation, followed by a sequence of three or more matching -, _, or * characters, each followed optionally by any number of spaces or tabs, forms a thematic break.

Example 43:
```markdown
***
---
___
```

#### Wrong characters:

Example 44:
```markdown
+++
```

Example 45:
```markdown
===
```

#### Not enough characters:

Example 46:
```markdown
--
**
__
```

#### Up to three spaces of indentation are allowed:

Example 47:
```markdown
 ***
  ***
   ***
```

#### Four spaces of indentation is too many:

Example 48:
```markdown
    ***
```

Example 49:
```markdown
Foo
    ***
```

#### More than three characters may be used:

Example 50:
```markdown
_____________________________________
```

#### Spaces and tabs are allowed between the characters:

Example 51:
```markdown
 - - -
```

Example 52:
```markdown
 **  * ** * ** * **
```

Example 53:
```markdown
-     -      -      -
```

#### Spaces and tabs are allowed at the end:

Example 54:
```markdown
- - - -    
```

#### However, no other characters may occur in the line:

Example 55:
```markdown
_ _ _ _ a

a------

---a---
```

#### It is required that all of the characters other than spaces or tabs be the same. So, this is not a thematic break:

Example 56:
```markdown
 *-*
```

#### Thematic breaks do not need blank lines before or after:

Example 57:
```markdown
- foo
***
- bar
```

#### Thematic breaks can interrupt a paragraph:

Example 58:
```markdown
Foo
***
bar
```

#### If a line of dashes that meets the above conditions for being a thematic break could also be interpreted as the underline of a setext heading, the interpretation as a setext heading takes precedence. Thus, for example, this is a setext heading, not a paragraph followed by a thematic break:

Example 59:
```markdown
Foo
---
bar
```

#### When both a thematic break and a list item are possible interpretations of a line, the thematic break takes precedence:

Example 60:
```markdown
* Foo
* * *
* Bar
```

#### If you want a thematic break in a list item, use a different bullet:

Example 61:
```markdown
- Foo
- * * *
```

## 4.2 ATX headings

#### Simple headings:

Example 62:
```markdown
# foo
## foo
### foo
#### foo
##### foo
###### foo
```

#### More than six # characters is not a heading:

Example 63:
```markdown
####### foo
```

Example 64:
```markdown
#5 bolt

#hashtag
```

#### This is not a heading, because the first # is escaped:

Example 65:
```markdown
\## foo
```

#### Contents are parsed as inlines:

Example 66:
```markdown
# foo *bar* \*baz\*
```

#### Leading and trailing spaces or tabs are ignored in parsing inline content:

Example 67:
```markdown
#                  foo                     
```

#### Up to three spaces of indentation are allowed:

Example 68:
```markdown
 ### foo
  ## foo
   # foo
```

#### Four spaces of indentation is too many:

Example 69:
```markdown
    # foo
```

Example 70:
```markdown
foo
    # bar
```

#### A closing sequence of # characters is optional:

Example 71:
```markdown
## foo ##
  ###   bar    ###
```

#### It need not be the same length as the opening sequence:

Example 72:
```markdown
# foo ##################################
##### foo ##
```

#### Spaces or tabs are allowed after the closing sequence:

Example 73:
```markdown
### foo ###     
```

#### A sequence of # characters with anything but spaces or tabs following it is not a closing sequence, but counts as part of the contents of the heading:

Example 74:
```markdown
### foo ### b
```

#### The closing sequence must be preceded by a space or tab:

Example 75:
```markdown
# foo#
```

#### Backslash-escaped # characters do not count as part of the closing sequence:

Example 76:
```markdown
### foo \###
## foo #\##
# foo \#
```

#### ATX headings need not be separated from surrounding content by blank lines, and they can interrupt paragraphs:

Example 77:
```markdown
****
## foo
****
```

Example 78:
```markdown
Foo bar
# baz
Bar foo
```

#### ATX headings can be empty:

Example 79:
```markdown
## 
#
### ###
```

## 4.3 Setext headings

#### Simple examples:

Example 80:
```markdown
Foo *bar*
=========

Foo *bar*
---------
```

#### The content of the header may span more than one line:

Example 81:
```markdown
Foo *bar
baz*
====
```

#### The contents are the result of parsing the headings’s raw content as inlines. The heading’s raw content is formed by concatenating the lines and removing initial and final spaces or tabs.

Example 82:
```markdown
  Foo *bar
baz*	
====
```

#### The underlining can be any length:

Example 83:
```markdown
Foo
-------------------------

Foo
=
```

#### The heading content can be preceded by up to three spaces of indentation, and need not line up with the underlining:

Example 84:
```markdown
   Foo
---

  Foo
-----

  Foo
  ===
```

#### Four spaces of indentation is too many:

Example 85:
```markdown
    Foo
    ---

    Foo
---
```

#### The setext heading underline can be preceded by up to three spaces of indentation, and may have trailing spaces or tabs:

Example 86:
```markdown
Foo
   ----      
```

#### Four spaces of indentation is too many:

Example 87:
```markdown
Foo
    ---
```

#### The setext heading underline cannot contain internal spaces or tabs:

Example 88:
```markdown
Foo
= =

Foo
--- -
```

#### Trailing spaces or tabs in the content line do not cause a hard line break:

Example 89:
```markdown
Foo  
-----
```

#### Nor does a backslash at the end:

Example 90:
```markdown
Foo\
----
```

#### Since indicators of block structure take precedence over indicators of inline structure, the following are setext headings:

Example 91:
```markdown
`Foo
----
`

<a title="a lot
---
of dashes"/>
```

#### The setext heading underline cannot be a lazy continuation line in a list item or block quote:

Example 92:
```markdown
> Foo
---
```

Example 93:
```markdown
> foo
bar
===
```

Example 94:
```markdown
- Foo
---
```

#### A blank line is needed between a paragraph and a following setext heading, since otherwise the paragraph becomes part of the heading’s content:

Example 95:
```markdown
Foo
Bar
---
```

#### But in general a blank line is not required before or after setext headings:

Example 96:
```markdown
---
Foo
---
Bar
---
Baz
```

#### Setext headings cannot be empty:

Example 97:
```markdown

====
```

#### Setext heading text lines must not be interpretable as block constructs other than paragraphs. So, the line of dashes in these examples gets interpreted as a thematic break:

Example 98:
```markdown
---
---
```

Example 99:
```markdown
- foo
-----
```

Example 100:
```markdown
    foo
---
```

Example 101:
```markdown
> foo
-----
```

#### If you want a heading with &gt; foo as its literal text, you can use backslash escapes:

Example 102:
```markdown
\> foo
------
```

#### We find interpretation 4 most natural, and interpretation 4 increases the expressive power of CommonMark, by allowing multiline headings. Authors who want interpretation 1 can put a blank line after the first paragraph:

Example 103:
```markdown
Foo

bar
---
baz
```

#### Authors who want interpretation 2 can put blank lines around the thematic break,

Example 104:
```markdown
Foo
bar

---

baz
```

#### or use a thematic break that cannot count as a setext heading underline, such as

Example 105:
```markdown
Foo
bar
* * *
baz
```

#### Authors who want interpretation 3 can use backslash escapes:

Example 106:
```markdown
Foo
bar
\---
baz
```

## 4.4 Indented code blocks

#### An indented code block cannot interrupt a paragraph, so there must be a blank line between a paragraph and a following indented code block. (A blank line is not needed, however, between a code block and a following paragraph.)

Example 107:
```markdown
    a simple
      indented code block
```

#### If there is any ambiguity between an interpretation of indentation as a code block and as indicating that material belongs to a list item, the list item interpretation takes precedence:

Example 108:
```markdown
  - foo

    bar
```

Example 109:
```markdown
1.  foo

    - bar
```

#### The contents of a code block are literal text, and do not get parsed as Markdown:

Example 110:
```markdown
    <a/>
    *hi*

    - one
```

#### Here we have three chunks separated by blank lines:

Example 111:
```markdown
    chunk1

    chunk2
  
 
 
    chunk3
```

#### Any initial spaces or tabs beyond four spaces of indentation will be included in the content, even in interior blank lines:

Example 112:
```markdown
    chunk1
      
      chunk2
```

#### An indented code block cannot interrupt a paragraph. (This allows hanging indents and the like.)

Example 113:
```markdown
Foo
    bar
```

#### However, any non-blank line with fewer than four spaces of indentation ends the code block immediately. So a paragraph may occur immediately after indented code:

Example 114:
```markdown
    foo
bar
```

#### And indented code can occur immediately before and after other kinds of blocks:

Example 115:
```markdown
# Heading
    foo
Heading
------
    foo
----
```

#### The first line can be preceded by more than four spaces of indentation:

Example 116:
```markdown
        foo
    bar
```

#### Blank lines preceding or following an indented code block are not included in it:

Example 117:
```markdown

    
    foo
    
```

#### Trailing spaces or tabs are included in the code block’s content:

Example 118:
```markdown
    foo  
```

## 4.5 Fenced code blocks

#### Here is a simple example with backticks:

Example 119:
````markdown
```
<
 >
```
````

#### With tildes:

Example 120:
```markdown
~~~
<
 >
~~~
```

#### Fewer than three backticks is not enough:

Example 121:
```markdown
``
foo
``
```

#### The closing code fence must use the same character as the opening fence:

Example 122:
````markdown
```
aaa
~~~
```
````

Example 123:
````markdown
~~~
aaa
```
~~~
````

#### The closing code fence must be at least as long as the opening fence:

Example 124:
```````markdown
````
aaa
```
``````
```````

Example 125:
```markdown
~~~~
aaa
~~~
~~~~
```

#### Unclosed code blocks are closed by the end of the document (or the enclosing block quote or list item):

Example 126:
````markdown
```
````

Example 127:
``````markdown
`````

```
aaa
``````

Example 128:
```markdown
> ```
> aaa

bbb
```

#### A code block can have all empty lines as its content:

Example 129:
````markdown
```

  
```
````

#### A code block can be empty:

Example 130:
````markdown
```
```
````

#### Fences can be indented. If the opening fence is indented, content lines will have equivalent opening indentation removed, if present:

Example 131:
````markdown
 ```
 aaa
aaa
```
````

Example 132:
````markdown
  ```
aaa
  aaa
aaa
  ```
````

Example 133:
````markdown
   ```
   aaa
    aaa
  aaa
   ```
````

#### Four spaces of indentation is too many:

Example 134:
````markdown
    ```
    aaa
    ```
````

#### Closing fences may be preceded by up to three spaces of indentation, and their indentation need not match that of the opening fence:

Example 135:
````markdown
```
aaa
  ```
````

Example 136:
````markdown
   ```
aaa
  ```
````

#### This is not a closing fence, because it is indented 4 spaces:

Example 137:
````markdown
```
aaa
    ```
````

#### Code fences (opening and closing) cannot contain internal spaces or tabs:

Example 138:
````markdown
``` ```
aaa
````

Example 139:
```markdown
~~~~~~
aaa
~~~ ~~
```

#### Fenced code blocks can interrupt paragraphs, and can be followed directly by paragraphs, without a blank line between:

Example 140:
````markdown
foo
```
bar
```
baz
````

#### Other blocks can also occur before and after fenced code blocks without an intervening blank line:

Example 141:
```markdown
foo
---
~~~
bar
~~~
# baz
```

Example 142:
````markdown
```ruby
def foo(x)
  return 3
end
```
````

Example 143:
```markdown
~~~~    ruby startline=3 $%@#$
def foo(x)
  return 3
end
~~~~~~~
```

Example 144:
`````markdown
````;
````
`````

#### Info strings for backtick code blocks cannot contain backticks:

Example 145:
````markdown
``` aa ```
foo
````

#### Info strings for tilde code blocks can contain backticks and tildes:

Example 146:
```markdown
~~~ aa ``` ~~~
foo
~~~
```

#### Closing code fences cannot have info strings:

Example 147:
````markdown
```
``` aaa
```
````

## 4.6 HTML blocks

#### For instance, &lt;pre&gt; within an HTML block started by &lt;table&gt; will not affect the parser state; as the HTML block was started in by start condition 6, it will end at any blank line. This can be surprising:

Example 148:
```markdown
<table><tr><td>
<pre>
**Hello**,

_world_.
</pre>
</td></tr></table>
```

#### Some simple examples follow. Here are some basic HTML blocks of type 6:

Example 149:
```markdown
<table>
  <tr>
    <td>
           hi
    </td>
  </tr>
</table>

okay.
```

Example 150:
```markdown
 <div>
  *hello*
         <foo><a>
```

#### A block can also start with a closing tag:

Example 151:
```markdown
</div>
*foo*
```

#### Here we have two HTML blocks with a Markdown paragraph between them:

Example 152:
```markdown
<DIV CLASS="foo">

*Markdown*

</DIV>
```

#### The tag on the first line can be partial, as long as it is split where there would be whitespace:

Example 153:
```markdown
<div id="foo"
  class="bar">
</div>
```

Example 154:
```markdown
<div id="foo" class="bar
  baz">
</div>
```

#### An open tag need not be closed:

Example 155:
```markdown
<div>
*foo*

*bar*
```

#### A partial tag need not even be completed (garbage in, garbage out):

Example 156:
```markdown
<div id="foo"
*hi*
```

Example 157:
```markdown
<div class
foo
```

#### The initial tag doesn’t even need to be a valid tag, as long as it starts like one:

Example 158:
```markdown
<div *???-&&&-<---
*foo*
```

#### In type 6 blocks, the initial tag need not be on a line by itself:

Example 159:
```markdown
<div><a href="bar">*foo*</a></div>
```

Example 160:
```markdown
<table><tr><td>
foo
</td></tr></table>
```

#### Everything until the next blank line or end of document gets included in the HTML block. So, in the following example, what looks like a Markdown code block is actually part of the HTML block, which continues until a blank line or the end of the document is reached:

Example 161:
````markdown
<div></div>
``` c
int x = 33;
```
````

#### To start an HTML block with a tag that is not in the list of block-level tags in (6), you must put the tag by itself on the first line (and it must be complete):

Example 162:
```markdown
<a href="foo">
*bar*
</a>
```

#### In type 7 blocks, the tag name can be anything:

Example 163:
```markdown
<Warning>
*bar*
</Warning>
```

Example 164:
```markdown
<i class="foo">
*bar*
</i>
```

Example 165:
```markdown
</ins>
*bar*
```

Example 166:
```markdown
<del>
*foo*
</del>
```

#### In this case, we get a raw HTML block that just includes the &lt;del&gt; tag (because it ends with the following blank line). So the contents get interpreted as CommonMark:

Example 167:
```markdown
<del>

*foo*

</del>
```

#### Finally, in this case, the &lt;del&gt; tags are interpreted as raw HTML inside the CommonMark paragraph. (Because the tag is not on a line by itself, we get inline HTML rather than an HTML block.)

Example 168:
```markdown
<del>*foo*</del>
```

#### A pre tag (type 1):

Example 169:
```markdown
<pre language="haskell"><code>
import Text.HTML.TagSoup

main :: IO ()
main = print $ parseTags tags
</code></pre>
okay
```

#### A script tag (type 1):

Example 170:
```markdown
<script type="text/javascript">
// JavaScript example

document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>
okay
```

#### A textarea tag (type 1):

Example 171:
```markdown
<textarea>

*foo*

_bar_

</textarea>
```

#### A style tag (type 1):

Example 172:
```markdown
<style
  type="text/css">
h1 {color:red;}

p {color:blue;}
</style>
okay
```

#### If there is no matching end tag, the block will end at the end of the document (or the enclosing block quote or list item):

Example 173:
```markdown
<style
  type="text/css">

foo
```

Example 174:
```markdown
> <div>
> foo

bar
```

Example 175:
```markdown
- <div>
- foo
```

#### The end tag can occur on the same line as the start tag:

Example 176:
```markdown
<style>p{color:red;}</style>
*foo*
```

Example 177:
```markdown
<!-- foo -->*bar*
*baz*
```

#### Note that anything on the last line after the end tag will be included in the HTML block:

Example 178:
```markdown
<script>
foo
</script>1. *bar*
```

#### A comment (type 2):

Example 179:
```markdown
<!-- Foo

bar
   baz -->
okay
```

#### A processing instruction (type 3):

Example 180:
```markdown
<?php

  echo '>';

?>
okay
```

#### A declaration (type 4):

Example 181:
```markdown
<!-- <!DOCTYPE html> -->
```

#### CDATA (type 5):

Example 182:
```markdown
<![CDATA[
function matchwo(a,b)
{
  if (a < b && a < 0) then {
    return 1;

  } else {

    return 0;
  }
}
]]>
okay
```

#### The opening tag can be preceded by up to three spaces of indentation, but not four:

Example 183:
```markdown
  <!-- foo -->

    <!-- foo -->
```

Example 184:
```markdown
  <div>

    <div>
```

#### An HTML block of types 1–6 can interrupt a paragraph, and need not be preceded by a blank line.

Example 185:
```markdown
Foo
<div>
bar
</div>
```

#### However, a following blank line is needed, except at the end of a document, and except for blocks of types 1–5, above:

Example 186:
```markdown
<div>
bar
</div>
*foo*
```

#### HTML blocks of type 7 cannot interrupt a paragraph:

Example 187:
```markdown
Foo
<a href="bar">
baz
```

#### Compare:

Example 188:
```markdown
<div>

*Emphasized* text.

</div>
```

Example 189:
```markdown
<div>
*Emphasized* text.
</div>
```

#### The main potential drawback is that one can no longer paste HTML blocks into Markdown documents with 100% reliability. However, in most cases this will work fine, because the blank lines in HTML are usually followed by HTML block tags. For example:

Example 190:
```markdown
<table>

<tr>

<td>
Hi
</td>

</tr>

</table>
```

#### There are problems, however, if the inner tags are indented and separated by spaces, as then they will be interpreted as an indented code block:

Example 191:
```markdown
<table>

  <tr>

    <td>
      Hi
    </td>

  </tr>

</table>
```

## 4.7 Link reference definitions

#### A link reference definition does not correspond to a structural element of a document. Instead, it defines a label which can be used in reference links and reference-style images elsewhere in the document. Link reference definitions can come either before or after the links that use them.

Example 192:
```markdown
[foo]: /url "title"

[foo]
```

Example 193:
```markdown
   [foo]: 
      /url  
           'the title'  

[foo]
```

Example 194:
```markdown
[Foo*bar\]]:my_(url) 'title (with parens)'

[Foo*bar\]]
```

Example 195:
```markdown
[Foo bar]:
<my url>
'title'

[Foo bar]
```

#### The title may extend over multiple lines:

Example 196:
```markdown
[foo]: /url '
title
line1
line2
'

[foo]
```

#### However, it may not contain a blank line:

Example 197:
```markdown
[foo]: /url 'title

with blank line'

[foo]
```

#### The title may be omitted:

Example 198:
```markdown
[foo]:
/url

[foo]
```

#### The link destination may not be omitted:

Example 199:
```markdown
[foo]:

[foo]
```

#### However, an empty link destination may be specified using angle brackets:

Example 200:
```markdown
[foo]: <>

[foo]
```

#### The title must be separated from the link destination by spaces or tabs:

Example 201:
```markdown
[foo]: <bar>(baz)

[foo]
```

#### Both title and destination can contain backslash escapes and literal backslashes:

Example 202:
```markdown
[foo]: /url\bar\*baz "foo\"bar\baz"

[foo]
```

#### A link can come before its corresponding definition:

Example 203:
```markdown
[foo]

[foo]: url
```

#### If there are several matching definitions, the first one takes precedence:

Example 204:
```markdown
[foo]

[foo]: first
[foo]: second
```

#### As noted in the section on Links, matching of labels is case-insensitive (see matches).

Example 205:
```markdown
[FOO]: /url

[Foo]
```

Example 206:
```markdown
[ΑΓΩ]: /φου

[αγω]
```

#### Whether something is a link reference definition is independent of whether the link reference it defines is used in the document. Thus, for example, the following document contains just a link reference definition, and no visible content:

Example 207:
```markdown
[foo]: /url
```

#### Here is another one:

Example 208:
```markdown
[
foo
]: /url
bar
```

#### This is not a link reference definition, because there are characters other than spaces or tabs after the title:

Example 209:
```markdown
[foo]: /url "title" ok
```

#### This is a link reference definition, but it has no title:

Example 210:
```markdown
[foo]: /url
"title" ok
```

#### This is not a link reference definition, because it is indented four spaces:

Example 211:
```markdown
    [foo]: /url "title"

[foo]
```

#### This is not a link reference definition, because it occurs inside a code block:

Example 212:
````markdown
```
[foo]: /url
```

[foo]
````

#### A link reference definition cannot interrupt a paragraph.

Example 213:
```markdown
Foo
[bar]: /baz

[bar]
```

#### However, it can directly follow other block elements, such as headings and thematic breaks, and it need not be followed by a blank line.

Example 214:
```markdown
# [Foo]
[foo]: /url
> bar
```

Example 215:
```markdown
[foo]: /url
bar
===
[foo]
```

Example 216:
```markdown
[foo]: /url
===
[foo]
```

#### Several link reference definitions can occur one after another, without intervening blank lines.

Example 217:
```markdown
[foo]: /foo-url "foo"
[bar]: /bar-url
  "bar"
[baz]: /baz-url

[foo],
[bar],
[baz]
```

#### Link reference definitions can occur inside block containers, like lists and block quotations. They affect the entire document, not just the container in which they are defined:

Example 218:
```markdown
[foo]

> [foo]: /url
```

## 4.8 Paragraphs

#### A simple example with two paragraphs:

Example 219:
```markdown
aaa

bbb
```

#### Paragraphs can contain multiple lines, but no blank lines:

Example 220:
```markdown
aaa
bbb

ccc
ddd
```

#### Multiple blank lines between paragraphs have no effect:

Example 221:
```markdown
aaa


bbb
```

#### Leading spaces or tabs are skipped:

Example 222:
```markdown
  aaa
 bbb
```

#### Lines after the first may be indented any amount, since indented code blocks cannot interrupt paragraphs.

Example 223:
```markdown
aaa
             bbb
                                       ccc
```

#### However, the first line may be preceded by up to three spaces of indentation. Four spaces of indentation is too many:

Example 224:
```markdown
   aaa
bbb
```

Example 225:
```markdown
    aaa
bbb
```

#### Final spaces or tabs are stripped before inline parsing, so a paragraph that ends with two or more spaces will not end with a hard line break:

Example 226:
```markdown
aaa     
bbb     
```

## 4.9 Blank lines

#### Blank lines at the beginning and end of the document are also ignored.

Example 227:
```markdown
  

aaa
  

# aaa

  
```

# 5 Container blocks

## 5.1 Block quotes

#### Here is a simple example:

Example 228:
```markdown
> # Foo
> bar
> baz
```

#### The space or tab after the &gt; characters can be omitted:

Example 229:
```markdown
># Foo
>bar
> baz
```

#### The &gt; characters can be preceded by up to three spaces of indentation:

Example 230:
```markdown
   > # Foo
   > bar
 > baz
```

#### Four spaces of indentation is too many:

Example 231:
```markdown
    > # Foo
    > bar
    > baz
```

#### The Laziness clause allows us to omit the &gt; before paragraph continuation text:

Example 232:
```markdown
> # Foo
> bar
baz
```

#### A block quote can contain some lazy and some non-lazy continuation lines:

Example 233:
```markdown
> bar
baz
> foo
```

#### without changing the meaning:

Example 234:
```markdown
> foo
---
```

#### then the block quote ends after the first line:

Example 235:
```markdown
> - foo
- bar
```

#### For the same reason, we can’t omit the &gt; in front of subsequent lines of an indented or fenced code block:

Example 236:
```markdown
>     foo
    bar
```

Example 237:
````markdown
> ```
foo
```
````

#### Note that in the following case, we have a lazy continuation line:

Example 238:
```markdown
> foo
    - bar
```

#### A block quote can be empty:

Example 239:
```markdown
>
```

Example 240:
```markdown
>
>  
> 
```

#### A block quote can have initial or final blank lines:

Example 241:
```markdown
>
> foo
>  
```

#### A blank line always separates block quotes:

Example 242:
```markdown
> foo

> bar
```

#### Consecutiveness means that if we put these block quotes together, we get a single block quote:

Example 243:
```markdown
> foo
> bar
```

#### To get a block quote with two paragraphs, use:

Example 244:
```markdown
> foo
>
> bar
```

#### Block quotes can interrupt paragraphs:

Example 245:
```markdown
foo
> bar
```

#### In general, blank lines are not needed before or after block quotes:

Example 246:
```markdown
> aaa
***
> bbb
```

#### However, because of laziness, a blank line is needed between a block quote and a following paragraph:

Example 247:
```markdown
> bar
baz
```

Example 248:
```markdown
> bar

baz
```

Example 249:
```markdown
> bar
>
baz
```

#### It is a consequence of the Laziness rule that any number of initial &gt;s may be omitted on a continuation line of a nested block quote:

Example 250:
```markdown
> > > foo
bar
```

Example 251:
```markdown
>>> foo
> bar
>>baz
```

#### When including an indented code block in a block quote, remember that the block quote marker includes both the &gt; and a following space of indentation. So five spaces are needed after the &gt;:

Example 252:
```markdown
>     code

>    not code
```

## 5.2 List items

#### For example, let Ls be the lines

Example 253:
```markdown
A paragraph
with two lines.

    indented code

> A block quote.
```

#### And let M be the marker 1., and N = 2. Then rule #1 says that the following is an ordered list item with start number 1, and the same contents as Ls:

Example 254:
```markdown
1.  A paragraph
    with two lines.

        indented code

    > A block quote.
```

#### Here are some examples showing how far content must be indented to be put under the list item:

Example 255:
```markdown
- one

 two
```

Example 256:
```markdown
- one

  two
```

Example 257:
```markdown
 -    one

     two
```

Example 258:
```markdown
 -    one

      two
```

Example 259:
```markdown
   > > 1.  one
>>
>>     two
```

#### The converse is also possible. In the following example, the word two occurs far to the right of the initial text of the list item, one, but it is not considered part of the list item, because it is not indented far enough past the blockquote marker:

Example 260:
```markdown
>>- one
>>
  >  > two
```

#### Note that at least one space or tab is needed between the list marker and any following content, so these are not list items:

Example 261:
```markdown
-one

2.two
```

#### A list item may contain blocks that are separated by more than one blank line.

Example 262:
```markdown
- foo


  bar
```

#### A list item may contain any kind of block:

Example 263:
````markdown
1.  foo

    ```
    bar
    ```

    baz

    > bam
````

#### A list item that contains an indented code block will preserve empty lines within the code block verbatim.

Example 264:
```markdown
- Foo

      bar


      baz
```

#### Note that ordered list start numbers must be nine digits or less:

Example 265:
```markdown
123456789. ok
```

Example 266:
```markdown
1234567890. not ok
```

#### A start number may begin with 0s:

Example 267:
```markdown
0. ok
```

Example 268:
```markdown
003. ok
```

#### A start number may not be negative:

Example 269:
```markdown
-1. not ok
```

#### An indented code block will have to be preceded by four spaces of indentation beyond the edge of the region where text will be included in the list item. In the following case that is 6 spaces:

Example 270:
```markdown
- foo

      bar
```

#### And in this case it is 11 spaces:

Example 271:
```markdown
  10.  foo

           bar
```

#### If the first block in the list item is an indented code block, then by rule #2, the contents must be preceded by one space of indentation after the list marker:

Example 272:
```markdown
    indented code

paragraph

    more code
```

Example 273:
```markdown
1.     indented code

   paragraph

       more code
```

#### Note that an additional space of indentation is interpreted as space inside the code block:

Example 274:
```markdown
1.      indented code

   paragraph

       more code
```

Example 275:
```markdown
   foo

bar
```

Example 276:
```markdown
-    foo

  bar
```

#### This is not a significant restriction, because when a block is preceded by up to three spaces of indentation, the indentation can always be removed without a change in interpretation, allowing rule #1 to be applied. So, in the above case:

Example 277:
```markdown
-  foo

   bar
```

#### Here are some list items that start with a blank line but are not empty:

Example 278:
````markdown
-
  foo
-
  ```
  bar
  ```
-
      baz
````

#### When the list item starts with a blank line, the number of spaces following the list marker doesn’t change the required indentation:

Example 279:
```markdown
-   
  foo
```

#### A list item can begin with at most one blank line. In the following example, foo is not part of the list item:

Example 280:
```markdown
-

  foo
```

#### Here is an empty bullet list item:

Example 281:
```markdown
- foo
-
- bar
```

#### It does not matter whether there are spaces or tabs following the list marker:

Example 282:
```markdown
- foo
-   
- bar
```

#### Here is an empty ordered list item:

Example 283:
```markdown
1. foo
2.
3. bar
```

#### A list may start or end with an empty list item:

Example 284:
```markdown
*
```

#### However, an empty list item cannot interrupt a paragraph:

Example 285:
```markdown
foo
*

foo
1.
```

#### Indented one space:

Example 286:
```markdown
 1.  A paragraph
     with two lines.

         indented code

     > A block quote.
```

#### Indented two spaces:

Example 287:
```markdown
  1.  A paragraph
      with two lines.

          indented code

      > A block quote.
```

#### Indented three spaces:

Example 288:
```markdown
   1.  A paragraph
       with two lines.

           indented code

       > A block quote.
```

#### Four spaces indent gives a code block:

Example 289:
```markdown
    1.  A paragraph
        with two lines.

            indented code

        > A block quote.
```

#### Here is an example with lazy continuation lines:

Example 290:
```markdown
  1.  A paragraph
with two lines.

          indented code

      > A block quote.
```

#### Indentation can be partially deleted:

Example 291:
```markdown
  1.  A paragraph
    with two lines.
```

#### These examples show how laziness can work in nested structures:

Example 292:
```markdown
> 1. > Blockquote
continued here.
```

Example 293:
```markdown
> 1. > Blockquote
> continued here.
```

#### So, in this case we need two spaces indent:

Example 294:
```markdown
- foo
  - bar
    - baz
      - boo
```

#### One is not enough:

Example 295:
```markdown
- foo
 - bar
  - baz
   - boo
```

#### Here we need four, because the list marker is wider:

Example 296:
```markdown
10) foo
    - bar
```

#### Three is not enough:

Example 297:
```markdown
10) foo
   - bar
```

#### A list may be the first block in a list item:

Example 298:
```markdown
- - foo
```

Example 299:
```markdown
1. - 2. foo
```

#### A list item can contain a heading:

Example 300:
```markdown
- # Foo
- Bar
  ---
  baz
```

## 5.3 Lists

#### Changing the bullet or ordered list delimiter starts a new list:

Example 301:
```markdown
- foo
- bar
+ baz
```

Example 302:
```markdown
1. foo
2. bar
3) baz
```

#### In CommonMark, a list can interrupt a paragraph. That is, no blank line is needed to separate a paragraph from a following list:

Example 303:
```markdown
Foo
- bar
- baz
```

#### In order to solve the problem of unwanted lists in paragraphs with hard-wrapped numerals, we allow only lists starting with 1 to interrupt paragraphs. Thus,

Example 304:
```markdown
The number of windows in my house is
14.  The number of doors is 6.
```

#### We may still get an unintended result in cases like

Example 305:
```markdown
The number of windows in my house is
1.  The number of doors is 6.
```

#### There can be any number of blank lines between items:

Example 306:
```markdown
- foo

- bar


- baz
```

Example 307:
```markdown
- foo
  - bar
    - baz


      bim
```

#### To separate consecutive lists of the same type, or to separate a list from an indented code block that would otherwise be parsed as a subparagraph of the final list item, you can insert a blank HTML comment:

Example 308:
```markdown
- foo
- bar

<!-- -->

- baz
- bim
```

Example 309:
```markdown
-   foo

    notcode

-   foo

<!-- -->

    code
```

#### List items need not be indented to the same level. The following list items will be treated as items at the same list level, since none is indented enough to belong to the previous list item:

Example 310:
```markdown
- a
 - b
  - c
   - d
  - e
 - f
- g
```

Example 311:
```markdown
1. a

  2. b

   3. c
```

#### Note, however, that list items may not be preceded by more than three spaces of indentation. Here - e is treated as a paragraph continuation line, because it is indented more than three spaces:

Example 312:
```markdown
- a
 - b
  - c
   - d
    - e
```

#### And here, 3. c is treated as in indented code block, because it is indented four spaces and preceded by a blank line.

Example 313:
```markdown
1. a

  2. b

    3. c
```

#### This is a loose list, because there is a blank line between two of the list items:

Example 314:
```markdown
- a
- b

- c
```

#### So is this, with a empty second item:

Example 315:
```markdown
* a
*

* c
```

#### These are loose lists, even though there are no blank lines between the items, because one of the items directly contains two block-level elements with a blank line between them:

Example 316:
```markdown
- a
- b

  c
- d
```

Example 317:
```markdown
- a
- b

  [ref]: /url
- d
```

#### This is a tight list, because the blank lines are in a code block:

Example 318:
````markdown
- a
- ```
  b


  ```
- c
````

#### This is a tight list, because the blank line is between two paragraphs of a sublist. So the sublist is loose while the outer list is tight:

Example 319:
```markdown
- a
  - b

    c
- d
```

#### This is a tight list, because the blank line is inside the block quote:

Example 320:
```markdown
* a
  > b
  >
* c
```

#### This list is tight, because the consecutive block elements are not separated by blank lines:

Example 321:
````markdown
- a
  > b
  ```
  c
  ```
- d
````

#### A single-paragraph list is tight:

Example 322:
```markdown
- a
```

Example 323:
```markdown
- a
  - b
```

#### This list is loose, because of the blank line between the two block elements in the list item:

Example 324:
````markdown
1. ```
   foo
   ```

   bar
````

#### Here the outer list is loose, the inner list tight:

Example 325:
```markdown
* foo
  * bar

  baz
```

Example 326:
```markdown
- a
  - b
  - c

- d
  - e
  - f
```

# 6 Inlines

#### Inlines are parsed sequentially from the beginning of the character stream to the end (left to right, in left-to-right languages). Thus, for example, in

Example 327:
```markdown
`hi`lo`
```

## 6.1 Code spans

#### This is a simple code span:

Example 328:
```markdown
`foo`
```

#### Here two backticks are used, because the code contains a backtick. This example also illustrates stripping of a single leading and trailing space:

Example 329:
```markdown
`` foo ` bar ``
```

#### This example shows the motivation for stripping leading and trailing spaces:

Example 330:
```markdown
` `` `
```

#### Note that only one space is stripped:

Example 331:
```markdown
`  ``  `
```

#### The stripping only happens if the space is on both sides of the string:

Example 332:
```markdown
` a`
```

#### Only spaces, and not unicode whitespace in general, are stripped in this way:

Example 333:
```markdown
` b `
```

#### No stripping occurs if the code span contains only spaces:

Example 334:
```markdown
` `
`  `
```

#### Line endings are treated like spaces:

Example 335:
```markdown
``
foo
bar  
baz
``
```

Example 336:
```markdown
``
foo 
``
```

#### Interior spaces are not collapsed:

Example 337:
```markdown
`foo   bar 
baz`
```

#### Note that backslash escapes do not work in code spans. All backslashes are treated literally:

Example 338:
```markdown
`foo\`bar`
```

#### Backslash escapes are never needed, because one can always choose a string of n backtick characters as delimiters, where the code does not contain any strings of exactly n backtick characters.

Example 339:
```markdown
``foo`bar``
```

Example 340:
```markdown
` foo `` bar `
```

#### Code span backticks have higher precedence than any other inline constructs except HTML tags and autolinks. Thus, for example, this is not parsed as emphasized text, since the second * is part of a code span:

Example 341:
```markdown
*foo`*`
```

#### And this is not parsed as a link:

Example 342:
```markdown
[not a `link](/foo`)
```

#### Code spans, HTML tags, and autolinks have the same precedence. Thus, this is code:

Example 343:
```markdown
`<a href="`">`
```

#### But this is an HTML tag:

Example 344:
```markdown
<a href="`">`
```

#### And this is code:

Example 345:
```markdown
`<https://foo.bar.`baz>`
```

#### But this is an autolink:

Example 346:
```markdown
<https://foo.bar.`baz>`
```

#### When a backtick string is not closed by a matching backtick string, we just have literal backticks:

Example 347:
````markdown
```foo``
````

Example 348:
```markdown
`foo
```

#### The following case also illustrates the need for opening and closing backtick strings to be equal in length:

Example 349:
```markdown
`foo``bar``
```

## 6.2 Emphasis and strong emphasis

#### Rule 1:

Example 350:
```markdown
*foo bar*
```

#### This is not emphasis, because the opening * is followed by whitespace, and hence not part of a left-flanking delimiter run:

Example 351:
```markdown
a * foo bar*
```

#### This is not emphasis, because the opening * is preceded by an alphanumeric and followed by punctuation, and hence not part of a left-flanking delimiter run:

Example 352:
```markdown
a*"foo"*
```

#### Unicode nonbreaking spaces count as whitespace, too:

Example 353:
```markdown
* a *
```

#### Unicode symbols count as punctuation, too:

Example 354:
```markdown
*$*alpha.

*£*bravo.

*€*charlie.
```

#### Intraword emphasis with * is permitted:

Example 355:
```markdown
foo*bar*
```

Example 356:
```markdown
5*6*78
```

#### Rule 2:

Example 357:
```markdown
_foo bar_
```

#### This is not emphasis, because the opening _ is followed by whitespace:

Example 358:
```markdown
_ foo bar_
```

#### This is not emphasis, because the opening _ is preceded by an alphanumeric and followed by punctuation:

Example 359:
```markdown
a_"foo"_
```

#### Emphasis with _ is not allowed inside words:

Example 360:
```markdown
foo_bar_
```

Example 361:
```markdown
5_6_78
```

Example 362:
```markdown
пристаням_стремятся_
```

#### Here _ does not generate emphasis, because the first delimiter run is right-flanking and the second left-flanking:

Example 363:
```markdown
aa_"bb"_cc
```

#### This is emphasis, even though the opening delimiter is both left- and right-flanking, because it is preceded by punctuation:

Example 364:
```markdown
foo-_(bar)_
```

#### This is not emphasis, because the closing delimiter does not match the opening delimiter:

Example 365:
```markdown
_foo*
```

#### This is not emphasis, because the closing * is preceded by whitespace:

Example 366:
```markdown
*foo bar *
```

#### A line ending also counts as whitespace:

Example 367:
```markdown
*foo bar
*
```

#### This is not emphasis, because the second * is preceded by punctuation and followed by an alphanumeric (hence it is not part of a right-flanking delimiter run:

Example 368:
```markdown
*(*foo)
```

#### The point of this restriction is more easily appreciated with this example:

Example 369:
```markdown
*(*foo*)*
```

#### Intraword emphasis with * is allowed:

Example 370:
```markdown
*foo*bar
```

#### This is not emphasis, because the closing _ is preceded by whitespace:

Example 371:
```markdown
_foo bar _
```

#### This is not emphasis, because the second _ is preceded by punctuation and followed by an alphanumeric:

Example 372:
```markdown
_(_foo)
```

#### This is emphasis within emphasis:

Example 373:
```markdown
_(_foo_)_
```

#### Intraword emphasis is disallowed for _:

Example 374:
```markdown
_foo_bar
```

Example 375:
```markdown
_пристаням_стремятся
```

Example 376:
```markdown
_foo_bar_baz_
```

#### This is emphasis, even though the closing delimiter is both left- and right-flanking, because it is followed by punctuation:

Example 377:
```markdown
_(bar)_.
```

#### Rule 5:

Example 378:
```markdown
**foo bar**
```

#### This is not strong emphasis, because the opening delimiter is followed by whitespace:

Example 379:
```markdown
** foo bar**
```

#### This is not strong emphasis, because the opening ** is preceded by an alphanumeric and followed by punctuation, and hence not part of a left-flanking delimiter run:

Example 380:
```markdown
a**"foo"**
```

#### Intraword strong emphasis with ** is permitted:

Example 381:
```markdown
foo**bar**
```

#### Rule 6:

Example 382:
```markdown
__foo bar__
```

#### This is not strong emphasis, because the opening delimiter is followed by whitespace:

Example 383:
```markdown
__ foo bar__
```

#### A line ending counts as whitespace:

Example 384:
```markdown
__
foo bar__
```

#### This is not strong emphasis, because the opening __ is preceded by an alphanumeric and followed by punctuation:

Example 385:
```markdown
a__"foo"__
```

#### Intraword strong emphasis is forbidden with __:

Example 386:
```markdown
foo__bar__
```

Example 387:
```markdown
5__6__78
```

Example 388:
```markdown
пристаням__стремятся__
```

Example 389:
```markdown
__foo, __bar__, baz__
```

#### This is strong emphasis, even though the opening delimiter is both left- and right-flanking, because it is preceded by punctuation:

Example 390:
```markdown
foo-__(bar)__
```

#### This is not strong emphasis, because the closing delimiter is preceded by whitespace:

Example 391:
```markdown
**foo bar **
```

#### This is not strong emphasis, because the second ** is preceded by punctuation and followed by an alphanumeric:

Example 392:
```markdown
**(**foo)
```

#### The point of this restriction is more easily appreciated with these examples:

Example 393:
```markdown
*(**foo**)*
```

Example 394:
```markdown
**Gomphocarpus (*Gomphocarpus physocarpus*, syn.
*Asclepias physocarpa*)**
```

Example 395:
```markdown
**foo "*bar*" foo**
```

#### Intraword emphasis:

Example 396:
```markdown
**foo**bar
```

#### This is not strong emphasis, because the closing delimiter is preceded by whitespace:

Example 397:
```markdown
__foo bar __
```

#### This is not strong emphasis, because the second __ is preceded by punctuation and followed by an alphanumeric:

Example 398:
```markdown
__(__foo)
```

#### The point of this restriction is more easily appreciated with this example:

Example 399:
```markdown
_(__foo__)_
```

#### Intraword strong emphasis is forbidden with __:

Example 400:
```markdown
__foo__bar
```

Example 401:
```markdown
__пристаням__стремятся
```

Example 402:
```markdown
__foo__bar__baz__
```

#### This is strong emphasis, even though the closing delimiter is both left- and right-flanking, because it is followed by punctuation:

Example 403:
```markdown
__(bar)__.
```

#### Any nonempty sequence of inline elements can be the contents of an emphasized span.

Example 404:
```markdown
*foo [bar](/url)*
```

Example 405:
```markdown
*foo
bar*
```

#### In particular, emphasis and strong emphasis can be nested inside emphasis:

Example 406:
```markdown
_foo __bar__ baz_
```

Example 407:
```markdown
_foo _bar_ baz_
```

Example 408:
```markdown
__foo_ bar_
```

Example 409:
```markdown
*foo *bar**
```

Example 410:
```markdown
*foo **bar** baz*
```

Example 411:
```markdown
*foo**bar**baz*
```

#### For the same reason, we don’t get two consecutive emphasis sections in this example:

Example 412:
```markdown
*foo**bar*
```

#### The same condition ensures that the following cases are all strong emphasis nested inside emphasis, even when the interior whitespace is omitted:

Example 413:
```markdown
***foo** bar*
```

Example 414:
```markdown
*foo **bar***
```

Example 415:
```markdown
*foo**bar***
```

#### When the lengths of the interior closing and opening delimiter runs are both multiples of 3, though, they can match to create emphasis:

Example 416:
```markdown
foo***bar***baz
```

Example 417:
```markdown
foo******bar*********baz
```

#### Indefinite levels of nesting are possible:

Example 418:
```markdown
*foo **bar *baz* bim** bop*
```

Example 419:
```markdown
*foo [*bar*](/url)*
```

#### There can be no empty emphasis or strong emphasis:

Example 420:
```markdown
** is not an empty emphasis
```

Example 421:
```markdown
**** is not an empty strong emphasis
```

#### Any nonempty sequence of inline elements can be the contents of an strongly emphasized span.

Example 422:
```markdown
**foo [bar](/url)**
```

Example 423:
```markdown
**foo
bar**
```

#### In particular, emphasis and strong emphasis can be nested inside strong emphasis:

Example 424:
```markdown
__foo _bar_ baz__
```

Example 425:
```markdown
__foo __bar__ baz__
```

Example 426:
```markdown
____foo__ bar__
```

Example 427:
```markdown
**foo **bar****
```

Example 428:
```markdown
**foo *bar* baz**
```

Example 429:
```markdown
**foo*bar*baz**
```

Example 430:
```markdown
***foo* bar**
```

Example 431:
```markdown
**foo *bar***
```

#### Indefinite levels of nesting are possible:

Example 432:
```markdown
**foo *bar **baz**
bim* bop**
```

Example 433:
```markdown
**foo [*bar*](/url)**
```

#### There can be no empty emphasis or strong emphasis:

Example 434:
```markdown
__ is not an empty emphasis
```

Example 435:
```markdown
____ is not an empty strong emphasis
```

#### Rule 11:

Example 436:
```markdown
foo ***
```

Example 437:
```markdown
foo *\**
```

Example 438:
```markdown
foo *_*
```

Example 439:
```markdown
foo *****
```

Example 440:
```markdown
foo **\***
```

Example 441:
```markdown
foo **_**
```

#### Note that when delimiters do not match evenly, Rule 11 determines that the excess literal * characters will appear outside of the emphasis, rather than inside it:

Example 442:
```markdown
**foo*
```

Example 443:
```markdown
*foo**
```

Example 444:
```markdown
***foo**
```

Example 445:
```markdown
****foo*
```

Example 446:
```markdown
**foo***
```

Example 447:
```markdown
*foo****
```

#### Rule 12:

Example 448:
```markdown
foo ___
```

Example 449:
```markdown
foo _\__
```

Example 450:
```markdown
foo _*_
```

Example 451:
```markdown
foo _____
```

Example 452:
```markdown
foo __\___
```

Example 453:
```markdown
foo __*__
```

Example 454:
```markdown
__foo_
```

#### Note that when delimiters do not match evenly, Rule 12 determines that the excess literal _ characters will appear outside of the emphasis, rather than inside it:

Example 455:
```markdown
_foo__
```

Example 456:
```markdown
___foo__
```

Example 457:
```markdown
____foo_
```

Example 458:
```markdown
__foo___
```

Example 459:
```markdown
_foo____
```

#### Rule 13 implies that if you want emphasis nested directly inside emphasis, you must use different delimiters:

Example 460:
```markdown
**foo**
```

Example 461:
```markdown
*_foo_*
```

Example 462:
```markdown
__foo__
```

Example 463:
```markdown
_*foo*_
```

#### However, strong emphasis within strong emphasis is possible without switching delimiters:

Example 464:
```markdown
****foo****
```

Example 465:
```markdown
____foo____
```

#### Rule 13 can be applied to arbitrarily long sequences of delimiters:

Example 466:
```markdown
******foo******
```

#### Rule 14:

Example 467:
```markdown
***foo***
```

Example 468:
```markdown
_____foo_____
```

#### Rule 15:

Example 469:
```markdown
*foo _bar* baz_
```

Example 470:
```markdown
*foo __bar *baz bim__ bam*
```

#### Rule 16:

Example 471:
```markdown
**foo **bar baz**
```

Example 472:
```markdown
*foo *bar baz*
```

#### Rule 17:

Example 473:
```markdown
*[bar*](/url)
```

Example 474:
```markdown
_foo [bar_](/url)
```

Example 475:
```markdown
*<img src="foo" title="*"/>
```

Example 476:
```markdown
**<a href="**">
```

Example 477:
```markdown
__<a href="__">
```

Example 478:
```markdown
*a `*`*
```

Example 479:
```markdown
_a `_`_
```

Example 480:
```markdown
**a<https://foo.bar/?q=**>
```

Example 481:
```markdown
__a<https://foo.bar/?q=__>
```

## 6.3 Links

#### Here is a simple inline link:

Example 482:
```markdown
[link](/uri "title")
```

#### The title, the link text and even the destination may be omitted:

Example 483:
```markdown
[link](/uri)
```

Example 484:
```markdown
[](./target.md)
```

Example 485:
```markdown
[link]()
```

Example 486:
```markdown
[link](<>)
```

Example 487:
```markdown
[]()
```

#### The destination can only contain spaces if it is enclosed in pointy brackets:

Example 488:
```markdown
[link](/my uri)
```

Example 489:
```markdown
[link](</my uri>)
```

#### The destination cannot contain line endings, even if enclosed in pointy brackets:

Example 490:
```markdown
[link](foo
bar)
```

Example 491:
```markdown
[link](<foo
bar>)
```

#### The destination can contain ) if it is enclosed in pointy brackets:

Example 492:
```markdown
[a](<b)c>)
```

#### Pointy brackets that enclose links must be unescaped:

Example 493:
```markdown
[link](<foo\>)
```

#### These are not links, because the opening pointy bracket is not matched properly:

Example 494:
```markdown
[a](<b)c
[a](<b)c>
[a](<b>c)
```

#### Parentheses inside the link destination may be escaped:

Example 495:
```markdown
[link](\(foo\))
```

#### Any number of parentheses are allowed without escaping, as long as they are balanced:

Example 496:
```markdown
[link](foo(and(bar)))
```

#### However, if you have unbalanced parentheses, you need to escape or use the &lt;...&gt; form:

Example 497:
```markdown
[link](foo(and(bar))
```

Example 498:
```markdown
[link](foo\(and\(bar\))
```

Example 499:
```markdown
[link](<foo(and(bar)>)
```

#### Parentheses and other symbols can also be escaped, as usual in Markdown:

Example 500:
```markdown
[link](foo\)\:)
```

#### A link can contain fragment identifiers and queries:

Example 501:
```markdown
[link](#fragment)

[link](https://example.com#fragment)

[link](https://example.com?foo=3#frag)
```

#### Note that a backslash before a non-escapable character is just a backslash:

Example 502:
```markdown
[link](foo\bar)
```

Example 503:
```markdown
[link](foo%20b&auml;)
```

#### Note that, because titles can often be parsed as destinations, if you try to omit the destination and keep the title, you’ll get unexpected results:

Example 504:
```markdown
[link]("title")
```

#### Titles may be in single quotes, double quotes, or parentheses:

Example 505:
```markdown
[link](/url "title")
[link](/url 'title')
[link](/url (title))
```

#### Backslash escapes and entity and numeric character references may be used in titles:

Example 506:
```markdown
[link](/url "title \"&quot;")
```

#### Titles must be separated from the link using spaces, tabs, and up to one line ending. Other Unicode whitespace like non-breaking space doesn’t work.

Example 507:
```markdown
[link](/url "title")
```

#### Nested balanced quotes are not allowed without escaping:

Example 508:
```markdown
[link](/url "title "and" title")
```

#### But it is easy to work around this by using a different quote type:

Example 509:
```markdown
[link](/url 'title "and" title')
```

#### Spaces, tabs, and up to one line ending is allowed around the destination and title:

Example 510:
```markdown
[link](   /uri
  "title"  )
```

#### But it is not allowed between the link text and the following parenthesis:

Example 511:
```markdown
[link] (/uri)
```

#### The link text may contain balanced brackets, but not unbalanced ones, unless they are escaped:

Example 512:
```markdown
[link [foo [bar]]](/uri)
```

Example 513:
```markdown
[link] bar](/uri)
```

Example 514:
```markdown
[link [bar](/uri)
```

Example 515:
```markdown
[link \[bar](/uri)
```

#### The link text may contain inline content:

Example 516:
```markdown
[link *foo **bar** `#`*](/uri)
```

Example 517:
```markdown
[![moon](moon.jpg)](/uri)
```

#### However, links may not contain other links, at any level of nesting.

Example 518:
```markdown
[foo [bar](/uri)](/uri)
```

Example 519:
```markdown
[foo *[bar [baz](/uri)](/uri)*](/uri)
```

Example 520:
```markdown
![[[foo](uri1)](uri2)](uri3)
```

#### These cases illustrate the precedence of link text grouping over emphasis grouping:

Example 521:
```markdown
*[foo*](/uri)
```

Example 522:
```markdown
[foo *bar](baz*)
```

#### Note that brackets that aren’t part of links do not take precedence:

Example 523:
```markdown
*foo [bar* baz]
```

#### These cases illustrate the precedence of HTML tags, code spans, and autolinks over link grouping:

Example 524:
```markdown
[foo <bar attr="](baz)">
```

Example 525:
```markdown
[foo`](/uri)`
```

Example 526:
```markdown
[foo<https://example.com/?search=](uri)>
```

#### Here is a simple example:

Example 527:
```markdown
[foo][bar]

[bar]: /url "title"
```

#### The link text may contain balanced brackets, but not unbalanced ones, unless they are escaped:

Example 528:
```markdown
[link [foo [bar]]][ref]

[ref]: /uri
```

Example 529:
```markdown
[link \[bar][ref]

[ref]: /uri
```

#### The link text may contain inline content:

Example 530:
```markdown
[link *foo **bar** `#`*][ref]

[ref]: /uri
```

Example 531:
```markdown
[![moon](moon.jpg)][ref]

[ref]: /uri
```

#### However, links may not contain other links, at any level of nesting.

Example 532:
```markdown
[foo [bar](/uri)][ref]

[ref]: /uri
```

Example 533:
```markdown
[foo *bar [baz][ref]*][ref]

[ref]: /uri
```

#### The following cases illustrate the precedence of link text grouping over emphasis grouping:

Example 534:
```markdown
*[foo*][ref]

[ref]: /uri
```

Example 535:
```markdown
[foo *bar][ref]*

[ref]: /uri
```

#### These cases illustrate the precedence of HTML tags, code spans, and autolinks over link grouping:

Example 536:
```markdown
[foo <bar attr="][ref]">

[ref]: /uri
```

Example 537:
```markdown
[foo`][ref]`

[ref]: /uri
```

Example 538:
```markdown
[foo<https://example.com/?search=][ref]>

[ref]: /uri
```

#### Matching is case-insensitive:

Example 539:
```markdown
[foo][BaR]

[bar]: /url "title"
```

#### Unicode case fold is used:

Example 540:
```markdown
[ẞ]

[SS]: /url
```

#### Consecutive internal spaces, tabs, and line endings are treated as one space for purposes of determining matching:

Example 541:
```markdown
[Foo
  bar]: /url

[Baz][Foo bar]
```

#### No spaces, tabs, or line endings are allowed between the link text and the link label:

Example 542:
```markdown
[foo] [bar]

[bar]: /url "title"
```

Example 543:
```markdown
[foo]
[bar]

[bar]: /url "title"
```

#### When there are multiple matching link reference definitions, the first is used:

Example 544:
```markdown
[foo]: /url1

[foo]: /url2

[bar][foo]
```

#### Note that matching is performed on normalized strings, not parsed inline content. So the following does not match, even though the labels define equivalent inline content:

Example 545:
```markdown
[bar][foo\!]

[foo!]: /url
```

#### Link labels cannot contain brackets, unless they are backslash-escaped:

Example 546:
```markdown
[foo][ref[]

[ref[]: /uri
```

Example 547:
```markdown
[foo][ref[bar]]

[ref[bar]]: /uri
```

Example 548:
```markdown
[[[foo]]]

[[[foo]]]: /url
```

Example 549:
```markdown
[foo][ref\[]

[ref\[]: /uri
```

#### Note that in this example ] is not backslash-escaped:

Example 550:
```markdown
[bar\\]: /uri

[bar\\]
```

#### A link label must contain at least one character that is not a space, tab, or line ending:

Example 551:
```markdown
[]

[]: /uri
```

Example 552:
```markdown
[
 ]

[
 ]: /uri
```

Example 553:
```markdown
[foo][]

[foo]: /url "title"
```

Example 554:
```markdown
[*foo* bar][]

[*foo* bar]: /url "title"
```

#### The link labels are case-insensitive:

Example 555:
```markdown
[Foo][]

[foo]: /url "title"
```

#### As with full reference links, spaces, tabs, or line endings are not allowed between the two sets of brackets:

Example 556:
```markdown
[foo] 
[]

[foo]: /url "title"
```

Example 557:
```markdown
[foo]

[foo]: /url "title"
```

Example 558:
```markdown
[*foo* bar]

[*foo* bar]: /url "title"
```

Example 559:
```markdown
[[*foo* bar]]

[*foo* bar]: /url "title"
```

Example 560:
```markdown
[[bar [foo]

[foo]: /url
```

#### The link labels are case-insensitive:

Example 561:
```markdown
[Foo]

[foo]: /url "title"
```

#### A space after the link text should be preserved:

Example 562:
```markdown
[foo] bar

[foo]: /url
```

#### If you just want bracketed text, you can backslash-escape the opening bracket to avoid links:

Example 563:
```markdown
\[foo]

[foo]: /url "title"
```

#### Note that this is a link, because a link label ends with the first following closing bracket:

Example 564:
```markdown
[foo*]: /url

*[foo*]
```

#### Full and collapsed references take precedence over shortcut references:

Example 565:
```markdown
[foo][bar]

[foo]: /url1
[bar]: /url2
```

Example 566:
```markdown
[foo][]

[foo]: /url1
```

#### Inline links also take precedence:

Example 567:
```markdown
[foo]()

[foo]: /url1
```

Example 568:
```markdown
[foo](not a link)

[foo]: /url1
```

#### In the following case [bar][baz] is parsed as a reference, [foo] as normal text:

Example 569:
```markdown
[foo][bar][baz]

[baz]: /url
```

#### Here, though, [foo][bar] is parsed as a reference, since [bar] is defined:

Example 570:
```markdown
[foo][bar][baz]

[baz]: /url1
[bar]: /url2
```

#### Here [foo] is not parsed as a shortcut reference, because it is followed by a link label (even though [bar] is not defined):

Example 571:
```markdown
[foo][bar][baz]

[baz]: /url1
[foo]: /url2
```

## 6.4 Images

Example 572:
```markdown
![foo](/url "title")
```

Example 573:
```markdown
![foo *bar*]

[foo *bar*]: train.jpg "train & tracks"
```

Example 574:
```markdown
![foo ![bar](/url)](/url2)
```

Example 575:
```markdown
![foo [bar](/url)](/url2)
```

Example 576:
```markdown
![foo *bar*][]

[foo *bar*]: train.jpg "train & tracks"
```

Example 577:
```markdown
![foo *bar*][foobar]

[FOOBAR]: train.jpg "train & tracks"
```

Example 578:
```markdown
![foo](train.jpg)
```

Example 579:
```markdown
My ![foo bar](/path/to/train.jpg  "title"   )
```

Example 580:
```markdown
![foo](<url>)
```

Example 581:
```markdown
![](/url)
```

#### Reference-style:

Example 582:
```markdown
![foo][bar]

[bar]: /url
```

Example 583:
```markdown
![foo][bar]

[BAR]: /url
```

#### Collapsed:

Example 584:
```markdown
![foo][]

[foo]: /url "title"
```

Example 585:
```markdown
![*foo* bar][]

[*foo* bar]: /url "title"
```

#### The labels are case-insensitive:

Example 586:
```markdown
![Foo][]

[foo]: /url "title"
```

#### As with reference links, spaces, tabs, and line endings, are not allowed between the two sets of brackets:

Example 587:
```markdown
![foo] 
[]

[foo]: /url "title"
```

#### Shortcut:

Example 588:
```markdown
![foo]

[foo]: /url "title"
```

Example 589:
```markdown
![*foo* bar]

[*foo* bar]: /url "title"
```

#### Note that link labels cannot contain unescaped brackets:

Example 590:
```markdown
![[foo]]

[[foo]]: /url "title"
```

#### The link labels are case-insensitive:

Example 591:
```markdown
![Foo]

[foo]: /url "title"
```

#### If you just want a literal ! followed by bracketed text, you can backslash-escape the opening [:

Example 592:
```markdown
!\[foo]

[foo]: /url "title"
```

#### If you want a link after a literal !, backslash-escape the !:

Example 593:
```markdown
\![foo]

[foo]: /url "title"
```

## 6.5 Autolinks

#### Here are some valid autolinks:

Example 594:
```markdown
<http://foo.bar.baz>
```

Example 595:
```markdown
<https://foo.bar.baz/test?q=hello&id=22&boolean>
```

Example 596:
```markdown
<irc://foo.bar:2233/baz>
```

#### Uppercase is also fine:

Example 597:
```markdown
<MAILTO:FOO@BAR.BAZ>
```

#### Note that many strings that count as absolute URIs for purposes of this spec are not valid URIs, because their schemes are not registered or because of other problems with their syntax:

Example 598:
```markdown
<a+b+c:d>
```

Example 599:
```markdown
<made-up-scheme://foo,bar>
```

Example 600:
```markdown
<https://../>
```

Example 601:
```markdown
<localhost:5001/foo>
```

#### Spaces are not allowed in autolinks:

Example 602:
```markdown
<https://foo.bar/baz bim>
```

#### Backslash-escapes do not work inside autolinks:

Example 603:
```markdown
<https://example.com/\[\>
```

#### Examples of email autolinks:

Example 604:
```markdown
<foo@bar.example.com>
```

Example 605:
```markdown
<foo+special@Bar.baz-bar0.com>
```

#### Backslash-escapes do not work inside email autolinks:

Example 606:
```markdown
<foo\+@bar.example.com>
```

#### These are not autolinks:

Example 607:
```markdown
<>
```

Example 608:
```markdown
< https://foo.bar >
```

Example 609:
```markdown
<m:abc>
```

Example 610:
```markdown
<foo.bar.baz>
```

Example 611:
```markdown
https://example.com
```

Example 612:
```markdown
foo@bar.example.com
```

## 6.6 Raw HTML

#### Here are some simple open tags:

Example 613:
```markdown
<a><bab><c2c>
```

#### Empty elements:

Example 614:
```markdown
<a/><b2/>
```

#### Whitespace is allowed:

Example 615:
```markdown
<a  /><b2
data="foo" >
```

#### With attributes:

Example 616:
```markdown
<a foo="bar" bam = 'baz <em>"</em>'
_boolean zoop:33=zoop:33 />
```

#### Custom tag names can be used:

Example 617:
```markdown
Foo <responsive-image src="foo.jpg" />
```

#### Illegal tag names, not parsed as HTML:

Example 618:
```markdown
<33> <__>
```

#### Illegal attribute names:

Example 619:
```markdown
<a h*#ref="hi">
```

#### Illegal attribute values:

Example 620:
```markdown
<a href="hi'> <a href=hi'>
```

#### Illegal whitespace:

Example 621:
```markdown
< a><
foo><bar/ >
<foo bar=baz
bim!bop />
```

#### Missing whitespace:

Example 622:
```markdown
<a href='bar'title=title>
```

#### Closing tags:

Example 623:
```markdown
</a></foo >
```

#### Illegal attributes in closing tag:

Example 624:
```markdown
</a href="foo">
```

#### Comments:

Example 625:
```markdown
foo <!-- this is a --
comment - with hyphens -->
```

Example 626:
```markdown
foo <!--> foo -->

foo <!---> foo -->
```

#### Processing instructions:

Example 627:
```markdown
foo <?php echo $a; ?>
```

#### Declarations:

Example 628:
```markdown
foo <!ELEMENT br EMPTY>
```

#### CDATA sections:

Example 629:
```markdown
foo <![CDATA[>&<]]>
```

#### Entity and numeric character references are preserved in HTML attributes:

Example 630:
```markdown
foo <a href="&ouml;">
```

#### Backslash escapes do not work in HTML attributes:

Example 631:
```markdown
foo <a href="\*">
```

Example 632:
```markdown
<a href="\"">
```

## 6.7 Hard line breaks

#### A line ending (not in a code span or HTML tag) that is preceded by two or more spaces and does not occur at the end of a block is parsed as a hard line break (rendered in HTML as a &lt;br /&gt; tag):

Example 633:
```markdown
foo  
baz
```

#### For a more visible alternative, a backslash before the line ending may be used instead of two or more spaces:

Example 634:
```markdown
foo\
baz
```

#### More than two spaces can be used:

Example 635:
```markdown
foo       
baz
```

#### Leading spaces at the beginning of the next line are ignored:

Example 636:
```markdown
foo  
     bar
```

Example 637:
```markdown
foo\
     bar
```

#### Hard line breaks can occur inside emphasis, links, and other constructs that allow inline content:

Example 638:
```markdown
*foo  
bar*
```

Example 639:
```markdown
*foo\
bar*
```

#### Hard line breaks do not occur inside code spans

Example 640:
```markdown
`code  
span`
```

Example 641:
```markdown
`code\
span`
```

#### or HTML tags:

Example 642:
```markdown
<a href="foo  
bar">
```

Example 643:
```markdown
<a href="foo\
bar">
```

#### Hard line breaks are for separating inline content within a block. Neither syntax for hard line breaks works at the end of a paragraph or other block element:

Example 644:
```markdown
foo\
```

Example 645:
```markdown
foo  
```

Example 646:
```markdown
### foo\
```

Example 647:
```markdown
### foo  
```

## 6.8 Soft line breaks

Example 648:
```markdown
foo
baz
```

#### Spaces at the end of the line and beginning of the next line are removed:

Example 649:
```markdown
foo 
 baz
```

## 6.9 Textual content

#### Any characters not given an interpretation by the above rules will be parsed as plain textual content.

Example 650:
```markdown
hello $.;'there
```

Example 651:
```markdown
Foo χρῆν
```

#### Internal spaces are preserved verbatim:

Example 652:
```markdown
Multiple     spaces
```
