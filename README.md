# webiste_test
Premetto che non ho mai ricevuto molta formazione in merito alla programmazione, sopratutto sulle basi di SQL e HTML.
Ho effettuato diverse ricerche su internet e ho optato per utilizzare Php e un database MySQL, nonostante non lo avessi mai visto o utilizzato prima.
Tutto ciò che ho fatto è frutto di impegno e ragionamenti, cercando parti codice su internet e adattandolo alle mie esigenze. Anche se ammetto di non essere stato in grado di completare tutte le richieste in quanto non ne sono ancora capace ma mi piacerebbe imparare perché la sfida mi intriga molto

Nella homepage abbiamo due textbox che ci permettono di filtrare per descrizione dell'articolo che vogliamo acquistare e inserire la quantità desiderata.

Cliccando sul pulsante "Submit" viene effettuato il controllo nella tabella "magazzino" del database per vedere quali fornitori dispongono di unità sufficienti per soddisfare la richiesta.
Con il comando while(($product = mysqli_fetch_assoc($featured))): vengono estratte come array le righe della query eseguita a inizio pagina:
SELECT * 
	FROM magazzino AS A 
	INNER JOIN articolo AS B ON A.CodArt = B.id 
	INNER JOIN fornitore AS C ON A.CodFor = C.id
	WHERE Des LIKE'%term%'
    ORDER BY A.CodArt
 (%term verrà sostituito dalla parola cercata in precedenza tramite il comando str_replace)

Una volta caricati i prodotti ci sono una serie di IF che, a seconda della quantità acquistata o dell'importo totale (prezzo unitario * quantità che si desidera acquistare), applicano percentuali di sconto diverse. Inoltre viene indicato anche che tipo di sconto viene applicato.
if (($product["CodFor"] = 1) && ($product["Prezzo"] * $qtaor >= 1000)){
				$price = $product["Prezzo"] * $qtaor * 95 / 100;
				$sconto = "Sconto del 5% per ordini di importo pari o superiore a 1000€";
			}
				else if (($product["CodFor"] = 2) && ($qtaor >= 5) && ($qtaor < 10)) {
					$price = $product["Prezzo"] * $qtaor * 97 / 100;
					$sconto = "Sconto del 5% per ordini pari o superiori a 5 unità";
				}
				else if (($product["CodFor"] = 2) && ($qtaor >= 10)) {
					$price = $product["Prezzo"] * $qtaor * 95 / 100;
					$sconto = "Sconto del 5% per ordini pari o superiori a 10 unità";
				}
				else if (($product["CodFor"] = 3) && ($product["Prezzo"] * $qtaor >= 1000)) {
					$price = $product["Prezzo"] * $qtaor * 95 / 100;
					$sconto = "Sconto del 5% per ordini pari o superiori a 1000€";
						if (date("m") == "09") {
							$price = $price * 98 / 100;
							$sconto = "Sconto del 5% + 2% per ordini pari o superiori a 1000€ effettuati in settembre";
						}
				}
				else {
					$price = $product["Prezzo"];
				    $sconto = "";
				}
I prodotti vengono visualizzati tramite il seguente codice, che va a leggere ogni campo dall'array $product
                                              
Ho tentato anche di evidenziare il fornitore con tempi di consegna minore per ogni prodotto (e di conseguenza poi avrei fatto anche quelli con prezzo minore) ma non sono stato in grado di trovare la soluzione.
Dopo vari tentativi ho deciso di lasciare l'ultimo come commento nella pagina control.php.


