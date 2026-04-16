# markdown-ts-mode-lab

This repository is a development workspace for `markdown-ts-mode`.

It contains files used to organize work, track features, and manually
test behavior while developing improvements to the mode.

It is intended as a companion resource for discussions and patches
submitted to `emacs-devel`.

## Contents

- `test.md`
  A comprehensive Markdown document used for manual testing and
  exploration.

  Covers:
  - CommonMark and GFM constructs
  - Parser edge cases and known limitations
  - Editing behavior (filling, navigation, list handling, etc.)

  Sections include inline comments describing what is being exercised.

- `features.md`
  A feature checklist derived from the tree-sitter-markdown parser.

  Tracks:
  - implemented features
  - missing functionality
  - extension-dependent behavior
  - parser limitations

- `patches.md`
  Tracks patches related to `markdown-ts-mode`.

  Includes:
  - debbugs links
  - review status
  - planned and in-progress work

- `demo/`
  A folder containing `test.md` rendered on the default theme and
  other themes, with the hide markup feature turned off (raw) and on.

## Upstream parser

This work is based on the tree-sitter Markdown grammar:

<https://github.com/tree-sitter-grammars/tree-sitter-markdown>

That parser:

- targets CommonMark with optional extensions (GFM, etc.)
- enables/disables features via compile-time flags
- is primarily designed for syntax highlighting, not full correctness

As a result:

- some behaviors in `test.md` reflect parser limitations
- not all Markdown constructs can be represented perfectly
- issues may originate from the parser rather than `markdown-ts-mode`

Where relevant, such cases are documented inline in `test.md`.

## Setup (Tree-sitter grammars)

To view `test.md` as intended, install the required grammars.

Run:

`M-x treesit-install-language-grammar ...`

Install the following:

- markdown
- markdown-inline
- yaml
- toml
- html
- c
- javascript
- python
- rust

Missing grammars will result in incorrect or incomplete fontification.
If you installed with the mode already initialized on the buffer,
re-start it with `M-x markdown-ts-mode RET`.

## Usage

Open `test.md` in Emacs using `markdown-ts-mode`.

The file is intended for:

- visual inspection (fontification, structure)
- interactive testing (filling, navigation, editing commands)

Compare behavior with:

- inline comments in the file
- screenshots in `screenshots/` (when relevant)

## Before reporting issues

Please keep in mind:

- `markdown-ts-mode` is under active development
- not all features listed in `feature_development_control.md` are
  implemented
- some behaviors are known limitations of the parser

Before reporting a bug:

1. Ensure all required grammars are installed
2. Check `feature_development_control.md` to confirm the feature is
   expected to work
3. Verify whether the behavior is already documented as a limitation

## Notes

- Behavior depends on installed grammars and their build flags
- Some cases reflect parser limitations and are documented inline
- This is not an automated test suite; it is a development and
  exploration aid






## Screenshots

* [Default Theme Raw](demo/demo-default-theme-raw.md)
* [Default Theme Hidden Markup](demo/demo-default-theme-hidden.md)
* [Modus Operandi Raw](demo/demo-modus-operandi-raw.md)
* [Modus Operandi Hidden Markup](demo/demo-modus-operandi-hidden.md)
* [Modus Vivendi Raw](demo/demo-modus-vivendi-raw.md)
* [Modus Vivendi Hidden Markup](demo/demo-modus-vivendi-hidden.md)
* [Leuven Raw](demo/demo-leuven-raw.md)
* [Leuven Hidden Markup](demo/demo-leuven-hidden.md)
* [Leuven Dark Raw](demo/demo-leuven-dark-raw.md)
* [Leuven Dark Hidden Markup](demo/demo-leuven-dark-hidden.md)
