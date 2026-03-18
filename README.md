# markdown-ts-mode-lab

This repository is a development workspace for `markdown-ts-mode`.

It contains files used to organize work, track features, and manually
test behavior while developing improvements to the mode.

It is intended as a companion resource for discussions and patches
submitted to `emacs-devel`.

## Contents

* `test.md`
  A comprehensive Markdown document used for manual testing and
  exploration.

  Covers:

  * CommonMark and GFM constructs
  * Parser edge cases and known limitations
  * Editing behavior (filling, navigation, list handling, etc.)

  Sections include inline comments describing what is being exercised.

* `features.md`
  A feature checklist derived from the tree-sitter-markdown parser.

  Tracks:

  * implemented features
  * missing functionality
  * extension-dependent behavior
  * parser limitations

* `patches.md`
  Tracks patches related to `markdown-ts-mode`.

  Includes:

  * debbugs links
  * review status
  * planned and in-progress work

* `screenshots/`
  Visual snapshots of test.md rendering for reference, typically
  generated using the latest local code, including changes not yet
  submitted.

## Upstream parser

This work is based on the tree-sitter Markdown grammar:

<https://github.com/tree-sitter-grammars/tree-sitter-markdown>

That parser:

* targets CommonMark with optional extensions (GFM, etc.)
* enables/disables features via compile-time flags
* is primarily designed for syntax highlighting, not full correctness

As a result:

* some behaviors in `test.md` reflect parser limitations
* not all Markdown constructs can be represented perfectly
* issues may originate from the parser rather than `markdown-ts-mode`

Where relevant, such cases are documented inline in `test.md`.

## Setup (Tree-sitter grammars)

To view `test.md` as intended, install the required grammars.

Run:

`M-x treesit-install-language-grammar ...`

Install the following:

* markdown
* markdown-inline
* yaml
* toml
* html
* c
* javascript
* python
* rust

Missing grammars will result in incorrect or incomplete fontification.
If you installed with the mode already initialized on the buffer,
re-start it with `M-x markdown-ts-mode RET`.

## Usage

Open `test.md` in Emacs using `markdown-ts-mode`.

The file is intended for:

* visual inspection (fontification, structure)
* interactive testing (filling, navigation, editing commands)

Compare behavior with:

* inline comments in the file
* screenshots in `screenshots/` (when relevant)

## Before reporting issues

Please keep in mind:

* `markdown-ts-mode` is under active development
* not all features listed in `feature_development_control.md` are
  implemented
* some behaviors are known limitations of the parser

Before reporting a bug:

1. Ensure all required grammars are installed
2. Check `feature_development_control.md` to confirm the feature is
   expected to work
3. Verify whether the behavior is already documented as a limitation

## Notes

* Behavior depends on installed grammars and their build flags
* Some cases reflect parser limitations and are documented inline
* This is not an automated test suite; it is a development and
  exploration aid


## Screenshots

### Default Theme Raw

![test-default-raw-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-01.png)

![test-default-raw-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-02.png)

![test-default-raw-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-03.png)

![test-default-raw-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-04.png)

![test-default-raw-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-05.png)

![test-default-raw-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-06.png)

![test-default-raw-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-07.png)

![test-default-raw-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-08.png)

![test-default-raw-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-09.png)

![test-default-raw-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-10.png)

![test-default-raw-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-11.png)

![test-default-raw-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-12.png)

![test-default-raw-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-raw-13.png)


### Default Theme Hidden Markup

![test-default-hidden-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-01.png)

![test-default-hidden-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-02.png)

![test-default-hidden-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-03.png)

![test-default-hidden-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-04.png)

![test-default-hidden-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-05.png)

![test-default-hidden-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-06.png)

![test-default-hidden-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-07.png)

![test-default-hidden-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-08.png)

![test-default-hidden-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-09.png)

![test-default-hidden-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-10.png)

![test-default-hidden-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-11.png)

![test-default-hidden-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-12.png)

![test-default-hidden-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-default-hidden-13.png)


### Modus Operandi Raw

![test-modus-operandi-raw-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-01.png)

![test-modus-operandi-raw-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-02.png)

![test-modus-operandi-raw-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-03.png)

![test-modus-operandi-raw-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-04.png)

![test-modus-operandi-raw-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-05.png)

![test-modus-operandi-raw-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-06.png)

![test-modus-operandi-raw-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-07.png)

![test-modus-operandi-raw-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-08.png)

![test-modus-operandi-raw-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-09.png)

![test-modus-operandi-raw-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-10.png)

![test-modus-operandi-raw-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-11.png)

![test-modus-operandi-raw-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-12.png)

![test-modus-operandi-raw-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-raw-13.png)


### Modus Operandi Hidden Markup

![test-modus-operandi-hidden-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-01.png)

![test-modus-operandi-hidden-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-02.png)

![test-modus-operandi-hidden-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-03.png)

![test-modus-operandi-hidden-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-04.png)

![test-modus-operandi-hidden-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-05.png)

![test-modus-operandi-hidden-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-06.png)

![test-modus-operandi-hidden-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-07.png)

![test-modus-operandi-hidden-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-08.png)

![test-modus-operandi-hidden-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-09.png)

![test-modus-operandi-hidden-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-10.png)

![test-modus-operandi-hidden-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-11.png)

![test-modus-operandi-hidden-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-12.png)

![test-modus-operandi-hidden-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-operandi-hidden-13.png)


### Modus Vivendi Raw

![test-modus-vivendi-raw-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-01.png)

![test-modus-vivendi-raw-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-02.png)

![test-modus-vivendi-raw-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-03.png)

![test-modus-vivendi-raw-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-04.png)

![test-modus-vivendi-raw-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-05.png)

![test-modus-vivendi-raw-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-06.png)

![test-modus-vivendi-raw-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-07.png)

![test-modus-vivendi-raw-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-08.png)

![test-modus-vivendi-raw-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-09.png)

![test-modus-vivendi-raw-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-10.png)

![test-modus-vivendi-raw-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-11.png)

![test-modus-vivendi-raw-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-12.png)

![test-modus-vivendi-raw-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-raw-13.png)


### Modus Vivendi Hidden Markup

![test-modus-vivendi-hidden-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-01.png)

![test-modus-vivendi-hidden-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-02.png)

![test-modus-vivendi-hidden-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-03.png)

![test-modus-vivendi-hidden-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-04.png)

![test-modus-vivendi-hidden-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-05.png)

![test-modus-vivendi-hidden-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-06.png)

![test-modus-vivendi-hidden-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-07.png)

![test-modus-vivendi-hidden-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-08.png)

![test-modus-vivendi-hidden-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-09.png)

![test-modus-vivendi-hidden-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-10.png)

![test-modus-vivendi-hidden-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-11.png)

![test-modus-vivendi-hidden-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-12.png)

![test-modus-vivendi-hidden-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-modus-vivendi-hidden-13.png)


### Leuven Raw

![test-leuven-raw-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-01.png)

![test-leuven-raw-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-02.png)

![test-leuven-raw-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-03.png)

![test-leuven-raw-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-04.png)

![test-leuven-raw-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-05.png)

![test-leuven-raw-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-06.png)

![test-leuven-raw-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-07.png)

![test-leuven-raw-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-08.png)

![test-leuven-raw-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-09.png)

![test-leuven-raw-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-10.png)

![test-leuven-raw-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-11.png)

![test-leuven-raw-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-12.png)

![test-leuven-raw-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-raw-13.png)


### Leuven Hidden Markup

![test-leuven-hidden-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-01.png)

![test-leuven-hidden-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-02.png)

![test-leuven-hidden-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-03.png)

![test-leuven-hidden-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-04.png)

![test-leuven-hidden-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-05.png)

![test-leuven-hidden-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-06.png)

![test-leuven-hidden-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-07.png)

![test-leuven-hidden-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-08.png)

![test-leuven-hidden-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-09.png)

![test-leuven-hidden-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-10.png)

![test-leuven-hidden-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-11.png)

![test-leuven-hidden-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-12.png)

![test-leuven-hidden-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-hidden-13.png)


### Leuven Dark Raw

![test-leuven-dark-raw-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-01.png)

![test-leuven-dark-raw-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-02.png)

![test-leuven-dark-raw-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-03.png)

![test-leuven-dark-raw-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-04.png)

![test-leuven-dark-raw-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-05.png)

![test-leuven-dark-raw-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-06.png)

![test-leuven-dark-raw-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-07.png)

![test-leuven-dark-raw-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-08.png)

![test-leuven-dark-raw-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-09.png)

![test-leuven-dark-raw-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-10.png)

![test-leuven-dark-raw-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-11.png)

![test-leuven-dark-raw-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-12.png)

![test-leuven-dark-raw-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-raw-13.png)


### Leuven Dark Hidden Markup

![test-leuven-dark-hidden-01.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-01.png)

![test-leuven-dark-hidden-02.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-02.png)

![test-leuven-dark-hidden-03.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-03.png)

![test-leuven-dark-hidden-04.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-04.png)

![test-leuven-dark-hidden-05.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-05.png)

![test-leuven-dark-hidden-06.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-06.png)

![test-leuven-dark-hidden-07.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-07.png)

![test-leuven-dark-hidden-08.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-08.png)

![test-leuven-dark-hidden-09.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-09.png)

![test-leuven-dark-hidden-10.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-10.png)

![test-leuven-dark-hidden-11.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-11.png)

![test-leuven-dark-hidden-12.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-12.png)

![test-leuven-dark-hidden-13.png](https://codeberg.org/LionyxML/markdown-ts-mode-lab/raw/branch/screenshots/test-leuven-dark-hidden-13.png)
