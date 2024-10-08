___
# Introduzione
Durante il corso ci troveremo ad analizzare diversi tipi di problema, e per farlo avremo bisogno di diversi **modelli computazionali**, ovvero elementi che, dato un *input*, ci offriranno un *output*.
I primi modelli saranno semplici ed in grado di risolvere pochi problemi. I modelli saranno via via più complessi, fino ad arrivare al modello più sofisticato, la **Macchina di Turing**. Esistono tuttavia problemi che nemmeno tale modello (che corrisponde al *calcolatore*) può calcolare.
# Automi a Stati Finiti (DFA)
>Un **DFA** è un modello computazionale con una quantità finita di memoria, limitata in particolare dal numero di stati dell'automa.
## Primo esempio incompleto
![[Pasted image 20240917142713.png]]

L'esempio qui presente non è ancora un **DFA** a tutti gli effetti, tuttavia ha alcune caratteristiche fondamentali di questi ultimi:
* *Stati*
* *Input*
* *Transizioni* fra gli stati sulla base degli input
## Esempio di DFA
![[Pasted image 20240917143730.png]]

Vi sono due principali differenze rispetto all'esempio precedente:
* La **freccia rossa** indica che $q_1$ è lo stato di partenza dell'automa.
* Il **doppio cerchio verde** indica che $q_2$ è uno *stato accettante*(o *finale*), ciò significa che la computazione deve finire in tale stato. Per esempio la stringa $t = 0,1,0$ non può essere accettata perché finirebbe in stato $q_3$.
## Di nuovo su DFA
> Un DFA è un riconoscitore di stringhe. Le stringhe da esso accettate rappresentano il suo **linguaggio**.
## Definizione formale di DFA
Un DFA $D$ è una quintupla ($Q,\Sigma, \delta, q_0, F$) dove:
* $Q$ è un insieme di *finito* stati.
* $\Sigma$ è un insieme *finito* di input (alfabeto).
* $\delta: Q \times \Sigma \to Q$ è la *funzione di transazione*.
* $q_0 \in Q$ viene detto *stato iniziale* $\implies$ deve essercene uno e solo uno.
* $F \subseteq Q$ è l'insieme degli *stati accettanti* $\implies$ può essere unico, nullo o possono essere molti.
## Esempio
![[Pasted image 20240917145137.png]]

Scriviamolo come una quintupla $D = (Q, \Sigma, \delta, q_0, F)$:
* $Q = \{q_1,q_2,q_3\}$
* $\Sigma = \{0,1\}$
* $q_0 = q_1$
* $F = \{q_2\}$
* $\delta(q_0,0) = q_1, \delta(q_1,1) = q_2, \delta(q_2,0) = q_3, \delta(q_2,1) = q_2, \delta(q_3,0) = \delta(q_3,1) = q_2$
## Di nuovo su DFA
>In generale, dati $m$ stati iniziali e $n$ input, il numero totale di transazioni sarà $m \times n$, pertanto ogni stato dovrà avere un output per ogni specifico input.

Per esempio, il seguente *non* è un DFA:
![[Pasted image 20240917150031.png]]
## Qual è il linguaggio di un DFA?
![[Pasted image 20240917150817.png]]

Il *linguaggio* di questo automa è:
>$L(D) =$ Insieme delle stringhe con almeno un $1$, dopo l'ultimo $1$ la stringa deve terminare con un numero pari di $0$. 

Per *verificare la correttezza* del nostro assunto possiamo cominciare dalle **proprietà** di ogni stato:
* $q_1$: le stringhe che terminano in $q_1$ sono composte da soli $0$ (oltre alla stringa vuota). 
* $q_1$: le stringhe che terminano in $q_2$ contengono  almeno un $1$ e hanno un numero pari di $0$ dopo l'ultimo $1$.
* $q_3$: le stringhe che terminano in $q_3$ contengono almeno un $1$ e hanno un numero dispari di $0$ dopo il primo $1$.

Dopo aver determinato le **proprietà** dei vari stati, si può procedere ad una *dimostrazione per induzione* del nostro assunto.
## Esempi di DFA
![[Pasted image 20240918140500.png]]

$L(D) = \{w \in \{0,1\}^* | \text{ ultimo carattere letto è 1}   \}$

![[Pasted image 20240918140812.png]]

$L(E) = \{w \in \{0,1\}^* | \text{ ultimo carattere letto è 0 oppure } w = \epsilon   \}$

![[Pasted image 20240918141708.png]]
## Definizione di Stringa Accettata da un DFA
Sia $M = \{Q,\Sigma,\delta,q_0,F\}$ e sia $w = w_1,w_2, ... , w_n$ una stringa tale che $\forall i \in [1,n]: w_i \in \Sigma$ diciamo che $M$ **accetta** $w$ $\iff$ esistono degli stati $r_0,r_1, ... , r_n \in Q$ tale che: 
* $r_0 = q_0$
* $r_n \in F$
* $\forall i \in [0,n-1]: \delta(r_1, w_{i+1}) = r_{i + 1}$
## Esempio
![[Pasted image 20240918142946.png]]

Dimostriamo che accetta $101$:
* **Sequenza di stati**: $q_0, q_1, q_0,  q_1$

## Definizione di Linguaggio di un DFA
Sia $M$ un DFA. Il **linguaggio riconosciuto** da $M$, indicato con $L(M)$, è l'insieme delle stringhe che $M$ accetta.
## Definizione di Linguaggio Regolare
Un linguaggio $A$ si dice **regolare** $\iff$ esiste un DFA $M$ tale che $L(M) = A$.
## Esempi di Linguaggio Regolare
* Dimostrare che l'insieme delle stringhe binarie che contengono un numero dispari di $1$ è regolare.
![[Pasted image 20240918145450.png]]

* Dimostrare che l'insieme delle stringhe binarie che contengono la sottostringa $001$ è regolare:
![[Pasted image 20240918145506.png]]
## Operazioni Regolari
Siano $A$ e $B$ due **linguaggi qualsiasi**(non necessariamente **regolari**), definiamo le seguenti $3$ **operazioni regolari**:
* **Unione**: $a \cup B = \{w\ |\ w \in A \lor w \in B\}$.
* **Concatenazione**:  $A_° B = \{w_1w_2\ |\ w_1 \in A \land w_2 \in B\}$.
* **Star**: $A^* = \{w_1,w_2, ..., w_n\ |\ \forall i \in [1,k]: w_i \in A \land K \geq 0\}$.
## Esempi
* $A = \{a,b\}$.
* $B = \{a, cc\}$.
* $A \cup B = \{a, b, cc\}$.
* $A_° B = \{aa, acc, ba, bcc\}$.
* $B* = \{\epsilon, a, cc, aa, acc, cca, cccc, ...\}$ (è un insieme **infinito**, possiamo prendere quante stringhe vogliamo e concatenarle, inoltre $\epsilon$ sta sempre nell'insieme **star**).
## Teorema
La **classe dei linguaggi regolari** è **chiusa** rispetto alle **operazioni regolari**, cioè, se $A$ e $B$ sono regolari, allora $A \cup B$, $A_° B$ e $A*$ sono tutti **regolari**.
## Dimostrazione
Dimostriamo che se $A$ e $B$ sono regolari, allora $A \cup B$ è regolari:

Siano $A$ e $B$ regolari, allora esistono due DFA $M_1 = \{Q_1, \Sigma_1, \delta_1, q_1, F_1\}$ e $M_2 = \{Q_2, \Sigma_2, \delta_2, q_2, F_2\}$ tali che $L(M_1) = A$ e $L(M_2) = B$.
Costruisco un nuovo DFA $M = ...$ tale che $L(M) = A \cup B$.
**Idea**: $M$ simula $M_1$ e $M_2$ "in parallelo" .
Sia dunque $M = \{Q, \Sigma, \delta, q_0, F\}$ il DFA definito come segue:
* Assumiamo che $\Sigma_1 = \Sigma_2 = \Sigma$.
* $Q = Q_1 \times Q_2 = \{(q_1,q_2)\ |\ q_1 \in Q_1 \land q_2 \in Q_2\}$
* $q_0 = (q_1,q_2)$.
* $F = \{(r_1r_2) \in Q\ |\ r_1\in F_1 \lor r_2 \in F_2\}$
* $\delta((r_1r_2), a) = (\delta_1(r_1,a), \delta_2(r_2,a))$
## Esempio
Consideriamo il seguente DFA:
![[Pasted image 20240924140820.png]]
Il suo alfabeto è $\Sigma = \{a,b\}$

A questo punto possiamo aggiungere uno stato c, che fungerà da **stato pozzo** (stato da cui non si può uscire), ottenendo ancora un **linguaggio regolare**:

![[Pasted image 20240924141059.png]]
Con alfabeto $\Sigma = \{a,b,c\}$
# Automi a Stati Finiti Non-Deterministici (NFA)
![[Pasted image 20240925140734.png]]Differenze rispetto ai **DFA**:
* Lo stato $q_1$ ha due archi etichettati con $1$.
* Lo stato $q_2$ non ha archi etichettati con $1$.
* Include delle $\epsilon-transazioni$, che non prendono caratteri in input.
* Esempi di input accettati sono $\{1,0,1\}$, $\{1,1\}$ $\implies$ basta che uno dei cammini porti allo stato accettante, motivo per cui l'automa viene detto **non-deterministico**.
* Un esempio di input non accettato è $\{0\}$.
Possiamo pensare a questa computazione come se fosse **thread-base**, cioè come se spawnasse un nuovo thread ogni volta che l'automa deve fare una scelta, andando così a generare un **albero della computazione**.
![[Pasted image 20240924143350.png]]

>In generale, **ogni NFA può essere trasformato in un DFA corrispondente**.
## Esempi di NFA
Scriviamo un **NFA** per il linguaggio delle **stringhe binarie** contenenti un $1$ nella terza posizione dalla fine (per esempio $\{00110\}$)
![[Pasted image 20240924145555.png]]

Trasformiamolo in un DFA:
* **IDEA**: memorizziamo gli ultimi 3 bit letti:
![[Pasted image 20240924150651.png]]

Che linguaggio riconosce il seguente NFA:
![[Pasted image 20240924151400.png]]
$L(D) =$ Strighe composte da soli $0$ di lunghezza pari a multipli di $3$.
## Definizione di NFA
Un NFA è una quintupla $(Q,\Sigma, \delta, q_0, F)$ dove:
* $Q$ è un insieme finito di stati.
* $\Sigma$ è un alfabeto finito
* $\delta : Q \times (\Sigma \cup \{\epsilon\})$ $\to$ $\mathbb{P}(Q)$ (**powerset** di Q, per esempio $A = \{a,b\}, \quad \mathbb{P}(Q) = \{\emptyset\}, \{a\}, \{b\}, \{a,b\}$).
* $q_0 \in Q$ è lo stato iniziale
* $F \in Q$ è l'insieme degli stati accentanti.
## Definizione di Stringa Accettata da un NFA
Sia $N = (Q, \Sigma, \delta, q_0, F)$ un NFA e sia $w$ una stringa costruita su $\Sigma$. Diciamo che $N$ accetta $w$ $\iff$ $w = y_1, y_2, ..., y_n$ dove $\forall i : y_i \in \Sigma \cup \{\epsilon\}$ ed esiste una sequenza di stati $r_0,r_1, ..., r_n \in Q$ tale che:
* $r_0 = q_0$
* $r_n \in F$
* $\forall i \in [0, n-1] : r_{i + 1} \in \delta(r_i, y_{i + 1})$
## Ancora su NFA
![[Pasted image 20240925140734.png]]
* $Q = \{q_1,q_2,q_3,q_4\}$
* $\Sigma = \{0,1\}$
* $q_0 = q_1$
* $F = \{q_4\}$
* $\delta(q_1, 0) = \{q_1\}$ $\delta(q_1,1) = \{q_1,q_2\}$ $\delta(q_1, \epsilon) = \emptyset$ $\delta(q_2, 0) = \{q_3\}$ ...
Per specificare quando vogliamo prendere la direzione etichettata con $\epsilon$ dobbiamo scriverlo esplicitamente nella stringa ($11 \to 1 \epsilon 1$)
## Teorema
Per ogni **NFA** $N$ esiste un **DFA** $D$ tale che $L(D) = L(N)$.
## Dimostrazione
![[Pasted image 20240925141428.png]]
**Idea**: non sapendo quale ramo farà terminare la computazione, ad ogni esecuzione mi salvo lo stato corrente.
![[Pasted image 20240925141638.png]]
In questo modo abbiamo *linearizzato l'albero*.

Sia dunque $N = (Q, \Sigma, \delta, q_0, F)$ e costruisco un DFA $D=\{Q',\Sigma,\delta',q_0',F'\}$.
**IPOTESI**: Assumiamo per il momento che $N$ non contenga $\epsilon-transazioni$.

A questo punto avremo:
* $Q'= \mathbb{P}(Q)$.
* $q_0' = \{q_0\}$ $\to$ è un insieme perché stiamo prendendo un elemento di $Q$.
* $F' = \{R \in Q' | \exists r \in R : r \in F\}$
* $\delta'(R,a) = \bigcup_{r \in R} \delta(r,a)$.

Nel caso in cui $N$ contenesse $\epsilon-transizioni$ possiamo pensare di introdurre la funzione $E(R)$:
* $E(R) = \{q | q \text{ può essere raggiunto da qualsiasi } r \in R \text{ con 0 o più }\epsilon-transizioni\}$
A questo punto avremo:
* $Q'= \mathbb{P}(Q)$.
* $q_0' = E(\{q_0\})$.
* $F' = \{R \in Q' | \exists r \in R : r \in F\}$
* $\delta'(R,a) = \bigcup_{r \in R} E(\delta(r,a))$.
## Esempio di conversione da NFA a DFA
![[Pasted image 20240925145002.png]]
*Note*:
![[Pasted image 20240925145002.png]]
## Proprietà di conversione fra NFA e DFA
* Ogni **NFA** è convertibile in un **DFA** *equivalente*.
* Ogni **DFA** è convertibile in un **NFA** *equivalente*.
## Corollario
Un linguaggio $A$ è regolare $\iff$ esiste un **NFA** che lo riconosce.
## Dimostrazione:
* $\implies$ sia $A$ regolare, per definizione esiste un DFA $D$, tale che $L(D) = A$. Converto $D$ in un NFA equivalente.
* $\impliedby$ Assumo che esista un NFA $N$, tale che $L(N) = A$. Converto $N$ in un DFA equivalente e dimostro la regolarità. 
## Dimostrazione di regolarità di $A_° B$
Se $A$ e $B$ sono **regolari**, allora $A_° B$ è **regolare**.
![[Pasted image 20240925150908.png]]

Siano $A$ e $B$ regolari, allora esistono $N_1$ e $N_2$ tali che $L(N_1) = A$ e $L(N_2) = B$. Costruisco un nuovo NFA $N$ tale che $L(N) = A_° B$
![[Pasted image 20240925151624.png]]
Ciò che abbiamo è:
* $N_1 = (Q_1, \Sigma, \delta_1, q_1, F_1)$.
* $N_2 = (Q_2, \Sigma, \delta_2, q_2, F_2)$.
* $N = (Q, \Sigma, \delta, q_0, F)$.
In particolare $N$ sarà così costruito:
* $Q = q_1 \cup q_2$.
* $q_0 = q_1$.
* $F = F_2$.
* $\delta(q,a) = \delta_1(q,a) \to \text{se } q \in Q_1 \\ F_1,\ \delta_2(q,a) \to \text{se } q \in Q_2,\ \delta_1(q,a) \to \text{se } q \in F_1 \land a \neq \epsilon,\ \{q_2\} \cup \delta_1(q,a) \text{se } q \in F_1 \land a = \epsilon$
## Dimostrazione regolarità di $A^*$
Se $A$ è *regolare*, allora $A^*$ è *regolare*.
$A^* = \{w_1, ..., w_k | \forall i : w_i \in A \land k \geq 0\}$.

Sia $A$ regolare, allora esiste un NFA $N$ tale che $L(N) = A$. Costruisco un NFA $M$ tale che $LD(M) = A^*$.
![[Pasted image 20240925153153.png]]
# Espressioni Regolari
 Le **espressioni regolari** (o **regexp**) sono un formalismo utilizzato per descrivere i linguaggi regolari.
## Esempio 1
$$(0 \cup 1)_° 0^*$$
Si tratta di una scrittura simile a quella delle operazioni aritmetiche, per esempio: $$(3 + 5) \times 7$$
Nel nostro caso l'espressione regolare ci dice:
* $(0 \cup 1) \to$ scegli fra $0$ e $1$.
* $_° \to$ concatenaci.
* $0^* \to$ quanti $0$ vogliamo (anche nessun0). 

Per esempio stringhe che rispettano il linguaggio identificato da tale **regexp** sono:
* $0, \quad 1, \quad 00, \quad 100...$
Al contrario, stringhe non accettate sono:
* $01, \quad 101...$
## Esempio 2
$$(0 \cup 1)*$$
In questo caso la **regexp** ci indica:
* Una generica stringa binaria, anche vuota
## Regexp rispetto agli alfabeti 
Talvolta, nelle **regexp**, un **alfabeto** viene anche indicata con $\Sigma^*$, per esempio: $$\Sigma^* = (a \cup b)^*$$
Sia $\Sigma$ un alfabeto. L'insieme delle **regexp** definite su $\Sigma$ è definito come segue:
* Se $a \in \Sigma$, allora $a$ è una regexp.
* $\epsilon$ è una regexp.
* $\emptyset$ è una regexp.
* Se $R_1$ e $R_2$ sono regexp, allora $R_1 \cup R_2$ è una regexp.
* Se $R_1$ e $R_2$ sono regexp, allora $R{_1°} R_2$ è una regexp.
* Se $R$ è una regexp, allora $R^*$ è una regexp.
## Convenzioni
* L'operatore $_°$ generalmente viene **eliso** $\to$ $R_{1°} R_2 = R_1R_2$.
* **Precedenza degli operatori** $\to$ prima $^*$, poi $_°$ e infine $\cup$.
## Linguaggio Definito da una Regexp
Sia $R$ una **regexp**, definiamo il suo linguaggio $L(R)$ come segue:
* Se $R=a$ per qualche $a$, allora $L(R) = \{a\}$.
* Se $R=\epsilon$, allora $L(R) = \{\epsilon\}$.
* Se $R = \emptyset$, allora $L(R) = \emptyset$.
* Se $R = R_1 \cup R_2$, allora $L(R) = L(R_1) \cup L(R_2)$ $\to$ Si noti che il simbolo $\cup$ assume significati diversi, nel primo caso fa parte della sintassi delle **regexp**, nel secondo è l'**unione insiemistica**.
* Se $R = R_{1°} R_2$, allora $L(R) = L(R_1)_° L(R_2)$
* Se $R = R_1^*$, allora $L(R) = (L(R_1))^*$
## Esempi
Applichiamo la funzione $L()$ alla seguente **regexp**: $$(0\cup1)_°0^*$$
$$L((0\cup1)_°0^*) = L(0 \cup 1)_° L(0^*) = L(0) \cup L(1)_° L(0^*) = \{0\} \cup \{1\} _° L(0^*) = \{0,1\} _° L(0^*) = \{0,1\} _° (L(0))^* = \{0,1\} _° (\{0\})^*$$

$L(0^*10^*) =$ Linguaggio delle stringhe binarie con esattamente un $1$.
$L(\Sigma^* 1 \Sigma^*) =$ Linguaggio delle stringhe binarie con almeno un $1$.
$L((\Sigma\Sigma)^*) = L(\{0 \cup 1\}_°\{0 \cup 1\}) = \{00,\ 01,\ 10,\ 11\}^*$ = Stringhe binarie di lunghezza pari.
$L(0 \cup \epsilon)(1 \cup \epsilon) = \{0,\ 1,\ 01, \epsilon\}$.
$L(1^*\emptyset) = (1^*)_° L(\emptyset) = \emptyset \to$ Questo per definizione di **concatenamento**.
$L(\emptyset^*) = L(\emptyset)^* = \emptyset^* = \{\epsilon\} \to$ per definizione di **star**.
## Teorema
$A$ è **regolare** $\iff$ esiste una **regexp** $R$ tale che $L(R) = A$.
## Lemma
Sia $R$ una **regexp**, allora $L(R)$ è **regolare**.
## Dimostrazione
Avviene per **induzione** sulla **struttura** di $R$.

*Nota*: induzione strutturale $\to$ tutte le regexp più piccole di quella che sto valutando sono regolari.

* Sia $R=a$ per qualche $a$, allora $L(R) = \{a\}$.
  **Dimostro** che $L(R)$ è regolare
  ![[Pasted image 20241001150506.png]]
* Sia $R = \epsilon$, allora $l(R) = \{\epsilon\}$.
  **Dimostro** che $L(R)$ è regolare
  ![[Pasted image 20241001150526.png]]
* Sia $R = \emptyset$, allora $L(R) = \emptyset$.
  **Dimostro** che $L(R)$ è regolare
  ![[Pasted image 20241001150551.png]]
* Sia $R = R_1 \cup R_2$, allora $L(R) = L(R_1) \cup L(R_2)$. Per ipotesi $L(R_1)$ e $L(R_2)$ sono regolari. Concludo che $L(R) = L(R_1) \cup L(R_2)$ è regolare perché i linguaggi regolari sono **chiusi** rispetto a $\cup$.
* Segue per $_°$ e per $^*$.
## Esempio
Convertiamo $(a,b \cup a)^*$ in un **NFA**.
...

## Lemma
Se $a$ è **regolare**, allora esiste una **regexp** $R$, tale che $L(R) = a$.

Sia $a$ **regolare**, allora esiste un **DFA** $D$ tale che $L(D) = a$.
L'idea è quella di tradurre il **DFA** in una **regexp** equivalente.
![[Pasted image 20241001150946.png]]
* **GNFA**: Generalized NFA, è un NFA, i cui archi sono etichettati non con dei caratteri ma con delle regexp.
*Idea*: Non "mangiano" un carattere alla volta, ma blocchi di caratteri.
![[Pasted image 20241001151449.png]]
## Dettagli
Lavoriamo con **GNFA** che rispettano i seguenti *vincoli*:
* Hanno un solo **stato inziale** ed un solo **stato accettante** (diverso dall'inziale).
* Lo **stato iniziale** ha archi in uscita verso tutti gli altri stati e nessun arco in entrata.
* Lo **stato accettante** ha archi in entrata da tutti gli altri stati e nessun arco in uscita.
* Il resto del grafo è completamente connesso.
## Costruzione del GNFA a partire da un DFA
![[Pasted image 20241001152440.png]]

Abbiamo ottenuto così un **GNFA** con $k+2$ stati
## Rimuovere stati dal GNFA
![[Pasted image 20241001153107.png]]

Ad ogni iterazione rimuovo uno stato $q_{strip}$ fino ad ottenere un automa con 2 stati, uno inziale ed uno accettante, con un collegamento fatto da tutte le **regexp**.
## Da DFA a regexp
![[Pasted image 20241002141032.png]]
# Linguaggi non Regolari
* È **facile** dimostrare che un linguaggio $A$ è **regolare** $\to$ (NFA, DFA, regexp).
* È invece **difficile** dimostrare che un linguaggio $A$ non è **regolare**.
## Esempio
$$\{0^n1^n\ |\ n \geq 0\}$$
$$\{\epsilon,\ 01,\ 0011,\ 000111\, ...\}$$
## Di nuovo su linguaggi non regolari
**Osservazione**: Il linguaggio delle stringhe binarie che hanno lo stesso numero di $01$ e $10$ è regolare (**ESERCIZIO**)

La non regolarità si può dimostrare utilizzando un risultato noto come **Pumping Lemma**.
## Pumping Lemma
Sia $A$ un **linguaggio regolare**, allora esiste un intero $p \geq 1$ tale che per ogni stringa $s \in A$, tale che $|s| \geq p$, si hanno le seguenti condizioni:
* $s = xyz$ per qualche $x,y,z$ tali che:
  * $\forall i \geq 0: xy^iz \in A$ ($i$ copie concatenate di $y$, anche $0$).
  * $|y| > 0$
  * $|xy| \leq p$
## Dimostrazione
Sia $A$ regolare, allora esiste un DFA $D$, tale che $L(D)=A$. Poniamo $p$ pari al numero di stati del DFA $D$. Considero una stringa $s = w_1,w_2,..w_n$ con $n \geq p$. e tale che $s \in A$ (cioè il DFA la riconosce).
Visto che $s \in A$ esiste una **sequenza di stati** $q_0,q_1,...,q_n$ tali che:
* $q_0$ è lo *stato inziale*.
* $q_n$ è lo *stato accettante*.
* Ogni stato passa in un altro secondo la *funzione di transizione* $\delta$.

Poniamo:
* $p$ uguale al numero di stati del DFA
* $s = w_1,...w_n$ con $n \geq p$.
* $q_0,q_1,...,q_n$ con $n \geq p$ (ovvero $n + 1$ stati $\geq p+1$).

**Quindi**: In questa sequenza di stati ce n'è almeno uno che si ripete. Chiamiamo $q_i$ tale stato.

Vediamo quindi l'**"attraversamento" del DFA**:
![[Pasted image 20241002143639.png]]

Le **frecce** incluse nel cammino sono etichettate con i caratteri di $s$. Otteniamo il seguente schema:
![[Pasted image 20241002143951.png]]

La dimostrazione dei primi due punti è banale.

Dimostriamo che $|xy| \leq p$:
* Se abbiamo una sequenza di $p+1$ stati, ci deve essere uno stato che si ripete. Se tocco $p+1$ stati ho letto $p$ caratteri (quello in più viene dallo *stato iniziale*).
  I primi caratteri della stringa sono $xy$. Quindi $|xy| \leq p$.
## Utilizzo del Pumping Lemma
Sia $A$ il linguaggio di cui vogliamo mostrare la **non-regolarità**:
* Assumo *per assurdo* che $A$ sia **regolare**.
* Visto che $A$ è regolare, deve valere il **Pumping Lemma**.
* Contraddico il **Pumping Lemma** (controesempio).
* Concludo per assurdo che $A$ non è regolare.
Il **passo difficile** è il terzo.
## Contraddire il Pumping Lemma
* **Pumping Lemma**: Per tutte le stringhe $s \in A$ con $|s| \geq p$ esistono $xyz$ tali che $s = xyz$ e:
	* $\forall i \geq 0 \quad xy^iz \in A$
	* $|y| > 0$
	* $|xy| \leq p$
* **Contrario del Pumping Lemma**: Esiste una stringa $s \in A$ con $s \geq p$, tale che **per ogni** $xyz$ tali che $s = xyz$ si abbia:
	* $\exists i \geq 0 \quad xy^iz \notin A$. **or**
	* $|y| = 0$ **or**
	* $|xy| > p$

**Rifrasando il tutto**: Esiste $s \in A$ con $|s| \geq p$ tale che per ogni $xyz$ tali che $s = xyz$ con $|y| > 0$ e $|xy| \leq p$ si abbia che: $$\exists i \geq 0 \quad xy^iz \notin A$$
## Esempio 1
Dimostriamo che $A = \{0^n1^n\}$ non è regolare.

Assumiamo per assurdo che $A$ sia regolare, allora deve valere il pumping lemma. Prendiamo come controesempio $s = 1^p0^p$.
* Osservo intanto che la stringa $s \in A$ e che rispetta la **pumping length** (ovvero che $|s| \geq p$).
* Scriviamo $s$ nella forma $s = xyz$ con $|y| > 0$ e $|xy| \leq p$.
* Dimostriamo che esiste $i \geq 0$ tale che $xy^iz \notin A$.

**Dimostrazione senza usare l'ipotesi $|xy| \leq p$**:
	Ragioniamo sui caratteri che occorrono in $y$:
		* $y$ contiene solo $0$. Allora $xy^2z$ ha forma $0^{p+k}1^p$ con $k > 0$ (perché per ipotesi $y$ non è vuota). Tale stringa non sta in $A$ perché ha più $0$ che $1$
		* $y$ contiene solo $1$. Analogamente ma specularmente a sopra otteniamo una stringa di forma $0^p1^{p+k}$. La conclusione è la stessa.
		* $y$ contiene sia $0$ che >$1$. Ma allora $xy^2z$ avrà degli $1$ prima degli $0$. Tale stringa non sta nel linguaggio.
![[Pasted image 20241002151809.png]]

**Dimostrazione usando l'ipotesi $|xy| \leq p$**:
	In tal caso so che $y$ comprende solo $0$, di conseguenza:
		* $xy^2z$ non sta in $A$ perché ha forma $0^{p+k}1^p$ con $k > 0$.
## Esempio 2
Dimostriamo che $F = \{ww\ |\ w \in \{0,1\}^*\}$ è non regolare.

Assumiamo per assurdo che $F$ sia regolare. Prendiamo come controesempio per il **pumping lemma** la stringa $s = 0^p10^p1$:
* Osservo intanto che la stringa $s \in A$ e che rispetta la **pumping length**.
* Sia $s = xyz$ con $y > 0$ e $|xy| \leq p$.
* Applicando la condizione $|xy| \leq p$ sappiamo che $y$ sta nei primi $p\ 0$.
* Quindi $xy^2z$ ha forma $0^{p+k}10^p1 \notin A$ per $k > 0$.
## Esercizio 1
Sia $D$ l'insieme delle stringhe che contengono un numero pari di $a$, un numero dispari di $b$ e non contengono la sotto-stringa $ab$
* Costruire una regexp per $D$
* Costruire un **DFA** per $D$
**DFA**:
![[Pasted image 20241008143237.png]]
*Nota*: lo stato pozzo viene generalmente omesso per leggibilità
*Nota*: Questo DFA potrebbe avere uno stato in meno e cominciare da quello in alto a destra.

**Regexp corrispondente**: $b(bb)^*(aa)^*$
## Esercizio 2
Sia $D$ l'insieme delle stringhe che contengono lo stesso numero di occorrenze delle sotto-stringhe $01$ e $10$. Dimostrare che $D$ è regolare.
**DFA**:
![[Pasted image 20241008143518.png]]
**Regexp corrispondente**: $R = \epsilon \cup 0 \cup 1 \cup 0(0 \cup 1)^*0 \cup 1(1\cup 0)^*1$ 
## Esempio 3
Dimostrare che se $A$ è regolare, allora $\overline{A}$ è regolare.
* $\overline{A} = \{w | w \notin A\}$
**Dimostrazione**: 
	Dato che $A$ è regolare, allora esiste un **DFA** $D$, tale che $L(D)=A$. Sia $D=(Q,\Sigma,\delta,q_0,F)$, definisco un nuovo **DFA** $D'=(Q,\Sigma,\delta,q_0,Q-F)$ 
	Allora è facile dimostrare che per ogni $w \in \Sigma^*(\to \text{tutte le stringhe costruite sullo stesso alfabeto}),w \in L(D) \iff w \notin L(D')$ 
	* Se $w \in L(D)$, allora esistono stati $q_0,q_1,...,q_n$ tali che $q_n \in F$ e ciascuno stato va nel prossimo secondo $\delta$. Visto che $q_n \notin Q-F$, abbiamo che $w \notin L(D')$.
	* Se $w \notin L(D)$, allora esistono stati $q_0,q_1,---,q_n$ tali che $q_n \notin F$ e ciascuno stato va nel prossimo secondo $\delta$. Visto che $q_n \in Q-F$, abbiamo che $w \in L(D')$.
## Esempio 4
Dimostrare che $A= \{a^{2^n}\ |\ n \geq 0\}$ non è regolare.
**Dimostrazione**:
	Assumiamo per assurdo che $A$ sia regolare e sia $p$ la sua **pumping length**.
	Consideriamo la stringa $s = a^{2^p}$.
	Abbiamo in particolare che $s \in A$ e $|s| \geq p$.
	Sia $s = xyz$ con $|y| > o$ e $|xy| \leq p$, osserviamo che:
	* $|xyz| < |xy^2z|$ perché la $|y| > 0$.
	* $2^p = |xyz| < |xy^2z| \leq 2^p+p$ perché $|xy| \leq p$.
	* $2^p = |xyz| < |xy^2z| \leq 2^p+p < 2^p + 2^p$ perché $p < 2^p\  \forall p\geq1$
	* $2^p + 2^p = 2^{p+1}$.
	Abbiamo dimostrato che $2^p < |xy^2z| < 2^{p+1}$, quindi $xy^2z$ non sta nel linguaggio $A$ ($xy^2z \notin A$).
## Esempio 5
Dimostrare che $G = \{ab^nc^n | n \geq 0\}$ non è regolare.
**Dimostrazione**:
	Assumiamo per assurdo che $G$ sia regolare e sia $p$ la sua **pumping length**.
	Consideriamo la stringa $s = ab^pc^p$. Osserviamo che $s \in G$ e $|s| \geq 0$
	Assumiamo $s = xyz$ con $|y| > 0$ e $|xy| \leq p$. Ragiono per casi:
	* $a$ occorre in $y$. osservo che $xy^2z \notin G$ perché contiene più di una $a$. (uguale e contrario con il **pumping down**).
	* $a$ non occorre in $y$. Dato che $|xy| \leq p$, allora $y$ contiene solo $b$.
	  Allora $xy^2z = ab^{p+k}c^p$ con $k > 0$.
	  Quindi $xy^2z \notin G$.

Utilizzare il fatto che $G$ non è regolare, per dimostrare la non regolarità di $F = \{a^ib^jc^k\ |\ i,j,k \geq 0 \land (i = 1 \implies j = k)\}$.
**Dimostrazione**:
	Assumiamo per assurdo che $F$ sia regolare.
	Osserviamo che $G = F \cap ab^*c^*$ 
	Allora poiché $F$ e $ab^*c^*$ sono regolari per assunzione, di conseguenza per chiusura degli operatori regolari anche $G$ risulta essere regolare. Ma questo è assurdo.