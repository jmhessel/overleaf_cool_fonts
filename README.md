# How do you make cool fonts work with pdflatex in overleaf?

1. Find the ttf font you want. https://tug.org/FontCatalogue/imfellenglish/ is a good start. Google around for the ttf.
2. Run `ttf2tfm [your ttf file here]`
3. Make a ".fd" file. Here's an example:

`t1QTWestEndRegular.fd`:

```
\ProvidesFile{t1QTWestEndRegular.fd}
\DeclareFontFamily{T1}{QTWestEndRegular}{}
\DeclareFontShape{T1}{QTWestEndRegular}{m}{n}{ <-> QTWestEndRegular}{}
\pdfmapline{+QTWestEndRegular\space <QTWestEndRegular.ttf\space <T1-WGL4.enc}
```

Then, in your overleaf, you include

1. [fontname].ttf
2. [fontname].tfm
3. [fontname].fd

then you can use, e.g., as:

```
\usepackage[T1]{fontenc}    % use 8-bit T1 fonts
\newcommand\merlottitlefont[1]{{\usefont{T1}{QTWestEndRegular}{m}{n}#1}}
\newcommand\merlotfont[1]{{\usefont{T1}{QTWestEndRegular}{m}{n}#1}}

\newcommand{\modelname}{\merlotfont{VIP-ANT}\xspace}
```
