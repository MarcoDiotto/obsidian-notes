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
Abbiamo che $A \implies^*00\#11$ perché $a \implies 0A1 \implies 00A11 \implies 00B11 \implies 00\#11$

Sia $G$ una **CFG**, definiamo il suo linguaggio come:
* $L(G)=\{w\in\Sigma^*\ |\ S \implies^* w\}$
## Esempio 2
Si assuma $\Sigma = \{0,1\}$, si forniscano **CFG** per i seguenti linguaggi:
* Stringhe che comprendono almeno tre $1$: $S \to A1A1A1A1\quad A \to 0A\ |\ 1A\ |\ \epsilon$.
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
* Eliminiamo le produzioni della forma $A \to \epsilon$, dove $A$ non è lo **start symbol**. Per tutte le regole della forma $R \to uAv$ introduco una nuova regola $R \to uv$. Ciò deve essere fatto per tutte le occorrenze di $A$. Per esempio, data una regola del tipo $R \to uAvAw$, sarà necessario introdurre nuove regole: $R \to uvAw,\ R\to uAvw,\ R \to uavw$. 
* Eliminiamo le produzioni "unitarie" della forma $A \to B$. Per tutte le regole della forma $B \to u$, introduco una nuova regola $A \to u$.
* Rimpiazziamo ogni regola della forma $A \to u_1,u_2,..,u_k$ con $k \geq 3$ e la sostituiamo con nuove regole del tipo $A \to u_1,A_1,\ A_1 \to u_2A_2,..,\ A_{k-2} \to u_{k-1}u_k$. Nel nostro caso $u$ può essere sia un **terminale**, sia un **non-terminale**. Pertanto andiamo a rimpiazzare ogni terminale $u_i$ con un nuovo **non-terminale** $U_i$ e aggiungiamo la regola $U_i \to u_i$.

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
Un esempio è in **PDA** per: $$\{0^n1^n\ |\ n \geq 0\}$$
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
* $|xy| > 0$ ($\to$ se non fosse così sarebbe banalmente sempre vero).
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

Consideriamo una stringa $w \in A$ con $|w| \geq p$. Ciò implica che $|w| \geq b^{|V|} + 1$. Ragioniamo sull'altezza dei **parse tree** di $w$:
* Parse tree di altezza $1$ $\implies$ stringa di lunghezza massima $b$
* Parse tree di altezza $2$ $\implies$ stringa  di lunghezza massima $b^2$
In generale parse tree di altezza $h$ genera stringhe di lunghezza massima $b^h$.

I parse tree di $w$ hanno altezza almeno $|V| + 1$.
Fra tutti i parse tree di $w$ prendiamo quello col numero minimo di nodi.
Prendiamo il *cammino* più lungo di tale **parse tree**, ovvero la sua *altezza*, Tale cammino deve contenere almeno $|V| + 1$ **non-terminali**. Ciò implica che lungo tale cammino, c'è almeno un non-terminale $R$ che si ripete. Ci concentriamo su un non-terminale che si ripete fra i $|V| + 1$ non-terminali in basso al cammino.

Per la dimostrazione della prima condizione basta guardare il disegno.
## Dimostrazione seconda condizione ($|vy| > 0$)
Assumiamo per assurdo che $|xy| = 0$, cioè $|v| = |y| = 0$.
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
Osserviamo che se $s = uvxyz$, allora $vyz$ deve stare a cavallo fra le due metà della stringa. Infatti se cade nella prima o nella seconda metà esco dal linguaggio con un **pumping up**. Se $vyz$ sta a cavallo delle due metà, allora $uv^2xy^2y = 0^p1^io^j1^p$, dove $i \ne p \lor j \ne p$. Questa stringa non sta nel linguaggio $D$ perché la prima metà è diversa dalla seconda.
## Esercizio 1
Dimostrare che la classe dei linguaggi context free è chiusa rispetto ad unione, concatenazione e star.

Dimostriamo la chiusura rispetto all'unione, cioè se $A$ e $B$ sono CFL (context-free language), allora $A \cup B$ è un CFL.
Dato che $A$ e $B$ sono CFL, esistono delle CFG $G = (V_1,\Sigma_1, R_1, S_1)$ e $H = (V_2,\Sigma_2,R_1,S_2)$, tali che $L(G) = A$ e $L(H) = B$. Costruiamo una nuova CFG $I = (V_3,\Sigma_3,R_3,S_3)$ tali che $L(I) = A \cup B$:
* $V_3 = V_1 \cup V_2 \cup \{S_3\}$
* $\Sigma_3 = \Sigma_1 \cup \Sigma_2$
* $R_3 = R_1 \cup R_2 \cup \{S_3 \to S_1, S_3 \to S_2\}$
* $S_3 =$ nuovo **start symbol** che non occorre il $V_1 \cup V_2$.
*Nota*: questa soluzione è corretta solo per $V_1 \cap V_2 = \emptyset$. Posso tuttavia assumerlo senza perdita di generalità.
## Esercizio 2
* Usare i linguaggi $A = \{a^mb^nc^n\ |\ m,n \geq 0\}$ e $B = \{a^mb^mc^n\ |\ m,n \geq 0\}$ per dimostrare che la classe dei CFL non è chiusa rispetto a $\cap$.
* Usare tale risultato per dimostrare che non è chiusa rispetto al complemento.

Osserviamo che sia $A$ che $B$ sono CFL.
Assumiamo per assurdo che la classe dei CFL sia chiusa rispetto a $\cap$, quindi $A \cap B$ è CFL.
$$A \cup B = \{a^nb^nc^n\ |\ n \geq 0\}$$ che abbiamo dimostrato essere non CFL perché non rispetta il pumping lemma.

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
Definizione di MdT per il seguente linguaggio: $\{w\#w\ |\ w \in \{0,1\}^*\}$ (non CLF, ma riconoscibile da una MdT):
![[Pasted image 20241030142159.png]]

**Passi di esecuzione**:
* Fai zig-zag fra posizioni corrispondenti a sinistra e a destra di $\#$ per verificare che essere contengano lo stesso simbolo. Se non è così o non trovi $\#$: RIFIUTA. Altrimenti sostituisci con $\times$ i simboli corrispondenti.
* Quando hai controllato tutti i simboli di a sinistra di $\#$, verifica se ci sono simboli rimanenti a destra di $\#$. in tal caso RIFIUTA, altrimenti ACCETTA.
## Definizione formale di MdT
Una MdT è una settupla $(Q,\Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$ dove:
* $Q$ è un insieme finito di stati.
* $\Sigma$ è un alfabeto finito di input, tale che $U\text{(blank)} \notin \Sigma$.
* $\Gamma$ è un alfabeto finito per il nastro, tale che $U \in \Gamma$ e $\Sigma \subseteq \Gamma$.
* $\delta: Q \times \Gamma \to Q \times \Gamma \times \{L,R\}$ è la funzione di transizione.
* $q_0 \in Q$ è lo stato iniziale.
* $q_{accept} \in q$ è lo stato di accettazione.
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
* Sia $M$ nella configurazione $uaq_ibv$ e sia $\delta(q_i,b) = (q_j,c,L)$ (dove $L$ sta per *left*), allora la prossima configurazione sarà $uq_jacb$.
* Sia $M$ nella configurazione $uaq_ibv$ e sia $\delta(q_i,b) = (q_j,c,R)$ (dove $R$ sta per $right$), allora la prossima configurazione sarà $uacq_jv$.
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

