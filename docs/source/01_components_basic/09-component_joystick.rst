.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati e maker.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anticipazioni sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_joystick:

Modulo Joystick
==========================

.. image:: img/09_joystick.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

Un modulo joystick è un dispositivo in grado di misurare il movimento di una manopola in due direzioni: orizzontale (asse X) e verticale (asse Y). Questo tipo di modulo può essere utilizzato per controllare giochi, robot, fotocamere e molto altro.

Specifiche
---------------------------
* Tensione di alimentazione: 3.3V o 5V
* Dimensioni PCB: 34 x 26mm
* Tipo di segnale in uscita: DO e AO
* Uscita analogica: X, Y, uscita analogica su 2 assi
* Uscita digitale: Z, uscita digitale

Pinout
---------------------------
* **+5V**: Ingresso di alimentazione positiva dal controllore principale. 
* **GND**: Collegamento a massa.
* **VRX**: Uscita analogica. Tensione analogica dell’asse X. Spostando il joystick da sinistra a destra, la tensione in uscita varia da 0 a VCC. Quando il joystick è in posizione centrale (a riposo), il valore sarà circa metà di VCC.
* **VRY**: Uscita analogica. Tensione analogica dell’asse Y. Spostando il joystick su o giù, la tensione in uscita varia da 0 a VCC. Quando il joystick è in posizione centrale (a riposo), la lettura sarà approssimativamente metà di VCC.
* **SW**: Uscita digitale. L’interruttore integrato invia un segnale flottante per impostazione predefinita.

.. tip::
    Per leggere correttamente lo stato dell’interruttore, è necessario utilizzare una resistenza di pull-up. Quando si preme la manopola del joystick, l’uscita dello switch diventa LOW; altrimenti rimane HIGH. Assicurati che il pin d’ingresso collegato al pulsante abbia la resistenza di pull-up interna abilitata oppure una resistenza di pull-up esterna collegata.

Principio di funzionamento
---------------------------
Il joystick funziona grazie alla variazione di resistenza di due potenziometri (di solito da 10 kΩ). Variando la resistenza sugli assi X e Y, l’Arduino riceve tensioni diverse che vengono interpretate come coordinate X e Y. Il processore necessita di un’unità ADC per convertire i valori analogici del joystick in valori digitali e procedere con l’elaborazione.

Le schede Arduino sono dotate di sei canali ADC a 10 bit. Questo significa che la tensione di riferimento dell’Arduino (5V) è suddivisa in 1024 segmenti. Quando il joystick si muove lungo l’asse X, il valore ADC varia da 0 a 1023, con il valore centrale pari a circa 512. L'immagine seguente mostra i valori ADC approssimativi in base alla posizione del joystick.

.. image:: img/09_joystick_xy.png
    :width: 400
    :align: center

Schema elettrico
---------------------------

.. image:: img/09_joystick_schematic.png
    :width: 80%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson09_joystick` (Arduino UNO)
* :ref:`esp32_lesson09_joystick` (ESP32)
* :ref:`pico_lesson09_joystick` (Raspberry Pi Pico)
* :ref:`pi_lesson09_joystick` (Raspberry)

* :ref:`uno_lesson53_direction_indicator` (Arduino UNO)
