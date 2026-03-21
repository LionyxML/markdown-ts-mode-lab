# markdown-ts-mode Feature Development Control

Complete feature list derived from the tree-sitter-markdown parser
(split_parser branch). Every node type and capability the parser
exposes is listed here so we can track what markdown-ts-mode supports.

---

## 1. Block-Level - CommonMark

### Document Structure

- [x] `document` root node handling
- [x] `section` grouping (heading + its content, nested sections)

### ATX Headings

- [x] ATX heading fontification (levels 1–6)
- [x] ATX heading markers (`#` through `######`)
- [x] ATX heading closing hashes
- [x] Heading content parsed via inline parser

### Setext Headings

- [x] Setext heading level 1 (`===` underline)
- [x] Setext heading level 2 (`---` underline)
- [x] Setext underline fontification
- [x] Multi-line setext heading content

### Paragraphs

- [x] Paragraph recognition

### Thematic Breaks

- [x] Thematic break (`***`, `---`, `___`)
- [x] Thematic break fontification / overlay

### Block Quotes

- [x] Block quote recognition and fontification
- [x] Block quote marker (`>`) fontification
- [x] Nested block quotes
- [x] Block quotes containing all block types

### Lists

- [x] Unordered list marker: minus (`-`)
- [x] Unordered list marker: plus (`+`)
- [x] Unordered list marker: star (`*`)
- [x] Ordered list marker: dot (`1.`)
- [x] Ordered list marker: parenthesis (`1)`)
- [x] Ordered list starting from arbitrary number
- [x] List item nesting via indentation
- [x] List items containing all block types (paragraphs, quotes, code, etc.)

### Fenced Code Blocks

- [x] Backtick fenced code blocks
- [x] Tilde fenced code blocks (`~~~`)
- [x] `info_string` / `language` extraction
- [x] `code_fence_content` fontification
- [x] Language-specific fontification inside code blocks
- [x] Language-specific indentation inside code blocks
- [x] Non-tree-sitter mode fontification (e.g., `elisp` via `emacs-lisp-mode`)
- [x] Opening/closing fence delimiter fontification

### Indented Code Blocks

- [x] Indented code block recognition (4+ spaces)
- [x] Indented code block fontification

### HTML Blocks

- [x] HTML block type 1 (`<pre>`, `<script>`, `<style>`, `<textarea>`)
- [x] HTML block type 2 (`<!-- -->` comments)
- [x] HTML block type 3 (`<?` processing instructions)
- [x] HTML block type 5 (`<![CDATA[`)
- [x] HTML block type 6 (block-level HTML elements)
- [x] HTML block type 7 (complete open/close tag on its own line)

### Link Reference Definitions

- [x] Link reference definition recognition
- [x] `link_label` handling
- [x] `link_destination` (bare URL and `<angle-bracketed>`)
- [x] `link_title` (`"double"`, `'single'`, `(parenthesized)`)
- [x] Multi-line link reference definitions

---

## 2. Inline-Level - CommonMark

### Emphasis (Italic)

- [x] Star emphasis (`*text*`)
- [x] Underscore emphasis (`_text_`)
- [x] Emphasis delimiter fontification / hiding
- [x] Nested emphasis

### Strong Emphasis (Bold)

- [x] Star strong emphasis (`**text**`)
- [x] Underscore strong emphasis (`__text__`)
- [x] Strong emphasis delimiter fontification / hiding
- [x] Nested strong emphasis

### Code Spans

- [x] Single backtick code span
- [x] Multi-backtick code span
- [x] Code span delimiter fontification
- [x] Code span face

### Links

- [x] Inline link (`[text](url "title")`)
- [x] Full reference link (`[text][label]`)
- [x] Collapsed reference link (`[text][]`)
- [x] Shortcut link (`[text]`)
- [x] Link text fontification
- [x] Link destination fontification
- [x] Link title fontification
- [x] Clickable link buttons (browse-url)
- [x] File path links (find-file)
- [x] Link destination hiding when markup is hidden

### Images

- [x] Inline image (`![alt](url "title")`)
- [x] Full reference image (`![alt][label]`)
- [x] Collapsed reference image (`![alt][]`)
- [x] Shortcut reference image (`![alt]`)
- [x] Image description fontification

### Autolinks

- [x] URI autolink (`<https://...>`)
- [x] Email autolink (`<user@domain>`)
- [x] Autolink fontification as clickable button
- [x] Angle bracket hiding when markup is hidden

### Inline HTML

- [x] Open tags with attributes
- [x] Closing tags
- [x] Self-closing tags
- [x] Inline HTML comments (`<!-- -->`)
- [x] Inline processing instructions (`<? ?>`)
- [x] Inline declarations (`<!TYPE ...>`)
- [x] Inline CDATA sections (`<![CDATA[ ]]>`)

### Hard Line Breaks

- [ ] Backslash hard line break (`\` before newline)
- [ ] Trailing spaces hard line break (2+ spaces before newline)

### Backslash Escapes

- [x] Backslash escape recognition (all ASCII punctuation)
- [x] Backslash hiding when markup is hidden

### Entity and Numeric Character References

- [ ] Named HTML entity references (`&amp;`, `&copy;`, etc.)
- [ ] Decimal numeric character references (`&#123;`)
- [ ] Hexadecimal numeric character references (`&#x1F4A9;`)

---

## 3. GFM (GitHub Flavored Markdown) Extensions

### Strikethrough

- [x] Strikethrough (`~~text~~`)
- [x] Strikethrough delimiter fontification / hiding
- [x] Strikethrough face (`:strike-through t`)

### Pipe Tables

- [x] Pipe table recognition
- [x] Table header row fontification
- [x] Table delimiter row recognition
- [x] Table data row fontification
- [x] Table cell fontification
- [x] Delimiter cell fontification
- [ ] Left alignment marker (`:---`)
- [ ] Right alignment marker (`---:`)
- [ ] Center alignment marker (`:---:`)
- [x] Escaped pipes within cells
- [ ] Table editing (create, align, add/remove rows and columns)

### Task Lists

- [x] Checked task list marker (`[x]` / `[X]`)
- [x] Unchecked task list marker (`[ ]`)
- [x] Task list checkbox fontification
- [x] Nested task lists

---

## 4. Other Extensions (Non-GFM)

### YAML Front Matter

- [x] YAML metadata block (`---` delimited at document start)
- [x] YAML fontification via embedded parser

### TOML Front Matter

- [x] TOML metadata block (`+++` delimited at document start)
- [x] TOML fontification via embedded parser

### LaTeX / Math

Requires grammar compiled with `EXTENSION_LATEX=1` (disabled by default).
Rules can be added safely - they won't match if the extension is absent.

- [ ] Inline math (`$...$`)
- [ ] Display math (`$$...$$`)
- [ ] LaTeX delimiter fontification
- [ ] LaTeX content handling (no markdown processing inside)

### Wiki Links

Requires grammar compiled with `EXTENSION_WIKI_LINK=1` (disabled by default).
Rules can be added safely - they won't match if the extension is absent.

- [ ] Wiki link (`[[destination]]`)
- [ ] Wiki link with display text (`[[destination|text]]`)
- [ ] Wiki link fragment identifiers (`[[page#section]]`)

### Tags

Requires grammar compiled with `EXTENSION_TAGS=1` (disabled by default).
Rules can be added safely - they won't match if the extension is absent.

- [ ] Hashtag-style tags (`#identifier`)
- [ ] Tag fontification

---

## 5. Editing / Mode Features (not parser-derived)

### Filling

- [x] fill-paragraph respecting list items
- [x] fill-paragraph skipping code blocks
- [x] fill-paragraph skipping tables
- [x] fill-paragraph for HTML comments
- [x] fill-region over multiple paragraphs
- [x] Adaptive fill prefix for list items
- [ ] Auto-fill respecting markdown structure (lists, blocks)
- [ ] Filling inside code blocks in language mode

### Navigation

- [x] Imenu support for headings
- [x] Outline integration (`outline-minor-mode`)
- [ ] Navigate between headings (next/previous)
- [ ] Navigate between code blocks (next/previous)

### List Editing

- [ ] Auto-continue lists (RET inserts next item marker)
- [ ] Numbered list auto-increment
- [ ] List promotion / demotion
- [ ] List reordering (move up/down)
- [ ] List renumbering

### Heading Editing

- [ ] Heading promotion / demotion (apply to children)
- [ ] Heading reordering (move up/down)

### Block Editing

- [ ] Block quote wrapping / unwrapping
- [ ] Code block insertion (with language prompt)
- [ ] Commenting / uncommenting in code blocks in language mode

### Link Editing

- [ ] Link insertion helper
- [ ] Link/reference completion (completing-read for existing refs)

### Markup Visibility

- [x] Toggle markup hiding (`markdown-ts-toggle-hide-markup`)

### Visual Enhancements (overlays / rendering)

- [ ] Inline image preview
- [ ] Task list checkbox toggle (click to check/uncheck)
- [ ] Horizontal rule overlay (thematic break rendering)

### Other

- [x] Comment support (HTML comments)
- [ ] Mode menu item
- [ ] Markdown-aware kill/yank (respect block boundaries)
- [ ] Table of contents generation from headings
- [ ] Theme support for markdown-ts faces (modus-themes, etc.)
- [ ] Tests for delicate features
- [ ] Export to HTML / preview

### Parser Bugs

Bugs in the tree-sitter-markdown parser that we cannot fix on our side.

- [ ] HTML block type 4 (`<!` declarations like `<!DOCTYPE>`) - parser
      enters infinite loop on uppercase `<!DOCTYPE html>`. Lowercase
      `<!doctype html>` works as a
      workaround. [tree-sitter-markdown#233](https://github.com/tree-sitter-grammars/tree-sitter-markdown/issues/233)
- [ ] Footnote support: parser doesn't recognize footnotes; not
      CommonMark/GFM, no build flag; would need custom handling

---

## 6. Extension Build Flags Reference

| Extension                               | Env Var                       | Default  |
| --------------------------------------- | ----------------------------- | -------- |
| GFM (tables, strikethrough, task lists) | `NO_DEFAULT_EXTENSIONS` unset | enabled  |
| YAML front matter (`minus_metadata`)    | `NO_DEFAULT_EXTENSIONS` unset | enabled  |
| TOML front matter (`plus_metadata`)     | `NO_DEFAULT_EXTENSIONS` unset | enabled  |
| LaTeX / Math                            | `EXTENSION_LATEX` set         | disabled |
| Wiki Links                              | `EXTENSION_WIKI_LINK` set     | disabled |
| Tags                                    | `EXTENSION_TAGS` set          | disabled |
