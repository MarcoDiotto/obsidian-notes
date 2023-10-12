
---
## CLASSI ASINTOTICHE 

$\newline$  
- $\textbf{CLASSE O}$ 

$$
O(g(n))\ = \  \{f(n)\ | \  \exists \ c\textgreater0, \ \exists \  n_0 \in \mathbb{N}  \ \backepsilon \ \forall n \geq n_0 : f(n) \textless c \ \cdot \ g(n) \}
$$

$O(gn)$ è l'insieme di tutte le funzioni tali per cui esiste $c\textgreater0$ per $n$ sufficientemente grande, dove $f(n)\leq c \cdot g(n)$ (le costanti hanno poco interesse)

#### *Esempio*

$$\frac{1}{2}n^2-3n = O(n^2)$$
Per dimostrare l'uguaglianza dobbiamo trovare $c$ e $n_0$.

$$\exists \ c \ \textgreater \ 0, \   \exists \ n_0 \in \mathbb{N} \backepsilon  \forall n \geq n_0 : \frac{1}{2}n^2-3n \leq c \cdot n^2 $$
Da cui si ricava:


$$\frac{1}{2}n^2-3n \leq c \cdot n^2 \iff  \frac{1}{2}n - 3 \leq c \cdot n$$
$$\iff \frac{1}{2}n - c \cdot n \leq 3$$
$$\iff (\frac{1}{2}-c)\cdot n \leq 3 $$
Da cui si ricava $c\geq \frac{1}{2} \ \textgreater \ 0 \ \forall \ n \geq 1$  (poiché per noi i naturali iniziano da $1$).

E infine  $c = \frac{1}{2}$ e $n_0 = 1$

***

 - $\textbf{CLASSE}$ $\Omega$ 

$$\Omega(g(n)) = \{f(n)\ | \ \exists \  c \ \textgreater \ 0, \exists \ n_0 \in \mathbb{N} \backepsilon \forall n \geq n_0 :  c \cdot g(n) \leq f(n) \  \}$$

Si evidenzia di conseguenza un comportamento opposto rispetto alla classe asintotica precedente. $f(n)$ si trova sempre "sopra" $c \cdot g(n)$ dopo un certo valore $n_0$.

#### *Esempio*

$$\frac{1}{2}n^2-3n = \Omega(n^2)$$

Per dimostrare l'uguaglianza dobbiamo trovare $c$ e $n_0$.

$$\exists \ c \ \textgreater \ 0, \ \exists \ n_0 \in \mathbb{N} \backepsilon \forall n \geq n_0 : c \cdot n^2 \leq \frac {1}{2}n^2-3n$$
Da cui si ricava:

$$c \cdot n^2 \leq \frac {1}{2}n^2-3n \iff c \cdot n \leq \frac{1}{2}n-3$$
$$\iff n(\frac{1}{2}-c) \geq 3$$

Ma $\frac{1}{2}-c \ \textgreater \ 0$, perciò $c<\frac{1}{2}$ e $0 < c < \frac{1}{2}$.

Si ha poi:

$$n\geq \frac{3}{\frac{1}{2}-c} = \frac{6}{1-2c}$$
Scegliamo $c =\frac{1}{14}$.

Si ottiene:
$$n\geq \frac{6}{1-\frac{1}{7}} = 7$$

Quindi infine: $c = \frac{1}{14}$  e $n_0 = 7$

***

- $\textbf{ClASSE}$ $\Theta$

$$
\Theta(f(n)) = \{f(n)\ |\ \exists \ c_1 > 0, \ \exists \ c_2 > 0, \exists \ n_0 \in \mathbb{N} \backepsilon \forall n \geq n_0 : c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)  \}
$$
Dopo $n_0$ $f(n)$ è sotto a $c_2 \cdot g(n)$ e sempre sopra a $c_1 \cdot g(n)$.  


