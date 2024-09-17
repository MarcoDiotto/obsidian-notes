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