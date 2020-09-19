# authorfix
Fix common exported BibTeX author formatting in Python (and Vim) :scroll:

## Info
This script changes `Lastname, Firstname` to `Firstname Lastname` (in LaTeX BibTeX bibliography entries).

A common exporting format of BibTeX on e.g. scholar.google.com is this (sample article):
```
@article{fournier2017survey,
  title={A survey of sequential pattern mining},
  author={Fournier-Viger, Philippe and Lin, Jerry Chun-Wei and Kiran, Rage Uday and Koh, Yun Sing and Thomas, Rincy},
  journal={Data Science and Pattern Recognition},
  volume={1},
  number={1},
  pages={54--77},
  year={2017}
}
```

Notice the formatting of the authors:
`Fournier-Viger, Philippe and Lin, Jerry Chun-Wei and Kiran, Rage Uday and Koh, Yun Sing and Thomas, Rincy`

Running this script on this string changes it to:
`Philippe Fournier-Viger and Jerry Chun-Wei Lin and Rage Uday Kiran and Yun Sing Koh and Rincy Thomas`

## Vim Macro
Add this to your `.vimrc`:
```vimscript
vnoremap <leader>af c<C-R>=system('authorfix', getreg('"'))[:-2]<CR><ESC>x
```

`authorfix` needs to be in your `PATH` for this.

## Installation
```bash
curl \
  -L https://raw.githubusercontent.com/lolei/authorfix/master/authorfix.py \
  -o $HOME/.local/bin/authorfix && chmod +x $HOME/.local/bin/authorfix
```

## Additional Resources
I use additional automatic fixes in Vim for imported BibTeX entries:
* [Title Case Capitalization](https://github.com/nickjj/title-case-converter)
* [Converting `{}` to `""`](https://github.com/LoLei/dotfiles/blob/d2d3fb97f654710c64cbac828db3937ebc30904b/.vimrc#L150)

## Background
* Inspired by [nickjj/title-case-converter](https://github.com/nickjj/title-case-converter)
* I had a working regex to to the same in sed, but for some reason in wouldn't work in vim: `s/\v(?!and\b)\b([[:alpha:]-]+ ?[[:alpha:]-]*)(,) ([[:alpha:]-]+ ?[[:alpha:]-]*)\b(?<!\b and)/\3 \1/g`
  * Also this Python version handles if a person has multiple last names, and will enclose them in `{}`, which makes LaTeX use them correctyl in citations.
