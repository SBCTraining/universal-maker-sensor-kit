.. note::

    Ciao, benvenuto nella Comunità degli appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Indentazione
==============

L'indentazione si riferisce agli spazi all'inizio di una linea di codice.
Come i programmi Python standard, anche i programmi MicroPython vengono solitamente eseguiti dall'alto verso il basso:
Il programma attraversa ogni riga in successione, la esegue nell'interprete e poi passa alla riga successiva,
proprio come se le digitassi una per una nella Shell.
Un programma che semplicemente sfoglia l'elenco delle istruzioni riga per riga non è molto intelligente, quindi MicroPython, proprio come Python, ha il suo metodo per controllare la sequenza di esecuzione del suo programma: l'indentazione.

Devi inserire almeno uno spazio prima di print(), altrimenti apparirà un messaggio di errore "Sintassi non valida". Si raccomanda di solito di standardizzare gli spazi premendo uniformemente il tasto Tab.



.. code-block:: python

    if 8 > 5:
    print("Eight is greater than Five!")

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 2
SyntaxError: sintassi non valida

Devi usare lo stesso numero di spazi nello stesso blocco di codice, altrimenti Python ti darà un errore.


.. code-block:: python

    if 8 > 5:
    print("Eight is greater than Five!")
            print("Eight is greater than Five")
            
>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 2
SyntaxError: invalid syntax
