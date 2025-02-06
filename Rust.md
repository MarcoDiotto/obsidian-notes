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
`match` è l'equivalente di `switch`, viene utilizzato per confrontare un valore con diverse opzioni.
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
# Pattern Matching
## Matching Values
La keyword `match` permette anche di confrontare un valore rispetto a uno o più **pattern**. I pattern possono essere semplici valori (e in tal caso l'uso di `match` è simile a quello di `switch` in C++), ma anche condizioni più complesse.

```rust
#[rustfmt::skip]
fn main() {
    let input = 'x';
    match input {
        'q'                       => println!("Quitting"),
        'a' | 's' | 'w' | 'd'     => println!("Moving around"),
        '0'..='9'                 => println!("Number input"),
        key if key.is_lowercase() => println!("Lowercase: {key}"),
        _                         => println!("Something else"),
    }
}
```

```sh
Lowercase: x
```

Una variabile nel pattern (come `key` nel nostro esempio) creerà un binding che potrà essere usato nel relativo ramo del confronto.

Di seguito viene spiegata un po' di sintassi di `match`:
* `|` corrisponde ad un **or**.
* `..` espande il range il più possibile.
* `1..=5`rappresenta un range inclusivo.
* `_` è una **wildcard**.
## `@` syntax
La sintassi `@` permette di fare un binding parziale di un pattern ad una variabile.

```rust
let opt = Some(123);
match opt {
    outer @ Some(inner) => {
        println!("outer: {outer:?}, inner: {inner}");
    }
    None => {}
}
```

```sh
outer: Some(123), inner: 123
```

In questo caso `outer` contiene tutto il pattern `Some(123)`, mentre `inner` ha destrutturato `123` dal pattern originario.
## Destructuring structs
Come le tuple, anche le struct possono essere **destrutturate** col matching.

```rust
struct Foo {
    x: (u32, u32),
    y: u32,
}

#[rustfmt::skip]
fn main() {
    let foo = Foo { x: (1, 2), y: 3 };
    match foo {
        Foo { x: (1, b), y } => println!("x.0 = 1, b = {b}, y = {y}"),
        Foo { y: 2, x: i }   => println!("y = 2, x = {i:?}"),
        Foo { y, .. }        => println!("y = {y}, other fields were ignored"),
    }
}
```

```shell
x.0 = 1, b = 2, y = 3
```
## Destructuring Enums
Come le tuple, anche gli `enum` possono essere destrutturati.

In questo modo possiamo anche usare i pattern per fare binding delle variabili a parte dei nostri valori, così si può ispezionare la struttura dei nostri tipi.

```rust
enum Result {
    Ok(i32),
    Err(String),
}

fn divide_in_two(n: i32) -> Result {
    if n % 2 == 0 {
        Result::Ok(n / 2)
    } else {
        Result::Err(format!("cannot divide {n} into two equal parts"))
    }
}

fn main() {
    let n = 100;
    match divide_in_two(n) {
        Result::Ok(half) => println!("{n} divided in two is {half}"),
        Result::Err(msg) => println!("sorry, an error happened: {msg}"),
    }
}
```

```sh
100 divided in two is 50
```
## `Let` Control Flow
Rust ha dei costrutti per il **control flow** che differiscono da altri linguaggi. Tali costrutti vengono usati per pattern matching e sono i seguenti:
* `if let`.
* `while let`.
* `let else`.
### `if let` Expressions
Con `if let` possiamo eseguire codice differente a seconda della corrispondenza di un valore con un determinato pattern.

```rust
use std::time::Duration;

fn sleep_for(secs: f32) {
    if let Ok(duration) = Duration::try_from_secs_f32(secs) {
        std::thread::sleep(duration);
        println!("slept for {duration:?}");
    }
    
    else {
        println!("{secs} non è in tempo valido");
    }
}

fn main() {
    sleep_for(-10.0);
    sleep_for(0.8);
}
```

```sh
-10 non è in tempo valido  
slept for 800.000012ms
```
### `while let` Statements
Analogamente a come succede con `if let`, `while let` testa ripetutamente un valore rispetto ad  un pattern.

```rust
fn main() {
    let mut name = String::from("Comprehensive Rust 🦀");
    let mut res: String = String::new();
    while let Some(c) = name.pop() {
        res.push(c);
    }
    println!("{res}");
    // (There are more efficient ways to reverse a string!)
}
```

```sh
🦀 tsuR evisneherpmoC
```

In questo caso `String::pop` ritorna `Some(c)` finché la stringa non sarà vuota, dopodiché ritornerà `None`. In questo modo continuiamo ad iterare fino al raggiungimento di `None`

*Nota*: `while let` non può essere utilizzato come un espressione perché potrebbe non tornare alcun valore se la condizione è falsa.
### `let else` Statements

Si usa `else` come ramo alternativo di `let`.  Il caso `else` deve essere diverso da quello del successo(`return`, `break` o panic).

```rust
fn hex_or_die_trying(maybe_string: Option<String>) -> Result<u32, String> {
    let Some(s) = maybe_string else {
        return Err(String::from("got None"));
    };

    let Some(first_byte_char) = s.chars().next() else {
        return Err(String::from("got empty string"));
    };

    let Some(digit) = first_byte_char.to_digit(16) else {
        return Err(String::from("not a hex digit"));
    };

    Ok(digit)
}
```

Questo codice non è altro che una versione più "pulita" di questo:

```rust
fn hex_or_die_trying(maybe_string: Option<String>) -> Result<u32, String> {
    // TODO: The structure of this code is difficult to follow -- rewrite it with let-else!
    if let Some(s) = maybe_string {
        if let Some(first_byte_char) = s.chars().next() {
            if let Some(digit) = first_byte_char.to_digit(16) {
                Ok(digit)
            } else {
                Err(String::from("not a hex digit"))
            }
        } else {
            Err(String::from("got empty string"))
        }
    } else {
        Err(String::from("got None"))
    }
}
```

*Nota*: I `let else` hanno "appiattito" gli `if let` del caso originale.
# Methods and Traits
## Methods
In Rust si possono aggiungere dei **metodi** alle nostre struct grazie al blocco `imp`

```rust
#[derive(Debug)]
struct CarRace {
    name: String,
    laps: Vec<i32>,
}

impl CarRace {
    // No receiver, a static method
    fn new(name: &str) -> Self {
        Self { name: String::from(name), laps: Vec::new() }
    }

    // Exclusive borrowed read-write access to self
    fn add_lap(&mut self, lap: i32) {
        self.laps.push(lap);
    }

    // Shared and read-only borrowed access to self
    fn print_laps(&self) {
        println!("Recorded {} laps for {}:", self.laps.len(), self.name);
        for (idx, lap) in self.laps.iter().enumerate() {
            println!("Lap {idx}: {lap} sec");
        }
    }

    // Exclusive ownership of self (covered later)
    fn finish(self) {
        let total: i32 = self.laps.iter().sum();
        println!("Race {} is finished, total lap time: {}", self.name, total);
    }
}

fn main() {
    let mut race = CarRace::new("Monaco Grand Prix");
    race.add_lap(70);
    race.add_lap(68);
    race.print_laps();
    race.add_lap(71);
    race.print_laps();
    race.finish();
    // race.add_lap(42); -> errore, l'oggetto non esiste più.
}
```

```sh
Recorded 2 laps for Monaco Grand Prix:  
Lap 0: 70 sec  
Lap 1: 68 sec  
Recorded 3 laps for Monaco Grand Prix:  
Lap 0: 70 sec  
Lap 1: 68 sec  
Lap 2: 71 sec  
Race Monaco Grand Prix is finished, total lap time: 209
```

L'argomento `self` specifica il **ricevente**, ovvero *l'oggetto su cui il metodo viene applicato*. I riceventi più comuni per un oggetto sono:
* `&self` $\to$ l'oggetto subisce **borrowing** usando una **shared reference**. In altre parole l'oggetto è acceduto in sola lettura e può essere utilizzato nuovamente dopo la chiamata al metodo.
* `&mut self` $\to$ l'oggetto subisce **borrowing** usando una **exclusive reference**. In altre parole l'oggetto è acceduto in lettura e scrittura e può essere utilizzato nuovamente dopo la chiamata al metodo.
* `self` $\to$ l'**ownership** dell'oggetto passa al metodo. L'oggetto verrà deallocato dopo la fine del metodo (se l'ownership non viene esplicitamente spostata). Avere l'ownership tuttavia non comporta la mutabilità dell'oggetto.
* `mut self` $\to$ come `self` ma l'oggetto è mutabile.
* Nessun ricevente $\to$ metodo statico della struct. Tipicamente usato per creare **costruttori** che vengono chiamati `new` per convenzione.

*Nota*: `self` non è altro che un **type alias** per `impl`
## Traits
Rust usa i **traits** per astrarre sui tipi, sono simili alle **interfacce**.
Come accade per le interfacce, un trait definisce una serie di metodi che un tipo deve avere per implementare tale trait.

```rust
trait Pet {
    /// Return a sentence from this pet.
    fn talk(&self) -> String;

    /// Print a string to the terminal greeting this pet.
    fn greet(&self);
}
```
### Implementing Traits
Per fare in modo che una struct implementi un trait, si utilizza la keyword `for`, come evidenziato nell'esempio seguente.

```rust
trait Pet {
    fn talk(&self) -> String;

    fn greet(&self) {
        println!("Oh you're a cutie! What's your name? {}", self.talk());
    }
}

struct Dog {
    name: String,
    age: i8,
}

impl Pet for Dog {
    fn talk(&self) -> String {
        format!("Woof, my name is {}!", self.name)
    }
}

fn main() {
    let fido = Dog { name: String::from("Fido"), age: 5 };
    fido.greet();
}
```

```sh
Oh you're a cutie! What's your name? Woof, my name is Fido!
```

*Nota*: come accade per le interfacce in Java, anche i trait possono avere dei metodi di default, come per esempio `greet(&self)` in questo esempio.
### Supertaits
Un trait può richiedere l'implementazione di altri traits, chiamati **supertraits**. Nell'esempio seguente, ogni tipo che implementi `Pet`, dovrà anche implementare `Animal`.

```rust
trait Animal {
    fn leg_count(&self) -> u32;
}

trait Pet: Animal { // -> Animal è supertrait per Pet
    fn name(&self) -> String;
}

struct Dog(String);
// VIsto che dog implementa Pet, dovrà anche implementare Animal
impl Animal for Dog {
    fn leg_count(&self) -> u32 {
        4
    }
}

impl Pet for Dog {
    fn name(&self) -> String {
        self.0.clone()
    }
}

fn main() {
    let puppy = Dog(String::from("Rex"));
    println!("{} has {} legs", puppy.name(), puppy.leg_count());
}
```

```sh
Rex has 4 legs
```

*Nota*: tale feature viene chiamata **trait inheritance**, tuttavia non bisogna aspettarsi che questa funzioni come l'inheritance dei linguaggi ad oggetti. Si tratta semplicemente di ulteriori requisiti da implementare per un trait.
### Associated Types
Gli **associated type** sono "placeholder" forniti dall'implementazione del trait.
Gli associated type sono spesso chiamati **output types**, poiché il tipo viene scelto da chi fornisce l'implementazione e non dal chiamante.

```rust
#[derive(Debug)]
struct Meters(i32);
#[derive(Debug)]
struct MetersSquared(i32);

trait Multiply {
    type Output;
    fn multiply(&self, other: &Self) -> Self::Output;
}

impl Multiply for Meters {
    type Output = MetersSquared;
    fn multiply(&self, other: &Self) -> Self::Output {
        MetersSquared(self.0 * other.0)
    }
}

fn main() {
    println!("{:?}", Meters(10).multiply(&Meters(20)));
}
```

```sh
MetersSquared(200)
```

Nell'esempio sopra riportato `Output` è un associated type che viene definito dall'implementazione del trait.
In questo caso `Output` è stato sostituito da `MetersSquared`. Inoltre `Output` non fa parte di `self` (ovvero `Meters`), ma solo del trait, e pertanto può essere modificato anche con un accesso in sola lettura, come nel nostro caso.
## Deriving
I tratti supportati possono essere automaticamente implementati per i tipi custom.

```rust
#[derive(Debug, Clone, Default)]
struct Player {
    name: String,
    strength: u8,
    hit_points: u8,
}

fn main() {
    let p1 = Player::default(); // Default trait adds `default` constructor.
    let mut p2 = p1.clone(); // Clone trait adds `clone` method.
    p2.name = String::from("EldurScrollz");
    // Debug trait adds support for printing with `{:?}`.
    println!("{p1:?} vs. {p2:?}");
}
```

```sh
Player { name: "", strength: 0, hit_points: 0 } vs. Player { name: "EldurScrollz", strength: 0, hit_points: 0 }
```
# Generics
## Generic Functions
Rust supporta i **generics**, che permettono di astrarre algoritmi o strutture dati sopra i tipi utilizzati o salvati.

```rust
/// Pick `even` or `odd` depending on the value of `n`.
fn pick<T>(n: i32, even: T, odd: T) -> T {
    if n % 2 == 0 {
        even
    } else {
        odd
    }
}

fn main() {
    println!("picked a number: {:?}", pick(97, 222, 333));
    println!("picked a string: {:?}", pick(28, "dog", "cat"));
}
```

```sh
picked a number: 333  
picked a string: "dog"
```

I **generics** di Rust sono simili ai **template** di C++, tuttavia con più restrizioni. Rust infatti compila parzialmente la funzione che utilizza i generics, pertanto la funzione dovrà essere valida per ogni tipo che rispetti le limitazioni imposte.
## Trait Bounds
Quando si lavora con i generics spesso si vuole che il tipo implementi qualche trait, in modo da poter chiamare i tipi del trait. Ciò si può fare con `T: Trait`.

```rust
fn duplicate<T: Clone>(a: T) -> (T, T) {
    (a.clone(), a.clone())
}

fn main() {
    let foo = String::from("foo");
    let pair = duplicate(foo);
    println!("{pair:?}");
}
```

```sh
("foo", "foo")
```

Questo si può fare anche con la clausola `where` che abbiamo già incontrato.

```rust
fn duplicate<T>(a: T) -> (T, T)
where
    T: Clone,
{
    (a.clone(), a.clone())
}
```

Questa forma è ancora più potente, poiché il tipo a sinistra di `:` può essere arbitrario.

*Nota*: Quando più trait sono necessari, è possibile collegarli con `+`.
## Generic Data Types
È possibile usare generics per astrarre il field type concreto.

```rust
pub trait Logger {
    /// Log a message at the given verbosity level.
    fn log(&self, verbosity: u8, message: &str);
}

struct StderrLogger;

impl Logger for StderrLogger {
    fn log(&self, verbosity: u8, message: &str) {
        eprintln!("verbosity={verbosity}: {message}");
    }
}

/// Only log messages up to the given verbosity level.
struct VerbosityFilter<L> {
    max_verbosity: u8,
    inner: L,
}

impl<L: Logger> Logger for VerbosityFilter<L> {
    fn log(&self, verbosity: u8, message: &str) {
        if verbosity <= self.max_verbosity {
            self.inner.log(verbosity, message);
        }
    }
}

fn main() {
    let logger = VerbosityFilter { max_verbosity: 3, inner: StderrLogger };
    logger.log(5, "FYI");
    logger.log(2, "Uhoh");
}
```

```sh
verbosity=2: Uhoh
```

* **Perché `L` è specificato due volte in** `impl<L: Logger> .. VerbosityFilter<L>`**? Non è ridondante?**  
	* Questo accade perché si tratta di una sezione di implementazione generica per un tipo generico. Le due dichiarazioni sono indipendenti.
	* Significa che questi metodi sono definiti per **qualsiasi** `L`.  
	* È possibile scrivere `impl VerbosityFilter<StderrLogger> { .. }`.
		* `VerbosityFilter` è ancora un tipo generico, quindi puoi usare `VerbosityFilter<f64>`, ma i metodi definiti in questo blocco saranno disponibili **solo per** `VerbosityFilter<StderrLogger>`.
* Si noti che **non mettiamo un vincolo di trait** (`trait bound`) **direttamente sul tipo** `VerbosityFilter`. È possibile farlo, ma in genere, in Rust, i vincoli sui trait vengono specificati nei blocchi `impl`.

*Nota*: Se provassimo a usare `VerbosityFilter` su un tipo che **non implementa il trait** `Logger`, il compilatore Rust ci darebbe un errore, perché il tipo `L` non soddisferebbe il vincolo `L: Logger` definito nell'implementazione del trait `Logger` per `VerbosityFilter<L>`.
## Generic Traits
Anche i **traits** possono essere **generici**, così come tipi e funzioni. I parametri dei trait ottengono tipi concreti quando vengono utilizzati.

```rust
#[derive(Debug)]
struct Foo(String);

/* https://doc.rust-lang.org/stable/std/convert/trait.From.html
 *
 * pub trait From<T>: Sized {
 *   fn from(value: T) -> Self;
 * }
 */
 
impl From<u32> for Foo {
    fn from(from: u32) -> Foo {
        Foo(format!("Converted from integer: {from}"))
    }
}

impl From<bool> for Foo {
    fn from(from: bool) -> Foo {
        Foo(format!("Converted from bool: {from}"))
    }
}

fn main() {
    let from_int = Foo::from(123);
    let from_bool = Foo::from(true);
    println!("{from_int:?}, {from_bool:?}");
}
```

```sh
Foo("Converted from integer: 123"), Foo("Converted from bool: true")
```

*Nota*: L'implementazione del trait non deve coprire tutti i possibili tipi di parametri (sarebbe impossibile). Per esempio il codice funzionato sopra non funzionerebbe con `Foo:from("Hello")`, in quanto non abbiamo fornito supporto per le stringhe. Rust non ha (ancora) delle euristiche per scegliere la corrispondenza "più specifica".
## `impl Trait`
Come per i **trait bounds**, anche la sintassi `impl Trait` può essere usata in argomenti di funzione e return values.

```rust
// Syntactic sugar for:
//   fn add_42_millions<T: Into<i32>>(x: T) -> i32 {
fn add_42_millions(x: impl Into<i32>) -> i32 {
    x.into() + 42_000_000
}

fn pair_of(x: u32) -> impl std::fmt::Debug {
    (x + 1, x - 1)
}

fn main() {
    let many = add_42_millions(42_i8);
    println!("{many}");
    let many_more = add_42_millions(10_000_000);
    println!("{many_more}");
    let debuggable = pair_of(27);
    println!("debuggable: {debuggable:?}");
}
```

```sh
42000042  
52000000  
debuggable: (28, 26)
```

`impl Trait`  consente di lavorare con tipi che non è possibile nominare. Il significato di `impl Trait` è un po' diverso a seconda della posizione in cui viene usato:
* **Per un parametro**, `impl Trait` è come un parametro generico anonimo con un vincolo di trait.
* **Per un tipo di ritorno**, significa che il tipo di ritorno è un tipo concreto che implementa il trait, senza dover nominare il tipo. Questo può essere utile quando non vuoi esporre il tipo concreto in un'API pubblica.

L'inferenza è difficile nella posizione di ritorno. Una funzione che restituisce `impl Foo` sceglie il tipo concreto che restituisce, senza doverlo scrivere esplicitamente nel codice. Una funzione che restituisce un tipo generico come `collect<B>() -> B` può restituire qualsiasi tipo che soddisfi `B`, e il chiamante potrebbe dover scegliere un tipo, come con `let x: Vec<_> = foo.collect()` o con il turbofish(`::`), `foo.collect::<Vec<_>>()`.
## `dyn Trait`
Oltre che per lo **static dispatch** con i generics, Rust permette di usare i trait anche per il **dynamic dispatch** **type erased** con i trait objects.

```rust
struct Dog {
    name: String,
    age: i8,
}
struct Cat {
    lives: i8,
}

trait Pet {
    fn talk(&self) -> String;
}

impl Pet for Dog {
    fn talk(&self) -> String {
        format!("Woof, my name is {}!", self.name)
    }
}

impl Pet for Cat {
    fn talk(&self) -> String {
        String::from("Miau!")
    }
}

// Uses generics and static dispatch.
fn generic(pet: &impl Pet) {
    println!("Hello, who are you? {}", pet.talk());
}

// Uses type-erasure and dynamic dispatch.
fn dynamic(pet: &dyn Pet) {
    println!("Hello, who are you? {}", pet.talk());
}

fn main() {
    let cat = Cat { lives: 9 };
    let dog = Dog { name: String::from("Fido"), age: 5 };

    generic(&cat);
    generic(&dog);

    dynamic(&cat);
    dynamic(&dog);
}
```

```sh
Hello, who are you? Miau!  
Hello, who are you? Woof, my name is Fido!  
Hello, who are you? Miau!  
Hello, who are you? Woof, my name is Fido!
```

* I **generics**, incluso `impl Trait`, utilizzano il **monomorfismo** per creare un'istanza specializzata della funzione per ogni tipo diverso con cui il generico viene istanziato. Questo significa che chiamare un metodo di un trait all'interno di una funzione generica utilizza ancora **static dispatch**, poiché il compilatore ha tutte le informazioni sul tipo e può risolvere quale implementazione del trait utilizzare per quel tipo.
* Quando si utilizza `dyn Trait`, si usa invece il **dynamic dispatch** tramite una **tabella dei metodi virtuali** (vtable). Questo significa che c'è una sola versione della funzione `fn dynamic` che viene usata indipendentemente dal tipo di `Pet` passato.
* Quando si usa `dyn Trait`, l'oggetto trait deve essere "indiretto". In questo caso è una reference, anche se tipi di puntatori intelligenti come `Box` possono essere utilizzati.
* Durante l'esecuzione, un `&dyn Pet` è rappresentato come un **"fat pointer"**, cioè una coppia di due puntatori: un puntatore punta all'oggetto concreto che implementa `Pet`, e l'altro punta alla vtable per l'implementazione del trait per quel tipo. Quando si chiama il metodo `talk` su `&dyn Pet`, il compilatore cerca il puntatore della funzione `talk` nella vtable e poi invoca la funzione, passando il puntatore al `Dog` o `Cat` in quella funzione. Il compilatore non ha bisogno di conoscere il tipo concreto di `Pet` per fare questo.
* Un `dyn Trait` è considerato "type-erased" (con **"eliminazione del tipo"**), perché non abbiamo più la conoscenza a tempo di compilazione di quale sia il tipo concreto.
# Standard Library Types
## Standard Library
Come altri linguaggi di programmazione, anche Rust ha la sua **standard library**, nella quale sono contenuti i tipi più comuni usati su Rust.
In particolare, la standard library di Rust si compone di tre livelli:
* `core` include i tipi più basici e le funzioni che non dipendono da `libc`, da un allocator o addirittura da un sistema operativo .
* `alloc` include i tipi che necessitano di un **global heap allocator**, come ad esempio `Vec`, `Box` e `Arc`.
## Documentazione
La documentazione ufficiale di Rust è presente a [questo link](https://doc.rust-lang.org/stable/std/).
In alternativa, è possibile ottenere la documentazione con il seguente comando:

```sh
rustup doc --std
```

È possibile documentare anche il codice creato da noi con la sintassi `///`.
```rust
/// Determine whether the first argument is divisible by the second argument.
///
/// If the second argument is zero, the result is false.
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    if rhs == 0 {
        return false;
    }
    lhs % rhs == 0
}
```

La documentazione è trattata come **Markdown**. Tutta la documentazione è generata automaticamente in `docs.rs` usando il tool `rustdoc`.

Per documentare un item da dentro l'item stesso (per esempio da dentro un modulo) si utilizza `//!` oppure `/*! .. */`, che rappresentano gli **inner doc comments**.

```rust
//! This module contains functionality relating to divisibility of integers.
```
## [Option](https://doc.rust-lang.org/stable/std/option/index.html)
`Option<T>` può contenere due valori:
* Un valore di tipo `T`.
* `None`.

Nel prossimo esempio si utilizza `String::find` che ritorna un `Option<usize>`.

```rust
pub enum Option<T> {
    None,
    Some(T),
}
```

```rust
fn main() {
    let name = "Löwe 老虎 Léopard Gepardi";
    let mut position: Option<usize> = name.find('é');
    println!("find returned {position:?}");
    assert_eq!(position.unwrap(), 14);
    position = name.find('Z');
    println!("find returned {position:?}");
    assert_eq!(position.expect("Character not found"), 0);
}
```

```sh
find returned Some(14)  
find returned None

thread 'main' panicked at src/main.rs:9:25:  
Character not found
...
```

* `unwrap` torna il valore in `Option` oppure andrà in panic.
	* Si può andare in panic su `None` ma non si può non controllare `None`.
## [Result](https://doc.rust-lang.org/stable/std/result/index.html)
`Result` è simile ad `Option`, ma indica *il successo o il fallimento* di un'operazione, ognuna con una differente variante di `enum`.
È un generic (`Result<T,E>`), in cui `T` è usato nella variante `Ok` ed `E` è usato nella variante `Err`.

```rust
enum Result<T, E> {
   Ok(T),
   Err(E),
}
```

*Nota*: `Result` è il tipo standard per implementare l'**error handling**.

```rust
use std::fs::File;
use std::io::Read;

fn main() {
    let file: Result<File, std::io::Error> = File::open("diary.txt");
    match file {
        Ok(mut file) => {
            let mut contents = String::new();
            if let Ok(bytes) = file.read_to_string(&mut contents) {
                println!("Dear diary: {contents} ({bytes} bytes)");
            } else {
                println!("Could not read file content");
            }
        }
        Err(err) => {
            println!("The diary could not be opened: {err}");
        }
    }
}
```

```sh
The diary could not be opened: No such file or directory (os error 2)
```
## [String](https://doc.rust-lang.org/stable/std/string/struct.String.html)
`String` rappresenta una stringa UTF-8 modificabile.
`String` implementa `Deref<Target = str>`, il che significa che tutti i metodi di `str` possono essere chiamati su `String`.

```rust
fn main() {
    let mut s1 = String::new();
    s1.push_str("Hello");
    println!("s1: len = {}, capacity = {}", s1.len(), s1.capacity());

    let mut s2 = String::with_capacity(s1.len() + 1);
    s2.push_str(&s1);
    s2.push('!');
    println!("s2: len = {}, capacity = {}", s2.len(), s2.capacity());

    let s3 = String::from("🇨🇭");
    println!("s3: len = {}, number of chars = {}", s3.len(), s3.chars().count());
}
```

```sh
s1: len = 5, capacity = 8  
s2: len = 6, capacity = 6  
s3: len = 8, number of chars = 2
```

Alcuni metodi e alcune caratteristiche di `String`:
* `String::new` restituisce una nuova stringa vuota; si utilizza `String::with_capacity` quando si conosce la quantità di memoria da allocare per aggiungere dati alla stringa.
* `String::len` restituisce la dimensione della stringa in **byte** (che può essere diversa dalla sua lunghezza in caratteri).
* `String::chars` restituisce un iteratore sui caratteri effettivi. Si noti che un **char** può essere diverso da quello che consideriamo un "carattere" a causa dei **[grapheme clusters](https://docs.rs/unicode-segmentation/latest/unicode_segmentation/struct.Graphemes.html)**.
* Quando si parla di stringhe, si può fare riferimento sia a `&str` che a `String`.
* Quando un tipo implementa `Deref<Target = T>`, il compilatore ti permette di chiamare i metodi di `T` in modo trasparente.
* `String` è implementata come un **wrapper** attorno a un vettore di byte. Molte operazioni supportate sui **vector** sono anche disponibili su `String`, ma con alcune garanzie aggiuntive.
* Ci sono diversi modi per indicizzare una `String` (nel nostro esempio usiamo la stringa `s3`):
	* Per ottenere un carattere: `s3.chars().nth(i).unwrap()`, dove `i` è entro i limiti oppure fuori dai limiti.
	* Per ottenere una sottostringa: `s3[0..4]`, assicurandosi che l’intervallo sia allineato ai confini dei caratteri.
* Molti tipi possono essere convertiti in una stringa usando il metodo `to_string`. Questo tratto è implementato automaticamente per tutti i tipi che implementano `Display`, quindi *qualsiasi cosa che può essere formattata può anche essere convertita in una stringa*.
## [Vec](https://doc.rust-lang.org/stable/std/vec/struct.Vec.html)
`Vec` è lo standard *resizable heap-allocated buffer*.
`Vec` implementa `Deref<Target = [T]>`, pertanto si possono chiamare metodi di **slice** su un `Vec`.

```rust
fn main() {
    let mut v1 = Vec::new();
    v1.push(42);
    println!("v1: len = {}, capacity = {}", v1.len(), v1.capacity());

    let mut v2 = Vec::with_capacity(v1.len() + 1);
    v2.extend(v1.iter());
    v2.push(9999);
    println!("v2: len = {}, capacity = {}", v2.len(), v2.capacity());

    // Canonical macro to initialize a vector with elements.
    let mut v3 = vec![0, 0, 1, 2, 3, 4];

    // Retain only the even elements.
    v3.retain(|x| x % 2 == 0);
    println!("{v3:?}");

    // Remove consecutive duplicates.
    v3.dedup();
    println!("{v3:?}");
}
```

```sh
v1: len = 1, capacity = 4  
v2: len = 2, capacity = 2  
[0, 0, 2, 4]  
[0, 2, 4]
```

* `Vec` è un tipo di **collection**, insieme a `String` e `HashMap`. I dati che contiene sono memorizzati nello **heap**. Questo significa che la quantità di dati **non** deve essere nota a tempo di compilazione e può crescere o diminuire a runtime.
* Nota che `Vec<T>` è un tipo generico, ma **non è necessario specificare esplicitamente `T`**. Come sempre con l'inferenza dei tipi in Rust, il tipo `T` viene determinato durante la prima chiamata a `push`.
* La macro `vec![...]` è il metodo **canonico** da usare al posto di `Vec::new()` e permette di aggiungere **elementi iniziali** direttamente al vettore.
* Per indicizzare il vettore si usano le **parentesi quadre** `[ ]`, ma se si supera il limite degli indici il programma andrà in **panic**. In alternativa, il metodo `get` restituisce un `Option`, che può essere gestito in modo sicuro.
* La funzione `pop` rimuove l'ultimo elemento del vettore.
## [HashMap](https://doc.rust-lang.org/stable/std/collections/struct.HashMap.html)
Le **HashMap** standard, forniscono protezione da attacchi `HashDos`.

```rust
use std::collections::HashMap;

fn main() {
    let mut page_counts = HashMap::new();
    page_counts.insert("Adventures of Huckleberry Finn", 207);
    page_counts.insert("Grimms' Fairy Tales", 751);
    page_counts.insert("Pride and Prejudice", 303);

    if !page_counts.contains_key("Les Misérables") {
        println!(
            "We know about {} books, but not Les Misérables.",
            page_counts.len()
        );
    }

    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        match page_counts.get(book) {
            Some(count) => println!("{book}: {count} pages"),
            None => println!("{book} is unknown."),
        }
    }

    // Use the .entry() method to insert a value if nothing is found.
    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        let page_count: &mut i32 = page_counts.entry(book).or_insert(0);
        *page_count += 1;
    }

    println!("{page_counts:#?}");
}
```

```sh
We know about 3 books, but not Les Misérables.  
Pride and Prejudice: 303 pages  
Alice's Adventure in Wonderland is unknown.  
{  
"Alice's Adventure in Wonderland": 1,  
"Pride and Prejudice": 304,  
"Adventures of Huckleberry Finn": 207,  
"Grimms' Fairy Tales": 751,  
}
```
# Standard Library Traits
## Comparison
Questi tratti supportano la comparison fra valori. Tutti i tratti possono essere derivati per tipi che contengono campi che implementano questi tratti.
### `PartialEq` ed `Eq`
`PartialEq` è una relazione di equivalenza parziale, con i metodi `eq` e `ne`. Gli operatori `==` e `!=` chiamano questi metodi.

```rust
struct Key {
    id: u32,
    metadata: Option<String>,
}
impl PartialEq for Key {
    fn eq(&self, other: &Self) -> bool {
        self.id == other.id
    }
}
```

*Nota*: `eq` rappresenta una relazione di equivalenza completa, ovvero una relazione riflessiva, simmetrica e transitiva.
### `PartialOrd` ed `Ord`
`PartialOrd` definisce un ordinamento parziale, con un metodo `partial_cmp`. È utilizzato per implementare gli operatori `<`, `<=`, `>=` e `>`.

```rust
use std::cmp::Ordering;
#[derive(Eq, PartialEq)]
struct Citation {
    author: String,
    year: u32,
}
impl PartialOrd for Citation {
    fn partial_cmp(&self, other: &Self) -> Option<Ordering> {
        match self.author.partial_cmp(&other.author) {
            Some(Ordering::Equal) => self.year.partial_cmp(&other.year),
            author_ord => author_ord,
        }
    }
}
```

`Ord` rappresenta un ordinamento totale, com `cmp` che ritorna `Ordering`.
## Operators
L'*overloading degli operatori* è implementato con i traits in `std::ops`.

```rust
#[derive(Debug, Copy, Clone)]
struct Point {
    x: i32,
    y: i32,
}

impl std::ops::Add for Point {
    type Output = Self;

    fn add(self, other: Self) -> Self {
        Self { x: self.x + other.x, y: self.y + other.y }
    }
}

fn main() {
    let p1 = Point { x: 10, y: 20 };
    let p2 = Point { x: 100, y: 200 };
    println!("{p1:?} + {p2:?} = {:?}", p1 + p2);
}
```

```sh
Point { x: 10, y: 20 } + Point { x: 100, y: 200 } = Point { x: 110, y: 220 }
```

*Nota*: In questo caso `Output` è un **associated type** e non un **type parameter** poiché gli associated types sono controllati da chi implementa il trait mentre i type parameter sono controllati dal chiamante.
## `From` e `Into`
I tipi implementano`From` e `Into` per facilitare la **type conversion**. Diversamente da `as`, questi tipi comportano *conversione infallibile e senza perdite*.

```rust
fn main() {
    let s = String::from("hello");
    let addr = std::net::Ipv4Addr::from([127, 0, 0, 1]);
    let one = i16::from(true);
    let bigger = i32::from(123_i16);
    println!("{s}, {addr}, {one}, {bigger}");
}
```

```sh
hello, 127.0.0.1, 1, 123
```

`Into` è implementato automaticamente quando viene implementato `From`.

```rust
fn main() {
    let s: String = "hello".into();
    let addr: std::net::Ipv4Addr = [127, 0, 0, 1].into();
    let one: i16 = true.into();
    let bigger: i32 = 123_i16.into();
    println!("{s}, {addr}, {one}, {bigger}");
}
```

```sh
hello, 127.0.0.1, 1, 123
```

* È comune implementare solo `From`, poiché il tipo otterrà automaticamente anche l'implementazione di `Into`.
* Quando si dichiara il tipo di input di una funzione come *qualsiasi cosa che può essere convertita in una* `String`, la regola è opposta: si deve usare `Into`. La funzione accetterà sia i tipi che implementano `From`, sia quelli che implementano solo `Into`.
## Casting
Rust non ha **type conversion** implicita, ma supporta **cast espliciti** con `as`.

```rust
fn main() {
    let value: i64 = 1000;
    println!("as u16: {}", value as u16);
    println!("as i16: {}", value as i16);
    println!("as u8: {}", value as u8);
}
```

```sh
as u16: 1000  
as i16: 1000  
as u8: 232
```

*Nota*: A differenza di `From` e `Into` il cast con `as` non è infallibile e può portare a bug abbastanza subdoli.
## `Read` e `Write`

Usando `Read` e `BufRead` si possono astrarre le sorgenti `u8`.

```rust
use std::io::{BufRead, BufReader, Read, Result};

fn count_lines<R: Read>(reader: R) -> usize {
    let buf_reader = BufReader::new(reader);
    buf_reader.lines().count()
}

fn main() -> Result<()> {
    let slice: &[u8] = b"foo\nbar\nbaz\n";
    println!("lines in slice: {}", count_lines(slice));

    let file = std::fs::File::open(std::env::current_exe()?)?;
    println!("lines in file: {}", count_lines(file));
    Ok(())
}
```

```sh
lines in slice: 3  
lines in file: 16581
```

Allo stesso modo, `Write` ti permette di astrarre sui destinatari di dati `u8`.

```rust
use std::io::{Result, Write};

fn log<W: Write>(writer: &mut W, msg: &str) -> Result<()> {
    writer.write_all(msg.as_bytes())?;
    writer.write_all("\n".as_bytes())
}

fn main() -> Result<()> {
    let mut buffer = Vec::new();
    log(&mut buffer, "Hello")?;
    log(&mut buffer, "World")?;
    println!("Logged: {buffer:?}");
    Ok(())
}
```

```sh
Logged: [72, 101, 108, 108, 111, 10, 87, 111, 114, 108, 100, 10]
```
## The `Default` Trait
`Default` produce un valore di default per un valore.

```rust
#[derive(Debug, Default)]
struct Derived {
    x: u32,
    y: String,
    z: Implemented,
}

#[derive(Debug)]
struct Implemented(String);

impl Default for Implemented {
    fn default() -> Self {
        Self("John Smith".into())
    }
}

fn main() {
    let default_struct = Derived::default();
    println!("{default_struct:#?}");

    let almost_default_struct =
        Derived { y: "Y is set!".into(), ..Derived::default() };
    println!("{almost_default_struct:#?}");

    let nothing: Option<Derived> = None;
    println!("{:#?}", nothing.unwrap_or_default());
}
```

```sh
Derived {  
x: 0,  
y: "",  
z: Implemented(  
"John Smith",  
),  
}  
Derived {  
x: 0,  
y: "Y is set!",  
z: Implemented(  
"John Smith",  
),  
}  
Derived {  
x: 0,  
y: "",  
z: Implemented(  
"John Smith",  
),  
}
```
# Closures
Le **closures** in Rust sono funzioni anonime che possono catturare variabili dall'ambiente in cui sono definite. Sono simili alle lambda functions di altri linguaggi come Python o JavaScript.

## Closure Syntax
Le **closures** sono create con barre verticali: `|..| ..`

```rust
fn main() {
    let value = Some(13);
    dbg!(value.map(|num| format!("{num}")));

    let mut nums = vec![1, 10, 99, 24];
    // Sort even numbers first.
    nums.sort_by_key(|v| if v % 2 == 0 { (0, *v) } else { (1, *v) });
    dbg!(nums);
}
```

```sh
[src/main.rs:4:5] value.map(|num| format!("{num}")) = Some(  
"13",  
)  
[src/main.rs:9:5] nums = [  
10,  
24,  
1,  
99,  
]
```

Analizziamo il codice:

```rust
let value = Some(13);
dbg!(value.map(|num| format!("{num}")));
```

- `value` è un'istanza di `Option<i32>` che contiene il valore `Some(13)`.
- Il metodo `.map(|num| format!("{num}"))` viene chiamato su `value`:
    - Se `value` è `Some(num)`, allora esegue la closure `|num| format!("{num}")`, che converte `num` in una `String` (`"13"`).
    - Se `value` fosse `None`, la closure non verrebbe eseguita e restituirebbe `None`.
- Il risultato sarà quindi `Some("13".to_string())`.
- `dbg!` è una macro di debug che stampa il valore e lo restituisce.

```rust
let mut nums = vec![1, 10, 99, 24];
// Sort even numbers first.
nums.sort_by_key(|v| if v % 2 == 0 { (0, *v) } else { (1, *v) });
dbg!(nums);
```

- Il vettore iniziale è `[1, 10, 99, 24]`.
- `sort_by_key` ordina i numeri in base alla chiave restituita dalla closure `|v| if v % 2 == 0 { (0, *v) } else { (1, *v) }`:
    - Se `v` è pari (`v % 2 == 0`), la chiave è `(0, v)`, dando priorità agli elementi pari.
    - Se `v` è dispari, la chiave è `(1, v)`, quindi questi numeri verranno ordinati dopo i pari.
- Il primo elemento della tupla `(0, *v)` o `(1, *v)` determina la priorità (pari prima, dispari dopo), mentre il secondo (`*v`) ordina i numeri normalmente all'interno del loro gruppo
## Caratteristiche principali delle closures in Rust
### Possono essere assegnate a variabili

```rust
let add_one = |x| x + 1;
println!("{}", add_one(5)); // Output: 6
```

Qui, `add_one` è una closure che prende un valore `x` e restituisce `x + 1`.
### Possono catturare variabili dall'ambiente esterno

```rust
let multiplier = 2;
let multiply = |x| x * multiplier;
println!("{}", multiply(4)); // Output: 8
```

La closure `multiply` usa la variabile `multiplier` definita all'esterno.
### Possono essere usate come argomenti per funzioni di ordine superiore

```rust
let numbers = vec![1, 2, 3, 4];
let doubled: Vec<_> = numbers.iter().map(|x| x * 2).collect();
println!("{:?}", doubled); // Output: [2, 4, 6, 8]
```

Qui `.map(|x| x * 2)` applica la closure a ogni elemento del vettore.
### Possono avere diversi modi di cattura (by value, by reference, by mutable reference)

```rust
let mut count = 0;
let mut increment = || count += 1;
increment();
println!("{}", count); // Output: 1
```

La closure `increment` cattura `count` **mutabilmente**, quindi può modificarlo.