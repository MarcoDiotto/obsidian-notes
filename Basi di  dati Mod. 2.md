
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

## Algoritmo per trovare l'Insieme delle Chiavi

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
Uno schema di relazione $R(T,F)$ è in **3NF** $\iff$ per ogni dipendenza funzionale $X \to Y \in F^+$ tale che $Y \nsubseteq X$ si ha che $X$ è una *superchiave* oppure gli attributi di $X$ \\ $Y$ sono primi.

Verificare se uno schema è in 3NF ha costo **esponenziale**.

*Osservazione*: per definizione ogni schema in BCNF è anche in 3NF ma non viceversa.
## Esempio
Si consideri $Telefoni(\{Prefisso,\ Numero,\ Località\},\ F)$ con $$F = \{Prefisso,\ Numero \to Località,\ Località \to Prefisso\}.$$
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
Convertiamo lo schema in 3NF in modo da preservare dati e dipendenze, sperando di essere fortunati e rimuovere tutte le anomalie. Questo verifica in particolare se la conversione produce in realtà BCNF.
### Dipendenze Multivalore
Una nuova forma di anomalie non prevenuta neppure da BCNF si può verificare in presenza di **attributi moltivalore indipendenti**. Per esempio la relazione sottostante non ha dipendenze funzionali non banali.

![[Pasted image 20240304092458.png]]
C'è però una forte ridondanza: se ci sono $m$ docenti e $n$ libri di testo, si memorizzano $m \times n$ righe.
### Dipendenze Multivalore
Si può fare di meglio, memorizzando solo $m + n$ righe.

![[Pasted image 20240304092900.png]]

La teoria della normalizzazione è stata perciò generalizzata per rimuovere anche questo tipo di anomalie dovute **dipendenze multivalore** (4NF).
## Esercizi
Gli esercizi di quest'unità si trovano al [seguente link](https://mega.nz/file/Nu9WkRhI#yeXMahz0jqufbNg3Xte7wcI1XNPUyAInbzgcCle7SMI)
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
## Asserzioni
Le asserzioni esprimono **imvarianti globali** sull'intero schema relazionale
```SQL
CREATE ASSERTION <name> CHECK (<condition>)
```

La condizione deve essere vera quando l'asserzione è creata è continua a essere tale dopo ogni modifica del database.

*Nota*: le asserzioni sono strettamente **più potenti** dei CHECK, ma molto più complicate da implementare, data la loro inefficienza nessuno dei principali DBMS le implementa.

**Esempio**

Nessuno può  essere il presidente di uno studio senza avere un reddito di almeno 100.000:

```SQL
CREATE ASSERTION RichPresident CHECK(
	NOT EXISTS(
		SELECT Studio.name
		FROM Studio, MovieExec
		WHERE Studio.president = MovieExec.code AND
			  MovieExec.netWorth < 100000
	)
);
```

## Esercizi
Gli esercizi corretti di trovano alla slide 31 del documento a questo [link](https://mega.nz/file/139GwQyI#XFwQyfcoNjsCtg1LWm14CiP-bz8V-AwuUiUT3gqSBCs).
## Check o Asserzioni?

![[Pasted image 20240311091904.png]]

Utilizzare *check con sotto-query* è pericoloso in presenza di join o prodotti nelle sotto-query perché può portare ad incongruenze.
# Triggers
___
## Introduzione
I trigger sono lo standard de facto per il **mantenimento di invarianti globali** nei DBMS, perché possono essere implementati *efficientemente*.

Seguono un paradigma di tipo: **Evento**-**Condizione**-**Azione**:

* Un trigger è associato ad un **evento** che ne determina l’attivazione. Esempi tipici di eventi sono INSERT, DELETE o UPDATE su una certa tabella.
* Quando un trigger viene attivato, esso può controllare una certa **condizione**. Se la condizione è falsa, il trigger termina
* Se invece la condizione é vera, viene eseguita la cosiddetta **azione** associata al trigger. L’azione é una sequenza arbitraria di operazioni sullo schema relazionale.

*Nota*: nessuno dei DBMS in commercio si adeguano allo standard per motivi storici.
## Trigger per Riga e per Statement
Un evento può coinvolgere righe multiple, quindi SQL fornisce due tipi di trigger diversi:

* **Trigger per riga**: eseguiti per ognuna delle righe coinvolte dall’evento scatenante (*eseguito n volte*). Si può usare OLD ROW e NEW ROW per riferirsi alla tupla coinvolta dall’evento prima e dopo la sua occorrenza. 
* **Trigger per statement**: eseguiti *una sola volta* per evento scatenante. Si può usare OLD TABLE e NEW TABLE per riferirsi a tutte le tuple coinvolte dall’evento prima e dopo la sua occorrenza. 

*Nota*: è possibile fare uso di OLD TABLE e NEW TABLE anche all’interno di un trigger per riga (la riga viene interpretata come una tabella con una singola tupla al suo interno).
## Before e After Trigger
In fase di definizione di un trigger è possibile specificare se l’azione debba essere eseguita prima o dopo l’evento scatenante: 

* **BEFORE trigger**: attivati prima dell’evento scatenante. Di solito vengono utilizzati per impedire l’esecuzione di un’operazione o per modificarne preventivamente il comportamento. 
* **AFTER trigger**: attivati dopo l’evento scatenante. Hanno visibilità dello stato della base di dati dopo l’esecuzione di un’operazione e quindi sono talvolta necessari per motivi di espressività. 

*Nota*: un AFTER trigger può simulare l’annullamento di un’operazione facendo un rollback dello stato della base di dati alla situazione precedente, ma l’uso di BEFORE trigger è preferibile quando possibile.
## Progettazione di Trigger
I trigger forniscono un modo **indiretto** per mantenere invarianti globali: essi non adottano lo stile dichiarativo delle asserzioni. 

Metodologia per il mantenimento di invarianti tramite trigger:

* Quali operazioni possono violare l’invariante? 
* Il mantenimento dell’invariante può essere controllato per ogni riga coinvolta dall’operazione oppure no? (Trigger per *riga* o per *statement*)
* Cosa bisogna fare prima o dopo dell’operazione per garantire il mantenimento dell’invariante?

**Esempio 1**:

Supponiamo di volere utilizzare un trigger per garantire che non sia mai possibile abbassare uno stipendio:

 *Quali operazioni possono violare l’invariante?*
> L’invariante può essere violata da un’operazione di aggiornamento.

 *Il mantenimento dell’invariante può essere controllato per ogni riga coinvolta dall’operazione oppure no?*
>Si, perché l’informazione è contestuale alla riga modificata.

*Cosa bisogna fare prima o dopo dell’operazione per garantire il mantenimento dell’invariante?*
>Impedire l’aggiornamento della riga (BEFORE) oppure riportare lo stipendio al valore originale (AFTER).


Codice SQL per impedire qualsiasi abbassamento di stipendio:
```SQL
CREATE TRIGGER NetWorthTrigger 
AFTER UPDATE OF netWorth ON MovieExec 
REFERENCING OLD ROW AS OldTuple, NEW ROW AS NewTuple 
FOR EACH ROW 
WHEN (OldTuple.netWorth > NewTuple.netWorth) 
	UPDATE MovieExec 
	SET netWorth = OldTuple.netWorth 
	WHERE code = NewTuple.code;
```

*Nota*: i trigger possono fare chiamate ricorsive, bisogna stare attenti ai loop infiniti.

**Esempio 2**:

Supponiamo di volere utilizzare un trigger per garantire che la media degli stipendi non scenda mai sotto 500.000:

 *Quali operazioni possono violare l’invariante?*
> L’invariante può essere violata da un’operazione di inserimento, aggiornamento o cancellazione.

 *Il mantenimento dell’invariante può essere controllato per ogni riga coinvolta dall’operazione oppure no?*
>Visto che la media è un’informazione globale della tabella, non possiamo ricorrere ad un controllo puntuale per riga.

*Cosa bisogna fare prima o dopo dell’operazione per garantire il mantenimento dell’invariante?*
>Possiamo mantenere l’invariante annullando l’operazione che l’ha violata, cioè riportando la tabella allo stato originale (AFTER).

Garantire che la media degli stipendi non scenda mai sotto 500.000:

```SQL
CREATE TRIGGER AvgNetWorthTrigger 
AFTER UPDATE ON MovieExec 
REFERENCING OLD TABLE AS OldStuff, NEW TABLE AS NewStuff 
FOR EACH STATEMENT 
WHEN (500000 > (SELECT AVG(netWorth) FROM MovieExec)) 
BEGIN 
	DELETE FROM MovieExec 
	WHERE (name, address, code, netWorth) 
	IN (SELECT * FROM NewStuff); 
	INSERT INTO MovieExec (SELECT * FROM OldStuff); 
END;
```

*Nota*: servon0 trigger analoghi per INSERT e DELETE.

**Esempio 3**:

Supponiamo di volere utilizzare un trigger per garantire che la data di uscita di un film non possa mai essere `NULL`, usando il valore di default 1915 in tal caso:

 *Quali operazioni possono violare l’invariante?*
> L’invariante può essere violata da un’operazione di inserimento o aggiornamento.

 *Il mantenimento dell’invariante può essere controllato per ogni riga coinvolta dall’operazione oppure no?*
>Si, perché l’informazione è contestuale alla riga inserita o modificata.

*Cosa bisogna fare prima o dopo dell’operazione per garantire il mantenimento dell’invariante?*
>Possiamo mantenere l’invariante correggendo il valore della data nella riga, prima o dopo l’operazione.

La data di uscita di un film non può mai essere `NULL` (default a 1915):

```SQL
CREATE TRIGGER FixYearTrigger 
BEFORE INSERT ON Movies 
REFERENCING NEW ROW AS NewRow, NEW TABLE AS NewStuff 
FOR EACH ROW 
WHEN NewRow.year IS NULL 
UPDATE NewStuff SET year = 1915;
```

*Nota*: serve un trigger analogo per UPDATE.
## Uso dei Trigger

**Trigger passivi**: tali trigger provocano il fallimento di un’operazione sotto determinate condizioni. 
Usi tipici: 
* Definizione di vincoli di integrità (*es.* no abbassamenti di stipendio).
* Controlli dinamici di autorizzazione (*es.* si possono inserire dati solo se il codice del dipartimento coincide con quello dell’utente che ha richiesto l’operazione).

**Trigger attivi**: tali trigger modificano, anche in modo complesso, lo stato della base di dati in corrispondenza di certi eventi. 
Usi tipici: 
* Definizione di vincoli di integrità (*es.* CASCADE). 
* Meccanismi di auditing e logging.
* Definizione di business rules (regole aziendali).

**Chiavi Esterne**: è possibile utilizzare i trigger per implementare vincoli di tipo FOREIGN KEY, gestendo sia la politica CASCADE che la politica SET NULL.

**Dipendenze Funzionali**: è possibile utilizzare i trigger per garantire che un’arbitraria dipendenza funzionale $X \to Y$ sia sempre rispettata.
## Trigger o Vincoli?
Se avete possibilità di scelta, è **sempre preferibile** utilizzare i diversi tipi di vincoli messi a disposizione dal DBMS invece dei trigger: 
* I vincoli sono standard e gestiti in modo uniforme da tutti i DBMS. 
* I vincoli hanno una semantica semplice e non presentano problemi in termini di debugging. 
* I vincoli garantiscono che una certa proprietà valga già al momento della loro definizione, a differenza dei trigger che sono reattivi. 

Talvolta i trigger sono necessari per la loro espressività, per esempio: 
* Per invarianti che coinvolgono più di una tabella. 
* Per invarianti che coinvolgono più righe di una stessa tabella.
## Triggers in Postgres
Postgres offre un sistema di trigger potente e fedele allo standard SQL:

```SQL
CREATE TRIGGER name { BEFORE | AFTER } { evt [ OR ... ] }
ON table_name
[ REFERENCING { { OLD | NEW } TABLE AS tab } [ ... ] ] 
[ FOR EACH { ROW | STATEMENT } ] [ WHEN ( condition ) ]
EXECUTE FUNCTION func ( args )
```

Differenze rispetto allo standard: 
* È possibile usare OR per associare uno stesso trigger a più eventi. 
* Non è possibile riferire OLD ROW e NEW ROW in REFERENCING, ma c’è un modo custom per accedere a tali righe. 
* Il corpo del trigger deve essere definito in una **funzione** separata.
## Funzioni e Trigger
Postgres supporta la definizione di funzioni scritte in vari linguaggi. Il suo linguaggio nativo è chiamato **PL/pgSQL**. 
PL/pgSQL può essere usato per definire **trigger functions**, cioè funzioni: 
* Con trigger come tipo di ritorno.
* Senza argomenti: il passaggio di parametri avviene in modo custom in fase di creazione del trigger, perché non esiste un chiamante.

```SQL
CREATE FUNCTION my_trigger() RETURNS trigger AS $$ 
	trigger function definition 
$$ LANGUAGE plpgsql;
```

*Nota*: Il comando CREATE TRIGGER accetta solamente trigger functions.
## Trigger Functions
Tolti i due vincoli già menzionati, una trigger function può essere una funzione PL/pgSQL arbitraria. 
In questa lezione ci focalizziamo su un *formato semplificato*:

```SQL
BEGIN 
	statement_1; 
	... 
	statement_n; 
END;
```

dove ogni statement è un’istruzione SQL, un condizionale (IF) oppure un RETURN. Prossimamente discuteremo PL/pgSQL in dettaglio.
## Passaggio di Parametri
Quando una trigger function viene invocata da Postgres, vengono create nel suo scope alcune variabili speciali. Le più importanti: 
* **NEW**: la nuova riga per operazioni di INSERT/UPDATE all’interno di un trigger per riga (NULL nel caso di DELETE).
* **OLD**: la vecchia riga per operazioni di DELETE/UPDATE all’interno di un trigger per riga (NULL nel caso di INSERT). 
* **TG_NARGS**: numero di argomenti passati tramite la CREATE TRIGGER.
* **TG_ARGV**: vettore di argomenti passati tramite la CREATE TRIGGER.
  
Ci sono inoltre una serie di variabili informative come TG OP, che dicono quale evento ha scatenato il trigger.
## Valore di Ritorno
Una trigger function associata ad un **BEFORE trigger per riga** può: 
* ritornare NULL per indicare che l’operazione (INSERT, UPDATE o DELETE) sulla riga deve essere abortita.
* Nel caso di INSERT o UPDATE: ritornare una riga, che diverrà la nuova riga che sarà inserita o sostituirà la riga aggiornata.
* Se non si vuole interferire con l’operazione: ritornare NEW nel caso di INSERT o UPDATE, ritornare OLD nel caso di DELETE.

Una trigger function deve ritornare NULL in tutti gli altri casi, cioè nel caso di **trigger per statement** ed **AFTER trigger per riga**.
## Trigger per Riga

```SQL
CREATE TRIGGER name { BEFORE | AFTER } { evt [ OR ... ] }
ON table_name
[ REFERENCING { { OLD | NEW } TABLE AS tab } [ ... ] ]
FOR EACH ROW
[ WHEN ( condition ) ]
EXECUTE FUNCTION func ( args )
```

*Punti chiave*:
* Un BEFORE trigger per riga può prevenire operazioni o modificarle.
* La clausola WHEN può fare riferimento a OLD e NEW per specificare una condizione di attivazione e non può fare uso di sotto-query.
* È possibile usare REFERENCING per vedere i cambiamenti complessivi nell’intera tabella, non solo nella riga (solo per AFTER trigger).
## Trigger per Statement

```SQL
CREATE TRIGGER name { BEFORE | AFTER } { evt [ OR ... ] }
ON table_name
[ REFERENCING { { OLD | NEW } TABLE AS tab } [ ... ] ]
FOR EACH STATEMENT
EXECUTE FUNCTION func ( args )
```

*Punti chiave*:
* Un trigger per statement viene eseguito una volta anche se nessuna riga è coinvolta nell’operazione scatenante.
* Sebbene la clausola WHEN possa essere usata anche in un trigger per statement, essa è inutile perché OLD e NEW non sono popolati.
* È possibile usare REFERENCING per vedere i cambiamenti complessivi nell’intera tabella (solo per AFTER trigger).
## Modello di Esecuzione
L’ordine di esecuzione dei trigger dipende dal loro **tipo**:
* I **BEFORE trigger per statement** si attivano *prima di tutti*, per la precisione prima che l’evento abbia inizio.
* **I BEFORE trigger per riga** si attivano *immediatamente prima di operare sulla riga coinvolta* (anche prima dei CHECK).
* Gli **AFTER trigger per riga** si attivano *alla fine dell’evento*, ma prima degli AFTER trigger per statement.
* Gli **AFTER trigger per statement** vengono eseguiti *per ultimi*.
## Sottigliezze
Alcune specificità di Postgres da tenere bene a mente:
* Un trigger per riga ha visibilità dei cambiamenti effettuati sulle righe precedenti, anche nel caso di BEFORE trigger, ma l’ordine di visita delle righe non è predicibile.
* Se più di un trigger viene definito per lo stesso evento sulla stessa tabella, essi sono eseguiti in ordine **alfabetico** fino a terminazione o finché uno di essi non ritorna NULL (nel caso di BEFORE trigger per riga, in cui altri trigger *per la stessa riga* vengono ignorati).
* Un trigger può attivare ricorsivamente altri trigger, potenzialmente introducendo **ricorsioni infinite**. Evitare ricorsioni infinite è compito del programmatore.
## Esempio: Trigger per Dipendenze Funzionali
Vediamo un modo per garantire la dipendenza funzionale $A \to B$: 
```SQL
CREATE TRIGGER FuncDep
	BEFORE INSERT OR UPDATE ON Relation
	FOR EACH ROW
	EXECUTE FUNCTION fix_func_dep ()

CREATE FUNCTION fix_func_dep() RETURNS TRIGGER AS $$
	IF (EXISTS SELECT * FROM Relation
		WHERE A = NEW.A AND B != NEW.B)
	THEN RETURN NULL;
	END IF;
	RETURN NEW;
$$ LANGUAGE plpgsql;
```
# Funzioni e Procedure
___
## Introduzione
Abbiamo visto come usare una funzione per definire il corpo di un trigger. In realtà il concetto di funzione è più generale ed ha altri utilizzi. 
Perché definire una funzione in SQL: 
* **Incapsulare funzionalità** di uso comune per favorirne il riutilizzo.
* **Offrire interfacce** di accesso semplificate ad utenti inesperti di SQL.
* **Centralizzare** lato server una **sequenza di operazioni** di cui non ci interessano i risultati intermedi (benefici di performance).

*Nota*: noi ci concentreremo su [**PL/pgSQL**](https://www.postgresql.org/docs/current/plpgsql.html).
## Dichiarazione di Funzioni
Una funzione si può dichiarare con la sintassi:

```SQL
CREATE FUNCTION my_fun ( args ) RETURNS type 
AS function_body 
LANGUAGE plpgsql;
```

dove `function_body` è un **blocco** con la *seguente struttura*:

```SQL
[ DECLARE declarations ] 
BEGIN 
	statements 
END;
```

*Nota*: Postgres richiede che il `function_body` sia una stringa. Lo possiamo definire in più righe facendolo precedere e terminare da `$$`.
## Dichiarazione di variabili
Tutte le variabili utilizzate in un **blocco** vanno dichiarate nella sezione opportuna, associandole al loro **tipo**:

```SQL
name [ CONSTANT ] type [ NOT NULL ] [ = expr ];
```
Il tipo di una variabile può essere un qualsiasi tipo SQL. Ci sono inoltre alcuni tipi e sintassi particolari che è importante menzionare:
* `var%TYPE`: il tipo della variabile o **colonna** chiamata `var`.
* `tab%ROWTYPE`: il tipo record delle **righe** della tabella `tab`.
* `RECORD`: un qualsiasi tipo **record** $\to$ riga, ma senza sapere le relative colonne (da usare con attenzione).
* `SETOF t`: un **insieme di elementi di tipo `t`** (solo per *valori di ritorno*).
## Esempio
La seguente funzione ha lo scopo di concatenare due stringhe:

```SQL
CREATE FUNCTION my_concat(a text, b text, 
						  uppercase boolean = false) 
RETURNS text AS $$ 
BEGIN
	IF uppercase THEN RETURN UPPER(a || ’ ’ || b); 
	END IF;
	RETURN LOWER(a || ’ ’ || b);
END; $$ LANGUAGE plpgsql;
```

Tutte le seguenti invocazioni sono lecite:
* `SELECT my concat(’Hello’, ’World’)`.
* `SELECT my concat(’Hello’, ’World’, true)`.
* `SELECT my concat(b := ’World’, a := ’Hello’)`.
## Assegnamento
Un assegnamento ad una variabile si effettua con la sintassi: 
```SQL
var = expr;
```

Il risultato di un comando SQL che ritorna una **singola riga**, per esempio certe `SELECT`, può essere salvato in una variabile con la sintassi: 

```SQL
SELECT expr INTO [STRICT] var FROM ... 
```

L’opzione `STRICT` richiede alla query di ritornare *esattamente una riga*, in caso contrario viene dato un errore a runtime. Se viene omessa, solo la prima riga del risultato viene assegnata (NULL in caso di risultato vuoto).
## Ritornare un Valore
Una funzione che ritorna **un singolo valore** può usare la sintassi:

```SQL
RETURN expr
```

Se è necessario ritornare un record, è possibile utilizzare i cosiddetti **parametri di output** per definirne implicitamente il tipo:

```SQL
CREATE FUNCTION sum_n_product(x int, y int, OUT sum int, 
							  OUT prod int) 
AS $$ 
BEGIN 
	sum = x + y; 
	prod = x * y; 
END; $$ LANGUAGE plpgsql;
```
## Ritornare un insieme di valori
Una funzione che ritorna un **insieme di valori** (`SETOF`) deve costruirlo in maniera incrementale tramite le sintassi: 

```SQL
RETURN NEXT expr; -- aggiunge un record al risultato
RETURN QUERY query; -- aggiunge un insieme al risultato 
```

L’insieme di valori da ritornare può poi essere restituito con `RETURN` *senza passare alcun argomento* (o lasciando terminare la funzione).
## Esempio
>Data la tabella `PC(model, speed, ram, hd, price)`, definire una funzione che ritorna un insieme di modelli associati ai rispettivi prezzi, cioè solo la prima e la quinta colonna della tabella.

Abbiamo almeno due diverse possibili opzioni:
* Abusare del **polimorfismo**, ritornando `SETOF RECORD`:
  
  ```SQL
  CREATE FUNCTION f() RETURNS SETOF RECORD AS $$ 
  BEGIN 
  RETURN QUERY SELECT model, price FROM pc; 
  END; $$ LANGUAGE plpgsql;
  ```
  
  Utilizzo poi:
  
  ```SQL
  SELECT m,p FROM f() AS (m character(20), p real);
  ```

* Usare la sintassi `RETURNS TABLE` al posto di `RETURNS` (conoscendo a priori i *tipi di ritorno*):
  
  ```SQL
  CREATE FUNCTION f() RETURNS TABLE(m integer, p real) AS $$
   BEGIN
   RETURN QUERY SELECT model, price FROM pc;
   END;
   $$ LANGUAGE plpgsql;
  ```
  
  Utilizzo poi:
  
  ```SQL
  SELECT * FROM f();
  ```
## Nota di Implementazione
Si noti che la sintassi:

```SQL
CREATE FUNCTION f()
RETURNS TABLE(m character(20), p real) ...
```

e solo una versione *più fedele allo standard* della sintassi:

```SQL
CREATE FUNCTION f(OUT m character(20), OUT p real)
RETURNS SETOF RECORD ...
```

Nel caso di funzioni con parametri di output che ritornano un insieme di valori si può usare `RETURN NEXT` senza argomenti per aggiungere gli attuali valori dei parametri di output come nuova riga del risultato.
## Condizionali
Sintassi del condizionale:

```SQL
IF boolean-expr THEN
	statements
[ ELSIF boolean-expr THEN 
	statements
	... ] 
[ ELSE
	statements ]
END IF;
```

*Nota*: C’è inoltre un costrutto `CASE` in due forme (vedere manuale).

## Cicli
Tradizionale ciclo `WHILE`
```SQL
WHILE boolean-expr LOOP
	statements
END LOOP;
```

Il ciclo `FOR` ha invece una sintassi piuttosto complessa:

```SQL
FOR name IN [ REVERSE ] int-expr .. int-expr 
			[ BY int-expr ] LOOP 
	statements
END LOOP;
```

*Nota*: La variabile di iterazione non deve essere dichiarata ed è **locale** al ciclo.

Il ciclo FOR può essere utilizzato anche per iterare sui risultati prodotti da una certa query:

```SQL
FOR target IN query LOOP
	statements
END LOOP;
```

L’iterazione su un array si effettua invece con `FOREACH`:

```SQL
FOREACH target IN ARRAY expr LOOP
	statements
END LOOP
```

## Variabile found
Ciascuna funzione contiene una variabile booleana `FOUND`:
* `SELECT INTO` imposta `FOUND` a `true` *se viene assegnata una riga alla variabile corrispondente*, a `false` altrimenti.
* `UPDATE`, `INSERT` e `DELETE` impostano `FOUND` a `true` *se almeno una riga è stata toccata dall’operazione*, a `false` altrimenti.
* Un ciclo `FOR` imposta `FOUND` a `true` *se ha iterato almeno una volta*, a `false` altrimenti.
* `RETURN QUERY` imposta `FOUND` a `true` *se la query ha ritornato almeno una riga*, a `false` altrimenti.
## Esempio
Un altro modo per risolvere l'esempio precedente:

```SQL
CREATE FUNCTION f3(OUT m character(20), OUT p real)
RETURNS SETOF RECORD AS $$
declare r RECORD;
BEGIN
	FOR r IN SELECT model, price FROM lab.pc LOOP
	SELECT r.model,r.price INTO m, p;
	RETURN NEXT;
	END LOOP;
END;
$$ LANGUAGE plpgsql;
```
## Messaggi ed Eccezioni

Una funzione può riportare messaggi o errori con la sintassi:
```SQL
RAISE [ level ] ’format’ [, expr [, ... ]]
				[USING option = expr];
```

dove:
* `level` indica il livello di severità dell’errore (`DEBUG`, `LOG`, ...). Il livello di default `EXCEPTION` solleva anche un’**eccezione**.
* `format` è una format string che specifica il messaggio da riportare la clausola `USING` permette di popolare informazioni aggiuntive sull’errore, per esempio il suo codice di errore `ERRCODE` 

Si può usare `RAISE` senza parametri per rilanciare un’eccezione catturata.

Per **catturare** un'eccezione si può catturare la sintassi:

```SQL
BEGIN
	statements
EXCEPTION
	WHEN cond [ OR cond ... ] THEN handler
	[ WHEN cond [ OR cond ... ] THEN handler ... ]
END;
```

Le condizioni `cond` seguono una sintassi particolare, si consulti il manuale per i dettagli. Per esempio è possibile *fare azioni diverse in base al codice di errore*, usando la condizione speciale `others` come fallback.

Quando un’eccezione viene catturata, il contenuto delle variabili locali persiste, ma *tutti i cambiamenti al database effettuati nel blocco che ha sollevato l’eccezione vengono annullati.*

```SQL
INSERT INTO mytab(firstname, lastname) VALUES(’Tom’, ’Jones’);
BEGIN
	UPDATE mytab SET firstname = ’Joe’
	WHERE lastname = ’Jones’;
	x := x + 1;
	y := x / 0;
	EXCEPTION
		WHEN division_by_zero THEN
		RAISE NOTICE ’caught division_by_zero’;
		RETURN x;
END;
```

Qui `x` viene incrementata di 1, ma nel database troveremo `Tom Jones`.
## Procedure
Una procedura è una funzione che non ritorna alcun risultato:
```SQL
CREATE PROCEDURE my_proc ( args )
AS proc_body
LANGUAGE plpgsql;
```

Una procedura può essere invocata tramite il comando `CALL`. Questo è il metodo più moderno per gestire funzioni senza risultato:
* **Prima** di Postgres 11: comando `PERFORM`.
* Una procedura differisce da una funzione `void` solo nella gestione delle **transazioni**.
# Sicurezza del Database
___
## Introduzione
Tutti i DBMS principali implementano meccanismi di
* **Autenticazione**: identificare chi sta operando sul database.
* **Autorizzazione**: determinare chi può fare cosa (tramite permessi)

L’autenticazione è normalmente effettuata tramite l’utilizzo di un *nome utente ed una password*. E’ un prerequisito per l’autorizzazione.
### Controllo degli Accessi
Il **controllo degli accessi** è il meccanismo con cui viene verificato che chi richiede un’operazione sia effettivamente autorizzato a farla.
## Autenticazione
La gestione degli utenti non fa parte dello standard SQL. Ci focalizziamo sull’implementazione di Postgres, ma altri DBMS sono simili. 
Il modo più semplice per creare utenti è tramite la sintassi: 

```SQL
CREATE USER NomeUtente WITH PASSWORD NuovaPwd 
```

Ulteriori opzioni popolari da aggiungere in coda al comando: 
* `SUPERUSER`: l’utente ignora tutti i controlli di sicurezza.
* `CREATEDB`: consente la creazione di nuovi database.
* `VALID UNTIL ts`: specifica la durata massima della password.

Postgres permette di controllare il processo di autenticazione tramite il *file di configurazione* `pg hba.conf`.
È possibile specificare il **metodo di autenticazione** desiderato per ciascuna richiesta di autenticazione, definita da una quadrupla che include:
* **Tipo di connessione**: locale, remota, cifrata (via TLS)... 
* **Database**: lista di database o keyword all 3 utente: lista di utenti o keyword all.
* **Indirizzo**: hostname, indirizzo IP, range di IP... 

La *prima quadrupla che fa match* definisce il metodo di autenticazione. Se non si trova alcuna quadrupla valida, l’autenticazione è *vietata*.

I metodi di autenticazione supportati includono: trust, reject, password, MD5, SCRAM, peer...
## Metodi di Autenticazione: Password
Protocollo per l’utente `peter` con password `123456`:
* In fase di creazione utente, il **server** salva `y = 123456`.
* Il **client** manda lo **username** (`peter`) e richiede una connessione.
* Il **server** richiede la **password** per lo **username** `peter`.
* Il **client** fornisce la propria **password** `x = 123456`.
* Il **server** verifica che `x = y` ed autorizza l’accesso.

Problemi di *sicurezza*:
* Se il canale di comunicazione non è cifrato, la password è **esposta**: questo problema è facile da risolvere tramite l’uso di SSL / TLS.
* La password è memorizzata **in chiaro sul server**, quindi esposta a chiunque riuscisse ad ottenerne il controllo.
## Metodi di Autenticazione: MD5
Protocollo per l’utente `peter` con password `123456`:
* In fase di creazione utente, il **server** salva `y = MD5(123456 + peter)`.
* Il **client** manda lo **username** (`peter`) e richiede una connessione.
* Il **server** richiede un **MD5 della password** proponendo un [[Tecnologie e Applicazioni Web#Nonce| salt]] `abcd`.
* Il **client** calcola `x = MD5(MD5(123456 + peter) + abcd)` e poi lo invia al **server**.
* Il **server** verifica che `x = MD5(y + abcd)` ed autorizza l’accesso.

Questo protocollo non richiede di memorizzare la password in chiaro sul server, ma non è più raccomandato a causa dell’uso di MD5 e del **salt corto**. Inoltre il furto di y permette l’impersonazione dell’utente. Per evitare questi problemi è meglio utilizzare il più complesso **protocollo SCRAM**.
## Autorizzazione
SQL mette a disposizione diversi tipi di permessi, fra cui: 
* `SELECT` su una **tabella** (*operazione ristretta ad un set di attributi X*).
* `INSERT` su una **tabella** (*operazione. ristretta ad un set di attributi X*).
* `UPDATE` su una **tabella** (*operazione ristretta ad un set di attributi X*).
* `DELETE` su una **tabella** (*`SELECT` richiesto per `DELETE` non banali*).
* `TRIGGER`, necessario per definire un **trigger** su una **tabella**.
* `EXECUTE`, necessario per eseguire una **funzione** o **procedura**.

Si noti che `SELECT` e `SELECT(X)` sono due *permessi differenti*, dove il primo è *più generale* del secondo.
## Esempio
```SQL

INSERT INTO Studio(name)
	SELECT DISTINCT studioName
	FROM Movies
	WHERE studioName NOT IN (SELECT name 
							 FROM Studio);
```
Questa query ha bisogno di tutti i seguenti permessi:
* `INSERT(name)` su `Studio`.
* `SELECT(studioName)` su `Movies`.
* `SELECT(name)` su `Studio`.

In alternativa si possono avere *permessi più generali* di questi.
## Permessi e Trigger
La gestione dei permessi è delicata per i **trigger**:
* il permesso `TRIGGER` per una **tabella** abilita la definizione di trigger **arbitrari** su di essa.
* Il creatore del trigger deve avere il permesso `TRIGGER` sulla **tabella** e tutti i permessi richiesti per **eseguire** l’azione del trigger.
* Quando un trigger viene attivato, esso viene eseguito con i **permessi del suo creatore**, indipendentemente da chi ha indotto l’attivazione.

*Nota*: l’uso di trigger può abilitare **scalate di privilegi**.
## Permessi e Funzioni
Quando una funzione viene dichiarata, è possibile specificarne i permessi di esecuzione tramite le opzioni:
* `SECURITY INVOKER`: la funzione viene eseguita con i **permessi dell’utente chiamante** (default).
* `SECURITY DEFINER`: la funzione viene eseguita con i **permessi dell’utente che l’ha definita**.

*Nota*: sebbene l’uso di `SECURITY DEFINER` possa abilitare **scalate di privilegi**, un suo utilizzo sapiente può essere utile per fornire **accesso controllato** a funzionalità che richiedono permessi elevati.
## Assegnare permessi

Il **proprietario di uno schema relazionale** ha tutti i permessi possibili sulle tabelle e gli altri elementi di tale schema. Tali permessi *possono essere concessi ad altri utenti* usando la sintassi:
```SQL
GRANT ListaPermessi ON Elemento TO ListaUtenti
```

*Note*:
* e possibile utilizzare `ALL PRIVILEGES` per indicare **tutti i permessi**.
* È possibile utilizzare `PUBLIC` per autorizzare **tutti gli utenti**, compresi quelli **non ancora esistenti**.
## Delegare Permessi
I permessi possono essere assegnati fornendo la possibilità di delegarli ad altri utenti:

```SQL
GRANT ListaPermessi ON Elemento TO ListaUtenti
WITH GRANT OPTION
```

È *sempre possibile* delegare una versione **meno generale** di un privilegio (delegabile) che si possiede.

**Esempio**: 
>Un utente che ha ricevuto il permesso `SELECT WITH GRANT OPTION` può delegare `SELECT(X)` con X arbitrario sullo stesso elemento.

## Diagramma di Autorizzazione
>Un **diagramma di autorizzazione** è un **grafo orientato** i cui nodi sono etichettati con una *tripla* $(u, p, m)$, dove $u$ è un utente, $p$ è un permesso e $m$ può avere una delle seguenti forme:
>* ⊥: il permesso è stato assegnato, ma non può essere delegato.
>* ∗: il permesso è stato assegnato e può essere delegato.
>* ∗∗: il permesso è stato concesso in qualità di proprietario.

Un arco da $(u_1, p, m_1)$ a $(u_2, p, m_2)$ modella che $u_1$ detiene il permesso $p$ con modalità $m_1$ e lo ha delegato ad $u_2$ con modalità $m_2$.

## Esempio

![[Pasted image 20240320111643.png]]

Sia `A` il proprietario di `t`:
* `A: GRANT p ON t TO B WITH GRANT OPTION`.
* `A: GRANT p ON t TO C WITH GRANT OPTION`.
* `B: GRANT p ON t to D`.
* `C: GRANT p ON t to D`.
* `C: GRANT p ON t to E`.
## Revoca di Permessi
I permessi assegnati possono essere **revocati** tramite la sintassi:

```SQL
REVOKE ListaPermessi ON Elemento FROM ListaUtenti
```

La revoca deve essere **terminata** da una di queste due opzioni:
* `CASCADE`: il permesso viene *ricorsivamente revocato a tutti gli utenti* che lo hanno ricevuto **solamente** tramite il target della revoca.
* `RESTRICT`: fa *fallire la revoca se essa comporterebbe la revoca di ulteriori permessi* secondo la politica `CASCADE`.

*Nota*: un utente può revocare soltanto permessi **assegnati direttamente da se stesso**, a meno di revoche indirette tramite `CASCADE`.
## Esempi

![[Pasted image 20240320112134.png]]

* `A: REVOKE p ON t FROM B` non revoca il permesso anche a `D`, dato che esiste ancora un cammino da `A` verso `D`.

![[Pasted image 20240320112240.png]]

* `A: REVOKE p ON t FROM C` invece revoca il permesso anche ad `E`, dato che ora non esiste più un cammino da `A` verso `E`.
## Revoca di Deleghe
È possibile **revocare** *solo la possibilità di delega*, ma *non il permesso*:

```SQL
REVOKE GRANT OPTION FOR ListaPermessi 
					ON Elemento FROM ListaUtenti
```

![[Pasted image 20240320112545.png]]

Se `A` revoca a `B` la possibilità di delegare `p` (con l’opzione `CASCADE`):

![[Pasted image 20240320112630.png]]
## Revoca e Generalità
E’ possibile che un utente possieda sia un permesso $p$ che una sua variante meno generale $p^{-}$ sullo stesso oggetto.

Normalmente revocare $p^-$ non ha alcun effetto su $p$. Se invece viene revocato $p$, la scelta dipende dal DBMS:
* *Postgres* **revoca** automaticamente anche $p^-$.
* Lo *standard SQL* invece suggerisce di **lasciare** assegnato $p^-$

*Nota*: in generale l’autorizzazione nei DBMS è sostanzialmente standard, ma ci sono piccole differenze che possono introdurre **vulnerabilità inaspettate**.
## Ruoli
Assegnare manualmente i permessi ad ogni singolo utente è spesso un processo **costoso** ed **error-prone**, visto l’elevato numero di utenti.

![[Pasted image 20240320113027.png]]

Un **ruolo** è un *collettore di permessi*, che permette di introdurre un livello di indirezione durante la loro assegnazione.
## Gestione dei Ruoli
Un ruolo può essere creato tramite il comando:

```SQL
CREATE ROLE NomeRuolo;
```

Una volta fatto ciò è possibile usare alcuni comandi già visti:
* `GRANT`: per **assegnare** permessi a ruoli e ruoli ad utenti.
* `REVOKE`: per **rimuovere** permessi a ruoli e ruoli ad utenti.

I ruoli assegnati ad un utente non sono **attivi** di default. 
L’attivazione di un ruolo per ottenerne i permessi viene effettuata tramite il comando: 

```SQL
SET ROLE NomeRuolo;
```
## Benefici dei Ruoli
I ruoli hanno numerosi **benefici** rispetto all’uso tradizionale dei permessi:
* I ruoli raggruppano **insiemi di permessi** logicamente **collegati**.
* È molto **meno costoso** assegnare ruoli che permessi, visto che ci sono molti meno ruoli che permessi.
* È molto **più difficile** sbagliare l’assegnazione di un ruolo che di un insieme di permessi.
* Le **operazioni di revoca** sono analogamente semplificate.
* I ruoli **non** sono **attivi** di default, contrariamente ai permessi: questo è più fedele al *principio del minimo privilegio*.
## Ruoli in Postgres
In Postgres non c’è una vera e propria **differenza** fra utente e ruolo: infatti il comando `CREATE USER` *è un alias per* `CREATE ROLE WITH LOGIN`.
Alcune specificità:
* L’opzione `CREATEROLE` consente al ruolo di **creare** altri ruoli. Questo può condurre a **scalate di privilegi**.
* Ruoli assegnati con `WITH ADMIN OPTION` possono essere delegati.
* È possibile assegnare ruoli ad altri ruoli, introducendo una forma di **ereditarietà** dei permessi.
* Il **diagramma di autorizzazione** è costruito attorno ai ruoli: se un permesso viene assegnato tramite un ruolo, qualsiasi altro *utente con quel ruolo può revocarlo*.
## Ruoli in Postgres : Ereditarietà
Le opzioni `INHERIT` (default) e `NOINHERIT` consentono di gestire il meccanismo di ereditarietà:

```SQL
CREATE ROLE joe LOGIN INHERIT;
CREATE ROLE admin NOINHERIT;
CREATE ROLE wheel NOINHERIT;
GRANT admin TO joe;
GRANT wheel TO admin; 
```

Permessi concessi:
* *login come `joe`*: permessi di `joe` e di `admin` (ma non di wheel).
* *Dopo `SET ROLE admin`*: solo i permessi di `admin`.
* *Dopo `SET ROLE wheel`*: solo i permessi di `wheel` 

*Nota*: sia nel primo che nel secondo caso si può fare `SET ROLE wheel`.
## Raccomandazioni Generali
Un’opportuna politica di autorizzazione è **necessaria** per la sicurezza di un database.
Alcune raccomandazioni:
* Definire un insieme di **ruoli** in fase di progettazione del database a partire dall’*analisi dei requisiti*.
* Definire le politiche di **confidenzialità** ed **integrità** per il database, mappandole su opportuni assegnamenti di permessi a ruoli.
* Assegnare i ruoli agli utenti rispettando il **principio del minimo privilegio** e facendo attenzione all’utilizzo dell’**ereditarietà**.

*Nota*: una buona politica di autorizzazione non è sufficiente per la sicurezza.
## SQL Injection

Consideriamo una web application che consenta di cercare le informazioni relative ad un utente, presentando il suo nome (`$u`) e password (`$p`). 

```SQL
user = get_parameter($u)
pass = get_parameter($p)
statement = "SELECT * FROM users WHERE name = ’" + 
			 user + "’ AND pwd = ’" + pass + "’;"
```

Il codice costruisce la query SQL da eseguire tramite concatenazione di stringhe, che però potrebbero essere state passate da un attaccante.

Se passiamo nome utente `marco` e password `’ OR ’1’ = ’1`:

```SQL
SELECT * FROM users WHERE name = ’marco’
						  AND pwd = ’’ OR ’1’ = ’1’;
```

Questa query ritorna l’intero contenuto della tabella `users`, andando a comprometterne la confidenzialità.

Se passiamo nome utente `marco` e password `’; DROP TABLE users --`:

```SQL
SELECT * FROM users WHERE name = ’marco’
			  AND pwd = ’’; DROP TABLE users -- ’; 
```

Questa query elimina l’intero contenuto della tabella users, andando a comprometterne l’integrità.
## Prevenire SQL Injection
Come per tutte le *forme di injection*, ci sono due approcci tradizionali per prevenire SQL injection:
* **Sanitizzazione**: analisi o trasformazione degli input processati per garantire l’assenza di contenuti malevoli, per esempio costrutti SQL.
* **Encoding**: trasformazione degli output generati per garantire che essi non vengano interpretati come codice eseguibile.

*Nota*: nel caso di SQL l’utilizzo dell’**encoding** è più comune, perché è raro avere casi d’uso in cui del codice SQL deve essere caricato in un’applicazione.
## Escaping
L’**escaping** è una delle più semplici forme di **encoding**, che converte caratteri speciali nella loro versione “letterale”.

```SQL
userName = escape(get_parameter($u))
pwd = escape(get_parameter($p))
statement = "SELECT * FROM users WHERE name = ’" +
			 userName + "’ AND password = ’" + pwd + "’;" 
```

Se passiamo nome utente `marco` e password `’ OR ’1’ = ’1`:

```SQL
SELECT * FROM users WHERE name = ’marco’ AND password = ’’’ OR ’’1’’ = ’’1’;
```
## Prepared Statement
Un **prepared statement** è un’istruzione SQL contenente dei “buchi” detti parametri, che vengono riempiti in modo disciplinato (tipato).

```SQL
userName = get_parameter($u)
pwd = get_parameter($p) statement = "SELECT *
									 FROM users
									 WHERE name = ?
									 AND password = ?;" 
statement.setString(1,userName); statement.setString(2,pwd);
```

I **prepared statement** sono il modo consigliato per evitare SQL injection, ma in alcuni casi non si possono usare.
## Sanitizzazione
Si consideri la seguente porzione di codice usata per stampare il contenuto di una tabella selezionabile da un menù a tendina:

```SQL
table = get_parameter($t)
statement = "SELECT * FROM " + table;
```

Poiché la sintassi dei **prepared statement** *non supporta l’uso di parametri nel nome della tabella*, è importante **sanitizzare** l’input ricevuto. 

```SQL
table = get_parameter($t);
if (table == "Student" || table == "Teacher") {
	statement = "SELECT * FROM " + table;
} 
else { throw new Exception("Unexpected!"); }
```
# Indici e Viste Materializzate
___
## Problema
Si consideri la seguente query: 

```SQL
SELECT *
FROM Movies
WHERE studio = ’Disney’ AND year = 2012; 
```

Se il nostro database contiene $10.000$ film ma la Disney ha prodotto solo $5$ film nel 2012, siamo costretti ad ispezionare $10.000$ **tuple** per ritornare alla fine solo $5$ **risultati**.

**Intuizione**
>Un **indice** è una struttura dati ausiliaria che ci permette di accedere in maniera più efficiente alle tuple di una relazione che soddisfano una determinata proprietà.

## Indici

**Logicamente**
>Dal punto di vista logico, un indice su un attributo $A$ di una relazione $R$ è una lista di coppie $(a_i , P_i)$, dove $a_i$ è un *valore* di $A$ presente in *almeno una tupla* di $R$ e $P_i$ è un *insieme di puntatori* alle tuple di $R$ per cui $A$ vale $a_i$ . Tale lista è **ordinata** rispetto al valore di $A$.

**Fisicamente**
>Dal punto di vista fisico, un indice è spesso memorizzato in una *struttura ad albero* simile ad un Binary Search Tree, che consente di trovare in modo efficiente i puntatori alle tuple che soddisfano una condizione su $A$.

*Nota*: quando un indice viene creato, esso viene utilizzato automaticamente dal **query planner** del DBMS quando ritenuto vantaggioso.
## Indici per Attributo
Tramite un indice su `year` solo **metà** delle tuple devono essere esaminate per trovare i film prodotti nel 2012.

![[Pasted image 20240327161649.png]]

*Nota*: le tuple non sono ordinate rispetto ad `year` nella memoria fisica, ma abbiamo un modo efficiente per trovare le sole tuple rilevanti per la query.
## Indici Multi-attributi
È possibile generalizzare la definizione di **indice** al caso di una **tupla** di attributi $X$, assumendo il classico ordinamento lessicografico fra tuple.

![[Pasted image 20240327162030.png]]

*Nota*: l'**ordine** degli attributi è rilevante nella costruzione di un indice multi-attributo e va scelto con cura.

![[Pasted image 20240327162248.png]]
## Esempio 1
Assumiamo che ci siano $10.000$ film e che la Disney ne abbia prodotti $200$, di cui solo $5$ nel 2012.
```SQL
SELECT *
FROM Movies
WHERE studio = 'Disney' AND year = 2012;
```

Scelte possibili:
* Nessun indice: $10 000$ tuple
* Indice su `studio`: $200$ tuple
* Indice multi-attributo su `(studio, year)`: $5$ tuple.

*Nota*: l'uso di indici non aiuta solo le ricerche su una singola tabella ma è molto utile anche in caso di **join**.
## Esempio 2
Assumiamo che ci siano $10 000$ film e $500$ produttori.

```SQL
SELECT e.name
FROM Movies m, MovieExec e
WHERE m.title = 'Star Wars' AND m.producer = e.code
```

Scelte possibili:
* Nessun indice: $10 500$ tuple
* Indice su `m.title`: $200$ tuple
* Indice su `m.title` e su  `e.code`: $5$ tuple.
## Tuple o Pagine?
Il numero di tuple è una misura **imprecisa** del costo di un’operazione, perché ignora in larga parte l’organizzazione fisica della memoria.
Una metrica migliore è basata sul numero di **pagine** caricate in RAM:
* Ciascuna pagina tipicamente contiene molte **tuple**.
* Anche una singola tupla richiede che l’**intera pagina** corrispondente sia caricata in RAM.
* L’accesso a tutte le tuple in una pagina è solo leggermente più costoso dell’accesso ad una singola tupla.

Il numero di pagine accedute è spesso funzione del numero di tuple accedute.

Se una tabella è fortemente “clusterizzata” su un certo attributo nella memoria fisica, è possibile accedere a molte tuple caricando solo poche pagine: il numero di tuple è una stima **pessimistica** del costo effettivo.

```SQL
SELECT *
FROM Movies
WHERE year = 2001
```

Supponiamo che la tabella `Movies` occupi $700$ pagine, che ogni pagina contenga $100$ tuple e che vi siano $300$ film prodotti nel 2001.

Quante pagine devono essere caricate in RAM con un indice su `year`?
* Se i film sono salvati su disco per anno, possono bastare $3$ pagine.
* Nel caso peggiore potrebbero servire addirittura $300$ pagine.
## Indici: Pro e Contro
**Pro**
>Un indice su un attributo può accelerare di molto l’esecuzione delle query in cui un valore (o un intervallo di valori) è specificato per quell’attributo, oltre che le join che coinvolgono quell’attributo.

**Contro**
>Ciascun indice costruito su una tabella rende le operazioni di inserimento, cancellazione ed aggiornamento su quella tabella più costose, dato che anche l’indice deve essere aggiornato.
## Suggerimenti
Quando definire un indice?
* Su una **chiave** (o una "quasi" chiave).
* Sulle **chiavi esterne** (per semplificare le join).
* Quando le operazioni di **modifica** sono **rare**.
* Quando le tuple sono "**clusterizzate**" su un certo attributo sulla memoria fisica (comando `CLUSTER` di Postgres).

Quando non definire un indice?
* Su **tabelle piccole**, che quindi occupano un numero ridotto di pagine.
* Su **attributi poco selettivi** (*e.g.* sesso o stato civile).
* Su **attributi modificati di frequente**.
## Definizione di Indici
Una sintassi tipica per definire un nuovo indice è la seguente: 

```SQL
CREATE INDEX NomeIndice ON NomeTabella (Attributi);
```

Una sintassi tipica per l’eliminazione di un indice è la seguente:

```SQL
DROP INDEX NomeIndice;
```

Una volta che un indice è definito, il DBMS lo usa automaticamente:
* Usare `ANALYZE` per collezionare statistiche sulla distribuzione dei dati, che il **query planner** sfrutterà per decidere quali indici usare.
* Usare `EXPLAIN` per verificare che gli indici siano usati nel momento aspettato: potremmo avere sbagliato a definirli o la distribuzione dei dati potrebbe essere cambiata senza che il **query planner** lo sappia.
## Esempio di EXPLAIN

![[Pasted image 20240327170118.png]]

## Modello di Costo
Consideriamo la relazione `StarsIn(movie, year, starName)` ed i seguenti patterns di operazioni tipiche:

![[Pasted image 20240327170712.png]]

### Costo di $Q_1$
```SQL
SELECT movie, year
FROM StarsIn
WHERE starName = s
```

Assumendo che `StarsIn` occupi $10$ pagine e che in media ogni attore abbia recitato in $3$ film, abbiamo i seguenti costi:
* Senza indice: $10$.
* Indice su `starName`: $1 + 3$.
* Indice su `(movie, year)`: $10$.
* Entrambi gli indici: $1 + 3$.
### Costo di $Q_2$
```SQL
SELECT starName
FROM StarsIn
WHERE movie = t AND year = y
```

Assumendo che `StarsIn` occupi $10$ pagine e che in media ogni attore abbia recitato in $3$ film, abbiamo i seguenti costi:
* Senza indice: $10$.
* Indice su `starName`: $10$.
* Indice su `(movie, year)`: $1 + 3$.
* Entrambi gli indici: $1 + 3$.
### Costo di /
```SQL
INSERT
INTO StarsIn
VALUES(m,y,s)
```

Assumendo che `StarsIn` occupi $10$ pagine e che in media ogni attore abbia recitato in $3$ film, abbiamo i seguenti costi:
* Senza indice: $2$.
* Indice su `starName`: $2 + 2$.
* Indice su `(movie, year)`: $2 + 2$.
* Entrambi gli indici: $2 + 2 + 2$.
### Cosa Fare?
Supponiamo di eseguire $Q_1$ con probabilità $p_1$, $Q_2$ con probabilità $p_2$ e / con probabilità $1 - p_1 - p_2$.

![[Pasted image 20240327171533.png]]

Se $p_1 = 0.4$ e $p_2 = 0.1$ otteniamo che la soluzione migliore è usare solo il primo indice (su `starName`).
## Selezione Automatica di Indici
Un DBMS può suggerire automaticamente gli indici migliori sulla base di un modello di costo simile a quello considerato:
* Usa i log delle query per stimare il costo delle operazioni più frequenti.
* Genera un insieme di **indici candidati** $I$ e stima i tempi di esecuzione rispetto ai vari $J \subseteq I$.
* Ritorna l’insieme di indici $J_{min}$ che ottimizza i tempi di esecuzione.

Il secondo passo potrebbe essere implementato in maniera **greedy** per motivi di efficienza.
### Algoritmo Greedy
* Usa i log delle query per stimare il costo delle operazioni più frequenti.
* Genera un insieme di indici candidati $I$ ed inizializza $J = \emptyset$.
* Finché è possibile migliorare i tempi di esecuzione:
	* identifica $i_{min} \in I$, l’indice che ottimizza meglio i tempi di esecuzione assumendo di avere già creato gli indici in $J$.
	* Imposta $J = J \cup \{i_{min}\}$.
	* Imposta $I = I$ \\ $\{i_{min}\}$
## Viste e Performance
```SQL
CREATE VIEW MovieProd AS
		SELECT m.title, m.year, e.name
		FROM Movies m, MovieExec e
		WHERE m.producer = e.code
```

Questa vista è utile quando vogliamo trovare il nome del produttore di un film, ma deve essere **valutata** ogni volta che ci facciamo una query sopra. Questo è potenzialmente inefficiente.
## Viste Materializzate
SQL permette di materializzare una vista in memoria, in modo che essa non venga valutata ad ogni query che la coinvolge:

```SQL
CREATE MATERIALIZED VIEW MovieProd AS
		SELECT m.title, m.year, e.name
		FROM Movies m, MovieExec e
		WHERE m.producer = e.code
```

L’uso di viste materializzate può *migliorare le prestazioni* delle query, ma comporta un **costo aggiuntivo** derivante dalla necessità di riflettere sulla vista le modifiche alle tabelle su cui la vista è costruita.
## Viste Materializzate: Mantenimento

```SQL
CREATE MATERIALIZED VIEW MovieProd AS
		SELECT m.title, m.year, e.name
		FROM Movies m, MovieExec e
		WHERE m.producer = e.code
```

Non c'è bisogno di aggiornare `MovieProd` nei seguenti casi:
* Modifiche a **tabelle** diverse da `Movies` e `MovieExec`.
* Modifiche ad **attributi** di `Movies` e `MovieExec` diversi da quelli menzionati nella definizione di `MovieProd`

*Approccio conservativo*: in tutti gli altri casi rigeneriamo la vista, ma ci sono diverse ottimizzazioni. Postgres delega la responsabilità all’utente tramite il comando `REFRESH MATERIALIZED VIEW`.
## Viste Materializzate: Ottimizzazioni
```SQL
CREATE MATERIALIZED VIEW MovieProd AS
		SELECT m.title, m.year, e.name
		FROM Movies m, MovieExec e
		WHERE m.producer = e.code
```

Assumiamo di voler aggiungere un nuovo film: `Kill Bill`, prodotto nel `2003` dal produttore con codice `23456` `(Quentin Tarantino)`.
In questo caso *non serve rigenerare `MovieProd`*:

```SQL
INSERT INTO MovieProd
VALUES (’Kill Bill’, 2003, ’Quentin Tarantino’);
```

Assumiamo ora di voler cancellare un film: `Il Re Leone`, prodotto nel `1994`.
In questo caso *non serve rigenerare `MovieProd`*:

```SQL
DELETE FROM MovieProd
WHERE title = ’Il Re Leone’ AND year = 1994;
```

Assumiamo infine di voler cancellare il produttore con codice `45678`.
Anche in questo caso *non serve rigenerare `MovieProd`*:

```SQL
DELETE FROM MovieProd
WHERE (title,year) IN (SELECT title, year
					   FROM Movies
					   WHERE producer = 45678
);
```
## Viste Materializzate e Performance
In sostanza, le viste materializzate:
* Possono *velocizzare le query*, ma rendono le operazioni di modifica più **costose** (come gli **indici**) o potenzialmente **invalidanti** (Postgres).
* In certi DBMS vengono *mantenute in modo incrementale* per quanto possibile, ma richiedono di essere **rigenerate** dopo certe operazioni.
* Possono essere **inlined** automaticamente dal DBMS in una query per *migliorarne l’efficienza*, sfruttando il fatto che parte dell’informazione è già stata computata e salvata in memoria.
## Inlining di Viste Materializzate

Vista materializzata $V$:

```SQL
SELECT AV
FROM RV
WHERE CV
```

Query $Q$:

```SQL
SELECT AQ
FROM FR
WHERE CQ
```

Condizioni per l'*inlining* di $V$ in $Q$:
* $RV \subseteq RQ$.
* $CQ = CV$ AND $CQ'$  per qualche $CQ'$
* Ogni attributi di $CQ'$ che proviene da $RV$ fa parte di $AV$.
* Ogni attributi di $AQ$ che proviene da $RV$ fa parte di $AV$.

Risultato dell'*inlining*:

```SQL
SELECT AQ
FROM V, RQ \ RV
WHERE CQ'
```
## Esempio di Inlining di Viste Materializzate
Vista Materializzata $V$

```SQL
CREATE MATERIALIZED VIEW MovieProd AS
		SELECT m.title, m.year, e.name
		FROM Movies m, MovieExec e
		WHERE m.producer = e.code
```

Query $Q$:

```SQL
SELECT s.starName
FROM StarsIn s, Movies m, MovieExec e
WHERE s.title = m.title 
		AND s.year = m.year
		AND m.producer = e.code
		AND e.name = ’Tarantino’
```

Risultato dell'inlining:

```SQL
SELECT s.starName
FROM StarsIn s, MovieProd mp
WHERE s.title = mp.title
		AND s.year = mp.year
		AND mp.name = ’Tarantino’
```
# Transazioni
___
## Introduzione
Quando programmiamo applicazioni che si interfacciano con un database, è normale raggruppare insieme una **sequenza di operazioni** su di esso per implementare una determinata funzionalità. 

Questa pratica necessaria può creare problemi quando: 
* Ci sono molte operazioni **concorrenti** sulla base di dati, per esempio perché più persone stanno contemporaneamente prenotando un posto a sedere sullo stesso volo.
* Certe operazioni **falliscono** e non possono essere completate, per esempio perché troppe persone sono attive nello stesso momento.

Entrambi questi scenari possono danneggiare l’integrità della base di dati.
## Concorrenza
Un utente `u` vuole riservare un posto sul proprio volo:

```SQL
SELECT seatNo 
FROM Flights 
WHERE fltNo = 123 AND fltDate = DATE ’2020-03-07’ AND
									seatStatus = ’available’
```

Una volta scoperto che il posto `22A` è libero, u procede alla prenotazione:

```SQL
UPDATE Flights
SET seatStatus = ’occupied’
WHERE fltNo = 123 AND fltDate = DATE ’2020-03-07’
				  AND seatNo = ’22A’
```

Ma anche l’utente `v` vuole prenotare un posto sullo stesso volo e proprio nello stesso momento.

![[Pasted image 20240327104150.png]]

Col risultato che  ad entrambi viene assegnato lo stesso posto.
## Fallimenti
Visto che la compagnia aerea ha lasciato il posto `22A` a `u`, il biglietto di `v` va rimborsato. Si prelevano 800 euro dal conto della compagnia: 

```SQL
UPDATE Accounts
SET balance = balance - 800
WHERE acctNo = 123; 
```

e si accreditano poi sul conto di `v`: 

```SQL
UPDATE Accounts
SET balance = balance + 800
WHERE acctNo = 456;
```
## Transazioni
Una *transazione* è una sequenza di operazioni sul database che soddisfa le seguenti proprietà:
* **Serializzabilità**: l’esecuzione concorrente di più transazioni è equivalente ad una loro esecuzione seriale in un qualche ordine.
* **Atomicità**: se la transazione termina prematuramente, tutti i suoi effetti parziali sono annullati.
* **Persistenza**: le modifiche effettuate da una transazione terminata con successo sono permanenti.

*Nota*: in certi libri di testo una presentazione leggermente diversa: ACID, un popolare acronimo per Atomicity, Consistency, Isolation e Durability.
## Serializzabilità
Questa esecuzione non è più ammissibile, perché viola la condizione di serializzabilità delle transazioni:

![[Pasted image 20240327104859.png]]

Non è possibile che due utenti trovino il posto `22A` libero se le due transazioni sono eseguite una dopo l’altra.

Questa esecuzione è invece ammissibile rispetto alla condizione di serializzabilità, anche se ha favorito `v` rispetto ad `u`:

![[Pasted image 20240327105005.png]]

Non importa chi è **penalizzato** fra `u` e `v`, l’importante è che uno dei due sia costretto a trovarsi un altro posto a sedere.
## Atomicità
Supponiamo che *avvenga un crash* dopo aver prelevato 800 euro dal conto della compagnia:

```SQL
UPDATE Accounts
SET balance = balance - 800
WHERE acctNo = 123; 
```

La seguente operazione nella stessa transazione non verrà più eseguita:

```SQL
UPDATE Accounts
SET balance = balance + 800
WHERE acctNo = 456;
```

Alla fine del crash anche la prima operazione sarà pertanto **annullata**.
## Programmare Transazioni
Normalmente ogni operazione SQL è gestita come una **transazione indipendente**. 
È possibile però usare i seguenti comandi:
* `START TRANSACTION` indica l’**inizio** di una nuova transazione.
* `COMMIT` indica la terminazione **corretta** di una transazione: tutto ciò che è stato fatto durante la transazione deve essere reso persistente.
* `ROLLBACK` indica la terminazione **anomala** di una transazione: tutto ciò che è stato fatto durante la transazione deve essere annullato.

*Nota*: tipicamente API come JDBC offrono metodi che permettono di gestire le transazioni, che si appoggiano a questi comandi SQL.
## Transazioni e Vincoli

Data l’**atomicità** delle transazioni, è possibile *differire* il controllo di alcuni vincoli di integrità alla fine di una transazione.
Ciascun vincolo può appartenere ad una fra tre categorie:
* `NOT DEFERRABLE`: viene sempre *controllato dopo ogni operazione*.
* `DEFERRABLE INITIALLY IMMEDIATE`: viene *controllato dopo ogni operazione* della transazione, ma è possibile **rilassarlo** per farlo controllare solo prima del commit.
* `DEFERRABLE INITIALLY DEFERRED`: viene *controllato solo prima del commit*, ma è possibile **rafforzarlo** per farlo controllare dopo ogni operazione della transazione.

*Nota*: i vincoli differibili possono essere configurati tramite `SET CONSTRAINTS`.
## Implementazione di Transazioni
Una transazione è una *sequenza di operazioni serializzabile*.
Costo in termini di performance:
* **Soluzione banale**: ciascuna transazione prende un *lock globale* sul database, che viene rilasciato solo dopo commit o rollback.
* **Ottimizzazioni**: insieme di *lock locali*, che predicano solo su porzioni del database, e gestione rilassata delle transazioni *read only*, che non possono compromettere l’integrità della base di dati.

*Note*: 
* I DBMS moderni usano soluzioni senza lock come MVCC (multiversion concurrency control).
* I DBMS principali forniscono ulteriore controllo al programmatore definendo diversi **livelli di isolamento** fra transazioni.
* **Rilassare** il livello di isolamento ideale (`SERIALIZABLE`) può portare ad un incremento delle **prestazioni**, ma è in generale **rischioso**.
## Transazioni Read Only
Una transazione può essere dichiarata **read only** tramite la sintassi:

```SQL
SET TRANSACTION READ ONLY;
```
L’effetto di tale dichiarazione è il seguente:
* La transazione può **solo leggere** dati (`SELECT`), ma non scriverli.
* Tutte le query nella transazione possono vedere solo le scritture committate **prima dell’inizio** della transazione.
* Più transazioni read only che operano sugli stessi dati possono essere eseguite **concorrentemente** senza rischi per l’integrità dei dati.

*Nota*: una transazione read only fornisce una lettura **consistente** dello stato del database prima dell’inizio della transazione.
## Transazioni Read Uncommitted
Il livello di isolamento `READ UNCOMMITTED` consente ad una transazione di leggere **dirty data**, cioè dati scritti da altre transazioni che non hanno ancora fatto commit:
* Quando ciò si verifica, si parla di **dirty read**.
* Il rischio di una dirty read è che la transazione che ha scritto i dirty data potrebbe **abortire**: in tal caso, i dirty data dovrebbero essere **rimossi** e *non dovrebbero influenzare le altre transazioni*. 

*Nota*: SQL limita l’uso di `READ UNCOMMITTED` alle sole transazioni read only, a meno che lo sviluppatore non decida di rilassare questo vincolo.

## Esempio di Dirty Reads
Consideriamo la seguente definizione di una transazione per effettuare un bonifico fra due conti correnti:
* Accredita immediatamente l’importo nel conto $2$.
* Controlla se il conto 1 conteneva abbastanza denaro:
	* In caso positivo, addebita l’importo nel conto $1$ (`commit`).
	* In caso negativo, annulla l’accredito nel conto $2$ (`rollback`).

Consideriamo due transazioni eseguite concorrentemente:
* $T_1$ trasferisce $150$ dal conto $A_1$ al conto $A_2$.
* $T_2$ trasferisce $250$ dal conto $A_2$ al conto $A_3$.

![[Pasted image 20240327111319.png]]
## Transazioni Read Committed
Il livello di isolamento `READ COMMITTED` impedisce il fenomeno delle **dirty read**, fornendo un *maggiore isolamento*:
* Quando una transazione vuole effettuare una **scrittura**, acquisisce un **lock** che viene rilasciato solo dopo la sua terminazione.
* Si può verificare il fenomeno di **unrepeatable read**: due letture degli stessi dati in momenti diversi possono portare a **risultati diversi** a causa dell’*intervento* di un’altra transazione.
* Si può verificare il fenomeno di **lost update**, cioè la **perdita** di una modifica da parte di una transazione causata da un *aggiornamento* operato da un’altra transazione.
## Esempio di Unrepeatable Read
Calcolo della media dei voti di tutti gli studenti in presenza di una cancellazione concorrente:

![[Pasted image 20240327111659.png]]

La media calcolata è **sbagliata**.
## Esempio di Lost Update
Vendita concorrente di articoli da un sito di e-commerce:

![[Pasted image 20240327111817.png]]

Il numero di articoli rimanenti è **sbagliato**.
## Transazioni Repeatable Read
Il livello di isolamento `REPEATABLE READ` **impedisce** il fenomeno delle **dirty read**, delle **unrepeatable read** e dei **lost update**:
* Quando una transazione vuole *effettuare una lettura oppure una scrittura*, acquisisce un **lock** che viene rilasciato solo dopo la sua terminazione.
* Per motivi di **efficienza**, i lock vengono implementati a livello di **righe**.
* Si può verificare il fenomeno dei **fantasmi**: un’altra transazione può aggiungere dati ad una tabella *prima che la transazione in corso sia stata completata*, andando ad influenzarne il risultato.
## Esempio di Prevenzione di Unrepeatable Read
Calcolo della media dei voti di tutti gli studenti in presenza di una cancellazione concorrente:

![[Pasted image 20240327112232.png]]

La media calcolata è **corretta**.
## Esempio di Prevenzione di Lost Update
Vendita concorrente di articoli da un sito di e-commerce:

![[Pasted image 20240327112425.png]]

Il numero di articoli rimanenti è **corretto**.
## Esempio di Fantasmi
Calcolo della media dei voti di tutti gli studenti in presenza di una cancellazione concorrente:

![[Pasted image 20240327112515.png]]

La media calcolata è di nuovo **sbagliata**.
## Riassunto dei Livelli di Isolamento
Ci sono *quattro possibili livelli di isolamento*, che offrono:
* Diversi livelli di **performance** .
* Diverse **garanzie di integrità**.

![[Pasted image 20240327112731.png]]

## Interazioni fra Livelli di Isolamento
Il livello di isolamento di una transazione riguarda *esclusivamente ciò che può vedere quella transazione*:
* Se $T$ è `SERIALIZABLE`, la sua esecuzione deve essere **equivalente** al caso in cui tutte le altre transazioni sono state eseguite interamente **prima** o interamente **dopo** $T$.
* Se un’altra transazione gira con un **diverso livello di isolamento**, essa potrebbe vedere **immediatamente** i dati scritti da $T$ (anche prima della sua terminazione) (*e.g.* se tale transazione è `READ UNCOMMITTED`, essa può vedere i **dirty data** scritti da $T$)
## Esempio 1 sui Livelli di Isolamento
A che livello di isolamento andrebbe eseguita la seguente transazione?

 >Per ogni cliente della banca, contare le operazioni effettuate negli ultimi $500$ giorni, ed aggiungere il nome del cliente ad un elenco se le operazioni sono più di $300$. L’elenco servirà a scopi di marketing.
 
Visto che la transazione viene usata solo a fini di marketing, è plausibile che qualche sporadico errore nei risultati non vada ad inficiare il quadro generale $\implies$ `READ UNCOMMITTED` per **maggiore efficienza**.
## Esempio 2 sui Livelli di Isolamento
A che livello di isolamento andrebbe eseguita la seguente transazione?

>Effettuare un trasferimento fondi, sottraendo un ammontare da un conto per poi aggiungerlo ad un altro. Se la sottrazione ha portato ad un valore negativo, l’operazione va annullata.

![[Pasted image 20240327113542.png]]

Bisogna acquisire un blocco in fase di lettura già alla prima riga, altrimenti potremmo trasferire gli stessi soldi più volte $\implies$ `REPEATABLE READ`.
## Esempio 3 sui Livelli di Isolamento
A che livello di isolamento andrebbe eseguita la seguente transazione?

>Gestire un prelievo allo sportello come segue: il cassiere legge il saldo corrente del cliente e gli chiede conferma; se il saldo disponibile supera la cifra richiesta dal cliente, viene poi effettuato il pagamento.

![[Pasted image 20240327113726.png]]

La durata delle transazioni dovrebbe essere corta per motivi di efficienza, quindi facciamo due transazioni: una a livello `READ COMMITTED` con solo la **lettura preliminare** ed una a livello `REPEATABLE READ` per il pagamento.
## Transazioni in Postgres
PostgreSQL considera ciascuna istruzione SQL come una transazione: se non viene eseguito `BEGIN`, ciascuna istruzione ha un `BEGIN` implicito e (se ha successo) un corrispondente `COMMIT`.
Il livello di isolamento di default in Postgres è `READ COMMITTED`, ma i livelli di isolamento garantiscono proprietà **più forti** rispetto allo standard.

![[Pasted image 20240327113945.png]]

*Nota*: sebbene la tabella non evidenzi differenze, `SERIALIZABLE` offre **garanzie migliori** rispetto a `REPEATABLE READ`.

`SERIALIZABLE` garantisce l’**assenza di anomalie di serializzazione**, che invece sono **possibili** a livello `REPEATABLE READ`.

![[Pasted image 20240327114227.png]]

`SERIALIZABLE` **garantisce** che la tabella contenga lo stesso colore in tutte le righe alla fine dell’esecuzione di $T_1$ e $T_2$, mentre `REPEATABLE READ` potrebbe portare ad *invertire i colori delle varie righe*.