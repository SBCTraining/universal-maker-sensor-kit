.. note::
    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per arricchire le tue competenze.
    - **Anteprime Esclusive**: Ottieni un accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Variabili
=============
Le variabili sono contenitori utilizzati per memorizzare i valori dei dati.

Creare una variabile è molto semplice. Devi solo nominarla e assegnarle un valore. Non è necessario specificare il tipo di dato della variabile quando la si assegna, poiché la variabile è un riferimento e accede agli oggetti di diversi tipi di dati tramite assegnazione.

Le regole per la denominazione delle variabili devono seguire le seguenti regole:

* I nomi delle variabili possono contenere solo numeri, lettere e trattini bassi
* Il primo carattere del nome della variabile deve essere una lettera o un trattino basso
* I nomi delle variabili sono sensibili al maiuscolo e minuscolo

Creare una Variabile
----------------------
Non esiste un comando per dichiarare variabili in MicroPython. Le variabili vengono create quando assegni un valore per la prima volta. Non è necessario utilizzare una dichiarazione di tipo specifico e puoi persino cambiare il tipo dopo aver impostato la variabile.



.. code-block:: python

    x = 8       # x è di tipo int
    x = "lily"  # x ora è di tipo str
    print(x)

>>> %Run -c $EDITOR_CONTENT
lily


Casting
-------------
Se vuoi specificare il tipo di dato per la variabile, puoi farlo tramite il casting.



.. code-block:: python

    x = int(5)    # y sarà 5
    y = str(5)    # x sarà '5'
    z = float(5)  # z sarà 5.0
    print(x,y,z)

>>> %Run -c $EDITOR_CONTENT
5 5 5.0

Ottieni il Tipo
-------------------
Puoi ottenere il tipo di dato di una variabile con la funzione `type()`.



.. code-block:: python

    x = 5
    y = "hello"
    z = 5.0
    print(type(x),type(y),type(z))

>>> %Run -c $EDITOR_CONTENT
<class 'int'> <class 'str'> <class 'float'>

Virgolette Singole o Doppie?
-------------------------------

In MicroPython, puoi usare virgolette singole o doppie per definire variabili stringa.



.. code-block:: python

    x = "hello"
    # è lo stesso di
    x = 'hello'

Sensibile alle Maiuscole
---------------------------------
I nomi delle variabili sono sensibili al caso.



.. code-block:: python

    a = 5
    A = "lily"
    #A non sovrascriverà a
    print(a, A)

>>> %Run -c $EDITOR_CONTENT
5 lily


