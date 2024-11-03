La challenge è stata completata in due fasi. Inizialmente si è analizzato il codice C e si è identificata la vulnerabilità. Successivamente si è capito come sfruttare tale vulnerabilità ed è stato definito uno script in python per ottenere la password nascosta.
## Identificazione della vulnerabilità
La vulnerabilità trovata è un semplice `off by one` dovuto ad una errata allocazione dello spazio per un buffer.
```c
#define PWDLEN 16 // max PWD len without NULL terminator

char *buffer1; // buffer for stored password
char buffer2[PWDLEN]; // buffer of size PWDLEN for typed pwd
```

In tale porzione di codice notiamo che vengono creati due buffer. Il contenuto del primo verrà allocato dinamicamente nell'*heap*, mentre il contenuto del secondo sarà inserito nello *stack* e avrà dimensione 16.

```c
for (i=0;i<=PWDLEN && (c=getchar())!=EOF && c!='\n'; i++) {
	buffer2[i]=c;
}
```

Il `for` sopra riportato contiene la vulnerabilità: vengono ottenuti in input ben $17$ caratteri, mentre la password dovrebbe essere lunga esattamente $15$ caratteri. Il codice di conseguenza risulta avere i seguenti problemi:
* L'attaccante può sovrascrivere il carattere di terminazione (in posizione $15$ contando da $0$).
* L'attaccante può sovrascrivere il byte meno significativo nella posizione dello stack adiacente a quella del buffer (in posizione $16$ contando da $0$).

*Nota*: La versione corretta del `for` dovrebbe avere come clausola `i < PWDLEN - 1`.
## Utilizzo della vulnerabilità
A questo punto si è fatto uso del del codice pubblico per scoprire che i due buffer si trovano in posizioni adiacenti nello stack (a $16$ byte di distanza l'uno dall'altro, ovvero la dimensione di `buffer2`):
![[Pasted image 20241103151734.png]]

Si noti inoltre che quando si utilizza una password di dimensione inferiore a quella richiesta si riceve un messaggio di errore che spiega quale dovrebbe essere la dimensione della password.

Iniziamo a sfruttare la vulnerabilità, scriviamo una password di $16$ caratteri, così sovrascriviamo solamente il carattere di terminazione:
![[Pasted image 20241103152012.png]]
Notiamo che il contenuto di `buffer2` è cambiato. La `printf` sta provando a stampare ciò che si trova oltre al carattere di terminazione sovrascritto dal carattere `6`, ovvero l'inizio dell'indirizzo dell'*heap* contenuto in `buffer1`.

A questo punto scriviamo una password di $17$ caratteri, inseriamo nell'ultima posizione un valore casuale, per esempio lo $0$:
![[Pasted image 20241103152357.png]]

Notiamo subito svariati problemi:
* Abbiamo sovrascritto l'ultimo byte dell'indirizzo dell'*heap* contenuto in `buffer1`, ci siamo cioè spostati nell'*heap*.
* A seguito di tale spostamento, in `buffer1` non è più contenuta alcuna password, la dimensione della password diventa $0$.
* L'esecuzione abortisce, poiché non riesce a fare la `free()` a `buffer1`, l'area di memoria a cui esso punta non è più valida, tuttavia il programma è riuscito ad eseguire quasi fino alla fine, possiamo pertanto sfruttare questa vulnerabilità.

Notiamo ora che ad ogni esecuzione l'indirizzo dell'*heap* contenuto in `buffer1` termina sempre con il byte `60`. Proviamo a spostarci avanti di un byte, andando al byte in posizione $61$:

![[Pasted image 20241103153124.png]]

La dimensione della password si è ridotta di esattamente una posizione e `buffer1` si è spostato avanti di una posizione, andando a perdere esattamente il primo carattere della stringa in esso salvata.

Continuando con tale metodo fino alla fine possiamo autenticarci per la stringa di lunghezza nulla:
![[Pasted image 20241103153710.png]]

A questo punto capiamo come sfruttare la vulnerabilità per ottenere la password completa. Possiamo fare un semplice bruteforce con le seguenti caratteristiche:
* Parte dall'ultima posizione per identificare un carattere della password alla volta, e lo inserisce nella stringa in input al programma, fino a completarla correttamente.
* Ad ogni esecuzione prova al più $128$ byte diversi (quelli contenuti nella *tabella ASCII*) per identificare il carattere corrispondente alla posizione che stiamo valutando.
* Modifica la stringa in input al programma di conseguenza.

In particolare la stringa che ad ogni esecuzione diamo in input al programma è composta come segue:
* La prima posizione è quella su cui si esegue il bruteforce, ad ogni esecuzione il byte in essa contenuto cambia, fino a che non si ottiene il carattere corretto.
* Nelle successive $n$ posizioni si trovano i caratteri della stringa già identificati nelle iterazioni relative alle posizioni precedenti.
* Nelle successive $15-n$ posizioni si trova un *pad* numerico, necessario per "bucare" l'area di memoria di `buffer2`. Ogni volta che un nuovo carattere viene identificato, la sua dimensione diminuirà di $1$
* Nell'ultima posizione si trova il byte $b$ relativo alla posizione del carattere  della password che si vuole identificare. Ogni volta che tale carattere sarà trovato, tale byte si ridurrà di $1$ ($b = b - 1$).

A questo punto è semplice definite uno script in python per l'identificazione della password:
```python
import subprocess
import struct

  

def bruteforce():
	buff = b'\x00'
	pad = b'\x001234567890123'
	
	for i in range (14, -1, -1):
		for byte in range(0, 128):
			if byte == 10 or byte == 13:
				continue
			p = subprocess.Popen(['./pwdChallenge'],
			stdout=subprocess.PIPE, stderr=subprocess.PIPE, 
			stdin=subprocess.PIPE)
	
			output = p.communicate(input=struct.pack('B', 
				     byte)+buff+pad+struct.pack('B', 96 + i))
			
			if 'Authenticated!' in output[0].decode():
				buff = struct.pack('B', byte) + buff
				pad = pad[:-1]
				break
	return buff

  

def main():

	p = subprocess.Popen(['./pwdChallenge'],
		stdout=subprocess.PIPE, stderr=subprocess.PIPE, 
		stdin=subprocess.PIPE)
	
	pwd = bruteforce()
	output = p.communicate(pwd)
	
	print("Password: ", pwd.decode())
	print("Output: ", output[0].decode())

  
if __name__ == '__main__':
	main()
```

L'output di tale script è:
![[Pasted image 20241103160023.png]]
In tal modo la password `0ffby0n3r3v3ng3` è stata ottenuta.

*Nota*: tale bruteforce è estremamente più efficiente di un generico bruteforce che ricerca tutte le possibili password di $15$ caratteri. Quest'ultimo infatti dovrebbe provare ben $128^{15}$ combinazioni di password, mentre quello sopra riportato ne prova solamente $128*15$. Entrambi i bruteforce sarebbero inoltre più efficienti se si avesse la sicurezza che la password ricercata contiene solamente caratteri alfanumerici.