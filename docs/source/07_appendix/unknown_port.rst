.. note:: 

   Ciao, benvenuti nella Community di appassionati di SunFounder Raspberry Pi, Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

   **Perché unirsi?**

   - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
   - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
   - **Anteprime Esclusive**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime.
   - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
   - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

   👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _unknown_com_port:

Sempre visualizzato "Unknown COMxx"?
======================================

Quando colleghi l'ESP32 al computer, l'IDE di Arduino mostra spesso ``Unknown COMxx``. Perché accade questo?

.. image:: img/unknown_device.png

Questo succede perché il driver USB per ESP32 è diverso da quello delle schede Arduino regolari. L'IDE di Arduino non può riconoscere automaticamente questa scheda.

In tale scenario, devi selezionare manualmente la scheda corretta seguendo questi passaggi:

#. Clicca su **"Seleziona un'altra scheda e porta"**.

    .. image:: img/unknown_select.png

#. Nella ricerca, digita **"esp32 dev module"**, poi seleziona la scheda che appare. Successivamente, seleziona la porta corretta e clicca **OK**.

    .. image:: img/unknown_board.png

#. Ora, dovresti essere in grado di vedere la tua scheda e porta in questa finestra di visualizzazione rapida.

    .. image:: img/unknown_correct.png