La challenge è stata eseguita principalmente attraverso l'esecuzione dinamica, inizialmente estraendo la password criptata dal programma e successivamente verificando come  l'eseguibile effettua la criptazione dell'input.
## Estrazione della password criptata
Dopo aver avviato **gdb** e aver fatto eseguire il programma con un `break` sul `main`, ho ottenuto il codice *assembly* del `main` grazie al comando `disass main`. A questo punto noto che viene caricato il contenuto di un'area di memoria nel registro `rdi` appena prima della chiamata a `strcmp`(mentre la password ottenuta in input, dopo essere stata criptata verrà spostata dal registro `rax` al registro `rsi`):

![[Pasted image 20241011143449.png]]

A questo punto è sufficiente ottenere  la stringa presente  nell'indirizzo `rdi` grazie al comando `x/s 0x555555601070 `:
![[Pasted image 20241011143543.png]]
Scopro in tal modo che la password criptata corrisponde alla stringa **vF34j4q6**.
A questo punto non devo fare altro che scoprire come viene criptata la password inserita dall'utente ed applicare tale criptazione in maniera inversa alla stringa trovata.
## Verifica del sistema di criptazione
La ricerca del sistema di criptazione è la parte della challenge che più richiede l'utilizzo dell'analisi dinamica. Pertanto in questa fase ho utilizzato **gdb**, inserendo in input al programma una password casuale di 8 caratteri, per esempio `aaaaaaaa`:

```
gdb password
(gdb) source ../GDB/peda/peda.py
gdb-peda$ break main
gdb-peda$ run aaaaaaaa
```

La prima cosa che noto è che la stringa ottenuta in input viene inserita all'interno del registro `rax`:
![[Pasted image 20241011144744.png]]
Dopo una prima chiamata a `strlen` il registro `rax` assume il valore `0x8`, è la lunghezza della stringa in input.
Noto a questo punto che anche la stringa criptata contenente la password originale viene caricata e che la sua lunghezza viene salvata nel registro `rbx`.
Una successiva istruzione `cmp` confronterà la lunghezza delle due stringhe e qualora fossero diverse il programma terminerà con un **exit code 2**.

Dopo una serie di altre operazioni entriamo nel *ciclo while di criptazione*. Il valore `0x0` viene inserito nello **stack**, precisamente nella posizione `rbp-0x4c`. Tale valore verrà successivamente confrontato con `0x7`, per verificare che il contatore relativo al carattere della stringa da criptare sia inferiore alla lunghezza totale di essa. In caso affermativo (cioè se è minore di `0x7`) si ritorna all'inizio del ciclo:
![[Pasted image 20241011145838.png]]

Una volta ricominciato il ciclo, in `rax` torna ad essere salvata la stringa in input mentre in `rdx` l'attuale valore del contatore. In seguito `rdx` verrà sommato a `rax`, in tal modo si scorre la stringa e di conseguenza si ottiene il carattere che si desidera criptare. Grazie all'istruzione `movzx  eax,BYTE PTR [rax]` tale carattere viene salvato in `eax` (i primi 32 bit di `rax`). Successivamente tale valore viene spostato in momentaneamente in `rdx` (mentre in `rax` viene reinserito il contatore) e viene eseguita la seguente istruzione:
```
mov    eax,DWORD PTR [rbp+rax*4-0x40]
```

La particolarità di tale istruzione è che ad ogni esecuzione del ciclo caricherà in `eax` elementi consecutivi (nel nostro caso distanti fra loro 4 byte). Ciò è chiarito dall'utilizzo di `rax` nell'istruzione. Infatti alla prima esecuzione esso vale $0$ e in `eax` verrà caricato il valore contenuto in `rbp-0x40`, alla successiva iterazione varrà $1$, pertanto accederemo in memoria ad una posizione distante $4$ byte da `rbp-0x40` ecc.

Nel nostro caso (in cui appunto `rax` vale $0$) carichiamo in `eax` il valore `0xf`. Successivamente avviene l'istruzione:
```
lea    ecx,[rdx+rax*1]
```

Che sostanzialmente salva in  `ecx` il valore contenuto in `rdx`, in questo caso la prima `a`, traslato però (secondo la codifica ASCII) di $n$ posizioni, dove $n$ è il valore contenuto in `rax`, nel nostro caso $15$. In `ecx` otteniamo quindi il valore `p`.
La situazione al momento è la seguente:
![[Pasted image 20241011151602.png]]

Successivamente in `rax` viene reinserita la stringa in input col primo carattere criptato e il contatore viene aumentato di $1$:
![[Pasted image 20241011151742.png]]
![[Pasted image 20241011151807.png]]
A questo punto la criptazione continua  per gli altri valori fino alla fine del ciclo.
## Conclusione
Noto successivamente che i valori di criptazione sono presenti nell'*assembly* del programma all'inizio del `main`:
![[Pasted image 20241011152025.png]]
Noto in particolare che il primo valore è salvato in `rbp-0x40`, la posizione da cui il programma ha caricato `0xf` prima, e che il valore salvato è proprio `0xf`.
Inoltre tutti gli altri elementi sono salvati in una posizione distante 4 byte dal precedente: sono tutti i **valori di criptazione** della password in input.

A questo punto è sufficiente sottrarre in ordine tali valori al rispettivo carattere della *password criptata*, in modo da ottenerne la versione *non-offuscata*, ovvero `g00dj0b!`.
![[Pasted image 20241011153103.png]]

*Nota*: Fra tali valori il più interessante è `0xffffffd0`, esso è salvato in complemento a due, e pertanto in fase di decriptazione dovrà essere sommato in valore assoluto al carattere criptato corrispondente e non sottratto.