
# Lezione 1
___

## Anomalie e dipendenze funzionali

Poiché un oggetto può essere modellato in maniera differente, sorge il dubbio su quale sia la forma migliore per modellarlo.

La teoria della $\color{red}normalizzazione$ si occupa di risolvere questi problemi.

![[Pasted image 20240212092142.png]]
* $\color{red} Rindonzanza \ dei \ dati$ : anomalie in presenza di aggiornamenti
* $\color{red} Scarsa \  espressività$ : impossibile rappresentare determinate informazioni

![[Pasted image 20240212092818.png]]


La $\color{red} teoria \  della \ normalizzazione$ fornisce una serie di strumenti/algoritmi per stabilire in modo rigoroso la bontà di uno schema relazionale e per migliorare schemi relazionali esistenti.

### Notazione
* Lettere maiuscole all'inizio dell'alfabeto (es: A, B, C) : attributi
* Lettere maiuscole ala fine dell'alfabeto  es: (T, X, Y) : insieme di attributi
* R(T) : schema relazionale costruito sugli attributi di T
* r: istanza dello schema relazionale
* t, u, v : ennuple di un'istanza di uno schema relazionale
* t[X] : ennupla ottenuta da t considerando i soli attributi X


### Dipendenza Funzionale

$\textbf{Definizione dipendenza funzionale}$
Sia R(T) uno schema di relazione e siano X, Y due insiemi di attributi non vuoti tali che X $\cup$ Y $\subseteq$ T, una dipendenza funzionale è un qualsiasi vincolo della forma X   $\rightarrow$ Y

$\textbf{Definizione di soddisfacibilità}$
Un'istanza R(T) soddisfa la dipendenza funzionale X $\rightarrow$ Y se e solo se ogni coppia di ennuple in r che coincide su X coincide anche su Y.
Formalmente chiediamo $\forall$t1, t2 $\in$ r : $t_1$[X] = $t_2$[X] $\implies$ $t_1$[Y] = $t_2$[Y]

$\textbf{Definizione di implicazione}$

Sia R(T, F) uno schema di relazione. Diciamo che F implica logicamente la dipendenza funzionale X $\rightarrow$ Y , indicato con F |= X $\rightarrow$ Y , se e solo se ogni istanza valida di R(T, F) soddisfa anche X $\rightarrow$ Y .

### Assiomi di Armstrong

Come possiamo dimostrare che F |= X $\rightarrow$ Y? E’ una proprietà difficile da dimostrare, perché quantifica su tutte le possibili istanze valide. 

![[Pasted image 20240212100219.png]]

$\color{red} Teorema$
F |- X $\rightarrow$ Y se e solo se  F |= X $\rightarrow$ Y.


*Come dimostrare che F |- x $\rightarrow$ Y?*

Una **derivazione** di X $\rightarrow$ Y da F è una sequenza finita di dipendenze funzionali $f_1$...$f_{i-1}$ tale che $f_n$ = X $\rightarrow$ Y  ed ogni $f_i$ è un elemento di F oppure può essere ottenuta da $f_1$...$f{i-1}$ usando una regola di inferenza
E’ comodo rappresentare una derivazione di F ⊢ X $\rightarrow$ Y come un albero rovesciato la cui radice è X $\rightarrow$ Y ed ogni altro nodo è giustificato da F oppure da una regola di inferenza.

$\textbf{Unione}$
Se X $\rightarrow$ Y e Y $\rightarrow$ X allora X $\rightarrow$ YZ
$\textbf{Decomposizione}$
Se X $\rightarrow$ YZ, allora X $\rightarrow$ Y.
$\textbf{Indebolimento}$
Se X $\rightarrow$ Y allora XZ $\rightarrow$ Y.