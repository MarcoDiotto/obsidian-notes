___
##  Ordinamenti di confronto

**Utilizzano solamente confronti fra coppie di elementi per determinare l'ordine degli elementi**

Vogliamo determinare un limite inferiore per questo metodo:
* Un banale limite inferiore è $\Omega (n)$
*  Il limite inferiore più stretto tuttavia è $\Omega (n \ log \ n)$
* 

##### $\color{red}Dimostrazione$

$\color{green}Ipotesi$: supponiamo tutti gli elementi di input distinti.
Utilizziamo un $\color{green} albero \ di \ decisione$.

Esempio: ordina 3 elementi <$a_1, a_2, a_3$> utilizzando un insertion sort.

![[Pasted image 20240212104224.png]]

Per un input di dimensione $n$ <$a_1 ... a_n$> 
* ogni nodo interno è etichettato da $i, j$ con $i,j \in {1...n}$
	* significa confronto $a_i$ vs $a_j$
	* il sottoalbero sinistro da i successivi confronti se $a_i$ < $a_j$
	* il sottoalbero destro da i successivi confronti se $a_i$ > $a_j$
* ogni foglia da una permutazione <$\pi(1), \pi(2)...\pi(n)$> tale che $a_{\pi(1)} \leq a_{\pi(2)}....\leq a_{\pi(n)}$

Dato un qualsiasi algoritmo di ordinamento per confronto:
* un albero di decisione per ogni $n$
* l'albero modella tutte le possibili tracce di esecuzione
* tempo di esecuzione (# confronti) è la lunghezza di un cammino nell'albero
* tempo di esecuzione nel caso peggiore è l'$\color{green} altezza \ dell' \ albero$

Il limite inferiore sulle altezze di tutti gli alberi di decisione dove ogni permutazione compare come foglia è un limite inferiore al tempo di esecuzione  di un qualsiasi algoritmo di ordinamento per confronti.

**Quante sono le foglie di un albero di decisione di nostro interesse?**
	$\geq n!$ perché per essere corretto ogni permutazione deve comparire almeno una volta

$\color{red} Lemma$ : un albero binario di altezza $h$ ha al più $2^h$ foglie

##### $\color{red} Dimostrazione \ per \ induzione$

$(h=0)$  un albero con solo la radice ha un'unica foglia, $f=1 \leq 2^0 =1$

Assumiamo vera la proprietà per alberi di altezza $k<h$, cioè $f\leq2^k$ . Dimostro che è vera per h, cioè $f\leq2^h$ .
Sia $r$ la radice dell'albero $T$ di altezza $h$.

* Se $r$ ha un solo figlio:

![[Pasted image 20240212110839.png]]

$f$ sono le foglie di $T$ che sono le foglie di $T_1$.
$f = f_1 \leq 2^{h-1} \leq 2^h$ $\rightarrow$ per ipotesi induttiva poiché l'altezza di $T_1$ è $h-1 < h$

* Se $r$ ha 2 figli:

![[Pasted image 20240212111145.png]]

Il numero di foglie di $T$ è Il numero di foglie di $T_1$ e di $T_2$. Se $T_1$ ha altezza $h_1$ che è $<h$ e $T_2$ ha altezza $h_2$ che è $<h$ :  $f = f_1 + f_2 \leq 2^{h_1} + 2^{h_2}$  $\rightarrow$ per ipotesi induttiva $\leq 2^{max\{h1,h1\}} = 2^{1+ max\{h1,h1\}} = 2^h$ perché $h = 1+ max\{h1,h2\}$. 

#### $\color{red} Teorema$
Qualsiasi algoritmo di ordinamento per confronto richiede $\Omega(nlogn)$ confronti nel caso peggiore.

##### $\color{red} Dimostrazione$

Bisogna determinare l'altezza di un albero di decisione dove ogni permutazione appare come foglia. Si consideri un albero di decisione di altezza $h$ con le foglie che corrispondono ad un ordinamento per confronto di n elementi. Allora:

$$n!\leq f \leq 2^h \rightarrow per \ lemma$$ 
Utilizzo l' $\color{green}approssimazione \ di \ Stirling$:
$$n! = \sqrt{2\pi n} \cdot (\frac{2}{n})^h  \cdot (1 + \Theta(\frac{1}{n}))$$
Perciò per $n$ sufficientemente grandi coincide col termine più grande
$$h \geq log\ n! \geq log(\frac{n}{e})^n = n\ log(\frac{n}{e}) = n (log\ n - log\ e) = n (log\ n - \Theta(1)) = \Omega(n\ log\ n)$$

$\color{green}Corollario$: Heapsort e Mergesort sono algoritmi di ordinamento per confronto asintoticamente ottimali. La dimostrazione si deriva dal fatto che il loro limite superiore del tempo di esecuzione $O(n log n)$ corrisponde al limite inferiore $\Omega(n log n)$ nel caso peggiore.

___

## Counting Sort

**Assunzione**: i numeri da ordinare sono interi in un intervallo limitato da $0$ a $k$ per qualche intero $k$

**Input**:  `A[1..n]` dove  `A[j]` $\in$  `[0..k]`, `n` e `k` sono parametri.
**Output**:  `B[1..n]` ordinato.
**Memoria ausiliaria**:  `C[0...k]`

 ```
 countingsort(array A, array B, int n, int k)               
	 array C[0...k]
     for i = to k
	     C[i] = 0
	 for j = 1 to n
		 C[A[j]] = C[A[j]] +1
		 //C[i] = |{ x ∈ {1, n}, A[x] = i }| 
	 for i = 1 to k
		 C[i] = C[i] + C[i - 1]
		 //C[i] = |{ x ∈ {1, n}, A[x] = i }|
	 for j = n down to 1                //somme prefisse
		 B[C[A[j]]] = A[j]
		 C[A[j]] = C[A[j]] - 1
  ```  


L'algoritmo parte dal fondo per essere $\color{green} stabile$.
##### Tempo di esecuzione
Il primo ciclo costa $\Theta(k)$, il secondo $\Theta(n)$, il terzo $\Theta(k)$ e l'ultimo $\Theta(n)$, pertanto il tempo di esecuzione è $\color{red}\Theta(k + n)$.
In particolare se $k$ è limitato superiormente da $n$ il tempo di esecuzione è $\color{red}\Theta(n)$, tuttavia se la condizione non è verificata l'algoritmo non è conveniente.
