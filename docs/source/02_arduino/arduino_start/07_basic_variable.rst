.. note::

    Ciao e benvenuto nella community Facebook per gli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Esplora a fondo Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e anticipazioni.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni e giveaway durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi!

Variabile
============

La variabile è uno degli strumenti più potenti e fondamentali in un programma. Serve a memorizzare e richiamare dati all'interno del codice.

Il seguente sketch utilizza variabili: memorizza il numero del pin del LED integrato nella variabile ``ledPin`` e il valore "500" nella variabile ``delayTime``.

.. code-block:: C
    :emphasize-lines: 1,2

    int ledPin = 13;
    int delayTime = 500;

    void setup() {
        pinMode(ledPin,OUTPUT); 
    }

    void loop() {
        digitalWrite(ledPin,HIGH); 
        delay(delayTime); 
        digitalWrite(ledPin,LOW); 
        delay(delayTime);
    }

Aspetta, ma non è la stessa cosa che fa ``#define``? La risposta è NO.

* Il ruolo di ``#define`` è semplicemente quello di sostituire del testo, e non viene considerato dal compilatore come parte effettiva del programma.
* Una ``variabile``, invece, esiste nel programma e serve a memorizzare e richiamare valori. Può anche essere modificata durante l’esecuzione, cosa che un define non permette.

Lo sketch qui sotto modifica autonomamente il valore della variabile, facendo lampeggiare il LED integrato per un tempo sempre più lungo a ogni ciclo.

.. code-block:: C

    int ledPin = 13;
    int delayTime = 500;

    void setup() {
        pinMode(ledPin,OUTPUT); 
    }

    void loop() {
        digitalWrite(ledPin,HIGH); 
        delay(delayTime); 
        digitalWrite(ledPin,LOW); 
        delay(delayTime);
        delayTime = delayTime+200; // A ogni ciclo il valore aumenta di 200
    }

Dichiarare una variabile
----------------------------

Dichiarare una variabile significa crearla.

Per dichiararla servono due elementi: il tipo di dato e il nome della variabile. Il tipo di dato va scritto prima del nome e separato da uno spazio, e la dichiarazione deve terminare con ``;``.

Ecco un esempio:

.. code-block:: C

    int delayTime;

**Tipo di dato**

Qui ``int`` è un tipo di dato chiamato intero, utilizzato per memorizzare numeri compresi tra -32768 e 32767. Non può essere usato per memorizzare numeri decimali.

Le variabili possono contenere diversi tipi di dati oltre agli interi. Il linguaggio Arduino (ricorda, è C++) supporta nativamente alcuni tipi tra i più utili e comuni:

* ``float``: memorizza numeri decimali, ad esempio 3.1415926.
* ``byte``: contiene numeri da 0 a 255.
* ``boolean``: contiene solo due valori possibili, ``True`` o ``False``, anche se occupa un byte in memoria.
* ``char``: contiene numeri da -127 a 127. Poiché è dichiarato come ``char``, il compilatore tenterà di associarlo a un carattere secondo la |link_ascii|.
* ``string``: memorizza una sequenza di caratteri, ad esempio ``Halloween``.



**Nome della variabile**


Puoi assegnare qualsiasi nome alla variabile, ad esempio ``i``, ``apple``, ``Bruce``, ``R2D2``, ``Sectumsempra``, ma ci sono alcune regole da rispettare:

1. Descrivi il suo scopo. In questo esempio ho chiamato la variabile ``delayTime``, così è chiaro a cosa serve. Funzionerebbe anche se la chiamassi ``barryAllen``, ma chi legge il codice si confonderebbe.

2. Usa una convenzione coerente. Puoi usare CamelCase, come in ``delayTime``, dove la T maiuscola aiuta a distinguere le parole. Oppure puoi usare lo stile con underscore, scrivendola come ``delay_time``. Entrambe le forme vanno bene, ma scegline una e sii coerente per migliorare la leggibilità.

3. Non usare parole chiave. Se usi una parola riservata, come int, l’IDE la evidenzierà per segnalarti che non può essere usata come nome di variabile. Se viene colorata, cambiala.

4. Non usare simboli speciali. Non sono ammessi spazi, #, $, /, +, %, ecc. Usa lettere (maiuscole o minuscole), numeri (non come primo carattere) e underscore: bastano per qualsiasi combinazione utile.


**Assegnare un valore a una variabile**

Una volta dichiarata, possiamo assegnare un valore alla variabile utilizzando l'operatore di assegnazione ``=``.

Possiamo assegnare un valore subito al momento della dichiarazione:


.. code-block:: C

    int delayTime = 500;

Oppure possiamo assegnarglielo successivamente:

.. code-block:: C

    int delayTime; // nessun valore iniziale
    delayTime = 500; // valore assegnato: 500
    delayTime = delayTime +200; // valore aggiornato: 700