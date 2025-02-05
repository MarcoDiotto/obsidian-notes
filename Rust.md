___
# Introduzione
## Ecosistema
* `rustc` $\to$ compilatore di Rust.
* `cargo` $\to$ dependency manager e build tool, è simile a `pip` per python ma con ulteriori funzionalità.
	* `cargo new [nome_progetto]` crea un nuovo progetto.
	* `cargo run` esegue il progetto
	* `cargo check` controlla presenza di errori.
	* `cargo build` compila senza runnare.
	* `cargo build --release` produce una release build.
	* Per aggiungere dipendenze è sufficiente modificare `Cargo.toml`.
* `rustup` $\to$ toolchain installer e updater di rust. Aggiorna i componenti sopra e scarica la documentazione per la standard library.
## Caratteristiche di Rust
* **Staticamente compilato** come C++.
* Ampio supporto per piattaforme ed architetture.
* Usato per svarianti dispositivi.
## Benefici di Rust
* Compile time memory safety (no double free, use-after-free, variabili non inizializzate, ...).
* No undefined runtime behavior(bound checking per array, gestione di integer overflow).
* Modern language features (Enums, generics, ...)
# Hello World!
```rust
fn main() {
	println!("Hello 🌍!");
}
```

* Funzioni introdotte da `fn.`
* Uso di parentesi graffe come in C e C++.
* `main` come entry point del programma.
* Stringhe UTF-8 con caratteri unicode.
* presenza di **hygienic macros** (si riconoscono dal `!`). Le macro igieniche prevengono i conflitti fra nomi utilizzati all'interno del contesto delle macro e fuori da esso, rendendo il codice più sicuro ed affidabile. Da notare che `println!()` è una macro e non una funzione. Questo perché in Rust una funzione ha un numero predeterminato (e controllato a tempo di compilazione) di argomenti, mentre quelli di una macro possono cambiare dinamicamente.
## Variabili
Rust implementa la **type safety** tramite il typing statico.
Si utilizza `let` per fare i **binding**.

```rust
fn main() {
    let x: i32 = 10;
    println!("x: {x}");
    // x = 20;
    // println!("x: {x}");
}
```

Il codice commentato non funziona poiché le variabili inizializzate con `let` sono **immutabili**.
## Valori
Di seguito si riportano alcuni tipi **buit-int**.

|                        | **Tipi**                                                                      | **Esempi**                     |
| ---------------------- | ----------------------------------------------------------------------------- | ------------------------------ |
| Signed Integers        | `i8`, `i16`, `i32`, `i64`, `i128`, `isize`, `i8`, `i16`, `i32`, `i64`, `i128` | `-10`, `0`, `1_000`, `123_i64` |
| Unsigned Integers      | `u8`, `u16`, `u32`, `u64`, `u128`, `usize`                                    | `0`, `123`, `10_u16`           |
| Floating point numbers | `f32`, `f64`                                                                  | `3.14`, `-10.0e20`, `2_f32`    |
| Unicode values         | `char`                                                                        | `'a'`, `'α'`, `'∞'`            |
| Booleans               | `bool`                                                                        | `true`, `false`                |
Dove:
* in `iN`,`uN`,`fN`, `N` indica la dimensione in bit.
* `isize` e `usize` indicano la dimensione di un pointer.
* i `char` sono lunghi 32 bit.
* i `bool` sono lunghi 8 bit.

**Esempio**:
```rust
fn interproduct(a: i32, b: i32, c: i32) -> i32 {
    return a * b + b * c + c * a;
}

fn main() {
    println!("result: {}", interproduct(120, 100, 248));
}
```

```sh
result: 66560
```
## Type Inference

Quando si introduce una variabile con `let`, Rust controllerà *come la variabile viene usata* per determinarne il tipo:

```rust
fn takes_u32(x: u32) {
    println!("u32: {x}");
}

fn takes_i8(y: i8) {
    println!("i8: {y}");
}

fn main() {
    let x = 10;
    let y = 20;

    takes_u32(x);
    takes_i8(y);
    // takes_u32(y);
}
```

```sh
u32: 10  
i8: 20
```

Il codice commentato darebbe un errore, in quanto la **type inference** di Rust ci dice che `y` ha tipo `i8` e pertanto la chiamata a `takes_u32(y)` necessiterebbe di un cast implicito, che non è permesso in quanto le variabili sono immutabili.

**Esempio**: Numeri di Fibonacci

```rust
fn fib(n: u32) -> u32 {
    if n < 2 {
        // The base case.
        return n;
    } else {
        // The recursive case.
        return fib(n-1) + fib(n-2);
    }
}

fn main() {
    let n =20;
    println!("fib({n}) = {}", fib(n));
}
```

```sh
fib(20) = 6765
```

Per `n` troppo grande (n che produce un risultato $> 2^{32}$) la funzione andrà in **panic**.
# Control Flow
## `if` Expressions

Gli `if` sono uguali a quelli di ogni altro linguaggio di programmazione.
```rust
fn main() {
    let x = 10;
    if x == 0 {
        println!("zero!");
    } else if x < 100 {
        println!("biggish");
    } else {
        println!("huge");
    }
}
```

```sh
biggish
```

In aggiunta si possono usare gli `if` come **espressioni** (cioè frammenti di codice che producono un valore):
```rust
fn main() {
    let x = 10;
    let size = if x < 20 { "small" } else { "large" };
    println!("number size: {}", size);
}
```

```sh
number size: small
```
## `match` Expressions 
`match` è l'equivalente di `case...when`, viene utilizzato per confrontare un valore con diverse opzioni.
```rust
fn main() {
    let val = 1;
    match val {
        1 => println!("one"),
        10 => println!("ten"),
        100 => println!("one hundred"),
        _ => {
            println!("something else");
        }
    }
}
```

```sh
one
```

Come `if`, anche `match` può ritornare un valore.

```rust
fn main() {
    let flag = true;
    let val = match flag {
        true => 1,
        false => 0,
    };
    println!("The value of {flag} is {val}");
}
```

```sh
The value of true is 1
```
## Loops
I loop in Rust si fanno con le keyword `while`, `loop` e `for`.
### `while`
I `while` di Rust corrispondono a quelli degli altri linguaggi di programmazione:

```rust
fn main() {
    let mut x = 200;
    while x >= 10 {
        x = x / 2;
    }
    println!("Final x: {x}");
}
```

```sh
Final x: 6
```

*Nota*: `let mut x` sta ad indicare che `x` è una variabile **mutabile**, se non fosse così questo codice produrrebbe un errore.
### `for`
Come il `while`, anche il `for` corrisponde a quello degli altri linguaggi di programmazione.
```rust
fn main() {
    for x in 1..5 {
        println!("x: {x}");
    }

    for elem in [1, 2, 3, 4, 5] {
        println!("elem: {elem}");
    }
}
```

```sh
x: 1  
x: 2  
x: 3  
x: 4  
elem: 1  
elem: 2  
elem: 3  
elem: 4  
elem: 5
```
### `loop`

I `loop` ciclano all'infinito, o finché non incontrano un `break`.

```rust
fn main() {
    let mut i = 0;
    loop {
        i += 1;
        println!("{i}");
        if i > 5 {
            break;
        }
    }
}
```

```sh
1  
2  
3  
4  
5  
6
```

## `break` e `continue`

* `break` viene usato per uscire subito da qualsiasi tipo di loop.
* `continue` viene usato per procedere subito all'iterazione successiva.

```rust
fn main() {
    let mut i = 0;
    loop {
        i += 1;
        if i > 5 {
            break;
        }
        if i % 2 == 0 {
            continue;
        }
        println!("{}", i);
    }
}
```

```sh
1
3
5
```
## Labels
Sia `continue` che `break` possono avere un argomento **label** opzionale, che è usato per uscire da loop annidati.

Nell'esempio sotto riportato, la label `'outer` viene usata per uscire dal `for` esterno.
```rust
fn main() {
    let s = [[5, 6, 7], [8, 9, 10], [21, 15, 32]];
    let mut elements_searched = 0;
    let target_value = 10;
    'outer: for i in 0..=2 {
        for j in 0..=2 {
            elements_searched += 1;
            if s[i][j] == target_value {
                break 'outer;
            }
        }
    }
    print!("elements searched: {elements_searched}");
}
```

```sh
elements searched: 6
```
## Blocks and Scopes
### Blocks
In Rust, un **blocco** contiene una sequenza di espressioni, chiuse fra le parentesi graffe `{}`. Ogni blocco ha un valore e un tipo, che è quello *dell'ultima espressione del blocco*.

```rust
fn main() {
    let z = 13;
    let x = {
        let y = 10;
        println!("y: {y}");
        z - y
    };
    println!("x: {x}");
}
```

```sh
y: 10  
x: 3
```

*Nota*: se l'ultima espressione termina con `;`, allora il tipo e e il valore del blocco sono `()`.
### Scopes and Shadowing
Lo **scope** di una variabile è *limitato al suo blocco di appartenenza*.
Le variabili degli scope più esterni e quelle dello stesso scope sono soggette a shadowing.

```rust
fn main() {
    let a = 10;
    println!("before: {a}");
    {
        let a = "hello";
        println!("inner scope: {a}");

        let a = true;
        println!("shadowed in inner scope: {a}");
    }

    println!("after: {a}");
}
```

```sh
before: 10  
inner scope: hello  
shadowed in inner scope: true  
after: 10
```
## Funzioni
```rust
fn gcd(a: u32, b: u32) -> u32 {
    if b > 0 {
        gcd(b, a % b)
    } else {
        a
    }
}

fn main() {
    println!("gcd: {}", gcd(143, 52));
}
```

```sh
gcd: 13
```

Le funzioni di Rust sono simili a quelle di C++, ma con alcune differenze:

* La dichiarazione di una funzione può includere un tipo di ritorno specificato dopo una freccia `->`. La funzione può anche non richiedere un `return` esplicito se l'ultimo valore in un blocco è il valore di ritorno.

```rust
fn somma(a: i32, b: i32) -> i32 {
    a + b // L'ultimo valore è automaticamente il ritorno
}
```

* I parametri di una funzione sono di default immutabili. Per forzare la mutabilità dei parametri bisogna usare la keyword `mut`.
* Una funzione senza tipo di ritorno esplicito ha **return type** `()`, ovvero lo **unit type**.
* Concetto di **ownership** e **borrowing**: le funzioni possono prendere in prestito variabili tramite riferimenti o prenderne la **proprietà** (trasferendo l'ownership). Questo permette al linguaggio di prevenire errori di memoria come i **dangling pointer**.

```rust
fn usa_referenza(x: &i32) {
    println!("{}", x);  // La funzione prende in prestito x (immutabile)
}

fn prendi_possesso(x: String) {
    println!("{}", x); // La funzione prende la proprietà di x
}

```

* Come in C++ , le funzioni sono *valori di prima classe* il che significa che possono essere passate come argomenti o restituite da altre funzioni. Rust inoltre supporta **funzioni anonime** (**closures**), simili alle lambda di C++.

```rust
fn esegui_chiusura<F>(funzione: F)
where F: Fn() {
    funzione();
}

let chiusura = || println!("Ciao!");
esegui_chiusura(chiusura);

```

### Ownership
In **Rust**, ogni valore ha un'unica **proprietà**, ovvero è posseduto da una variabile. Quando una variabile possiede un valore, è responsabile per la **memoria** che quel valore occupa. Quando la variabile esce dal suo scope, la memoria viene **deallocata automaticamente**.
#### Regole dell'ownership
* **Ogni valore in Rust ha un proprietario**:  Una variabile è il "proprietario" di un valore.
* **Ogni valore può avere un solo proprietario alla volta**:  Se una variabile cede la proprietà di un valore, l'altra variabile diventa il nuovo proprietario. La variabile originale *non può più accedere* al valore.
* **Quando il proprietario esce dallo scope**, il valore viene deallocato.

```rust
fn main() {
    let s1 = String::from("Ciao");  // s1 è il proprietario di "Ciao"
    let s2 = s1;  // s1 cede la proprietà a s2

    // println!("{}", s1); // ERRORE: s1 non può essere utilizzato perché ha ceduto la proprietà
    println!("{}", s2); // OK: s2 è il nuovo proprietario
}

```
### Borrowing
Il **borrowing** consente di **prendere in prestito un valore** senza trasferirne la proprietà. Ci sono due tipi di prestito:
* **Immutabile borrowing** (`&T`):  
    Un riferimento immutabile permette di accedere al valore senza modificarlo. Più variabili possono prendere in prestito un valore in modo immutabile contemporaneamente.	 
* **Mutabile borrowing** (`&mut T`):  
    Un riferimento mutabile permette di modificare il valore, ma **è consentito solo un prestito mutabile per volta**. Non è possibile avere un riferimento mutabile e uno immutabile allo stesso valore nello stesso momento.

**Esempio di immutable borrowing**:
```rust
fn main() {
    let s1 = String::from("Ciao");
    let s2 = &s1;  // s2 prende in prestito immutabilmente s1

    println!("{}", s1); // OK: puoi leggere la stringa da s1
    println!("{}", s2); // OK: puoi leggere la stringa da s2

    // s1 e s2 non interferiscono tra loro
}

```

**Esempio di mutable borrowing**:

```rust
fn main() {
    let mut s1 = String::from("Ciao");
    let s2 = &mut s1;  // s2 prende in prestito mutabilmente s1

    s2.push_str(", mondo!"); // Modifica s1 attraverso s2

    println!("{}", s2); // OK: s2 è il riferimento mutabile
    println!("{}", s1); // ERRORE: non possiamo usare s1 mentre è mutabilmente preso in prestito
}

```
#### Regole del borrowing:
- È  possibile avere **uno o più prestiti immutabili** contemporaneamente, ma **solo un prestito mutabile** alla volta.
- Non è possibile avere **prestiti mutabili e immutabili** contemporaneamente sullo stesso valore.
### Closures
Vediamo nel dettaglio il codice per creare una **closure**:

```rust
fn esegui_chiusura<F>(funzione: F)
where F: Fn() {
    funzione();
}

let chiusura = || println!("Ciao!");
esegui_chiusura(chiusura);

```
#### Definizione della funzione `esegui_chiusura`
```rust
fn esegui_chiusura<F>(funzione: F) where F: Fn() {
    funzione(); 
}
```

- `fn esegui_chiusura<F>(funzione: F)`: Qui stiamo dichiarando una funzione chiamata `esegui_chiusura`. La funzione prende come parametro una variabile chiamata `funzione` di tipo generico `F`.
    - Il tipo `F` è un parametro generico, quindi `esegui_chiusura` può accettare **qualsiasi tipo** che soddisfi il vincolo indicato più avanti (cioè, il tipo `F` deve essere un tipo di chiusura che può essere invocato senza argomenti e che restituisce `()`).

- `where F: Fn()`: Questo vincolo (`where`) stabilisce che il tipo `F` deve essere una chiusura che implementa il tratto `Fn()`.
    - `Fn()` significa che `F` deve essere una chiusura che può essere chiamata senza argomenti. Se avesse avuto argomenti, sarebbe stato `Fn(A)` dove `A` sarebbe stato un tipo di argomento.
    - Quindi, questo vincolo garantisce che la funzione `esegui_chiusura` accetti solo chiusure che non richiedono argomenti e che restituiscono `()` (il tipo unità, cioè "niente").

- `funzione();`: Qui stiamo invocando la chiusura passata come parametro. La chiusura viene eseguita quando `funzione()` viene chiamato, in pratica, si esegue il codice dentro la chiusura.
#### Creazione di una chiusura
```rust
let chiusura = || println!("Ciao!");
```

- `let chiusura = || println!("Ciao!");`: Qui stiamo creando una chiusura (una funzione anonima) che non prende argomenti e stampa "Ciao!" quando viene eseguita.
    - Le chiusure in Rust possono essere definite utilizzando `||` (senza argomenti, in questo caso). Se la chiusura avesse avuto argomenti, li avremmo messi tra le barre, ad esempio `|x| println!("{}", x)`.
    - La chiusura `chiusura` è del tipo `Fn()`, cioè una funzione che non prende parametri e restituisce `()`.
#### Chiamata della funzione con la chiusura
```rust
esegui_chiusura(chiusura);
```

* `esegui_chiusura(chiusura)`: Qui stiamo chiamando la funzione `esegui_chiusura` passando come parametro la chiusura `chiusura`.
	- Poiché `chiusura` è una chiusura che non richiede argomenti e restituisce `()`, essa soddisfa il vincolo `Fn()` e può essere passata a `esegui_chiusura`.
	- Dentro la funzione `esegui_chiusura`, viene chiamata la chiusura `funzione()`, che stampa "Ciao!" sul terminale.
## Macros
Le macro vengono espanse in codice Rust durante la compilazione e possono accettare un numero variabile di argomenti. Sono caratterizzate dal simbolo `!` alla fine. La standard library di Rust include una serie di macro utili.

- `println!(format, ..)` stampa una riga sullo standard output, applicando il formato descritto in `std::fmt`.
- `format!(format, ..)` funziona esattamente come `println!`, ma restituisce il risultato come una stringa.
- `dbg!(expression)` registra il valore dell'espressione e lo restituisce.
- `todo!()` segna un pezzo di codice come non ancora implementato. Se eseguito, causerà un **panic**.
- `unreachable!()` segna un pezzo di codice come irraggiungibile. Se eseguito, causerà un **panic**.

**Esempio**:
```rust
fn factorial(n: u32) -> u32 {
    let mut product = 1;
    for i in 1..=n {
        product *= dbg!(i);
    }
    product
}

fn fizzbuzz(n: u32) -> u32 {
    todo!()
}

fn main() {
    let n = 4;
    println!("{n}! = {}", factorial(n));
}
```

```sh
[src/main.rs:5:20] i = 1  
[src/main.rs:5:20] i = 2  
[src/main.rs:5:20] i = 3  
[src/main.rs:5:20] i = 4
```

```sh
4! = 24
```
# Tuple ed Array
## Array
```rust
fn main() {
    let mut a: [i8; 10] = [42; 10];
    a[5] = 0;
    println!("a: {a:?}");
}
```

```sh
a: [42, 42, 42, 42, 42, 0, 42, 42, 42, 42]
```

Un array ha tipo `[T;N]` dove:
* `T` indica il **tipo** che ha ciascun elemento all'interno dell'array
* `N` indica il **numero** di elementi nell'array.

*Nota*: la dimensione dell'array è parte integrante del suo tipo.

La macro `println!` è leggermente diversa da prima, per stampare correttamente gli elementi dell'array, infatti, abbiamo bisogno di `{:?}` che fornisce l'**output di debug**. Gli elementi di un array possono essere stampati solo con l'output di debug.

*Nota*:  aggiungere `#` invoca un formato **pretty printing**, che stampa in maniera più carina. Di seguito si riporta l'output del codice di esempio con `println!("a: {a:#?}")`
```sh
a: [  
42,  
42,  
42,  
42,  
42,  
0,  
42,  
42,  
42,  
42,  
]
```
## Tuple
```rust
fn main() {
    let t: (i8, bool) = (7, true);
    println!("t.0: {}", t.0);
    println!("t.1: {}", t.1);
}
```

```sh
t.0: 7  
t.1: true
```

* Come gli array, le tuple hanno una lunghezza fissa.
* Le tuple raggruppano valori di tipi diversi in un tipo composto.
* È possibile accedere ai campi di una tupla utilizzando il punto seguito dall'indice del valore, ad esempio `t.0`, `t.1`.
* La tupla vuota `()` è chiamata **unit type** e rappresenta l'assenza di un valore di ritorno, simile a `void` in altri linguaggi.
## Array Iteration
```rust
fn main() {
    let primes = [2, 3, 5, 7, 11, 13, 17, 19];
    for prime in primes {
        for i in 2..prime {
            assert_ne!(prime % i, 0);
        }
    }
}
```

Questa porzione di codice scorre l'array `primes` per verificare che ogni numero in esso contenuto sia effettivamente primo.
In particolare:
- `assert_ne!(x, y)` verifica che `x` **sia diverso da** `y`.
- Se la condizione non è soddisfatta, il programma **termina con un panic**.
- Qui si verifica che `prime % i` **non sia uguale a zero**, cioè che `prime` **non sia divisibile** per `i`.
- Se `prime` fosse divisibile per qualche `i`, significherebbe che **non è un numero primo**, e il programma si interromperebbe.
## Pattern e Destructuring
In Rust è possibile usare il **pattern matching** per destrutturare un valore più grande (come una tupla) nelle sue parti costitutive:

```rust
fn check_order(tuple: (i32, i32, i32)) -> bool {
    let (left, middle, right) = tuple;
    left < middle && middle < right
}

fn main() {
    let tuple = (1, 5, 3);
    println!(
        "{tuple:?}: {}",
        if check_order(tuple) { "ordered" } else { "unordered" }
    );
}
```

```sh
(1, 5, 3): unordered
```

* Come gli **array**, anche le **tuple** possono essere stampate solo in **debug output**.
* I pattern utilizzati qui sono **irrefutable**, il che significa che il compilatore può verificare staticamente che il valore sulla destra dell'`=` abbia la stessa struttura del pattern.
* Un nome di variabile è un pattern irrefutable che corrisponde sempre a qualsiasi valore, ed è per questo che possiamo usare `let` anche per dichiarare una singola variabile.
* Rust supporta inoltre l'uso dei pattern nelle condizioni, permettendo di eseguire contemporaneamente confronti di uguaglianza e destrutturazione. Questa forma di pattern matching verrà discussa più dettagliatamente in seguito.
### Pattern irrefutable
In Rust, un **pattern irrefutabile** è un pattern che **deve sempre avere corrispondenza** con il valore su cui viene applicato. Il compilatore può garantire staticamente che l'assegnazione avrà sempre successo.
####  Esempio di pattern irrefutabile con `let`

```rust
let x = 5;
```

Qui `x` è un pattern irrefutabile perché **qualsiasi valore** può essere assegnato a una variabile.

```rust
let (a, b) = (10, 20);
```

Anche questo è irrefutabile, perché la tupla `(10, 20)` corrisponde perfettamente al pattern `(a, b)`. Il compilatore sa **a priori** che `a` e `b` riceveranno un valore.
 
 Un esempio **non valido** sarebbe:

```rust
let (a, b) = 10; // Errore: il valore a destra non è una tupla
```

Questo codice non compila perché `10` non può essere destrutturato in `(a, b)`. Il pattern non è irrefutable.

#### Pattern irrefutable vs. pattern refutable

Un **pattern refutabile** è un pattern che **potrebbe non corrispondere** a tutti i valori possibili, portando a un errore in fase di esecuzione se non gestito correttamente.

Esempio con `if let` (pattern refutabile):

```rust
if let Some(x) = Some(5) {
	println!("Il valore è {}", x);
}
```

Qui `Some(x)` è **refutabile**, perché se il valore fosse `None`, il pattern non corrisponderebbe.

Se provassimo ad usare un pattern refutabile con `let`, il compilatore darebbe errore:

```rust
let Some(x) = Some(5); //Errore! "Some(x)" è refutable
```

Rust non permette di usare **pattern refutable** in `let` perché l'assegnazione potrebbe fallire.
# References
##  Shared References
Una **reference** è un modo per accedere ad un altro valore senza dover ottenere la **proprietà** su quel valore ed è chiamata anche **borrowing**.
Le **shared references** sono *read-only* e i dati referenziati non possono cambiare.

```rust
fn main() {
    let a = 'A';
    let b = 'B';
    let mut r: &char = &a;
    println!("r: {}", *r);
    r = &b;
    println!("r: {}", *r);
}
```

```sh
r: A  
r: B
```

Come in C++ una shared reference ad un tipo `T` ha tipo `&T`, pertanto una reference viene fatta con l'operatore `&`. Al contrario l'operatore `*` viene utilizzato per deferenziare una reference.
*Nota*: a differenza di C++, una reference non è mai mutabile, anche se il valore che referenzia è `let mut`.
## Exclusive Reference
Le **exclusive reference** (o **mutable reference**) sono reference che permettono la modifica del valore che referenziano. Hanno tipo `&mut T`

```rust
fn main() {
    let mut point = (1, 2);
    let x_coord = &mut point.0;
    *x_coord = 20;
    println!("point: {point:?}");
}
```

```sh
point: (20, 2)
```

* Si noti la differenza tra `let mut x_coord: &i32` e `let x_coord: &mut i32`. Il primo rappresenta una shared reference che può essere associata a valori diversi, mentre il secondo rappresenta una exclusive reference a un valore mutabile.
* **Exclusive** significa che solo questa reference può essere utilizzata per accedere al valore. Non possono esistere contemporaneamente altre reference (né shared né exclusive) e il valore referenziato non può essere accessibile mentre il riferimento esclusivo esiste.

Esempio di più di una exclusive reference per uno stesso valore:

```rust
fn main() {
    let mut point = (1, 2);
    let x_coord = &mut point.0;
    let x_coord2 = &mut point.0;
    *x_coord = 20;
    *x_coord2 = 20;
    println!("point: {point:?}");
}
```

```sh
Compiling playground v0.0.1 (/playground)  
error[E0499]: cannot borrow `point.0` as mutable more than once at a time  
--> src/main.rs:5:20  
|  
4 | let x_coord = &mut point.0;  
| ------------ first mutable borrow occurs here  
5 | let x_coord2 = &mut point.0;  
| ^^^^^^^^^^^^ second mutable borrow occurs here  
6 | *x_coord = 20;  
| ------------- first borrow later used here  
  
For more information about this error, try `rustc --explain E0499`.  
error: could not compile `playground` (bin "playground") due to 1 previous error
```

Esempio di un'exclusive reference e di una shared reference per lo stesso valore:

```rust
fn main() {
    let mut point = (1, 2);
    let x_coord = &mut point.0;
    let mut x_coord2 = &point.0;
    *x_coord = 20;
    println!("point: {point:?}");
}
```

```sh
error[E0502]: cannot borrow `point.0` as immutable because it is also borrowed as mutable  
--> src/main.rs:5:24  
|  
4 | let x_coord = &mut point.0;  
| ------------ mutable borrow occurs here  
5 | let mut x_coord2 = &point.0;  
| ^^^^^^^^ immutable borrow occurs here  
6 | *x_coord = 20;  
| ------------- mutable borrow later used here  
  
For more information about this error, try `rustc --explain E0502`.  
error: could not compile `playground` (bin "playground") due to 1 previous error
```
## Slices
Uno **slice** viene usato per controllare una parte di un insieme più grande.

```rust
fn main() {
    let a: [i32; 6] = [10, 20, 30, 40, 50, 60];
    println!("a: {a:?}");
    let s: &[i32] = &a[2..4];
    println!("s: {s:?}");
}
```

```sh
a: [10, 20, 30, 40, 50, 60]  
s: [30, 40]
```

* Se lo slice inizia dall'indice $0$, la sintassi degli intervalli di Rust ci permette di omettere l'indice iniziale, quindi `&a[0..a.len()]` e `&a[..a.len()]` sono equivalenti.
* Lo stesso vale per l'ultimo indice, quindi `&a[2..a.len()]` e `&a[2..]` sono identici.
* Per creare facilmente uno slice dell'intero array, possiamo quindi usare `&a[..]`.
* `s` è una reference ad uno slice di `i32`. Si noti che il tipo di `s` (`&[i32]`) non specifica più la lunghezza dell'array. Questo ci permette di eseguire operazioni su slice di dimensioni diverse.
* Gli slice fanno **borrowing** un altro oggetto. In questo esempio, `a` deve rimanere **vivo** (cioè nello **scope**) almeno per tutto il tempo in cui lo slice esiste.
## Stringhe
Rust fornisce due tipi di stringhe:
* `&str` è uno slice di caratteri UTF-8, simile a `&[u8]`. `&str` pertanto è una reference **immutabile** ad una stringa UTF-8 salvata in un'area di memoria.
* `String` è un *owned buffer* di caratteri UTF-8, simile a `Vec<T>`. In particolare `String` è un **wrapper** di un vettore di bytes.

```rust
fn main() {
    let s1: &str = "World";
    println!("s1: {s1}");

    let mut s2: String = String::from("Hello ");
    println!("s2: {s2}");
    s2.push_str(s1);
    println!("s2: {s2}");

    let s3: &str = &s2[s2.len() - s1.len()..];
    println!("s3: {s3}");
}
```

```sh
s1: World  
s2: Hello  
s2: Hello World  
s3: World
```

* Come per molti altri tipi, `String::from()` crea una stringa a partire da un **string literal**, mentre `String::new()` crea una nuova stringa vuota, alla quale è possibile aggiungere dati utilizzando i metodi `push()` e `push_str()`.
* La macro `format!()` è un modo conveniente per generare una **owned string** (`String`) a partire da valori dinamici. Accetta le stesse specifiche di formattazione di `println!()`.
```rust
fn main() {
    let nome = "Marco";
    let eta = 21;

    let messaggio = format!("Ciao, mi chiamo {} e ho {} anni.", nome, eta);

    println!("{}", messaggio);
}

```

```sh
Ciao, mi chiamo Marco e ho 21 anni.
```


* È possibile ottenere **slice** di tipo `&str` da una `String` usando `&` e, opzionalmente, una selezione di intervallo. Tuttavia, se l'intervallo di byte selezionato **non è allineato ai confini dei caratteri**, l'espressione genererà un **panic**. L'iteratore `chars` scorre sui caratteri ed è preferibile rispetto alla gestione manuale dei confini dei caratteri.

```rust
fn main() {
    let parola = String::from("Rust🚀");

    // Itera sui caratteri della stringa
    for c in parola.chars() {
        println!("{}", c);
    }
}
```

```sh
R
u
s
t
🚀
```

*Nota*: si può utilizzare `.bytes()` per iterare secondo la rappresentazione in bytes dei caratteri.
* Le **byte strings** permettono di creare direttamente valori `&[u8]`:

```rust
fn main() {
    println!("{:?}", b"abc");
    println!("{:?}", &[97, 98, 99]);
}
```

```sh
[97, 98, 99]
[97, 98, 99]
```

* Le **raw strings** permettono di creare valori `&str` con gli *escapes disabilitati*. Le virgolette doppie possono possono essere incluse con lo stesso numero di `#` da ogni parte delle virgolette.

```rust
fn main() {
    println!(r#"<a href="link.html">link</a>"#);
    println!("<a href=\"link.html\">link</a>");
}
```

```sh
<a href="link.html">link</a>  
<a href="link.html">link</a>
```
## Reference Validity
Rust utilizza una serie di regole per le **reference** che garantisce la loro sicurezza d'uso. Per esempio le reference non possono mai essere `null`. Inoltre *le reference non possono vivere più dei dati a cui puntano*.

```rust
fn main() {
    let x_ref = {
        let x = 10;
        &x
    };
    println!("x: {x_ref}");
}
```

Questo codice genera un errore poiché si sta provando a stampare una reference ad un elemento che non esiste più:

```sh
Compiling playground v0.0.1 (/playground)  
error[E0597]: `x` does not live long enough  
--> src/main.rs:5:9  
|  
| let x_ref = {  
| ----- borrow later stored here  
| let x = 10;  
| - binding `x` declared here  
| &x  
| ^^ borrowed value does not live long enough  
| };  
| - `x` dropped here while still borrowed  
  
For more information about this error, try `rustc --explain E0597`.  
error: could not compile `playground` (bin "playground") due to 1 previous error
```

 *Nota*: Rust permette di rendere un tipo **nullable** con il tipo `Option`, di cui si discuterà in seguito.
# User-Defined Types
## Named Structs
Come C++, anche Rust permette di definire delle **struct**:

```rust
struct Person {
    name: String,
    age: u8,
}

fn describe(person: &Person) {
    println!("{} is {} years old", person.name, person.age);
}

fn main() {
    let mut peter = Person { name: String::from("Peter"), age: 27 };
    describe(&peter);

    peter.age = 28;
    describe(&peter);

    let name = String::from("Avery");
    let age = 39;
    let avery = Person { name, age };
    describe(&avery);

    let jackie = Person { name: String::from("Jackie"), ..avery };
    describe(&jackie);
}
```

```sh
Peter is 27 years old  
Peter is 28 years old  
Avery is 39 years old  
Jackie is 39 years old
```

* La sintassi `..avery` ci permette di copiare la maggior parte dei campi da un istanza già creata della stessa struct, senza doverli copiare tutti. Deve necessariamente essere l'ultimo elemento.
* Diversamente da C++ non c'è **ereditarietà** fra struct.
## Tuple Structs
Se i nomi dei campi non sono importanti si possono usare le **tuple structs**.

```rust
struct Point(i32, i32);

fn main() {
    let p = Point(17, 23);
    println!("({}, {})", p.0, p.1);
}
```

```sh
(17, 23)
```

Ciò viene spesso usato per *single-field wrappers* (chiamati **newtypes**).

```rust
struct PoundsOfForce(f64);
struct Newtons(f64);

fn compute_thruster_force() -> PoundsOfForce {
    todo!("Ask a rocket scientist at NASA")
}

fn set_thruster_force(force: Newtons) {
    // ...
}

fn main() {
    let force = compute_thruster_force();
    set_thruster_force(force);
}
```
## Enums
Come in altri linguaggi, la keyword `enum` permette la creazione di un tipo che abbia alcuni possibili valori.
```rust
#[derive(Debug)]
enum Direction {
    Left,
    Right,
}

#[derive(Debug)]
enum PlayerMove {
    Pass,                        // Simple variant
    Run(Direction),              // Tuple variant
    Teleport { x: u32, y: u32 }, // Struct variant
}

fn main() {

    let player_move: PlayerMove = PlayerMove::Run(Direction::Left);
    println!("On this turn: {player_move:?}");
    
    let player_move: PlayerMove = PlayerMove::Teleport{x: 4, y: 2};
    println!("On this turn: {player_move:?}");
}
```

```sh
On this turn: Run(Left)  
On this turn: Teleport { x: 4, y: 2 }
```
## Type Aliases
Un **type alias** crea un altro nome per un tipo. I due tipi possono essere usati intercambiabilmente. È molto simile a `typedef` in C.

```rust
enum CarryableConcreteItem {
    Left,
    Right,
}

type Item = CarryableConcreteItem;

// Aliases are more useful with long, complex types:
use std::cell::RefCell;
use std::sync::{Arc, RwLock};
type PlayerInventory = RwLock<Vec<Arc<RefCell<Item>>>>;
```

*Nota*: In genere è preferibile utilizzare un **newtype**, in quanto crea un nuovo (diverso) tipo. Si preferisca `struct InventoryCount(usize)` a `type InventoryCount = usize`.
## `const`
* I valori `const` sono valutati a compile-time. 
* Vengono messi *inline* ogni volta in cui sono utilizzati.

```rust
const DIGEST_SIZE: usize = 3;
const FILL_VALUE: u8 = calculate_fill_value();

const fn calculate_fill_value() -> u8 {
    if DIGEST_SIZE < 10 {
        42
    } else {
        13
    }
}

fn compute_digest(text: &str) -> [u8; DIGEST_SIZE] {
    let mut digest = [FILL_VALUE; DIGEST_SIZE];
    for (idx, &b) in text.as_bytes().iter().enumerate() {
        digest[idx % DIGEST_SIZE] = digest[idx % DIGEST_SIZE].wrapping_add(b);
    }
    digest
}

fn main() {
    let digest = compute_digest("Hello");
    println!("digest: {digest:?}");
}
```

```sh
digest: [222, 254, 150]
```

* Solo funzioni `const` possono essere chiamate a *compile time* per generare valori `const`. Le funzioni `const` possono tuttavia essere chiamate a *runtime*.
* `const` è semanticamente molto simile a `constexpr` in C++.
## `static`
Le variabili `static` *vivranno per tutta la durata del programma*.

```rust
static BANNER: &str = "Welcome to RustOS 3.14";

fn main() {
    println!("{BANNER}");
}
```

```sh
Welcome to RustOS 3.14
```

* `static` garantisce **object identity** (identità di oggetto), le variabili `static` pertanto hanno un indirizzo in memoria ed uno stato interno.
* Le variabili `static` non vengono **inserite inline** quando utilizzate e hanno una reale posizione di memoria associata. Questo è utile per codice **unsafe** e **embedded**. Quando una **variabile globale** *non ha bisogno di un'identità di oggetto* generalmente si preferisce usare `const`.
* Visto che le variabili `static` possono essere accedute da qualsiasi **thread**, esse devono essere `Sync`. La mutabilità interna è possibile grazie ad un `Mutex`, di cui si parlerà in seguito.

```rust
use std::sync::Mutex;
static COUNTER: Mutex<i32> = Mutex::new(0);
fn main() {
    let mut num = COUNTER.lock().unwrap();
    *num += 1;
    println!("Counter: {}", num);
}
```

```sh
Counter: 1
```



