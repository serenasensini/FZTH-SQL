# Java-Collections

Molte applicazioni richiedono di gestire collezioni di oggetti; gli array sono uno strumento di basso livello con molte limitazioni, come la dimensione della struttura e/o la ricerca non dinamica. Le Collections rappresentano gruppi di oggetti (elementi) che possono essere ordinati, duplicati e/o modificati.

## Cosa sono
Ci sono degli strumenti che sono stati introdotti a partire da Java 2 che hanno permesso di rappresentare altri tipi di strutture dati, come visibile nella figura seguente:
![Collections](http://fresh2refresh.com/wp-content/uploads/2013/08/Java-Framework.png)

L'interface Collection dichiara i metodi di una generica collezione:
- List: Collezioni sequenziali di oggetti i cui elementi possiedono una posizione (anche se l'accesso rimane dinamico) e senza gestione dei duplicati;
- Set: Collezioni che **non** ammettono duplicati i cui elementi e **non** possiedono posizione;
(- Map: Collezioni con chiave-valore che **non** ammettono duplicati sulle chiavi.)

L'interface Collection dichiara i metodi di una generica collezione. Questi metodi permettono di svolgere operazioni come:
- Aggiungere un oggetto;
- Restituire la dimensione della collezione;
- Verificare se la collezione è vuota;
- Rimuovere un oggetto.

## Come si usano

Codice dell'interfaccia Collection:
```
public interface Collection<E> extends Iterable<E> {
// Ope r a r igfaZYk]
int size();
boolean isEmpty();
boolean contains(Object element);
boolean add(E element); // O p tional
boolean remove(Object element); // O p tional
Iterator iterator();
// Ope r aragfakmdd±afka]e]
boolean containsAll(Collection<?> c);
boolean addAll(Collection<? extends E> c); // Opt i onal
boolean removeAll(Collection<?> c); // Opt i onal
boolean retainAll(Collection<?> c); // Opt i onal
void clear(); 
```

## Liste

## Insiemi

## Mappe
L'interface Map offre le operazioni di un dizionario: una mappa è una collezione di coppie chiave-valore, e fornisce le seguenti operazioni:
- Accesso per chiave: ottenere il valore associato ad una chiave;
- Cancellare una coppia tramite la chiave;
- Inserire una nuova coppia chiave-valore.

Esempio:
```
  HashMap<Integer, String> map = new HashMap<Integer, String>();

  //Adding elements
  map.put(12, "Marco");
  map.put(2, "Luca");
  map.put(17, "Giovanni");

  // Get values by key
  String marco= map.get(12);
  System.out.println("Number 12 is: "+marco);

  // Remove by key
  hmap.remove(3);
  HashMap<String, HashMap> selects = new HashMap<String, HashMap>();

  // Search with for-each
  for(Map.Entry<Integer, String> entry : map.entrySet()) {
      String key = entry.getKey();
      String value = entry.getValue();

      System.out.println(value);
  }

}
```
