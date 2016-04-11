---
layout: post
title: Venn Diagrams with LaTeX and TikZ
tags:
- latex
- logic 
comments: true
date: 
---

## The Initial Diagram ##

First, add the following to the preamble:


``` tex
\usepackage{tikz}
\usetikzlibrary{shapes,backgrounds}
```

The next step is to define the three circles in the body of the document. This only needs to to be done once; they can be called repeatedly in the same document. I named them in a way that I could remember which was the subject term, middle term, and predicate term:

``` tex
\def\sub{(0,0) circle (1.5cm)}
\def\mid{(-60:2cm) circle (1.5cm)}
\def\pred{(0:2cm) circle (1.5cm)}
```


Once the circles have been defined, they can be drawn and labeled. I prefer to use a heavier line than the default, that can be called as an option to *tikzpicture*.

``` tex
\begin{tikzpicture}[thick]

  \begin{scope}

    % Draw the circles
    \draw \sub;
    \draw \pred;
    \draw \mid;

    % Label the circles
    \draw (-2,-0) node {$S$};
    \draw (1,-4) node {$M$};
    \draw (4,0) node {$P$};

  \end{scope}

\end{tikzpicture}
```

## Shading ##

### Universal Negations ###


Shading is simple with TikZ, and, in most cases, relatively intuitive. To shade an entire circle, use the "\fill" command. For example, "\fill \sub" fills the entire subject circle. To fill the intersection of the subject and predicate circles, we need to tell TikZ to ignore everything that is outside the predicate circle, then fill the subject circle. This is done with the "\clip" command. This code produces shades the intersection of *S* and *P*:

``` tex
\begin{tikzpicture}[thick]
  \begin{scope}
    \begin{scope} %Shade intersection of S and P
      \clip \pred;
      \fill[gray] \sub;
    \end{scope}

    \draw \sub;
    \draw \pred;
    \draw \mid;

    \draw (-2,-0) node {$S$};
    \draw (1,-4) node {$M$};
    \draw (4,0) node {$P$};
  \end{scope}
\end{tikzpicture}
```



### Universal Affirmations

Shading everything that is one circle, but not in another is a bit trickier. It involves using something called the "even odd rule" in TikZ. This code shades the portion of the subject circle that is not in the predicate circle:

``` tex
\begin{tikzpicture}[thick]
  \begin{scope}[even odd rule]% Shade S without P
    \clip \pred (-1.5,-1.5) rectangle (1.5,1.5);
    \fill[gray] \sub;
  \end{scope}

  \draw \sub;
  \draw \pred;
  \draw \mid;

  \draw (-2,-0) node {$S$};
  \draw (1,-4) node {$M$};
  \draw (4,0) node {$P$};
\end{tikzpicture}
```


To shade S without M:


\begin{scope}[even odd rule]% Shade S without M
  \clip \mid (-1.5,-1.5) rectangle (1.5,1.5);
  \fill[gray] \sub;
\end{scope}



M without S:


\begin{scope}[even odd rule]% Shade M without S
  \clip \sub (-0.5,-3.3) rectangle (2.5,0);
  \fill[gray] \mid;
\end{scope}



M without P:


\begin{scope}[even odd rule]% Shade M without P
  \clip \pred (-0.5,-3.3) rectangle (2.5,0);
  \fill[gray] \mid;
\end{scope}


P without M:


\begin{scope}[even odd rule]% Shade P without M
  \clip \mid (-0,-1.5) rectangle (3.5,1.5);
  \fill[gray] \pred;
\end{scope}



Finally, to shade P without S:


\begin{scope}[even odd rule]% Shade P without S
  \clip \sub (0,-1.5) rectangle (3.5,1.5);
  \fill[gray] \pred;
\end{scope}



\section{Particulars}

\textbf{I} and \textbf{O} sentences require an ``x'' to be placed in some region of the diagram. To do that, just draw a node at the desired location. Here are the locations of the seven sections in the diagram, as found in Figure \ref{fig:particulars}. 

\begin{verbatim}
\draw (-0.5,0.3) node {1};
\draw (1,0.3) node {2};
\draw (2.5,0.3) node {3};
\draw (0.2,-0.9) node {4};
\draw (1,-0.6) node {5};
\draw (1.8,-0.9) node {6};
\draw (1,-2) node {7};
\end{verbatim}

\begin{figure}[h]
\begin{center}
\begin{tikzpicture}[thick]
\begin{scope}
  % Draw the circles
    \draw \sub;
    \draw \pred;
    \draw \mid;  
% Label the circles
    \draw (-2,-0) node {$S$};
    \draw (1,-4) node {$M$};
    \draw (4,0) node {$P$};
% Add other labels
\draw (-0.5,0.3) node {1};
\draw (1,0.3) node {2};
\draw (2.5,0.3) node {3};
\draw (0.2,-0.9) node {4};
\draw (1,-0.6) node {5};
\draw (1.8,-0.9) node {6};
\draw (1,-2) node {7};
  
\end{scope}

\end{tikzpicture}

\caption{Particulars}
\label{fig:particulars}
\end{center}
\end{figure}


\section{Examples}

Here are some examples to show how full arguments are diagrammed. 

\subsection{Celarent (EAE-1)}

\begin{figure}[h]
  \centering
\begin{tikzpicture}[thick]

\begin{scope}
    \draw (-2,-0) node {$A$};
    \draw (1,-4) node {$B$};
    \draw (4,0) node {$C$};

\begin{scope}[even odd rule]% Shade S without M
            \clip \mid (-1.5,-1.5) rectangle (1.5,1.5);
        \fill[gray] \sub;
        \end{scope}

\begin{scope} %Shade intersection of M and P
  \clip \pred;
  \fill[gray] \mid;
\end{scope}

\draw \sub;
\draw \pred;
\draw \mid;
\end{scope}

\end{tikzpicture}
  
  \caption{Celarent}
  \label{fig:celarent}
\end{figure}

\newpage

Figure \ref{fig:celarent} is produced by the following code:

% \begin{enumerate}\addtolength{\itemsep}{-0.5\baselineskip}
% \item No B are C
% \item \underline{All A are B}
% \item [$\therefore$] No A are C
% \end{enumerate}



\begin{verbatim}
\begin{tikzpicture}[thick]
  \begin{scope}
    \draw (-2,-0) node {$A$};
    \draw (1,-4) node {$B$};
    \draw (4,0) node {$C$};

    \begin{scope}[even odd rule]% Shade S without M
      \clip \mid (-1.5,-1.5) rectangle (1.5,1.5);
      \fill[gray] \sub;
    \end{scope}

    \begin{scope} %Shade intersection of M and P
      \clip \pred;
      \fill[gray] \mid;
    \end{scope}

    \draw \sub;
    \draw \pred;
    \draw \mid;
  \end{scope}
\end{tikzpicture}

\end{verbatim}


\newpage
\subsection{Disamis (IAI-3)}

\begin{figure}[h]
  \centering
  \begin{tikzpicture}[thick]

    \begin{scope}
      \draw (-2,-0) node {$A$};
      \draw (1,-4) node {$B$};
      \draw (4,0) node {$C$};

      \begin{scope}[even odd rule]% Shade M without S
        \clip \sub (-0.5,-3.3) rectangle (2.5,0);
        \fill[gray] \mid;
      \end{scope}

      \draw (1,-.6) node {X};

      \draw \sub;
      \draw \pred;
      \draw \mid;
    \end{scope}

  \end{tikzpicture}
  
  \caption{Disamis}
  \label{fig:disamis}
\end{figure}

Figure \ref{fig:disamis}  is produced by: 

\begin{verbatim}
\begin{tikzpicture}[thick]
  \begin{scope}
    \draw (-2,-0) node {$A$};
    \draw (1,-4) node {$B$};
    \draw (4,0) node {$C$};

    \begin{scope}[even odd rule]% Shade M without S
      \clip \sub (-0.5,-3.3) rectangle (2.5,0);
      \fill[gray] \mid;
    \end{scope}

    \draw (1,-.6) node {X};

    \draw \sub;
    \draw \pred;
    \draw \mid;
  \end{scope}
\end{tikzpicture}

\end{verbatim}

\section{Scaling}

TikZ graphics can be scaled easily with an option to the \texttt{tikzpicture} environment. This doubles the size of the picture:

\begin{verbatim}
\begin{tikzpicture}[thick,scale=2]
\end{verbatim}

This reduces the size by half:

\begin{verbatim}
\begin{tikzpicture}[thick,scale=.5]
\end{verbatim}

Unfortunately, this won't scale the text at the nodes, which will make the labels look ridiculously out of proportion. This can be fixed by adding an option to also scale the nodes.

\begin{verbatim}
\begin{tikzpicture}[thick,scale=2, every node/.style={transform shape}]
\end{verbatim}

Figures \ref{fig:doublescale} and \ref{fig:halfscale} are double and half-size, respectively.


\begin{figure}[h]
  \centering
\begin{tikzpicture}[thick,scale=2, every node/.style={transform shape}]

\begin{scope}
    \draw (-2,-0) node {$A$};
    \draw (1,-4) node {$B$};
    \draw (4,0) node {$C$};

\begin{scope}[even odd rule]% Shade M without S
            \clip \sub (-0.5,-3.3) rectangle (2.5,0);
        \fill[gray] \mid;
        \end{scope}

\draw (1,-.6) node {X};

\draw \sub;
\draw \pred;
\draw \mid;
\end{scope}

\end{tikzpicture}
  
  \caption{Double Scale}
  \label{fig:doublescale}
\end{figure}


\begin{figure}[h]
  \centering
\begin{tikzpicture}[thick,scale=.5, every node/.style={transform shape}]

\begin{scope}
    \draw (-2,-0) node {$A$};
    \draw (1,-4) node {$B$};
    \draw (4,0) node {$C$};

\begin{scope}[even odd rule]% Shade M without S
            \clip \sub (-0.5,-3.3) rectangle (2.5,0);
        \fill[gray] \mid;
        \end{scope}

\draw (1,-.6) node {X};

\draw \sub;
\draw \pred;
\draw \mid;
\end{scope}

\end{tikzpicture}
  
  \caption{Half Scale}
  \label{fig:halfscale}
\end{figure}

\end{document}
