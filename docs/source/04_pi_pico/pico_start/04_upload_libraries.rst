
.. note::

    Ciao, benvenuto nella Comunità degli appassionati di SunFounder Raspberry Pi, Arduino e ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Accedi in anteprima ai nuovi annunci di prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _add_libraries_py:

Caricare le Librerie su Pico
===================================

In alcuni progetti, avrai bisogno di librerie aggiuntive. Quindi, qui carichiamo prima queste librerie sul Raspberry Pi Pico W, per poter eseguire direttamente il codice in seguito.

#. Scarica il codice pertinente dal link sottostante.

   * :download:`SunFounder Universal Maker Sensor Kit <https://codeload.github.com/sunfounder/universal-maker-sensor-kit/zip/refs/heads/main>`


#. Apri l'IDE Thonny e collega il Pico al tuo computer con un cavo micro USB, quindi clicca sull'interprete "MicroPython (Raspberry Pi Pico).COMXX" nell'angolo in basso a destra.

   .. image:: img/sec_inter.png

#. Nella barra di navigazione superiore, clicca su **Visualizza** -> **File**.

   .. image:: img/th_files.png

#. Cambia il percorso alla cartella dove hai scaricato il `pacchetto di codici <https://codeload.github.com/sunfounder/universal-maker-sensor-kit/zip/refs/heads/main>`_ prima, e poi vai alla cartella ``universal-maker-sensor-kit-main/pico/libs``.

   .. image:: img/th_path.png

#. Seleziona tutti i file o le cartelle nella cartella "libs/" (tenendo premuto Shift e cliccando sul primo e ultimo file nella cartella), poi clicca con il tasto destro e seleziona **Carica in /**, ci vorrà un po' per caricare.

   .. image:: img/th_upload.png

#. Ora vedrai i file che hai appena caricato all'interno del tuo drive ``Raspberry Pi Pico``.

   .. image:: img/th_done.png