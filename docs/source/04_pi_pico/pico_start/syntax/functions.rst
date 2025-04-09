.. note::

    Ciao, benvenuto nella Comunità degli appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci la tua conoscenza di Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Funzioni
==============

In MicroPython, una funzione è un gruppo di istruzioni correlate che eseguono un compito specifico.

Le funzioni aiutano a suddividere il nostro programma in blocchi modulari più piccoli. Man mano che il nostro programma cresce, le funzioni lo rendono più organizzato e gestibile.

Inoltre, evitano la duplicazione e rendono il codice riutilizzabile.

Creare una Funzione
----------------------

.. code-block::

    def function_name(parameters): 
        """docstring"""
        statement(s)

* Una funzione viene definita utilizzando la parola chiave ``def``

* Un nome di funzione per identificare univocamente la funzione. La denominazione della funzione segue le stesse regole della denominazione delle variabili:
    
   * Può contenere solo numeri, lettere e underscore.
   * Il primo carattere deve essere una lettera o un underscore.
   * È case sensitive.

* Parametri (argomenti) attraverso i quali passiamo valori alla funzione. Sono opzionali.

* I due punti (:) segnano la fine dell'intestazione della funzione.

* Docstring opzionale, utilizzato per descrivere la funzione della funzione, solitamente usiamo le triple virgolette in modo che il docstring possa essere espanso su più righe.

* Una o più istruzioni MicroPython valide che compongono il corpo della funzione. Le istruzioni devono avere lo stesso livello di indentazione (solitamente 4 spazi).

* Ogni funzione necessita di almeno un'istruzione, ma se per qualche motivo c'è una funzione che non contiene alcuna istruzione, inserisci l'istruzione pass per evitare errori.

* Un'istruzione ``return`` opzionale per restituire un valore dalla funzione.


Chiamare una Funzione
---------------------------

Per chiamare una funzione, aggiungi le parentesi dopo il nome della funzione.



.. code-block:: python

    def my_function():
        print("Your first function")

    my_function()

>>> %Run -c $EDITOR_CONTENT
Your first function

L'istruzione return
-----------------------

L'istruzione return viene utilizzata per uscire da una funzione e tornare al punto in cui è stata chiamata.

**Sintassi di return**

.. code-block:: python

    return [expression_list]

L'istruzione può contenere un'espressione che viene valutata e restituisce un valore. Se non c'è un'espressione nell'istruzione, o l'istruzione ``return`` stessa non esiste nella funzione, la funzione restituirà un oggetto ``None``.



.. code-block:: python

    def my_function():
            print("Your first function")

    print(my_function())

>>> %Run -c $EDITOR_CONTENT
Your first function
None

Qui, ``None`` è il valore di ritorno, perché l'istruzione ``return`` non viene utilizzata.

Argomenti
-------------

Le informazioni possono essere passate alla funzione come argomenti.

Specifica gli argomenti tra parentesi dopo il nome della funzione. Puoi aggiungere quanti argomenti vuoi, separandoli con virgole.



.. code-block:: python

    def welcome(name, msg):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)

    welcome("Lily", "Welcome to China!")

>>> %Run -c $EDITOR_CONTENT
Hello Lily, Welcome to China!


Numero di Argomenti
*************************

Per impostazione predefinita, una funzione deve essere chiamata con il numero corretto di argomenti. Ciò significa che se la tua funzione si aspetta 2 parametri, devi chiamare la funzione con 2 argomenti, né più né meno.



.. code-block:: python

    def welcome(name, msg):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)

    welcome("Lily", "Welcome to China!")

Qui, la funzione welcome() ha 2 parametri.

Poiché abbiamo chiamato questa funzione con due argomenti, la funzione funziona senza problemi e senza errori.

Se viene chiamata con un numero diverso di argomenti, l'interprete mostrerà un messaggio di errore.

Di seguito è riportata la chiamata a questa funzione, che contiene uno e nessun argomento e i rispettivi messaggi di errore.

.. code-block::

    welcome("Lily")＃Only one argument

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
TypeError: function takes 2 positional arguments but 1 were given

.. code-block::

    welcome()＃No arguments

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
TypeError: function takes 2 positional arguments but 0 were given


Argomenti Predefiniti
*************************

In MicroPython, possiamo utilizzare l'operatore di assegnazione (=) per fornire un valore predefinito per il parametro.

Se chiamiamo la funzione senza argomento, utilizza il valore predefinito.



.. code-block:: python

    def welcome(name, msg = "Welcome to China!"):
        """This is a welcome function for
        the person with the provided message"""
        print("Hello", name + ', ' + msg)
    welcome("Lily")

>>> %Run -c $EDITOR_CONTENT
Hello Lily, Welcome to China!

In questa funzione, il parametro ``name`` non ha un valore predefinito ed è richiesto (obbligatorio) durante la chiamata.

D'altra parte, il valore predefinito del parametro ``msg`` è "Benvenuta in Cina!". Pertanto, è opzionale durante la chiamata. Se viene fornito un valore, sovrascriverà il valore predefinito.

Qualsiasi numero di argomenti nella funzione può avere un valore predefinito. Tuttavia, una volta che c'è un argomento predefinito, tutti gli argomenti alla sua destra devono anche avere valori predefiniti.

Ciò significa che gli argomenti non predefiniti non possono seguire argomenti predefiniti. 

Ad esempio, se definiamo l'intestazione della funzione sopra come:

.. code-block:: python

    def welcome(name = "Lily", msg):

Riceveremo il seguente messaggio di errore:

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
SyntaxError: non-default argument follows default argument


Argomenti Parola Chiave
**************************

Quando chiamiamo una funzione con determinati valori, questi valori vengono assegnati agli argomenti in base alla loro posizione.

Ad esempio, nella funzione welcome() sopra, quando l'abbiamo chiamata come welcome("Lily", "Benvenuta in Cina"), il valore "Lily" viene assegnato al parametro ``name`` e allo stesso modo "Benvenuta in Cina" al parametro ``msg``.

MicroPython consente di chiamare funzioni con argomenti parola chiave. Quando chiamiamo la funzione in questo modo, l'ordine (posizione) degli argomenti può essere cambiato. 

.. code-block:: python

    # argomenti parola chiave
    welcome(name = "Lily",msg = "Welcome to China!")

    # argomenti parola chiave (fuori ordine)
    welcome(msg = "Welcome to China！",name = "Lily") 

    #1 argomento posizionale, 1 argomento parola chiave
    welcome("Lily", msg = "Welcome to China!")

Come possiamo vedere, possiamo mescolare argomenti posizionali e argomenti parola chiave durante le chiamate di funzione. Ma dobbiamo ricordare che gli argomenti parola chiave devono seguire gli argomenti posizionali.

Avere un argomento posizionale dopo un argomento parola chiave risulterà in un errore. 

Ad esempio, se la chiamata alla funzione come segue:

.. code-block:: python

    welcome(name="Lily","Welcome to China!")

Risulterà in un errore:

>>> %Run -c $EDITOR_CONTENT
Traceback (most recent call last):
  File "<stdin>", line 5, in <module>
SyntaxError: non-keyword arg after keyword arg


Argomenti Arbitrari
***********************

A volte, se non sai il numero di argomenti che verranno passati alla funzione in anticipo. 

Nella definizione della funzione, possiamo aggiungere un asterisco (*) davanti al nome del parametro.



.. code-block:: python

    def welcome(*names):
        """This function welcomes all the person
        in the name tuple"""
        #names è una tuple con argomenti
        for name in names:
            print("Welcome to China!", name)
            
    welcome("Lily","John","Wendy")

>>> %Run -c $EDITOR_CONTENT
Welcome to China! Lily
Welcome to China! John
Welcome to China! Wendy

Qui, abbiamo chiamato la funzione con più argomenti. Questi argomenti sono impacchettati in una tupla prima di essere passati alla funzione. 

All'interno della funzione, utilizziamo un ciclo for per recuperare tutti gli argomenti.

Ricorsione
----------------
In Python, sappiamo che una funzione può chiamare altre funzioni. È anche possibile che la funzione si chiami da sola. Questi tipi di costrutti sono denominati funzioni ricorsive.

Questo ha il vantaggio di significare che puoi ciclare attraverso i dati per raggiungere un risultato.

Lo sviluppatore deve essere molto attento con la ricorsione in quanto può essere abbastanza facile scivolare nella scrittura di una funzione che non termina mai, o che usa quantità eccessive di memoria o potenza del processore. Tuttavia, quando scritta correttamente la ricorsione può essere un approccio molto efficiente ed elegante dal punto di vista matematico alla programmazione.



.. code-block:: python

    def rec_func(i):
        if(i > 0):
            result = i + rec_func(i - 1)
            print(result)
        else:
            result = 0
        return result

    rec_func(6)

>>> %Run -c $EDITOR_CONTENT
1
3
6
10
15
21

In questo esempio, rec_func() è una funzione che abbiamo definito per chiamare se stessa ("ricorsione"). Utilizziamo la variabile ``i`` come dati, e si decrementerà (-1) ogni volta che ricorriamo. Quando la condizione non è maggiore di 0 (cioè 0), la ricorsione termina.

Per i nuovi sviluppatori, potrebbe essere necessario del tempo per determinare come funziona, e il modo migliore per testarlo è provarlo e modificarlo.

**Vantaggi della Ricorsione**

* Le funzioni ricorsive rendono il codice pulito ed elegante.
* Un compito complesso può essere suddiviso in sottoproblemi più semplici usando la ricorsione.
* La generazione di sequenze è più facile con la ricorsione che utilizzando alcune iterazioni annidate.

**Svantaggi della Ricorsione**

* A volte la logica dietro la ricorsione è difficile da seguire.
* Le chiamate ricorsive sono costose (inefficienti) poiché richiedono molto tempo e memoria.
* Le funzioni ricorsive sono difficili da debuggare.
