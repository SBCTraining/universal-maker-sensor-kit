.. note:: 

    Ciao, benvenuto nella Community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all’aiuto della community e del nostro team.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato alle novità sui prodotti e alle anteprime esclusive.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a promozioni festive e giveaway.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _uno_lesson32_passive_buzzer:

Lezione 32: Modulo Buzzer Passivo
====================================

In questa lezione imparerai a riprodurre una melodia utilizzando un modulo buzzer passivo con Arduino. Vedremo come programmare Arduino per controllare il buzzer e generare note di diversa durata. Questo progetto è perfetto per i principianti perché offre un’esperienza pratica nella produzione di suoni e nella comprensione delle note musicali applicate all’elettronica. Inoltre, acquisirai familiarità con l'uso della scheda Arduino Uno e del modulo buzzer passivo.

Componenti Necessari
--------------------------

Per questo progetto sono necessari i seguenti componenti.

È sicuramente comodo acquistare un kit completo. Ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - COMPONENTI INCLUSI
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

In alternativa, puoi acquistare i componenti singolarmente dai seguenti link:

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Descrizione del Componente
        - Link per l’acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|


Collegamenti
---------------------------

.. image:: img/Lesson_32_passive_buzzer_module_uno_bb.png
    :width: 100%


Codice
---------------------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/eebc46ab-2a9d-4731-8778-3c8f07b0003b/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Inclusione della libreria pitches:
   Questa libreria fornisce i valori di frequenza delle note musicali, permettendo di usare la notazione musicale nel codice.

   .. code-block:: arduino
       
      #include "pitches.h"

2. Definizione di costanti e array:

   * ``buzzerPin`` è il pin digitale dell’Arduino a cui è collegato il buzzer.

   * ``melody[]`` è un array che contiene la sequenza delle note da riprodurre.

   * ``noteDurations[]`` contiene la durata di ciascuna nota.

   .. raw:: html
      
      <br/>

   .. code-block:: arduino
   
      const int buzzerPin = 8;
      int melody[] = {
        NOTE_C4, NOTE_G3, NOTE_G3, NOTE_A3, NOTE_G3, 0, NOTE_B3, NOTE_C4
      };
      int noteDurations[] = {
        4, 8, 8, 4, 4, 4, 4, 4
      };

3. Riproduzione della melodia:

   * Il ciclo ``for`` scorre tutte le note dell'array melody.

   * La funzione ``tone()`` riproduce ciascuna nota sul buzzer per la durata specificata.

   * Un ritardo tra una nota e l'altra consente di distinguerle.

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
   Poiché la melodia viene eseguita una sola volta all'interno della funzione setup, la funzione loop rimane vuota.
