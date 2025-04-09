.. note::

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche grazie al supporto del nostro team e della community.
    - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson44_digital_dice:

Lezione 44: Dado Digitale
=============================================================


Questo progetto simula il lancio di un dado utilizzando un display OLED.  
La simulazione viene attivata scuotendo l'interruttore a vibrazione, facendo scorrere i numeri da 1 a 6 sul display,  
proprio come nel lancio di un dado reale.  
Dopo un breve intervallo, il display si ferma mostrando un numero scelto casualmente che rappresenta il risultato del lancio.




Componenti Necessari
--------------------------

Per questo progetto sono richiesti i seguenti componenti.

È sicuramente conveniente acquistare l'intero kit, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome
        - COMPONENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti singolarmente dai link riportati di seguito.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_vibration`
        - |link_sw420_vibration_module_buy|
    *   - :ref:`cpn_oled`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_44_Digital_dice_uno_bb.png
    :width: 100%


Codice
---------------------------

.. note::
   Per installare la libreria, apri il Library Manager dell'Arduino IDE, cerca **"Adafruit SSD1306"** e **"Adafruit GFX"**, quindi installale.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/70e73ef9-2968-4845-befd-23185286fd93/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Analisi del Codice
---------------------------

Una panoramica dettagliata del codice:

1. Inizializzazione delle variabili:

   ``vibPin``: Pin digitale collegato al sensore di vibrazione.

2. Variabili volatili:

   ``rolling``: Flag volatile che indica lo stato del lancio del dado. È dichiarata volatile perché viene utilizzata sia nel programma principale che nella routine di interrupt.

3. ``setup()``:

   Configura il pin del sensore di vibrazione come input.  
   Assegna un interrupt al sensore per attivare la funzione ``rollDice`` al cambiamento di stato.  
   Inizializza il display OLED.

4. ``loop()``:

   Controlla continuamente se ``rolling`` è attivo; in tal caso, mostra numeri casuali da 1 a 6.  
   Il ciclo si ferma se la vibrazione dura più di 500 millisecondi.

5. ``rollDice()``:

   Routine di interrupt del sensore di vibrazione. Avvia il lancio del dado memorizzando il tempo corrente al momento della vibrazione.

6. ``displayNumber()``:

   Visualizza sul display OLED il numero selezionato.