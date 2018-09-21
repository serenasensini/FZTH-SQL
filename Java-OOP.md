# Java_Tutorial

Breve tutorial su ereditarietà, classi astratte, interfacce.

## Ereditarietà 
E' uno dei concetti fondamentali nel paradigma di programmazione a oggetti. Permette di estendere classi esistenti, aggiungendo metodi e componenti. Se la classe B __eredita__ dalla classe A, si dice che B è una **sottoclasse** di A e che A è una **superclasse** di B. I due termini sono spesso sostituiti con i rispettivi figlio, padre, o classe estesa e classe base. L'ereditarietà è una relazione di generalizzazione su un certo oggetto: la superclasse definisce un concetto più generale, mentre la sottoclasse rappresenta una specifica  variante del concetto originale; questo tipo di relazione si chiama **is-a**.

### Codice:
```
public class Animale{

  public String nome;
  public String verso;
  
  public Animale(String nome, String verso){
    this.nome = nome;
    this.verso = verso;
  }
  
  public String verso(){...};
  public String moto(){...};
 
}

public class Mammifero extends Animale {
    public String pelo;
    public int mammelle;
    public String specie;
    public int numero_figli = 0;
    
    public Mammifero(String nome, String verso, String pelo, int mammelle, String specie){
      //invoca il costruttore della classe padre
      super(nome, verso);
      this.pelo = pelo;
      this.mammelle = mammelle;
      this.specie = specie;
    }

    public Mammifero riproduciti() {
       numero_figli++;
    }
    
    //GETTER E SETTER...
}
```

### Tips
- [x] E' possibile definire un costruttore in una classe padre? Sì, perché può essere implementata;
- [ ] E' possibile definire un due padri e farli estendere entrambi ad una classe figlia? No, perché Java non prevede il polimorfismo. Si può aggirare il problema usando le interfacce.
- [ ] E' possibile definire un metodo astratto nella classe padre? No, perché in tal caso si usa una classe padre astratta.

## Classi astratte
L’ereditarietà porta a riflettere sul rapporto fra __progetto e struttura__; nello specifico, una classe può definire uno schema e le proprietà base di una classe di entità lasciando “in bianco” alcune operazioni che verranno poi implementate dalle classi derivate. Una classe con queste caratteristiche **fattorizza**, operazioni  comuni a tutte le sue sottoclassi, e definisce dati comuni, ma non implementa le altre operazioni. Non è quindi possibile creare istanze di classi astratte, perché esistono dei metodi non definiti (quelli lasciati in bianco!).
Si definisce quindi **classi astratta** la struttura di una classe che può essere derivata, che non può essere però istanziata.

### Codice
```
/*Ogni animale avrà questa struttura*/
public abstract class Animale{

  public String nome;
  public String verso;
  
    //questi metodi non vengono implementati perché ogni sottoclasse avrà un comportamento differente (ex: un cane abbaia, un gatto miagola..)
  public abstract String verso();
  public abstract String moto();
  
  //questo metodo e' fattorizzato, perché sarà uguale per tutti gli animali
  public void stampaAnimale(){
    System.out.println("Sono un " + nome +  " e il mio verso e' " + verso); 
  }
}

/*Questa classe prende le proprietà di animale (grazie al concetto di ereditarietà) e definisce le proprie. */
public Cane extends Animale{

  public int numero_zampe;
  public String specie;
  
  public Cane(int numero, String spec){
    this.nome = "cane";
    this.verso = "Bau!";
    this.numero_zampe = numero;
    this.specie = spec;
  }
  
  public String verso(){
    return verso;
  }
  
  public String moto(){
    return "camminando a quattro zampe!";
  }
  
  //GETTER E SETTER...

}
```

### Tips
- [x] E' possibile definire un costruttore in una classe astratta? Sì, definendolo su proprietà **non** astratta;
- [ ] E' possibile definire un costruttore E usarlo? No, perché una classe astratta non può essere istanziata;
- [x] Quando una classe si definisce astratta? Quando anche solo una delle proprietà della classe (sia esso un attributo o un metodo) viene definito astratto;
- [x] Quando uso una classe astratta? Quando non tutti i metodi che definisco nella mia classe astratta dovranno essere implementati nella classe che la estende, ma comunque voglio avere uno schema "di base" da cui partire. 

## Interfacce 

Una interfaccia (interface) in Java ha una struttura simile a una classe, ma può contenere SOLO metodi d'istanza astratti e costanti (quindi **non** può contenere costruttori, variabili statiche, variabili di istanza e metodi statici). Definisce una sorta di "schema" o "bozza" pura e semplice di quella che poi sarà la struttura vera e propria di un oggetto. Si può dichiarare che una classe implementa (implements) una data interfaccia: in questo caso deve realizzare **tutti** i suoi metodi, fornendo dei metodi con la stessa intestazione (la prima riga del metodo) e con un corpo ben definito (le operazioni all'interno). 

### Codice
```
/*Ogni animale avrà questa struttura*/
public interface Animale{

  public String nome;
  public String verso;
  
    //questi metodi non vengono implementati perché ogni sottoclasse avrà un comportamento differente (ex: un cane abbaia, un gatto miagola..)
  public String verso();
  public String moto();
  
}

public interface Mammifero{
  
  public int periodoGestazione(int giorni);
  
}

/*Questa classe prende le proprietà di animale (grazie al concetto di ereditarietà) e definisce le proprie. */
public Cane implements Animale, Mammifero{

  public int numero_zampe;
  public String specie;
  
  public Cane(int numero, String spec){
    this.nome = "cane";
    this.verso = "Bau!";
    this.numero_zampe = numero;
    this.specie = spec;
  }
  
  public String verso(){
    return verso;
  }
  
  public String moto(){
    return "camminando a quattro zampe!";
  }
  
  public int periodoGestazione(int giorni){
    return 60;
  }
  
  //GETTER E SETTER...

}
```

### Tips
- [ ] Si può istanziare un'interfaccia? No;
- [x] Le classi che implementano l'interfaccia possono implementarne anche altre interfacce? Sì, perché tramite le interfacce è possibile avere una sorta di polimorfismo;
- [x] I metodi in un'interfaccia sono public o private? Sempre public.
- [x] Quando uso un'interfaccia? Quando può accadere che la mia interfaccia debba essere implementata insieme ad altre interfacce e quando voglio che tutti i metodi definiti in essa vengano definiti nella classe che la implementa.