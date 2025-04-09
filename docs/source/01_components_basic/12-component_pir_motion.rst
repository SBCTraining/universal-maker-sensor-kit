.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker ed entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_pir_motion:

Modulo Sensore di Movimento PIR (HC-SR501)
============================================

.. image:: img/12_pir_module.png
    :width: 300
    :align: center


Il sensore di movimento a infrarossi passivo (PIR) è un sensore in grado di rilevare il movimento. È comunemente utilizzato in sistemi di sicurezza e illuminazione automatica. Il sensore dispone di due finestrelle che rilevano la radiazione infrarossa. Quando un oggetto, come una persona, passa davanti al sensore, questo rileva la variazione della quantità di radiazione IR e genera un segnale in uscita.

Specifiche
---------------------------
* Tensione di alimentazione: 5V~20V  
* Uscita: Di default bassa; diventa alta al passaggio di una persona
* Tempo di ritardo: 5~200s (regolabile)
* Tempo di blocco: 8s
* Angolo di rilevamento: <120°, entro 7 metri (regolabile)
* Modalità di trigger: L = non ripetibile, H = ripetibile
* Dimensioni PCB: 32 x 24mm
* Dimensioni lente: 23mm
* Temperatura di lavoro: -15~+70℃

Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva dal controllore principale.  
* **GND**: Collegamento a massa.
* **DO**: Uscita digitale. Di default è a livello basso; diventa alto quando rileva il passaggio di qualcuno.

Principio di funzionamento
------------------------------
Il sensore PIR è composto da due finestrelle collegate a un amplificatore differenziale. Se davanti al sensore c’è un oggetto fermo, entrambe le finestrelle ricevono la stessa quantità di radiazione e l’uscita è zero. Se un oggetto in movimento entra nel campo visivo, una delle finestrelle riceverà più radiazione dell’altra, facendo variare l’uscita (alto o basso). Questa variazione è ciò che segnala il movimento rilevato.

.. image:: img/12_pir_working_principle.jpg
    :width: 500
    :align: center

Dopo il collegamento del modulo, è previsto un tempo di inizializzazione di circa un minuto. Durante questa fase, il modulo può generare da 0 a 3 segnali di uscita a intervalli. Dopo l’inizializzazione, entra in modalità standby. È importante evitare fonti luminose o di disturbo nelle vicinanze della lente, così da ridurre falsi rilevamenti. È consigliabile anche evitare ambienti con forti correnti d’aria, poiché il vento può interferire con il sensore.

.. image:: img/12_pir_module_back.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/><br/> 

Regolazione della distanza
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Ruotando il potenziometro per la regolazione della distanza in senso orario, l’intervallo di rilevamento aumenta fino a circa 0-7 metri. Ruotandolo in senso antiorario, la distanza si riduce fino a un minimo di circa 0-3 metri.

Regolazione del ritardo
^^^^^^^^^^^^^^^^^^^^^^^^^^
Ruotando il potenziometro per la regolazione del ritardo in senso orario, si aumenta il tempo di ritardo fino a un massimo di circa 300s. Ruotandolo in senso antiorario, il ritardo si riduce fino a un minimo di 5s.

Due modalità di trigger
^^^^^^^^^^^^^^^^^^^^^^^^^^
È possibile selezionare la modalità di funzionamento tramite il jumper.

* H: Modalità di trigger ripetibile. Dopo il rilevamento, il modulo emette un segnale alto. Se qualcuno entra di nuovo nell’area di rilevamento durante il tempo di ritardo, l’uscita rimane alta.
* L: Modalità di trigger non ripetibile. Dopo il rilevamento, l’uscita passa ad alto livello. Terminato il tempo di ritardo, torna automaticamente a livello basso.

Esempi
---------------------------
* :ref:`uno_lesson12_pir_motion` (Arduino UNO)
* :ref:`esp32_lesson12_pir_motion` (ESP32)
* :ref:`pico_lesson12_pir_motion` (Raspberry Pi Pico)
* :ref:`pi_lesson12_pir_motion` (Raspberry Pi)

* :ref:`uno_lesson40_motion_triggered_relay` (Arduino UNO)
* :ref:`uno_iot_intrusion_alert_system` (Arduino UNO)
* :ref:`esp32_motion_triggered_relay` (ESP32)
* :ref:`esp32_iot_intrusion_alert_system` (ESP32)