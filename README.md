# latex-turnip-pkgs
Custom LaTeX packages for personal use.

All tested with TeXLive LuaLaTeX 2022.

## turniptodo
This is the most polished one :)

Dependencies: etoolbox, xcolor, newfile, currentfile packages from TeXLive

Installation: Copy `turniptodo.sty` into your project folder.

It has four commands:

1. `\todomark{Finish this sentence}` becomes `[TODO1 Finish this sentence]`
2. `\todocite{https://ieeexplore.ieee.org/document/8918510}` becomes `[TC1]`.
     - By default, it adds a footnote with the thing you're citing. This can be disabled with [nofootnotes] option.
     - It also supports an optional argument, e.g. `\todocite[Page 1]{Bee Movie Script}` to `[TC1, Page 1]`
3. `See \todoref{figure showing performance results}` becomes `See Section ??1`
4. `\todopending{Maybe mention XYZ?}` becomes `[TODO?1 Maybe mention XYZ]`
     - `\todopending` and `\todomark` are almost the same, but options like `[error]` ignore todopending.

When you compile your document, four files `todocite.txt,todomark.txt,todoref.txt,todopending.txt` will be created summarizing the TODOs you have left in your document.


### Options
Options can be passed to the package when you import it e.g. `\usepackage[hidetodo, warn]{turniptodo}`.
- `[hidetodo]` hides all todos
- `[warn]` will emit a warning on compile for every TODO in your document
    - `[nowarn]` will disable warnings
- `[error]` will emit an error on compile for every TODO in your document
    - `[noerror]` will disable errors
- `[release]` is the equivalent of `[hidetodo,error]`. Errors will be emitted for every TODO, but they will all be hidden. This is useful if you want to send a "finished"-looking version to someone.
- `[disablewrite]` stops it from generating `todoblah.txt` files.
- `[nofootnotes]` disables footnotes for `\todocite`


## turnipcite
This sets my custom biblography settings, including:
- Numeric cite marks, e.g. `[3]`
- Cite-ordered numbers, e.g. `\cite{a}, \cite{b}` -> `[1],[2]` instead of sorting by e.g. author
- Sanitized references
    - If a DOI is present, the URL will be removed
    - If a DOI and `booktitle` are present, the `eventtitle` will be removed (Zotero likes to fill it with redundant information from `booktitle`)

`\turnipbib{}` will create a normal references page.
A message can be added in the argument, e.g. `\turnipbib{All URLs accessed on 01-01-01 unless otherwise states}` which will be placed between the references header and the rest of the list.

### Options
- `withbreak`, `nobreak` enables/disables a Page Break included by default inside `\turnipbib`
- `sanitize`, `nosanitize` enables/disables reference sanitization as shown above.

## turnipwordcount
LaTeX- and LuaLaTeX-compatible macros for invoking `texcount`.

Equivalent to calling `texcount -1 -sum -merge -q {file}`.

`\quickwordcount{file}` returns the wordcount for `file.tex` in the form "X words".

When not using LuaLaTeX, creates a file `words.sum` in the top-level directory.