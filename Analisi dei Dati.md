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

