.. note:: 

    Ciao, benvenuto nella community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti esclusivi**: Approfitta di sconti riservati sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

Come caricare uno Sketch sulla scheda?
=============================================

In questa sezione imparerai come caricare lo sketch creato precedentemente sulla scheda Arduino, oltre ad alcune considerazioni importanti.

**1. Seleziona scheda e porta**

Le schede di sviluppo Arduino sono generalmente fornite con un cavo USB. Usalo per collegare la scheda al computer.

Seleziona la **Scheda** e la **Porta** corrette nell’IDE Arduino. Normalmente, la scheda Arduino viene riconosciuta automaticamente dal computer e viene assegnata una porta che puoi selezionare da qui.

    .. image:: img/board_port.png
        :width: 90%


Se la scheda è già collegata ma non viene riconosciuta, controlla se appare il logo **INSTALLED** nella sezione **Arduino AVR Boards** del **Gestore Schede**. In caso contrario, scorri verso il basso e clicca su **INSTALLA**.

    .. image:: img/upload1.png
        :width: 90%

In particolare, per UNO R4, cerca **"UNO R4"** nel **Gestore Schede** e verifica che la libreria corrispondente sia installata.

    .. image:: img/install_uno_r4_lib.png
        :width: 90%

Riavviare l’IDE Arduino e ricollegare la scheda risolve la maggior parte dei problemi. Puoi anche selezionare la scheda e la porta manualmente tramite **Strumenti** -> **Scheda** o **Porta**.


**2. Verifica dello Sketch**

Cliccando il pulsante Verifica, lo sketch verrà compilato per controllare la presenza di eventuali errori.

    .. image:: img/sp221014_174532.png
        :width: 90%

Se elimini o scrivi per errore dei caratteri, puoi usare questa funzione per individuare e correggere gli errori. La barra dei messaggi ti mostrerà dove si è verificato l’errore e di che tipo si tratta.

    .. image:: img/sp221014_175307.png
        :width: 90%

Se non ci sono errori, vedrai un messaggio come questo.

    .. image:: img/sp221014_175512.png
        :width: 90%


**3. Caricamento dello Sketch**

Completati i passaggi precedenti, clicca sul pulsante **Carica** per trasferire lo sketch sulla scheda.

    .. image:: img/sp221014_175614.png
        :width: 90%

Se il caricamento è andato a buon fine, vedrai il seguente messaggio di conferma.

    .. image:: img/sp221014_175654.png
        :width: 90%

Allo stesso tempo, vedrai lampeggiare il LED integrato.

.. image:: img/1_led.jpg
    :width: 400
    :align: center

.. raw:: html
    
    <br/>

Una volta caricato lo sketch, la scheda Arduino lo eseguirà automaticamente ogni volta che viene alimentata. Il programma può essere sovrascritto caricandone uno nuovo.




