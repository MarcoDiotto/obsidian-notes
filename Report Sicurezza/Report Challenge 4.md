Inizio la challenge scaricando il file di backup nel modo seguente:
![[Pasted image 20241204160317.png]]

Dopo aver scaricato il file di backup, posso aprirlo con un IDE.
Dall'analisi del file di backup si nota un certo utilizzo di prepared statements, che vanificano la possibilità di utilizzare SQL injection. C'è tuttavia un unica porzione di codice (quella relativa alla visualizzazione delle informazioni dell' utente) in cui è presente una query non sicura:
![[Pasted image 20241204160840.png]]
La query in questione è: 
```php
$query = "SELECT * FROM utenti WHERE username = '" . $_SESSION['username'] . "'";
```
Da tale query otteniamo tre informazioni:
* Il campo in cui faremo injection è `username`, ovvero l'unico che viene passato in input.
* Se la query passata è sbagliata verrà mostrato l'errore corrispondente.
* Non possiamo fare injection "direttamente" su tale query (perché non abbiamo form o altri mezzi per accedervi direttamente), tuttavia essa rende non sicure anche le altre query. Tale comportamento viene chiarificato da un esempio:
	* Creiamo un nuovo utente che abbia come `username` `' OR username = 'admin' #` e una password qualsiasi
	* Le query di registrazione e di login saranno sicure poiché vengono utilizzati i prepared statements.
	* Tuttavia quando si cercherà di accedere alla pagina di informazioni per l'utente `' OR username = 'admin' #`, il codice SQL presente nello `username` non verrà sanitizzato e verrà eseguita la query `SELECT * FROM utenti WHERE username = '' OR username = 'admin' #`.

Il risultato di tale query è il seguente:
![[Pasted image 20241204162901.png]]

Siamo vicini al risultato, tuttavia la password non viene mostrata.
A questo punto dovrei provare a far stampare la password nelle prime $5$ righe della tabella. Inizio con delle query necessarie a capire il numero di colonne presenti nella tabella `utenti`.
Inizio con una query che raggruppa tutti gli elementi in base alla sesta colonna, se essa esiste non avrò in output un errore:
L'utente della prima query sarà `' GROUP BY 6 #` e l'output ottenuto il seguente:
  ![[Pasted image 20241204163756.png]]
  Non ci sono errori, infatti la tabella ha sei colonne. Continuo così fino all'ottenimento di un errore.
  L'utente `' GROUP BY 8` # genera un errore, pertanto capisco che la tabella ha sette colonne.
  ![[Pasted image 20241204164634.png]]

A questo punto quindi è sufficiente utilizzare il nome utente `' UNION ALL SELECT 1,password,1,1,1,1,1 FROM utenti WHERE username = 'admin' #` per ottenere la password in seconda posizione.
![[Pasted image 20241204165249.png]]
*Nota*: ciò è possibile perché `Name` e `Password` hanno entrambi lo stesso tipo. Tuttavia, inserendo `password` in seconda posizione non siamo automaticamente sicuri che essa sarà stampata in seconda posizione nella tabella. Dovremmo provare una query con password in ogni posizione per essere sicuri che essa venga effettivamente stampata.

A questo punto è sufficiente effettuare il login e completare la challenge.
![[Pasted image 20241204165828.png]]