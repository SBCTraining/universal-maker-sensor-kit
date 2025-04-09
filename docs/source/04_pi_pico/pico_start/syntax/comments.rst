.. note::

    Ciao, benvenuto nella Comunità degli appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Commenti
=============

I commenti nel codice ci aiutano a comprendere il codice stesso, rendono l'intero codice più leggibile e commentano una parte del codice durante i test, in modo tale che questa parte di codice non venga eseguita.

Commento su una singola riga
--------------------------------

I commenti su una singola riga in MicroPython iniziano con #, e il testo seguente è considerato un commento fino alla fine della riga. I commenti possono essere posizionati prima o dopo il codice.

.. code-block:: python

    print("hello world") #This is a annotationhello world

>>> %Run -c $EDITOR_CONTENT
hello world

I commenti non sono necessariamente testi utilizzati per spiegare il codice. Puoi anche commentare una parte del codice per impedire a MicroPython di eseguire il codice.


.. code-block:: python

    #print("Non può essere eseguito!")
    print("hello world") # Questa è un'annotazione

>>> %Run -c $EDITOR_CONTENT
hello world

Commento su più righe
------------------------------

Se desideri commentare su più righe, puoi usare più segni #.

.. code-block:: python

    # Questo è un commento
    # scritto su
    # più di una sola riga
    print("Hello, World!")

>>> %Run -c $EDITOR_CONTENT
Hello, World!

Oppure, puoi utilizzare stringhe su più righe al posto delle attese.

Poiché MicroPython ignora le stringhe letterali che non sono assegnate a variabili, puoi aggiungere più righe di stringhe (triple virgolette) al codice e inserire commenti in esse:

.. code-block:: python

    """
    This is a comment
    written in
    more than just one line
    """
    print("Hello, World!")

>>> %Run -c $EDITOR_CONTENT
Hello, World!

Finché la stringa non è assegnata a una variabile, MicroPython la ignorerà dopo aver letto il codice e la tratterà come se avessi fatto un commento su più righe.
