# Concetti di Base
___
## Popolazione e Campione
### Terminologia
* **popolazione**: tutte le unità statistiche di interesse.
* **parametro**: una caratteristica numerica della popolazione di interesse $\theta$.
* **censimento**: osservazione di tutte le unità della popolazione per valutare $\theta$.
* **campione**: sottoinsieme della popolazione utilizzato per stimare $\theta$ quando il censimento non è opportuno
* **statistica**: una qualsiasi funzione dei dati censuari o campionari
* **stimatore**: statistica $\hat{\theta}$ applicata al campione e utilizzata per ricostruire $\theta$ (*astratto*)
* **stima**: valore dello stimatore corrispondente al particolare campione osservato (*concreto*).
### Errori campionari e non campionari
* **errori campionari**: sono *inevitabili* e dovuti al fatto che osserviamo solo un campione dei dati. Diminuiscono al crescere della dimensione campionaria se lo stimatore $\hat{\theta}$ è ragionevole.
* **errori non campionari**: sono *evitabili* e dovuti ad una sbagliata costruzione del campione o all'utilizzo di uno stimatore non appropriato. Possono non diminuire al crescere della dimensione campionaria. 
### Campionamento Casuale

Per evitare gli *errori campionari* dovremmo conoscere perfettamente la popolazione. Ciò è difficile e pertanto conviene utilizzare un **campione casule**, per evitare gli errori dovuti ad avere un campione non rappresentativo della popolazione.

**Campionamento casuale semplice**: Da una popolazione di $n$ individui Si estraggono $m$ elementi *indipendenti* con *uguale probabilità (* $\frac{1}{n}$).
Si può inoltre stratificare un *macro-campione* e poi utilizzare il **campionamento casuale semplice** nelle varie sotto-unità.
Le osservazioni ottenute con il **campionamento casuale semplice** sono **i.i.d** $\rightarrow$ indipendenti ed identicamente distribuite.
## Statistiche Campionarie
### Dati Campionari

* **Lettere Maiuscole**: variabili casuali.
* **Lettere Minuscole**: osservazioni su variabili casuali

Consideriamo un campione casuale di dimensioni $n \rightarrow (X_1 ... X_n)$.

 *Esempio*: se prendiamo un campione casuale dei tempi di elaborazione di 30 processi, una **variabile casuale** è data dall'insieme di tutti i campioni, mentre un'**osservazione**  è un singolo campione.
### Statistiche campionarie

* Statistiche che misurano la *posizione* : **media, mediana, quantili , percentili, quartili**.
* Statistiche che misurano la *variabilità*: **varianza, deviazione standard, scarto interquantile**.

Le statistiche stesse sono **variabili casuali**. Anche in questo caso bisogna stare attenti a non applicare le statistiche a campioni falsati da **errori** **non** **campionari**.
### Media Campionaria

Supponiamo che le osservazioni $X_i$ siano variabili i.i.d con valore atteso $E(X) = \mu$ e varianza $Var(X) = \sigma^2$. 
La media campionaria è  uno stimatore di popolazione $\mu = E(X)$.
### Stime e Stimatori 

*Nota*: useremo $\hat{\theta}$ sia per la **stima** che per lo **stimatore**, tuttavia siccome la stima è calcolata su un campione, difficilmente sarà uguale alla popolazione $\theta$.

Se il campione è *ben costruito*, al crescere di $n$, lo *stimatore*:
* convergerà a $\theta$.
* si osservano *stime* difficilmente lontane da $\theta$

**Proprietà dello Stimatore**:
* Uno *stimatore* è **non** **distorto** se $E(\hat{\theta} = \theta)$ per tutti i valori di $\theta$. La **distorsione** dello stimatore è $Bias(\hat{\theta}) = E(\hat{\theta} - \theta)$. Lo stimatore non distorto non **sottostima** né **sovrastima** il parametro.
*Esempio*:
$$ E(\overline{X}) = \frac{1}{n} \cdot \sum_{i=1}^n E(X_i) = \frac{1}{n} \cdot \sum_{i = 1}^n \mu = \mu$$

* Uno *stimatore* è **consistente** se al crescere della dimensione campionaria $n$ il suo errore campionrio converge a 0. $$Pr(|\hat{\theta} - \theta| > \epsilon) \rightarrow 0\ per\ n \rightarrow \infty,\ per\ qualsiasi\ \epsilon > 0$$ ovvero: $$\hat{\theta} \overset{p}{\to}  \theta\ per\ n \rightarrow \infty$$ la **consistenza** si può verificare con la **Legge dei grandi numeri**, o con la **Diseguaglianza di Chebyshev**, ma solo se i dati sono indipendenti. Vediamo un *esempio* con la media campionaria $\overline X$.
* Per la **legge dei grandi numeri** $\overline X \overset{p}{\to} \mu$, per $n \to \infty$.
* Per la **Disuguaglianza di Checyshev**: $$Pr(|\overline X - \mu| > \epsilon) \leq \frac{Var(\overline X)}{\epsilon^2}$$ Siccome:$$Var(\overline X) = Var(\frac{1}{n} \cdot \sum_{i = 1}^n Var[X_i]) = \frac{1}{n^2} \cdot \sum_{i = 1}^n Var[X_i] = \frac{\sigma^2}{n}$$ Abbiamo che: $$Pr(|\overline X - \mu| > \epsilon) \leq \frac{\sigma^2 / n}{\epsilon^2} \to 0\ per\ n \to \infty$$
$\color{red} \textbf{Teorema}$
Uno *stimatore* è **consistente** se al *crescere della dimensione campionaria* ($n \rightarrow \infty$ ) *la distorsione va a $0$*  ($Bias(\hat{\theta} \rightarrow 0$) e *la varianza va a $0$*  ($Var[\hat{\theta}] \rightarrow 0$).
###  Normalità Asintotica
In generale uno stimatore $\hat{\theta}$, la cui distribuzione al crescere di $n$ è via via meglio approssimata ad una distribuzione normale (**asintoticamente normale**), e pertanto abbiamo una probabilità maggiore di estrarre un buon campione al crescere di $n$ (è improbabile osservare valori $\overline{x}$ che distano da $\mu$) . Un esempio è quello della *media campionaria*, come afferma anche il *CLT*.

![[Pasted image 20240215095822.png]]

Generalmente noi cercheremo degli **stimatori asonticamente normali**.
La **media** tuttavia ha il difetto di essere sensibile ad osservazioni estreme.
### Mediana Campionaria
* Stima la mediana di popolazione
* Molto meno sensibile alle osservazioni estreme rispetto alla media.

La **Mediana di popolazione** $M$ suddivide la distribuzione di $X$ in due parti uguali, ovver:
$$Pr(X>M) \leq 0.5\ e\ Pr(X<M) \leq 0.5$$
La **Mediana Campionaria** $\hat{M}$ è:
* inferiore al più a metà dei dati campionari
* superiore al più a metà dei dati campionari

La *Mediana* è **roubusta, consistente** e **asintoticamente normale**, tuttavia ha una **varianza** maggiore della *media* e pertanto è meno efficiente

La relazione fra *media* e *mediana* determina la forma della distribuzione:

![[Pasted image 20240215101631.png]]

Nel *caso continuo* la mediana si ottiene risolvendo l'equazione: $F(M) = Pr(X \leq M) = 0.5$.

![[Pasted image 20240215101856.png]]

Nel *caso discreto* l'equazione $F(M) = 0.5$:
* ha un intervallo di valori come soluzione
* non ha soluzione

![[Pasted image 20240215102044.png]]

#### Calcolo Mediana Campionaria
Dopo aver ordinato le osservazioni:
* Se $n$ è *pari* allora $\hat{M}$ è un qualsiasi valore fra le osservazioni in posizione $\frac{n}{2}$ e $\frac{n+2}{2}$
* Se $n$ è *dispari*  allora $\hat{M}$ è il valore dell'osservazioni in posizione $\frac{n+1}{2}$

### Quantili, Percentili e Quartili
* **Quatile di ordine p**: numero $x$ tale che: $$Pr(X < x) \leq p\ \ \ Pr(X > x) \leq 1-p$$ , cioè può assumere qualsiasi valore fra 0 e 1
* **Percentile**: il percentile di ordine $\gamma$ corrisponde al quantile di ordine $0.01\gamma$
* **Quartile**: divide la funzione di ripartizione in quarti (Esempio: 1° quartile $=$ 25° percentile)
### Varianza e Deviazione Standard Campionaria
* La **Varianza Campionaria** è definita come: $$S^2 = \frac{1}{\color{blue}n-1} \cdot \sum_{i=1}^n (X_i - \overline{X})^2$$ e misura la dispersione attorno alla media campionaria
* La **Deviazione Standard Campionaria** è la radice quadrata della varianza campionaria: $$S = \sqrt{S^2}$$

La **Varianza** è al quadrato perchè altrimenti gli scarti positivi e negativi potrebbero bilanciarsi.
Talvolta tuttavia sarebbe utile usare il valore assoluto poichè la **Varianza** è molto sensibile ai *valori anomali*.
#### Proprietà della Varianza Campionaria
* Il coefficiente $\frac{1}{n-1}$ che appare in $S^2$ è necessario perché $S^2$ non sia *distorta*: $$Bias(S^2) = E(S^2) - \sigma^2 = 0$$
* $S^2$ è uno stimatore *consistente* di $\sigma^2$: $$S^2 \overset{p} \to \sigma^2\ per\ n \to \infty$$
* $S^2$ è uno stimatore *asintoticamente normale*: $$S^2 \overset{d} \to N\{\sigma^2,Var(S^2)\}\ per\ n \to \infty$$
#### Trasformazioni
* **Valore Atteso**: in genere il valore atteso della trasformazione è diverso dalla trasformazione del valore atteso $$E\{g(X)\} \neq g\{E(X)\}$$ a meno che $g(\cdot)$ non sia lineare.
* **Convergenza in Probabilità**: se $g(\cdot)$ è continua  $$X \overset{p} \to \theta \implies g(X) \overset{p} \to g(\theta).$$
* **Normalità Asintotica**: se $g'(\theta)$ esiste e non è nulla $$X \overset{p} \to N(\theta, \psi^2) \implies g(X) \overset{p} \to N(g(\theta), g'(\theta)^2 \cdot \psi^2).$$
#### Deviazione Standard Campionaria
La **Deviazione Standard** $S$ è una funzione di $S^2$ $$S = g(S^2),\ con\ g(\cdot) = \sqrt{\cdot}$$
* $S$ è uno stimatore **distorto** di $\sigma$: $$Bias(S) = E(S) - \sigma \neq 0$$ tuttavia la distorsione svanisce asintoticamente.
* $S$ è uno stimatore **consistente** di $\sigma$: $$S \overset{p} \to \sigma,\ per\ n \to \infty$$
* $S$ è uno stimatore **asintoticamente normale**: $$S \overset{p} \to N(\sigma, \frac{1}{4\sigma^2}Var(S^2))\ per\ n \to \infty$$
### Errore Standard
L'**Errore Standard** di uno stimatore  corrisponde alla **deviazione standard**  dello stesso: $$SE(\hat{\theta}) = SD(\hat{\theta})$$. Per esempio l'errore standard della media campionaria è: $$SE(\hat{\mu}) = SE(\overline{X}) = \frac{\sigma}{\sqrt{n}} $$ Anche l'errore standard deve essere stimato e in particolare $\hat{SE}(\hat{\mu})$ è uno stimatore di $SE(\hat{\mu})$ ottenuto mediante la **deviazione standard campionaria**: $$\hat{SE}(\hat{\mu}) = \frac{S}{\sqrt{n}}$$
* asintoticamente **non distorto**
* **consistente**
* asintoticamente **normale**
### Precisione e Accuratezza
La qualità di uno stimatore viene valutata in base:
* **Accuratezza**: stimatore tanto *più accurato* quanto *meno è distorto*.
* **Precisione**: stimatore tanto più *preciso* quanto *meno è variabile*.
Accuratezza e precisione sono combinate nell'**errore quadratico medio**: $$MSE(\hat{\theta}) = E(\hat{\theta} - \theta)^2 = Var(\hat{\theta}) + Bias(\hat{\theta})^2$$
### Confronto fra stimatori
* Se entrambi gli stimatori sono *non distorti* si prende quello con la *minor varianza*.
* Se entrambi sono *distorti* si prende quello con l'*errore quadratico medio inferiore*, tuttavia uno stimatore con un *basso errore quadratico medio* ma un'*alta varianza* è spesso considerato inaccettabile.
### Scarto Interquantile
Si vuole una misura della variabilità che sia *meno sensibile della varianza*  alle osservazioni estreme. Si utilizza lo **Scarto Interquantile**: $$\mathcal{IQR} = \mathcal{Q_3} - \mathcal{Q_1}$$
dove $\mathcal{Q_1}$ e $\mathcal{Q_3}$ sono rispettivamente il *primo* e il *terzo quartile*.
Lo  scarto interquantile si trova anche nella **versione campionaria**: $$\hat{\mathcal{IQR}} = \mathcal{\hat{Q_3}} - \mathcal{\hat{Q_1}}$$
dove $\mathcal{\hat{Q_1}}$ e $\mathcal{\hat{Q_3}}$ sono rispettivamente il *primo* e il *terzo quartile campionario*.
### Valori anomali
Una regola empirica suggerisce che i **valori anomali** (o **outliers**) sono le osservazioni che sono:
* **inferiori** a $\mathcal{\hat{Q_1}} - 1.5 \cdot \mathcal{\hat{IQR}}$
* **superiori** a $\mathcal{\hat{Q_3}} + 1.5 \cdot \mathcal{\hat{IQR}}$

Questa regola è ben motivata per **distribuzioni normali**, tuttavia i dati registrati hanno spesso **distribuzioni esponenziali**.

Quando si incontrano **dati anomali** è importante capire la causa di tali valori, poichè spesso contengono **informazioni importanti**. Vengono tuttavia rimossi quando:
* corrispondono ad **errori**
* corrispondono ad osservazioni provenienti da **altre popolazioni**
## Analisi grafice
### Sintesi grafiche
Utili per individuare:
* **modello probabilistico** per descrivere i dati
* **metodo statistico** per l'analisi dei dati
* **outliers**
* fonti di **eterogeneità** $\rightarrow$ dati molto diversi fra loro
* **patterns** e **trends**
* **relazioni** fra 2 o più variabili
### Istogrammi
* Servono per visualizzare la **forma di una distribuzione**.
* Sono costruiti da un insieme di **rettangoli adiacenti**
* Si costruiscono dividendo il campo di variazione dei dati (o **range**) in intervalli (o **bins**) e contando il numero di osservazioni presenti in ciascun bin

Considereremo solo istogrammi formati da **bins della stessa ampiezza**:
* **istogrammi di frequenza**: l'*altezza dei rettangoli* corrisponde al *numero di osservazioni* di ogni intervallo.
* **istogrammi di frequenza relativa**: l'*altezza dei rettangoli* corrisponde alla *proporzione di osservazione* in ciascun intervallo.
**Esempio**:

![[Pasted image 20240222100131.png]]
In particolare nel caso di osservazioni  di *variabili continue* al crescere della dimensione campionaria gli istogrammi convergeranno alla *funzione di densità* della variabile.

![[Pasted image 20240222094858.png]]
### Esempi di istogrammi
![[Pasted image 20240222095021.png]]
### Scelta degli intervalli
Risulta importante scegliere intevalli utili a comprendere la distribuzione dei dati, poichè una cattiva scelta degli intervalli inficia la comprensione della loro distribuzione:

![[Pasted image 20240222095252.png]]
I software come R implementano regole per il calcolo ottimale automatico del numero di intervalli, tuttavia talvolta è necessario *ritoccarli a mano*.

### Grafico a scatola con i baffi
Il **grafico a scatola con i baffi** (o **boxplot**) viene costruito con le seguenti statistiche:
* *minimo*
* *primo quartile*
* *mediana*
* *terzo quartile*
* *massimo*

In particolare la **scatola** contiene il 50% delle osservazioni più centrali fra il *primo* e il *terzo quartile*, mentre i **baffi** si estendono dalla scatola parallelamente verso il *massimo* e il *minimo*. Le osservazioni anomale sono indicate con dei *punti oltre i baffi*.

![[Pasted image 20240222100007.png]]
### Boxplot appaiati
Utilizzati per confrontare *diverse popolazioni* o *sotto-popolazioni*:

![[Pasted image 20240222100435.png]]
### Grafici a dispersione
**Esempio**:

![[Pasted image 20240222100529.png]]
*Nota*: il professore consiglia di usare il **grafico a bolle** (a sinistra dell'esempio) o il **cheatring** (che vedremo nel 2° laboratorio).