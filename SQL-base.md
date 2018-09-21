# SQL_tutorial
Breve tutorial su SQL.

## Cos'è

> SQL è un linguaggio fondamentale per la creazione di database relazionali.

## Cos'è un database relazionale (RDBMS)

> La struttura fondamentale del modello relazionale e’ appunto la **relazione**, cioe’ una tabella costituita da __righe__
(tuple) e __colonne__ (attributi). Le relazioni rappresentano le entità che si ritiene essere interessanti nel database. 
Ogni istanza dell’entita’ trovera’ posto in una tupla della relazione, mentre gli attributi della relazione 
rappresenteranno le proprietà dell’entità. 
Ad esempio, se nel database si dovranno rappresentare dei clienti e i relativi ordini, si potra’ definire una relazione chiamata “Ordine_Cliente”, 
i cui attributi descrivono le caratteristiche dei clienti. Ciascuna tupla della relazione “Clienti” rappresentera’ 
una particolare persona con un certo nome e un certo ordine...

![alt text](https://www.okpedia.it/data/okpedia/database-relazionale-esempio.gif)

## Cos'è un database NON relazionale

> I dati sono conservati in documenti, non in tabelle, per cui la prima differenza con i DB relazionali sta nel fatto che le informazioni
non sono distribuite in differenti strutture logiche, ma vengono aggregate per oggetto in documenti la cui natura può essere di tipo 
chiave-valore o documenti basati su semantica JSON. 
L’assenza di tabelle permette ai database non relazioni di essere schemaless, ossia privi di un qualsiasi schema definito a priori e 
questa caratteristica conferisce ai DB NoSQL un altro vantaggio non trascurabile.

## Cos'è un DBMS

> E' un sistema software progettato per consentire la creazione, la manipolazione e l'interrogazione efficiente di database. Ne esistono vari, come ad esempio MYSQL, SQLServer, Oracle, PostgreQL, SQLite... 

## Creare un database

```
CREATE DATABASE Clienti; 
```

## Eliminare un database

```
DROP DATABASE Clienti;
```

## Creare una tabella

```
CREATE TABLE Clienti (
    ClienteID int,
    Cognome varchar(255),
    Nome varchar(255),
    Indirizzo varchar(255),
    Città varchar(255),    
);
```

## Modificare una tabella: aggiungere colonna

```
ALTER TABLE Clienti
ADD Nazione varchar(255); 
```

## Modificare una tabella: eliminare colonna

```
ALTER TABLE Clienti
DROP COLUMN Nazione;
```

## Eliminare una tabella

```
DROP TABLE Clienti; 
```

## Selezioni con SELECT: cosa sono e come usarle

> La maggior parte delle azioni che devi eseguire su un database vengono eseguite con istruzioni (statements) SQL.
La seguente istruzione SQL seleziona tutte le tuple presenti nella tabella "Clienti":

```
SELECT * FROM Clienti;
```

## Selezioni con SELECT DISTINCT
> Esiste poi una particolare istruzione, chiamata SELECT DISTINCT, che viene utilizzata per restituire solo valori distinti (diversi).
All'interno di una tabella, una colonna spesso contiene molti valori duplicati e a volte si desidera solo elencare i diversi valori (distinti).

```
SELECT DISTINCT nome FROM Clienti;
```

## Selezioni con WHERE: cosa sono e come usarle

> La clausola WHERE viene utilizzata per estrarre solo i record che soddisfano una condizione specificata. Le condizioni possono essere molteplici e sono utilizzate in OR, AND or NOT a seconda che ne debba essere soddisfatta solo una, entrambe o non debbano essere rispettate.

```
SELECT * FROM Clienti WHERE nome = 'Marco' AND cognome = 'Rossi' ;
```

## ORDER BY: cos'è e a cosa serve

> La parola chiave ORDER BY viene utilizzata per ordinare il set di risultati in ordine crescente o decrescente. La parola chiave ORDER BY ordina i record in ordine crescente (ASC) per default. Per ordinare i record in ordine decrescente, utilizzare la parola chiave DESC.

```
SELECT * FROM Clienti ORDER BY nome ;
```

## JOIN: cos'è e a cosa serve

> Una clausola JOIN viene utilizzata per combinare righe da due o più tabelle, in base a una colonna correlata tra di esse. Ne esistono tre tipi: INNER JOIN, che seleziona i record che matchano in entrambe le tabelle, LEFT JOIN che restituisce tutti i record dalla tabella di sinistra e i record corrispondenti dalla tabella di destra. Il risultato è NULL dal lato destro, se non c'è corrispondenza, RIGHT JOIN che restituisce tutti i record dalla tabella di destra e i record corrispondenti dalla tabella sinistra. Il risultato è NULL dal lato sinistro, quando non c'è corrispondenza.
```
CREATE TABLE Clienti (
    ClienteID int PRIMARY KEY,
    OrdineID int PRIMARY KEY,
    Cognome varchar(255),
    Nome varchar(255),
    Indirizzo varchar(255),
    Città varchar(255),    
);

CREATE TABLE Ordini (
    OrdineID int PRIMARY KEY,
    Prodotto varchar(255), 
);

SELECT Ordini.OrdineID, Clienti.Nome
FROM Ordini
LEFT JOIN Clienti ON Ordini.OrdineID=Clienti.ClienteID;
```

## Chiavi primarie: cosa sono e come usarle

> Il vincolo PRIMARY KEY identifica in modo univoco ogni record in una tabella di database. Le chiavi primarie devono contenere valori UNIQUE e non possono contenere valori NULL. Una tabella può avere solo una chiave primaria, che può consistere in campi singoli o multipli. 

```
CREATE TABLE Clienti (
    ClienteID int PRIMARY KEY,
    Cognome varchar(255),
    Nome varchar(255),
    Indirizzo varchar(255),
    Città varchar(255),    
);
```

## Inserimenti: come si eseguono
> L'istruzione INSERT INTO viene utilizzata per inserire nuovi record in una tabella. Nel primo esempio, inserisco solo i valori per le colonne specificate; nel secondo esempio, inserisco i valori di TUTTE le colonne presenti. Se le colonne non sono state dichiarate NULL, ovvero possono contenere valori nulli, allora è obbligatorio inserire dei valori quando inserisco una riga. **Importante**: se è stata definita una primary key su un attributo, questo non va specificato nell'inserimento; sarà il DBMS stesso a occuparsene.

```
INSERT INTO Clienti (Cognome, Nome, Indirizzo)
VALUES (value1, value2, value3);

INSERT INTO Clienti
VALUES (value1, value2, value3, ...);
```

## Aggiornamenti: come si eseguono
> L'istruzione UPDATE viene utilizzata per modificare i record esistenti in una tabella. Se la condizione non fosse verificata, l'update non verrà eseguito.

```
UPDATE Clienti
SET Cognome = "Rossi"
WHERE ClienteID = 1;
```

## Cancellazioni: come si eseguono
> L'istruzione DELETE viene utilizzata per eliminare i record esistenti in una tabella. Se la condizione non fosse verificata, il delete non verrà eseguito.

```
DELETE FROM Clienti
WHERE ClienteID = 1;
```

## Gestione delle date

>  DATE - format YYYY-MM-DD; DATETIME - format: YYYY-MM-DD HH:mm:SS

## Tips
- [x] il ; alla fine dei vari statements non è obbligatorio; tuttavia, è necessario in caso di più istruzioni (statements) eseguite insieme;

##  Q&A
- [x] conosci MySQL? Sì/no, ma conosco (anche) SQLServer, DB2, ecc;
- [x] Qual è la differenza tra un database relazione e non? In un caso, rappresento i miei dati tramite tabelle formate da tuple e che hanno relazioni tra loro; in un altro caso, ho un formato di rappresentazione di dati più simile a Json.

> Per approfondire: https://www.w3schools.com/sql/default.asp

