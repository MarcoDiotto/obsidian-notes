
# Anomalie e Dipendenze Funzionali
___

## Teoria della Normalizzazione

Poiché un oggetto può essere modellato in maniera differente, sorge il dubbio su quale sia la forma migliore per modellarlo.

La teoria della $\color{red}normalizzazione$ si occupa di risolvere questi problemi.
## Qualità di Schemi Relazionali

![[Pasted image 20240212092142.png]]
* $\color{red} Rindonzanza \ dei \ dati$ : anomalie in presenza di aggiornamenti
* $\color{red} Scarsa \  espressività$ : impossibile rappresentare determinate informazioni

![[Pasted image 20240212092818.png]]


La $\color{red} teoria \  della \ normalizzazione$ fornisce una serie di strumenti/algoritmi per stabilire in modo rigoroso la bontà di uno schema relazionale e per migliorare schemi relazionali esistenti.

## Notazione
* Lettere maiuscole all'inizio dell'alfabeto (es: $A, B, C$) : attributi
* Lettere maiuscole ala fine dell'alfabeto  es: ($T, X, Y$) : insieme di attributi
* $R(T)$ : schema relazionale costruito sugli attributi di $T$
* $r$: istanza dello schema relazionale
* $t, u, v$ : ennuple di un'istanza di uno schema relazionale
* $t[X]$ : ennupla ottenuta da $t$ considerando i soli attributi $X$


## Dipendenza Funzionali

### Definizione dipendenza funzionale
Sia $R(T)$ uno schema di relazione e siano $X$, $Y$ due insiemi di attributi non vuoti tali che $X$ $\cup$ $Y$ $\subseteq$ $T$, una dipendenza funzionale è un qualsiasi vincolo della forma X $\rightarrow$ Y

### Definizione di soddisfacibilità
Un'istanza $r$ di $R(T)$ soddisfa la dipendenza funzionale $X$ $\rightarrow$ $Y$ se e solo se ogni coppia di ennuple in $r$ che coincide su $X$ coincide anche su $Y$.
Formalmente chiediamo $\forall t1, t2 \in r : t_1[X] = t_2[X] \implies t_1[Y] = t_2[Y]$.

### Definizione di implicazione
Sia $R(T, F)$ uno schema di relazione. Diciamo che $F$ *implica logicamente* la dipendenza funzionale $X \rightarrow Y$ , indicato con $F \vDash X \rightarrow Y$, se e solo se ogni istanza valida di $R(T, F)$ soddisfa anche $X \rightarrow Y$.

## Assiomi di Armstrong

Come possiamo dimostrare che $F \vDash X \rightarrow Y$ ? E’ una proprietà difficile da dimostrare, perché quantifica su tutte le possibili istanze valide.

Regole di inferenza della forma  $F\vdash$ $X\rightarrow Y$ :
$$REFL: \frac{Y \subseteq X}{F \vdash X \rightarrow Y} \ \ AUGM: \frac{F \vdash X \rightarrow Y}{F \vdash XW \rightarrow YW} \ \ TRANS: \frac{F \vdash X \rightarrow Y\ \ \ F \vdash Y \rightarrow X}{F \vdash X \rightarrow Z}$$
**Nota**:
* $\vDash$ : sempre vero, *assioma*
* $\vdash$ : potrebbe essere sbagliato se le regole sono sbagliate, *derivazione*

### Teorema
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
### Definizione di Chiusura di F
Dato un insieme $F$ di dipendenze funzionali, la *chiusura* di $F$ è definita come l'insieme $F^+ = \{X \rightarrow Y\ |\ F \vdash X \rightarrow Y\}$.
### Definizione Problema dell'implicazione
Il *problema dell'implicazione* corrisponde a decidere, dati $F$ e $X \rightarrow Y$ se  $X \rightarrow Y \in F^+$ oppure no.  

**Nota**: calcolare $F^+$ applicando gli assiomi di Armstrong ha costo *esponenziale* e pertanto è un modo *algoritmicamente inefficiente* per risolvere il problema dell'implicazione.
### Definizione chiusura di X 
Sia $R(T,F)$ uno schema di relazione.  Dato $X \subseteq T$, la *chiusura* di $X$ rispetto ad $F$ e definita come l'insieme $X_{F}^{+} = \{ A \in T\ | \ F \vdash X \rightarrow A\}$ .
### Teorema
$F \vdash X \rightarrow Y$ se e solo se  $Y \subseteq X^+_F$.
 
 $\color{red} \textbf{Dimostrazione}$
 * $(\implies)$ Da $F \vdash X \rightarrow Y$ abbiamo $\forall A \in Y : F \vdash X \rightarrow A$ per la regola di decomposizione. La conclusione deriva dalla definizione di $X^+_F$.
 * $(\impliedby)$  Da $Y \subseteq X^+_F$ abbiamo $\forall A \in Y : F \vdash X \rightarrow A$ per definizione di $X^+_F$.
 * La conclusione deriva dalla regola di unione
 
**Nota**: calcolare $F^+$ utilizzando il teorema appena descritto ha costo *polinomiale* e pertanto è *algoritmicamente efficiente*.

### Calcolo di $X^+_F$

![[Pasted image 20240214110454.png]]

### Valutazione della complessità
* Il *while* esterno viene eseguito al più $a$ volte.
* Il *for* interno viene eseguito al più $d$ volte.
* *Verificare l'inclusione di insiemi ordinati* di cardinalità al più $a$ nel *for* interno ha costo $O(a)$.
Pertanto la complessità totale dell'algoritmo è $O(a^2d)$.
# Chiavi e Copertura Canonica
___
## Chiavi e attributi primi
### Definizione di superchiave
Dato uno schema di relazione $R(T,F)$, un insieme di attributi $X \subseteq T$ è una *superchiave* di $R$  $\iff$ $X \rightarrow  T \in F^+$.
### Definizione di Chiave
Una *chiave* è una superchiave minimale, cioè una superchiave tale che nessuno dei suoi sottoinsiemi propri sia a sua volta una superchiave.
### Definizi0ne di attributi primi
Un attributo è *primo* $\iff$ appartiene ad almeno una chiave.

## Verifica di Superchiave

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
## Verifica di Chiave
Dato $R(T,F)$ possiamo verificare se $X \subseteq T$ è una *chiave* tramite il seguente algoritmo di costo *polinomiale*.
* Verifica se $X$ è una superchiave. Se non lo è non è una chiave
* Verifica che $\forall A \in X$ si abbia $X \\ \{A\}^+_F \neq T$

**Esempio**:
Si consideri la relazione $R(T,G)$ con $T = ABCDEF$ e $G = \{AB \rightarrow C,\ E \rightarrow A,\ A \rightarrow E,\ B \rightarrow F\}. \ ABD$ è chiave perchè esso è una superchiave (come dimostrato precedentemente) e inoltre abbiamo che
* $A$ non può essere rimosso: $BD^+_G = BDF$
* $B$ non può essere rimosso: $AD^+_G = ADE$
* $D$ non può essere rimosso: $AB^+_G = ABCEF$
## Trovare una chiave
Dato $R(T, F)$, è possibile trovare una sua chiave in tempo *polinomiale*. L’idea dell’algoritmo è di partire da $T$ e rimuovere uno ad uno tutti gli attributi che non sono indispensabili per derivare $T$.
## Algoritmo per trovare una Chiave

![[Pasted image 20240214112747.png]]

### Esempio
Sia $G = \{AB \rightarrow C,\ E \rightarrow A,\ A\rightarrow E,\ B\rightarrow F\}$.  Costruiamo una chiave:
* Inizializziamo $K_0 = ABCDEF$
* Rimuoviamo $A$ da $K_0:\ BCDEF^+_G = ABCDEF$ quindi $A$ deve essere rimosso e aggiorniamo la chiave $K_1 = BCDEF$
*  Rimuoviamo $B$ da $K_1:\ CDEF^+_G = ACDEF$ quindi $B$ va tenuto
* Rimuoviamo $C$ da $K_1:\ BDEF^+_G = ABCDEF$ quindi $C$ deve essere rimosso e aggiorniamo la chiave $K_2 = BDEF$
* Rimuoviamo $D$ da $K_2:\ BEF^+_G = ABCDEF$ quindi $D$ va tenuto
* Rimuoviamo $E$ da $K_2:\ BDF^+_G = BDF$ quindi $E$ va tenuto
* Rimuoviamo $F$ da $K_2:\ BDE^+_G = ABCDEF$ quindi $F$ deve essere rimosso e aggiorniamo la chiave $K_3 = BDE$
L'algoritmo ritorna la *chiave* $K_3 = BDE$ , è l'unica chiave? 

## Trovare l'Insieme delle Chiavi
Dato $R(T,F)$ trovare *tutte* le chiavi ha costo *esponenziale*, perché ogni sottoinsieme di $T$ è potenzialmente una chiave. Esiste però un algoritmo piuttosto ottimizzato per la ricerca di tutte le chiavi.

**Intuizione**:

* Generiamo le possibili chiavi dalle più piccole alle più grandi
* Rappresentiamo i candidati da testare nella forma $X\ ::\ (Y)$, dove $X$ è l'insieme degli attributi da testare come *chiave*, e $Y$ l'insieme dei possibili attributi da aggiungere a $X$ qualora $X^+_F \neq T$
* $X^+_F = T$, allora $X$ è una *chiave* e possiamo scartare $X\ ::\ (Y)$
* Altrimenti calcoliamo $Y\ \\ \ X^+_F = \{A_1 ... A_n\}$ e generiamo i nuovi candidati $XA_1\ ::\ (A_1 ... A_n)\ XA_2\ ::\ (A_3 ... A_n)...XA_n\ ::\ ()$

**Nota**: se un attributo non compare mai alla destra di una dipendenza funzionale, allora esso deve fare parte di tutte le chiavi. L’insiemi di tali attributi sarà il primo che testeremo.

### Algoritmo per trovare l'Insieme delle Chiavi

![[Pasted image 20240214114822.png]]
## Verifica di Primalità
Ad oggi non esiste un *algoritmo efficiente* per trovare tutte gli attributi primi se non *trovare tutte le chiavi*
## Forma Canonica
Abbiamo visto vari algoritmi che operano sull'*insieme delle dipendenze funzionali*. Per questo motivo è utile portare tale insieme ad una **forma canonica** equivavente all'origine
### Definizione di equivalenza
Due insiemi di dipendenza funzionale $F$ e $G$ sono **equivalenti**, indicato con $F \equiv G$ $\iff$ $F^+ = G^+$.
Se $F=G$ allora $F \equiv G$, ma **in generale non vale il contrario** 
### Definizione di Attributo Estraneno
Sia $X \rightarrow Y \in F$. L'attributo $A \in X$ è detto **estraneo** $\iff$ $X$ \\ $\{A\}  \rightarrow Y \in F^+$.
### Definizione di Dipendenza Ridondante
La dipendenza $X \rightarrow Y \in F$ è **ridondante** $\iff$ $X\rightarrow Y \in (F$ \\ $\{X\rightarrow Y\})^+$. 
### Definizione e Proprietà di Forma Canonica
La **forma canonica** è un metodo per scrivere un insieme di dipendenze funzionali equivalente, che ci permette di eseguire  vari algoritmi
**Proprietà**:
* $|Y| =1$
* $X$ non contiene *attributi estranei*
* $X \to Y$ non è *ridondante*
## Copertura Canonica
$G$ è **copertura canonica** di $F \iff F  \equiv G$ e $G$ è in forma canonica.
**Teorema**: per ogni insieme di dipendemze funzionali $F$ esiste una copertura canonica
### Algoritmo per determinare la copertura canonica
Segue 3 passi:
* Decompone tutte le dipendenze funzionali che hanno più attributi sulla destra $X \to Y \implies \{ X \to A | A \in Y\}$.
* Togliere dalla parte sinistra delle dipendenze gli attributi che non impediscono di derivare la dipendenza stessa. $X \to A \implies X$ \\ $Z | A \in (X$ \\ $Z)^+_F$.
* Togliere le dipendenze funzionali non essenziali per derivare la dipendenza stessa. $X \to A \implies F^{new} = F$ \\ $\{X \to A\} | A \in X^+_{F - \{X \to A \}}$.

![[Pasted image 20240219090819.png]]

**Esempio**:
Abbiamo $F \{A \to BC, B \to C, A \to B, AB \to C\}$:
* $G = \{A \to B, A \to C, B \to C, A \to B, AB \to C \}$.
* $\{AB\}$\\ $\{A\}^+_F = B^+_F = BC$, quindi  $G = \{A \to B, B \to C, A \to B, \color{green}B \to C \color{default}$\},  $\to$  *se a sinistra c'è un solo elemento rimane com'è*. $Z \leftarrow AB$,  $\to$ $(AB$ \\ $\{A\}^+_G) = B^+_G = BC$, $\to$ $Z = B$.
* Dobbiamo verificarle tutte: $(A^+_{G- \{A \to B\}} = AC$, $A^+_{G - \{A \to C\}} = ABC$ $\to$ *si può togliere*,  $B^+_{G - \{B \to C\}} = B) \implies G = \{A \to B, B \to C\}$  .
## Esercizi
* Usando gli **assiomi di Armstrong**, si dimostri che se $X \to Y$ e $YW \to Z$ allora $XW \to Z$.
$$_{TRANS}\frac{_{AUGM}\frac{F \vdash X \to Y}{F \vdash XW \to YW}\ \ \ \ F\vdash Z}{F \vdash XW \to Z}$$
* Si supponga che una dipendenza funzionale $X \to Y$ sia soddisfatta da due istanze di relazione $r$ ed $s$ con gli stessi attributi. Dire se $r \cap s$ e $r \cup s$ soddisfano $X \to Y$, fornendo una dimostrazione o un controesempio oppurtuni.
$$\forall t_1, t_2 \in r \iff t_1[x] = t_2[x]\ allora\ t_1[y] = t2[y]$$
$$Considero:\ (r \cap s) \forall t_1, t_2 \in r \cap s\ allora\ t_1,t_2 \in r$$
* Si consideri lo schema di relazione $R(A,B,C,D)$ con dipendenze $F = \{AB \to C, C \to D, D \to A\}$. Si trovino tutte le dipendenze non banali derivabili da $F$ e tutte le chiavi di $R$.
$$\frac{F \vdash X \to Y}{F \vdash X \to Z | Z \in \mathcal{P}(Y)}$$
$$\color{white} A \to A, C \to CDA, \to D \to DA, \color{green} AB \to ABCD \color{white}, AC \to ACD, AD \to AD,\color{green}BC \to BCDA \color{white},BD \to BDAC, CD \to CDA, ABC \to ABCD, ABD \to ABCD, ACD \to ACD, BCD \to ABCD$$

Ulteriori esercizi risolti al [seguente link](https://mega.nz/file/B3sUhBjS#9mDUkgxGb5tXJDyfJ6c1d-2qCti-GCZiO8YcLy4vFb0).
# Decomposizione di Schemi
___
## Anomalie
Schemi di scarsa qualità soffrono di **anomalie** che vanno ad ostacolare le operazioni di inserimento, cancellazione ed aggiornamento dei dati.

![[Pasted image 20240226155107.png]]
## Decomposizione di Schemi
L'eliminazione di anomalie è tipicamente basata sulla **decomposizione** di schemi *mal definiti* in schemi *più piccoli*, equivalenti ma più disciplinati

![[Pasted image 20240226155352.png]]
### Definizione di Proiezione
Dato uno schema $R(T,F)$ e $Z \subseteq T$, la **proiezione** di $F$ su $Z$ è definita come l'insieme $\pi_Z(F) = \{X \to Y \in F^+ | X \cup Y \subseteq Z\}$.
### Definizione di Decomposizione
Dato uno schema $R(T,F)$, una sua **decomposizione** è un insieme di schemi $\rho = \{R_1(T_1,F_1) ... R_n(T_n, F_n)\}$ tale che $\bigcup_i T_i = T, \forall i : T_i \neq \emptyset$ e $\forall i : F_i = \pi_{T_i}(F)$.

*Nota*: visto che gli $F_i$ sono determinati da $F$ e dai $T_i$ per **proiezione**, per leggibilità indicheremo una **decomposizione** di $R(T,F)$ con la notazione più compatta $\rho = \{R_1(T_1) ... R_n(T_n)\}$.

## Proprietà delle Decomposizioni
Sebbene decomporre uno schema possa correggere le **anomalie**, non tutte le decomposizioni sono desiderabili:

* **Perdita di informazione**: la decomposizione va ad introdurre dei *dati spuri*, che possono inficiare la correttezza di alcune query $\to$ (introduce *informazioni sbagliate*)
* **Perdita di dipendenze**: la decomposizione perde alcune *dipendenze funzionali*, andando ad alterare la semantica dei dati rappresentati

*Proprietà desiderabili*: una buona decomposizione dovrebbe eliminare le anomalie, ma preservare i dati e le dipendenze

## Decomposizioni con Perdita di Informazione

![[Pasted image 20240226162104.png]]

Facend0 la join fra le tabelle ottengo due possibili numeri di telefono

Qual è il numero di telefono del proprietario della macchina targata $CG153SE$?
* $\pi_{Telefono}(\sigma_{Macchina = CG153SE}(R)) = \{423567\}$
* $\pi_{Telefono}(\sigma_{Macchina = CG153SE}(R_1 \bowtie R_2)) = \{423567,542635\}$
## Decomposizioni che Preservano i Dati
In generale un'operazione di decomposizione può *introdurre nuovi dati*, come formalizzato dal seguente teorema.
### Teorema
Sia $\rho = \{R_1(T_1) ... R_n(T_n)\}$ una decomposizione di $R(T,F)$, allora per ogni istanza $r$ di $R(T,F)$ si ha $r = \pi_{T_1})(r) \bowtie ... \bowtie \pi_{T_n}(r)$.

Una decomposizione **preserva i dati** ( non perde informazione) quando ciò non si verifica.
### Definizione di Decomposizione che Preserva i Dati
La decomposizione $\rho = \{R_1(T_1) ... R_n(T_n)\}$ di $R(T,F)$ **preserva i dati** $\iff$ per ogni istanza $r$ di $R(T,F)$ si ha $r = \pi_{T_1})(r) \bowtie ... \bowtie \pi_{T_n}(r)$.

### Teorema per verificare se una decomposizione preserva i dati
Sia $\rho = \{R_1(T_1), R_2(T_2)\}$ una decomposizione di $R(T,F)$, si ha che $\rho$ preserva i dati $\iff T_1 \cap T_2 \to T_1 \in F^+$ oppure $T_1 \cap T_2 \to T_2 \in F^+$.

Questo permette di ricondurre il problema di determinare se una certa decomposizione binaria preserva i dati al *problema dell'implicazione*, che ha costo **binomiale**.
#### Dimostrazione
Sia $\rho = \{R_1(T_1), R_2(T_2)\}$ una decomposizione di $R(T,F)$, dimostriamo che se $T_1 \cap T_2 \to T_1 \in F^+$ allora $\rho$ conserva i dati:
* Sia $r$ un'istanza valida di $R(T,F)$ e $s = (\pi_{T_1}r) \bowtie (\pi_{T_2}r)$, dobbiamo dimostrare che per ogni $t \in s$ abbiamo anche $t \in r$. $\to$ (che ogni riga di $r$ sia in $s$ e viceversa, dove $r$ è la tabella iniziale e $s$ l'unione delle due proiezioni $T_1$ e $T_2$).
* Per definizione di $s$ esistono due tuple $u,v \in r$ con $u[T_1] = t[T_1],\ v[T_2] = t[T_2]$ e $u[T_1 \cap T_2] = v[T_1 \cap T_2] = t[T_1 \cap T_2]$.
* Poiché $T_1 \cap T_2 \to T_1 \in F^+$, da $u[T_1 \cap T_2] = v[T_1 \cap T_2]$ otteniamo $u[T_1] = v[T_1]$ e quindi $t = v \in r$.
Il caso $T_1 \cap T_2 \to T_2 \in F^+$ è analogo.

Se: $$\frac{t \in s \to t \in v}{\exists u,v \in r\ |\ u[T_1] = t[T_1],\ v[T_2] = t[T_2]}$$ $$u[T_1 \cap T_2] = t[T_1 \cap T_2]$$ $$v[T_1 \cap T_2] = t[T_1 \cap T_2] \overset{per\ ipotesi}\to v[T_1] = t[T_1]$$ quindi $u = t$.

### Esempio
Si consideri $R(A,B,C,D)$ con $F = \{A \to BC\}$.
La decomposizione binaria $\{R_1(A,B,C), R_2(A,D)\}$ *preserva i dati*:
* $T_1 = \{A,B,C\}$ e $T_2 = \{A,D\}$
* $T_1 \cap T_2 = \{A\}$
* $A^+_F = \{A,B,C\} = T_1$ quindi $T_1 \cap T_2 \to T_1 \in F^+$$\to$ (vedo se $A^+_F$ dipende da $T_1 \cap T_2$)

![[Pasted image 20240226170943.png]]
### Esempio 2
Si consideri $R(A,B,C,D)$ con $F = \{A \to B, C \to D\}$.
La decomposizione binaria $\{R_1(A,B), R_2(C,D)\}$ *non preserva i dati*:
* $T_1 = \{A,B\}$ e $T_2 = \{C,D\}$
* $T_1 \cap T_2 = \emptyset$
* Abbiamo quindi $\{T_1 \cap T_2 \to T_1, T_1 \cap T_2 \to T_2\} \cap F^+ = \emptyset$

![[Pasted image 20240226172306.png]]
## Decomposizioni con perdita di dipendenze

![[Pasted image 20240226172426.png]]
*Nota*: la macchina può avere un solo proprietario.

Supponiamo di voler inserire (Luca Bianchi, $421448$, $CG153SE$)
* Nel primo caso violerei la dipendenza Macchina $\to$ Proprietario (avremo cioè la stessa macchina con due proprietari)
* Nel secondo caso non me ne posso accorgere se non dopo giunzione.
## Decomposizioni che Preservano le Dipendenze
Una decomposizione **preserva le dipendenze** $\iff$ l'unione delle dipendenze indotte sui singoli schemi equivale (cioè ha le stesse chiusure) alle dipendenze dello schema originale.
### Definizione di Decomposizione che Preserva Le Dipendenze
La decomposizione $\rho = \{R_1(T_1) ... R_n(T_n)\}$ di $R(T,F)$ **preserva le dipendenze** $\iff \bigcup_i \pi_{T_i}(F) \equiv F$.

Per *verificarlo algoritmicamente* applichiamo la definizione:
* Calcoliamo le proiezioni $\pi_{T_i}(F) = \{X \to Y \in F^+\ |\ X \cup Y \subseteq T_i\}$
* Verifichiamo se $\bigcup_i \pi_{T_i}(F) \equiv F$
## Verificare l'Equivalenza
### Teorema
$F \equiv G \iff F \subseteq G^+$ e $G \subseteq F^+$.
#### Dimostrazione
* Sia $F \equiv G$ allora $F^+ = G^+$ per definizione. Dato che si ha $F \subseteq F^+$ e $G \subseteq G^+$, ottengo $F \subseteq G^+$ e $G \subseteq F^+$ come desiderato.
* Poiché $F \subseteq G^+$, osservo che $F^+ \subseteq (G^+)^+ = G^+$. Analogamente da $G \subseteq F^+$ ottengo $G^+ \subseteq (F^+)^+ = F^+$. Concludo che $F^+ = G^+$.
### Teorema
$F \equiv G \iff F \subseteq G^+$ e $G \subseteq F^+$.
Sia $G = \bigcup_i \pi_{T_i}(F)$, per dimostrare che $F \equiv G$ osserviamo che:
* $F \subseteq G^+$ è verificabile  tramite il *problema dell'implicazione*, perché equivale a verificare che $\forall X \to Y \in F$ abbiamo $Y \subseteq X^+_G$
* $G \subseteq F^+$ vale per definizione, quindi non serve neppure verificarlo
Ci manca quindi solo da calcolare $G = \bigcup_i \pi_{T_i}(F)$ per avere un algoritmo che verifica se le dipendenze sono verificate o meno.
## Calcolo delle Proiezioni
Non è possibile calcolare $G = \bigcup_i \pi_{T_i}(F)$ in modo efficiente, perché il calcolo delle singole proiezioni $\pi_{T_i}(F)$ ha costo **esponenziale**.

![[Pasted image 20240226174736.png]]

## Riassunto
Alla luce di quanto discusso, possiamo verificare se la decomposizione $\rho = \{R_1(T_1) ... R_n(T_n)\}$ di $R(T,F)$ preserva le dipendenze tramite il seguente algoritmo:
* Calcola le proiezioni $\pi_{T_1}(F)$ per ogni $i \in [1,n]$
* Calcola $G = \bigcup_i \pi{T_i}(F)$
* Verifica che per ogni $X \to Y \in F$ si abbia $Y \subseteq X^+_G$
Tale algoritmo ha costo **esponenziale** a causa del calcolo delle proiezione.
### Esempio
Siano $R(A,B,C)$ e $F = \{A \to B, B \to C, C \to A\}$. Vogliamo verificare se la decomposizione $\rho = \{R_1(A,B), R_2(B,C)\}$ preserva le dipendenze.

Calcoliamo $\pi_{AB}(F)$, considerando i due sottoinsiemi propri $A$ e $B$.
* $A^+_F = ABC$, quindi $B \to C \in \pi_{AB}(F)$
* $B^+_F = BCA$, quindi $B \to A \in \pi_{AB}(F)$
Concludiamo quindi $\pi_{AB}(F) = \{A \to B, B \to A\}$.

Calcoliamo ora $\pi_{BC}(F)$ considerando i due sottoinsiemi propri $B$ e $C$:
* $B^+_F = BCA$ quindi $B \to C \in \pi_{BC}(F)$
* $C^+_F = CAB$ quindi $C \to B \in \pi_{BC}(F)$
Concludiamo quindi $\pi_{BC}(F) = \{B \to C, C \to B\}$

A questo punto possiamo calcolare: $$G = \pi_{AB}(F) \cup \pi_{BC}(F) = \{A \to B, B \to A, B \to C, C \to B\}$$ Iteriamo sulla dipendenza $F = \{A \to B, B \to C, C \to A\}$ e verifichiamo che siano tutte derivabili da $G$:
* $A \to B$: abbiamo $B \in A^+_G = ABC$
* $B \to C$: Abbiamo $C \in B^+_G = BAC$
* $C \to A$: abbiamo $A \in C^+_G = CBA$
Concludiamo che la decomposizione in esame preserva le dipendenze.
## Ottimizzare la verifica
Per fortuna non ci interessa davvero calcolare $G = \bigcup_i \pi_T{T_i}(F)$, ma ci basta verificare che per ogni $X \to Y \in F$ abbiamo $Y \subseteq X^+_G$. In effetti esiste un algoritmo che calcola $X^+_G$ in tempo **polinomiale** senza calcolare $G$.

![[Pasted image 20240226181722.png]]

Dati uno schema $R(T,F)$ e $\rho = \{R_1(T_1) ... R_n(T_n)\}$ è quindi possibile verificare se $\rho$ preserva le dipendenze tramite il seguente algoritmo di complessità **polinomiale**.

![[Pasted image 20240228103632.png]]
### Esempio

$F = \{A \to B, B \to C, C \to A\}$ e $\rho = \{R_1(A,B), R_2(B,C)\}$

Partiamo dalla dipendenza $A \to B$:
* Partiamo inizializzando $FC(A,F,\rho) = \{A\}$
* Consideriamo $R_1(\{A,B\})$, abbiamo: $(\{A\} \cap \{A,B\})^+_F \cap \{A,B\} = A^+_F \cap \{A,B\} = \{A,B\}$, quindi aggiungiamo $B$ a $FC(A,F,\rho)$
* Consideriamo $R_2(\{B,C\})$, abbiamo: $(\{A,B\} \cap \{B,C\})^+_F \cap \{B,C\} = B^+_F \cap \{B,C\}  )= \{B,C\}$, quindi aggiungiamo $C$ a $FC(A,F,\rho)$
* Otteniamo quindi $B \in FC(A,F,\rho) = \{A,B,C\}$

Passiamo alla dipendenza$B \to C$:
* Partiamo inizializzando $FC(B,F,\rho) = \{B\}$
* Consideriamo $R_1(\{A,B\})$, abbiamo: $(\{B\} \cap \{A,B\})^+_F \cap \{A,B\} = B^+_F \cap \{A,B\} = \{A,B\}$, quindi aggiungiamo $A$ ad $FC(B,F,\rho)$
* Consideriamo $R_2(\{B,C\})$, abbiamo: $(\{A,B\} \cap \{B,C\})^+_F \cap \{B,C\} = B^+_F \cap \{B,C\} = \{B,C\}$, quindi aggiungiamo $C$ ad $FC(B,F,\rho)$
* Otteniamo quindi $C \in FC(B,F,\rho) = \{A,B,C\}$

Passiamo alla dipendenza $C \to A$:
* Passiamo inizializzando $FC(C,F,\rho) = \{C\}$
* Consideriamo $R_1(\{A,B\})$, abbiamo: $(\{C\} \cap \{A,B\})^+_F \cap \{A,B\} = \emptyset$ quindi per ora non aggiungiamo niente a $FC(C,F,\rho)$
* Consideriamo  $R_2(\{B,C\})$,abbiamo: $(\{C\} \cap \{B,C\})^+_F \cap \{B,C\} = C^+_F \cap \{B,C\} = \{B,C\}$, quindi aggiungiamo  $B$ ad $FC(C,F,\rho)$
* Consideriamo $R_1(\{A,B\})$, abbiamo: $(\{B,C\} \cap \{A,B\})^+_F \cap \{A,B\} = B^+_F \cap \{A,B\} = \{A,B\}$ quindi aggiungiamo $A$ ad $FC(C,F,\rho)$
* Otteniamo quindi $A \in FC(C,F,\rho) = \{A,B,C\}$
## Teorema
In generale la preservazione dei dati è **indipendente** dalla preservazione delle dipendenze. Esiste però un teorema che collega le due proprietà, che è particolarmente utile perché applicabile a decomposizioni non binarie.

**Teorema**: Sia $\rho = \{R_1(T_1) ... R_n(T_n)\}$ una decomposizione di $R(T,F)$ che preserva le dipendenze e tale che almeno uno degli insiemi $T_j$ sia una superchiave per $R(T,F)$, allora $\rho$ preserva anche i dati.
# Forme Normali
___
## Introduzione
L'obbiettivo delle forme normali è garantire che uno schema sia di buona qualità e viene spesso ottenuto tramite un processo di **normalizzazione** basato su una decomposizione dello schema di partenza.

**Proprietà desiderabili**: 
* Uno schema in forma normale non deve contenere anomalie
* Il processo di normalizzazione deve preservare i dati
* Il processo di normalizzazione deve preservare le dipendenze
## Forma Normale di Boyce-Codd(BCNF)
### Definizione
Uno schema di relazione $R(T,F)$ è in BCNF $\iff$ per ogni dipendenza funzionale $X \to Y \in F^+$ tale che $Y \nsubseteq X$ si ha che $X$ è una superchiave.

Verificare se uno schema è in BCNF ha costo **polinomiale**.
#### Esempio
Si consideri $Prodotti(\{Articolo,\ Magazzino,\ Quantità,\ Indirizzo\},\ F)$ con $F = \{Articolo\ Magazzino \to Quantità, Magazzino \to Indirizzo\}$. Dato che $\{Magazzino\}^+_F = \{Magazzino,\ Indirizzo\}$, lo schema non è in BCNF.
### Dipendenze Anomale
Una dipendenza che viola BCNF è detta **anomala**. Nel nostro esempio abbiamo una dipendenza anomala $Magazzinio \to Indirizzo$.

![[Pasted image 20240228112020.png]]

Tale dipendenza anomala evidenzia che lo schema mescola informazioni relative ai magazzini con alte **indipendenti** relative agli articoli.
### Conversione in BCNF
L'algoritmo di conversione in BCNF è detto anche **algoritmo di analisi**, perché decompone lo schema originale fino a normalizzazione.

Sia $R(T,F)$ lo schema di partenza:
* Se $R(T,F)$ è già in BCNF, ritorna $\{R(T,F)\}$
* Altrimenti seleziona $X \to Y \in F$ che viola BCNF. Calcola gli insiemi di attributi $T_1 = X^+_F$ e $T_2 = X \cup (T$ \\ $T_1)$
* Calcola le proiezioni $F_1 = \pi_{T_1}(F)$ e $F_2 = \pi_{T_2}(F)$
* Decomponi ricorsivamente $R_1(T_1,F_1)$ e $R_2(T_2,F_2)$ in $\rho_1$ e $\rho_2$
* Ritorna la loro unione $\rho_1 \cup \rho_2$
#### Esempio
Si consideri $Telefoni(\{Prefisso,\ Numero,\ Località\},\ F)$ con $$F =\{Prefisso\ Numero \to Località,\ Località \to Prefisso\}$$
La dipendenza $Località \to Prefisso$ viola BCNF, dato che: $$\{Località\}^+_F = \{Località,\ Prefisso\}$$
Applicando l'algoritmo di conversione in BCNF, abbiamo:
* $R_1(\{Località,\ Prefisso\},\ F_1)$ con $F_1$ da calcolare per proiezione
* $R_2(\{Località,\ Numero\},\ F_2 )$ con $F_2$ da calcolare per proiezione

Dato $F =\{Prefisso\ Numero \to Località,\ Località \to Prefisso\}$

calcoliamo la sua proiezione per $R_1(\{Località,\ Prefisso\})$:
* $\{Località\}^+_F = \{Località,\ Prefisso\}$, da cui $Località \to Prefisso \in F_1$
* $\{Prefisso\}^+_F = \{Prefisso\}$, da cui nessuna nuova dipendenza

Calcoliamo poi la sua proiezione per $R_2(\{Località,\ Numero\})$:
* $\{Località\}^+_F = \{Località,\ Prefisso\}$, da cui nessuna nuova dipendenza
* $\{Numero\}^+_F = \{Numero\}$, da cui nessuna nuova dipendenza

Abbiamo quindi $F_1 = \{Località \to Prefisso\}$ e $F_2 = \emptyset$.

Abbiamo deomposto $Telefoni(\{Prefisso,\ Numero,\ Località\},\ F)$ con $$F =\{Prefisso\ Numero \to Località,\ Località \to Prefisso\}$$
nei seguenti schemi:
* $R_1(\{Località,\ Prefisso\}, \{Località \to Prefisso\})$
* $R_2(\{Località,\ Numero\}, \emptyset)$

Entrambi gli schemi sono in BCNF, ma è andata perduta la dipendenza funzionale $Prefisso\ Numero \to Località$.
### Perdita di dipendenze

![[Pasted image 20240228114338.png]]
Dato lo stesso $Prefisso$ e $Numero$ avremmo due $Località$ **differenti**.
### Correttezza della Conversione in BCNF
L'algoritmo di conversione in BCNF *termina* quando non ci sono più dipendenze anomale. Per garantire che ciò avverrà, dimostriamo che tutti gli schemi **con solo due attributi** sono in BCNF.

Consideriamo $R(\{A,B\},F)$ e sia $X \to Y \in F$. Dimostriamo che in nessun caso viene violata BCNF:
* Se $X = \{A\}$ ho due casi:
	* Se $B \notin Y$, allora $Y \subseteq X$ e la dipendenza è *banale*.
	* Se $B \in Y$, allora $X$ è una *superchiave*.
* Se $X = \{B\}$, il caso è simmetrico al precedente.
* Se $X = \{A,B\}$, allora $Y \subseteq X$ e la dipendenza è *banale*.
### La Conversione in BCNF Preserva i Dati
Supponiamo che $R(T,F)$ sia decomposto in $\{R_1(T_2),\ R_2(T_2)\}$, allora deve esistere $X \to Y \in F$ che viola BCNF. Per costruzione $T_1 = X^+_F$ e $T_2 = X \cup (T$ \\ $T_1)$.

Osserviamo che $T_1 \cap T_2 = X$. Dato che $X \to X^+_F \in F^+$, abbiamo che $T_1 \cap T_2 \to T_1 \in F^+$, quindi la decomposizione preserva i dati per il teorema visto precedentemente.

Il risultato si può quindi dimostrare **per induzione** sul numero di passi effettuati dall'algoritmo di conversione in BCNF
### Proprietà di BCNF

**Pregi**:
* BCNF garantisce l'**assenza di anomalie** (niente dipendenze anomale)
* L'algoritmo di conversione in BCNF **preserva i dati**
* Verificare se uno schema è in BCNF ha costo **esponenziale**

**Difetti**:
* L'algoritmo di conversione in BCNF ha costo **esponenziale**, perché richiede di calcolare le proiezioni delle dipendenze.
* L'algoritmo di conversione in BCNF **non preserva le dipendenze** nel caso generale.
## Terza Forma Normale(3NF)
### Definizione
Uno schema di relazione $R(T,F)$ è in **3NF** $\iff$ per ogni dipendenza funzionale $X \to Y \in F^+$ tale che $Y \nsubseteq X$ si ha che $X$ è una *superchiave* oppure gli attributi di $X$ \\ $Y$ sono primi.

Verificare se uno schema è in 3NF ha costo **esponenziale**.

*Osservazione*: per definizione ogni schema in BCNF è anche in 3NF ma non viceversa.
## Esempio
Si consideri $Telefoni(\{Prefisso,\ Numero,\ Località\},\ F)$ con $$F = \{Prefisso\ Numero \to Località,\ Località \to prefisso\}.$$
Calcoliamo le chiavi, osservando che $Numero$ deve fare parte di tutte:
* $\{Numero\}^+_F = \{Numero\}$
* $\{Numero,\ Prefisso\}^+_F = \{Numero,\ Prefisso,\ Località\}$
* $\{Numero,\ Località\}^+_F = \{Numero,\ Località,\ Prefisso\}$

Dato che $\{Numero,\ Prefisso\}$ e $\{Numero,\ Località\}$ sono chiavi, si ha che ogni attributo è *primo*, e quindi lo schema è in 3NF.
### Conversione in 3NF
L'algoritmo di conversione in 3NF è anche detto **algoritmo di sintesi**, perché basato sulla generazione di nuovi schemi più piccoli.

Sia $R(T,F)$ lo schema di partenza:
* Costruisci $G$, una copertura canonica di $F$.
* Sostituisci in $G$ ciascun insieme di dipendenze $X \to A_1, ..., X \to A_n$
* Per ogni $X \to Y \in G$ crea un nuovo schema $S_i(XY)$
* Elimina ogni schema contenuto in un altro schema
* Se la decomposizione non contiene alcuno schema i cui attributi costituiscano una superchiave per $R$, aggiungi un nuovo schema $S(W)$ dove $W$ è una chiave di $R$ (*garantisce la preservazione dei dati*).
### Esempio
Sia $R(\{A,B,C,D\},\ \{AB \to C,\ C \to D,\ D \to E\})$, osserviamo che l'insieme delle dipendenze è già in forma canonica. Otteniamo quindi:
* $R_1(\{A,B,C\})$ tramite $AB \to C$
* $R_2(\{C,D\})$ tramite $C \to D$
* $R_3(\{B,D\})$ tramite $D \to B$

Nessuno schema è contenuto in un altro, quindi nessuno di essi viene eliminato. Poiché $\{A,B,C\}$ è una superchiave di $R$, non è necessario aggiungere altri schemi.
### La conversione in 3NF Preserva i Dati e le Dipendenze
#### Preservazione delle dipendenze
Poiché per ogni $X \to Y \in G$ viene creato uno schema $S_i(XY)$, abbiamo $X \to Y \in \pi_{XY}(G)$, quindi $G$ è contenuto nell'unione delle proiezioni.
#### Preservazione dei dati
L'ultimo passo della conversione in 3NF garantisce che la decomposizione contenga almeno uno schema i cui attributi formano una superchiave dello schema iniziale. Poiché la decomposizione preserva le dipendenze, essa deve preservare anche i dati per il teorema visto.
### 3NF ed Anomalie
Si consideri $Telefoni(\{Prefisso,\ Numero,\ Località\},\ F)$ con $$F = \{Prefisso\ Numero \to Località,\ Località \to Prefisso\}.$$
Abbiamo già visto che lo schema è in 3NF, ma non garantisce l'assenza di **anomalie**. In particolare si noti la *replicazione del prefisso*:

![[Pasted image 20240304091615.png]]
### Proprietà di 3NF
**Pregi**:
* L'algoritmo di conversione in 3NF **preserva i dati e le dipendenze**.
* L'algoritmo di conversione in 3NF ha costo **polinomiale**, perché non richiede il calcolo delle proiezioni.

**Difetti**:
* Verificare se uno schema è in 3nF ha costo **esponenziale**, perché richiede di identificare gli attributi primi.
* Uno schema in 3NF può ancora contenere **anomalie**.
### Strategie per Schemi di Scarsa Qualità
#### Strategia 1
Convertiamo lo schema in BCNF per eliminare le anomalie. Se notiamo che la conversione non ha preservato le dipendenze, ci accontentiamo di una conversione in 3NF
#### Strategia 2
Convertiamo lo schema in 3NF in modo da preservare dati e dipendenze, sperando di essere fortunati e rimuovere tutte le anomalie. Questo di verifica in particolare se la conversione produce in realtà BCNF.
### Dipendenze Multivalore
Una nuova forma di anomalie non prevenuta neppure da BCNF si può verificare in presenza di **attributi moltivalore indipendenti**. Per esempio la relazione sottostante non ha dipendenze funzionali non banali.

![[Pasted image 20240304092458.png]]
C'è però una forte ridondanza: se ci sono $m$ docenti e $n$ libri di testo, si memorizzano $m \times n$ righe.
### Dipendenze Multivalore
Si può fare di meglio, memorizzando solo $m + n$ righe.

![[Pasted image 20240304092900.png]]

La teoria della normalizzazione è stata perciò generalizzata per rimuovere anche questo tipo di anomalie dovute **dipendenze multivalore** (4NF).
## Esercizi
# Vincoli di Integrità
___
## Introduzione
Molto spesso i dati salvati all'interno di un database devono soddisfare determinati **vincoli di integrità** dipendenti dalla semantica dei dati.
* Garantire che certi attributi abbiano sempre un valore $\to$ (NOT NULL)
* Garantire che un certo insieme di attributi sia una chiave $\to$ (PRIMARY KEY, UNIQUE)
* Garantire l'integrità referenziale $\to$ (vincoli su FOREIGN KEY)
* Garantire determinati vincoli sui valori degli attributi, anche in relazione fra loro.

**Esempi**:
* Garantire che l'età di una persona sia sempre un numero positivo
* Garantire che il primario di un ospedale sia anche un dottore.
## NOT NULL
Il più semplice vincolo che possiamo esprimere è che un certo attributo non deve mai essere impostato a **NULL**.

**Esempio**:
```SQL
CREATE TABLE Movies (
	title    CHAR(100) NOT NULL,
	year     INT,
	lenght   INT,
	genre    CHAR(10)
)
```

## Chiavi -UNIQUE
Data una tabella $R(T)$ ed un insieme di attributi $X \subseteq T$, possiamo specificare che *nessuna coppia di tuple in $R(T)$ coincida su tutti gli attributi in $X$*, a meno che almeno uno di essi non sia NULL.

**Esempio**:
```SQL
CREATE TABLE Movies(
	title    CHAR(100) NOT NULL,
	year     INT,
	lenght   INT,
	genre    CHAR(10),
	UNIQUE (title, year)
)
```
*Nota*: se riguarda un singolo attributo può essere dichiarata anche in-line

## PRIMARY KEY
Il vincolo **PRIMARY KEY** si comporta come UNIQUE  ma impone in aggiunta il vincolo NOT NULL per tutti gli attributi specificati.

**Esempio**:
```SQL
CREATE TABLE Movies(
title    CHAR(100),
year     INT,
lenght   INT,
genre    CHAR(10),
PRIMARY KEY (title, year)
)
```
*Nota*: se riguarda un singolo attributo può essere dichiarata anche in-line
## FOREIGN KEY
Dati una tabella $R(T)$ ed $X \subseteq T$, possiamo specificare un vincolo di **integrità referenziale** secondo cui $X$ è una **chiave esterna** di $R(T)$:
* Il vincolo deve riferire una tabella $S(U)$ ed un insieme di attributi in $Y \subseteq U$, dichiarati PRIMARY KEY o UNIQUE
* per ogni tupla $t \in R(T)$ tale che tutti gli attributi in $X$ sono diversi da NULL, deve esistere una tupla $t' \in S(U)$ tale che $T[X] = t'[Y]$

*Nota*: implicitamente richiediamo $|X| = |Y|$

Possiamo indicare che un attributo è una chiave esterna subito dopo la dichiarazione dello stesso:
```SQL
REFERENCES <table> (<attribute>)
```

oppure alla fine di tutte le dichiarazioni:
```SQL
FOREIGN KEY (<attributes>) REFERENCES <table> (<attributes>)
```

**Esempio**:
```SQL
CREATE TABLE MovieExec(
	name      CHAR(50),
	address   VARCHAR(255),
	code      INT PRIMARY KEY,
	netWorth  INT
)

CREATE TABLE Studio(
	name      CHAR(30) PRIMARY KEY,
	address   VARCHAR(255),
	president INT,
	FOREIGN KEY (president) REFERENCES MovieExec(code)
)
```

In questo caso *è possibile avere uno studio senza presidente* ma *non è possibile avere un presidente che non sia anche un produttore esecutivo*.
## Mantenimento dell'Integrità Referenziale
```SQL
CREATE TABLE MovieExec(
	name      CHAR(50),
	address   VARCHAR(255),
	code      INT PRIMARY KEY,
	netWorth  INT
)

CREATE TABLE Studio(
	name      CHAR(30) PRIMARY KEY,
	address   VARCHAR(255),
	president INT,
	FOREIGN KEY (president) REFERENCES MovieExec(code)
)
```

Le seguenti operazioni su `Studio` sono **impedite**:
* Inserimento di una tupla il cui attributi `president` non è NULL e non coincide con l'attributo `code` di una tupla in `MovieExec`.
* Aggiornamento di una tupla per cambiare il suo attributo `president` ad un valore non NULL che non coincide con l'attributo `code` di una tupla in `MovieExec`.
* Ci sono ulteriori casi problematici.

Le seguenti operazioni su `MovieExec` sono **pericolose**:
* Cancellazione di una tupla il cui attributo `code` coincide con l'attributo `president` di qualche tupla in `Studio`.
* Aggiornamento di una tupla per cambiare il suo attributo `code` in modo tale che non coincida più con l'attributo `president` di qualche tupla in `Studio`.

Questi casi possono essere gestiti tramite diverse **politiche di integrità**.
## Politiche di Integrità Referenziale
SQL mette a disposizione tre politiche per gestire i due casi descritti:
* **Default**: rifiuta la modifica.
* **CASCADE**: applica la stessa modifica (DELETE o UPDATE) sulle tuple che fanno uso della chiave esterna.
* **SET NULL**: imposta la chiave esterna a NULL sulle tuple che fanno uso della stessa.

*Nota*: possiamo specificare una politica diversa per DELETE e UPDATE, utilizzando la sintassi ON DELETE oppure ON UPDATE seguito da CASCADE oppure SET NULL.

**Esempio**:
```SQL
CREATE TABLE Studio(
	name      CHAR(30) PRIMARY KEY,
	address   VARCHAR(255),
	president INT,
	FOREIGN KEY (president) REFERENCES MovieExec(code)
		ON DELETE SET NULL
		ON UPDATE CASCADE
)
```
## CHECK su Attributi
Possiamo specificare vincoli complessi sul valore di un attributo usando la sintassi **CHECK** seguita da un'espressione booleana fra parentesi:
* Si può utilizzare qualsiasi espressione ammessa da WHERE.
* Secondo lo standard SQL si possono riferire altre relazioni tramite sotto-query, ma questo non è supportato nei DBMS commerciali (Postgres).
* Il vincolo è controllato ogni volta che una tupla assume un nuovo valore per quell'attributo (INSERT o UPDATE).

*Nota*: questo **non è necessariamente sufficiente** a garantire che il vincolo non sia mai violato.

**Esempio 1**:
```SQL
CREATE TABLE MovieExec(
	name      CHAR(50),
	address   VARCHAR(255),
	code      INT PRIMARY KEY CHECK (code >= 100000),
	netWorth  INT
)

CREATE TABLE Studio(
	name      CHAR(30) PRIMARY KEY,
	address   VARCHAR(255),
	president INT,
	FOREIGN KEY (president) REFERENCES MovieExec(code)
)
```

**Esempio 2**:
```SQL
CREATE TABLE Studio(
	name      CHAR(30) PRIMARY KEY,
	address   VARCHAR(255),
	president INT,
	FOREIGN KEY (president) REFERENCES MovieExec(code)
)
```

```SQL
CREATE TABLE Studio(
	name      CHAR(30) PRIMARY KEY,
	address   VARCHAR(255),
	president INT CHECK (president in (SELECT
									   FROM MovieExec))
)
```
La seconda forma offre meno garanzie della prima! Se una entry di `MovieExec`cambia il valore di `code`:
* Nel primo caso possiamo usare una politica di integrità referenziale.
* Nel secondo caso non è possibile garantire integrità referenziale, perché `Studio` non viene toccata.
## CHECK su Tuple
SQL permette di specificare anche vincoli sull'intera tupla piuttosto che sul singolo attributo. Le considerazioni sulla sintassi e sulla semantica sono sostanzialmente le stesse del caso precedente.

```SQL
CREATE TABLE MovieExec(
	name      CHAR(50),
	address   VARCHAR(255),
	code      INT PRIMARY KEY,
	netWorth  INT,
	CHECK (code >= 100000 AND netWorth >= 0)
)
```
*Nota*: in questo semplice esempio avremmo potuto usare anche due CHECK su attributi, che sono potenzialmente più efficienti.
## CHECK su Attributi o su Tuple?
* Se un vincolo coinvolge più di un attributo e non è una congiunzione di vincoli su attributi indipendendi, è **necessario ricorrere a CHECK su tuple** per motivi di espressività.
* Se un vincolo coinvolge un solo attributo, **possiamo scegliere fra i due tipi** ma i *CHECK su attributi sono più efficienti dei CHECK su tuple* dato che devono essere controllati meno di frequente.

**Reminder**:
* $A \implies B$ equivale a $\lnot A \lor B$
* $\lnot(A \land B)$ equivale a $\lnot A \lor \lnot B$
* $\lnot (A \lor B)$ equivale a $\lnot A \land \lnot B$
## Equivalenze Logice
Come garantire che **tutti** coloro che soddisfano la proprietà $A$ devono soddisfare la proprietà $B$?
* Logicamente equivalente a $A \implies B$.
* Esprimere quindi equivalentemente con $\lnot A \lor B$.

Come garantire che **solo** coloro che soddisfano la proprietà $A$ possono soddisfare la proprietà $B$?
* Logicamente equivalente a $B \to A$.
* Esprimibile quindi equivalente con $\lnot B \lor A$.
## Aggiornare i Vincoli
Possiamo dare un nome ai vincoli anteponendo alla loro dichiarazione la dicitura, questo ci permette di eliminarli in seguito:
```SQL
CONSTRAINT NomeV [FOREIGN KEY, UNIQUE, CHECK, etc.]...
```

Possiamo **cancellare** un vincolo esistente a partire dal suo nome:
```SQL
ALTER TABLE NomeT DROP CONSTRAINT NomeV
```

Possiamo **inserire** un nuovo vincolo, ricorrendo alla sintassi:
```SQL
ALTER TABLE NomeT ADD [CONTRAINT NomeV] DefV
```

Il vincolo *deve già valere* sulla tabella al momento del suo inserimento. Questa caratteristica è molto desiderabile nella pratica
La **modifica** di un vincolo non è supportata, ma può essere effettuata tramite una cancellazione seguita da un inserimento.