## Idea di risoluzione
La challenge è stata completata mediante la creazione di uno script. In particolare sono stati sfruttati gli OTP pubblicati: 
```sh
OTP1 = 754104, generated on 8 April 2020 at 21:45  
OTP2 = 353471, generated on 8 April 2020 at 21:46  
OTP3 = 084633, generated on 8 April 2020 at 21:47
```

per risalire al PIN originale.

L'idea di risoluzione prevede sostanzialmente la costruzione di un *bruteforce* così definito:
* Genera tutti i possibili PIN a $8$ cifre (ovvero $100$ milioni di PIN).
* Genera un OTP per ogni PIN, rispetto a ciascuno dei `timestamp` pubblicati.
* Salva solamente i PIN che generano gli OTP pubblicati rispetto al relativo `timestamp`. Si noti che, grazie all'operazione di modulo, più PIN diversi possono generare lo stesso OTP. Dall'esecuzione dello script si è notato che all'incirca $100$ PIN generano lo stesso OTP per un determinato `timestamp`. Ciò significa che la probabilità che un PIN generi l'OTP richiesto è di $\frac{1}{1000000}$.
* A questo punto è sufficiente identificare l'unico PIN dal cui *hash* è stato possibile generare tutti e tre gli OTP.
## Spiegazione dello script
Di seguito viene riportato lo script utilizzato:
```python

import hashlib
import numpy as np
from functools import reduce



def generate_pins():
    pins = []
    for pin in range (0, 100000000):
        pins.append(f'{pin:08d}')
    return pins


def find_possible_pins(otp,timestamp, pins):
    results = []
    
    for pin in pins:
        h = hashlib.sha256((pin+timestamp).encode()).digest()
        generated_otp = ''
        for i in range(6):
            digit = h[i] % 10
            generated_otp += str(digit)
        if (generated_otp == otp):
            results.append(pin)
    #print(results)
    return results

def main():
    
    pins = generate_pins()
	
    otp1 = '754104'
    otp2 = '353471'
    otp3 = '084633'
    
    timestamp1 = '{}-{}-{}-{}:{}'.format(2020,4,8,21,45)
    timestamp2 = '{}-{}-{}-{}:{}'.format(2020,4,8,21,46)
    timestamp3 = '{}-{}-{}-{}:{}'.format(2020,4,8,21,47)
    
    possible_pins1 = find_possible_pins(otp1,timestamp1,pins)
    possible_pins2 = find_possible_pins(otp2,timestamp2,pins)
    possible_pins3 = find_possible_pins(otp3,timestamp3,pins)
    
    res = reduce(np.intersect1d, (possible_pins1,possible_pins2,possible_pins3))
    
    print(res)
    

if __name__ == '__main__':
    main()

```

*Nota*: questa versione dello script non è la migliore in quanto a sfruttamento della memoria e della CPU, tuttavia è stata riportata poiché considerata di più facile lettura e comprensione. 

Ora viene riportata una spiegazione passo per passo del funzionamento dello script:
* La funzione `generate_pins()` crea semplicemente una lista con tutti i possibili PIN di $8$ cifre decimali.
* La funzione `find_possible_pins(otp,timestamp, pins)` è molto simile a quella utilizzata dal programma originale per creare l'OTP. Essa genera l'hash di ciascun PIN trovato al punto precedente rispetto al `timestamp` inserito in *input*. Dall'hash si procede alla generazione di ciascun OTP. Qualora l'OTP trovato fosse uguale a quello originale (inserito in input), il PIN che lo ha generato sarà inserito in una lista di *PIN candidati*. Tale lista verrà ritornata dalla funzione.
* Dopo aver ottenuto le $3$ liste, relative a ciascuna coppia *OTP-timestamp*, sarà sufficiente trovare l'unico PIN presente in tutte e tre le liste (approssimativamente unico, poiché la probabilità che un PIN generi tutti e tre gli OTP è di $\frac{1}{1000000^3}$). Per fare ciò si è usata la funzione `intersect1d` di `NumPy`, assieme alla funzione `reduce` di `functools`, che permette di applicare la funzione passata come primo argomento a tutte le liste passate come argomenti successivi.
* Viene infine stampato il PIN ottenuto.

![[Pasted image 20241109144207.png]]
Dall'immagine qui riportata si evince che:
* Il PIN è stato identificato univocamente come `41131337`.
* Nonostante tale bruteforce sembri particolarmente costoso, esso può essere eseguito da un semplice laptop in meno di $10$ minuti. Ciò significa che una versione più ottimizzata dello script (per esempio con un approccio multi-threading) o un computer più potente, possono ottenere il PIN in maniera ancora più veloce. A livello di sicurezza sarebbe necessario rendere tale bruteforce computazionalmente impossibile per renderlo inutilizzabile.