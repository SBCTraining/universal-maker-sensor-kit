.. note:: 

    Ciao, benvenuto nella community SunFounder su Facebook dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci la tua esperienza con Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima annunci sui nuovi prodotti e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di offerte esclusive sui nostri ultimi prodotti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

Struttura di un Programma Arduino
====================================

Diamo un’occhiata al nuovo file sketch. Anche se ha solo poche righe di codice, si tratta in realtà di uno sketch “vuoto”.
Caricare questo sketch sulla scheda di sviluppo non produrrà alcun effetto.

.. code-block:: C

    void setup() {
    // inserisci qui il tuo codice di configurazione, viene eseguito una sola volta:

    }

    void loop() {
    // inserisci qui il codice principale, verrà eseguito in loop:

    }

Se rimuoviamo ``setup()`` e ``loop()`` e rendiamo davvero lo sketch un file ``vuoto``, noterai che non supera la verifica.
Essi rappresentano l’equivalente dello scheletro umano: sono indispensabili.

Durante l’esecuzione dello sketch, ``setup()`` viene eseguito per primo e il codice al suo interno (tra le parentesi graffe ``{}``) viene eseguito una sola volta all’avvio o al reset della scheda.
``loop()``, invece, è utilizzato per scrivere la logica principale del programma e il suo contenuto viene eseguito continuamente dopo ``setup()``.

Per comprendere meglio ``setup()`` e ``loop()``, vediamo quattro sketch il cui obiettivo è far lampeggiare il LED integrato sulla scheda Arduino. Esegui ogni esperimento e osserva gli effetti.

* Sketch 1: Fa lampeggiare continuamente il LED integrato.

.. code-block:: C
    :emphasize-lines: 8,9,10,11

    void setup() {
        // codice di configurazione, eseguito una volta sola:
        pinMode(13,OUTPUT); 
    }

    void loop() {
        // codice principale, eseguito continuamente:
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

* Sketch 2: Fa lampeggiare il LED integrato una sola volta.

.. code-block:: C
    :emphasize-lines: 4,5,6,7

    void setup() {
        // codice di configurazione, eseguito una volta sola:
        pinMode(13,OUTPUT);
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

    void loop() {
        // codice principale, eseguito continuamente:
    }

* Sketch 3: Fa lampeggiare lentamente il LED una volta, poi lampeggia velocemente.

.. code-block:: C
    :emphasize-lines: 4,5,6,7,12,13,14,15

    void setup() {
        // codice di configurazione, eseguito una volta sola:
        pinMode(13,OUTPUT);
        digitalWrite(13,HIGH);
        delay(1000);
        digitalWrite(13,LOW);
        delay(1000);
    }

    void loop() {
        // codice principale, eseguito continuamente:
        digitalWrite(13,HIGH);
        delay(200);
        digitalWrite(13,LOW);
        delay(200);
    }    

* Sketch 4: Genera un errore.

.. code-block:: C
    :emphasize-lines: 6,7,8,9

    void setup() {
        // codice di configurazione, eseguito una volta sola:
        pinMode(13,OUTPUT);
    }

    digitalWrite(13,HIGH);
    delay(1000);
    digitalWrite(13,LOW);
    delay(1000);

    void loop() {
        // codice principale, eseguito continuamente:
    }    

Grazie a questi sketch possiamo riassumere alcune caratteristiche fondamentali di ``setup-loop``:

* ``loop()`` viene eseguito ripetutamente dopo l’accensione della scheda.
* ``setup()`` viene eseguito solo una volta all’accensione o al reset della scheda.
* Dopo l’avvio, ``setup()`` viene eseguito per primo, seguito da ``loop()``.
* Il codice deve essere scritto all’interno delle parentesi graffe ``{}`` di ``setup()`` o ``loop()``; al di fuori di esse, verrà generato un errore.

.. note::  
    I comandi come ``digitalWrite(13,HIGH)`` servono a controllare il LED integrato. Spiegheremo il loro utilizzo in dettaglio nei capitoli successivi.


