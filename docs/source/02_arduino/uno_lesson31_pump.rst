.. note:: 

    Ciao, benvenuto nella Community Facebook di SunFounder per appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all'aiuto della community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni l'accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni e Giveaway Festivi**: Partecipa a giveaway e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi!

.. _uno_lesson31_pump:

Lezione 31: Pompa Centrifuga
==================================

In questa lezione imparerai a controllare una pompa centrifuga con un Arduino Uno R3 o R4 e un modulo driver motore L9110. Vedrai come configurare e programmare l'Arduino per avviare la pompa in una direzione, farla funzionare per un determinato periodo di tempo e poi spegnerla. Questo progetto pratico è ideale per i principianti e offre una comprensione fondamentale del controllo dei motori e della gestione delle uscite nei progetti Arduino.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI NEL KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistare i componenti separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l'acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-

* Arduino UNO R3 o R4
* :ref:`cpn_pump`
* :ref:`cpn_l9110`


Collegamenti
---------------------------

.. image:: img/Lesson_31_pump_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f5fad7fa-4b2c-4630-a832-d3a5e077d9fa/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Due pin vengono definiti per il controllo del motore: ``motorB_1A`` e ``motorB_2A``. Questi pin si collegano al modulo L9110 per controllare la direzione e la velocità del motore.
  
   .. code-block:: arduino
   
      const int motorB_1A = 9;
      const int motorB_2A = 10;

2. Configurazione dei pin e controllo della pompa:

   - La funzione ``setup()`` imposta i pin come ``OUTPUT``, permettendo ad Arduino di inviare segnali al modulo motore.

   - La funzione ``analogWrite()`` regola la velocità del motore. Impostando un pin su ``HIGH`` e l’altro su ``LOW``, la pompa gira in una direzione. Dopo 5 secondi, entrambi i pin sono settati a 0 per spegnere la pompa.

   .. raw:: html

      <br/>
   
   .. code-block:: arduino
   
      void setup() {
         pinMode(motorB_1A, OUTPUT);  // imposta il pin 1 della pompa come uscita
         pinMode(motorB_2A, OUTPUT);  // imposta il pin 2 della pompa come uscita
         analogWrite(motorB_1A, HIGH); 
         analogWrite(motorB_2A, LOW);
         delay(5000);  // attesa di 5 secondi
         analogWrite(motorB_1A, 0);  // spegne la pompa
         analogWrite(motorB_2A, 0);
      }
