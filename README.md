# latex-turnip-pkgs
Custom LaTeX packages for personal use.

All tested with Overleaf TeXLive 2020+

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
