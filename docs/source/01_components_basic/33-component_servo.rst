.. note:: 

    Ciao! Benvenuto nella community Facebook degli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e anticipazioni.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni a tema e concorsi con premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_servo:

Servomotore (SG90)
==========================

.. image:: img/33_servo.png
    :width: 300
    :align: center

I servomotori sono dispositivi in grado di ruotare fino a un angolo o una posizione specifica. Vengono utilizzati per muovere bracci robotici, sterzi, supporti per fotocamere e altro ancora. Un servomotore ha tre fili: alimentazione, massa e segnale. Il filo di alimentazione è solitamente rosso e va collegato al pin 5V della scheda Arduino. Il filo di massa è di solito nero o marrone e va collegato a un pin GND. Il filo del segnale è normalmente giallo o arancione e va collegato a un pin PWM.

Pinout
---------------------------
* Filo marrone: GND
* Filo arancione: Pin del segnale, da collegare al pin PWM della scheda principale.
* Filo rosso: VCC

Principio di funzionamento
------------------------------
Un servo è generalmente composto dai seguenti elementi: involucro, albero, sistema di ingranaggi, potenziometro, motore DC e scheda embedded.

Funziona nel seguente modo:

* Il microcontrollore invia segnali PWM al servo, che vengono ricevuti dalla scheda interna tramite il pin del segnale e utilizzati per controllare il motore interno.
* Il motore fa girare il sistema di ingranaggi, che a sua volta muove l’albero del servo dopo una riduzione.
* L’albero e il potenziometro sono connessi insieme.
* Quando l’albero ruota, muove anche il potenziometro, il quale invia un segnale di tensione alla scheda embedded.
* Quest’ultima determina direzione e velocità di rotazione in base alla posizione attuale, così da fermarsi esattamente nella posizione definita e mantenerla.


.. image:: img/33_servo_internal.png
    :width: 450
    :align: center

.. raw:: html
    
    <br/>

.. _cpn_servo_pulse:

**Impulso di lavoro**

L’angolo è determinato dalla durata dell’impulso applicato al filo di controllo, secondo il principio della modulazione della larghezza dell’impulso (PWM).

* Il servo si aspetta un impulso ogni 20 ms. La durata dell’impulso determina l’angolo di rotazione.
* Ad esempio, un impulso di 1,5 ms posiziona il servo a 90 gradi (posizione neutra).
* Un impulso inferiore a 1,5 ms farà ruotare l’albero in senso antiorario rispetto al punto neutro.
* Un impulso superiore a 1,5 ms causerà la rotazione in senso orario.
* I limiti minimo e massimo dell’impulso variano da un servo all’altro.
* In generale, la larghezza dell’impulso varia da circa 0,5 ms a 2,5 ms.

.. image:: img/33_servo_duty.png
    :width: 90%
    :align: center

.. raw:: html
    
    <br/>



Esempi
---------------------------
* :ref:`uno_lesson33_servo` (Arduino UNO)
* :ref:`esp32_lesson33_servo` (ESP32)
* :ref:`pico_lesson33_servo` (Raspberry Pi Pico)
* :ref:`pi_lesson33_servo` (Raspberry Pi)

* :ref:`uno_lesson37_trashcan` (Arduino UNO)
* :ref:`esp32_trashcan` (ESP32)