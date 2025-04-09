.. note:: 

    Ciao, benvenuto nella community SunFounder su Facebook per appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anticipo agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto per esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

Verifica di ``GPIO Zero``
=================================

``GPIO Zero`` è un modulo per il controllo dei pin GPIO del Raspberry Pi. Questo pacchetto fornisce una serie di classi e funzioni intuitive per gestire i GPIO su Raspberry Pi. Per esempi e documentazione, visita: https://gpiozero.readthedocs.io/en/latest/.

L'ultima versione del sistema operativo Raspberry Pi include GPIO Zero di default. Per verificarne l'installazione, apri il Terminale ed esegui:

.. code-block::

    python

.. image:: img/zero_01.png
    :width: 100%


Successivamente, digita ``import gpiozero`` all'interno della CLI di Python. Se non appare alcun errore, GPIO Zero è installato correttamente.

.. code-block::

    import gpiozero

.. image:: img/zero_02.png
    :width: 100%


Se desideri uscire dalla CLI di Python, digita:

.. code-block::

    exit()

.. image:: img/zero_03.png
    :width: 100%


