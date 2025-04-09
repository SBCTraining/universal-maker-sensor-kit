.. note::

    Ciao, benvenuto nella comunità degli appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Introduzione a MicroPython
======================================

MicroPython è un'implementazione software di un linguaggio di programmazione largamente compatibile con Python 3, scritto in C, ottimizzato per funzionare su un microcontrollore.

MicroPython consiste in un compilatore Python per bytecode e un interprete runtime per quel bytecode. All'utente viene presentato un prompt interattivo (il REPL) per eseguire immediatamente i comandi supportati. Sono incluse una selezione di librerie core Python; MicroPython include moduli che danno al programmatore accesso all'hardware a basso livello.

* Riferimento: `MicroPython - Wikipedia <https://en.wikipedia.org/wiki/MicroPython>`_

La Storia Inizia Qui
--------------------------------

Le cose cambiarono nel 2013 quando Damien George lanciò una campagna di crowdfunding (Kickstarter).

Damien era uno studente universitario all'Università di Cambridge e un appassionato programmatore di robotica. Voleva ridurre il mondo di Python da una macchina da gigabyte a un kilobyte. La sua campagna Kickstarter era per supportare il suo sviluppo mentre trasformava il suo proof of concept in un'implementazione finita.

MicroPython è supportato da una comunità diversificata di Pythonisti che ha un forte interesse nel vedere il progetto riuscire.

Oltre a testare e supportare la base di codice, gli sviluppatori hanno fornito tutorial, librerie di codice e porting hardware, così Damien ha potuto concentrarsi su altri aspetti del progetto.

* Riferimento: `realpython <https://realpython.com/micropython/>`_


Perché MicroPython？
-----------------------

Anche se la campagna Kickstarter originale ha rilasciato MicroPython come una scheda di sviluppo "pyboard" con STM32F4, MicroPython supporta molte architetture di prodotto basate su ARM. Le porte supportate principali sono ARM Cortex-M (molti schedari STM32, TI CC3200/WiPy, schede Teensy, serie Nordic nRF, SAMD21 e SAMD51), ESP8266, ESP32, PIC 16bit, Unix, Windows, Zephyr e JavaScript.
In secondo luogo, MicroPython permette un feedback veloce. Questo perché puoi usare il REPL per inserire comandi interattivamente e ottenere risposte. Puoi anche modificare il codice e eseguirlo immediatamente invece di attraversare il ciclo codice-compilazione-caricamento-esecuzione.

Mentre Python ha gli stessi vantaggi, per alcune schede microcontrollore come il Raspberry Pi Pico, sono piccole, semplici e hanno poca memoria per eseguire il linguaggio Python in toto. Ecco perché MicroPython si è evoluto, mantenendo le principali caratteristiche di Python e aggiungendone di nuove per lavorare con queste schede microcontrollore.

Successivamente imparerai a installare MicroPython nel Raspberry Pi Pico.