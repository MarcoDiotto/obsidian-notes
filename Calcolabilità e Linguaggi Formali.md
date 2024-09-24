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
![[Pasted image 20240924141709.png]]Differenze rispetto ai **DFA**:
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

Ce linguaggio riconosce il seguente NFA:
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