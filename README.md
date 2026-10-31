# fk-markdown

Markdown for fckt: read as CommonMark reads its core, and written as HTML with
[fk-html](https://github.com/m4xy/fk-html).

```kotlin
import uk.m4xy.markdown.Markdowns

Markdowns.render("# Hello\n\nSome *emphasis*, and [a link](https://fckt.dev).")
// <h1 id="hello">Hello</h1><p>Some <em>emphasis</em>, and <a href="https://fckt.dev">a link</a>.</p>
```

It reads headings, with `#` or underlined; paragraphs; fenced code, with the language it's in, and
indented code; quotes; lists, of `-`, `*` or `+`, or numbered, nested by indenting an item's lines
to its text, and tight unless a blank line is between their items; rules; and tables, as GitHub
writes them, with each column aligned as its delimiter row says. In a paragraph, it
reads emphasis and strong emphasis, code spans, links and images, with titles, autolinks in `<>`,
backslash escapes, and line breaks, two spaces or a backslash at a line's end.

HTML written in Markdown is text, escaped as any text is, so what anyone wrote can be shown as it
is. Reference links and HTML blocks aren't read yet.

`Markdowns.parse` gives the document's blocks, `Block` and `Inline` values, to look through or
change; `Markdowns.html` writes blocks as fk-html's `Html`, to put in a page built with it; and
`Markdowns.render` does both, to text. `Markdowns.htmlWith` takes a function that highlights code:
given a code block's language and its code, it gives the block's HTML, or `None` to show it as text. Each heading has an id, as GitHub gives one, so a link
to `#effects-with-operations` goes to the heading "Effects with operations"; `Markdowns.slugOf`
says what a heading's id is.

## The command

`cli` is a command, `markdown`, that writes Markdown files, or what it reads from standard input, as
HTML; `--page "Title"` makes a whole document.

```sh
cd cli && kiln compile
build/bin/markdown --page "Notes" notes.md > notes.html
```

## Building

```sh
kiln build          # compiles and tests it
kiln publishLocal   # for other projects: library("uk.m4xy:fk-markdown:0.1.0")
```
