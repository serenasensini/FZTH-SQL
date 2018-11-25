# Ajax
Asynchronous JavaScript and XML.

## Cos'è [?](https://it.wikipedia.org/wiki/AJAX)

AJAX non è un linguaggio di programmazione, ma una tecnica di sviluppo software. AJAX utilizza solo una combinazione di:
- Un oggetto XMLHttpRequest incorporato nel browser (per richiedere dati da un server Web);
- DOM JavaScript e HTML (per visualizzare o utilizzare i dati)
E' normale trasportare i dati come testo normale, come XML o testo JSON.

AJAX consente di aggiornare le pagine Web in modo asincrono scambiando dati con un server Web dietro le quinte. Ciò significa che è possibile aggiornare parti di una pagina Web senza ricaricare l'intera pagina.

AJAX rappresenta il sogno di ogni sviluppatore, perché permette di:
- Aggiornare una pagina Web senza doverla ricaricare;
- Richiedere dati da un server, anche dopo che la pagina è stata caricata;
- Ricevere dati da un server, anche dopo che la pagina è stata caricata;
- Invia dati a un server di nascosto, senza dover cambiare pagina.

## Come funziona
Usato in combinazione con JQuery, permette di effettuare richieste lato server per ottenere/validare/salvare dati. A questo [link](https://www.w3schools.com/jquery/ajax_ajax.asp) sono disponibili tutti i parametri che è possibile utilizzare all'interno di una chiamata Ajax. Qui sotto uno schema di come funziona una chiamata con Ajax:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--xgVyrrP4--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/azyz8o8wd62fn84zhxsk.gif)

Esempio:

```
//al click del bottone 'button'...
$("button").click(function(){
  //richiamo un oggetto ajax...
    $.ajax({
    //...che richiama il metodo back-end "check_insert" e...
    url: "check_insert", 
    //...in caso di successo, colora di verde il 'div1'
    success: function(result){
        $("#div1").css('green');
    },
    //in caso di insuccesso, di verde, e stampa l'errore
    error: function(xhr){
        $("#div1").css('red');
        console.log(xhr);
    };
    });
});
```
