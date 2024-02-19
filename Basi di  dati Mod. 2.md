
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
* Lettere maiuscole all'inizio dell'alfabeto (es: $A, B, C$) : attributi
* Lettere maiuscole ala fine dell'alfabeto  es: ($T, X, Y$) : insieme di attributi
* $R(T)$ : schema relazionale costruito sugli attributi di $T$
* $r$: istanza dello schema relazionale
* $t, u, v$ : ennuple di un'istanza di uno schema relazionale
* $t[X]$ : ennupla ottenuta da $t$ considerando i soli attributi $X$


### Dipendenza Funzionale

$\textbf{Definizione dipendenza funzionale}$
Sia $R(T)$ uno schema di relazione e siano $X$, $Y$ due insiemi di attributi non vuoti tali che $X$ $\cup$ $Y$ $\subseteq$ $T$, una dipendenza funzionale è un qualsiasi vincolo della forma X $\rightarrow$ Y

$\textbf{Definizione di soddisfacibilità}$
Un'istanza $r$ di $R(T)$ soddisfa la dipendenza funzionale $X$ $\rightarrow$ $Y$ se e solo se ogni coppia di ennuple in $r$ che coincide su $X$ coincide anche su $Y$.
Formalmente chiediamo $\forall t1, t2 \in r : t_1[X] = t_2[X] \implies t_1[Y] = t_2[Y]$.

$\textbf{Definizione di implicazione}$
Sia $R(T, F)$ uno schema di relazione. Diciamo che $F$ *implica logicamente* la dipendenza funzionale $X \rightarrow Y$ , indicato con $F \vDash X \rightarrow Y$, se e solo se ogni istanza valida di $R(T, F)$ soddisfa anche $X \rightarrow Y$.

### Assiomi di Armstrong

Come possiamo dimostrare che $F \vDash X \rightarrow Y$ ? E’ una proprietà difficile da dimostrare, perché quantifica su tutte le possibili istanze valide.

Regole di inferenza della forma  $F\vdash$ $X\rightarrow Y$ :
$$REFL: \frac{Y \subseteq X}{F \vdash X \rightarrow Y} \ \ AUGM: \frac{F \vdash X \rightarrow Y}{F \vdash XW \rightarrow YW} \ \ TRANS: \frac{F \vdash X \rightarrow Y\ \ \ F \vdash Y \rightarrow X}{F \vdash X \rightarrow Z}$$
**Nota**:
* $\vDash$ : sempre vero, *assioma*
* $\vdash$ : potrebbe essere sbagliato se le regole sono sbagliate, *derivazione*

$\color{red} Teorema$
F $\vdash$ X $\rightarrow$ Y se e solo se  F $\vDash$ X $\rightarrow$ Y.


*Come dimostrare che $F \vdash x \rightarrow Y$?*

Una **derivazione** di X $\rightarrow$ Y da F è una sequenza finita di dipendenze funzionali $f_1$...$f_{i-1}$ tale che $f_n$ = X $\rightarrow$ Y  ed ogni $f_i$ è un elemento di F oppure può essere ottenuta da $f_1$...$f{i-1}$ usando una regola di inferenza
E’ comodo rappresentare una derivazione di F ⊢ X $\rightarrow$ Y come un albero rovesciato la cui radice è X $\rightarrow$ Y ed ogni altro nodo è giustificato da F oppure da una regola di inferenza.

$\textbf{Unione}$
Se $X \rightarrow Y$ e $Y \rightarrow Z$ allora $X \rightarrow YZ$
$\textbf{Decomposizione}$
Se $X \rightarrow YZ$, allora $X \rightarrow Y$.
$\textbf{Indebolimento}$
Se $X \rightarrow Y$ allora $XZ \rightarrow Y$.
## Problema dell'implicazione
#### Definizione di Chiusura di F
Dato un insieme $F$ di dipendenze funzionali, la *chiusura* di $F$ è definita come l'insieme $F^+ = \{X \rightarrow Y\ |\ F \vdash X \rightarrow Y\}$.
#### Definizione Problema dell'implicazione
Il *problema dell'implicazione* corrisponde a decidere, dati $F$ e $X \rightarrow Y$ se  $X \rightarrow Y \in F^+$ oppure no.  

**Nota**: calcolare $F^+$ applicando gli assiomi di Armstrong ha costo *esponenziale* e pertanto è un modo *algoritmicamente inefficiente* per risolvere il problema dell'implicazione.

#### Definizione chiusura di X 
Sia $R(T,F)$ uno schema di relazione.  Dato $X \subseteq T$, la *chiusura* di $X$ rispetto ad $F$ e definita come l'insieme $X_{F}^{+} = \{ A \in T\ | \ F \vdash X \rightarrow A\}$ .

#### Teorema
$F \vdash X \rightarrow Y$ se e solo se  $Y \subseteq X^+_F$.
 
 $\color{red} \textbf{Dimostrazione}$
 * $(\implies)$ Da $F \vdash X \rightarrow Y$ abbiamo $\forall A \in Y : F \vdash X \rightarrow A$ per la regola di decomposizione. La conclusione deriva dalla definizione di $X^+_F$.
 * $(\impliedby)$  Da $Y \subseteq X^+_F$ abbiamo $\forall A \in Y : F \vdash X \rightarrow A$ per definizione di $X^+_F$.
 * La conclusione deriva dalla regola di unione
 
**Nota**: calcolare $F^+$ utilizzando il teorema appena descritto ha costo *polinomiale* e pertanto è *algoritmicamente efficiente*.

#### Calcolo di $X^+_F$

![[Pasted image 20240214110454.png]]

#### Valutazione della complessità
* Il *while* esterno viene eseguito al più $a$ volte.
* Il *for* interno viene eseguito al più $d$ volte.
* *Verificare l'inclusione di insiemi ordinati* di cardinalità al più $a$ nel *for* interno ha costo $O(a)$.
Pertanto la complessità totale dell'algoritmo è $O(a^2d)$.
# Lezione 2
___
## Chiavi e Coperture Canoniche
### Chiavi e attributi primi
#### Definizione di superchiave
Dato uno schema di relazione $R(T,F)$, un insieme di attributi $X \subseteq T$ è una *superchiave* di $R$  $\iff$ $X \rightarrow  T \in F^+$.
#### Definizione di Chiave
Una *chiave* è una superchiave minimale, cioè una superchiave tale che nessuno dei suoi sottoinsiemi propri sia a sua volta una superchiave.
#### Definizi0ne di attributi primi
Un attributo è *primo* $\iff$ appartiene ad almeno una chiave.

### Verifica di Superchiave

Dato $R(T,F)$ possiamo verificare se $X \subseteq T$ è una *superchiave* tramite il seguente algoritmo di costo *polinomiale*.
* Calcola la *chiusura* $X^+_F$
* Verifica se $X^+_F = T$

**Esempio**:
Si consideri la relazione $R(T,G)$ con $T = ABCDEF$ e $G = \{AB \rightarrow C,\ E \rightarrow A,\ A \rightarrow E,\ B \rightarrow F\}. \ ABD$ è superchiave
* $ABD^+_0 = ABD$
* $ABD^+_1 = ABCD$ (tramite $AB \rightarrow C$)
* $ABD^+_2 = ABCD$ E(tramite $A \rightarrow E$)
* $ABD^+_3 = ABCDEF$ (tramite $B \rightarrow F$)
Se io li aggiungo tutti allora $ABD$ è una superchiave.
### Verifica di Chiave
Dato $R(T,F)$ possiamo verificare se $X \subseteq T$ è una *chiave* tramite il seguente algoritmo di costo *polinomiale*.
* Verifica se $X$ è una superchiave. Se non lo è non è una chiave
* Verifica che $\forall A \in X$ si abbia $X \\ \{A\}^+_F \neq T$

**Esempio**:
Si consideri la relazione $R(T,G)$ con $T = ABCDEF$ e $G = \{AB \rightarrow C,\ E \rightarrow A,\ A \rightarrow E,\ B \rightarrow F\}. \ ABD$ è chiave perchè esso è una superchiave (come dimostrato precedentemente) e inoltre abbiamo che
* $A$ non può essere rimosso: $BD^+_G = BDF$
* $B$ non può essere rimosso: $AD^+_G = ADE$
* $D$ non può essere rimosso: $AB^+_G = ABCEF$
### Trovare una chiave
Dato $R(T, F)$, è possibile trovare una sua chiave in tempo *polinomiale*. L’idea dell’algoritmo è di partire da $T$ e rimuovere uno ad uno tutti gli attributi che non sono indispensabili per derivare $T$.
#### Algoritmo
![[Pasted image 20240214112747.png]]

**Esempio**:
Sia $G = \{AB \rightarrow C,\ E \rightarrow A,\ A\rightarrow E,\ B\rightarrow F\}$.  Costruiamo una chiave:
* Inizializziamo $K_0 = ABCDEF$
* Rimuoviamo $A$ da $K_0:\ BCDEF^+_G = ABCDEF$ quindi $A$ deve essere rimosso e aggiorniamo la chiave $K_1 = BCDEF$
*  Rimuoviamo $B$ da $K_1:\ CDEF^+_G = ACDEF$ quindi $B$ va tenuto
* Rimuoviamo $C$ da $K_1:\ BDEF^+_G = ABCDEF$ quindi $C$ deve essere rimosso e aggiorniamo la chiave $K_2 = BDEF$
* Rimuoviamo $D$ da $K_2:\ BEF^+_G = ABCDEF$ quindi $D$ va tenuto
* Rimuoviamo $E$ da $K_2:\ BDF^+_G = BDF$ quindi $E$ va tenuto
* Rimuoviamo $F$ da $K_2:\ BDE^+_G = ABCDEF$ quindi $F$ deve essere rimosso e aggiorniamo la chiave $K_3 = BDE$
L'algoritmo ritorna la *chiave* $K_3 = BDE$ , è l'unica chiave? 

### Trovare l'Insieme delle Chiavi
Dato $R(T,F)$ trovare *tutte* le chiavi ha costo *esponenziale*, perché ogni sottoinsieme di $T$ è potenzialmente una chiave. Esiste però un algoritmo piuttosto ottimizzato per la ricerca di tutte le chiavi.

**Intuizione**:

* Generiamo le possibili chiavi dalle più piccole alle più grandi
* Rappresentiamo i candidati da testare nella forma $X\ ::\ (Y)$, dove $X$ è l'insieme degli attributi da testare come *chiave*, e $Y$ l'insieme dei possibili attributi da aggiungere a $X$ qualora $X^+_F \neq T$
* $X^+_F = T$, allora $X$ è una *chiave* e possiamo scartare $X\ ::\ (Y)$
* Altrimenti calcoliamo $Y\ \\ \ X^+_F = \{A_1 ... A_n\}$ e generiamo i nuovi candidati $XA_1\ ::\ (A_1 ... A_n)\ XA_2\ ::\ (A_3 ... A_n)...XA_n\ ::\ ()$

**Nota**: se un attributo non compare mai alla destra di una dipendenza funzionale, allora esso deve fare parte di tutte le chiavi. L’insiemi di tali attributi sarà il primo che testeremo.

### Algoritmo per trovare l'Insieme delle Chiavi

![[Pasted image 20240214114822.png]]
### Verifica di Primalità
Ad oggi non esiste un *algoritmo efficiente* per trovare tutte gli attributi primi se non *trovare tutte le chiavi*
### Forma Canonica
Abbiamo visto vari algoritmi che operano sull'*insieme delle dipendenze funzionali*. Per questo motivo è utile portare tale insieme ad una **forma canonica** equivavente all'origine
#### Definizione di equivalenza
Due insiemi di dipendenza funzionale $F$ e $G$ sono **equivalenti**, indicato con $F \equiv G$ $\iff$ $F^+ = G^+$.
Se $F=G$ allora $F \equiv G$, ma **in generale non vale il contrario** 
#### Definizione di Attributo Estraneno
Sia $X \rightarrow Y \in F$. L'attributo $A \in X$ è detto **estraneo** $\iff$ $X$ \\ $\{A\}  \rightarrow Y \in F^+$.
#### Definizione di Dipendenza Ridondante
La dipendenza $X \rightarrow Y \in F$ è **ridondante** $\iff$ $X\rightarrow Y \in (F$ \\ $\{X\rightarrow Y\})^+$. 
# Lezione 3
___
## Forma Canonica
La **forma canonica** è un metodo per scrivere un insieme di dipendenze funzionali equivalente, che ci permette di eseguire  vari algoritmi
**Proprietà**:
* $|Y| =1$
* $X$ non contiene *attributi estranei*
* $X \to Y$ non è *ridondante*

#### Copertura Canonica
$G$ è **copertura canonica** di $F \iff F  \equiv G$ e $G$ è in forma canonica.
**Teorema**: per ogni insieme di dipemdemze funzionali $F$ esiste una copertura canonica
#### Algoritmo per determinare la copertura canonica
Segue 3 passi:
* Decompone tutte le dipendenze funzionali che haanno più attributi sulla destra $X \to Y \implies \{ X \to A | A \in Y\}$.
* Togliere dalla parte sinistra delle dipendenze gli attributi che non impediscono di derivare la dipendenza stessa. $X \to A \implies X$ \\ $Z | A \in (X$ \\ $Z)^+_F$.
* Togliere le dipendenze funzionali non essemziali per derivare la dipendenza stessa. $X \to A \implies F^{new} = F$\\ $\{X \to A\} | A \in X^+_{F - \{X \to A \}}$.

![[Pasted image 20240219090819.png]]

**Esempio**:
Abbiamo $F \{A \to BC, B \to C, A \to B, AB \to C\}$:
* $G = \{A \to B, A \to C, B \to C, A \to B, AB \to C \}$.
* $\{AB\}$\\ $\{A\}^+_F = B^+_F = BC$, quindi  $G = \{A \to B, B \to C, A \to B, \color{green}B \to C \color{default}$\},  $\to$  *se a sinistra c'è un solo elemento rimane com'è*. $Z \leftarrow AB$,  $\to$ $(AB$\\ $\{A\}^+_G = B^+_G = BC$, $\to$ $Z = B$.
* Dobbiamo verificarle tutte: $(A^+_{G- \{A \to B\}} = AC$, $A^+_{G - \{A \to C\}} = ABC$ $\to$ *si può togliere*,  $B^+_{G - \{B \to C\}} = B) \implies G = \{A \to B, B \to C\}$  .
## Esercizi
* Usando gli **assiomi di Armstrong**, si dimostri che se $X \to Y$ e $YW \to Z$ allora $XW \to Z$.
$$_{TRANS}\frac{_{AUGM}\frac{F \vdash X \to Y}{F \vdash XW \to YW}\ \ \ \ F\vdash Z}{F \vdash XW \to Z}$$
* Si supponga che una dipendenza funzionale $X \to Y$ sia soddisfatta da due istanze di relazione $r$ ed $s$ con gli stessi attributi. Dire se $r \cap s$ e $r \cup s$ soddisfano $X \to Y$, fornendo una dimostrazione o un controesempio oppurtuni.
$$\forall t_1, t_2 \in r \iff t_1[x] = t_2[x]\ allora\ t_1[y] = t2[y]$$
$$Considero:\ (r \cap s) \forall t_1, t_2 \in r \cap s\ allora\ t_1,t_2 \in r$$
* Si consideri lo schema di relazione $R(A,B,C,D)$ con dipendenze $F = \{AB \to C, C \to D, D \to A\}$. Si trovino tutte le dipendenze non banali derivabili da $F$ e tutte le chiavi di $R$.
$$\frac{F \vdash X \to Y}{F \vdash X \to Z | Z \in \mathcal{P}(Y)}$$
$$\color{white} A \to A, C \to CDA, \to D \to DA, \color{green} AB \to ABCD b\color{white}, AC \to ACD, AD \to AD,\color{green}BC \to BCDA \color{white},BD \to BDAC, CD \to CDA, ABC \to ABCD, ABD \to ABCD, ACD \to ACD, BCD \to ABCD$$