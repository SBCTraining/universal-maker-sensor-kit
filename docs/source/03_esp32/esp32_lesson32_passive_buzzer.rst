.. note::

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza di Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson32_passive_buzzer:

Lezione 32: Modulo Buzzer Passivo
====================================

In questa lezione, imparerai a suonare una melodia su un modulo buzzer passivo utilizzando una scheda di sviluppo ESP32. Copriremo la programmazione dell'ESP32 per controllare il buzzer e creare note musicali con durate variabili. Questo progetto è ideale per i principianti in elettronica e programmazione, fornendo esperienza pratica nella generazione di suoni e nei principi digitali del suono. Svilupperai competenze pratiche nell'utilizzo della scheda ESP32 e nell'integrazione di componenti semplici come il buzzer passivo.

Componenti Necessari
------------------------

In questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori per Maker Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
------------

.. image:: img/Lesson_32_Passive_buzzer_esp32_bb.png
    :width: 100%


Codice
----------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/1f3f8514-29eb-491f-b40f-0d808ef0aaac/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Inclusione della libreria delle frequenze:

   Questa libreria fornisce i valori di frequenza per varie note musicali, consentendo di utilizzare la notazione musicale nel tuo codice.

   .. code-block:: arduino
       
      #include "pitches.h"

2. Definizione di costanti e array:

   * ``buzzerPin`` è il pin digitale sulla Scheda di Sviluppo ESP32 dove è collegato il buzzer.

   * ``melody[]`` è un array che memorizza la sequenza di note da suonare.

   * ``noteDurations[]`` è un array che memorizza la durata di ogni nota nella melodia.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino
   
      const int buzzerPin = 25;
      int melody[] = {
        NOTE_C4, NOTE_G3, NOTE_G3, NOTE_A3, NOTE_G3, 0, NOTE_B3, NOTE_C4
      };
      int noteDurations[] = {
        4, 8, 8, 4, 4, 4, 4, 4
      };

3. Esecuzione della melodia:

   * Il ciclo ``for`` itera su ogni nota della melodia.

   * La funzione ``tone()`` suona una nota sul buzzer per una durata specifica.

   * Viene aggiunto un ritardo tra le note per distinguerle.

   * La funzione ``noTone()`` interrompe il suono.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino
   
      void setup() {
        for (int thisNote = 0; thisNote < 8; thisNote++) {
          int noteDuration = 1000 / noteDurations[thisNote];
          tone(buzzerPin, melody[thisNote], noteDuration);
          int pauseBetweenNotes = noteDuration * 1.30;
          delay(pauseBetweenNotes);
          noTone(buzzerPin);
        }
      }

4. Funzione loop vuota:

   Poiché la melodia viene suonata solo una volta nel setup, non c'è codice nella funzione loop.
