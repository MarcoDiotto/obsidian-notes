# Lezione I
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
Qualsiasi algoritmo di ordinamento per confronto richiede $\Omega(n\ log\ n)$ confronti nel caso peggiore.

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

 ```c
 countingsort(array A, array B, int n, int k)               
	 array C[0...k]
     for i = 0 to k
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


# Lezione 2
___
## Radix Sort

* Aumenta l'applicabilità del **Counting Sort**.
* Serve per ordinare elementi con $d$ cifre, dove la cifra meno significativa è in posizione 1 e quella più significativa in posizione $d$.
 
```c
radixsort(array A, int d)
	for int i to d
		//Usa un ordinamento stabile per ordinare l'array a
		//sulla cifra i

```

Utilizzo un **Counting Sort**, e lo applico partendo dalle cifre meno significative:

![[Pasted image 20240213122817.png]]

#### $\color{red} \textbf{Dimostrazione della correttezza per induzione}$

**Caso Base**:
	$i = 1$ $\rightarrow$ ordino l'unica colonna disponibile.

**Ipotesi Induttiva**: 
	suppongo che le cifre delle colonne $i...i-1$ siano ordinate.

**Passo Induttivo**: 
	dimostro che un algoritmo stabile sulla colonna $i$ lascia le colonne $1...i$ ordinate.

* Se  2 cifre in posizione $i$ sono uguali, per la stabilità rimangono nello stesso ordine e per ipotesi induttiva sono ordinate.
* Se 2 cifre in posizione $i$ sono diverse, allora l'algoritmo di ordinamento sulla colonna $i$-esima le ordina e le mette in posizione corretta. 

#### $\color{red} \textbf{Analisi della complessità}$

*Lemma*: Dati $n$ numeri di $d$ cifre, dove ogni cifra può variare fino a $k$ valori possibili, la procedura **radix sort** correttemente ordina i numeri nel tempo di $\color{green}\Theta(d(n + k))$.

##### $\color{red} \textbf{Dimostrazione del lemma per induzione}$
* Per ogni iterazione $\theta(n + k)$.
* $d$ iterazioni.
* totale è $\color{green}\Theta(d(n + k))$.

Se $k = O(n)$, il tempo di esecuzione è $\color{green}\Theta(d\cdot n)$  e se $d$ è costante $\color{green}\Theta(n)$.


### Come ripartire le chiavi in cifre?

*Esempio*: consideriamo una parola di 32 bit, spezzo una parola in 4 byte (in 4 cifre di 8 bit).
$$ b=32,\ r=8,\ d=4,\ ci \in [0...2^r-1]$$ 
*Lemma*: Dati $n$ numeri di $b$ bit e un intero positivo $r \in b$, la procedura `radixsort` ordina correttamente questi numeri in tempo $\color{green}\Theta((\frac{b}{r})\cdot (n+2^n))$ se l'algoritmo di ordinamento stabile usato richiede tempo $\color{green} \Theta(n + k)$ per input nel'intervallo $[0...k]$.

##### $\color{red} \textbf{Dimostrazione del lemma}$
Per $r \leq b$
* Spezziamo ogni numero in $\lceil \frac{b}{r} \rceil$ cifre di $n$ bit ciascuna.
* Ogni cifra varia in $[0...2^r-1]$
* Possiamo applicare il **counting sort** con $k=2^r-1$.
* Ogni passaggio richiede $\color{green} \Theta(n + k)$ ovvero $\color{green} \Theta(n + 2^r)$.
* Esegue d = $\lceil \frac{b}{r} \rceil$ passaggi.
* Infine il tempo di esecuzione totale è $\color{green}\Theta((\frac{b}{r}) \cdot (n + 2^r)$.


Dati i valori di $n$ ed $b$, vogliamo scegliere il valore $r$ con $r \in b$ , che rende minima $(\frac{b}{r}) \cdot (n+2^r)$.

* Se $b \leq \lfloor log\ n \rfloor$  allora per qualsiasi valore $r \leq b$ si ha $(n + 2^r) = \color{green} \Theta(n)$. Quindi scegliendo $r = b$ si ottiene $(\frac{b}{b}) \cdot (n + 2^b) = \color{green} \Theta(n)$.
* Se $b \geq \lfloor log\ n \rfloor$ allora scegliamo $r$ che sia massimo sotto la condizione che $n \geq 2^r \rightarrow  r=log\ n$. Quindi si ottiene che $(\frac{b}{log\ n}) \cdot (n + 2^{log\ n}) = \color{green} \Theta(\frac{b \cdot n}{log\ n})$.
* Se $b = O(log\ n)$, per esempio $b = c \cdot log\ n$ con $c$ costante, i numeri variano fra $0...2^b-1 = 0...2^{c \cdot log\ n}-1 = 0...n^c-1$. Il tempo di esecuzione del **radix sort** pertanto è $\Theta(\frac{n \cdot c \cdot log\ n}{log\ n}) = \color{green}\Theta(n)$.

Da cui si deduce che: $[0...n^c-1]$ con $n$ numeri:
* **counting sort** $\rightarrow$ $\Theta(n+n^c) = \Theta(n)$.
* **radix sort** $\rightarrow$ $\Theta(n)$.


$\color{red} \textbf{Esercizio}$
* Dimostrare come ordinare $n$ numeri interi compresi nell'intervallo fra $0..n^4-1$ nel tempo $O(n)$.

$\Theta(d(n+k))$ con $d =$ **#cifre** e $k=$ **numero di valori che vogliamo**. 

Se rappresento il numero in base $n$ ogni cifra varia fra $[0...n-1]$. 
Per rappresentare un numero nell'intervallo $[0...n^4-1]$ in base $n$ uso $\color{green}\log_n(n^4) = 4$. 

# Lezione 3
___
## Tabelle Hash
Nell'applicazione ha bisogno:
* *Insieme dinamico* su cui sono definite le operazioni **instert**, **delete** e **search**.
* Ogni elemento ha una *chiave* estratta dall'*universo*  $U = \{0,1...w-1\}$  dove $v$ non è troppo grande.
* Nessun elemento ha la stessa chiave (*chiavi distinte*).

### Array

Si può utilizzare un array `T[0...w-1]`:
* Ogni posizione (o *cella*) corrisponde ad una *chiave* in $U$.
* Se c'è un elemento $x$ con chiave $k$ allora `T[k]` contiene un puntatore ad $x$.
* Altrimenti se l'insieme non contiene alcun elemento con chiave $k$ $\rightarrow$ `T[k] = NIL`.

Di seguito una *tabella ad indirizzamento diretto*:

![[Pasted image 20240213134541.png]]

Se la chiave non è presente nell'insieme si inserisce un `NIL`.

##### $\color{red} \textbf{Search}$
```C
Direct_access_search(T, k)
	Return T[k]
```

Il tempo di esecuzione è $\color{green} \Theta(1)$.

##### $\color{red} \textbf{Insert}$
```C
Direct_access_insert(T, x)
	T[x.key] = x
```

Il tempo di esecuzione è $\color{green} \Theta(1)$.

##### $\color{red} \textbf{Delete}$
```C
Direct_access_delete(T, x)
	T[x.key] = NIL
```

Il tempo di esecuzione è nuovamente $\color{green} \Theta(1)$.


* **Vantaggio**: Tutte le operazioni avvengo in tempo $\color{green} \Theta(1)$.
* **Svantaggio**: Lo spazio utilizzato è proporzionale a $w$, non al numero $n$ di elementi memorizzati $\rightarrow$ grande spreco di memoria $n << w$.


### Tabelle Hash
* Lo spazio può essere ridotto a $\color{green} \Theta(|K|)$. $\rightarrow$ $K =$ insieme considerato.
* Il tempo di **ricerca** è *costante* ma *solo nel caso medio*, nel caso peggiore è $\color{green} \Theta(n)$.

**Idea**: invece di memorizzare un elemento con chiave `k` nella cella con indice `k`, si una una funzione `h` e si memorizza l'elemento nella cella `h[k]`.
* `h` $\rightarrow$ la funzione hash
* `h.U` $\rightarrow$ $\{0 ... m-1\}$, dove $m$ è la dimensione della tabella hash che è generalmente molto più piccola di $|U|$.
 
![[Pasted image 20240214090632.png]]

Le tabelle hash possono soffrire del problema delle **collisioni**

### Collisioni
Quando un elemento da inserire è mappato in una cella già occupata, si verifica una **collisione**.

* $|U| > m$ $\rightarrow$ *può accadere* che ci siano collisioni.
* $|K| > m$  $\rightarrow$ *c'è sicuramente* una collisione.

Metodi di risoluzione delle collisioni:
* **Concatenamento** (o **lista di collisioni**).
* **Indirizzamento aperto**.

### Risoluzione delle collisioni mediante il concatenamento
Si mettono tutti gli elementi che sono associati alla *stessa cella* in una **lista concatenata**:
* la *cella* `j` contiene un puntatore alla testa della lista, di tutti gli elementi memorizzati che sono mappati in `j` $\rightarrow$ `h[k] = j`.
* Non ci sono elementi, la cella `j` contiene `NIL`.
##### $\color{red} \textbf{Insert}$
```c
chained_hash_insert(T, x)
 inserisce x in testa alla lista T[h(x.key)]
```

Il tempo di esecuzione è $\color{green} \Theta(1)$.

**Ipotesi**: 
* Il calcolo della tabella hash è $\color{green} \Theta(1)$.
* Si suppone che l'elemento da inserire non sia nella lista.
##### $\color{red}\textbf{Search}$
```c
chained_has_search(T, k)
	ricerca un elemento con chiave k nella lista T[h[k]]
```

Il tempo di esecuzione di questa funzione nel caso peggiore è proporzionale alla lunghezza della lista nella cella `h[k]`
##### $\color{red} \textbf{Delete}$
```c
chained_hash_delete(T, x)
	cancella x dalla lista T[h(x.key)]
```

* Il tempo di esecuzione nel caso peggiore è  $\color{green} O(1)$ se la lista è **doppiamente concatenata**. Poiché si fornisce il puntatore all'elemento `x`,  per cancellare non è richiesta alcuna **ricerca**.
* Se la lista è **singolarmente concatenata**, la cancellazione richiede di cercare il predecessore di `x` nella lista `T[h(x.key)]` $\rightarrow$ *il costo della cancellazione è il costo della ricerca*
### Analisi del'hashing con concatenamento

Sia `T` una *tabella hash*  con $m$ *celle* in cui sono stati mappati $n$ *elementi* nella quale vogliamo cercare l'elemento con chiave `k`.

* Il **caso** **peggiore** si verifica quando tutti gli elementi sono mappati nella stessa cella $\rightarrow$ unica lista di lunghezza $n$.  Il tempo di esecuzione della ricerca è $\color{green} O(n)$, a cui si somma il tempo per il calcolo della funzione hash (che supponiamo essere $\color{green} \Theta(1)$).
* Il **caso medio** dipende dal modo in cui la funzione hash distribuisce mediamente le chiavi per le $m$ celle.
#### Caso Medio

**Ipotesi**:  *hashing uniforme ed indipendente* $\rightarrow$ ogni elemento ha la stessa probabilità di essere mandato in una qualsiasi delle $m$ celle, indipendentemente dalle celle in cui sono mandati gli altri elementi $\rightarrow$ $\forall i \in [0 ... m-1]\ Q(i) = \frac{1}{m}$ con $Q =$ probabilità che una chiave finisca nella cella $i$.

**Definizione**: il *fattore di carico* di una tabella hash con $m$ celle e $n$ elementi memorizzati è $\alpha = \frac{n}{m}$.

**Osservazione**: $$\alpha < 1 \ \ \ \ \alpha = 1 \ \ \ \ \alpha >1$$
$\alpha > 1$ perché gli elementi  sono memorizzati su liste!

Sotto l'ipotesi di *hashing uniforme ed indipendente*:
* $nj =$ lunghezza della lista `T[j]`.
* il valore medio di $nj$ è $\frac{n_0+n_1+ ... +n_{m-1}}{m} = \frac{n}{m} = \color{green} \alpha$.
* Di conseguenza $\alpha \rightarrow$ numero medio di elementi memorizzati in una lista.

**Ipotesi**: calcolo della funzione hash *costante*.
###### $\color{red} \textbf{Teorema}$
In una tabella hash in cui le collisioni sono risolte con il concatenamento, una *ricerca senza successo* richiede un tempo $\color{green} \Theta(1 + \alpha)$ nel caso medio, nell'ipotesi di *hashing uniforme ed indipendente*.

$\color{red} \textbf{Dimostrazione}$:
* calcolo $j = h(k) \rightarrow \color{green} O(1)$.
* accedo a `T[j]` $\rightarrow \color{green} O(1)$.
* scorro la lista `T[j]` $\rightarrow \color{green} \Theta(a)$.
Di conseguenza il tempo totale è $\color{green} \Theta(1 + \alpha)$ .
###### $\color{red} \textbf{Teorema}$
In una tabella hash in cui le collisioni sono risolte con il concatenamento, una ricerca *con successo* richiede un tempo $\color{green} \Theta(1 + \alpha)$  nel caso medio, nell'ipotesi di *hashing uniforme ed indipendente*

$\color{red} \textbf{Dimostrazione}$:
* calcolo $j = h(k) \rightarrow \color{green} O(1)$.
* accedo a `T[j]` $\rightarrow \color{green} O(1)$.
* scorro la lista `T[j]` fino a trovare $k$ $\rightarrow$ mediamente trovo l'elemento a metà: $\color{green} \Theta(\frac{\alpha}{2})$.
Di conseguenza il tempo totale di esecuzione è $\color{green} \Theta(1 + \frac{\alpha}{2})\rightarrow \Theta(1 + \alpha)$

**Interpretazione**: nel caso medio il costo della ricerca è $\Theta(1 + \alpha)$, se $n = O(m) \rightarrow$ il numero delle celle è proporzionale al numero di elementi da memorizzare:
$$\alpha = \frac{n}{m} = \frac{O(n)}{m} = O(1)$$
**Attenzione**: se $n$ cresce le prestazioni possono peggiorare.