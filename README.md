# How do you make cool fonts work with pdflatex in overleaf?

1. find `T1-WGL4.enc`. This can be got as `wget http://tug.ctan.org/fonts/verdana/T1-WGL4.enc`
2. Find the ttf font you want. https://tug.org/FontCatalogue/imfellenglish/ is a good start. Google around for the ttf. you can also do this to convert otf to ttf: `fontforge -lang=ff -c 'Open($1); Generate($2); Close();' font.otf font.ttf`
3. Run `ttf2tfm -p T1-WGL4.enc [fontname].ttf`
4. Make a ".fd" file. Here's an example:

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
3. t1[fontname].fd   (yes, you need the t1 there...)

then you can use, e.g., as:

```
\usepackage[T1]{fontenc}    % use 8-bit T1 fonts
\newcommand\merlottitlefont[1]{{\usefont{T1}{QTWestEndRegular}{m}{n}#1}}
\newcommand\merlotfont[1]{{\usefont{T1}{QTWestEndRegular}{m}{n}#1}}

\newcommand{\modelname}{\merlotfont{VIP-ANT}\xspace}
```

Useful links:
- https://www.rocketshipgames.com/blogs/tjkopena/2015/12/importing-ttf-fonts-into-latex-with-kerning-ligatures/
