[Link del Corso](https://secgroup.dais.unive.it/teaching/laboratorio-sistemi-operativi/)
# Processi
___
## Sistema Operativo:
* **Gestore** delle risorse
* **Competizione** fra processi(*racing*)
* **Astrazione** $\rightarrow$ vediamo solo le performance
## Cooperazione fra Processi
* Diversi compiti $\to$ **Modularità**
* **Parallelismo** $\to$ più risorse fanno la stessa cosa per aumentare l'efficienza
* **Condivisione** di informazioni
* **Multitasking**
* **Replicazione** $\to$ per esempio un *server* che fa una `fork` per servire più *client*
## Modelli di Comunicazione
* **Message Passing**:

```mermaid
flowchart LR
	A(P1) -- M1 --> D(P2)
	D -- M2 --> B(P3)
	C(P4) -- M3 --> D
```

* **Memoria condivisa**:


```mermaid
flowchart LR
	A((MEMORIA)) --> B(P1)
	A --> C(P2)
	A --> D(P3)
	A --> E(P4)
```

### Nominazione Diretta

```c
send(m)
receive(&m)
send(P,m)
receive(Q,&m)
receive(&Q,&m)
```

```mermaid
flowchart LR
	Q -- M --> P
```
```mermaid
flowchart LR
	? --> P
	? --> P
	? --> P
```

Svincolo chi scrive e chi legge utilizzando le **porte** o **mailbox**

```mermaid
flowchart LR
	A[[A]] --> B(P3)
	A --> C(P4)
	D(P1) --> A
	E(P2) --> A
```
* **Send sincrona**: attende finchè non viene eseguita la receive
* **Send asincrona**: non attende $\to$ *messaggio "bufferizzato"*. Se il buffer è pieno si passa alla *send sincrona* o si genera un *errore*

* **Receive sincrona**: bloccante
* **Receive asincrona**: periodicamente si controlla se ci sono messaggi