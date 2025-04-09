.. note::

    Ciao, benvenuto nella comunità di appassionati di SunFounder Raspberry Pi, Arduino e ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue abilità.
    - **Anteprime Esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotti e anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _install_micropython_on_pico:

Installazione di MicroPython sul Tuo Pico
==============================================


Ora passiamo all'installazione di MicroPython sul Raspberry Pi Pico, l'IDE Thonny offre un modo molto conveniente per installarlo con un solo clic.

.. note::
    Puoi anche usare il |link_micropython_pi| fornito ufficialmente da Raspberry Pi trascinando e rilasciando un file ``rp2_pico_xxxx.uf2`` sul Raspberry Pi Pico.



#. Apri l'IDE Thonny.

   .. image:: img/set_pico1.png

#. Premi e tieni premuto il pulsante **BOOTSEL** e poi collega il Pico al computer tramite un cavo Micro USB. Rilascia il pulsante **BOOTSEL** dopo che il tuo Pico è stato montato come un dispositivo di archiviazione di massa chiamato **RPI-RP2**.

   .. image:: img/bootsel_onboard.png
      :width: 70%
      :align: center

   .. raw:: html

      <br/>

#. Nell'angolo in basso a destra, clicca sul pulsante di selezione dell'interprete e seleziona **Installa Micropython**.

   .. note::
      Se il tuo Thonny non ha questa opzione, aggiornalo all'ultima versione.

   .. image:: img/set_pico2.png

#. Nella sezione **Target volume**, apparirà automaticamente il volume del Pico che hai appena collegato. Nella sezione **variant**, seleziona **Raspberry Pi.Pico/Pico H**. Seleziona la versione più recente nel menu a discesa della versione.

   .. image:: img/set_pico3.png

#. Clicca sul pulsante **Installa**, attendi il completamento dell'installazione.

   .. image:: img/set_pico4.png


#. Congratulazioni, ora il tuo Raspberry Pi Pico è pronto all'uso.

   .. image:: img/set_pico5.png