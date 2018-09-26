---
layout: post
title: Tiwtorial LaTeX
permalink: teaching/latex-refresher/cy/
---

# Cyfarwyddiadau

+ Edrychwch dros y daflen gwaith hon *cyn* dod i'r sesiwn os gwelwch yn dda:
  + Naill ai gweithiwch trwy'r daflen gwaith yma cyn dod i'r sesiwn, a dewch ag
  unrhyw broblemau / anawsterau i'r sesiwn felly gallwn ni edrych drostyn nhw
  gyda'n gilydd.
  + Neu gweithiwch trwy'r daflen gwaith yma yn y sesiwn, yn cyfeirio unrhyw
  anawsterau sy'n codi wrth i chi eu cyrraedd.

+ Unrhyw beth a ddymunwch fynd dros sydd ddim yn y daflen gwaith yma, *dewch ag
enghreifftiau* a gallwn ni gweithio trwyddynt gyda'n gilydd.

+ Rydw i'n awgrymu defnyddio [Overleaf](https://www.overleaf.com/), offeryn we
ar gyfer ysgrifennu a crynhoi ffeiliau $$\TeX$$.
Mae'n dda iawn ar gyfer dysgu $$\LaTeX$$.
Croeso i chi defnyddio unrhyw beth rydych yn gyfforddus gyda.
Nodwch fod cyfyngiadau ar gyfrifau am ddim ar Overleaf, ac felly rydw i'n
awgrymu cael fersiwn lleol o LaTeX ar gyfer gwaith difrifol.

# Cynnwys

+ <a href="#1">1. Sylfeini</a>
+ <a href="#2">2. Adrannau</a>
+ <a href="#3">3. Rhestrau & Thablau</a>
+ <a href="#4">4. Mathemateg</a>
+ <a href="#5">5. Ffigyrau</a>
+ <a href="#6">6. Labeli</a>
+ <a href="#7">7. Cod</a>
+ <a href="#8">8. Amgylcheddau</a>
+ <a href="#9">9. Llyfryddiaethau</a>
+ <a href="#10">10. Cyflwyniadau</a>

&nbsp;

---

<h1 id="1">1. Sylfeini</h1>

Mae nifer o orchmynion LaTeX yn dechrau gyda ôl-slaes `\`.
Mae unrhyw beth sy'n dechrau gyda `%` yn sylwadau ac yn cael eu hanwybyddu.
Mae angen i ni ddweud wrth LaTeX pa fath o ddogfen byddwn yn creu (erthygl yn yr
achos yma), ac yn lle mae'r dogfen ei hun yn dechrau a lle mae'n gorffen:

    \documentclass{article}

    \begin{document}
    % Eich cynnwys fan hyn...
    \end{document}

Enw'r cod rhwng `\begin` a `\end` y ddogfen yw'r prif gorff.
Enw'r cod sy'n dod cyn `\begin{document}` yw'r rhaglith.
Dyma le ysgrifennwn ddatganiadau o ba becynnau a ddefnyddiwn.
Hefyd, dyma le mae gwybodaeth teitl yn mynd:

    \title{Fy teitl arbennig}
    \author{G Palmer}
    \date{28/9/2016}

Fe allwn gynhyrchu dyddiad heddiw yn awtomatig gyda `\today`.
Yna i greu'r teitl, ym mhrif gorff y ddogfen, mae angen i ni ddatgan fod eisiau
creu teitl:

    \begin{document}
    \maketitle
    \end{document}

Mae nifer o erthyglau yn cynnwys abstract, sy'n braslunio cynnwys y ddogfen yn
gryno.
O fewn y prif gorff, fe allwn greu abstract yn defnyddio:

    \begin{abstract}
    % Eich abstract fan hyn...
    \end{abstract}

> ***Her:*** Crëwch erthygl gyda theitl, awdur, dyddiad, ac abstract.


&nbsp;

---

<h1 id="2">2. Adrannau</h1>

Mae adrannau yn ddefnyddiol ar gyfer trefnu eich erthygl i ddarnau hylaw ar
gyfer darllen.
Fe allwch weithredu'r rhain yn hawdd yn LaTeX:

    \section{Crwbanod}
    % Cynnwys am grwbanod fan hyn...

    \section{Clociau}
    % Cynnwys am glociau fan hyn...

Nodwch fod rhifo adrannau yn awtomatig, felly nid oes angen cynnwys rhifau yn
deitlau'r adrannau.
Fe allwch greu isadrannau (wedi'i rhifo 2.1, 2.2 a.y.b.) gyda `\subsection{}`.

I creu tabl cynnwys ar dechrau'r dogfen, sy'n rhestri pa tudalennau y mae pob
adran yn dechrau arno yn awtomatig, gallwch rhoi'r datganiad isod ar dechrau'r
dogfen:

    \tableofcontents

> ***Her:*** Ychwanegwch tair adran i'ch erthygl, wedi enwi 'Bwyd & Diod',
'Dodrefn', a 'Mathemateg'.
O dan yr adran Bwyd a Diod, ychwanegwch isadrannau 'Ffrwythau' a 'Llysiau'.
O dan yr isadran 'Ffrwythau', ychwanegwch dau is-isadran pellach o'r enw
'Ffrwythau Sitrws', ac 'Aeron'.
Arbrofwch gyda adrannau pellach.


&nbsp;

---

<h1 id="3">3. Rhestrau & Thablau</h1>

Mae rhestrau bwled, rhestrau rhifedig, a thablau yn ffyrdd cyfleus o dangos
cynnwys dogfen.
Fe allwch greu rhestrau bwled gan ddefnyddio `itemize`, a rhoi eitemau i mewn
i'r rhestr gan ddefnyddio `\item`.
Dangosir enghraifft isod:

    \begin{itemize}
      \item Dalek
      \item Cyberman
      \item Weeping angel
    \end{itemize}

Ar gyfer rhestrau rhifedig, defnyddiwch `enumerate`:

    \begin{enumerate}
      \item Dalek
      \item Cyberman
      \item Weeping angel
    \end{enumerate}

Fe all rhestrau cael eu nythu, a gallwch ddefnyddio cymysgedd o `itemize` ac
`enumerate`:

    \begin{itemize}
      \item Cymdeithion
      \begin{enumerate}
        \item Rose
        \item Martha
        \item Donna
      \end{enumerate}
      \item Anghenfilod
      \begin{itemize}
        \item Dalek
        \item Cyberman
        \item Weeping angel
      \end{itemize}
    \end{itemize}

Mae tablau yn ffordd arall o drefnu cynnwys.
Fe allwch weithredu'r rhain trwy ddefnyddio `tabular`.
Ceisiwch ddeall yr enghraifft isod:

    \begin{tabular}{|c|c|c|}
    Cymydaith & Cyfres & Gelyn Cyntaf \\
    \hline
    Rose & 1, 2 & Autons \\
    Martha & 3 & Judoon \\
    Donna & 4 & Adipose \\
    \hline
    \end{tabular}

Mae'r llinell gyntaf yn setio opsiynau'r tabl.
Gwelwch fod yna tair colofn wedi'i chanoli, `c` (ceisiwch amnewid rhaid gyda `r`
neu `l` ar gyfer colofnau aliniadau de a chwith).
Mae `|` yn dynodi fod llinell fertigol wedi'i thynnu cyn neu rhwng colofnau.
Yn yr amgylchedd tabl ei hun rydym yn ychwanegu cynnwyd rhes wrth res.
Mae `&` yn dynodi diwedd colofn, ac i roi unrhyw cynnwys pellach yn y golofn
nesa.
Mae `\\` yn dynodi fod y rhes wedi benu, a dylai unrhyw cynnwys pellach fod yn
gelloedd yn y rhes nesa.
Rhwng rhesi, mae rhoi `\hline` yn tynnu llinell lorweddol.
Nodwch yn yr enghraifft syml hon, mae angen i bob rhes cynnwys tair colofn yn
unig, er gallwn ychwanegu gymaint o resi a ddymunwn.

Rhoddir hwn:

<img src="{{site.baseurl}}/images/tabular_example_cy.png" width="400">{: .center-image }

Mae rhagor o wybodaeth ar dablau ar gael
[fan hyn](https://en.wikibooks.org/wiki/LaTeX/Tables).

Gall creu tablau mwy bert gan defnyddio'r pecyn `booktabs`.
Gyda'r pecyn yma nid oes angen llinellau fertigol, a'r unig llinellau fertigol
sydd angen yw `\toprule`, `\midrule` a `bottomrule`:

    \usepackage{booktabs}

    \begin{tabular}{ccc}
    \toprule
    Cymydaith & Cyfres & Gelyn Cyntaf \\
    \midrule
    Rose & 1, 2 & Autons \\
    Martha & 3 & Judoon \\
    Donna & 4 & Adipose \\
    \bottomrule
    \end{tabular}

Cymharwch yr allwbn yma i'r uchod:

<img src="{{site.baseurl}}/images/booktabs_example_cy.png" width="400">{: .center-image }

> ***Her:*** O dan yr adran Dodrefn, crëwch restr rhifedig yn rhestru'r holl
ddodrefn sydd yn yr ystafell, wedi'i threfnu gan faint.
O dan bob eitem, crëwch restr bwled yn rhestru rhai priodweddau arall y darn o
ddodrefn yna.
Arbrofwch gyda nythu pellach.

> ***Her:*** O dan yr adran Ffrwythau, crëwch dabl o 7 ffrwyth, yn cynnwys
gwybodaeth am eu lliw, maint, a siâp.
Arbrofwch gydag aliniadau cell wahanol, a ffiniau cell.




&nbsp;

---

<h1 id="4">4. Mathemateg</h1>

Fe allwch ysgrifennu mathemateg yn LaTeX yn dwy ffordd, yn y llinell, neu mewn
amgylchedd hafaliad.
Fe allwch greu mathemateg yn y llinell fel hon $$y = mx + c$$ trwy lapio'r
fathemateg rhwng dau arwydd `$`.
Os ydych chi eisiau creu hafaliad ar wahân, yna defnyddiwch yr amgylchedd
hafaliad:

    \begin{equation}
    % Eich mathemateg fan hyn...
    \end{equation}

Mae nifer o weithrediadau mathemategol yn LaTeX yn sythweledol: mae `+`, `-`,
`=`, `>`, `<`, a rhifau a llythrennau Lladin fel y teipwich chi nhw.
Gallwch chi greu llythrennau bach Groegaidd trwy eil sillafu gyda ôl-slaes,
$$\alpha$$ yw `\alpha`, ac ar gyfer prif lythrennau sillafwch gyda phrif
lythyren ar y dechrau, $$\Gamma$$ yw `\Gamma`.
Rhagor o symbolau defnyddiol:

+ $$\neq$$ yw `\neq`
+ $$\geq$$ yw `\geq`
+ $$\leq$$ yw `\leq`
+ $$\mathbb{R}$$ yw `\mathbb{R}`
+ $$\mathbb{N}$$ yw `\mathbb{N}`
+ $$\mathbb{Q}$$ yw `\mathbb{Q}`
+ $$\mathbb{C}$$ yw `\mathbb{C}`
+ $$\in$$ yw `\in`
+ $$\int$$ yw `\int`
+ $$\cup$$ yw `\cup`
+ $$\propto$$ yw `\propto`
+ $$\infty$$ yw `\infty`
+ $$\rightarrow$$ yw `\rightarrow`

Ffeindiwch mwy o symbolau
[fan hyn](http://web.ift.uib.no/Teori/KURS/WRK/TeX/symALL.html).
Nodwch ar gyfer rhai o'r symbolau a ffontiau mathemategol, mae angen y pecynnau
`amsmath` a `amsfonts`.
Ychwanegwch y rhain i'r rhaglith:

    \usepackage{amsmath}
    \usepackage{amsfonts}

Ar gyfer cymeriadau gydag acen, ychwanegwch y trawsffurfiad i'r cymeriad
priodol, er enghraifft $$\hat{a}$$ yw `\hat{a}`, $$\bar{\beta}$$ yw
`\bar{\beta}`.
I godi i b&#373;er defnyddiwch `^`, ac i adio indecs defnyddiwch `_`, er
enghraifft $$x^{4a - 2}$$ yw `x^{4a - 2}`, a $$W_{\alpha}$$ yw `W_{\alpha}`.

+ Ysgrifennir ffracsiynau gan ddefnyddio `\frac{}{}` gyda'r rhifiadur yn y
braced cyrliog cyntaf, a'r enwadur yn yr ail fraced cyrliog.
Ysgrifennir ffracsiynau yn y llinell fel $$1/2$$ gyda `1/2`.

+ Ond angen teipio bracedi fel `(` a `[` yn uniongyrchol i mewn i LateX.
Angen i fracedi cyrliog `{` dilyn ôl-slaes `\{`.
Nid yw'r bracedi yma yn newid eu maint i'w cynnwys.
Er mwyn gwneud hyn rhagflaenwch y braced chwith gyda `\left` a'r braced de gyda
`\right`.
Cymharwch $$(\frac{x^y}{a^b})$$ gyda $$\left(\frac{x^y}{a^b}\right)$$, wedi'i
chreu gan `(\frac{x^y}{a^b})` a `\left(\frac{x^y}{a^b}\right)` yn eu trefn.
**Rhaid** i `\left` a `\right` dod yn barau; os oes ond angen un braced,
amnewidiwch y braced diangen gyda `.`, e.e. `\left[ a \right.`.

+ Er mwyn creu matricsau, defnyddiwch yr amgylchedd `pmatrix` (edrychwch hefyd
ar `matrix`, `bmatrix`, `vmatrix`,
[ayyb](http://latex.wikia.com/wiki/Matrix_environments).
Mae'r gystrawen yn debyg iawn i dablau.
Mae'r matrics canlynol wedi'i chreu gan y cod isod:

  $$ \begin{pmatrix}a & b \\ c & d\end{pmatrix}$$

      \begin{pmatrix}
      a & b \\
      c & d
      \end{pmatrix}

+ Defnyddir amgylchedd arall, yr amgylchedd `align` i greu hafaliadau sydd
wedi'i alinio gan yr arwydd '='.
Er enghraifft, mae'r darn o fathemateg ganlynol wedi'i chreu gan y cod isod:

  $$\begin{align}(x+2)(x-3)+6 &= x^2 -3x + 2x - 6 + 6\\
  &= x^2 + x\\
  &= x(x+1)\end{align}$$

      \begin{align}
      (x+2)(x-3)+6 &= x^2 -3x + 2x - 6 + 6\\
      &= x^2 + x\\
      &= x(x+1)
      \end{align}

  Yn debyg i dablau a matricsau, mae `\\` yn dweud wrth LaTeX pryd i ddechrau
  llinell newydd.
  Hefyd rhaid rhagflaenu'r holl arwyddion `=` sydd yw alinio gan `&`.

+ Ysgrifennir hafaliadau darn wrth ddarn yn LaTeX gyda'r amgylchedd `cases`.
Eto, mae gan hwn cystrawen debyg i fatricsau, araeau a thablau.
Astudiwch yr enghraifft ganlynol o'r ffwythiant step Heavyside:

  $$H(x) = \begin{cases} 0 & x < 0\\\frac{1}{2} & x = 0\\1 & x > 0\end{cases}$$

      \begin{equation}
      H(x) =
        \begin{cases}
          0 & x < 0\\
          \frac{1}{2} & x = 0\\
          1 & x > 0
        \end{cases}
      \end{equation}

> ***Her:*** Ail-grëwch y rhain yn LaTeX:

1. $$ \frac{\partial c}{\partial t} = D \nabla^2 \left( c^3 - c - \gamma \nabla^2 c \right)$$

2. $$ H = \frac{1}{2} \int \left[ \sum_i \left( \frac{\partial \mathbf{S}}{\partial x_i} \right)^2 - J(\mathbf{S}) \right] dx$$

3. $$ e = \lim_{n \rightarrow \infty} \left( 1 + \frac{1}{n} \right)^n$$

4. $$\mathbf{J} = \begin{bmatrix} \frac{d f_1}{d x_1} & \cdots & \frac{d f_1}{d x_n}\\ \vdots & \ddots & \vdots \\ \frac{d f_n}{d x_1} & \cdots & \frac{d f_n}{d x_n} \end{bmatrix}$$

5. $$\begin{align}(\theta-20)(\theta+6)+169 &= \theta^2 -20\theta +6\theta -120 + 169\\
&= \theta^2 - 14\theta + 49\\
&= (\theta - 7)^2\end{align}$$

6. $$\mathbb{E}_X \left[ g(X) \right] \geq g\left( \mathbb{E}_X [X] \right)$$




&nbsp;

---

<h1 id="5">5. Ffigyrau</h1>

Ychwanegir ffigyrau trwy ddefnyddio'r amgylchedd `figure`.
Mae'r amgylchedd yma yn galluogi capsiynau:

    \begin{figure}
      % Eich ffigwr yma...
      \caption{Disgrifiad cryno o'r ffigwr.}
    \end{figure}

Fe ellir ychwanegu lluniau trwy ddefnyddio'r pecyn `graphicx`, a'r gorchymyn
`\includegraphics`.
Mae'r gorchymyn yma yn cymryd lled fel opsiwn, ac mae'n arferol i nodi hwn yn
nhermau `\textwidth`.
Yn gyntaf rhaid cynnwys y pecyn yn y rhaglith:

    \usepackage{graphicx}

Gadewch i ni ychwanegu `fy_llun.png`, a fyddwn yn rhoi hwn *yn yr un ffolder*
a'r brif dogfen, i fod yn hanner lled y tecst.
Nawr dylwn ni cael:

    \begin{figure}
      \includegraphics[width=0.5\textwidth]{fy_llun.png}
      \caption{Disgrifiad cryno o'r ffigwr.}
    \end{figure}

Gan ddefnyddio'r pecyn `subcaption` gallwn rhoi is-ffigyrau o fewn ffigyrau.
Mae amgylchedd `subfigure` yn gweithio'n debyg i'r amgylchedd `figure`, ac yn
galluogu capsiynau ar gyfer yr is-ffigyrau ac hefyd y ffigwr llawn:

    \begin{figure}
      \begin{subfigure}{0.5\textwidth}
        \includegraphics[width=\textwidth]{fy_llun_1.png}
        \caption{Disgrifiad cryno o'r is-ffigwr cyntaf.}
      \end{subfigure}
      \begin{subfigure}{0.5\textwidth}
        \includegraphics[width=\textwidth]{fy_llun_2.png}
        \caption{Disgrifiad cryno o'r ail is-ffigwr.}
      \end{subfigure}
      \caption{Capsiwn ar gyfer yr holl ffigwr.}
    \end{figure}

> ***Her:*** Ffeindiwch lun o ddarn o ddodrefn ar y we, a'i lawrlwytho.
Rhowch y llun fel ffigwr yn yr adran 'Dodrefn', ychwanegwch gapsiwn priodol.

Fe allwch greu diagramau yn defnyddio'r pecyn `tikz`.
Mae hwn yn becyn pwerus iawn a gallwch ddefnyddio i dynnu llun bron pob diagram
fyddwch chi angen.
Rhaid ei chynnwys yn y rhaglith:

    \usepackage{tikz}

Mae triniaeth sylfaenol yn cynnwys tynnu llinell goch rhwng dau gyfesuryn (0, 0)
a (0, 2):

    \draw[draw=red] (0, 0) -- (0, 2);

tynnu llun cylch glas gyda radiws 5 gyda chanol yn gyfesuryn (10, 20):

    \draw[fill=blue] (10, 20) circle (5);

a rhoi tecst wrth gyfesuryn (4, 5):

    \node at (4, 5) {Some text};

Rhaid i bob gorchymyn tikz gorffen gyda hanner colon.
Tynnir y diagram llif canlynol gyda'r cod tikz isod:

![Siart Llif Tikz]({{ site.baseurl }}/images/tikzflowchart-cy.png)


    \begin{tikzpicture}
      \draw[->] (0, 0) -- (2, 0);
      \draw[fill=yellow] (2, 0) -- (3, 1) -- (4, 0) -- (3, -1) -- cycle;
      \node at (3, 0) {Eat food?};
      \draw[->] (3, 1) -- (3, 3) node[pos=0.5, left] {Yes};
      \draw[fill=orange] (3, 4) circle (1) node {Full};
      \draw[->] (4, 0) -- (6, 0) node[pos=0.5, above] {No};
      \draw[fill=orange] (7, 0) circle (1) node {Hungry};
    \end{tikzpicture}


> ***Her:*** Ceisiwch ail-greu'r diagram hwn o giw yn defnyddio tikz:

![Diagram Ciw Tikz]({{ site.baseurl }}/images/tikzqueuediagram.png)


&nbsp;

---

<h1 id="6">6. Labeli</h1>

Labeli yw sut y gallwn gyfeirio at adrannau, ffigyrau, a hafaliadau (a llawer o
bethau arall) yn LaTeX.
Gallwn wneud hyn trwy'r gorchymyn `\label{}`.
I labelu adran, atodwch y gorchymyn yma i'r gorchymyn adran:

    \section{Crwbanod}\label{sec:crwbanod}

Fan hyn `sec:crwbanod` yw'r label rydw i wedi rhoi i'r adran er mwyn cyfeirio
ato yn hawdd.
Fe allaf alw'r adran hon gan ddefnyddio `\ref`, er enghraifft:

    Yn flaenorol, yn Adran~\ref{sec:crwbanod} fe drafodir crwbanod.

Nodwch y `~` fan hyn.
Mae hwn i wneud yn si&#373;r fydd yna dim toriad llinell rhwng y gair 'Adran'
a'r rhif a chrëwyd gan y gorchymyn `\ref`.

Hefyd fe ellir labelu ffigyrau a hafaliadau:

    \begin{equation}\label{eqn:pythagoras}
    a^2 + b^2 = c^2
    \end{equation}

    \begin{figure}
      \includegraphics[width=0.5\textwidth]{fy_llun.png}
      \caption{Disgrifiad cryno o'r ffigwr.}
      \label{fig:fyllun}
    \end{figure}

> ***Her:*** Yn eich erthygl, labelwch bob adran, isadran, hafaliad, a ffigwr.
Ysgrifennwch gwpl o frawddegau yn cyfeirio at bob un o rain.



&nbsp;

---

<h1 id="7">7. Cod</h1>

Ychwanegir pytiau cod trwy ddefnyddio pecyn o'r enw `listings`.
Yn gyntaf ychwanegwch y pecyn i'r rhaglith:

    \usepackage{listings}

Nawr ellir ychwanegu cod yn dwy ffordd, trwy deipio'r cod, neu trwy fewnbynnu
ffeil.
Er mwyn teipio'r cod yn uniongyrchol, defnyddiwch yr amgylchedd `lstlisting`:

    \begin{lstlisting}
    for i in range(100):
        print(i ** 2)
    \end{lstlisting}

Os oes cod mewn ffeil gadach chi (er enghraifft mewn ffeil `.py`, neu `.R`) yna
gallwch ddefnyddio `\lstinputlisting` mewn ffordd debyg i `\includegraphics`.
Gallwch hyn yn oed setio iaith y cod i wneud yn si&#373;r fod yna uwch-oleuo
cystrawen ystyrlon (er dylach gwneud yn si&#373;r fod yr iaith wedi'i
[chefnogi](https://www.sharelatex.com/learn/Code_listing)):

    \lstinputlisting[language=Python]{source_code.py}

Pecyn da arall ar gyfer cynnwys pytiau cod yw
[minted](ftp://ftp.dante.de/tex-archive/macros/latex/contrib/minted/minted.pdf)
sy'n galluogu uwch-oleuo cystrawen bert.

> ***Her:*** O dan eich tabl o ffrwythau, ychwanegwch ffigwr sy'n dangos y cod
LaTeX a ddefnyddioch i greu'r tabl.
Ychwanegwch gapsiwn priodol, labelwch y ffigwr, a ysgrifennwch frawddeg neu dau
yn cyfeirio ato.



&nbsp;

---

<h1 id="8">8. Amgylcheddau</h1>

Pob tro rydym yn dechrau adran gyda datganiad sy'n dechrau gyda `\begin{` a'i
gorffen gyda `\end{`, mae'r cynnwys o fewn y datganiadau yn tu fewn i
amgylchedd.
Dyma rhestr o rhai amgylcheddau defnyddiol nad ydynt wedi edrych arnyn nhw hyd
yn hyn:

+ `\begin{center}` ac `\end{center}`: Canoli'r holl cynnwys.
+ `\begin{figure}` ac `\end{figure}`: Amgylchedd ar gyfer ffigyrau, lluniau a diagrammau.
+ `\begin{table}` ac `\end{table}`: Amgylchedd yn debyg i `figure` ar gyfer tablau gyda `tabular`.
+ `\begin{multicols}` ac `\end{multicols}`: Amgylchedd i rhoi'r ysgrifen mewn colofnau.
+ `\begin{proof}` ac `\end{proof}`: Amgylchedd ar gyfer ysgrifennu profion mathemategol.

Gan ddefnyddio'r pecyn `asmthm` cawn mynediau i nifer o gorchmynion ar gyfer
creu amgylcheddau defnyddiol.
Defnyddiwn nhw fel arfer ar gyfer *theoremau*, *diffiniadau*, *gosodiadau*,
*sylwadau* ac yn y blaen.

I ddiffinio amgylchedd Theorem yn y rhaglith:

    \usepackage{asmthm}

    \newtheorem{theorem}{Theorem}

Mae hwn yn rhoi algylchedd `theorem` rhifol sy'n dechrau gyda'r gair `Theorem`.
Nawr allwn ni ysgrifennu theorem a prawf fel y ganlyn:

    \begin{theorem}
      $\log_a{B} + \log_a{C} = \log_a{BC}$
    \end{theorem}

    \begin{proof}
      Gadawer i $x = \log_a{B}$ and $y = \log_a{C}$.
      Nawr:
      \begin{align}
        a^x a^y &= BC\\
        a^{x + y} &= BC\\
        x + y &= \log_a{BC}\\
        \log_a{B} + \log_a{C} &= \log_a{BC}
      \end{align}
      fel sydd angen.
    \end{proof}

> ***Her:*** Dewisiwch day theorem syml a rhowch eu profion trwy diffinio
amgylchedd theorem newydd.

> ***Her:*** Crëwch amgylchedd diffiniad a'i ddefnyddio i diffinio dau term
mathemategol.


&nbsp;

---

<h1 id="9">9. Llyfryddiaethau</h1>

I greu llyfryddiaethau a chyfeiriadau, mae angen ychwanegu ffeil `.bib` yn
cynnwys holl wybodaeth y cyfeiriadau a ddefnyddiwyd.
Dylai'r ffeil cynnwys rhestr o gofnodion yn edrych fel hwn:

    @article{jackson57,
      author  = "Jackson, J.",
      title   = "Networks of waiting lines.",
      year    = "1957",
      journal = "Operations research",
      volume  = "5",
      number  = "4",
      pages   = "518--521"
    }

Mae'r llinell gyntaf fan hyn `jackson57` yw'r dynodwr a ddiffiniwyd gan y
defnyddiwr, a hwn a ddefnyddir i gyfeirio at yr erthygl yn y ffeil `.tex`.
Mae pob llinell arall yn disgrifio'r erthygl ei hun.
Mae cael gafael ar y wybodaeth hon yn hawdd os ydych yn defnyddio
[Google Scholar](https://scholar.google.co.uk/), chwiliwch am yr erthygl,
cliciwch `Cite` ac yna `BibTeX`.

Fe allwch gyfeirio at nifer o wahanol fath o ffynhonnell gwybodaeth, gan gynnwys
llyfrau a gwefannau, mae mwy o wybodaeth ar gael
[yma](https://en.wikibooks.org/wiki/LaTeX/Bibliography_Management#BibTeX).

I gyfeirio at ffynhonnellau yn y prif gorff, defnyddiwch y gorchymyn `\cite`:

    Fe astudiwyd rhwydweithiau o giwiau yn gyntaf yn \cite{jackson57}.

Yn olaf, rhaid dweud wrth LaTeX ble i ffeindio'r ffeil `.bib` ac i allbynnu
llyfryddiaeth.
Gadewch i ni alw ein ffeil bib yn `refs.bib`.
Ar ddiwedd y ddogfen (cyn `\end{document}`) ychwanegwch:

    \bibliographystyle{plain}
    \bibliography{refs}

> ***Her:*** Chwiliwch am erthygl, llyfr a gwefan (dibynadwy), a ychwanegwch nhw
i ffeil `.bib`.
Ysgrifennwch frawddegau sy'n cyfeirio at y ffynhonnellau yma, ac ychwanegwch
lyfryddiaeth i'ch erthygl.


&nbsp;

---

<h1 id="10">10. Cyflwyniadau</h1>

Hyd yn hyn rydym ond wedi ystyried y dosbarth dogfen `article`.
Gallwn creu cyflwyniadau fel rhai 'powerpoint' gyda latex trwy defnyddio'r
dosbarth dogfen `beamer`.
Dylai rhaglith y cyflwyniad beamer edrych fel hyn:

    \documentclass{beamer}

    \begin{document}
    % Eich cynnwys fan hyn...
    \end{document}

Mae cyflwyniad Beamer yn cynnwys cyfres o 'fframau'.
Mae gan rhain cynnwys tu fewn i amgylchedd `frame`.
Gall ffrâm cael teitl, wedi'i osod gan `\frametitle{`:

    \begin{frame}
      \frametitle{Teitl fy ffr\^{a}m}
      Cynnwys...
    \end{frame}

<img src="{{site.baseurl}}/images/beamer-cy.png" width="600">{: .center-image }

Gallwn cynnys popeth rydym wedi edrych arnynt hyd yn hyn o fewn cynnwys y ffrâm:
rhestrau, tablau, ffigyrau, mathemateg a cod.
Hefyd mae gan Beamer gorchmynion pellach ar gyfer trin
[troshaenau](https://www.sharelatex.com/blog/2013/08/20/beamer-series-pt4.html):

+ Mae `\pause` yn splitio ffrâm: rhoddir cynnwys cyn y gorchymyn hyn ar un
ffrâm, ac ar y ffrâm nesaf yn bydd y cynnwys cyn ac ar ôl y gorchymyn yma.
+ Mae `\onslide<3>{}` a `\only<3>{}` yn opsiynnau troshaen fwy hyblyg. Bydd y
cynnwys o fewn y cromfachau cyrliog yn dangos are y troshaen y rhif sydd o fewn
y symbolau `<` ac `>`; yn yr achos yma ar y 3ydd troshaen. I dangos cynnwys ar
fframau o'r trydydd troshaen ymlaen gallwn ychwanegu llinell doriad: `<3->`.
+ Nodwch bod `\onslide` ac `\only` yn ymddwyn bach yn wahanol o rhan leoliadau.
Cymharwch:

      \begin{frame}
        \frametitle{Enghreifftiau troshaen}
        \onslide<1->{Cyntaf}
      
        \onslide<2>{Ail}
      
        \onslide<3>{Trydydd}
      \end{frame}

  <img src="{{site.baseurl}}/images/onslide1-cy.png" width="230">
  <img src="{{site.baseurl}}/images/onslide2-cy.png" width="230">
  <img src="{{site.baseurl}}/images/onslide3-cy.png" width="230">

  i:

      \begin{frame}
        \frametitle{Enghreifftiau troshaen}
        \only<1->{Cyntaf}
      
        \only<2>{Ail}
      
        \only<3>{Trydydd}
      \end{frame}

  <img src="{{site.baseurl}}/images/only1-cy.png" width="230">
  <img src="{{site.baseurl}}/images/only2-cy.png" width="230">
  <img src="{{site.baseurl}}/images/only3-cy.png" width="230">

Gallwn addasu cyflwyniadau Beamer trwy dewis thema a thema lliw.
I osod rhain, defnyddiwch y gorchmynion isod mewn rhaglith y dogfen Beamer
(mae'r enghraifft yma yn dewis y thema `Singapore` a'r thema lliw `crane`):

    \usetheme{Singapore}
    \usecolortheme{crane}

Cymerwch cipolwg ar y
[matrics steiliau beamer](https://hartwork.org/beamer-theme-matrix/)
i weld esiamplau o holl cyfuniadau y themau a'r themau lliw.

> ***Her:*** Crëwch cyflwyniad tri ffrâm yn disgrifio theorem mathemategol o'ch
dewis. Dewisiwch thema a thema lliw, defnyddiwch mathemateg, ychwanegwch ffigwr,
ac arbrofwch gyda opsiynnau troshaen.

&nbsp;

---


Yn olaf, efallai bydd nifer ohonoch yn ffeindio'r
[templed yma](https://github.com/drvinceknight/CU_BSc_LaTeX_Template) o werth
wrth ysgrifennu eith prosiectau blwyddyn olaf.
[Dyma](https://www.overleaf.com/read/frqfmpwhzndm) linc i prosiect Overleaf gyda
datrysiadau i rhai o'r heriau.
