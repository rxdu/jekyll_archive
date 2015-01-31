---
layout: post
title: "Use of IEEE Conference LaTex Template with .bib File"
date: 2014-01-20 18:05:23 -0500
comments: true
categories: LaTex
---

Recently I need to use the IEEE LaTex template (from this [site](http://www.ieee.org/conferences_events/conferences/publishing/templates.html)) for a conference paper. This template doesn't use a .bib file for the management of references unless you make some modifictions. In my first try to use it, I got this error during compiling:

```
Something's wrong--perhaps a missing \item. \end{thebibliography}
```

 <!-- more -->
I googled this issue and tried different solutions. Finally I figured it out how to fix this error (thanks to Velin's help). The following are the steps to make a successful compilation.

* Download both  *LaTeX Archive Contents* and *LaTeX (Bibliography Files)*
* Extract both packages to the same folder
* Uncomment the line: 

```
\usepackage{cite}
```

* Uncomment the lines:

```
\bibliographystyle{IEEEtran}
\bibliography{IEEEabrv,../bib/paper}
```

specify the name and location of your .bib file. For example, change the second line above to: 

```
\bibliography{IEEEexample}
```

* Comment the lines:

```
\begin{thebibliography}{1}
\bibitem{IEEEhowto:kopka}
H.~Kopka and P.~W. Daly, \emph{A Guide to \LaTeX}, 3rd~ed.\hskip 1em plus
0.5em minus 0.4em\relax Harlow, England: Addison-Wesley, 1999.
\end{thebibliography}
```

* Cite at least one item in the paper. For example, add 

```
\cite{IEEEexample:article_typical} 
```

at the end of the acknowledgement section.

* Compile the tex file and you should get no error.

*PS*: If you have got the error before you try the steps stated above, you should clean the files generated from the unsuccessfuly compilation. Otherwise you will get the same error even if you have made all modifications.

You can also download the successfully compiled template from here: http://sdrv.ms/17ynR0g
