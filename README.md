= a

```sh
# get docker image
$ docker pull vvakame/review:4.0

# 間違い
$ docker run --rm -v $(pwd)/src:/work vvakame/review:4.0 /bin/sh -c "review-init hoge"

# 正解
$ docker run \
 --rm \
 -v $(pwd):/work \
 vvakame/review:4.0 /bin/sh -c "cd /work && review-init hoge"

$  docker run \
 --rm \
 -v $(pwd):/work \
 -v $(pwd)/.texmf-var:/root/.texmf-var \
 vvakame/review:4.0 /bin/sh -c "cd /work && review-pdfmaker ./config.yml"
```

## error log

INFO review-pdfmaker: compiling first.tex
WARN review-pdfmaker: No such directory - /work/sty
WARN review-pdfmaker: No such directory - /work/sty
WARN review-pdfmaker: No such directory - /work/sty
WARN review-pdfmaker: No such directory - /work/sty
WARN review-pdfmaker: No such directory - /work/sty
~/Documents/100_projects/toybox/simple-review4.0-build (master #)

> docker run --rm -v `pwd`/src:/work vvakame/review:4.0 /bin/sh -c "cd /work && review-pdfmaker config.yml"
> INFO review-pdfmaker: compiling first.tex
> WARN review-pdfmaker: No such directory - /work/sty
> WARN review-pdfmaker: No such directory - /work/sty
> WARN review-pdfmaker: No such directory - /work/sty
> WARN review-pdfmaker: No such directory - /work/sty
> WARN review-pdfmaker: No such directory - /work/sty
> INFO review-pdfmaker: uplatex -interaction=nonstopmode -file-line-error -halt-on-error **REVIEW_BOOK**.tex
> ERROR review-pdfmaker: failed to run command: uplatex -interaction=nonstopmode -file-line-error -halt-on-error **REVIEW_BOOK**.tex

Error log:
This is e-upTeX, Version 3.14159265-p3.8.1-u1.23-180901-2.6 (utf8.uptex) (TeX Live 2019/dev/Debian) (preloaded format=uplatex)
restricted \write18 enabled.
entering extended mode
(./**REVIEW_BOOK**.tex
pLaTeX2e <2018-12-01u02> (based on LaTeX2e <2018-12-01>)
(/usr/share/texlive/texmf-dist/tex/platex/jsclasses/jsbook.cls
Document Class: jsbook 2018/12/11 jsclasses (okumura, texjporg)
(/usr/share/texlive/texmf-dist/tex/platex/jsclasses/jslogo.sty))

! LaTeX Error: File `reviewmacro.sty' not found.

Type X to quit or <RETURN> to proceed,
or enter new name. (Default extension: sty)

Enter file name:
./**REVIEW_BOOK**.tex:68: Emergency stop.
<read \*>

l.68 ^^M

No pages of output.
Transcript written on **REVIEW_BOOK**.log.

=> これで解決できそう

## https://review-knowledge-ja.readthedocs.io/ja/latest/releases/review400.html#0ff035905a79b556751b53bb55b583e5
