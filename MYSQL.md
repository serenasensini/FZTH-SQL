# MYSQL cheatsheet

## Istruzione: SELECT FROM
Sintassi:
```
SELECT *
FROM tabella
```

_Esempio_: Selezionare tutti gli utenti dalla tabella "Utente"
```
SELECT *
FROM UTENTE
```

## Istruzione: WHERE
Sintassi:
```
SELECT *
FROM tabella
WHERE condizione1=valore1
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente" che abbiano cognome "Rossi"
```
SELECT *
FROM UTENTE
WHERE cognome="Rossi"
```

## Funzione: AVG, SUM, COUNT, MAX, MIN
Sintassi:
```
SELECT MIN(campo)
FROM tabella
```
Esempio: Selezionare l'età minore a tutti gli altri dalla tabella "Utente"
```
SELECT MIN(eta)
FROM UTENTE
```
Nota: le altre funzioni si usano in maniera analoga; MAX calcola il massimo, AVG calcola la media, SUM la somma, COUNT conta i record.

## Istruzione: GROUP BY
Sintassi:
```
SELECT *
FROM tabella
```
Esempio: Contare tutti gli utenti dalla tabella "Utente" raggruppati per nazione
```
SELECT COUNT(UtenteID), Nazione
FROM Utente
GROUP BY Nazione;
```

## Istruzione: HAVING
Sintassi:
```
SELECT *
FROM tabella
HAVING condizione1=valore1
```
Esempio: Contare tutti gli utenti dalla tabella "Utente", raggruppando per nazioni, con la condizione che il conteggio degli utenti raggruppati sia maggiore o uguale di 100.
```
SELECT COUNT(UtenteID), Nazione
FROM Utente
GROUP BY Nazione
HAVING COUNT(UtenteID) >= 100;
```

## Istruzione: EXISTS
Sintassi:
```
SELECT *
FROM tabella
WHERE EXISTS condizione1=valore1
```
Esempio: Selezionare il PIL dalla tabella "Nazione" se la subquery è verificata, ovvero se il conteggio degli utenti raggruppato per nazione sia maggiore o uguale a 100.
```
SELECT PIL
FROM Nazione
WHERE EXISTS (SELECT COUNT(UtenteID), Nazione
    FROM Utente
    GROUP BY Nazione
    HAVING COUNT(UtenteID) >= 100);
```

## Istruzione: ORDER BY
Sintassi:
```
SELECT *
FROM tabella
ORDER BY campo
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente" ordinati alfabeticamente tramite il nome.
```
SELECT *
FROM UTENTE
ORDER BY Nome
```
Nota: di default, l'ordinamento è ascendente (basso verso alto); se si volesse ottenere l'ordinamento decrescente, basta aggiungere DESC come nell'esempio.

## Istruzione: LIKE
Sintassi:
```
SELECT *
FROM tabella
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente" che hanno un nome che comincia per la "A" e finisce per "A".
```
SELECT *
FROM UTENTE
WHERE nome LIKE "A%A"
```
Nota: il carattere "%" rappresenta un numero indefinito di caratteri, compreso lo zero; volendo inserire una sola occorrenza di un carattere qualsiasi, basta usare il simbolo "\_".

## Istruzione: BETWEEN
Sintassi:
```
SELECT *
FROM tabella
WHERE campo BETWEEN valore1 AND valore2
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente" che hanno età compresa tra 18 e 24 anni.
```
SELECT *
FROM UTENTE
WHERE eta BETWEEN 18 AND 24
```

## Istruzione: AS
Sintassi:
```
SELECT campo AS alias
FROM tabella
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente" e mostrare il nome del campo "cognome" come "COG"
```
SELECT cognome as COG
FROM UTENTE
```

## Istruzione: LIMIT
Sintassi:
```
SELECT *
FROM tabella
LIMIT numero
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente", limitando i risultati a 10
```
SELECT *
FROM UTENTE
LIMIT 10
```

## Istruzione: DISTINCT
Sintassi:
```
SELECT DISTINCT campo
FROM tabella
```
Esempio: Selezionare tutti i nomi dalla tabella "Utente" senza duplicati
```
SELECT DISTINCT nome
FROM UTENTE
```
## Istruzione: PRIMARY KEY
### Cos'è
Una chiave primaria viene utilizzata solo per individuare ogni riga presente in una tabella. Essa può far parte dello stesso record corrente oppure essere un campo artificiale e non avere niente a che fare con il record corrente. Una chiave primaria può consistere di uno o più campi presenti in una tabella. Quando vengono utilizzati più campi come chiave primaria, viene assegnato loro il nome di chiave composta.
Le chiavi primarie possono essere specificate durante la creazione della tabella.

Sintassi:
```
CREATE TABLE CLIENTE(
  CLIENTE_ID integer,
  COGNOME varchar(30),
  NOME varchar(30),
  PRIMARY KEY (CLIENTE_ID));
```

## Relazione
### Cos'è
Una relazione è un legame logico che permette di aggregare informazioni tra una o più tabelle. Per esempio, i clienti effettuano gli ordini, e gli ordini contengono elementi.
Esistono diversi tipi di relazioni di database, ovvero:
- Uno a Uno: per esempio, ad un cliente della tabella CLIENTE è associato uno ed un solo indirizzo della tabella INDIRIZZO;
- Uno a N: per esempio, ad un cliente della tabella CLIENTE sono associati N ordini nella tabella ORDINE;
- N a N: per esempio, ad n ordini della tabella ORDINE possono essere associati N prodotti della tabella PRODOTTO, così come a N prodotti possono essere associati N ordini della tabella ORDINE;
- N a Uno: per esempio, ad N ordini della tabella ORDINE è associato uno ed un solo cliente della tabella CLIENTE.

(cfr. [Tutplus](https://code.tutsplus.com/it/articles/sql-for-beginners-part-3-database-relationships--net-8561))

## Istruzione: FOREIGN KEY
### Cos'è
Una chiave esterna rappresenta uno o più campi che fanno riferimento alla chiave primaria di un’altra tabella. Lo scopo della chiave esterna è garantire l’integrità referenziale dei dati. Cioè, sono consentiti solo i valori che si ritiene debbano apparire nel database.

Ad esempio, si supponga di avere di due tabelle: una tabella CLIENTE e una tabella ORDINE; ogni ordine dev'essere associato ad un cliente e quindi sarà necessario usare una chiave esterna sulla tabella degli ordini che sia in relazione con la chiave primaria della tabella dei clienti, come nell'esempio seguente. Così facendo, è possibile garantire che tutti gli ordini della tabella siano correlati a un cliente presente nella tabella dei clienti, e che quindi non sia possibile avere un ordine senza un cliente.

Sintassi:
```
CREATE TABLE ORDINE(
  ID_ORDINE integer,
  DATA date,
  ID_CLIENTE integer,
  PRIMARY KEY (ID_ORDINE),
  FOREIGN KEY (ID_CLIENTE) REFERENCES CLIENTE (ID_CLIENTE));
```

## Istruzione: JOIN
### Cos'è
Il JOIN è una clausola del linguaggio SQL che serve a combinare le tuple di due o più relazioni di un base di dati. Lo standard ANSI definisce alcune specifiche per il linguaggio SQL sul tipo di JOIN da effettuare: INNER, FULL, LEFT e RIGHT, alle quali diversi DBMS aggiungono CROSS. In alcuni casi è possibile che una tabella possa essere combinata con se stessa, in questo caso si parlerà di self-join. In ordine:
- OUTER-JOIN:  La tabella risultante da una outer join trattiene tutti quei record che non hanno alcuna corrispondenza tra le tabelle;
- LEFT-JOIN: il risultato di una query left outer join (o semplicemente left join) per le tabelle contiene sempre tutti i record della tabella di sinistra ("left"), mentre vengono estratti dalla tabella di destra ("right") solamente le righe che trovano corrispondenza nella regola di confronto della join;
- RIGHT-JOIN: il risultato di una query right outer join per le tabelle contiene sempre tutti i record della tabella di destra ("right"), mentre vengono estratti dalla tabella di sinistra ("left") solamente le righe che trovano corrispondenza nella regola di confronto della join;
- INNER-JOIN: questo tipo di clausola cerca di soddisfare la condizione in entrambe le tabelle, quindi confronta ogni riga della tabella a sinistra della join con ogni riga della tabella a destra; se la condizione è soddisfatta, allora la riga è aggiunta al risultato della query.

(cfr. [Wikipedia](https://it.wikipedia.org/wiki/Join_(SQL)))

Sintassi:
```
SELECT *
FROM tabella1 JOIN tabella2
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente", limitando i risultati a 10
```
SELECT *
FROM PRODOTTO LEFT JOIN UTENTE ON ID_PRODOTTO=ID_ACQUISTO
```
Nota: le clausole presenti nella ON sono valutate ANTERIORMENTE all'esecuzione del join mentre le clausole nella where sono valutate SUCCESSIVAMENTE all'esecuzione del join; per questa ragione, è buona pratica inserire la condizione di uguaglianza (come quella tra due chiavi) tra le tabelle nella clausola ON.

## Procedura: CREATE
Sintassi:
```
CREATE PROCEDURE nome()
  BEGIN
  istruzioni SQL
  END
```
Esempio: Selezionare tutti i record dalla tabella "Utente"
```
CREATE PROCEDURE GetAllUsers()
  BEGIN
    SELECT *
    FROM UTENTE
  END
```

## Procedura: PARAMETRI
Sintassi:
```
CREATE PROCEDURE nome(IN param1 tipo, OUT param2)
  BEGIN
  istruzioni SQL
  END
```
Esempio: Selezionare tutti i prodotti con il nome "n" passato come parametro
```
CREATE PROCEDURE GetProductsByName(IN n VARCHAR(30))
 BEGIN
  SELECT *
  FROM PRODOTTO
  WHERE nome = n
 END;

CALL GetProductsByName('Pane');
```
oppure:
```
CREATE PROCEDURE CountUsersByName(IN n VARCHAR(25),
 OUT totale INT)
BEGIN
 SELECT COUNT(*)
 INTO totale
 FROM UTENTE
 WHERE nome = n
 END;

CALL CountUsersByName('Cioccolata',@totale);
SELECT @totale;
 ```

## Procedura: CALL
Sintassi:
```
CALL nome()
```
Esempio: Richiamo la stored procedure dell'esempio precedente
```
CALL GetAllUsers();
```

## Funzione: CREATE
Sintassi:
```
CREATE FUNCTION nome (param1, param2, ecc)
    ISTRUZIONI SQL
SELECT nome();
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente"
```
CREATE FUNCTION hello (s CHAR(20))
    RETURN CHAR(50) DETERMINISTIC
    RETURN CONCAT('Hello, ',s,'!');
SELECT hello('world');
```

## Vista: CREATE
### Cos'è
Una vista è rappresentata da una query, il cui risultato può essere utilizzato come se fosse una tabella, anche se in questo caso si ha una tabella virtuale e non fisica. Le viste generalmente vengono utilizzate per semplificare le query. Se il database è realmente relazionale, leggere un insieme di dati avente un significato potrebbe essere complesso, perché potrebbe richiedere eccessive JOIN fra tabelle; con una vista è possibile semplificare molto la stesura di query che leggono le informazioni. (cfr. [Wikipedia](https://it.wikipedia.org/wiki/Vista_(basi_di_dati)))

Sintassi:
```
CREATE VIEW nome AS
  SELECT *
  FROM tabella
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente"
```
CREATE VIEW ProductsByUsers AS
  SELECT *
  FROM PRODOTTO LEFT JOIN UTENTE ON ID_PRODOTTO = PRODOTTO
```

## Vista: uso
Sintassi:
```
SELECT *
FROM vista
```
Esempio: Selezionare tutti gli utenti dalla tabella "Utente" tramite la vista precedentemente creata
```
SELECT *
FROM ProductsByUsers
```

## Tips:
- Stored procedure: [esempi](http://www.mysqltutorial.org/mysql-stored-procedure-tutorial.aspx)
- Funzioni: [esempi](http://www.mysqltutorial.org/mysql-functions.aspx)
