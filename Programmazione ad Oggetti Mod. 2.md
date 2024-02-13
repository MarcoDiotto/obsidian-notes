# Lezione 1
___
## Introduzione

I *paradigmi* di programmazione sono quello **operativo** e quello **funzionale**.
All'interno di tali *paradigmi* ci sono vari *stili di programmazione*.

Il *paradigma* è determinato dall'**assegnamento**.

```java
public class Main
{
	public static void main(String[] args)
	{
		int x = 3  //questa è un'inizializzazione
		x = 5 // questo è un assegnamento
	}
}
```

Per scrivere funzioni in *Java* non appartenenti a classi bisogna fare così:
 
```java
public class Main{
	public static int f(int n){
		return n + 1;
	}

	public int g(int n){
		return n+1;
	}
}
```

La funzione f è **statica** e non è un **metodo** poiché non necessita di istanze e utilizzo di altri oggetti.
Anche il **main** è un metodo **statico**, perché se così non fosse bisognerebbe istanziare qualcosa per poterlo avviare.
Nel **main** per invocare f basta fare `int x = f(7)` mentre per invocare g bisogna almeno istanziare l'oggetto cui appartiene `int y = new Main().g(7)`.
Un altro modo per invocare g è:

```java
Main o = new Main();
int y = 0.g(7);
```

La semantica è la stessa, tuttavia nel primo caso l'oggetto verrà distrutto dal **garbage collector** mentre nel secondo rimane attivo.
Un oggetto viene costruito **solo** con una `new`.

```java
Main o;
int x = o.g(y);
```

Il codice precedente **compila**, tuttavia a **runtime**  sarà lanciata un'eccezione.
La variabile `o` in questo caso non è un oggetto, è solo il "luogo in cui tenerlo", una **reference**.
*Java* è infatti un linguaggio in cui le chiamate avvengono **by reference**, solamente i *tipi primitivi* sono chiamati **by value**. Gli **oggetti** pertanto sono chiamati *reference types*.

```java
Main a = new Main();
Main b = a;
```

La variabile b è un *alias*, ovvero un altro pointer allo stesso oggetto. Le **classi** sono i *tipi*, gli **oggetti** sono i *valori* (o *istanze*).
Un linguaggio è *ad oggetti* quando offre il **subtyping** (ovvero una forma di **polimorfismo**).

## Polimorfismo

```java
public class Main{
	public class Animal
	{
	
		protected int weight;
		
		public Animal(int w)
		{
			this.weight = w;
		}
		public void eat(Animal a)
		{
			this.weight = a.weight;
		}
	}
	
	public class Dog extends Animal
	{
		private boolean pedgree;
		
		public(int w, boolean ped)
		{
			super(w);
			this.pedgree = ped;
		}
		
		public void bark()
		{
			System.out.println("bau!");
		}
		
		@Override
		public void eat(Animal a)
		{
			this.weight += a.weight * 3;
		}
	}
	
	public static void main(String[] args)
	{
		Dog fido = new Dog(30, false);
		Dog gigio = fido; //alias per fido
		Animal pluto = new Dog(40, true);
		Dog pippo = new Animal(50) // non si può fare
		pluto.bark() //non si può fare perché staticamente ha                      //tipo animal 
		pluto.eat(fido); //Dynamic dispatching, viene                                  //chiamata la eat di dog
		
		Collection<Integer> c = ArrayList<Integer>();
		int sz = c.size(); //Ancora dynamic dispatching
		
		gigio.eat(gigio); //legale per subsumption
		
		pluto = gigio; //pluto resta staticamente un Animal
	} 
}
```

L'*override* serve a modificare metodi preesistenti nelle sottoclassi e di conseguenza poterli usare, anche grazie al *dynamic dispatching*.

**Dynamic Dispatching** : dopo la chiamata del metodo viene utilizzato il tipo dinamico                                                              dell'oggetto, conosciuto a runtime.
**Subsumption** : possibilità di assegnare ad una cosa meno specifica, una più specifica.
