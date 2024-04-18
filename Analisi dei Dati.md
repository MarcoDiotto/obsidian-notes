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
* **Quartile**: divide la funzione di ripartizione in quarti (Esempio: 1° quartile $=$ 25° percentile)3
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
Il **metodo dei momenti** è il più semplice metodo per stimare il parametro di un modello statistico.

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
Per stimare il parametro $\theta$ si risolve il sistema di $k$ equazioni ottenuto uguagliando i $k$ momenti di popolazione ai rispettivi $k$ momenti campionari:

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

Lo stimatore di massima verosimiglianza è quel valore del parametro $\theta$ che massimizza la **funzione di verosimiglianza** ("likelihood").

La funzione di verosimiglianza è *proporzionale* alla probabilità di osservare ciò che è stato effettivamente osservato.

Nel **caso discreto** la funzione di verosimiglianza è proporzionale alla funzione di probailità congiunta dei dati: $$L(\theta) \propto \mathbb{P}(X_1 = x_1, ..., X_n = x_n; \theta)$$ che in un campione casuale semplice diventa: $$L(\theta)\propto \prod_{i = 1}^{n} \mathbb{P}(X_i = X_i; \theta)$$
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

![[Pasted image 20240307093227.png]]

La log-verosimiglianza è definita come: $$\mathcal{l}(\theta) = log\ L(\theta).$$Siccome il logaritmo è una funzione crescente,  massimizzare $L(\theta)$ o $\mathcal{l}(\theta)$ è **equivalente**.

Conviene massimizzare $\mathcal{l}(\theta)$ perché le derivate delle somme sono più facile delle derivate dei prodotti.

Inoltre quando la massimizzazione avviene numericamente, $L(\theta)$ può creare problemi per i valori molto piccoli che spesso assume.

Nel caso discreto la log-verosimiglianza è: $$\mathcal{l}(\theta) = \sum_{i = 1}^{n} log\ \mathbb{P}(X_i = x_i; \theta).$$
**Esempio dal Baron**:

![[Pasted image 20240305121439.png]]
![[Pasted image 20240305121507.png]]

## Caso Continuo
Nel caso continuo, la probabilità di osservare esattamente un certo valore $x$ è $\mathbb{P}(X = x) = 0$.

Per un valore "piccolo" $h$ abbiamo che: $$\mathbb{P}(x - h < X < x + h) = \int_{x-h}^{x+h}\mathcal{f}(x;\theta) dx \sim 2h\mathcal{f}(x;\theta)$$
![[Pasted image 20240307090649.png]]

Nel caso continuo il metodo della massima verosimiglianza **massimizza** la probabilità di osservare dei **valori vicini** a ciò che è stato effettivamente osservato: $$L(\theta) \propto \mathcal{f}(x_1, ..., x_n; \theta)$$
Nel caso di un campione casuale abbiamo: $$L(\theta) \propto \prod_{i = 1}^{n} \mathcal{f}(x_i; \theta)$$
La corrispondente log-verosimiglianza è (a meno di termini costanti che eliminiamo): $$\mathcal{l}(\theta) = \sum_{i = 1}^{n} log\ \mathcal{f}(x_i; \theta)$$
**Esempio dal Baron**:

![[Pasted image 20240307091458.png]]
![[Pasted image 20240307091513.png]]
## Problemi regolari di stima
Lo stimatore di massima verosimiglianza gode di importanti proprietà che valgono sotto *opportune assunzioni di regolarità*.

Una delle assunzioni è che stiamo lavorando con un **problema di stima regolare**.

La più rilevante condizione affinché un problema di stima sia regolare è che il **supporto** (= spazio in cui si muove la variabile) delle variabili casuali **non dipende dal parametro del modello**.

Le altre assunzioni sono più tecniche e richiedono che la funzione di probabilità (nel caso discreto) o di densità (nel caso continuo) sia **sufficientemente regolare**.

In particolare la funzione di probabilità/densità deve avere **derivate finite** fino ad un certo ordine.
## Esempi
Esempi di **problemi regolari di stima** sono stimare:
* I parametri $\mu$ e $\sigma^2$ di una variabile casuale normale
* Il parametro $\lambda$ di una variabile casuale di Poisson
* il parametro $p$ di una variabile casuale binomiale

Un esempio di **problema non regolare di stima** è stimare il parametro $\theta$ di una variabile uniforme nell'intervallo $[0,\theta]$.

Quest'ultimo non è un problema di stima regolare perché il supporto della variabile è $[0,\theta]$, cioè dipende dal parametro stesso.
## Verosimiglianza e problemi regolari di stima
Nei problemi regolari di stima, lo **stimatore di massima verosimiglianza** si trova ispezionando le derivate prime e seconde della (log-)verosimiglianza.

La derivata prima della log-verosimiglianza si chiama **funzione punteggio** (o **score function**).

I punti stazionari della verosimiglianza sono gli **zeri della funzione punteggio**, cioè i punti $\tilde{\theta}$ che risolvono l'**equazione di verosimiglianza**: $$\frac{d}{d\theta}\mathcal{l}(\tilde{\theta}) = 0$$ Un punto stazionario di $\mathcal{l}(\theta)$ è **un massimo locale** se la derivata seconda calcolata in quel punto è **negativa** $$\frac{d^2}{d\theta^2}\mathcal{l}(\tilde{\theta}) =<0$$
## Esempio di problema regolare di stima
Consideriamo un campione casuale semplice  dalla variabile casuale con densità: $$\mathcal{f}(x; \beta) = \begin{cases} \frac{\beta}{x^{\beta + 1}}, \ \ \ se\ x > 1, \beta > 1\\  0\ \ \ \ \ \ \ \ \ \  atrimenti   \end{cases}$$
La verosimiglianza per $\beta$ è $$L(\beta) = \beta^n \prod_{i = 1}^n X_i^{-(\beta + 1)}$$ 
La log-verosimiglianza è (a meno di termini costanti): $$\mathcal{l}(\beta) = n\ log(\beta) - \beta \sum_{i = 1}^n log X_i$$
La funzione punteggio è $$\mathcal{l}'(\beta) = \frac{n}{\beta} - \sum_{i = 1}^{n} log X_i$$
L'equazione di verosimiglianza è: $$\frac{n}{\beta} - \sum_{i = 1}^{n} log X_i = 0$$
La soluzione dell'equazione di verosimiglianza è $$\tilde{\beta} = \frac{n}{\sum_{i = 1}^{n} log X_i}$$
e coincide con lo stimatore di massima verosimiglianza poiché $$\mathcal{l}''(\beta) = - \frac{n}{\beta^2} < 0$$
Quindi la stima di massima verosimiglianza è $$\tilde{\beta} = \frac{n}{\sum_{i  = 1}^{n} log X_i}$$
## Esempio di problema non regolare di stima
Consideriamo un campione casuale semplice dalla variabile casuale con densità $U(0;\theta)$ ovvero: $$\mathcal{f}(x;\theta) = \begin{cases} \frac{1}{\theta}\ \ \ \ se\ x \in [0; \theta]\\ 0\ \ \ \ altrimenti \end{cases}$$
La verosimiglianza di $\theta$ è: $$L(\theta) = \begin{cases} \frac{1}{\theta^n}\ \ \ \ se\ 0 \leq X_i \leq \theta\ per\ ogni\ i\\ 0\ \ \ \ altrimenti \end{cases}$$
ovvero: $$L(\theta) = \begin{cases} \frac{1}{\theta^n}\ \ \ \ se\ max_iX_i \leq \theta\ e\ min_iX_i \geq 0\\ 0\ \ \ \ altrimenti \end{cases}$$
*Esempio con un ipotetico dataset di 50 osservazioni in cui il massimo delle osservazioni vale 5*:

![[Pasted image 20240307100555.png]]

Lo stimatore di massima verosimiglianza è $\hat{\theta} = max_iX_i$

Il massimo di $L(\theta)$ non può essere trovato tramite differenziazione di $L(\theta)$ (o di $\mathcal{l}(\theta)$) perché si trova in **un punto di discontinuità**.
## Errori standard
Gli errori standard servono a misurare la **precisione** degli stimatori.

*Reminder della terminologia di Statistica*:
* **accuratezza** $\to$ concetto opposto di **distorsione**.
* **precisione** $\to$ opposto di **variabilità**.
## Stimare gli errori standard
Gli errori standard solitamente sono **funzione del parametro stesso** e quindi *vanno a loro volta stimati*.

**Esempio del Baron**:

![[Pasted image 20240307101205.png]]

Tuttavia stimare gli errori standard può essere complicato anche in modelli semplici.

**Esempio del Baron**:

![[Pasted image 20240307101303.png]]
![[Pasted image 20240307101329.png]]
## Proprietà asintotiche dello stimatore di massima verosimiglianza
Sotto **assunzioni** che valgono nei problemi che affronteremo in questo corso, lo stimatore di massima verosimiglianza e:
* **Asintoticamente non distorto**: $$E(\hat{\theta}) \to \theta,\ \ \ \ per\ n \to \infty$$
* **Consistente**: $$\hat{\theta} \overset{p}\to \theta,\ \ \ \ per\ n \to \infty$$
* **Asintoticamente normale** con distribuzione limite: $$\hat{\theta} \sim N\{\theta, I(\theta)^{-1}\},\ \ \ \ \textbf{per\ n\ sufficientemente\ grande}$$ dove $I(\theta)$ è l'**informazione attesa di Fisher**.
## Informazione attesa di Fisher
L'**informazione attesa di Fisher** è definita come: $$I(\theta) = E\{-\frac{d^2}{d\theta^2}\mathcal{l}(\theta)\}$$ $$= E \{-\frac{d^2}{d\theta^2} \sum_{i = 1}^n log\ \mathcal{f}(X_i;\theta)\}$$ 
$$= \sum_{i = 1}^nE \{-\frac{d^2}{d\theta^2} log\ \mathcal{f}(X_i;\theta)\}$$
Nel caso di un *campione casuale semplice abbiamo*: $$I(\theta) = n\ E \{-\frac{d^2}{d\theta^2} log\ \mathcal{f}(X_i;\theta)\}$$ cioè l'informazione del campione è pari a $n$ volte l'informazione contenuta in una singola osservazione.
## Informazione attesa e osservata

L'**informazione osservata è definita come**: $$J(\theta) = -\mathcal{l}'' =\sum_{i = 1}^n \{-\frac{d^2}{d\theta^2} log\ \mathcal{f}(X_i;\theta)\} $$ $$ = \sum_{i = 1}^n g(X_i)$$
La *Legge dei grandi numeri* ci dice che per $n \to \infty$: $$\frac{J(\theta)}{n} \overset{p}\to E\{g(X_1)\} = E \{-\frac{d^2}{d\theta^2} log\ \mathcal{f}(X_i;\theta)\}$$ ovvero $J(\theta) \sim I(\theta)$ per $n$ *sufficientemente grande*.

Differenza fra le due informazioni:
* $I(\theta)$ e una media dell’informazione in ipotetici  campioni ripetuti.  
* $J(\theta)$ riflette l’informazione nel particolare campione osservato.
## Errore standard dello stimatore di massima verosimiglianza
Sappiamo che per campioni sufficientemente grandi e modelli che rispettino le assunzioni di regolarità: $$\hat{\theta} \sim N\{\theta, I(\theta)^{-1}\}$$ Quindi l'**errore standard** dello stimatore di massima verosimiglianza $\hat{\theta}$ è asintoticamente pari a: $$SE(\hat{\theta}) \sim I(\theta)^{-\frac{1}{2}}\ \ \ \ \ \textbf{per n sufficientemente grande}$$ La **stima dell'errore standard** di $\hat{\theta}$ è: $$\hat{SE}(\hat{\theta}) = I(\hat{\theta})^{\frac{1}{2}}$$
Alternativamente si può stimare l'errore standard di $\hat{\theta}$ con l'**informazione oservata**: $$\hat{SE}(\hat{\theta}) = J(\hat{\theta})^{\frac{1}{2}}$$ *Nota*: argomenti teorici suggeriscono di preferire la stima con $J$ perchè riflette l’effettiva informazione nei dati.
## Efficienza
Lo stimatore di massima verosimiglianza gode di una importante proprietà di ottimalità.

La **diseguaglianza di Cramér-Rao** identifica il limite inferiore della varianza di uno stimatore $\hat{\theta}$ **non distorto** di $\theta$: $$Var(\hat{\theta}) \geq I(\theta)^{-1}$$
dove $I(\theta)$ è l'informazione attesa di Fisher.

Uno stimatore non distorto la cui varianza raggiunge il limite di Cramér-Rao  è detto **efficiente**.

Lo stimatore di massima verosimiglianza è, quindi, **asintoticamente efficiente**.
## Esempi
Gli esempi si trovano alla slide 35 al [seguente link](https://mega.nz/file/Q3kAHQCK#P0YP3k5RwcRSebJIZJ_hhkFGa5pqbaojMK-UXjaBfIs)
## Invarianza
Una proprietà dello stimatore di massima verosimiglianza molto rilevante è l’**invarianza**:
>se $\hat{\theta}$ e lo stimatore di massima verosimiglianza di $\theta$ allora $g(\hat{\theta})$ è lo stimatore di massima verosimiglianza di $\psi = g(\theta)$.

**Esempio**:
Supponiamo che il numero di utenti che si collegano ad un server in un instante di tempo si distribuisca come una *variabile di Poisson* di parametro $\lambda$.
La stima di massima verosimiglianza di $\lambda$ è $\hat{\lambda} = \overline{X}$.
Ci interessa stimare la probabilità che il numero di utenti superi un certo *livello critico* $c$.
Il *parametro di interesse* è: $$\psi = \mathbb{P}(X > c) = 1 - F(c)$$
L’invarianza dice che lo stimatore di massima verosimiglianza di $\psi$ è: $$\hat{\psi} = 1 - \hat{F}(c)$$ dove $\hat{F}(c)$ è la funzione di ripartizione di una *variabile di Poisson* con parametro $\hat{\lambda}$.
Supponiamo che la soglia critica per le capacità del server sia $c = 75$ utenti contemporanei.
In un campione casuale di $25$ instanti di tempo è stato osservato $\overline{x} = 62.7$ utenti contemporanei.
Lo stima di massima verosimiglianza è $\hat{\lambda} = 62.7$. 
La stima di massima verosimiglianza di $\psi$ è: $$\hat{\psi} = 1 - \sum_{x = 0}^{75} \frac{e^{-62.5}(62.7)^x}{x!}$$
Ovvero, utilizzando *R*:
```R
1 - ppois(75, lambda = 62.7)
```
## Quando il parametro è un vettore
Nelle gran parte delle applicazioni di interesse, la dimensione del parametro è *maggiore di uno*: $$\theta = \begin{pmatrix} \theta_1 \\ ... \\ \theta_k \end{pmatrix}$$
I risultati discussi finora si estendono in modo naturale nel caso di un vettore di parametri.
In particolare, lo stimatore di $\theta$ è un *vettore casuale* (= *vettore di variabili casuali*): $$\hat{\theta} = \begin{pmatrix} \hat{\theta}_1 \\ ... \\ \hat{\theta}_k \end{pmatrix}$$ in cui ogni componente $\hat{\theta}_r\ (r = 1 ... k)$ è una variabile causale.

I primi due momenti di $\hat{\theta}$ sono:
* Il **vettore dei valori attesi**: $$\mu = \begin{pmatrix} \mu_1 \\ ... \\ \mu_k \end{pmatrix}$$ con $\mu_r = E(\hat{\theta}_r),\ r = 1 ... k$.
* La **matrice di varianze - covarianze** $\Sigma$: $$\Sigma = \begin{pmatrix} \sigma_1^2 & \sigma_{12} & ... & \sigma_{1k} \\ ... & ... & ... & ...\\ \sigma_{k1} & \sigma_{k2} & ... & \sigma_k^2 \end{pmatrix}$$ con $\sigma_{rs} = Cov(\hat{\theta}_r, \hat{\theta}_s)$ e $\sigma_r^2 = \sigma_{rr},\ r,s = 1 ... k$.
    * Sulla diagonale si trovano le *varianze*.
    * In tutte le altre posizioni si trovano le *covarianze*.
## Lo stimatore di massima verosimiglianza
Nei problemi di stima ‘regolari’ lo **stimatore di massima verosimiglianza** si ottiene risolvendo le **equazioni di verosimiglianza**: 

![[Pasted image 20240314095552.png]]

La soluzione è lo **stimatore di massima verosimiglianza** se la matrice Hessiana delle derivate seconde è *definita negativa*.

![[Pasted image 20240314095721.png]]

Nei problemi regolari di stima, lo stimatore di massima verosimiglianza ha distribuzione limite **normale multivariata** di dimensione $k$: $$\hat{\theta} \sim MVN_k (\theta, I(\theta)^{-1})\ \ \ \ \textbf{per $n$ sufficientemente grande.}$$ 
dove $I(\theta)$ è la **matrice dell'informazione attesa**, oppure: $$\hat{\theta} \sim MVN_k (\theta, J(\theta)^{-1})\ \ \ \ \textbf{per $n$ sufficientemente grande.}$$ dove $J(\theta)$ è la **matrice dell'osservazione osservata**.

La matrice dell'informazione attesa è $I(\theta) = E\{J(\theta)\}$ con:

![[Pasted image 20240314100239.png]]


* La funzione di densità della distribuzione **normale univariata** è: $$\mathcal{f}(x;\mu,\sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}}\ exp \{-\frac{1}{2\sigma^2}(x - \mu)^2\}$$
* La funzione di densità della distribuzione **normale multivariata** è: $$\mathcal{f}(x;\mu,\Sigma) = (2\pi)^{-\frac{k}{2}}|\Sigma|^{-\frac{1}{2}}\ exp \{-\frac{1}{2}(x - \mu)^T\Sigma^{-1} (x - \mu)\}$$ dove $|\Sigma|$ è il *determinante* di $\Sigma$.

**Grafico della funzione di densità di una distribuzione normale bivariata**:

![[Pasted image 20240314100831.png]]

## Esempio
Un esempio si trova alla slide 49 al [seguente link](https://mega.nz/file/Q3kAHQCK#P0YP3k5RwcRSebJIZJ_hhkFGa5pqbaojMK-UXjaBfIs)
## Conclusione
Gli stimatori di massima verosimiglianza di $\mu$ e $\sigma^2$ sono:
* $\hat{\mu} = \overline{X}$
* $\hat{\sigma}^2 = \frac{1}{n}\sum_{i = 1}^n (X_i - \overline{X})^2$

Le matrici di informazione osservata e attesa coincidono in $\hat{\theta} = (\hat{\mu}, \hat{\sigma}^2)$.
* L'**errore standard stimato di $\hat{\mu}$** è: $$\hat{SE}(\hat{\mu}) = \frac{\hat{\sigma}}{\sqrt{n}}$$
* L'**errore standard stimato di $\sigma^2$** è: $$\hat{SE}(\hat{\sigma}^2) = \hat{\sigma}^2 \sqrt{\frac{2}{n}}$$
# Unità Intervallare
___
## Stimatori ed Errori Campionari
Quando otteniamo una stima $\hat{\theta}$ sappiamo che quasi sicuramente sarà *diversa dal vero valore* del  parametro $\theta$ a causa dell’errore campionario.

In altri termini, abbiamo stimato $\theta$ a meno di qualche **errore**.

Sorgono alcune domande:
* Quanto possiamo ‘credere’ in una stima?
* Quanto può essere distante la stima dal vero valore del parametro?
* Se otteniamo una certa stima $\hat{\theta}$ quali sono i valori plausibili per $\theta$?

Per rispondere a queste domande useremo gli **intervalli di confidenza**.
## Intervalli di Confidenza
Un intervallo $[A,B]$ è detto **intervallo di confidenza** per $\theta$ di livello $(1 - \alpha) 100\%$ se contiene il parametro con probabilità $(1 - \alpha)$: $$\mathbb{P}(A \leq \theta \leq B) = 1 - \alpha$$
La **probabilità di copertura** dell’intervallo $(1 − \alpha)$ viene detta anche **livello di confidenza**.
Attenzione all’interpretazione: $\theta$ è un numero, mentre gli estremi dell’intervallo $A$ e $B$ dipendono dai dati e quindi sono **variabili casuali**.
Solo dopo aver osservato i dati $A$ e $B$ sono valori numerici.

Si potrebbe più precisamente scrivere l’intervallo come: $$[A(X_1, ... , X_n), B(X_1, ..., X_n)]$$
Al variare del campione *anche l'intervallo varia*.

Ci aspettiamo che $(1 - \alpha)100\%$ degli intervalli contengano $\theta$.
## Interpretazione

![[Pasted image 20240328085759.png]]

*Nota*: per avere livelli di confidenza maggiori è necessario "allargare" gli intervalli, tuttavia potremmo andare incontro ad intervalli talmente grandi da risultare inutili. È preferibile avere intervalli piccoli, con livelli di confidenza minori (a meno che il livello di confidenza non sia troppo basso).

È sbagliato affermare:

>‘Ho calcolato un intervallo di confidenza di livello $90\%$. L’intervallo è $[2, 5]$, quindi il parametro $\theta$ appartiene a questo intervallo con probabilità $90\%$

Il parametro è un **numero costante**: *o appartiene o non appartiene* all’intervallo che abbiamo calcolato con un particolare campione.

Il livello di confidenza dell’intervallo indica che *$\theta$ appartiene al $90\%$ degli intervalli* che possiamo calcolare con campioni diversi.

Ovviamente per ‘campioni diversi’ intendiamo campioni costruiti con la **stessa regola di campionamento** e con la **stessa dimensione**.
## Costruzione di un Intervallo di Confidenza
Il metodo più semplice per costruire un **intervallo di confidenza** $[A,B]$ con livello di confidenza $(1 - \alpha)$ richiede uno stimatore $\hat{\theta}$:
* **Non distorto** ($E (\hat{\theta}) = \theta$)
* Con **distribuzione normale** ($N\ \{\theta, Var(\hat{\theta})\}$)

In questo caso costruiremo l'intervallo di confidenza a partire dallo stimatore **standardizzato** ($Z$): $$Z= \frac{\hat{\theta} - \theta}{SE(\hat{\theta})}$$ che è distribuito come una variabile casuale **normale standard** $N(0,1)$.
La **quantità $Z$** verrà in seguito chiamata **statistica $Z$**.

Una volta costruita la statistica $Z$ *dobbiamo trovare i quantili della distribuzione normale standard* che identificano un’area di ampiezza pari a $(1 - \alpha)$.

![[Pasted image 20240328091209.png]]

Il numero $z_{\frac{\alpha}{2}}$ è tale che $\mathbb{P}(Z > z_{\frac{\alpha}{2}}) = \frac{\alpha}{2}$, cioè il  quantile di posizione $(1 - \frac{\alpha}{2})$ della distribuzione normale standard.

Abbiamo che: $$\mathbb{P}\ \{-z_{\frac{\alpha}{2}} \leq \frac{\hat{\theta} - \theta}{SE(\hat{\theta})}\} \leq z_{\frac{\alpha}{2}} = 1 - \alpha$$
ovvero: $$\mathbb{P}\ \{\hat{\theta} - z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta}) \leq \theta \leq \hat{\theta} + z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta}) = 1 - \alpha$$
Quindi gli *estremi dell'intervallo di confidenza* sono: $$A = \hat{\theta} - z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta})$$ $$B = \hat{\theta} + z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta})$$
o in forma compatta: $$\hat{\theta} \pm z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta})$$
Si tratta di un *intervallo centrato* in $\hat{\theta}$ con **margine di errore** pari a $z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta})$.
## Riassunto
Passaggi per calcolare un intervallo di confidenza di livello $(1 - \alpha)$ utilizzando la statistica $Z$:
1. Trovare uno stimatore $\hat{\theta}$ non distorto di $\theta$.
2. Controllare che lo stimatore si distribuisca come una variabile normale.
3. Calcolare l’errore standard dello stimatore $SE(\hat{\theta})$.
4. Calcolare il quantile $z_{\frac{\alpha}{2}}$.
5. Calcolare gli estremi dell’intervallo $\hat{\theta} \pm z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta})$.
## Livelli di Confidenza Approssimati
Nelle precedenti lezioni abbiamo spesso ottenuto stimatori *asintoticamente non distorti e normali*:$$\hat{\theta} \overset{p}\to N\ \{\theta, Var(\hat{\theta})\}$$ al crescere della dimensione campionaria.

Se applichiamo l’approccio descritto nelle pagine precedenti ad *uno stimatore asintoticamente normale e asintoticamente non distorto*, allora l’intervallo $\hat{\theta} \pm z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta})$ avrà livello **approssimativamente** pari a $(1 - \alpha)$.
## Intervallo di confidenza per la media di una popolazione
Campione casuale semplice da popolazione con media $\mu$ e varianza $\sigma^2$ che per il momento assumiamo **nota**.

Consideriamo l’ovvio stimatore non distorto $\hat{\mu} = \overline{X}$.

Quando possiamo usare la statistica $Z$?
* Se $X_1, . . . , X_n$ sono **normali**, allora $\hat{\mu} = \overline{X}$ è **normale**.
* Se $X_1, . . . , X_n$ **non** sono **normali** ma $n$ è **grande**, allora $\hat{\mu} = \overline{X}$ è **approssimativamente normale**.

*Errore standard*: $$SE(\hat{\mu}) = \frac{\sigma}{\sqrt{n}}$$ *Intervallo di confidenza*: $$\overline{X} \pm z_{\frac{\alpha}{2}}\cdot \frac{\sigma}{\sqrt{n}}$$
## Quantili
Il **quantile** $z_{\frac{\alpha}{2}}$ necessario per il calcolo degli intervalli di confidenza si può ottenere con:
* la *tavola della distribuzione normale*.
* Un qualsiasi *software per l’analisi dei dati*.

In $R$ il quantile $z_{\frac{\alpha}{2}}$ si ottiene con la funzione `qnorm`.

Per esempio per $\alpha = 0.05$ dobbiamo digitare:

```R
qnorm(1 - 0.05 / 2)
```

**Esempio dal Baron**:

![[Pasted image 20240328093644.png]]

## Quando non possiamo usare la statistica $Z$
Abbiamo già detto che possiamo calcolare l’*intervallo di confidenza* per la media $\mu$ con **varianza $\sigma^2$ nota** usando la statistica $Z$ se:
* $X_1, . . . , X_n$ sono **normali**.
* $X_1, . . . , X_n$ **non** sono **normali** ma $n<4 è ‘**grande**’.

Non possiamo invece usare la statistica $Z$ quando $X_1, . . . , X_n$ **non** sono **normali** e $n$ è ‘**piccolo**’.

Campioni piccoli appaiono in problemi anche molto rilevanti.

Soluzioni:
* Metodi che dipendono dal problema specifico.
* Approssimazioni che funzionano anche per valori di $n<4 piccoli (‘*metodi asintotici di ordine superiore*’).

*Nota*: in questo corso non tratteremo questi problemi.
## Intervallo di confidenza per la differenza di due medie
Campioni casuali semplici da due popolazioni:
* $X_1, . . . , X_n$ con media $\mu_X$ e varianza nota $\sigma^2_X$.
* $Y_1, . . . , Y_m$ con media $\mu_Y$ e varianza nota $\sigma^2_Y$.

Vogliamo calcolare un intervallo di confidenza per: $$\theta = \mu_X - \mu_Y$$ Assunzioni:
* I due campioni sono **indipendenti**.
* Le osservazioni sono **normalmente distribuite** oppure le **numerosità** dei due campioni $n$ e $m$ sono ‘**grandi**’.

Uno *stimatore non distorto* di $\theta$ è: $$\hat{\theta} = \overline{X} - \overline{Y}$$
L'*errore standard* dello stimatore è: $$SE(\hat{\theta}) = \sqrt{Var(\hat{\theta})} $$ $$= \sqrt{Var(\overline{X} + Var(\overline{Y})}$$ $$= \sqrt{\frac{\sigma^2_X}{n}} + \frac{\sigma^2_Y}{m}$$
L'*intervallo di confidenza* è: $$\hat{\theta} \pm z_{\frac{\alpha}{2}}\cdot SE(\hat{\theta})$$ ovvero: $$(\overline{X} - \overline{Y}) + z_{\frac{\alpha}{2}} \cdot \sqrt{\frac{\sigma^2_X}{n}} + \frac{\sigma^2_Y}{m}$$ 
**Esempio dal Baron**:

![[Pasted image 20240328095042.png]]
## Dimensione Campionaria
Gli intervalli di confidenza che abbiamo incontrato hanno la forma simmetrica: $$stimatore \pm margine\ d’errore$$
Potremmo ora chiederci quanto deve essere grande il campione per garantire una data precisione al nostro stimatore.

Ovvero quanto deve valere $n$ affinché il margine di errore sia **inferiore ad un dato valore $\Delta$**.
Dobbiamo risolvere la diseguaglianza: $$margine\ d’errore \leq \Delta$$ rispetto alla **numerosità campionaria** $n$.

Nell'*intervallo di confidenza per la media* il margine d'errore è: $$z_{\frac{\alpha}{2}} \cdot \frac{\sigma}{\sqrt n}$$
Quindi dobbiamo risolvere la disuguaglianza: $$z_{\frac{\alpha}{2}} \cdot \frac{\sigma}{\sqrt n} \leq \Delta$$ ottenendo:$$n \geq (\frac{z_{\frac{\alpha}{2}} \cdot\sigma}{\Delta})^2$$
Siccome $n$ è un **valore intero**, allora la minima dimensione campionaria che assicura la precisione desiderata sarà il *più piccolo intero che soddisfa la diseguaglianza*.

**Esempio dal Baron**:

![[Pasted image 20240328095751.png]]
## Quando la deviazione standard è ignota
Nelle precedenti pagine abbiamo visto come calcolare un *intervallo di confidenza* per la media $\mu$ assumendo che $\sigma^2$ sia **noto**.

Questa assunzione può essere ragionevole in alcuni casi, per esempio:
* Quando abbiamo un’ampia informazione da studi precedenti.
* I dati sono misurazioni ottenute da strumenti con precisione nota.

Molto più spesso, però, $\sigma^2$ non è noto e quindi andrà stimato con i dati.

In questi casi si dice che:
* $\mu$ è il **parametro di interesse**.
* $\sigma^2$ è il **parametro di disturbo**.

Come precedentemente distingueremo fra tre possibili situazioni:
* Campioni di *grandi dimensioni* da *qualsiasi distribuzione*.
* Campioni di *qualsiasi dimensione* dalla *distribuzione normale*.
* Campioni di *piccola dimensione* da una *distribuzione non normale*.

*Nota*: come nel caso di $\sigma^2$ noto, vedremo come risolvere i primi due problemi, mentre non tratteremo il terzo che richiede soluzioni specifiche o tecniche statistiche più avanzate.
## Campioni di grandi dimensioni
Se il campione ha grandi dimensioni allora ci aspettiamo che lo stimatore dell’errore standard $\hat{SE}(\hat{\theta})$ sia ragionevolmente vicino al ‘vero’ errore standard.
Possiamo, allora, calcolare un intervallo di confidenza di livello approssimato $1 - \alpha$ con la statistica $Z$: $$\hat{\theta} \pm z_{\frac{\alpha}{2}} \cdot \hat{SE}(\hat{\theta})$$
Nel caso della *media di una popolazione* avremo: $$\hat{\mu} \pm z_{\frac{\alpha}{2}} \cdot \frac{\hat{\sigma}}{\sqrt n}$$ ovvero:
$$\overline X \pm z_{\frac{\alpha}{2}} \cdot \frac{S}{\sqrt n}$$
Nel caso della *differenza di due medie*: $$\hat{\mu}_x - \hat{\mu}_y \pm z_{\frac{\alpha}{2}} \cdot \sqrt{\frac{\hat{\sigma}^2_x}{n} + \frac{\hat{\sigma}^2_y}{m}}$$ ovvero: $$\overline X - \overline Y \pm z_{\frac{\alpha}{2}} \cdot \sqrt{\frac{S^2_x}{n} + \frac{S^2_y}{m}}$$
**Esempio dal Baron**:

![[Pasted image 20240328101040.png]]
## Intervalli di confidenza per le proporzioni
Una situazione in cui non conosciamo la deviazione standard è quando dobbiamo stimare una **proporzione campionaria**.

Supponiamo che siamo interessati alla **sottopopolazione** che possiede un certo **attributo $A$**.

Definiamo la *proporzione delle popolazione* con l’attributo $A$ come $$p = \mathbb P(possedere\ l’attributo\ A)$$ La corrispondente *proporzione campionaria* è $$\hat{p} = \frac {n_A}{n}$$ con $n_A =$ numero di unita con l’attributo $A$.

Il problema può essere riformulato con le variabili indicatrici: $$X_i = \begin{cases} 1, \ \ \ \ se\ l'unità\ i\ possiede\ l'attributo\ A \\ 0, \ \ \ \ se\ l'unità\ i\ non\ possiede\ l'attributo\ A \end{cases}$$
$X_i$ è una **variabile Bernulliana** con parametro $p$: $$E(X_i) = p\ \ e\ \ Var(X_i) = p(1 - p)$$
Lo stimatore $\hat{p}$ è la **media campionaria**: $$\hat{p} = \overline{X} = \frac{1}{n} \sum_{i = 1}^n X_i$$ con: $$E(\hat{p}) = p\ \ e\ \ Var(\hat{p}) = \frac{p(1 - p)}{n}$$
Lo stimatore $\hat{p}$ è quindi:
* **Non distorto**.
* **Asintoticamente normale**.

La *distribuzione di $\hat{p}$* è **approssivamente** pari a: $$N\ (p, \frac{p(1 - p)}{n}),\ per\ n\ sufficientemente\ grande$$
L'*errore standard di $\hat{p}$* stimato è: $$\sqrt{\frac{\hat{p}(1 - \hat{p})}{n}} = \sqrt{\frac{\overline X (1 - \overline X)}{n}}$$
L’*intervallo di confidenza* per $p$ con livello di confidenza approssimativamente pari a $1 - \alpha$ è: $$\hat{p} \pm z_{\frac{\alpha}{2}}\sqrt{\frac{\hat{p}(1 - \hat{p})}{n}}$$ ovvero: $$\overline{X} \pm z_{\frac{\alpha}{2}}\sqrt{\frac{\overline{X}(1 - \overline{X})}{n}}$$
## Intervalli di confidenza per la differenza di due proporzioni
Supponiamo di avere due popolazioni **indipendenti** di dimensioni $n_1$ e $n_2$.

Vogliamo valutare in quale delle due popolazioni un certo attributo sia più frequente.

Possiamo costruire un *intervallo di confidenza* per la differenza della proporzione di unita con l’attributo $$\theta = p_1 - p_2$$ La *stimatore* di $\theta$ è la differenza delle proporzioni campionarie $$\hat{\theta} = \hat p_1 - \hat p_2$$
L'*errore standard* di $\hat \theta$ è $$SE(\hat \theta) = \sqrt{\frac{p_1 (1 - p_1)}{n_1} + \frac{p_2(1 - p_2)}{n_2}}$$
L'*errore standard stimato è quindi*: $$\hat{SE}(\hat \theta) = \sqrt{\frac{\hat p_1 (1 - \hat p_1)}{n_1} + \frac{\hat p_2(1 - \hat p_2)}{n_2}}$$
L'*intervallo di confidenza* con livello di confidenza approssimativamente pari a $(1 - \alpha)$ è : $$\hat p_1 - \hat p_2 \pm z_{\frac{\alpha}{2}} \cdot \sqrt{\frac{\hat p_1 (1 - \hat p_1)}{n_1} + \frac{\hat p_2(1 - \hat p_2)}{n_2}}$$
**Esempio dal Baron**:

![[Pasted image 20240328103810.png]]
![[Pasted image 20240328103832.png]]

