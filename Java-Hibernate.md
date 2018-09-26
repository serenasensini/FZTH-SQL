# Tutorial per usare Hibernate

> Disclaimer: il tutorial usa MySQL come DBMS, ma si può applicare a qualunque DBMS. Si presuppone che quindi le ultime versioni di questo siano già installate prima dell'inizio del tutorial.

## Cos'è [?](https://hibernate.org/)
Si tratta di un framework che fornisce un servizio di Object-relational mapping (ORM) ovvero gestisce la persistenza dei dati sul database attraverso la rappresentazione e il mantenimento su database relazionale di un sistema di oggetti Java.

## Come funziona
Dovendo mappare una certa entità Java con un'entità presente nel database, si può ricorrere ad un framework come Hibernate per la realizzazione del mapping: la gestione della persistenza dell'oggetto viene completamente gestita da quest'ultimo che, tramite determinate annotazioni all'interno delle classi Java, è in grado di "mappare" e lavorare con gli oggetti presenti all'interno di un certo database. 

[Link tutorial](https://www.tutorialspoint.com/hibernate/pdf/hibernate_quick_guide.pdf)

![Schema](https://www.tutorialspoint.com/hibernate/images/hibernate_high_level.jpg)

Nell'esempio, andremo quindi a creare una classe Utente così fatta:

```
import java.sql.Date;

public class Utente {

	public int idUtente;
	public String nome;
	public String cognome;
	public Date data_nascita;
	public String citta;
	public int telefono;
	
	/*E' fondamentale che ogni attributo presente abbia il suo getter e setter con lo stesso
	 * IDENTICO nome dell'attributo presente come variabile globale.
	 * esempio:
	 * getCOGNOME: sbagliato
	 * getCog: sbagliato
	 * getCognome: corretto
	 * */
	public int getIdUtente() {
		return idUtente;
	}
	public void setIdUtente(int idUtente) {
		this.idUtente = idUtente;
	}
	...		
}

```

Nel progetto avremo anche un file chiamato "UtenteDAO" che si occuperà di gestire le transazioni sull'entità Utente, per ora così fatta:

```
public class UtenteDAO {

}
```

Nel database andremo a creare una tabella così fatta:

```
CREATE TABLE UTENTE(
	ID_UTENTE INT PRIMARY KEY,
	NOME VARCHAR(255) NOT NULL,
	COGNOME VARCHAR(255) NOT NULL,
	DATA_NASCITA DATE,
	CITTA VARCHAR(255) NOT NULL,
	TELEFONO INT
)
```

Riassumendo, i primi due file saranno nella cartella src del progetto Eclipse, mentre nel database sarà presente una tabella creata grazie allo script sopra scritto. 

A questo punto, nella classe Utente andiamo ad aggiungere le seguenti annotazioni:
- @Entity: specifica che la classe è un'entità mappabile con Hibernate;
- @Table(name="nomeTabella"): ci permette di mappare la classe Java con il nome corretto dell'entità del database, qualora non fosse lo stesso;
- @Column: specifica le colonne (i campi) presenti nella tabella del database; aggiungendo il parametro name all'interno delle parentesi, posso dichiarare qual è il nome corretto da utilizzare, qualora non sia lo stesso per via di maiuscole, minuscole o regole di sintassi;
- @Id: è un'annotazione specifica per l'attributo (o gli) che sono chiavi primarie nella tabella;
- @GeneratedValue(strategy=GenerationType.IDENTITY): specifica il tipo di chiave utilizzata; in questo caso, abbia una chiave che si autoincrementa autonomamente.

Per fare questo, andremo ad utilizzare la libreria presente a questo (link)[], che dev'essere inclusa nel progetto. Per includere una libreria nel progetto, è sufficiente cliccare con il tasto destro sul nome del progetto in Eclipse, andare su "Properties", cliccare su Java Build Path/Libraries e cliccare su "Add external Jar". Una volta caricata, per aggiornare il file se ancora vi dovessero essere errori di import, è sufficiente premere Ctrl+Maiusc+O.

La classe viene quindi così modificata:

```
import java.sql.Date;

@Entity
@Table(name="UTENTE")
public class Utente {

  @GeneratedValue(strategy=GenerationType.IDENTITY)
  @Id
  @Column(name="ID_AVVISO")
	public int idUtente;
  @Column(name="ID_AVVISO")
	public String nome;
  @Column(name="ID_AVVISO")
	public String cognome;
  @Column(name="ID_AVVISO")
	public Date data_nascita;
  @Column(name="ID_AVVISO")
	public String citta;
  @Column(name="ID_AVVISO")
	public int telefono;
	...		
}

```

## Tips
- [X] Cos'è il modello MVC? Vedi (link) [https://it.wikipedia.org/wiki/Model-view-controller]
- [X] Cos'è il modello ORM? Vedi (link)[https://it.wikipedia.org/wiki/Object-relational_mapping]
- [X] Cosa uso per far dialogare il mio database con l'applicazione Java? Un driver ad hoc per il tipo di database; i principali (ultime versioni) sono MYSQL [driver](https://dev.mysql.com/downloads/connector/j/5.1.html), PostgreSQL (driver)[https://jdbc.postgresql.org/download.html], SQL Server (driver)[https://www.microsoft.com/it-it/download/details.aspx?id=11774], DB2 (driver)[http://www-01.ibm.com/support/docview.wss?uid=swg21363866]
- [X] Come faccio a rendere una parola tutta in maiuscolo tramite shortcut? Ctrl+Maiusc+X (maiuscolo), Ctrl+Maiusc+Y (minuscolo).
