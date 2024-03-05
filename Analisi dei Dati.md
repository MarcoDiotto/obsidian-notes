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
* Uno *stimatore* è **non** **distorto** se $E(\hat{\theta}) = \theta$ per tutti i valori di $\theta$. La **distorsione** dello stimatore è $Bias(\hat{\theta}) = E(\hat{\theta} - \theta)$. Lo stimatore non distorto non **sottostima** né **sovrastima** il parametro.
*Esempio*:
$$ E(\overline{X}) = \frac{1}{n} \cdot \sum_{i=1}^n E(X_i) = \frac{1}{n} \cdot \sum_{i = 1}^n \mu = \mu$$

* Uno *stimatore* è **consistente** se al crescere della dimensione campionaria $n$ il suo errore campionario converge a 0. $$Pr(|\hat{\theta} - \theta| > \epsilon) \rightarrow 0\ per\ n \rightarrow \infty,\ per\ qualsiasi\ \epsilon > 0$$ ovvero: $$\hat{\theta} \overset{p}{\to}  \theta\ per\ n \rightarrow \infty$$ la **consistenza** si può verificare con la **Legge dei grandi numeri**, o con la **Diseguaglianza di Chebyshev**, ma solo se i dati sono indipendenti. Vediamo un *esempio* con la media campionaria $\overline X$.
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
##  Laboratorio 1: Media Campionaria

```r
popolazione <- rexp(n = 5000, rate = 1/40)
media.pop <- mean(popolazione)
campione <- sample(popolazione, size = 50)
mean(campione)
```

Grazie a `sample` possiamo ottenere un campione casuale da utilizzare per i nostri calcoli.
### Non Distorsione e Normalità Asintotica della Media Campionaria
```r
medie <- replicate(1000, mean(sample(popolazione, size = 50)))
range(medie)
mean(medie)
```
La funzione `range` ci indica l'intervallo entro cui si trovano le nostre medie:
Grazie a `mean(medie)` facciamo la **media delle medie** e otteniamo un risultato molto vicino alla media dell'intera popolazione.$\to$ Abbiamo osservato la **non distorsione** della media campionaria.
#### Visualizzazione Grafica

```r
hist(medie, col = "steelblue")
```

![[Pasted image 20240227110944.png]]

```r
hist(medie, col = "steelblue", breaks = 15)
```

![[Pasted image 20240227110750.png]]

```r
abline(v = media.pop, col = "red", breaks = 15, main = "Titolo", xlab = "asse delle x", ylab = "asse delle y")
```

![[Pasted image 20240227111036.png]]

```r
hist(medie, col = "steelblue", breaks = 15, freq = FALSE)
```

![[Pasted image 20240227111159.png]]

```r
curve(dnorm(x, mean = media.pop, sd = media.pop /sqrt(50)), col = "red", lwd = 1.5, add = TRUE)
```

![[Pasted image 20240227111308.png]]

*Note*:
* Grazie a `breaks` inseriamo il numero di rettangoli
* Grazie ad `abline` posso aggiungere una linea, nel nostro caso la media
* Grazie a `main`,  `xlab` e `ylab` inserisco il titolo e i nomi degli assi x e y
* Grazie a `freq = FALSE` valuto la **densità** e non la **frequenza
* Grazie all'ultima funzione riusciamo a vedere la relativa curva normale

### Consistenza della Media Campionaria

```r
permutazione <- sample(popolazione)
numeratori <- cumsum(permutazione)
denominatori <- 1:5000
medie = numeratori / denominatori
```
*Note*:
* La funzione `sample` questa volta serve ad avere le osservazioni in ordine diverso
* La funzione `cumsum` fa le **somme cumulative** in ogni posizione del vettore
#### Visualizzazione grafica

```r
plot(medie, col = "steelblue", type = "l", lwd = 2)
```

![[Pasted image 20240227112603.png]]

```r
abline(h = media.pop, lty = dashed, col = "red", lwd = 1.5)
```

![[Pasted image 20240227112702.png]]

## Laboratorio 2: Analisi Descrittive
### Sintesi Numeriche
Iniziamo utilizzando i dati sui tempi di elaborazione dei processi presentati nel Capitolo 8 del Baron (2014)

Per leggere i dati si usa il seguente comando:
```r
cpu <- scan("CPU-times.txt")
cpu
```

Calcoliamo la **media**:
```r
mean(cpu)
```

Calcoliamo la **mediana**:
```r
median(cpu)
```

Calcoliamo **primo**, **secondo** e **terzo quartile**:
```r
quantile(cpu, probs = 0.25, type = 2)
quantile(cpu, probs = 0.5, type = 2)
quantile(cpu, probs = 0.75, type = 2)
```

`type = 2` serve per essere coerenti col libro di testo, le funzioni di default di R sono:
```r
quantile(cpu, probs = 0.25)
quantile(cpu, probs = 0.5)
quantile(cpu, probs = 0.75)
```

Calcoliamo la **varianza**:
```r
var(cpu)
```

Calcoliamo la **deviazione standard**:
```r
sd(cpu)
```

Calcoliamo lo **scarto interquantile**:
```r
Q1 <- quantile(cpu, probs = 0.25, type = 2)
Q3 <- quantile(cpu, probs = 0.75, type = 2)
Q3 - Q1
```

### Sintesi Grafiche
Per creare **istogrammi** si utilizza `hist`:
```r
isto <- hist(cpu, main = "Tempi elaborazione CPU", xlab = "Tempo (sec)"
ylab = "Frequenze", col = "steelblue")
```

![[Pasted image 20240227114228.png]]

Per **esplorare le componenti** di `isto`:
```r
names(isto)
```

Per **estrarre le componenti** di isto si utilizza `$`:
```r
##osservazioni per intervallo
isto$counts

## intervalli (breaks)
isto$breaks
```

Per ottenere l'istogramma con la **densità** si utilizza `freq = FALSE`:
```r
isto <- hist(cpu, freq = FALSE, main = "Tempi elaborazione CPU", xlab = "Tempo (sec)", ylab = "Densita'", col = "steelblue")
```

![[Pasted image 20240227114659.png]]

La **densità** si ottiene con:
```r
isto$density
```

che è equivalente a:
```r
freqrel <- isto$counts / sum(isto$counts)
freqrel / 20
```

L’opzione `breaks` permette, in principio, di modificare il numero di intervalli con cui è disegnato l’istogramma. In pratica, R prende l’indicazione fornita con `breaks` come un suggerimento e sceglie un numero di intervalli vicino che soddisfi delle regole interne:

```r
isto <- hist(cpu, freq = FALSE, main = "Tempi elaborazione CPU", xlab = "Tempo (sec)", ylab = "Densita'", col = "steelblue", breaks = 12)
```

![[Pasted image 20240227114904.png]]

Spesso è utile sovrapporre all’istogramma una stima della funzione di densità calcolata con la funzione `density`:

```r
hist(cpu, freq = FALSE, main = "Tempi elaborazione CPU",  xlab = "Tempo (sec)", ylab = "Densita'", col = "steelblue", breaks = 12)
lines(density(cpu), col = "red", lwd = 2) ## linea con spessore doppio (lwd = 2)
```

![[Pasted image 20240227114943.png]]

Per creare i **boxplot** si utilizza `boxplot`:
```r
bp <- boxplot(cpu, main = "Tempi elaborazione CPU", col = "steelblue")
```

![[Pasted image 20240227115106.png]]

Le statistiche utilizzate per disegnare il boxplot si possono ottenere con la funzione `summary`:
```r
summary(cpu)
```

In realtà, però, le statistiche usate dalla funzione `boxplot` sono leggermente diverse:
```r
bp$stats
```

Lo slot `stats` dell’oggetto `bp` contiene, nell’ordine, il “baffo” inferiore, il primo quartile, la mediana, il terzo quartile, il “baffo” superiore. Il baffo superiore si ferma a 89 poiché il boxplot non disegna punti oltre il seguente limite:
```r
59 + 1.5 * (59 - 34)
```

e l’osservazione più grande che non supera questo limite è appunto
```r
max(cpu[cpu <= 96.5])
```

Possiamo aggiungere al boxplot la **media dei tempi di elaborazione** con la funzione `points`:
```r
boxplot(cpu, col = "steelblue")
points(mean(cpu), pch = "+") ## pch significa "point character"
```

![[Pasted image 20240227115245.png]]

Il file **CPU-times-2.txt** contiene un secondo campione di tempi di elaborazione:
```r
cpu2 <- scan("CPU-times-2.txt")
```

Possiamo confrontare visivamente i due campioni attraverso due boxplot appaiati:
```r
boxplot(cpu, cpu2, col = c("steelblue", "lightblue"), names = c("Campione 1", "Campione 2"))
```

![[Pasted image 20240227115321.png]]
Nell’ultima chiamata a `boxplot` abbiamo usato la funzione `c` (“combine”) per creare un vettore di due colori, `c("steelblue", "lightblue")`, e un vettore di due etichette, `c("campione 1", "campione 2")`.

Vediamo come implementare i **grafici a dispersione** con un *esempio*:

Il file **antivirus.csv** contiene i dati discussi nel capitolo 8 del Baron (2014) sulla relazione fra l’utilizzo degli antivirus nell’ultimo mese e i virus (_worms_) individuati. Possiamo importare i dati in **R** con la funzione `read.csv`:
```r
antivirus <- read.csv("antivirus.csv")
antivirus
```

![[Pasted image 20240227115500.png]]

Di seguito il**grafico a dispersione** del numero di _worms_ in funzione del numero di volte che l’antivirus è stato eseguito nell’ultimo mese:
```r
with(antivirus, plot(x, y, xlab = "Esecuzioni antivirus", ylab = "Worms individuati"))
```

![[Pasted image 20240227115542.png]]

Siccome ci sono molte osservazioni ripetute il grafico non coglie davvero la struttura dei dati. Possiamo ovviare a questo problema aggiungendo un **piccola quantità di errore casuale** ad ogni osservazione con la funzione `jitter` (“agitato”):
```r
with(antivirus, plot(jitter(x), jitter(y), xlab = "Esecuzioni antivirus", ylab = "Worms individuati"))
```

![[Pasted image 20240227115636.png]]

Due esempi vengono riportati nel secondo laboratorio al [seguente link](https://mega.nz/file/BjUQTZwD#iYoqvoX_IAJopybZxiz6T2JDCEo2WPCZPvzjcsSKrtg).
## Esercizi Unità 1
Gli esercizi della prima unità sono presenti al [seguente link](https://mega.nz/file/cr1X0TJQ#sl-Tx23PS25I2uQyT1n5bJeXihw8t1i77Fw1o5035A4).
# Stime
___
## Modelli statistici
Supponiamo che i dati $x = (x_1, ..., x_n)$ provengano da una variabile casuale la cui distribuzione proviene da un parametro ignoto $\theta$.

*Terminologia*: 
	i dati sono generati da un **modello statistico** indicizzato da un parametro $\theta$ ignoto e appartenente allo **spazio parametrico** $\Theta \in \mathbb{R}^k$

Il *modello statistico* è:
* nel caso discreto una **classe di funzione di probabilità** $\mathbb{P}(x;\theta)$
* nel caso continuo una **classe di densità** $\mathcal{f}(x;\theta)$

**Esempi dal Baron**:

![[Pasted image 20240305112724.png]]
![[Pasted image 20240305112747.png]]
## Il Metodo dei Momenti
Il **metodo dei monìmenti** è il più semplice metodo per stimare il parametro di un modello statistico.

Questo metodo costruisce uno stimatore di $\theta$ confrontando:
* **Momenti di popolazione** $\to$ momenti teorici del modello statistico assunto.
* **Momenti campionari** $\to$ caratterizzano i dati osservati

## Momenti
* Il $k$-esimo momento di popolazione è: $$\mu_k = \mathbb{E}(X^k)$$
* Il $k$-esimo momento campionario è: $$M_k = \frac{1}{n}\sum_{i = 1}^{n} X^k_i\ \ \ \ \ \ \ (M_1 = \overline{X})$$ con valore osservato: $$m_k = \frac{1}{n}\sum_{i = 1}^{n} x^k_i\ \ \ \ \ \ \ (m_1 = \overline{x})$$

*Nota*: Il Baron non differenzia fra $M_k$ e $m_k$

Quindi:
* $M_k$ è uno **stimatore** di $\mu_k$
* $m_k$ è una **stima** di $\mu_k$
## Momenti Centrali
* Il $k$-esimo momento centrale di popolazione è: $$\mu_k' = \mathbb{E}(X - \mu)^k$$
* Il $k$-esimo momento centrale campionario è: $$M_k' = \frac{1}{n}\sum_{i = 1}^{n}(X_i - \overline{X})^k\ \ \ \ \ \ \ (M'_2 = \frac{S^2(n-1)}{n})$$ con valore osservato: $$m_k' = \frac{1}{n}\sum_{i = 1}^{n}(x_i - \overline{x})^k\ \ \ \ \ \ \ (m'_2 = \frac{s^2(n-1)}{n})$$

*Nota*: Il Baron non differenzia fra $M_k'$ e $m_k'$

Quindi:
* $M_k'$ è uno **stimatore** di $\mu_k'$
* $m_k'$ è una **stima** di $\mu_k'$
## Ancora sul Metodo dei Momenti
Per stimare il parametro $\theta$ si risolve il sistema di $k$ equazioni ottenuto uguagliando i $k$ momenti di popolazione ai rispettivi $k$ elementi campionari:

![[Pasted image 20240305114309.png]]
*Nota*: si sceglie fra momenti semplici e centrali puramente in base alla convenienza.

**Esempio dal Baron**:

![[Pasted image 20240305114401.png]]
## Ancora sul tempo di elaborazione:
Torniamo al campione dei 30 tempi di elaborazione: 

![[Pasted image 20240305114550.png]]

Quale modello statistico descrive accuratamente questi dati?

## La Distribuzione Gamma
Distribuzione continua per osservazioni positive: $$\mathcal{f}(x;\alpha;\lambda) = \frac{\lambda^\alpha}{\Gamma(\alpha)}x^{\alpha - 1} e^{-\lambda x},\ \ \ \ (x > 0)$$ Dove $\Gamma(\cdot)$ è la **funzione gamma**.

Parametro $\theta = (\alpha,\lambda)$:
* **Parametro di forma** $\alpha > 0$
* **Parametro di frequenza** $\lambda > 0$

**Spazio parametrico**: $\Theta \in \mathbb{R}_+ \times \mathbb{R}_+$ dove $\mathbb{R}_+$ sono i numeri reali positivi

Quando $\alpha = 1$ la distribuzione gamma si riduce alla distribuzione esponenziale: $$\mathcal{f}(x,\lambda) = \lambda e^{-\lambda x},\ \ \ \  x > 0$$
![[Pasted image 20240305115307.png]]

## Stima con il metodo dei momenti dei parametri di una distribuzione gamma

![[Pasted image 20240305115404.png]]

## Il Metodo della Massima Verosimiglianza

Lo stimatore di massima verosimiglianza è quel valore del parametro $\theta$ che massimizza la **funzione di verosimiglianza** ("likelyhood").

La funzione di verosimiglianza è *proporzionale* alla probabilità di osservare ciò che è stato effettivamente osservato.

Nel **caso discreto** la funzione di verosimiglianza è proporzionale alla funzione di probailità congiunta dei dati: $$L(\theta) \alpha\ \ \mathbb{P}(X_1 = x_1, ..., X_n = x_n; \theta)$$ che in un campione casuale semplice diventa: $$L(\theta)\alpha\ \ \prod_{i = 1}^{n} \mathbb{P}(X_i = X_i; \theta)$$
## Esempio
Una software house dichiara che il suo software per il riconoscimento facciale ha un’accuratezza del 80% in condizioni ‘difficili’ (volto parzialmente coperto e bassa luminosità). Un blogger dopo diversi esperimenti afferma che in realtà l’accuratezza del software  è pari al 70%.  Incuriositi dalla disputa, effettuiamo un esperimento su 15 fotografie di volti da ‘riconoscere in condizioni difficili’ e troviamo che solo in 11 fotografie il volto viene riconosciuto correttamente. Cosa concludiamo? Di seguito proviamo a dare una prima risposta con la funzione di verosimiglianza.
Indichiamo con $\theta$ la ‘vera’ proporzione di fotografie in cui il volto è riconosciuto correttamente nonostante le condizioni difficili. Innanzitutto, dobbiamo individuare un modello statistico che descrive il ‘meccanismo generatore dei dati’. In questo caso, il modello più ragionevole sembra essere quello binomiale. La verosimiglianza per $\theta$ è, quindi proporzionale alla  probabilità di osservare 11 successi su 15 prove in un  modello binomiale con probabilità di successo $\theta$: $$L(\theta) = \binom{15}{11}\ \theta^{11}(1 - \theta)^4$$
Se avesse ragione la software house allora il valore osservato della verosimiglianza sarebbe: $$L(0.8) = \binom{15}{11}\ 0.8^{11}0.2 = 0.19$$
![[Pasted image 20240305122217.png]]

Se avesse invece ragione il blogger: $$L(0.7) = \binom{15}{11}\ 0.7^{11}0.3^4 = 0.22$$
![[Pasted image 20240305122647.png]]

La verosimiglianza del blogger è più alta e possiamo quantificare la preferenza che il nostro esperimento gli accorda con il rapporto delle verosimiglianze:

![[Pasted image 20240305122749.png]]

e concludere che, alla luce del nostro esperimento, è 17% ‘più verosimile’ l’ipotesi del blogger.  Notiamo che i fattori binomiali si cancellano Infatti, tutte le procedure basate sulla verosimiglianza sono invarianti rispetto a termini costanti che appaiono nelle verosimiglianza. Per questo motivo la verosimiglianza è definita come proporzionale alla probabilità di osservare i dati.  I termini costanti possono essere, quindi, rimossi dal calcolo della verosimiglianza.
## La log-verosimiglianza
La log-verosimiglianza è definita come: $$\mathcal{l}(\theta) = log\ L(\theta).$$Siccome il logaritmo è una funzione crescente,  massimizzare $L(\theta)$ o $\mathcal{l}(\theta)$ è **equivalente**.

Conviene massimizzare $\mathcal{l}(\theta)$ perché le derivate delle somme sono più facile delle derivate dei prodotti.

Inoltre quando la massimizzazione avviene numericamente, $L(\theta)$ può creare problemi per i valori molto piccoli che spesso assume.

Nel caso discreto la log-verosimiglianza è: $$\mathcal{l}(\theta) = \sum_{i = 1}^{n} log\ \mathbb{P}(X_i = x_i; \theta).$$
**Esempio dal Baron**:

![[Pasted image 20240305121439.png]]
![[Pasted image 20240305121507.png]]
