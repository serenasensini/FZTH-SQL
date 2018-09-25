# Tutorial sulle eccezioni in Java

## Cosa sono

Il termine è usato per descrivere l'occorrenza di eventi che alterano il normale flusso di esecuzione di un programma. 
Esempi: NullPointerException, FileNotFoundException, ArrayIndexOutOfBoundsException...

## Come gestirle

### Prima alternativa

```
 try {
            //il file che cerco di aprire non esiste; viene quindi generata un'eccezione che può essere catturata e gestita
            file = open("filenonesistente.txt");
        } catch (FileNotFoundException f) {
            System.out.println("Il file non esiste.");
        }
   try {
            //l'oggetto "animale" non è stato inizializzato; l'eccezione viene catturata e gestita
            Animale animale;
            animale.getNome();
        } catch (NullPointerException e) {
            System.out.println("L'animale non è stato inizializzato");
        }
```

### Seconda alternativa

```
String[] array = {"bla"};
public int quintoElemento(String[] array)
 throws MiaEccezione
 {
    //l'array contiene un solo elemento; un accesso alla quinta posizione, genererà un'eccezione;
    if(array.length() < 5){
      //la classe MiaEccezione dev'essere creata, come di seguito;
      throw new MiaEccezione();
    }else{
      return array[5];
      }
    }
}

public class MiaEccezione extends Exception{
  public MiaEccezione(String message){
    super(message);
  }
}
```
