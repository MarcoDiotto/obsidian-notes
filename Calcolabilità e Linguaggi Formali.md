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
* $\forall i \in [0,n-1]: \delta(r_i, w_{i+1}) = r_{i + 1}$
## Esempio
![[Pasted image 20240918142946.png]]

Dimostriamo che accetta $1010$:
* **Sequenza di stati**: $q_0 (\to \text{iniziale}), q_1, q_0,  q_1,q_0$

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
$L(D) =$ Stringhe composte da soli $0$ di lunghezza pari o multipli di $3$.
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
* $Q = Q_1 \cup Q_2$.
* $q_0 = q_1$.
* $F = F_2$.
* $\delta(q,a) = \delta_1(q,a) \to \text{se } q \in Q_1 - F_1,\ \delta_2(q,a) \to \text{se } q \in Q_2,\ \delta_1(q,a) \to \text{se } q \in F_1 \land a \neq \epsilon,\ \{q_2\} \cup \delta_1(q,a) \text{se } q \in F_1 \land a = \epsilon$
## Dimostrazione regolarità di $A^*$
Se $A$ è *regolare*, allora $A^*$ è *regolare*.
$A^* = \{w_1, ..., w_k | \forall i : w_i \in A \land k \geq 0\}$.

Sia $A$ regolare, allora esiste un NFA $N$ tale che $L(N) = A$. Costruisco un NFA $M$ tale che $L(M) = A^*$.
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
* Se $R_1$ e $R_2$ sono regexp, allora $R_{1°} R_2$ è una regexp.
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
* Sia $R = \epsilon$, allora $L(R) = \{\epsilon\}$.
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

Assumiamo per assurdo che $A$ sia regolare, allora deve valere il pumping lemma. Prendiamo come controesempio $s = 0^p1^p$.
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
	* Se $w \notin L(D)$, allora esistono stati $q_0,q_1,...,q_n$ tali che $q_n \notin F$ e ciascuno stato va nel prossimo secondo $\delta$. Visto che $q_n \in Q-F$, abbiamo che $w \in L(D')$.
## Esempio 4
Dimostrare che $A= \{a^{2^n}\ |\ n \geq 0\}$ non è regolare.
**Dimostrazione**:
	Assumiamo per assurdo che $A$ sia regolare e sia $p$ la sua **pumping length**.
	Consideriamo la stringa $s = a^{2^p}$.
	Abbiamo in particolare che $s \in A$ e $|s| \geq p$.
	Sia $s = xyz$ con $|y| > 0$ e $|xy| \leq p$, osserviamo che:
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
# Linguaggi Context-Free
## Grammatiche Context-Free (CFG)
$$A \to 0A1\ |\ B$$
$$B \to \#$$
Una grammatica context-free viene descritta con **produzioni** o **regole**, che sono sostanzialmente riscritture.
Per esempio :
* la prima produzione significa $A$ può riscriversi come  $0A1$ oppure come $B$
* la seconda produzione significa $B$ può essere riscritta come $\#$
Notiamo che i caratteri possono essere divisi in:
* **Non Terminali** (o **variabili**): simboli che possono essere riscritti in un altro modo (indicati con *lettere maiuscole*)($A,B$).
* **Terminali**: simboli che non possono essere riscritti (indicati con *lettere minuscole*, *numeri* o *simboli*)($0,1,\#$).
* **Start symbol**: il primo carattere che vedo nella prima produzione ($A$).

Le **stringhe generate** sono stringhe generate di terminali ottenute dallo **start symbol** (*non terminale*) tramite riscritture permesse dalle *produzioni*.

Per esempio io potrei dire: $$A \implies 0A1$$ che deve essere riscritta poiché $A$ non è terminale. Posso ottenere ad esempio:
$$\implies 00A11$$
Ho ancora lo stesso problema. Cambio la produzione: $$00B11$$A questo punto devo solo riscrivere $B$ secondo il suo terminale: $$00\#11$$
Il linguaggio della nostra stringa è: $$L(G) = \{0^n\#1^n\ |\ n \geq 0\}$$
Tale linguaggio è **non regolare**, ma può essere descritto da una grammatica **context-free**. I linguaggi **context-free** sono più ampi di quelli **regolari**, pertanto *ogni linguaggio regolare potrà essere descritto da una grammatica context free*.

Il processo eseguito per scrivere un *non terminale* come sequenza di *terminali* è detto **derivazione**.
## Parse Tree
Un **parse tree** è un albero con lo **start symbol** alla radice, che cresce in base alle **produzioni**:
![[Pasted image 20241009142205.png]]
## Definizione di Linguaggio Context-Free
Un linguaggio $A$ si dice **context-free** $\iff$ esiste una **CFG** $G$ tale che $L(G) = A$.
## Definizioni chiave nella teoria delle CFG
### Definizione di CFG
* Una **CFG** $G$ è una quadrupla $(V,\Sigma,R,S)$ dove:
	* $V$ è un insieme finito di **non terminali** (o **variabili**).
	* $\Sigma$ è un insieme finito di **terminali**, tali che $V \cap \Sigma = \emptyset$.
	* $R$ è un insieme finito di **produzioni** (o **regole**) della forma $A \to w$, dove $A \in V$ e $w \in (V \cup \Sigma)^*$.
	* $S \in V$ è lo **start symbol**.
Per esempio nella grammatica di prima:
$$A \to 0A1\ |\ B$$$$B \to \#$$
Abbiamo:
* $V = \{A,B\}$.
* $\Sigma = \{0,1,\#\}$.
* $R = \{A \to 0A1,\ A \to B,\ B \to \#\}$.
* $S = A$.
Tali grammatiche sono dette **context-free** perché un *non-terminale* si scrive sempre allo stesso modo indipendentemente dal contesto (ovvero i simboli vicino al non-terminale).

* Siano ora $u,v,w \in (V \cup \Sigma)^*$ e sia $A \to w \in R$, diciamo che $uAv \implies uwv$ e lo chiamiamo "**produce**" (la freccia) 
* Diciamo che $u$ **deriva** $v$ (indicato con $u \implies^*v$) $\iff$ $u = v$ oppure $u \implies w_1 \implies w_2 \implies w_2 \implies ... \implies v$ per qualche $w_1,w_2,...$ 
## Esempio 1
Abbiamo che $A \implies^*00\#11$ perché $A \implies 0A1 \implies 00A11 \implies 00B11 \implies 00\#11$

Sia $G$ una **CFG**, definiamo il suo linguaggio come:
* $L(G)=\{w\in\Sigma^*\ |\ S \implies^* w\}$
## Esempio 2
Si assuma $\Sigma = \{0,1\}$, si forniscano **CFG** per i seguenti linguaggi:
* Stringhe che comprendono almeno tre $1$: $S \to A1A1A1\quad A \to 0A\ |\ 1A\ |\ \epsilon$.
* Stringhe che iniziano e finiscono con lo stesso simbolo: $S \to 0A0\ |\ 1A1\ |\ 0\ |\ 1\quad A \to 0A\ |\ 1A\ |\ \epsilon$.
* Stringhe di lunghezza dispari: $S \to CP\quad C \to 0\ |\ 1\quad P \to 00P\ |\ 01P\ |\ 10P\ |\ 11P\ |\ \epsilon$.
* Stringhe palindrome: $S \to 0S0\ |\ 1S1\ |\ 0\ |\ 1\ |\ \epsilon$.
* Nessuna stringa $S \to S$ oppure $\emptyset$.
## Dimostrazione di correttezza di una grammatica
$$A \to 0A1\ |\ B$$$$B \to \#$$
Abbiamo detto che $L(G) = \{0^n\#1^n\ |\ n \geq 0\}$.
Dimostriamo che $w \in L(G) \iff w \in 0^n\#1^n$ per qualche $n \geq 0$.
* $\implies$ Sia $w \in L(G)$, allora $A \implies^*w$. Facciamo *induzione sulla lunghezza della dimensione*. Distinguiamo due casi:
	* $A \implies0A1\implies^*w$. Allora $w = 0v1$ con $A \implies^*v$.
	* $A \implies B \implies^*w$. In questo caso $w = \#$, quindi $w$ ha la forma giusta.
	Per ipotesi induttiva: $v = 0^n\#1^n$ con $n \geq 0$, Ma allora $w = 0^{n+1}\#1^{n+1}$.
* $\impliedby$ Sia $w = 0^n\#1^n$ con $n \geq 0$, dimostro che $w \in L(G)$. Facciamo *induzione su $n$*:
	* Se $n = 0: w = \#$ e $A \implies B \implies \#$.
	* Se $n > 0: w = 0^{m+1}\#1^{m+1}$ con $m \geq 0$. Per ipotesi induttiva $A \implies^*0^m\#1^m$. Ma allora $A \implies 0A1\implies^*00^m\#11^m$.
## Esempio
$$S \to aSb\ |\ SS\ |\ \epsilon$$
Che stringa genera? Genera una stringa che rappresenta l'apertura  la chiusura delle parentesi.
## Ambiguità
Una **CFG** $G$ è ambigua $\iff$ esiste $w \in L(G)$ tale che $w$ ha almeno due **parse tree** diversi (ma non **derivazioni** diverse).
$$E \to E+E\ |\ E\times E\ |\ a$$
Tale CFG è ambigua perché $a + a \times a$ è parte del suo linguaggio e può essere derivata con due *parse tree* diversi:
![[Pasted image 20241009153118.png]]

Perché parse-tree diversi non significa derivazioni diverse?
	Immaginiamo di avere una grammatica del tipo: $$S \to AB$$$$A \to a$$$$B \to b$$ Non è ambigua, poiché genera solamente il **parse-tree**:
	![[Pasted image 20241015140631.png]]
	Tuttavia genera due possibili derivazioni: $$S \implies AB \implies aB \implies ab$$$$S \implies AB \implies Ab \implies ab$$
Per ovviare a tale problema usiamo sempre le **derivazioni a sinistra**, cioè utilizziamo la derivazione che riscrive sempre in non-terminale più a sinistra. Facciamo così solamente per convenzione, avremmo potuto prendere anche le derivazioni a destra.
## Forma normale di Chomsky
Una **CFG** è in forma normale di Chomsky $\iff$ ognuna delle sue **produzioni** è in uno dei seguenti formati:
* $A \to BC$ dove $B,C$ non sono lo **start symbol**.
* $A \to a$
* $S \to \epsilon$ dove $S$ è lo **start symbol**.
Essa è particolarmente importante, poiché qualsiasi **CFG** può essere convertita in forma normale di Chomsky.
## Esempio
$$S \to AB\ |\ \epsilon$$$$A \to 0$$$$B \to CD$$$$C \to 1$$
$$D \to 1$$
Questa è una **CFG** in forma normale di Chomsky.
## Teorema
Per ogni **CFG** $G$ esiste una **CFG** $H$ in forma normale di Chomsky, tale che $L(H) = L(G)$.
## Dimostrazione
Definiamo un algoritmo che converte $G$ in una **CFG** equivalente, che soddisfi la forma normale di Chomsky.
Di seguito riportiamo l'algoritmo:
* Generiamo un nuovo **start symbol** $S'$ ed aggiungiamo la **produzione** $S' \to S$. Tale trasformazione preserva il linguaggio ed assicura per costruzione che lo start symbol non occorra a destra di una produzione.
* Eliminiamo le produzioni della forma $A \to \epsilon$, dove $A$ non è lo **start symbol**. Per tutte le regole della forma $R \to uAv$ introduco una nuova regola $R \to uv$. Ciò deve essere fatto per tutte le occorrenze di $A$. Per esempio, data una regola del tipo $R \to uAvAw$, sarà necessario introdurre nuove regole: $R \to uvAw,\ R\to uAvw,\ R \to uvw$. 
* Eliminiamo le produzioni "unitarie" della forma $A \to B$. Per tutte le regole della forma $B \to u$, introduco una nuova regola $A \to u$.
* Rimpiazziamo ogni regola della forma $A \to u_1,u_2,..,u_k$ con $k \geq 3$ e la sostituiamo con nuove regole del tipo $A \to u_1A_1,\ A_1 \to u_2A_2,..,\ A_{k-2} \to u_{k-1}u_k$. Nel nostro caso $u$ può essere sia un **terminale**, sia un **non-terminale**. Pertanto andiamo a rimpiazzare ogni terminale $u_i$ con un nuovo **non-terminale** $U_i$ e aggiungiamo la regola $U_i \to u_i$.

*Note*:
* L'**ordine** in cui effettuiamo tali step è importante e ci garantisce la non-invalidazione di step precedenti.
* Negli step $2,3$ è necessario tenere traccia di cosa è già stato eliminato, altrimenti potrebbero essere re-inseriti e dare vita a loop.
## Esempio
$$S \to ASA\ |\ aB$$$$A \to B\ |\ S$$$$B \to b\ |\ \epsilon$$
Utilizziamo l'algoritmo per portare la grammatica in forma normale di Chomsky:
$$S_0 \to S$$$$S \to ASA\ |\ aB\ |\ a$$$$A \to B\ |\ S\ |\ \epsilon$$$$B \to b$$Rimuovendo anche la $\epsilon$ a destra di $A$ otteniamo:
$$S_0 \to S$$$$S \to ASA\ |\ aB\ |\ a\ |\ AS\ |\ SA\ |\ S$$$$A \to B\ |\ S$$$$B \to b$$Dobbiamo ora rimuovere le produzioni unitarie ($S \to S$ e $S_0 \to S$):
$$S_0 \to ASA\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$S \to ASA\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$A \to B\ |\ S$$$$B \to b$$
Ora togliamo $A \to B$ e $A \to S$:
$$S_0 \to ASA\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$S \to ASA\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$A \to b\ |\ ASA\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$B \to b$$
Dobbiamo ora modificare tutte le produzioni che contengono $ASA$:
$$S_0 \to AA_1\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$S \to AA_1\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$A \to b\ |\ AA_1\ |\ aB\ |\ a\ |\ AS\ |\ SA$$$$B \to b$$
$$A_1 \to SA$$
Ora modifichiamo le produzioni che contengono $aB$:
$$S_0 \to AA_1\ |\ UB\ |\ a\ |\ AS\ |\ SA$$$$S \to AA_1\ |\ UB\ |\ a\ |\ AS\ |\ SA$$$$A \to b\ |\ AA_1\ |\ UB\ |\ a\ |\ AS\ |\ SA$$$$B \to b$$
$$A_1 \to SA$$
$$U \to a$$
# Automi a Pila (Pushdown Automata, PDA)
Un **automa a pila** è sostanzialmente un **NFA** a cui viene aggiunto uno **stack**:
* Legge l'input sequenzialmente come un **NFA**.
* Ha uno stato interno che può cambiare.
* Ha a disposizione uno **stack infinito** su cui *leggere* e *scrivere*.

Un **NFA**(anche un **DFA**) ha una quantità di memoria proporzionale ai suoi dati, in questo caso abbiamo memoria infinita.

Lo **stack** è una struttura dati **LIFO** con operazioni di *push* e *pop*.
## Esempio
Creiamo un **PDA** per $\{0^n1^n\ |\ n \geq 0\}$:
* Leggi i simboli di input.
* Ogni volta che leggi uno $0$ fai *push* di $0$ sullo **stack**.
* Quando arriva un $1$ passa in un nuovo stato e fai *pop* di uno $0$ dallo **stack**.
* Finché arrivano $1$ continua a fare pop.
* Se hai finito l'*input* e lo **stack** è vuoto **accetta**.
* Se hai finito l'*input* e lo **stack** non è vuoto: **rifiuta**.
* Se arriva uno $0$ dopo un $1$: **rifiuta**.
* Se ho ancora **input** di tipo $1$ ma lo **stack** è vuoto: **rifiuta**.

*Nota*: perché **PDA** = **NFA** + **stack** e non **DFA** + **stack**? Si può dimostrare che **PDA** non deterministici e **PDA** deterministici non  sono equivalenti. 
Dimostreremo che **PDA** non deterministici e **CFG** sono equivalenti.
$$DFA = NFA$$$$CFG = PDA \neq DPDA\ (PDA\ \text{ deterministici})$$
## Definizione di PDA
Un **PDA** è una sestupla $\{Q,\Sigma,\Gamma,\delta,q_0,F\}$ dove:
* $Q$ è un insieme finito di **stati**.
* $\Sigma$ è un insieme finito di **input**, detto **alfabeto**.
* $\Gamma$ è un insieme finito di simboli che **posso scrivere sullo stack**, detto **alfabeto dello stack**.
* $\delta: Q \times \Sigma_\epsilon \times \Gamma_\epsilon \to \mathbb{P}(Q \times \Gamma_\epsilon)$ , dove $\Sigma_\epsilon = \Sigma \cup \{\epsilon\}$ e $\Gamma_\epsilon = \Gamma \cup \{\epsilon\}$ è la **funzione di transizione**.
* $q_0 \in Q$ è lo **stato iniziale**. 
* $F \subseteq Q$ è l'**insieme degli stati accettanti**.
## Come computa un PDA
Sia $M = (Q,\Sigma,\Gamma,\delta,q_0,F)$ un **PDA**. Diciamo che $M$ **accetta** la stringa $w$ $\iff$:
* $w = w_1w_2,...,w_n$, dove $\forall i \in [1,m]: w_i \in \Sigma_\epsilon$.
* Esistono una sequenza di stati $r_0,r_1,...,r_m \in Q$ e una sequenza di stack $s_0,s_1,...,s_m \in \Gamma^*$ tale che valgano le seguenti condizioni:
	* $r_0 = q_0$ e $s_0 = \epsilon$.
	* Per $i = 0,...,m-1$ abbiamo $(r_{i+1},b) \in \delta(r_i,w_{i+1},a)$ dove $s_i = at$ e $s_{i+1} = bt$ per qualche $a,b \in \Gamma_\epsilon$ e $t \in \Gamma^*$.
	* $r_m \in F$  ($\to$ non è richiesto che lo stack si svuoti per accettare).

*Note sul punto $2.2$*:
	Identifichiamo 4 possibilità:
	* $a \neq \epsilon,\ b \neq \epsilon \to$ si tratta di una *pop* seguita da una *push*.
	* $a = \epsilon,\ b \neq \epsilon \to$ si tratta di una semplice *push*.
	* $a \neq \epsilon,\ b = \epsilon \to$ si tratta di una *pop*.
	* $a = \epsilon,\ b = \epsilon \to$ non modifica lo *stack*.

Il linguaggio riconosciuto da un **PDA** resta composto dalle stringhe che vengono accettate dallo stesso.
## Notazione Grafica per PDA
![[Pasted image 20241016143138.png]]
L'automa passa da $q_i$ a $q_j$ leggendo un input $w$ quando $a$ è in cima allo **stack**. $b$ è la cima dello **stack** (Un altro esempio può essere $\epsilon \to b$, ovvero un **push** di $b$).
## Accettazione per stack vuoto
Molti **PDA** vogliono accettare solamente quando lo stack si è svuotato. Questo non è richiesto dalla definizione formale. 
Un esempio è un **PDA** per: $$\{0^n1^n\ |\ n \geq 0\}$$
Come testiamo se lo stack è vuoto?
* Non appena inizia la computazione facciamo *push* di un **simbolo convenzionale** (per esempio $)
* Quando rivedo  $ sono sicuro che lo **stack** si sia svuotato.
## Esempio 1
Troviamo un **PDA** per $\{0^n1^n\ |\ n \geq 0\}$:
![[Pasted image 20241016144858.png]]
## Esempio 2
Troviamo un **PDA** per $\{a^ib^jc^k\ |\ i,j,k \geq 0 \land (i = j \lor i = k)\}$
![[Pasted image 20241016151115.png]]

Di seguito viene riportata l'implementazione modificata, che accetta **casi-limite**, come ad esempio $bb$:
![[Pasted image 20241016152236.png]]
## Esempio 3
Troviamo un **PDA** per $\{ww^R\ |\ w \in \{0,1\}^*\}$, dove $w^R$ è letta da destra a sinistra. Per esempio $\color{green}100\color{red}001$ sta in questo linguaggio:
![[Pasted image 20241016153117.png]]
## Teorema
Un linguaggio $A$ è **context-free** $\iff$ esiste un **PDA**  $P$ tale che $L(P) = A$.
## Corollario
Qualsiasi linguaggio **regolare** è anche **context-free**.  ($\to$ cioè i linguaggi regolari formano un sottoinsieme dei linguaggi context-free)
## Dimostrazione
Sia $A$ un **linguaggio regolare**, allora esiste un **NFA** $N$ tale che $L(N) = A$.
Un **NFA** è un **PDA** che non tocca lo **stack**, quindi $N$ è anche un **PDA**. Concludo pertanto che $A$ è **context-free**.
## Dimostrazione del teorema $\implies$
Se $A$ è un **linguaggio context-free** allora esiste un **PDA** tale che $L(P) = A$.

*Idea*: dato che $A$ è context-free, esiste una **CFG** $G$ tale che $L(G) = A$. Converto quindi $G$ in un **PDA** equivalente.

**CFG di esempio**:
$$S \to AB$$ $$A \to a$$
$$B \to b\ |\ bB$$
$$C \to c$$

Verifichiamo per $w = abb$. La derivazione è la seguente: $$S \implies AB \implies aB \implies abB \implies abb$$

Simuliamo tale derivazione con un **PDA**:

![[Pasted image 20241022142037.png]]
Questa tecnica viene chiamata **parsing top-down**, ed è equivalente alla definizione di un **parsing tree**. ($\to$ è una tecnica poco usata perché computazionalmente inefficiente, tuttavia noi la useremo nella dimostrazione)
Passiamo alla **dimostrazione** vera e propria:

Sia $A$ un linguaggio **context-free**, allora esiste una **CFG** $G$ tale che $L(G) = A$. Costruiamo il seguente **PDA** a partire da $G$ (definizione a parole):
* Metti sullo **stack** $ e poi lo **start symbol** $S$.
* Ripeti i seguenti passi fino a terminazione:
	* Se sulla cima dello **stack** c'è un **non-terminale** $A$, scegli non deterministicamente una produzione $A \to u_1,...,u_k$ è fai **push** di $u_k,...,u_1$ dopo aver fatto **pop** di $A$.
	* Se sulla cima dello **stack** c'è un **terminale** $a$, confrontalo con il prossimo **carattere di input**. Se sono uguali fai **pop**, altrimenti **rifiuta** (lungo questo ramo del non-determinismo).
	* Se sulla cima dello **stack** c'è $ passa nello **stato di accettazione**. Ciò comporta **accettazione** se tutto l'input è stato consumato.
## Descrizione Grafica del PDA
![[Pasted image 20241022143803.png]]
## Esempio di conversione
Convertiamo la seguente **CFG** in un **PDA**:
$$S \to aTb\ |\ \epsilon$$
$$T \to Ta\ |\ \epsilon$$

![[Pasted image 20241022144611.png]]
## Dimostrazione del Teorema $\impliedby$
Sia $A$ un linguaggio tale per cui esiste un **PDA** $P$ tale che $L(P) = A$, allora $A$ è **context-free**.

*Idea*: Convertiamo $P$ in una **CFG** $G$ tale che $L(P) = L(G)$:
* Rendiamo $P$ *più disciplinato*, senza cambiare il suo linguaggio. Imponiamo in particolare tre requisiti (che non comportano **perdita di generalità**):
	* $P$ ha un solo stato accettante $q_{accept}$. ($\to$ faccio una $\epsilon$-transazione da tutti i vecchi stati accettanti a $q_{accept}$).
	* $P$ accetta solo quando lo **stack** è **vuoto** ($\to$ nel passaggio fra i vecchi stati accettanti a quello nuovo svuoto lo **stack**).
	* Ogni mossa di $P$ è una **push** oppure è una **pop** (al posto di nessuna delle due e di tutte e due assieme, comporta l'inserimento di stati intermedi).
	Visto che operiamo senza perdita di generalità, convertiamo solo $PDA$ che soddisfano tali vincoli.
* Definiamo una nuova  **CFG** che contiene un **non-terminale** $A_{pq}$ per ogni coppia di stati $p,q$ del **PDA**. La **CFG** conterrà delle produzioni opportune che avranno l'obbiettivo di simulare le transazioni del **PDA**.
  Tale **CFG** mi assicura che $A_{pq}$ deriva una stringa $x$ $\iff$ il **PDA** passa da $p$ con **stack vuoto** a $q$ con **stack vuoto** leggendo $x$.
  * Definiamo come **start symbol** della **CFG** il non terminale $A_{q_0q_{accept}}$ dove $q_0$ è lo **stato iniziale** del **PDA** e $q_{accept}$ è il suo **stato accettante**. 

Sviluppiamo il secondo passo definendo la **CFG** e dimostrando la proprietà desiderata.

La **CFG** ha un non terminale $A_{pq}$ per ogni coppia di stati $p,q$ del **PDA**. Le produzioni hanno tre formati possibili:
* $A_{pp} \to \epsilon$ per ogni stato $p$ del **PDA**.
* $A_{pq} \to A_{pr}A_{rq}$ per ogni tripla di stati $a,p,r$ del **PDA**.
* Se $(r,u) \in \delta(p,a,\epsilon)$ e $(q,\epsilon) \in \delta(s,b,u)$, allora $A_{pq} \to aA_{rs}b$ fa parte della **CFG**.

Ampliamo l'ultimo punto:
* $p$ è lo stato di partenza.
* $q$ è lo stato di arrivo.
* $a$ è il primo simbolo letto.
* $b$ è l'ultimo simbolo letto.
* $r$ è il secondo stato.
* $s$ è il penultimo stato.
* $u$ è il primo simbolo che metto sullo stack e anche l'ultimo che tolgo (corrisponde sostanzialmente al $).

Si può dimostrare che $A_{pq} \implies^* x \iff$ $p$ con **stack vuoto** arriva in $q$ con **stack vuoto** leggendo $x$.

Dimostriamo che se $A_{pq} \implies^* x$ allora $p$ con **stack vuoto** arriva in $q$ con **stack vuoto** leggendo $x$.
Per induzione sulla lunghezza della derivazione $A_{pq} \implies^* x$
* **Caso base**: derivazione di lunghezza $1$. L'unica produzione possibile che genera una stringa è $A_{pp} \to \epsilon$, cioè $A_{pp} \implies \epsilon$. Concludo banalmente perché $p$ con **stack vuoto** può rimanere fermo su $p$ con **stack vuoto** senza leggere caratteri.
* **Caso induttivo**: derivazioni con lunghezza $> 1$. Allora la derivazione sarà fatta così: $A_{pq} \implies \square \implies^* x$.
  Il carattere $\square$ dipende dalla regola della **CFG** che ho applicato:
  * $A_{pq} \implies A_{pr}A_{rq} \implies^* x$, in questo caso $x = yz$, dove $A_{pr} \implies^* y$ e $A_{rq} \implies^* z$. Tali derivazioni sono più corte di quelle di partenza, e quindi posso applicare l'ipotesi induttiva. L'ipotesi induttiva dice che $p$ con **stack vuoto** passa a $r$ con **stack vuoto** leggendo $y$ e che $r$ con **stack vuoto** passa a $q$ con **stack vuoto** leggendo $z$. Quindi $p$ con **stack vuoto** passa a $q$ con **stack vuoto** leggendo $yz = x$.
  * $A_{pq} \implies aA_{rs}b \implies^* x$
  * ...
# Linguaggi non Context-Free
Dimostrare che un linguaggio non è **context-free** è difficile in generale, perché dobbiamo dimostrare che esso non è generabile da alcuna **CFG** (oppure non riconoscibile da alcun**PDA**).
## Pumping Lemma per linguaggi Context-Free
Se $A$ è un linguaggio **context-free**, allora esiste un intero $p \geq 1$ (**pumping length**) tale che ogni stringa $w \in A$ con $|w| \geq p$ può essere divisa in cinque parti $w = uvxyz$ tali che:
* $\forall i \geq 0: uv^ixy^iz \in A$.
* $|vy| > 0$ ($\to$ se non fosse così sarebbe banalmente sempre vero).
* $|vxy| \leq p$.
## Idea della dimostrazione
Scegliamo una $p$ "molto grande", le stringhe con lunghezza $\geq p$ sono "molto lunghe". Essendo molto lunghe, tali stringhe avranno un **parse tree** "molto alto". Visto che i **non-terminali** sono in numero finito, in tale parse tree "molto alto" ci deve essere un non-terminale $R$ che si ripete.

**Parse-tree**:
![[Pasted image 20241023142122.png]]

* Se prendo il più piccolo dei due parse tree radicati in $R$ e lo metto al posto del più grande, ottengo un parse tree per $uxz$ (**pumping down**).
* Se prendo il più grande dei due parse tree radicati in $R$ e lo metto al posto del più piccolo, ottengo un parse tree per $uv^2xy^2z$ (**pumping up**).
## Dimostrazione
Se $A$ è **context-free**  esiste una **CFG** $G$, tale che $L(G) = A$. Definiamo $b$ come il numero massimo di simboli che occorrono a destra di una produzione di $G$. Assumiamo $b \geq 2$ (se $b < 2$ la dimostrazione è banale).
Sia $V$ l'insieme dei **non-terminali** di $G$.
Definiamo $p = b^{|V| + 1}$
Osserviamo che $b^{|V| + 1} \geq b^{|V|} + 1$ quando $b \geq 2$.

Consideriamo una stringa $w \in A$ con $|w| \geq p$. Ciò implica che $|w| \geq b^{|V| + 1}$. Ragioniamo sull'altezza dei **parse tree** di $w$:
* Parse tree di altezza $1$ $\implies$ stringa di lunghezza massima $b$
* Parse tree di altezza $2$ $\implies$ stringa  di lunghezza massima $b^2$
In generale parse tree di altezza $h$ genera stringhe di lunghezza massima $b^h$.

I parse tree di $w$ hanno altezza almeno $|V| + 1$.
Fra tutti i parse tree di $w$ prendiamo quello col numero minimo di nodi.
Prendiamo il *cammino* più lungo di tale **parse tree**, ovvero la sua *altezza*, Tale cammino deve contenere almeno $|V| + 1$ **non-terminali**. Ciò implica che lungo tale cammino, c'è almeno un non-terminale $R$ che si ripete. Ci concentriamo su un non-terminale che si ripete fra i $|V| + 1$ non-terminali in basso al cammino.

Per la dimostrazione della prima condizione basta guardare il disegno.
## Dimostrazione seconda condizione ($|vy| > 0$)
Assumiamo per assurdo che $|vy| = 0$, cioè $|v| = |y| = 0$.
Pertanto $uvxyz = uxz$. Ma allora se sostituisco il più piccolo albero radicato in $R$ al posto di quello più grande, ottengo un **parse tree** per $uxz$ che ha meno nodi del parse tree di partenza. Ciò è assurdo perché il parse tree di partenza è minimo.
## Dimostrazione terza condizione ($|vxy| \leq p$)
Abbiamo preso un **non-terminale** $R$ che occorre sul cammino più lungo dell'albero e si ripete fra i $|V| + 1$ non-terminali più in basso. Di conseguenza l'altezza del sotto-albero più grande radicato in $R$ è $|V| + 1$. Tale sotto-albero, che genera la stringa $vxy$, genera stringhe di lunghezza massima $b^{|V| + 1} = p$.
## Esempio 1
Dimostriamo che $B = \{a^nb^nc^n\ |\ n \geq 0\}$ non è context-free.
Assumo per assurdo che $B$ sia **context-free**, allora deve valere il pumping lemma. Sia $p$ la sua **pumping length**.

Consideriamo la stringa $s = a^pb^pc^p$. Abbiamo che $s \in B$ e $s \geq p$. Assumiamo che $s = uvxyz$, con $|vy| > 0$ e $|vxz| \leq p$. Ragioniamo per casi:
* $v$ contiene più di un tipo di carattere, oppure $y$ contiene più di un tipo di carattere. In tal caso $uv^2xy^2z \notin B$ perché non rispetta l'ordine dei caratteri.
  ![[Pasted image 20241023151831.png]]
* $v$ ed $y$ contengono al più un tipo di carattere. Per esempio $v$ contiene delle $a$ e $y$ contiene delle $b$. In generale c'è almeno un tipo di carattere che non occorre né in $v$ né in $y$. Di conseguenza $uv^2y^2z \notin B$ perché tale carattere sarà sotto-rappresentato.
## Esempio 2
Dimostriamo che $D = \{ww\ |\ w \in \{0,1\}^*\}$ non è context-free.
Assumo per assurdo che $D$ sia context-free, allora vale il pumping lemma. Sia $p$ la sua pumping length.

Consideriamo $s = 0^p10^p1$. Purtroppo questa stringa è *pompabile*

Consideriamo la stringa $s =0^p1^p0^p1^p$.
Osserviamo che se $s = uvxyz$, allora $vyz$ deve stare a cavallo fra le due metà della stringa. Infatti se cade nella prima o nella seconda metà esco dal linguaggio con un **pumping up**. Se $vyz$ sta a cavallo delle due metà, allora $uv^2xy^2y = 0^p1^i0^j1^p$, dove $i \ne p \lor j \ne p$. Questa stringa non sta nel linguaggio $D$ perché la prima metà è diversa dalla seconda.
## Esercizio 1
Dimostrare che la classe dei linguaggi context free è chiusa rispetto ad unione, concatenazione e star.

Dimostriamo la chiusura rispetto all'unione, cioè se $A$ e $B$ sono CFL (context-free language), allora $A \cup B$ è un CFL.
Dato che $A$ e $B$ sono CFL, esistono delle CFG $G = (V_1,\Sigma_1, R_1, S_1)$ e $H = (V_2,\Sigma_2,R_1,S_2)$, tali che $L(G) = A$ e $L(H) = B$. Costruiamo una nuova CFG $I = (V_3,\Sigma_3,R_3,S_3)$ tali che $L(I) = A \cup B$:
* $V_3 = V_1 \cup V_2 \cup \{S_3\}$
* $\Sigma_3 = \Sigma_1 \cup \Sigma_2$
* $R_3 = R_1 \cup R_2 \cup \{S_3 \to S_1, S_3 \to S_2\}$
* $S_3 =$ nuovo **start symbol** che non occorre in $V_1 \cup V_2$.
*Nota*: questa soluzione è corretta solo per $V_1 \cap V_2 = \emptyset$. Posso tuttavia assumerlo senza perdita di generalità.
## Esercizio 2
* Usare i linguaggi $A = \{a^mb^nc^n\ |\ m,n \geq 0\}$ e $B = \{a^mb^mc^n\ |\ m,n \geq 0\}$ per dimostrare che la classe dei CFL non è chiusa rispetto a $\cap$.
* Usare tale risultato per dimostrare che non è chiusa rispetto al complemento.

Osserviamo che sia $A$ che $B$ sono CFL.
Assumiamo per assurdo che la classe dei CFL sia chiusa rispetto a $\cap$, quindi $A \cap B$ è CFL.
$$A \cap B = \{a^nb^nc^n\ |\ n \geq 0\}$$ che abbiamo dimostrato essere non CFL perché non rispetta il pumping lemma.

Dimostriamo ora il secondo punto. Assumiamo per assurdo che valga la chiusura rispetto al complemento. Consideriamo due CFL $C$ e $D$. Osserviamo che:
* $\overline{C}$ e $\overline{D}$ sono CLF per chiusura rispetto al complemento.
* $\overline{C} \cup \overline{D}$ è CFL per chiusura rispetto ad unione.
* $\overline{\overline{C} \cup \overline{D}}$  è CFL per chiusura rispetto al complemento.
* $\overline{\overline{C} \cup \overline{D}} = \overline{\overline{C}} \cap \overline{\overline{D}} = C \cap D$ che è assurdo.
## Esercizio 3
Costruire un PDA per il linguaggio $\{a^ib^jc^k\ |\ i,j,k \geq 0 \land i+j \leq k\}$. Costruire poi una CFG per tale linguaggio.
$
**PDA**:
![[Pasted image 20241029144303.png]]

**Idea per CFG**: generiamo stringhe della forma $a^ib^jc^k$ con $k = i+j$ e aggiungiamo un numero arbitrario di $C$ in coda:
$$S \to AC$$$$C \to cC\ |\ \epsilon$$$$A \to aAc\ |\ B$$$$B \to bBc\ |\ \epsilon$$
## Esercizio 4
Costruire una CFG per l'insieme delle stringhe su $\Sigma = \{a,b\}$ con $|a| \geq |b|$. Si noti che questo linguaggio è diverso da $\{a^nb^m\ |\ n > m\}$ poiché le $a$ non devono necessariamente stare prima delle $b$.

**Idea per CFG**: costruiamo una CFG con due non-terminali $S$ e $T$. $T$ genera stringhe qualsiasi con un numero di $a$ maggiore uguale rispetto alle $b$. $S$ assicura di avere almeno una $a$ più delle $b$.
$$T \to aTb\ |\ bTa\ |\ a\ |\ \epsilon\ |\ TT$$$$S \to TaT$$
**Challenge 1**: dimostrare la correttezza.
**Challenge 2**: fare un PDA
## Esercizio 5
Sia $C$ un CFL e sia $R$ regolare. Dimostrare che $C \cap R$ è CFL.

Dato che $C$ è un CFL, allora esiste un PDA $P$ tale che $L(P) = C$.
Dato che $R$ è regolare, esiste un NFA $N$ tale che $L(N) = R$.

Costruisco un nuovo PDA $P'$ tale che $L(P') = C \cap R$.

**Idea**: $P'$ simula $P$ e $N$ in parallelo ed accetta se entrambi accettano.

**Dettagli**:
* Sia $P = (Q,\Sigma,\Gamma,\delta,q_0,F)$
* Sia $N = (Q',\Sigma,\delta',q_0',F')$.
* Sia $P' = (Q^",\Sigma,\Gamma,\delta^",q_0^",F^")$ dove:
	* $Q^" = Q \times Q'$
	* $\delta^" : Q^" \times \Sigma \times \Gamma \to \mathbb{P}(Q^" \times \Gamma) \implies \delta^"((q,q'),a,s) = \{(\hat{q},\hat{q}'\ |\ t)\ |\ (\hat{q},t) \in \delta(q,a,s) \land \hat{q}' \in \delta'(q',a)\}$
	* $q_0^" = (q_0,q')$
	* $F^" = F \times F'$
## Esercizio 6
Dimostrare che $C = \{0^n1^n0^n1^n\ |\ n \geq 0\}$ non è CFL.

Assumiamo per assurdo che $C$ sia CFL, allora deve valere il pumping lemma.
Sia $p$ la pumping length di $C$ e consideriamo la stringa $s = 0^p1^p0^p1^p$.
Sia $s = uvxyz$ con $|vy| > 0$ e $|vxy| \leq p$. Dimostriamo che $s$ non può essere pompata arrivando ad un assurdo.

* **Caso 1**: $v$ oppure $y$ contengono sia $0$ che $1$. In questo caso $uv^2xy^2z \notin C$ perché contiene dei simboli in ordine sbagliato.
* **Caso 2**: sia $v$ che $y$ contengono un solo tipo di simbolo. Sfruttiamo $|vxy| \leq p$:
	* **Caso 2.1**: $vxy$ tocca un solo blocco, per esempio il primo. Allora $uv^2xy^2z = 0^{p+k}1^p0^p1^p$ con $k > 0$ che non sta in $C$.
	* **Caso 2.2**: $vxy$ sta a cavallo fra due blocchi, per esempio i primi 2. Allora $uv^2xy^2z = 0^{p+k}1^{p + j}0^p1^p$ con $k > 0$ e $j > 0$ che non sta in $C$.

# Macchine di Turing
Una **macchina di Turing** (MdT) è un **modello teorico** di un calcolatore, con *memoria infinita* ed *utilizzabile in maniera arbitraria*.

**DFA** $\to$ memoria finita.
**PDA** $\to$ memoria infinita, ma in forma di stack.

**MdT**:
* *Stato interno*
* *Nastro infinito*
* *Testina*
![[Pasted image 20241030142219.png]]

**Differenze rispetto a DFA/PDA**:
* L'input è sul nastro e viene sia letto che scritto
* La testina può essere spostata sia a sinistra che a destra
* Memoria (nastro) infinita
* ACCETTO o RIFIUTO un input non appena entro in uno stato di accettazione o rifiuto
## Esempio di MdT
Definizione di MdT per il seguente linguaggio: $\{w\#w\ |\ w \in \{0,1\}^*\}$ (non CFL, ma riconoscibile da una MdT):
![[Pasted image 20241030142159.png]]

**Passi di esecuzione**:
* Fai zig-zag fra posizioni corrispondenti a sinistra e a destra di $\#$ per verificare che essere contengano lo stesso simbolo. Se non è così o non trovi $\#$: RIFIUTA. Altrimenti sostituisci con $\times$ i simboli corrispondenti.
* Quando hai controllato tutti i simboli di a sinistra di $\#$, verifica se ci sono simboli rimanenti a destra di $\#$. in tal caso RIFIUTA, altrimenti ACCETTA.
## Definizione formale di MdT
Una MdT è una settupla $(Q,\Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$ dove:
* $Q$ è un insieme finito di stati.
* $\Sigma$ è un alfabeto finito di input, tale che $\sqcup\text{(blank)} \notin \Sigma$.
* $\Gamma$ è un alfabeto finito per il nastro, tale che $\sqcup \in \Gamma$ e $\Sigma \subseteq \Gamma$.
* $\delta: Q \times \Gamma \to Q \times \Gamma \times \{L,R\}$ è la funzione di transizione.
* $q_0 \in Q$ è lo stato iniziale.
* $q_{accept} \in Q$ è lo stato di accettazione.
* $q_{reject} \in Q$ è lo stato di rifiuto ($q_{reject} \neq q_{accept}$).
## Come computa una MdT?
Una **configurazione** di una MdT descrive un momento della computazione per mezzo di tre parametri:
* **Stato interno**
* **Contenuto del nastro**
* **Posizione della testina**
![[Pasted image 20241030144109.png]]

In maniera compatta possiamo riscrivere questo esempio come: $001q_301$.
In generale una configurazione ha la forma $uqv$, dove $u,v \in \Gamma^*$ e $q \in Q$. 

Una MdT computa passando da una configurazione a quella successiva sulla base di quanto è definito da $\delta$.
## Regole di computazione
* Sia $M$ nella configurazione $uaq_ibv$ e sia $\delta(q_i,b) = (q_j,c,L)$ (dove $L$ sta per *left*), allora la prossima configurazione sarà $uq_jacv$.
* Sia $M$ nella configurazione $uaq_ibv$ e sia $\delta(q_i,b) = (q_j,c,R)$ (dove $R$ sta per *right*), allora la prossima configurazione sarà $uacq_jv$.
* Sia $M$ nella configurazione $q_ibv$ e sia $\delta(q_i,b) = (q_j,c,L)$, allora la prossima configurazione è $q_jcv$.
* Sia $M$ nella configurazione $q_ibv$ e sia $\delta(q_i,b) = (q_j,c,R)$, allora la prossima configurazione è $cq_jv$.

*Nota*: la testina non potrà mai essere all'estremità destra del nastro, poiché il nastro è infinito a destra.
## Condizioni di accettazione e di rifiuto
Una MdT accetta un input $w$ $\iff$ esistono delle configurazioni $c_1,c_2,...,c_k$ tali che:
* $c_1$ è la configurazione iniziale ($q_0w$).
* $c_k$ è una configurazione accettante $uq_{accept}v$ per qualche $u,v \in \Gamma^*$.
* Per ogni $i$, $c_i$ passa in $c_{i+1}$ secondo le regole di computazione date.

*Nota*: Visto che $q_{accept}$ fa terminare con accettazione e vogliamo che $q_{reject}$ termini con un rifiuto, la funzione di transizione (più precisamente) ha tipo $Q - \{q_{accept},q_{reject}\} \times \Gamma \to Q \times \Gamma \times \{L,R\}$.
## Linguaggi riconosciuti da MdT
Un linguaggio $A$ si dice **Turing-riconoscibile** (TR) $\iff$ esiste una MdT $M$, tale che $L(M) = A$.

Dato un input $w$, una MdT $M$ ha solo tre **possibili comportamenti**:
* $M$ accetta $w$.
* $M$ rifiuta $w$.
* $M$ va in loop quando eseguita su $w$.

Una macchina di Turing che non va mai in loop su nessun input si dice **decisore**.
Di conseguenza un linguaggio $A$ si dice **decidibile** $\iff$ esiste un decisore $M$ tale che $L(M) = A$.
## Esempio 1
$C = \{w\#w\ |\ w \in \{0,1\}^*\}$. Diamo una MdT $M$ tale che $L(M) = C$. 

![[Pasted image 20241030152133.png]]
## Esempio 2
Si definisca una MdT per $\{0^{2^n}\ |\ n \geq 0\}$ .

**Idea**: ogni passata sul nastro cancellerà metà degli $0$ presenti.

Su input $w$:
* Scorri il nastro da sinistra a destra cancellando uno $0$ si e uno $0$ no
	* Se tale passata ha trovato un solo $0$ **accetta**
	* Se tale passata ha trovato una quantità dispari ($> 1$) di $0$ **rifiuta**
* Riavvolgi il nastro a sinistra e riparti dallo step $1$.
## Varianti delle MdT
* MdT con *stay*, cioè la testina non è costretta a sinistra e destra ma può anche stare ferma. In questo caso $\delta$ diventa:
$$\delta: Q \times \Gamma \to Q \times \Gamma \times \{L,R,S \}$$
* MdT multi-nastro ($k \geq 1$ nastri):
	* Riceve input sul primo nastro.
	* Quando computa:
		* Legge da $k$ nastri.
		* Modifica $k$ nastri.
		* Sposta $k$ testine.
	$\delta$ diventa: 
$$\delta: Q \times \Gamma^k \to Q \times \Gamma^k \times \{L,R,S\}^k$$
![[Pasted image 20241105141151.png]]
## Teorema
Ogni MdT multi-nastro può essere convertita in una MdT a singolo nastro ad essa equivalente.
## Dimostrazione
**Idea**:
![[Pasted image 20241105142132.png]]

**Dimostrazione**: partiamo da una MdT multi-nastro e la convertiamo in una MdT singolo nastro come segue:
* $S =$ su input $w = w_1w_2...w_n$:
	* Metti il nastro nella forma $\#\dot{w_1}w_2w_3\#\dot{\sqcup}\#\dot{\sqcup}\#...\#\dot{\sqcup}\#$
	* Scorri il nastro leggendo i simboli col pallino e salvali nel tuo stato. Scorri poi nuovamente il nastro per aggiornare i simboli con pallino e per spostare i pallini secondo la funzione di transazione della MdT multi-nastro.
	* Se in un qualche momento sposti un pallino sopra ad un $\#$ fai *shift a destra* di una posizione per l'intero contenuto del nastro
## MdT non deterministica
La funzione $\delta$ di una MdT non deterministica è: $$\delta: Q \times \Gamma \to \mathbb{P}(Q \times \Gamma \times \{L,R\})$$
## Teorema
Ogni MdT non deterministica si può convertire in una MdT equivalente.
**Idea**: ragioniamo su una computazione non-deterministica come se essa fosse un *albero* di possibili computazioni. Descriviamo un possibile cammino di questo albero con un *indirizzo*.
![[Pasted image 20241105144139.png]]

Proviamo ad enumerare tutti i possibili indirizzi eseguendo una computazione deterministica per ciascuno di essi. Otteniamo nel nostro caso $11,\ 12,\ 21,\ 31$. Se una di queste accetta dobbiamo accettare anche noi. In questo caso l'albero è finito. Se l'albero è infinito non possiamo pre-computare tutti i percorsi, pertanto li enumereremo facendo una visita in ampiezza e non in profondità. Otteniamo quindi nel nostro caso: $1,\ 2,\ 3,\ 11, \ 12,\ 21 ...$ 

**Dimostrazione**: simuliamo la MdT non-deterministica con una MdT deterministica con $3$ nastri. Cosa fanno i $3$ nastri?
* Nastro *read only* che contiene l'input iniziale.
* Nastro *di lavoro* in cui eseguiamo una computazione deterministica sull'input iniziale.
* Nastro *degli indirizzi* che enumera i possibili modi per attraversare l'albero del non-determinismo.

Descriviamo la MdT con tre nastri:
* Inizializza il primo nastro con l'input $w$, il secondo nastro è vuoto, il terzo non è vuoto.
* Copia il primo nastro sul secondo.
* Simula una computazione deterministica sul secondo nastro, risolvendo il non-determinismo tramite l'indirizzo sul terzo nastro. Se accetta: **accept**.
* Aggiorna il terzo nastro con il prossimo indirizzo secondo l'ordine menzionato e torna allo step $2$.
## Enumeratori
![[Pasted image 20241105150916.png]]
## Differenze con MdT
* **MdT**:
	* La MdT è un *riconoscitore*.
	* Riceve input sul nastro e decide se accettare o no.
	* Linguaggio = insieme delle stringhe accettate.
* **Enumeratore**:
	* L'enumeratore è un *generatore*.
	* Non riceve alcun input, ma accumula caratteri nel buffer della stampante.
	* Linguaggio = insieme delle stringhe che stampa.
## Teorema
Un linguaggio è **Turing-riconoscibile** (**T.R.**) $\iff$ esiste un enumeratore che lo genera. In altre parole MdT ed enumeratori hanno lo stesso potere espressivo.
## Dimostrazione
* $\implies$ Sia $A$ un linguaggio T.R., dimostro che esiste un enumeratore $E$ tale che $L(E) = A$.
  Visto che $A$ è T.R, esiste una MdT $M$ tale che $L(M) = A$. Costruiamo un enumeratore $E$ tale che $L(E) = A$.
	* *Dimostrazione errata*:
		* $E$ = per tutte le stringhe $s_1,s_2,s_3 ...$
			* Esegui $M$ su $s_i$.
			* Se $M$ accetta: stampa $s_i$.
		 Il  problema in questo caso è che se $M$ va in loop sulla stringa $s$, essa non verrà mai stampata.
	* *Dimostrazione corretta*:
		* $E$ = per tutti gli $i = 0,1,2,3,4,...$
		* Genera $s_1,s_2,...,s_i$.
		* Testa $M$ su $s_1,...,s_i$ per $i$ passi di computazione.
		* Se $M$ accetta qualche $s_j$, stampala.
![[Pasted image 20241105152821.png]]
* $\impliedby$ Dimostro che, se esiste un enumeratore $E$, tale che $L(E) = A$, allora $A$ è T.R.
	* $M =$ su input $w$
		* Simula l'enumeratore $E$.
		* Ogni volta che $E$ stampa una stringa $v$, verifica se $v = w$.
		*  Se $v = w$ **accept**, altrimenti torna allo step $1$.
## Tesi di Church-Turing
La definizione "intuitiva" di algoritmo coincide con la classe degli algoritmi implementabili da una MdT.
## Problema delle radici intere di un polinomio (10° problema di Hilbert)
Il 10° problema di Hilbert è il seguente:
> Definire un algoritmo che, dato un polinomio, per esempio $x^2-y^2$, determina se esso ammette o meno meno una radice intera (cioè una sostituzione delle sue variabili con dei valori interi che lo facciano valutare $0$).

Si può dimostrare che tale algoritmo *non esiste*!
## Semplificazione del 10° problema di Hilbert
Il problema semplificato è il seguente:
> Determinare se un polinomio nella sola variabile $x$ ha una radice intera.

Definiamo il linguaggio $A$ per il seguente problema, dove :$$A = \{<p>\ |\ p\ \text{è un polinomio in }x\ \text{con una radice intera}\}$$
In altre parole $p$ ha una radice intera $\iff <p> \in A$, dove $<^.>$ è una funzione che trasforma polinomi nella loro rappresentazione come stringa.

Per esempio possiamo rappresentare $<3x^2-5x-3>\ =\ ^"3|-5|+3^"$

Il nostro problema ammette soluzione algoritmica $\iff$ $A$ è **decidibile** (= tale linguaggio è riconoscibile da un decisore).
## Costruiamo un decisore per il linguaggio $A = A = \{<p>\ |\ p\ \text{è un polinomio in }x\ \text{con una radice intera}\}$
Costruiamo la macchina $M$ per riconoscere il linguaggio $A$:
* $M =$ su input $<p>$:
	* Per tutti gli $x = 0,1,-1,2,-2,3,-3,...$
		* Calcola il valore $p(x)$.
		* Se $p(x) = 0$, ritorna **accept**.

$M$ *non* è un decisore perché non rifiuta mai, può andare in loop quando non trova una soluzione.
$M$ dimostra che $A$ è **T.R.**, ma non **decidibile**.

Possiamo modificare $M$ in modo tale che rifiuti sotto determinate condizioni:
* $M' =$ su input $<p>$:
	* Per tutti gli $x = 0,1,-1,2,-2,3,-3,...$ fino ad un determinato *limite*
		* Calcola il valore $p(x)$.
		* Se $p(x) = 0$, ritorna **accept**.
	* Se non hai trovato una radice intera, ritorna **reject**.

Si può infatti dimostrare che la radice intera, se esiste, è compresa fra: $-k \cdot \frac{C_{max}}{C_1}$ e $+k \cdot \frac{C_{max}}{C_1}$ dove $k$ è il numero di termini, $C_{max}$ è il coefficiente di massimo valore assoluto e $C_1$ è il coefficiente di grado massimo.
## Recap sulle MdT
Finora abbiamo visto $3$ modi per descrivere le MdT:
* **Formale**: $(Q,\Sigma,\Gamma,\delta,q_0,q_{accept},r_{reject})$
* **Implementativo**: "scrivi il nastro finché vedi $0$, poi torna all'inizio del nastro..."
* **Ad alto livello**: "per ogni $x = 1,-1,2,-2,...$ calcola $p(x)$"

 Quando descriviamo una MdT ad alto livello stiamo sostanzialmente utilizzando la tesi di Church-Turing.
## Esercizio 1 (Definizione formale di Enumeratore)
Dare una definizione formale di enumeratore e del linguaggio che genera.

 Un enumeratore è una settupla ($Q,\Sigma,\Gamma,\delta,q_0,q_p,q_h$) dove:
 * $Q$ è un insieme finito di stati.
 * $\Sigma$ è l'alfabeto finito per la stampa.
 * $\Gamma$ è l'alfabeto finito del nastro ($\sqcup \in \Gamma$).
 * $q_0$ è lo stato iniziale.
 * $q_p$ è lo stato di stampa.
 * $q_h$ è lo stato di terminazione.
 * $\delta: Q \times \Gamma \to Q \times \Gamma \times \{L,R\} \times \Sigma_\epsilon$

Una **configurazione** per un enumeratore è una coppia $(uqv,w)$, dove:
* $u \in \Gamma^*$.
* $q \in Q$.
* $v \in \Gamma^*$.
* $w \in \Sigma^*$.

Possiamo definire come una configurazione evolve nella successiva:
* Assumiamo che la configurazione corrente sia $(uaq_ibv,w)$ e sia $\delta(q_i,b) = (q_j,c,L,d)$, allora la prossima configurazione è $(uq_jacv, wd)$.
* Analogo per spostamento della testina a destra.
* Analogo all'estremità sinistra del nastro.
* Assumiamo che la configurazione corrente sia $(uq_pvw)$, allora la prossima configurazione è $(q_0uv, \epsilon)$.

Pertanto il linguaggio di un enumeratore è: $$L(E) = \{w \in \Sigma^*\ |\ \exists u,v \in \Gamma^*: (u,q_p,v,w) \text{ è raggiungibile da } (q_0,\epsilon)\}$$
## Esercizio 2
Dimostrare che la classe dei linguaggi T.R. è chiusa rispetto alle seguenti operazioni:

>**Unione**: se $A$ e $B$ sono T.R., allora $A \cup B$ è T.R.

Visto che $A$ e $B$ sono T.R., esistono MdT $M$ ed $N$ tali che $L(M) = A$ ed $L(N) = B$.

Vediamo una prima idea *sbagliata* di dimostrazione:
* Su input $w$:
	* Simula $M$ su $w$.
		* Se $M$ accetta: **accept**.
		* Se $M$ rifiuta: simula $N$ su $w$ e ritorna il suo output.

Tale soluzione è chiaramente sbagliata, visto che $M$ potrebbe non terminare mai.

Vediamo ora una seconda idea che sfrutta  una MdT non deterministica:
* Su input $w$:
	* Scegli in modo non deterministico se simulare $M$ o $N$ su $w$.
	* Se una delle due accetta: **accept**.

Vediamo infine una terza idea che utilizza una MdT con due nastri:
* Su input $w$:
	* Copia $w$ sul secondo nastro.
	* Simula $M$ su $w$ sul primo nastro per un passo di computazione.
	* Simula $N$ su $w$ sul secondo nastro per un passo di computazione.
	* Se $M$ o $N$ accettano: **accept**.

*Nota*: il loop infinito è equivalente a **reject**.

>**Intersezione**: se $A$ e $B$ sono T.R., allora $A \cap B$ è T.R.

Visto che $A$ e $B$ sono T.R., esistono MdT $M$ ed $N$ tali che $L(M) = A$ ed $L(N) = B$.

Costruisco la seguente MdT:
* Su input $w$:
	* Simula $M$ su $w$.
	* Se $M$ accetta: simula $N$ su $w$ e ritorna il suo output.
	* Se $M$ rifiuta: **reject**.

> **Concatenazione**: se $A$ e $B$ sono T.R., allora $A _° B$ è T.R.

Visto che $A$ e $B$ sono T.R., esistono MdT $M$ ed $N$ tali che $L(M) = A$ ed $L(N) = B$.

Costruiamo la seguente MdT:
* Su input $w$:
	* Spezza $w$ in $w_1w_2$ *non deterministicamente*:
	* Testa $M$ su $w_1$, se accetta simula $N$ su $w_2$. 
	*  Se $N$ accetta: **accept**.

>Star: se $A$ è T.R., allora $A ^* $ è T.R.

*Nota*: i linguaggi **decidibili** sono chiusi rispetto a $\cup,\ \cap,\ _°$ e $^*$. Essi inoltre sono chiusi anche rispetto al **complemento**. 
*Nota*: i T.R. non sono chiusi rispetto al complemento.
# Decidibilità
## Problemi decidibili
**Problema**: Determinare se un DFA $D$ accetta una stringa $w$.
**Linguaggio**: $A_{DFA} = \{<M,w>\ |\ M\text{ è DFA e } M \in L(M)\}$.

**Teorema**: $A_{DFA}$ è decidibile.

**Dimostrazione**: 
Costruisco un decisore $N$ tale che $L(N) = A_{DFA}$.
* $N =$ su input $<M,w>:$
	* Simuliamo il DFA $M$ su input $w$.
	* Se $M$ termina in uno stato di accettazione: **accept**.
	* Se $M$ termina in uno stato non di accettazione: **reject**.

**Problema**: Determinare e un NFA $N$ accetta una stringa $w$.
**Linguaggio**: $A_{NFA} = \{<N,w>\ |\ N \text{è un NFA e } w \in L(N)\}$.
**Teorema**: $A_{NFA}$ è decidibile.

**Dimostrazione 1**:
Costruisco una MdT non deterministica $M$ fatta come segue:
* $M =$ su input $<N,w>$:
	* Simulo $N$ su $w$ in modo non deterministico.
	* Se $N$ accetta: **accept**.
	* Se $N$ rifiuta: **reject** in questo ramo del non determinismo.

**Dimostrazione 2**:
Costruisco una MdT "tradizionale" $M$ fatta come segue:
* $M =$ su input $<N,w>$:
	* Converto $N$ in un DFA $D$ ad esso equivalente.
	* Esegui il decisore per $A_{DFA}$ su input $<D,w>$.
	* Ritorna il suo output.

*Nota*: in generale si può usare un decisore per creare altri decisori, come abbiamo fatto qui sopra.

*Nota*: si può dimostrare che anche il linguaggio $A_{REX} = \{<R,w>\ |\ R \text{ è regexp e } w \in L(R)\}$ è decidibile.

**Problema**: Dato un DFA, determinare se esso non accetta nessuna stringa.
**Linguaggio**: $E_{DFA} = \{<D>\ |\ D \text{ è un DFA e } L(D) = \emptyset\}$

**Teorema**: $E_{DFA}$ è decidibile.

**Dimostrazione**: Costruiamo un decisore $M$ per $E_{DFA}$:
* $M =$ su input $<D>$:
	* Marca lo stato iniziale di $D$.
	* Finché è possibile marcare nuovi stati:
		* Marca gli stati con una transizione in entrata da stati già marcati.
	* Se ho marcato almeno uno stato accettante: **reject**, altrimenti **accept**.


**Problema**: Dati due DFA $D_1$ e $D_2$, determinare se riconoscono lo stesso linguaggio.
**Linguaggio**: $EQ_{DFA} = \{<D_1,D_2>\ |\ D_1,D_2 \text{ sono DFA e } L(D_1) = L(D_2)\}$.

**Teorema**: $EQ_{DFA}$ è decidibile.

**Dimostrazione**:
Osserviamo che $L(D_1) = L(D_2) \iff$
* Tutte le stringhe di $L(D_1)$ stanno anche in $L(D_2)$.
* Tutte le stringhe di $L(D_2)$ stanno anche in $L(D_1)$. 

In alte parole:
* Non esiste una stringa di $L(D_1)$ tale che essa non stia in $L(D_2)$.
* Non esiste una stringa di $L(D_2)$ tale che essa non stia in $L(D_1)$.

Ovvero: $$L(D_1) = L(D_2) \iff (L(D_1) \cap \overline{L(D_2)}) \cup (\overline{L(D_1)} \cap L(D_2)) = \emptyset$$
Costruiamo un decisore $M$ per $EQ_{DFA}$:
* $M =$ su input $<D_1,D_2>$:
	* Costruisci un nuovo DFA $D$ tale che $L(D) = (L(D_1) \cap \overline{L(D_2)}) \cup (\overline{L(D_1)} \cap L(D_2))$.
	  Ciò è possibile perché la classe dei linguaggi regolari è chiusa rispetto a complemento, $\cap$ e $\cup$.
	  * Esegui il decisore per $E_{DFA}$ su $<D>$.
	  * Ritorna il suo output.
## Problemi su linguaggi context-free
**Problema**: determinare se una CFG $G$ genera una certa stringa $w$.
**Linguaggio**: $A_{CFG} = \{<G,w>\ |\ G \text{ è una CFG e } w \in L(G)\}$.

**Teorema**: $A_{CFG}$ è decidibile.

**Lemma**: Se $H$ è una CFG in *forma normale di Chomsky* e $w$ è una stringa di lunghezza $n$, allora se $w \in L(H)$ è possibile trovare una derivazione di $w$ che ha $2n-1$ passi. (Caso speciale: per $n = 0$ basta un passo).

**Dimostrazione**:
Costruiamo un decisore $M$ per $A_{CFG}$:
* $M =$ su input $<G,w>$:
	* Converti $G$ in *forma normale di Chomsky* (output = $H$).
	* Prova tutte le derivazioni di $2n-1$ passi dove $n = |w|$.
	  Se $n = 0$ prova solo le derivazioni di un passo.
	  * Se una di esse genera $w$: **accept**, altrimenti: **reject**.

**Domanda**: perché vale il lemma?
Ricordiamo le condizioni su di Chomsky:
* $A \to BC$ dove $B,C \neq S$
* $A \to a$
* $S \to \epsilon$
Quelli sopra riportati sono i tre tipi di produzioni ammessi da Chomsky.
CONTINUARE A CASA

**Problema**: Data una CFG $G$, determinare se essa non accetta nessuna stringa.
**Linguaggio**: $E_{CFG} = \{<G>\ |\ G \text{ è una CFG e } L(G) = \emptyset\}$

**Teorema**: $E_{CFG}$ è decidibile.

**Idea**:
$$S \to A\ |\ B$$ $$A \to \underline{a}A\ |\ \underline{a}$$ $$B \to \underline{b}B$$
Abbiamo sottolineato i terminali, a questo punto sottolineiamo $A$ perché genera solo terminali, ed $S$ perché genera $A$:
$$\underline{S} \to \underline{A}\ |\ B$$ $$\underline{A} \to \underline{a}\underline{A}\ |\ \underline{a}$$ $$B \to \underline{b}B$$
Così abbiamo la certezza che da $S$ vengono generate stringhe non vuote.

**Dimostrazione**
Costruisco un decisore per $E_{CFG}$:
* $M =$ su input $w$:
	* Sottolineo tutti i terminali di $G$ nelle sue produzioni.
	* Finché è possibile sottolineare non-terminali:
		* Sottolinea i non-terminali $A$ tali che esista una produzione $w_1,...,w_n$ dove tutti i $w_i$ sono sottolineati.
	* Se ho sottolineato lo start symbol: **reject**, altrimenti: **accept**.
## Teorema
Ogni linguaggio context-free è decidibile
## Dimostrazione
Sia $A$ un linguaggio context-free. Allora esiste una CFG $G$ tale che $L(G)  = A$.
Dimostriamo che esiste un decisore $M$ tale che $L(M) = A$.
* $M=$ su input $w$:
	* Esegui il decisore per $A_{CFG}$ su input $<G,w>$.
	* Ritorna il suo output.

# Indecidibilità
Obbiettivi:
* Dimostriamo che esistono linguaggi non decidibili.
* Diamo uno specifico esempio di linguaggio non decidibile.
## Recap
Sia $f: A \to B$ una funzione:
* $f$ è **iniettiva** $\iff$ $x \neq y$ implica $f(x) \neq f(y)$.
* $f$ è **suriettiva** $\iff \forall y \in B\ \exists x \in A\ |\ f(x) = y$.
* $f$ è **biettiva** $\iff$ $f$ è iniettiva e suriettiva.

Due insiemi $A$ e $B$ hanno la stessa cardinalità $\iff \exists f: A \to B$ biettiva.
## Esempio
L'insieme dei naturali $\mathbb{N}$ e l'insieme dei naturali pari hanno la stessa cardinalità.

Costruiamo una biezione da $\mathbb{N}$ ai naturali pari: $$f(n) = 2n$$
## Insieme numerabile
Un insieme si dice **numerabile** $\iff$:
* è **finito**.
* Ha la **stessa cardinalità** di $\mathbb{N}$.
## Esempio
L'insieme dei razionali positivi è numerabile.

**Dimostrazione**:

|     | $1$               | $2$               | $3$               | $4$           | $5$           | ... |
| --- | ----------------- | ----------------- | ----------------- | ------------- | ------------- | --- |
| $1$ | ==$\frac{1}{1}$== | ==$\frac{1}{2}$== | ==$\frac{1}{3}$== | $\frac{1}{4}$ | $\frac{1}{5}$ | ... |
| $2$ | ==$\frac{2}{1}$== | $\frac{2}{2}$     | $\frac{2}{3}$     | $\frac{2}{4}$ | $\frac{2}{5}$ | ... |
| $3$ | ==$\frac{3}{1}$== | $\frac{3}{2}$     | $\frac{3}{3}$     | $\frac{3}{4}$ | $\frac{3}{5}$ | ... |
| $4$ | $\frac{4}{1}$     | $\frac{4}{2}$     | $\frac{4}{3}$     | $\frac{4}{4}$ | $\frac{4}{5}$ | ... |
| $5$ | $\frac{5}{1}$     | $\frac{5}{2}$     | $\frac{5}{3}$     | $\frac{5}{4}$ | $\frac{5}{5}$ | ... |
| ... | ...               | ...               | ...               | ...           | ...           | ... |
**Obbiettivi**:
Dare una biezione da $\mathbb{N}$ ai razionali positivi, cioè produrre una lista di razionali positivi tale che:
* Non vi siamo ripetizioni
* Tutti i razionali positivi vi siano rappresentati

Procedendo lungo le diagonali ed eliminando i duplicati, troviamo una biezione fra $\mathbb{N}$ e i razionali positivi che rispetta gli obbiettivi.
## Dimostrazione di Cantor
**Teorema**: $\mathbb{R}$ non è numerabile.

**Dimostrazione**:

| $n$ | $f(n)$      |
| --- | ----------- |
| $1$ | $3.140$     |
| $2$ | $5.623$     |
| $3$ | $17.152$    |
| $4$ | $1.18927$   |
| $5$ | $3.5555655$ |
| ... | ...         |
Usa la tecnica della **diagonalizzazione**. Assumiamo per assurdo che $\mathbb{R}$ sia numerabile. Deve allora esistere una biezione fra $\mathbb{N}$ ed $\mathbb{R}$. Chiamiamola $f$. Costruiamo un numero reale che non occorre nel codominio di $f$ (la parte destra della tabella), arrivando ad un *assurdo*. Il nostro numero è: $$0.57838...$$
Esso differisce dall'i-esimo reale nell'i-esima cifra dopo la virgola, quindi è diverso da tutti i numeri nella tabella.
## Teorema
Esistono dei linguaggi che non sono T.R.
## Dimostrazione
La dimostrazione sfrutta un'osservazione sulla cardinalità, cioè dimostriamo che ci sono più linguaggi che MdT:

* *Dimostriamo che l'insieme delle MdT è numerabile*. 
	Per farlo osserviamo che l'insieme delle stringhe costruite su qualsiasi alfabeto $\Sigma$ finito è numerabile.
	Vediamo per esempio: $\Sigma = \{0,1\}$

| $1$        | $2$ | $3$ | $4$  | $5$  | $6$  | $7$  | $8$   | ... |
| ---------- | --- | --- | ---- | ---- | ---- | ---- | ----- | --- |
| $\epsilon$ | $0$ | $1$ | $00$ | $01$ | $10$ | $11$ | $000$ | ... |
	Enumerare le stringhe per lunghezza crescente mi da una biezione con $\mathbb{N}$.
	Qualsiasi MdT $(Q,\Sigma,\Gamma,\delta,q_0,q_{accept},q_{reject})$ è rappresentabile come una stringa. Le MdT sono un sottoinsieme delle stringhe, e quindi sono numerabili.

* *Dimostriamo che l'insieme dei linguaggi non è numerabile*:
	Osserviamo che qualsiasi linguaggio si può rappresentare come una stringa binaria **infinita**.
	$$L = \{0,00,01\}$$

|                |            |     |     |      |      |      |      |       |       |
| -------------- | ---------- | --- | --- | ---- | ---- | ---- | ---- | ----- | ----- |
| **Stringhe**   | $\epsilon$ | $0$ | $1$ | $00$ | $01$ | $10$ | $11$ | $000$ | $...$ |
| **Linguaggio** | $0$        | $1$ | $0$ | $1$  | $1$  | $0$  | $0$  | $0$   | $...$ |
	Osserviamo che l'insieme delle stringhe binarie infinite non è numerabile (dimostrazione per **diagonalizzazione**).
	Assumiamo per assurdo che l'insieme delle stringhe binarie infinite sia numerabile:

|     |          |
| --- | -------- |
| $1$ | $001100$ |
| $2$ | $11001$  |
| $3$ | $01100$  |
| $4$ | $10000$  |
| $5$ | $11100$  |
| $6$ | $...$    |
	Costruiamo una stringa binaria infinita che non compare nella tabella (**assurdo**): $$10011 ...$$
## Vediamo il nostro primo linguaggio non decidibile
Il primo linguaggio non decidibile che vedremo è quello relativo al problema dell'accettazione delle MdT.
$$A_{TM} = \{<M,w>\ |\ M \text{è MdT e } w \in L(M)\}$$

**Osservazione**: $A_{TM}$ è T.R, infatti possiamo costruire una MdT $N$ tale che $L(N) = A_{TM}$.

* $N =$ su input $<M,w>$:
	* Simula $M$ su $w$.
	* Ritorna il suo output.

*Nota*: questa macchina non è un decisore, potrebbe non terminare mai!

Dimostriamo ora che non esiste un decisore per $A_{TM}$.

**Teorema**: $A_{TM}$ è indecidibile.
**Dimostrazione**: Assumiamo per assurdo che $A_{TM}$ sia decidibile, allora esiste un decisore $H$ per $A_{TM}$.
$$H(<M,w>) = \begin{cases} \text{accept} \quad \text{se } M \text{ accetta } w \\ \text{reject}\ \quad \text{altrimenti} \end{cases}$$
Costruisco una nuova MdT $D$ definita come segue:
* $D=$ su input $<M>$:
	* Esegue $H$ su input $<M,<M>>$
	* Ritorna l'output invertito.
$$D(<M>) = \begin{cases} \text{accept} \quad \text{se } M \text{ non accetta } <M> \\ \text{reject}\ \quad \text{se } M \text{ accetta } <M>   \end{cases}$$
$$D(<D>) = \begin{cases} \text{accept} \quad \text{se } D \text{ non accetta } <D> \\ \text{reject}\ \quad \text{se } D \text{ accetta } <D>   \end{cases}$$

Siamo così arrivati ad un **assurdo** $\to$ $D(<D>)$ mi da il contrario di $D(<D>)$.
## Dietro le quinte...
La seguente tabella mostra le varie esecuzioni di $H(<M_i,<M_i>>)$ :

|       |          |          |          |          |       |            |
| ----- | -------- | -------- | -------- | -------- | ----- | ---------- |
|       | $<M_1>$  | $<M_2>$  | $<M_3>$  | $<M_4>$  | $...$ | $<D>$      |
| $M_1$ | accept   | accept   | reject   | accept   | $...$ | reject     |
| $M_2$ | reject   | accept   | reject   | accept   | $...$ | reject     |
| $M_3$ | reject   | reject   | reject   | reject   | $...$ | accept     |
| $M_4$ | accept   | accept   | accept   | accept   | $...$ | reject     |
| $...$ | $...$    | $...$    | $...$    | $...$    | $...$ | $...$      |
| $D$   | reject | reject | accept | reject | $...$ | **e qui?** |
In posizione $(D,<D>)$ arriviamo all'assurdo

**Recap**: $A_{TM}$ è T.R. ma non decidibile.
## Osservazione
$\overline{A_{TM}}$ non è T.R.
## Teorema
$A$ è decidibile $\iff$ sia $A$ che $\overline{A}$ sono T.R.
## Dimostrazione
* $\implies$ Sia  $A$ decidibile, dimostriamo che $A$ e $\overline{A}$ sono T.R.
	* Visto che $A$ è decidibile, esso è anche T.R.
	* Visto che $A$ è decidibile, anche $\overline{A}$ è decidibile, e quindi T.R.
* $\impliedby$ Assumiamo che sia $A$ che $\overline{A}$ siano T.R., allora abbiamo due MdT $M$ ed $N$ tali che $L(M) = A$ ed $L(N) = \overline{A}$. Costruiamo il seguente decisore per $A$: (con due nastri)
	* Su input $w$:
		* Simula $M$ su $w$ per un passo di computazione sul primo nastro.
			* Se $M$ accetta: **accetta**.
			* Se $M$ rifiuta: **reject**.
		* Simula $N$ su $w$ per un passo di computazione sul secondo nastro:
			* Se $N$ accetta: **reject**.
			* Se $N$ rifiuta: **accept**.
		* Torna al passo $1$.

*Nota*: da questa dimostrazione abbiamo concluso anche che la classe dei linguaggi T.R. non è chiusa rispetto al complemento.
## Problema 1
Sia $\Sigma$ un alfabeto finito. Dimostrare che "determinare se un DFA $D$ accetta tutte le stringhe su $\Sigma$" è un problema decidibile.
$$ALL_{DFA} = \{<D>\ |\ D \text{ è DFA e } L(D) = \Sigma^*\}$$
**Soluzione 1**:
Ci basiamo su $E_{DFA}$.
Costruiamo questo decisore per $ALL_{DFA}$:
* Su input $<D>$:
	* Costruisco un nuovo DFA $D'$ tale che $L(D') = \overline{L(D)}$.
	* Esegui il decisore per $E_{DFA}$ su $<D'>$.
	* Ritorno il suo output.

*Nota*: Posso applicare questa soluzione perché i linguaggi regolari sono chiusi rispetto al complemento (importante specificarlo all'esame).

**Soluzione 2**:
Ci basiamo su $EQ_{DFA}$.
Costruiamo il seguente decisore per $ALL_{DFA}$.
* Su input $<D>$:
	* Costruisco un nuovo DFA $D'$ tale che $L(D') = \Sigma^*$
	* Esegui il decisore per $EQ_{DFA}$ su $<D,D'>$.
	* Ritorna il suo output.

![[Pasted image 20241119143507.png]]
## Problema 2
Si consideri: $$\overline{E_{TM}} = \{<M>\ |\ M \text{ è MdT e } L(M) \neq \emptyset\}$$Dimostrare che esso è T.R.
Costruiamo una MdT $N$ tale che $L(N) = \overline{E_{TM}}$.

**Soluzione errata**:
* $N =$ su input $<M>$:
	* Per $i = 1,2,3,4, ...$
		* Esegui $M$ sulla stringa $s_i$.
		* Se $M$ accetta: **accept**

*Nota*: questa soluzione è sbagliata perché potremmo andare in loop infinito prima di accettare.

**Soluzione corretta**:
* $N =$ su input $<M>$:
	* Per $i = 1,2,3,4, ...$
		* Esegui $M$ su $s_1, ..., s_i$ per $i$ passi di computazione.
		* Se almeno una di tali computazioni accetta: **accept**.
## Problema 3
Si consideri: $$\{<R,S>\ | \ R,S \text{ sono regexp e } L(R) \subseteq L(S)\}$$
Dimostrare che esso è decidibile.

**Soluzione 1**:
Usiamo la seguente osservazione: 
	$L(R) \subseteq L(S) \iff$ tutte le stringhe di $L(R)$ stanno anche il $L(S)$, cioè non esiste una stringa di $L(R)$ che non stia in $L(S)$

* Su input $<R,S>$:
	* Convertiamo $R,S$ in DFA equivalenti $D_R,D_S$
	* Costruiamo un nuovo DFA $L(D'_S) = \overline{L(D_S)}$.
	* Costruiamo un nuovo DFA $D$ tale che $L(D_R) \cap L(D'_S)$.
	* Eseguiamo $E_{DFA}$ su $<D>$
	* Ritorna il suo output.

**Soluzione 2**:
Osserviamo che: $$L(R) \subseteq L(S) \iff L(R) \cap L(S) = L(R)$$
* Su input $<R,S>$:
	* Convertiamo $R,S$ in DFA equivalenti $D_R,D_S$.
	* Costruisco un nuovo DFA $D$ tale che $L(D) = L(D_R) \cap L(D_S)$.
	* Esegui il decisore per $EQ_{DFA}$ su $<D_R,D>$.
	* Ritorna il suo output.
## Problema 4
Data una CFG $G$ diciamo che una variabile $A$ è utilizzabile $\iff$ occorre nella derivazione di almeno una stringa $w \in L(G)$. Dimostrare che "determinare se una variabile è utilizzabile è decidibile".

**Esempio di variabile non utilizzabile**:
Nell'esempio seguente $B$ non è raggiungibile da $S$:
$$S \to A$$
$$A \to aA\ |\ a$$
$$B \to b$$
$$C \to B$$
**Esempio di variabile non utilizzabile**:
Nell'esempio seguente $A$ non è *generante*:
$$S \to A$$
$$A \to A$$

Possiamo dimostrare che le sole variabili non utilizzabili sono quelle che:
* Non sono raggiungibili dallo start symbol.
* Non generano stringhe di soli terminali.

**Idea**:
* Elimino le variabili non raggiungibili.
* Se sono raggiungibili e sono *generanti*: esse occorrono nella derivazione di qualche stringa, ovvero sono utilizzabili.


**Per chiudere**:
Dimostriamo che "determinare se una variabile è raggiungibile o generante" è decidibile:

**Raggiungibili**:
* Inizializzo $Reach = \{S\}$
* Finché è possibile estendere $Reach$:
	* Se ho una produzione nella forma $A \to v$ dove $A \in Reach$, inserisci le variabili di $v$ in $Reach$
* Ritorna $Reach$

**Generanti**:
* Inizializzo $Gen = \emptyset$.
* Se esiste una produzione $A \to v$ dove tutti i simboli di $v$ sono terminali o variabili in $Gen$, aggiungi $A$ a $Gen$.
* Itera finché possibile, poi ritorna $Gen$.
## Riduzione
>Intuitivamente diciamo che $A$ è riducibile a $B$ (indicato con $A \leq B$) quando una soluzione per $B$ ci consente di costruire una soluzione per $A$.

**Osservazioni**:
* Se $A \leq B$ e $B$ è *decidibile*, allora anche $A$ è *decidibile*.
* Se $A \leq B$ e $A$ è *indecidibile*, allora anche $B$ è *indecidibile* ($\to$ utile come tecnica di dimostrazione).
## Problema della fermata (Halting Problem)
$$HALT_{TM} = \{<M,w>\ |\ M \text{ è MdT che termina su input } w\}$$
**Teorema**: $HALT_{TM}$ è indecidibile.
**Dimostrazione**:
Dimostriamo che $A_{TM}$ è riducibile ad $HALT_{TM}$, cioè dimostriamo che, se avessimo un decisore per $HALT_{TM}$ allora potremmo costruire un decisore per $A_{TM}$ (Ciò è impossibile perché $A_{TM}$ è indecidibile).

Assumiamo di avere $N$ decisore per $HALT_{TM}$, costruisco il seguente decisore per $A_{TM}$:
* Su input $<M,w>$:
	* Esegui $N$ su input $<M,w>$.
	* Se $N$ rifiuta: **reject**.
	* Se $N$ accetta: simula $M$ su $w$ e ritorna il suo output. 
## Problema 2
Consideriamo ora il problema di determinare se il linguaggio di una MdT è vuoto.
$$E_{TM} = \{<M> \ |\ M \text{ è MdT e } L(M) = \emptyset\}$$
Tale linguaggio è **indecidibile**.

**Dimostrazione**:
Dimostriamo che $A_{TM}$ è riducibile a $E_{TM}$, cioè dimostriamo che se avessi un decisore $H$ per $E_{TM}$, allora potremmo costruire un decisore per $A_{TM}$ (impossibile).

**Soluzione sbagliata**:
Costruiamo il seguente decisore per $A_{TM}$
* Su input $<M,w>$:
	* Esegui il decisore per $E_{TM}$ su input $<M>$.
	* Se esso accetta: **reject**.
	* Se invece esso rifiuta: simulo $M$ su $w$ e ritorno il suo output.

L'ultimo passaggio potrebbe non terminare, quindi non ho costruito un decisore.

**Soluzione corretta**:
* Su input $<M,w>$:
	* Costruiamo una nuova MdT $N$ con la seguente proprietà:
		* $L(N) = \begin{cases} \text{NON VUOTO} \quad \text{se } M \text{ accetta } w \\ \text{VUOTO} \quad \text{altrimenti} \end{cases}$
		* Esegui il decisore per $E_{TM}$ su input $N$.
		* Se esso ritorna accept: **reject**.
		* Se invece esso ritorna reject: **accept**. 

Dobbiamo però costruire la MdT $N$:
* Su input $x$:
	* Se $x \neq w$: **reject**
	* Altrimenti: simula $M$ su $w$ e ritorna il suo output.
$$L(N) = \begin{cases} \{w\} \quad  \text{se } M \text{ accetta } w \\ \emptyset \quad \text{altrimenti}\end{cases}$$
## Problema 3
$$REG_{TM} = \{<M>\ |\ M \text{ è MdT e } L(M) \text{ è regolare}\}$$
Tale linguaggio è **indecidibile**.
**Dimostrazione**:
Dimostriamo che $A_{TM}$ è riducibile a $REG_{TM}$, cioè dimostriamo che, se avessimo un decisore $H$ per $REG_{TM}$, potremmo costruire un decisore per $A_{TM}$ (impossibile).

* Su input $<M,w>$:
	* Costruisci una nuova MdT $N$ tale che:
		* $L(N) = \begin{cases} \text{REGOLARE} \quad  \text{se } M \text{ accetta } w \\ \text{NON REGOLARE} \quad \text{altrimenti}\end{cases}$
	* Esegui il decisore su per $REG_{TM}$ su $<N>$.
	* Ritorno il suo output.

Costruiamo $N$:
* $N =$ su input $x$:
	* Se $x$ ha la forma $0^n1^n$ per qualche $n$: **accept**
	* Altrimenti: simula $M$ su $w$ e ritorna il suo output.

|                     |                       |                           |
| ------------------- | --------------------- | ------------------------- |
|                     | $x$ ha forma $0^n1^n$ | $x$ non ha forma $0^n1^n$ |
| $M$ accetta $w$     | accept                | accept                    |
| $M$ non accetta $w$ | accept                | reject                    |
|                     |                       |                           |
$$L(N) = \begin{cases} \Sigma^* \quad  \text{se } M \text{ accetta } w \\ \{0^n1^n \ \ n \geq 0\} \quad \text{altrimenti}\end{cases}$$
## Problema 4
$$EQ_{TM} = \{<M_1,M_2>\ |\ M_1,M_2 \text{ sono MdT e } L(M_1) = L(M_2)\}$$
Dimostriamo che questo problema è indecidibile.

**Dimostrazione**:
Dimostriamo per assurdo che, se $EQ_{TM}$ fosse decidibile, potremmo decidere $E_{TM}$, che è indecidibile. Sia $H$ l'ipotetico decisore per $EQ_{TM}$, costruiamo un decisore per $E_{TM}$ come segue:
* Su input $<M>$:
	* Costruisci una MdT $N$ tale che $L(N) = \emptyset$.
	* Eseguiamo $H$ su input $<M,N>$.
	* Ritorna il suo output.
Questo è assurdo perché $E_{TM}$ è indecidibile.
## Riduzioni basate su storie di computazione accettanti
Sia $M$ una MdT e sia $w$ una stringa. Una storia di computazione accettante per $M$ e $w$ è una sequenza di configurazioni della MdT $M$, tali che:
* la prima configurazione è la configurazione iniziale di $M$ su $w$.
* l'ultima configurazione è una configurazione accettante.
* Ogni configurazione discende dalla precedente (se ne ha una) secondo le regole di computazione di una MdT.

>$M$ accetta $w$ $\iff$ esiste una storia di computazione accettante per $M$ e $w$
## Automi linearmente limitati (LBA)

Un **LBA** è una MdT con un vincolo aggiuntivo: non può mai spostare la testina oltre la lunghezza del suo input iniziale.
*Esempio*: se l'input iniziale ha lunghezza $10$, un LBA opera con un nastro di $10$ celle.
## Problema 1
$$A_{LBA} = \{<M,w>\ |\ M \text{ è LBA e } w \in L(M)\}$$
Tale problema è decidibile ma prima di dimostrarlo abbiamo bisogno di un lemma.

**LEMMA**: Sia $M$ un LBA con $q$ stati e $g$ simboli possibili per il nastro. Se un nastro ha lunghezza $n$, il numero massimo di configurazioni del LBA è $qng^n$.

**DIMOSTRAZIONE**:
Una configurazione è una tripla che comprende:
* lo stato del LBA.
* la posizione della testina.
* il contenuto del nastro.

Nel nostro caso abbiamo:
* Numero di stati: $q$.
* Numero di posizioni della testina: $n$
* Possibili contenuti del nastro: $g^n$ ($\to$ g simboli per ogni cella)

Passiamo alla dimostrazione del problema:

**TEOREMA**: $A_{LBA}$ è decidibile.
**DIMOSTRAZIONE**: Costruisci il seguente decisore per $A_{LBA}$:
* Su input $<M,w>$ (con $M =$ LBA):
	* Simula $M$ su $w$ per $qng^n$ passi di computazione, oppure fino a terminazione.
	* Se $M$ ha terminato: ritorna il suo output.
	* Se $M$ non ha terminato: **reject**.
## Problema 2
$$E_{LBA} = \{<M> \ |\ M \text{ è LBA e } L(M) = \emptyset\}$$
Tale problema è indecidibile.
**DIMOSTRAZIONE**:
Costruiamo una riduzione da $A_{TM}$ a $E_{LBA}$ sfruttando la tecnica delle storie di computazione accettanti.
Assumiamo per assurdo che $E_{LBA}$ sia decidibile e costruiamo un decisore per $A_{TM}$ (che è impossibile):
* Decisore per $A_{TM}$
	*  Su input $<M, w>$ ($\to$ dove $M$ è MdT):
		* Costruiamo un LBA $N$ con la seguente caratteristica:
		  $L(N) = \begin{cases} \text{NON VUOTO} \quad \text{se } M \text{ accetta } w \\ \text{VUOTO} \quad \text{altrimenti}\end{cases}$
		* Esegui il decisore per $E_{LBA}$ su $<N>$
		* Ritorna il suo output invertito.

Costruiamo il nostro LBA $N$ in modo che $N$ sia l'insieme delle storie di computazione accettanti di $M$ e $w$.
* Se $L(N) = \emptyset$, allora non ci sono storie di computazione accettanti di $M$ e $w$, quindi $M$ non accetta $w$.
* Se $L(N) \neq \emptyset$, allora vi è una storia di computazione accettante di $M$ e $w$, quindi $M$ accetta $w$.

**Come è fatto nel concreto l'LBA $N$?**
Assumiamo di rappresentare le storie di computazione accettanti nel seguente formato: $$\#C_1\#C_2\#...\#C_k\#$$ dove le $C_i$ sono configurazioni.
Come verifichiamo se tale stringa è una storia di configurazione accettante?
* $C_1$ è configurazione iniziale di $M$ di $w$ ($\to$ semplice scansione di $C_1$, basta verificare $C_1=q_0w$ dove $q_0$ è lo stato iniziale di $M$).
* $C_k$ è una configurazione accettante di $M$ su $w$ ($\to C_k = uq_{accept}w$ per qualche $u,v$).
* $\forall i: C_{i+1}$ discende da $C_i$ secondo la funzione di transazione di $M$.
## Problema 3
$$ALL_{CFG} = \{<G>\ |\ G \text{ è CFG e } L(G) = \Sigma^*\}$$
Tale problema è indecidibile.

**DIMOSTRAZIONE**:
Assumiamo per assurdo che $ALL_{CFG}$ sia decidibile e costruiamo un decisore per $A_{TM}$ (assurdo). Il decisore per $A_{TM}$ è il seguente:
* Su input $<M,w>$:
	* Costruisci una CFG $G$ con la seguente proprietà:
	  $L(G) = \begin{cases} A \neq \Sigma^* \quad \text{se } M \text{ accetta } w \\ \Sigma^* \quad \text{altrimenti}\end{cases}$
	* Esegui il decisore per $ALL_{CFG}$ su input $G$.
	* Ritorna l'output invertito.
Costruiamo $G$ in modo tale che $L(G)$ contenga le stringhe che *non* sono storie di computazione accettanti per $M$ e $w$:
* Se $L(G) = \Sigma^*$, allora nessuna stringa è una storia di computazione accettante per $M$ e $w$, quindi $M$ non accetta $w$.
* Se $L(G) \neq \Sigma^*$, allora qualche stringa è una storia di computazione accettante per $M$ e $w$, quindi $M$ accetta $w$.

Specificare $G$ sarebbe molto complesso. Invece di dare $G$ possiamo definire un PDA $P$. Nella nostra costruzione $G$ è la conversione di $P$ in una CFG.

**COSTRUZIONE DEL PDA**:
Costruiamo il PDA $P$ in modo tale che $L(P)$ comprenda le stringhe che non sono storie di computazione accettante per $M$ e $w$:
$$\#C_1\#C_2\#...\#C_k\#$$
Quella sopra riportata è una stringa che codifica una storia di computazione accettante.

**Come verifichiamo che una stringa non è una storia di computazione accettante?**
* $C_i$ non è configurazione iniziale di $M$ su $w$, cioè $C_1 \neq q_0w$.
* $C_k$ non è configurazione accettante, cioè $C_k \neq uq_{accept}v$
* $\exists i : C_{i + 1}$ non discende da $C_i$ secondo la funzione di transazione della MdT $M$. ($\to$ è necessario cambiare la rappresentazione come stringa:$\#C_1\#C^R_2\#C_3\#C^R_4...\#C_k\#$ )

Il PDA $P$ sceglie non deterministicamente se verificare la condizione $1,2$ o $3$.

$ALL_{CFG}$ è indecidibile.
Dimostrare che $EQ_{CFG} = \{<G,H>\ |\ G,H \text{ sono CFG e } L(G) = L(H)\}$ 

*Nota*: Il cambio di configurazione nel punto $3$ è necessario per poter confrontare correttamente i valori nello stack.
# Definizioni di riducibilità
Utili perché:
* Permettono di dimostrare proprietà generali di ogni riduzione.
* Permettono di effettuare ragionamenti più sofisticati di quelli fatti finora.
## Definizione di mapping riducibilità  (o riducibilità attraverso funzioni)
Inizialmente abbiamo bisogno della definizione di **calcolabilità**:

> Una funzione $f: \Sigma^* \to \Sigma^*$ si dice **calcolabile** $\iff$ esiste una MdT $M$ tale che, per ogni stringa $w$, $M$ su input $w$ termina lasciando $f(w)$ sul nastro.

Un esempio banale è dato dalla somma:
	Possiamo pensare ad una sequenza di $n$ volte un carattere $a$
	Per esempio, potremmo scrivere $3 + 4$ come: $$aaa\#aaaa$$
	e successivamente come: $$aaaaaaa$$
	Abbiamo così lasciato sul nastro una sequenza di $7\ a$, ovvero la somma di $3$ e $4$.

**Definizione di mapping-riducibilità**:
> Un linguaggio $A$ è mapping-riducibile ad un linguaggio $B$ ($A \leq_m B$) $\iff$ esiste una funzione calcolabile $f$ tale che, per ogni stringa $w$, $w \in A \iff f(w) \in B$.

In altre parole, se prendo un punto che sta in $A$, il risultato della funzione $f$ applicata su tale punto dovrà essere in $B$.
Se invece il punto di partenza è fuori da $A$, allora finirò fuori da $B$.

*Osservazione*: $A \leq_m B \iff \overline{A} \leq_m \overline{B}$.
## Teorema
> Se $A \leq_m B$ e $B$ è **decidibile**, allora $A$ è **decidibile**.

**DIMOSTRAZIONE**:
Dato che $A \leq_m B$, esiste una funzione **calcolabile** $f$ tale che, per ogni stringa $w$, $w \in A \iff f(w) \in B$.
Visto che $B$ è decidibile, allora esiste un decisore $M$ tale che $L(M) = B$.

Costruiamo un decisore per $A$ come segue:
* Su input $w$:
	* Calcola $f(w)$.
	* Esegui $M$ su input $f(w)$.
	* Ritorna il suo output.

$w \in A \implies f(w) \in B \implies$ Il decisore ritorna **accept**.
$w \notin A \implies f(w) \notin B \implies$ Il decisore ritorna **reject**.

**COROLLARIO**: Se $a \leq_m B$ e $A$ è indecidibile, allora $B$ è indecidibile.
## Esempio
Dimostriamo che $A_{TM} \leq_m HALT_{TM}$.
$$A_{TM} = \{<M,w>\ |\ M \text{è MdT e } w \in L(M)\}$$
$$HALT_{TM} = \{<M,w>\ |\ M \text{ è MdT che termina su input } w\}$$

Dobbiamo trovare una $f$ calcolabile, tale che: $$<M,w> \in A_{TM} \iff f(<M,w>) \in HALT_{TM}$$
Diamo una MdT $F$ che implementa la funzione $f$:
* Su input $<M,w>$:
	* Costruiamo una nuova MdT N definita come segue:
		* Su input $x$:
			* Simula $M$ su $x$.
			* Se $M$ accetta: **accept**.
			* Se $M$ rifiuta: vai in loop.
		* Ritorna $<N,w>$

Dimostriamo la correttezza di ciò che abbiamo appena scritto, distinguendo $3$ casi:
* $M$ accetta $w \implies <M,w> \in A_{TM}$ In questo caso $N$ accetta $w$, quindi $<N,w> \in HALT_{TM}$.
* $M$ rifiuta $w \implies <M,w> \notin A_{TM}$ In questo caso $N$ va in loop su $w$, quindi $<N,w> \notin HALT_{TM}$.
* $M$ va in loop su $w \implies <M,w> \notin A_{TM}$ In questo caso $N$ va in loop su $w$, quindi $<N,w> \notin A_{TM}$.
## Esempio 2
Dimostriamo che $E_{TM} \leq_m EQ_{TM}$.

$$E_{TM} = \{<M> \ |\ M \text{ è MdT e } L(M) = \emptyset\}$$
$$EQ_{TM} = \{<M_1,M_2>\ |\ M_1,M_2 \text{ sono MdT e } L(M_1) = L(M_2)\}$$

Costruiamo una $f$ calcolabile tale che $<M> \in E_{TM} \iff f(<M>) \in EQ_{TM}$.
$f$ è implementata sulla seguente MdT $F$:
* Su input $<M>$:
	* Costruisci una nuova MdT $N$ tale che $L(N) = \emptyset$.
	* Ritorna $<M,N>$

$<M> \in E_{TM} \implies L(M) = \emptyset \implies <M,N> \in EQ_{TM}$
$<M> \notin E_{TM} \implies L(M) \neq \emptyset \implies <M,N> \notin EQ_{TM}$
## Esempio 3
Dimostriamo che $A_{TM} \leq_m \overline{E}_{TM}$.
Vogliamo costruire una $f$ calcolabile tale che $<M,w>\in A_{TM} \iff f(<M,w>) \in \overline{A}_{TM}$
Implementiamo $f$ tramite la seguente MdT $F$:
* Su input $<M,w>$:
	* Costruisci una nuova MdT $N$ definita come segue:
		* $N =$ su input $x$:
			* Se $x \neq w$: **reject**.
			* Altrimenti: simula $M$ su $w$ e ritorna il suo output.
	* Ritorna $N$.

Dimostriamo la correttezza di ciò che abbiamo appena scritto, distinguendo 2 casi:
* $<M,w> \in A_{TM} \implies M$ accetta $w$
	* $\implies L(N) = \{w\}$
	* $\implies L(N) \neq \emptyset$
	* $\implies <N> \notin E_{TM}$
	* $\implies <N> \in \overline{E}_{TM}$
* $<M,w> \notin A_{TM} \implies M$ non accetta $w$
	* $\implies L(N) = \emptyset$
	* $\implies <N> \in E_{TM}$
	* $\implies <N> \notin \overline{E}_{TM}$
## Problema
Dimostrare che $A_{TM} \nleq_m E_{TM}$.
## Teorema
Se $A \leq_m B$ e $B$ e T.R., allora anche $A$ è T.R.

**DIMOSTRAZIONE**:
Dato che $A \leq_m B$, esiste una $f$ calcolabile tale che, per ogni stringa $w$:
* $w \in A \iff f(w) \in B$
* Dato che $B$ è T.R., esiste una MdT $M$ tale che $L(M) = B$.
* Costruiamo una MdT $N$ tale che $L(N) = A$.
* Su input $w$:
	* Calcola $f(w)$.
	* Esegui $M$ su $<f(w)>$ e ritorna il suo output.

**COROLLARIO**: se $A \leq_m B$ e $A$ non è T.R., allora $B$ non è T.R.

> La mapping-riducibilità ci permette di dimostrare che alcuni problemi non sono T.R.
## Teorema
$EQ_{TM}$ non è T.R.

**DIMOSTRAZIONE**:
Dimostriamo che $\overline{A}_{TM} \leq_m EQ_{TM}$, cioè $A_{TM} \leq_m \overline{EQ}_{TM}$.

Costruiamo quindi una $f$ calcolabile tale che $<M,w> \in A_{TM} \iff f(<M,w>) \in \overline{EQ}_{TM}$,

$f$ è implementata dalla seguente MdT $F$:
* Su input $<M,w>$:
	* Costruiamo una nuova MdT $N_1$:
		* **reject**.
	* Costruiamo una nuova MdT $N_2$
		* Su input $x$:
			* Simula $M$ su $w$.
			* Ritorna il suo output.
	* Ritorniamo $<N_1,N_2>$.

*Nota*: $L(N_1) = \emptyset$.
*Nota*: Qualsiasi sia l'input di $N_2$, essa simulerà sempre su $w$.

Dimostriamo la correttezza di ciò che abbiamo appena scritto, distinguendo 2 casi:
* $<M,w> \in A_{TM} \implies M$ accetta $w$
	* $\implies L(N_2) = \Sigma^*$.
	* $\implies L(N_1) \neq L(N_2)$.
	* $\implies <N-1,N_2> \in \overline{EQ}_{TM}$.
* $<M,w> \notin A_{TM} \implies M$ non accetta $w$.
	* $\implies L(N_2) = \emptyset$.
	* $\implies L(N_1) = L(N_2)$.
	* $\implies <N_1,N_2> \notin \overline{EQ}_{TM}$.

**VARIAZIONI**:
* Costruiamo una nuova MdT $N_2$
	* Su input $x$:
		* Se $x \neq w$: **reject**.
		* Altrimenti simula $M$ su $w$ e ritorna il suo output.
* Ritorniamo $<N_1,N_2>$.

In questo caso:

* $<M,w> \in A_{TM} \implies M$ accetta $w$
	* $\implies L(N_2) = \{w\}$.
	* $\implies L(N_1) \neq L(N_2)$.
	* $\implies <N-1,N_2> \in \overline{EQ}_{TM}$.

E la dimostrazione sarebbe corretta lo stesso.


Se invece volessimo fare $A_{TM} \leq EQ_{TM}$:

$f$ è implementata dalla seguente MdT $F$:
* Su input $<M,w>$:
	* Costruiamo una nuova MdT $N_1$:
		* **accept**.
	* Costruiamo una nuova MdT $N_2$
		* Su input $x$:
			* Simula $M$ su $w$.
			* Ritorna il suo output.
	* Ritorniamo $<N_1,N_2>$.

*Nota*: in questo caso $L(N_1) = \Sigma^*$.
## Turing riducibilità
$$\overline{A_{TM}} \leq_m A_{TM}\ ????$$
*Reminder*: Se $A \leq_m B$ e $A$ non è T.R., allora $B$ non è T.R. Nel nostro caso infatti $\overline{A_{TM}}$ non è T.R. mentre $A_{TM}$ è T.R.

Introduciamo la **Turing riducibilità**:
* Un **oracolo** è per un linguaggio $B$ è un dispositivo( generico) che, per ogni stringa $w$ ritorna *accept* se $w \in B$ e *reject* se $w \notin B$.
* Una **MdT con oracolo** per il linguaggio $B$ è una MdT estesa con la possibilità di interrogare un oracolo per $B$.

**DEFINIZIONE**: Un linguaggio $A$ è Turing Riducibile ad un linguaggio $B$, rappresentato con la notazione $A \leq_T B \iff$ esiste una MdT con oracolo per $B$ che decide $A$. 

*Osservazione*: $\overline{A_{TM}} \nleq_m A_{TM}$ ma $\overline{A_{TM}} \leq_T A_{TM}$.
## Esempio 1
Dimostriamo che $\overline{A_{TM}} \leq_T A_{TM}$.

Costruiamo una MdT con oracolo per $A_{TM}$ che decide $\overline{A_{TM}}$:
* Su input $x$:
	* Invoca l'oracolo per $A_{TM}$ su $x$.
	* Inverti il suo responso.
## Esempio 2
Dimostriamo che $E_{TM} \leq_T A_{TM}$.

Dimostriamo che esiste una MdT con oracolo per $A_{TM}$ che decide $E_{TM}$.
* Su input $<M>$:
	* Costruiamo una nuova MdT $N$ con la seguente proprietà:
		* $L(N) = \begin{cases} \Sigma^* \quad \text{se } L(M) \neq \emptyset \\ \emptyset \quad \text{se } L(M) = \emptyset \end{cases}$
	* Esegui l'oracolo per $A_{TM}$ su input $<N,1>$.
	* Invertiamo il responso.

Definiamo la MdT $N$:
* $N=$ su input $x$:
	* Per $i=0,1,2,3,...$
		* Esegui $M$ su $s_0,s_1,...,s_i$ per $i$ passi di computazione.
		* Se una di tali computazioni accetta, ritorna con **accept**.
## Teorema
Se $A \leq_T B$ e $B$ è decidibile, allora $A$ è decidibile.

**DIMOSTRAZIONE**:
Sia $A \leq_T B$, allora esiste una MdT con oracolo per $B$ che decida $A$. Posso costruire un decisore per $A$ sostituendo tutte le chiamate all'oracolo per $B$ con chiamate al decisore per $B$.

**COROLLARIO**: Se $A \leq_T B$ è indecidibile, e $A$ è indecidibile, allora $B$ è indecidibile.
## Teorema
Se $A \leq_m B$, allora $A \leq_T B$.

**DIMOSTRAZIONE**:
Dato che $A \leq_m B$, esiste una funzione calcolabile $f$ tale che, $\forall w, w \in A \iff f(w) \in B$.
Costruisco una MdT con oracolo per $B$ che decide $A$ come segue:
* Su input $w$:
	* Calcola $f(w)$.
	* Esegui l'oracolo per $B$ su $f(w)$
	* Ritorna il suo output.
## Pro e contro di $\leq_m$ e $\leq_T$

| MAPPING $\leq_m$                                                                                                                                    | TURING $\leq_T$                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| $\color{green}+$Permette di dimostrare che certi problemi non sono Turing riconoscibili<br>(se $A \leq_m B$ e $A$ non è T.R. allora $B$ non è T.R.) | $\color{green}+$ Più intuitiva ($\overline{A_{TM}} \leq_T A_{TM}$)<br>$\color{green}+$ Se vale $\leq_m$, vale $leq_T$ |
| $\color{red}-$Non cattura certe riduzioni intuitiva ($\overline{A_{TM}} \nleq_m A_{TM}$)                                                            | $\color{red}-$Non ci aiuta a dimostrare che certi problemi non sono T.R:                                              |
## Teorema di Rice
**ENUNCIATO "INFORMALE"**: 
Qualsiasi proprietà non banale del linguaggio di una MdT è *indecidibile*.

**ESEMPI**:
$E_{TM} = \{<M>\ |\ M \text{è una MdT e } L(M) = \emptyset\}$
$A_{TM} = \{<M,w>\ |\ M \text{è MdT e } w \in L(M)\}$
$REG_{TM} = \{<M>\ |\ M \text{ è MdT e } L(M) \text{ è regolare}\}$

**ENUNCIATO FORMALE**: 
* Una **proprietà di una MdT** è un insieme $P$ contenente una serie di descrizioni $<M_1>,<M_2>,<M_3>...$ di MdT (ovvero un linguaggio che contiene una serie di MdT che hanno tale proprietà).
* Una **proprietà non banale** è una proprietà $P$ tale che esistano MdT $M,N$ tali che $<M> \in P$ e $<N> \notin P$ (ovvero $P$ è soddisfatta da certe MdT e non da altre).
* Una **proprietà del linguaggio** è una proprietà $P$, tale che, comunque prese due MdT $M,N$ tali che $L(M) = L(N)$, allora $<M> \in P \iff <N> \in P$ (Se $M$ ed $N$ hanno lo stesso linguaggio, o $P$ vale sia per $M$ che per $N$, oppure $P$ non vale per nessuna dei due).

**DIMOSTRAZIONE**:
Sia $P$ una proprietà non banale del linguaggio di una MdT.
Assumiamo per assurdo che $P$ sia decidibile e sia $H$ il suo decisore.
In tal caso riusciremo a costruire un decisore per $A_{TM}$, che è assurdo in quanto $A_{TM}$ è indecidibile.
Il decisore per $A_{TM}$ è il seguente:
* Su input $<M,w>$:
	* Costruisci una nuova MdT $N$ tale che $N$ ha la proprietà $P$ se $M$ accetta $w$ e $N$ non ha la proprietà $P$ altrimenti.
	* Esegui $H$ su input $N$.
	* Ritorna il suo output.

**Come è fatta la costruzione dello step $1$, cioè $N$?**:

**Costruzione di $N$**:
Visto che $P$ non è banale, devono esistere:
* Almeno una MdT che soddisfa $P$.
* Almeno una MdT che non soddisfa $P$.

Assumiamo senza perdita di generalità (cioè senza restringere le ipotesi) che la macchina $V_{\emptyset}$, tale che $L(V_{\emptyset}) = \emptyset$ non soddisfa $P$, cioè $<V_{\emptyset}> \notin P$. Sia invece $T$ una MdT che soddisfa $P$, cioè $<T> \in P$.

Costruiamo la macchina $N$ come segue:
* $N=$ su input $x$:
	* Esegui $M$ su $w$.
	* Se $M$ ha rifiutato: **reject**.
	* Se $M$ ha accettato: simula $<T>$ su $x$ e ritorna il suo output.

Pertanto il linguaggio di $N$ è:
$$L(N) = \begin{cases} L(T) \quad \text{se } M \text{ accetta } w\\ \emptyset\ (= V_{\emptyset}) \quad \text{altrimenti} \end{cases}$$

In particolare sappiamo che $<V_{\emptyset}> \notin P$ e $L(T) \in P$. 
## Problema 1
$$EQ_{CFG} = \{<G,H>\ |\ G,H \text{ sono CFG e } L(G) = L(H)\}$$
Dimostrare che $EQ_{CFG}$ è CO-Turing riconoscibile (il suo complemento è T.R.).

Costruiamo una MdT $M$ tale che $L(M) = \overline{EQ_{CFG}}$:
* $M =$ su input $<G,H>$:
	* Per $i = 1,2,3,4,...$
		* Esegui il decisore per $A_{CFG}$ su input $<G,s_i>$
		* Esegui il decisore per $A_{CFG}$ su input $<H,s_i>$
		* Se i due output sono diversi: **accept**

Può continuare all'infinito se tutte le stringhe sono uguali. Tuttavia, a noi non serve un decisore, ci basta sapere se due output sono diversi.
## Problema 2
Dimostrare che $A_{TM} \nleq_m E_{TM}$.
*Nota*: Ricordiamo che $A_{TM} \leq_m \overline{E_{TM}}$.

Assumiamo per assurdo che $A_{TM} \leq_m E_{TM}$. Tale affermazione è equivalente a $\overline{A_{TM}} \leq_m \overline{E_{TM}}$. Osserviamo che $\overline{A_{TM}}$ non è T.R. (dimostrato). Inoltre sappiamo che $\overline{E_{TM}}$ 
è T.R. (dimostrato). Ciò è impossibile, perché sappiamo che se $A \leq_m B$ e $A$ non è T.R., allora $B$ non è T.R.
## Problema 3
Si consideri la seguente affermazione: "Se $A \leq_m B$ e $B$ è regolare, allora anche $A$ è regolare". Dimostrare la sua verità o la sua falsità.

**RAGIONIAMO**: Se $A \leq_m B$, allora esiste una funzione calcolabile $f$, tale che, per ogni stringa $w$, $w \in A \iff f(w) \in B$. Sappiamo che $B$ è regolare, quindi esiste un DFA che lo riconosce. Dovremmo costruire un DFA che riconosca $A$. La funzione $f$ è calcolabile, ciò significa che ci serve una MdT per calcolarla (Un DFA è troppo semplice per farlo).

La proprietà è *falsa*, possiamo dimostrare che $\{0^n1^n\ |\ n \geq 0\} \leq_m 0^*1^*$.
La nostra funzione $f$ è:
$$f(w) = \begin{cases} 01 \quad \text{se }w \text{ ha forma } 0^n1^n \\ 10 \quad \text{altrimenti}\end{cases}$$
Nel nostro caso, $f$ è calcolabile perché può riconoscere $0^n1^n$ e da in output dei valori corretti rispetto alle limitazioni fornite ($0^*1^*$).
## Problema 4
Dimostrare che se $A$ è T.R. e $A \leq_m \overline{A}$, allora $A$ è decidibile.
Dato che $A \leq_m \overline{A}$, abbiamo che $\overline{A} \leq_m \overline{\overline{A}} = A$. Questo perché la mapping riducibilità e preservata dal complemento. Dato che $\overline{A} \leq_m A$, allora anche $\overline{A}$ è T.R.
Dato che sia $A$ che $\overline{A}$ sono T.R. concludiamo che $\overline{A}$ è decidibile per il teorema visto a lezione.
## Problema 5
Dimostrare che $A$ è T.R. $\iff A \leq_m A_{TM}$.
* $\implies$ Assumiamo che $A$ sia T.R., allora esiste una MdT $M$ tale che $L(M) = A$. Per dimostrare che $A \leq_m A_{TM}$ dobbiamo trovare una funzione calcolabile $f$ tale che, per ogni stringa $w$, $w \in A \iff f(w) \in A_{TM}$.
  Definiamo $f(w) = <M,w>$, tale funzione è calcolabile, inoltre:
	* $w \in A$. In tal caso $M$ accetta $w$, quindi $<M,w> \in A_{TM}$.
	* $w \notin A$. In tal caso $M$ non accetta $w$, quindi $<M,w> \notin A_{TM}$.
* $\impliedby$ Assumiamo che $A \leq_m A_{TM}$. Vogliamo dimostrare che $A$ è T.R. Visto che $A_{TM}$ è T.R. l'ipotesi $A \leq_m A_{TM}$ implica che $A$ è T.R.
## Problema 6
Dimostrare che $A$ è decidibile $\iff$ $A \leq_m 0^*1^*$.
* $\implies$ Dato che $A$ è decidibile, esiste un decisore $M$ tale che $L(M) = A$. Per dimostrare che $A \leq_m 0^*1^*$ dobbiamo costruire una funzione $f$ calcolabile, tale che $\forall w, w \in A \iff f(w) \in 0^*1^*$.
  Implementiamo $f$ tramite la seguente MdT $F$.
	* Su input $w$:
		* Esegui $M$ su $w$
		* Se $M$ accetta: scrivo $01$ sul nastro.
		* Se $M$ rifiuta: scrivo $10$ sul nastro.
		* *Nota*: $M$ non va in loop perché è un decisore. Se $M$ andasse in loop, $F$ non sarebbe calcolabile.
* $\impliedby$ Sia $A \leq_m 0^*1^*$. Possiamo dimostrare che $0^*1^*$ è regolare, pertanto esso è anche decidibile. Dato che $A \leq_m 0^*1^*$ e $0^*1^*$ è decidibile, allora anche $A$ è decidibile.
## Problema 7
**Tipico esercizio da esame**:
Si consideri il problema di determinare se una MdT con due nastri scrive un simbolo diverso da $\sqcup$ sul secondo nastro, quando computa su un dato input $w$.
* Formalizzare tale un problema come un linguaggio.
* Dimostrare che esso è indecidibile.

**Punto $1$**:
Il nostro linguaggio è $$B = \{<T,w>\ |\ T \text{ è MdT con 2 nastri che scrive un simbolo diverso da $\sqcup$ sul secondo nastro quando computa su } w\}$$
**Punto $2$**:
Assumiamo per assurdo che $B$ sia decidibile. Utilizziamo il decisore per $B$ per costruire un decisore per $A_{TM}$ (assurdo).
* Su input $<M,w>$:
	* Costruiamo una MdT $T$ con $2$ nastri tale che, se $M$ accetta $w$, allora $T$ scrive $0$ sul secondo nastro, e non tocca il secondo nastro in caso contrario.
	* Eseguiamo il decisore per $B$ su $<T,w>$
	* Ritorna il suo output.

Definiamo la macchina $T$:
* $T$ su input $x$:
	* Simula $M$ su $x$ sul primo nastro.
	* Se $M$ rifiuta : termina
	* Se $M$ accetta: scrivi $0$ sul secondo nastro

*Nota*: potremmo anche fare in modo che $T$ accetti $x$ come input ma simuli $M$ sempre su $w$. In tal caso nel decisore per $T$ potremmo passare $<M,\text{generica stringa}>$.