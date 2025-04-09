.. note::

    Ciao, benvenuto nella Comunità degli appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Tipi di Dati
===============

Tipi di Dati Integrati
------------------------
MicroPython dispone dei seguenti tipi di dati:

* Tipo di Testo: str
* Tipi Numerici: int, float, complex
* Tipi di Sequenza: list, tuple, range
* Tipo di Mappatura: dict
* Tipi di Insieme: set, frozenset
* Tipo Booleano: bool
* Tipi Binari: bytes, bytearray, memoryview

Ottenere il Tipo di Dato
----------------------------
Puoi ottenere il tipo di dato di qualsiasi oggetto utilizzando la funzione ``type()``:



.. code-block:: python

    a = 6.8
    print(type(a))

>>> %Run -c $EDITOR_CONTENT
<class 'float'>

Impostare il Tipo di Dato
-----------------------------
MicroPython non necessita di impostare specificamente il tipo di dato, questo viene determinato quando assegni un valore alla variabile.



.. code-block:: python

    x = "welcome"
    y = 45
    z = ["apple", "banana", "cherry"]

    print(type(x))
    print(type(y))
    print(type(z))

>>> %Run -c $EDITOR_CONTENT
<class 'str'>
<class 'int'>
<class 'list'>
>>> 

Impostare il Tipo di Dato Specifico
--------------------------------------

Se vuoi specificare il tipo di dato, puoi usare le seguenti funzioni costruttrici:

.. list-table:: 
    :widths: 25 10
    :header-rows: 1

    *   - Esempio
        - Tipo di Dato
    *   - x = int(20)
        - int
    *   - x = float(20.5)
        - float
    *   - x = complex(1j)
        - complex
    *   - x = str("Hello World")
        - str
    *   - x = list(("apple", "banana", "cherry"))
        - list
    *   - x = tuple(("apple", "banana", "cherry"))
        - tuple
    *   - x = range(6)
        - range
    *   - x = dict(name="John", age=36)
        - dict
    *   - x = set(("apple", "banana", "cherry"))
        - set
    *   - x = frozenset(("apple", "banana", "cherry"))
        - frozenset
    *   - x = bool(5)
        - bool
    *   - x = bytes(5)
        - bytes
    *   - x = bytearray(5)
        - bytearray
    *   - x = memoryview(bytes(5))
        - memoryview

Puoi stamparne alcuni per vedere il risultato.



.. code-block:: python

    a = float(20.5)
    b = list(("apple", "banana", "cherry"))
    c = bool(5)

    print(a)
    print(b)
    print(c)

>>> %Run -c $EDITOR_CONTENT
20.5
['apple', 'banana', 'cherry']
True
>>> 

Conversione di Tipo
-------------------------
Puoi convertire da un tipo all'altro con i metodi int(), float() e complex():
La conversione in python viene quindi eseguita utilizzando funzioni costruttrici:

* int() - costruisce un numero intero da un letterale intero, un letterale float (rimuovendo tutti i decimali) o un letterale stringa (a condizione che la stringa rappresenti un numero intero)
* float() - costruisce un numero float da un letterale intero, un letterale float o un letterale stringa (a condizione che la stringa rappresenti un float o un intero)
* str() - costruisce una stringa da una vasta varietà di tipi di dati, inclusi stringhe, letterali interi e letterali float



.. code-block:: python

    a = float("5")
    b = int(3.7)
    c = str(6.0)

    print(a)
    print(b)
    print(c)

Nota: Non puoi convertire numeri complessi in un altro tipo di numero.