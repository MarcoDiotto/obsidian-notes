# Ordinamento in O(n)
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

$\Theta(d(n+k))$ con $d =$ **# cifre** e $k=$ **numero di valori che vogliamo**. 

Se rappresento il numero in base $n$ ogni cifra varia fra $[0...n-1]$. 
Per rappresentare un numero nell'intervallo $[0...n^4-1]$ in base $n$ uso $\color{green}\log_n(n^4) = 4$. 

# Tabelle Hash
___
Nell'applicazione ha bisogno:
* *Insieme dinamico* su cui sono definite le operazioni **instert**, **delete** e **search**.
* Ogni elemento ha una *chiave* estratta dall'*universo*  $U = \{0,1...w-1\}$  dove $v$ non è troppo grande.
* Nessun elemento ha la stessa chiave (*chiavi distinte*).
## Array

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
### Funzioni Hash
Deve soddisfare l'*lhashing uniforme ed indipendente* $\to$ non sempre possibile

**Esempio**:
 Le chiavi sono numeri reali $k$ casuali e distribuiti in modo *indipendente* e *uniforme* nell'intervallo $0 \leq k < 1$.
La funzione hash: $$h(k) = \lfloor m \cdot k \rfloor$$ $$h : U \to \{0, ..., m-1\}$$
soddisfa la condizione di *hashing uniforme ed indipendente*.

**Ipotesi**: le chiavi sono numeri naturali.

1) $\textbf{Metodo della divisione}$: $$h(k) = k\ mod\ n$$ $m$ è la dimensione della tabella hash. $h(k)$ è il resto della divisione fra $k$  e $m$.
  **Vantaggi**:
  * semplice realizzazione.
 **Svantaggi**: 
 * evitare come $m$ le potenze di 2. Se $m = 2P$ allora $h(k)$ rappresenta i $p$ bit meno significativi di $k$.
   **Buona scelta per m**: 
* un numero primo non troppo vicino ad una potenza di 2 o di 10.
 
  **Esempio**:
  Devo memorizare $m = 2000$ e prevedendo una media di 3 conflitti , cerco un $m$ numero primo vicino a $\frac{n}{3} \simeq 666,66 ... \to m =701$. $\color{green} n = O(m)$

2) $\textbf{Metodo della moltiplicazione}$: $$h(k) = \lfloor k \cdot m \rfloor \ \ \ \ k \in [0,1)$$
**Idea**: data una chiave numero naturale $k \in U$ la traformo in un in $[0,1)$ e poi applico la stessa funzione hash.
* fisso una costante $A$ con $0 < A < 1$
* calcolo $k \cdot A$
* estraggo la parte frazionaria: $$k \cdot A\ mod\ 1 = k \cdot A - \lfloor k \cdot A \rfloor$$ $$h(k) = \lfloor m \cdot (k \cdot A\ mod\ 1)\rfloor  )$$
**Vantaggi**
* il valore di $n$ non è critico.
* funziona bene con tutti i valori di $A$.
* Knuth ha osservato che funziona particolarmente bene con $A \simeq \frac{\sqrt{5}-1}{2} = 0,618033$

Per semplificare il calcolo della fuzione hash:

![[Pasted image 20240219111103.png]]
* Sia $w$ la lunghezza della parola di memoria. Assumiamo che $k$ entri in una singola parola di memoria. Scelgo un intero $q$, $0 < q < 2^w$ e $m = 2^p$ con $0 <  p \leq w$
* Pongo $A = \frac{q}{2^w}$
* Calcolo $K \cdot  A = \frac{k \cdot q}{2^w}$
* $k \cdot q = r_12^w + r_0 \implies \frac{k \cdot q}{2^w} = \frac{r_12^w + r_0}{2^w} =r_1 + \frac{r_0}{2^w}$
* $h(k) = \lfloor m \cdot (k \cdot A\ mod\ 1)\rfloor = \lfloor 2^p \cdot {k \cdot q}{2^w}\ mod\ 1 \rfloor = p$ bit più significativi della parola men significativa di $k \cdot q$
* $h(k) = (k \cdot q\ mod\ 2^w) >> (w - p) \to$ scorrimento logico a destra di $w-p$ inserendo degli 0 nella nelle posizioni lasciate libere, di modo che i $p$ bit più significativi di $r_0$ si sposti nelle $p$ posizioni più a destra.
### Hashing Randomizzato
Invece di avere una singola funzione hash, abbiamo un **insieme di funzioni hash** opportunamente costruito, da cui il nostro programma all'inizio della computazione scglie **casualmente** $h \in \mathcal{H}$.
### Indirizzamento Aperto
**Idea**: Tutti gli elementi sono memorizzati nella tabella hash stessa $\to$ *non c'è memoria esterna*
* ogni cella della nostra tabella contiene un elemento dell'insieme dinamico oppure `NIL`
* Per cercare un elemento di chiave $k$
	1)  Calcoliamo $h(k)$ ed **esaminiamo** ($\to$ *ispezione*) la cella $h(k)$
	2) Se la cella $h(k)$ contiene la chiave $k$, la ricerca ha $\color{red} \textbf{successo}$. Se la cella contiene `NIL`, la ricerca termina con $\color{red} \textbf{insuccesso}$
	3) Può accadere che la cella $h(k)$ contenga una chiave che $\color{red} \textbf{NON}$ è $k$. Allora calcoliamo l'indice di un'altra cella in base alla chiave $k$ e all'**ordine di ispezione**(quante ispezioni ho gia fatto.)
	4) si continua la scansione della tabella finché non si trova la chiave $k$ ($\color{red} \textbf{successo}$), oppure una cella contiene `NIL`, oppure ho eseguito $m$ ispezioni senza successo ($\color{red} \textbf{insuccesso}$).
La funzione hash diventa: $$h: U\ x\ \{0,1, ..., m-1\}\  (ordine\ di\ ispezione) \to \{0,1, ..., m-1\}$$
$h(k,i)$ rappresenta la posizione della chiave $k$ dopo $i$ ispezioni fallite.
Si richiede che per ogni chiave la **sequenza di ispezioni** <$h(k,0),h(k,1), ..., h(k,m-1)$> sia una *permutazione* di di <$0,1, ..., m-1$> in modo che ogni posizione della tabella hash possa essere considerata come possibile cella in cui inserire una nuova chiave mentre la tabella si riempie.
### Operazioni con indirizzamento aperto
**Ipotesi**: gli elementi della tabella hash sono chiavi senza dati satellite: la chiave è identica all'elemento che contiene la chiave.
#### **Insert**
```c
Hash_insert(T, k)
	i = 0
	trovato = false
	repeat
		j = h(k,i)
		if T[j] == NIL // or T[j] == DELETED
			T[j] = k
			trovato = true
		else
			i = i + 1
	until trovato or i == m
	if trovato
		return j
	else
		error "overflow della tabella Hash"
```

**Post**: inserisce l'indice della tabella dove ha memorizzato la chiave $k$ oppure segna un errore se la tabella è piena.
#### **Search**

```c
Hash_search(T,k)
	i = 0
	trovato = false
	repeat
		j = h(k,i)
		if T[j] == k
			trovato = true
		else
			i = i + 1
	until trovato or T[j] == NIL or i == m
	if trovato
		return j
	else
		return NIL
```

**Post**: restituisce j se la cella $j$ contiene $k$ oppure `NIL` se la chiave $k$ non si trova nella tabella $T$.
#### Delete

La **delete** con l'indirizzamento aperto causa delle problematiche. Supponiamo ad esempio di voler inserire l'elemento 12 nella seguente tabella hash:

![[Pasted image 20240228085628.png]]

Notiamo quindi che l'operazione di cancellazione può comportare l'*impossibilità di accedere ad alcune chiavi*.

**Soluzione**: usare un valore speciale che diciamo essere `DELETED` invece di `NIL` per marcare una  cella come vuota a causa di una cancellazione. In particolare:
* *Bisogna modificare* l'operazione di **insert** per trattare la cella con `DELETED` come se fosse vuota in modo da poter inserire una nuova chiave in quella posizione.
* *Non bisogna modificare* l'operazione di **search** perché la cella contiene un valore che non corrisponde a quello cercato.

**Svantaggio**: il tempo di ricerca non dipende più soltanto dal fattore di carico, pertanto, in presenza di un *elevato numero di cancellazioni*, è preferibile utilizzare il *metodo di concatenamento*.
### Metodi di scansione (o ispezione)

**Hashing con permutazioni indipendenti ed uniformi**: ogni chiave ha la stessa probabilità di avere come sequenza di ispezioni una delle $m!$ permutazioni di <$0,1, ..., m-1$>, ovvero:
*  $h(k,0)$ distribuisca in modo uniforme ed indipendente su $m$ celle.
* $h(k,1)$ distribuisca in modo uniforme ed indipendente su $m-1$ celle.
* $h(k,2)$distribuisca in modo uniforme ed indipendente su $m-2$ celle.
$\simeq$ ogni esecuzione distribuisce in modo uniforme ed indipendente.
#### Ispezione Lineare

Data una funzione hash ausiliaria: $h': U \to \{0,1 ... m-1\}$, il numero dell'ispezione lineare usa la funzione hash: $$h(k,i) = (h'(k)+i)\cdot mod\ m $$ 
$$per\ i = 0 ... m-1$$

![[Pasted image 20240228092421.png]]

La prima cella esaminata è $T[h^i(k)]$, poi continua a scandire tutte le celle sequenzialmente fino alla cella $m-1$ e poi riprende dalla cella $0$ fino a $h^i(k)-1$.

*Nota*: la prima ispezione determina l'intera sequenza di ispezione $\to$ ci sono soltanto $m$ sequenze di ispezioni distinte.

**Vantaggi**: facile da implementare.

**Svantaggi**: *agglomerazione primaria* $\to$ si formano lunghe file di celle occupate che aumentano il tempo di ricerca.

![[Pasted image 20240228093140.png]]

Una cella vuota preceduta da $i$ celle occupate ha probabilità $\frac{i+1}{m}$ di essere la prossima cella occupata $\to$ *le lunghe file tendono ad essere sempre più lunghe.*
#### Ispezione Quadratica

$$h(k,i) = (h'(k) + c_1, + c_2 \cdot i^2)\cdot mod\ m$$
dove:
* $h'$ è una funzione hash ausiliaria.
* $c_1$ e $c_2 \neq 0$ sono costanti.
* $i =0,1 ... m-1$.

La prima posizione determina l'intera sequenza $\to$ ci sono soltanto $m$ sequenze di ispezione distinte.

**Svantaggio**: *addensamento/agglomerazione secondario* $\to$ se due chiavi $k_1$ e $k_2$ distinte $k_1 \neq k_2$ hanno lo stesso valore hash ausiliario $h'(k_1) = h'(k_2)$ allora hanno la *stessa* sequenza di ispezioni $\to$ *forma più lieve di agglomerato*.
#### Doppio Hashing

$$h(k,i) = (h_1(k) + i \cdot h_2(k))\cdot mod\ m$$
dove:
* $h_1$ e $h_2$ sono funzioni ausiliarie.
* $i = 0 ... m-1$

**Esempio**:

![[Pasted image 20240228095810.png]]

##### Come costruire una funzione hash col doppio hashing?

Il valore $h_2(k)$ deve essere **relativamente primo** ($\to MCD = 1)$ con la dimensione $m$ della tabella hash perché venga ispezionata l'intera tabella.

Due possibili modi:
* Si può scegliere $m$ come **potenza di 2** e definire $h_2$ in modo che produca sempre un **numero dispari**: $$m = 2^p\ \ \ \ \ h(k) = 2(h'(k) + 1)$$
* Si può scegliere $m$ **primo** e definire $h_2$ in modo che generi un **numero intero positivo minore di $m$**:
	* $m$ primo 
	* $h_1(k) = k\cdot mod\ m$
	* $h_2(k) = 1+(k\cdot mod\ m')$ con $m' < m$

**Vantaggio**: Doppio hashing usa $\Theta(m^2)$ sequenze di ispezioni, perché ogni possibile coppia $(h_1(k),\ h_2(k))$ produce una sequenza di ispezione *distinta*.
### Analisi dell'hashing ad indirizzamento aperto
Analisi in termini del *fattore di carico* ($\alpha = \frac{n}{m}$). con $0 \leq \alpha \leq 1$.

**Ipotesi**:
* Si assuma hashing c0n *permutazioni indipendenti e uniformi*: ogni chiave ha la stessa probabilità di avere come sequenza di ispezione una delle $m!$ permutazioni di <$0,1 ... m-1$> indipendentemente dalle altre chiavi.
* *Nessuna cancellazione*

#### Teorema
Nell'ipotesi di hashing con *permutazioni indipendenti e uniformi* e nello stesso tempo assumendo che *non avvengano cancellazioni*, data una tabella hash ad **indirizzamento aperto** con un fattore di carico $\alpha = \frac{n}{m}< 1$, il numero atteso di ispezioni in una **ricerca senza successo** è al massimo $\frac{1}{1-\alpha}$.
#### Dimostrazione (Intuizione)
$\alpha < 1 \to$ ci sono delle celle vuote, dunque mi fermo alla prima cella vuota (con `NIL`).
* Una prima ispezione è sempre eseguita.
* Seconda ispezione $=$ probabilità che la prima ispezione abbia trovato la cella occupata ($= \alpha = \frac{n}{m}$).
* Terza ispezione $=$ probabilità che la seconda ispezione abbia trovato la cella occupata ($= \frac{n}{m} \cdot \frac{n-1}{n-1}$)
* i-esima ispezione $=$ probabilità che la precedente ispezione abbia trovato la precedente (=$\frac{n}{m} \cdot \frac{n-1}{n-1} \cdot \frac{n-2}{m-2} \cdot ...$), in cui ogni termine è maggiorato da $\alpha$.
Il numero di ispezioni atteso pertanto è: $$1 + \alpha + \alpha^2 + \alpha^3 + ... \leq \sum_{i=o}^\infty \alpha^i = \frac{1}{1-\alpha}\ \ \ \ \ |\alpha| < 1$$
#### Interpretazione 
Se $\alpha$ è costante, una ricerca senza successo viene eseguita in tempo medio costante $\Theta(1)$.
* Se $\alpha = 0.5$ (tabella piena a metà), il numero medio di ispezioni è $\frac{1}{1-\frac{1}{2}} = 2$
* Se $\alpha = 0.9$ (piena al $90\%$) il numero medio di ispezioni è $\frac{1}{1-\frac{9}{10}} = 10$
Pertanto le prestazioni **degradano rapidamente** quando si riempie la tabella.

**Corollario**: l'inserimento di un elemento in una tabella hash ad **indirizzamento aperto** con fattore di carico $\alpha$ richede in media non più di $\frac{1}{1-\alpha}$ ispezioni, nell'ipotesi di hashing con *permutazioni indipendenti ed uniformi*, e assumendo che non avvengano cancellazioni.

**Conclusione**: un elemento è inserito solo se c'è spazio nella tabella, e quindi $\alpha < 1$. L'inserimento di una chiave richiede una ricerca senza successo seguita dalla sistemazione della chiave nella prima cella vuota che abbiamo trovato. Dunque il numero atteso di ispezioni è al massimo $\frac{1}{1-\alpha}$.
#### Teorema
Data una tabella hash ad **indirizzamento aperto** con un fattore di carico $\alpha < 1$, il numero atteso di ispezioni in una **ricerca con successo** è al massimo $\frac{1}{\alpha} \cdot ln(\frac{1}{1-\alpha})$ nell'ipotesi di hashing con *permutazioni indipendenti ed uniformi*, assumendo che *non avvengano cancellazioni* e che ogni chiave nella tabella abbia la stessa probabilità di essere cercata.
#### Interpretazione
* $\alpha = 0.5 \to$ ricerca con successo è minore di 1.387
* $\alpha = 0.9 \to$ ricerca con successo è minore di 2.559

![[Pasted image 20240229110952.png]]
# Programmazione Dinamica
___
## Introduzione
La **programmazione dinamica** è una tecnica di progettazione di algoritmi.

Si applica quando:
* Un problema si riduce ad un insieme di sotto-problemi più piccoli
* Diversamente dal *divide et impera*, i sotto-problemi sono **sovrapposti**. $\to$ molti problemi si ripetono, così un approccio *divide et impera* risolve tante volte lo stesso problema, quindi sarebbe **inefficiente**

**Idea**: risolvere ogni sotto-problema una sola volta memorizza la soluzione $\to$ utilizzo la soluzione quando incontro di nuovo lo stesso sotto-problema.

In genere è adatta a **problemi di ottimizzazione**:
* molte possibili soluzioni
* ogni soluzione ha un costo
* voglio **una** soluzione **ottima** (di costo minimo o massimo)

Per sviluppare un algoritmo di **programmazione dinamica**:
* caratterizzazione della struttura di una soluzione ottima
* definizione ricorsiva del *valore* di una soluzione ottima
* calcolo del valore di una soluzione ottima:
    * approccio **top-down**
    * approccio **bottom-up**
* individuazione di una soluzione ottima sulla base delle informazioni calcolate al passo precedente
## Taglio delle Aste
Un'azienda produce aste d'acciaio e le vende a pezzi.
* le aste prodotte hanno lunghezza $n$
* sul mercato i pezzi hanno un prezzo che dipende dalla lunghezza
* Il costo del taglio è irrilevante
$\to$ Dobbiamo trovare il modo di tagliare le aste che massimizzi il guadagno.
**Input**:
* asta di lunghezza $n$
* tabella di prezzi $p_i,\ i=1 ... n$
**Output**:
* determinare $r_n$, ovvero il ricavo massimo per un'asta di lunghezza $n$ che si può ottenere tagliando l'asta e vendendo i pezzi.

**Esempio**:

![[Pasted image 20240229114650.png]]

**In quanti modi posso tagliare un'asta di lunghezza n?**

![[Pasted image 20240229114904.png]]

Sapendo che i pezzi sono interi $> 0$, in ogni posizione $1,2 ... n-1$ posso decidere se tagliare o meno $\to 2 \cdot 2 \cdot 2 ... \cdot 2\ (n-1\ volte) = 2^{n-1}$.

Pertanto analizzare esplicitamente tutti i possibili modi di tagliare è **inefficiente** $\to \Theta(2^n).$

Il ricavo massimo $r_n$ per un asta di lunghezza $n$ è definibile in maniera **ricorsiva**:
*  $r_o = 0$
* $r_n = max\{p_n,\ r_1 + r_{n-1},\ r_2 + r_{n-2},\ ...\}$ quindi taglio in qualche posizione $i = 1 ... n-1$ e massimizzo il ricavo per i pezzi ottenuti.

Quando, come in questo caso, la soluzione è esprimibile come combinazione di soluzioni ottime di sotto-problemi, si dice che vale **la proprietà della sotto-struttura ottima**.
### Caratterizzazione più semplice
* Tagliare un pezzo in modo definitivo
* suddividere ulteriormente la parte che resta in modo ottimale

**Formulazione ricorsiva**:
* $r_0 = 0$
* $r_n = max_{1 \leq i \leq n}\{p_i + r_{n-i}\}$

![[Pasted image 20240304104346.png]]

### Algoritmo per il taglio dell'asta

**Input**:
* `p[1...m]` con $m \geq n$: vettore di prezzi, in `p[i]` è contenuto il prezzo di un'asta di lunghezza $i$ con $i \geq 0$.
* `n`: lunghezza dell'asta da tagliare. 

**Output**:
	ricavo massimo $r_n$

```c
Cut_rod(p,n)
	if n == 0
		return 0
	else
		q = -1  // -inf se i prezzi fossero annche negativi
	for i = 1 to n
		q = max(q, p[i] + Cut_rod(p, n-i))
	return q
```

$T(n)$ è il numero di chiamate ricorsive di `Cut_rod` quando la chiamata viene fatta con il secondo parametro uguale ad $n$

$$\left\{ \begin{array}{}  1 \ \ \ \ per\ n = 0 \\ 1 + \sum_{i = 1}^{n}T(n - i)\ \ \ \ \ per\ n > 0 \end{array} \right.$$
$$T(n) = 1 + \sum_{i = 1}^{n}T(n - i) = 1 + \sum_{j = 0}^{n-1}T(j)\ con\ j = n-i$$
### Dimostrazione
* $(n == 0) \to T(0) = 1 = 2^0$ per definizione
* $(n > 0)$ Assumiamo vero che per $n$ valga $T(n) = 2^n$ e lo dimostro per $n + 1$: $$T(n +1) = 1 + \sum_{j = 0}^{(n+1)-1}T(j) = 1 + \sum_{j = 0}^{n - 1 }T(j) + T(n) = T(n) + T(n) = 2T(n)$$ quindi $$T(n + 1) = 2 T(n) = 2 \cdot 2^n = 2^{n+1}$$ La complessità di `Cut_rod` è quindi esponenziale: $T(n) = O(2^n)$.
### Albero di ricorsione

![[Pasted image 20240304110204.png]]

### Osservazioni
* Lo stesso sotto-problema viene risolto più volte
* I sotto-problemi distinti sono pochi.

$\to$ se noi memorizziamo la soluzione dei sotto-problemi una volta calcolata, la possiamo riutilizzare se incontriamo lo stesso sotto-problema.

**Se**:
* I sotto-problemi distinti sono un numero **polinomiale**
* Ciascuno si risolve in tempo **polinomiale** (data la soluzione dei sotto-problemi), memorizzando le soluzioni ed evitando di ricalcolarle si ottiene un algoritmo polinomiale.

**2 possibilità**:
* *top-down* : salva in una tabella(vettore, hash) le soluzioni dei problemi già risolti $\to$ **memoization** 
* *bottom-up* : ordina i sotto-problemi in base alla dimensione, iniziando dai sotto-problemi più piccoli, e memorizza le soluzioni ottenute.
### Algoritmo top-down

```c
Memoized_cut_rod
	Sia r[0...n] un nuovo vettore
	for i = 0 to n
		r[i] = -1       //r[i] ricavo ottimo per lunghezza i
	return Memoized_cut_rod_aux(p,n,r)

Memoized_cut_rod_aux(p,j,n)
	if r[j] < 0
		if j == 0       //si può eliminare settando prima
			r[j] = 0    //r[0] = 0 nella funzione principale
		else
			q = -1
			for i = 1 to j
				q = max(q, p[i] + Memoized_cut_rod_aux(p,j-i,
													   r))
			r[j] = q
	return r[j] 
```

**Costo**:
Una chiamata ricorsiva per risolvere un problema precedentemente risolto termina immediatamente. Dunque si giunge al ramo `else` **una sola volta** per ciascun sotto-problema $j = 1,2, ..., n$.
Per risolvere un sotto-problema di dimensioni $j$, il ciclo `for` effettua $j$ iterazioni del ciclo `for` per tutte le chiamate ricorsive di `Memoized_cut_rod` è: $$\sum_{j = i}^{n} j = \frac{n(n + 1)}{2} = \Theta(n^2)$$Il tempo di esecuzione di `Memoized_cut_rod` è: $$T(n) = \Theta(n) + \Theta(n^2) = \Theta(n^2) $$
### Algoritmo bottom-up

```c
Bottom_up_cut_rod(p,n)
	Sia r[0...n] un vettore
	r[0] = 0
	for j = 1 to n
		q = -1
		for i = 1 to j
			q = max(q, p[i] + r[j-i])
		r[j] = q
	return r[n]
```

**Costo**: $$\sum_{j = 1}^{n}\Theta(1) \cdot j = \Theta(1) \cdot \frac{(n \cdot (n + 1))}{2} = \Theta(n^2)$$
### Trovare la soluzione ottima

* `r[0...n]` con `r[j]` ricavo ottenuto per il problema di dimensione $j$.
* `s[1...n]` con `s[j]` posizione del primo taglio che determina la soluzione ottima.

```c
Ext_bottom_up_cut_rod(p,n)
	r[0...n]
	s[1...n]
	r[0] = 0
	for j = 1 to n
		q = -1
		for i = 1 to j
			if q < p[i] + r[j - i]
			q = p[i] + r[j-i]
			s[j] = i
		r[j] = q
	return r,s

Print_cut_rod_solution(p, n)
	r,s = Ext_bottom_up_cut_rod(p,n)
	while n > 0
		print s[n]
		n = n - s[n]
```

**Costo**:
`Ext_bottom_up_cut_rod` costa $\Theta(n^2)$ mentre il ciclo `while` costa $O(n)$, quindi il costo totale è $$\Theta(n^2) + O(n) = O(n^2).$$
![[Pasted image 20240306085649.png]]

## Longest Common Subsequence (LCS)

*Cominciamo con un esempio tratto dalla bio-informatica*:

* Adenina
* Guanina
* Citosina
* Timina

Un filamento di DNA si può rappresentare come una stringa sull'alfabeto $\{A,G,C,T\}$.

**Edit distance**: il minimo numero di operazioni da fare ad una stringa per renderla uguale all'altra stringa.
*Esempio*
 *  $s_1 = A,C,T,A,C,C,T,G$
* $s_2 = A,T,C,A,C,C$
* Posso **inserire**, **cancellare**, **copiare** e nuovamente **copiare** un carattere. L'**edit distance** in questo caso è pertanto data da **4 operazioni**.

### LCS

![[Pasted image 20240306090837.png]]

* Indichiamo una **sequenza** con: $X = x_1 ... x_n$
* Una **sottosequenza** di $X = x_1 ... x_n$ è $x_{i1} ... x_{ik}$ tale che $i_1 ... i_k \in \{1 ... m\}$ con $i_1 < i_2 < ... < i_k$   una *successione strettamente crescente* <$i_1 ... i_k$> di indici di $X$.
### Problema LCS
Date due sequenze:
* $X = x_1 ... x_m$
* $Y = y_1 ... y_n$

Trovare una sequenza $W$ che sia:
* sottosequenza di $X$ e $Y$
* di lunghezza massima

*Osservazione 1*:
Non vi è un'unica LCS di due sequenze $X$ e $Y$
*Esempio*: $A,C$ e $C,A$ $\to$ $A \cdot C \in LCS$

Indichiamo con $LCS(X,Y)$ l'**insieme** delle $LCS$ di $X$ e $Y$.

*Osservazione 2*:
Un algoritmo di **brute-force**:
*  genera  tutte le sottosequenze di $X$
*  verifico se è sottosequeza di $Y$
*  tiene la più lunga

Le sottosequenze di $X = x_1 ... x_m$ sono $2^n$ perché possiamo scegliere se prendere ogni carattere o meno.

L'algoritmo di brute-force costa $O(2^n) \to$ **inefficiente**
### Risoluzione del Problema 
#### PASSO 1. Caratterizzazione della Struttura della Soluzione Ottima

**Prefissi**: Data $X = x_1 ... x_m$ per $k \leq m$ indichiamo con $X^k$ il prefisso di lunghezza $k$ di $X$ $$X^k = x_1 ... x_k$$
*Esempio*:
![[Pasted image 20240306092634.png]]

In generale $X = x_1 ... x_m$ ha $m+1$ prefissi, quindi se si riduce il problema LCS di $X$ e $Y$ al problema sui prefissi $\to O(m \cdot n)$ sotto-problemi.
* $X = x_1 ... x_m$
* $Y = y_1 ... y_n$ 

#### Teorema (Sottostruttura Ottima per LCS)
Siano:
* $X = x_1 ... x_m$
* $Y = y_1 ... y_n$ e 
* $W = w_1 ... w_k \in LCS(X,Y)$

Allora:
1) se $x_m = y_n$ allora $w_k = x_m = y_n$ e $W^{k-1} \in LCS(X^{m-1},Y^{n-1})$
2) se $x_m \neq y_n$:
	1) se $w_k \neq x_m$ allora $W^{k-1} \in LCS(X^{m-1},Y)$
	2) se $w_k \neq y_n$ allora $W^{k-1} \in LCS(X,Y^{n-1})$

#### Dimostrazione
1) se, per assurdo, $w_k \neq x_m$ allora potrei costruire una sequenza $W_{xm}$ che risulterebbe essere comune a $X$ e a $Y$ e sarebbe di lunghezza $k + 1$. $\to$ **ASSURDO** perché $W$ non sarebbe più $LCS(X,Y)$ in quanto sappiamo che $|W| = k$. Quindi deve essere che $w_k = x_m = y_m$.
   
   $W^{k-1}$ è una sottosequenza comune di $X^{m-1}$ e $Y^{n-1}$. Supponiamo per assurdo che ci sia una sottosequenza $W' \in LCS(X^{m-1},Y^{n-1})$ e $|W'| > |W^{k-1}| = k-1$. Possiamo concatenare a $W'$ il carattere $x_m = y_m \to W'x_m$ sottosequenza comune di $X$ e $Y$ e $|W'x_m| > k + 1 - k > k$ cioè $|W'x_m| > k \to$ **ASSURDO** perché $k$ è la lunghezza massima dell'$LCS(X,Y)$.

2) se $x_m \neq y_n$
	1)  se $w_k \neq x_m$ allora $W$ è una sottosequenza comune a $X^{m-1}$ e $Y$. Vorremmo dimostrare che $W \in LCS(X^{m-1},Y)$. Se ci fosse una sottosequenza comune $W'$ di $X^{m-1}$ e $Y$ più lunga di $W\ (|W'| > k)$ sarebbe anche sottosequennza di $X$ e $Y$ $\to$ **ASSURDO** perchè contraddico l'ipotesi che $W \in LCS(X,Y)$ perchè $|W'| > |W|$.
	2) Analogo.

#### PASSO 2. Soluzione ricorsiva per il valore della soluzione ottima
Date:
* $X = x_1 ... x_m$
* $Y = y_1 ... y_m$

Indichiamo con $c[i,j] =$ lunghezza $LCS(X^i,Y^j)$ con:
* $0 \leq i \leq m$
* $0 \leq j \leq n$

![[Pasted image 20240306101557.png]]
![[Pasted image 20240311104929.png]]
#### PASSO 3. Algoritmo bottom-up
**Manteniamo**:
* `c[i,j]` = lunghezza della $LCS(x^i,y^j)$.
* `b[i,j]` = informazioni utili recuperare la soluzione
  * $\nwarrow$ se $x_i = y_j \to LCS(x^i,y^j)$ ridotto a $LCS(x^{i-1},y^{j-1})$
  * $\leftarrow$ se $x_i \neq y_j \to LCS(x^i,y^j)$ ridotto a $LCS(x^{i},y^{j-1})$
  * $\uparrow$ $x_i \neq y_j \to LCS(x^i,y^j)$ ridotto a $LCS(x^{i-1},y^{j})$

```c
LCS(X, Y)
	
	m = X.length
	n = y.length
	
	//due array
	b[1...m, 1...n]
	c[0...m,0...n]
	
	for i = 0 to m
		c[i,0] = 0
	
	for j = 0 to n
		c[0,j] = 0
	
	for i = 1 to m
		for j = 1 to n
			if x[i] == y[j]
				c[i,j] = 1 + c[i-1, j-1]
				b[i,j] = ↖
			else
				if c[i-1,j] >= c[i,j-1]
					c[i,j] = c[i-1, j]
					b[i,j] = ↑
			else
				c[i,j] = c[i,j-1]
				b[i,j] = ←
```

![[Pasted image 20240311111308.png]]

#### Complessità dell'algoritmo
Il primo ciclo ha costo $\Theta(m)$, il secondo $\Theta(n)$ mentre il terzo $\Theta(m \cdot n)$ quindi l'algoritmo ha costo polinomiale $\Theta(n \cdot m)$.

#### PASSO 4. Come si costruisce una soluzione con algoritmo bottom-up

```c
printLCS(X,Y)
	
	b,c = LCS(X,Y)
	printLCSaux(X,b,X.length,Y.length)

printLCSaux(X,b,i,j)
	if i > 0 and j < 0
	if b[i,j] == ↖
		printLCSaux(X,b,i-1,j-1)
		print x[i]
	else if b[i,j] == ↑
		printLCSaux(X,b,i-1,j)
	else
		printLCSaux(X,b,i,j-1)
```

![[Pasted image 20240311112802.png]]
#### Complessità dell'algoritmo 
Il tempo di esecuzione di `printLCSaux` è $O(i+j)$ perché ad ogni chiamata decremento almeno uno fra $i$ e $j$.

Per quanto riguarda `printLCS`, la chiamata a `LCS` ha costo $\Theta(m \cdot n)$ mentre la chiamata a `printLCSaux` ha costo $O(m + n)$, pertanto il costo totale di `printLCS` è $\Theta(m \cdot n)$.
#### Ottimizzazioni
Il codice può essere ottimizzato *rispetto all'uso della memoria*, poiché per determinare `c[i,j]` usiamo:
* `c[i-1,j-1]`
* `c[i-1,j]`
* `c[i,j-1]`

Confrontando questi valori posso capire come è stato ottenuto l'**ottimo**.
#### printLCSaux Ottimizzata

```c
printLCSaux(X,c)
	if i > 0 and j > 0
		if c[i,j] == c[i-1,j]
			printLCSaux(X,c,i-1,j)
		else if c[i,j] == c[i,j-1]
			printLCSaux(X,c,i,j-1)
		else
			printLCSaux(X,c,i-1,j-1)
			print X[i]
```

**Ossercazione 1**:
>Non cambia il costo asintotico di memoria, che è sempre dato da $\Theta(m \cdot n)$ poiché devo sempre memorizzare `c`.

**Osservazione 2**
>Se sono interessato solo alla $\textbf{lunghezza}$ della LCS, posso evitare di mantenere tutta la tabella `c[i,j]` dato che posso che posso calcolare la riga `i+1` utilizzando solo la riga `i`.
>
>$\textbf{Da dimostrare}$: si può in utilizzare $min(m,n)$ posizioni, più uno spazio $O(1)$ aggiuntivo.
#### PASSO 3. Algoritmo top - down

```c
tdLCS(X,Y)
	
	m = x.length
	n = y.length
	
	c[0...m, 0...n] // nuovo vettore
	//inizializzo tutto a -1
	c[0...m, 0...n] = -1 // Θ(m * n)
	
	return tdLCSaux(X,Y,c,m,n)
```

#### PASSO 4. Come si costruisce una soluzione con algoritmo top-down

```c
tdprintLCSaux(X,b,i,j)
	if c[i,j] == -1
		if i == 0 or j == 0
			c[i,j] = 0
		else if x[i] == y[j]
			c[i,j] = 1 + tdLCSaux(X,Y,c,i-1,j-1)
		else
			c[i,j] = max(tdLCSaux(X,Y,c,i-1,j),
						 tdLCSaux(X,Y,c,i,j-1))
	return c[i,j]
```