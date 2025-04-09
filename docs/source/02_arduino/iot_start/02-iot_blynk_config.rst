.. note::

    Ciao e benvenuto nella community Facebook dedicata agli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue competenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri maker entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie al supporto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue abilità.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime riservate.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni festive e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

1.2 Configurazione di Blynk
==============================


#. Vai su `BLYNK <https://blynk.io/>`_ e clicca su **START FREE**.

   .. image:: img/sp220607_142551.png
        :width: 90%

   .. raw:: html

      <br/><br/>

#. Inserisci il tuo indirizzo email per registrare un account.

   .. image:: img/sp220607_142807.png
        :width: 70%
        :align: center

   .. raw:: html

      <br/>

#. Controlla la tua email e completa la registrazione dell’account.

   .. image:: img/sp220607_142936.png
    :width: 90%

   .. raw:: html

      <br/><br/>

#. Successivamente apparirà il **Blynk Tour**, che puoi leggere per conoscere le informazioni di base su Blynk.

   .. image:: img/sp220607_143244.png
    :width: 90%

   .. raw:: html

      <br/><br/>

#. Ora dobbiamo creare un template e un dispositivo tramite il **Quick Start**, clicca su **Let's go**.

   .. image:: img/sp220607_143608.png
    :width: 90%

   .. raw:: html

      <br/><br/>  

#. Seleziona il tipo di hardware e la modalità di connessione.

   .. image:: img/sp20220614173218.png
    :width: 90%

   .. raw:: html

      <br/><br/>

#. Qui ti viene indicato quale IDE è necessario preparare: consigliamo l’ **Arduino IDE**.

   .. image:: img/sp20220614173454.png
    :width: 90%

   .. raw:: html

      <br/><br/>

#. Qui viene suggerita una libreria da aggiungere, ma quella consigliata presenta alcuni problemi. Sarà necessario aggiungere manualmente altre librerie (ne parleremo più avanti). Clicca su **Next** per procedere alla creazione del nuovo template e dispositivo.

   .. image:: img/sp20220614173629.png
    :width: 90%

   .. raw:: html

      <br/><br/>

#. I passaggi successivi prevedono il caricamento del codice e la connessione della tua scheda a Blynk, ma a causa dei problemi con la libreria fornita, sarà necessario aggiungerne altre. Quindi, clicca su **Cancel** per interrompere il **Quick Start**.

   .. image:: img/sp20220614174006.png
    :width: 90%

   .. raw:: html

      <br/><br/>

#. Clicca sul pulsante **Search** e vedrai il nuovo dispositivo appena creato.

   .. image:: img/sp20220614174410.png
    :width: 90%

   .. raw:: html

      <br/><br/>

#. Accedi a questo **Quickstart Device** e clicca su **Device Info**: nella pagina delle informazioni del dispositivo troverai ``TEMPLATE_ID``, ``DEVICE_NAME`` e ``AUTH_TOKEN``, che ti serviranno nei passaggi successivi.

   .. image:: img/sp20220614174721.png
    :width: 90%