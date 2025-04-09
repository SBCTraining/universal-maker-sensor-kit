.. note:: 

   Ciao, benvenuti nella Community di appassionati di SunFounder Raspberry Pi, Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 con altri appassionati.

   **Perché unirsi?**

   - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra community e del nostro team.
   - **Impara e Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
   - **Anteprime Esclusive**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime.
   - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
   - **Promozioni Festive e Giveaway**: Partecipa ai giveaway e alle promozioni festive.

   👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _cpn_pico_w:

Raspberry Pi Pico W
=======================================

.. image:: img/pico_w_side.png
    :width: 60%
    :align: center

Il Raspberry Pi Pico W porta la connettività wireless nella linea di prodotti più venduti Raspberry Pi Pico. Basato sulla nostra piattaforma di silicio RP2040, i prodotti Pico incarnano i nostri valori di alta prestazione, basso costo e facilità d'uso nello spazio dei microcontrollori.

Il Raspberry Pi Pico W offre supporto LAN wireless 802.11 b/g/n a 2.4GHz, con un'antenna integrata e certificazione di conformità modulare. È in grado di operare sia in modalità stazione che punto di accesso. L'accesso completo alla funzionalità di rete è disponibile sia per gli sviluppatori C che MicroPython.

Il Raspberry Pi Pico W abbina RP2040 con 2MB di memoria flash e un chip di alimentazione che supporta tensioni di ingresso da 1,8–5,5V. Offre 26 pin GPIO, tre dei quali possono funzionare come ingressi analogici, su pad passanti con passo di 0,1” e bordi smussati.
Il Raspberry Pi Pico W è disponibile come unità singola o in bobine da 480 unità per l'assemblaggio automatizzato.

Caratteristiche
--------------------

* Formato 21 mm x 51 mm
* Chip microcontrollore RP2040 progettato da Raspberry Pi nel Regno Unito
* Processore dual-core Arm Cortex-M0+ con clock flessibile fino a 133 MHz
* 264kB di SRAM integrato
* 2MB di flash QSPI integrato
* LAN wireless 802.11n a 2.4GHz
* 26 pin GPIO multifunzione, inclusi 3 ingressi analogici
* 2 x UART, 2 x controller SPI, 2 x controller I2C, 16 x canali PWM
* 1 x controller USB 1.1 e PHY, con supporto host e dispositivo
* 8 x macchine a stati I/O programmabili (PIO) per supporto periferiche personalizzate
* Alimentazione supportata da 1.8-5.5V DC
* Temperatura operativa -20°C a +70°C
* Modulo con bordi smussati permette la saldatura diretta su schede portanti
* Programmazione tramite trascinamento utilizzando la memoria di massa su USB
* Modalità di basso consumo energetico e dormienza
* Orologio integrato preciso
* Sensore di temperatura
* Librerie di librerie intere e in virgola mobile accelerate su chip

Pin di Pico
-------------

.. image:: img/pico_pin.jpg
    :width: 100%
    :align: center

.. raw:: html

    <br/>

.. list-table::
    :widths: 3 5 10
    :header-rows: 1

    *   - Nome
        - Descrizione
        - Funzione
    *   - GP0-GP28
        - Pin di input/output generici
        - Possono agire sia come input che output e non hanno uno scopo fisso
    *   - GND
        - Terra a 0 volt
        - Diversi pin GND intorno a Pico W per facilitare il cablaggio.
    *   - RUN
        - Abilita o disabilita il tuo Pico
        - Avvia e ferma il tuo Pico W da un altro microcontrollore.
    *   - GPxx_ADCx
        - Input/output generico o ingresso analogico
        - Utilizzato come ingresso analogico così come input digitale o output – ma non entrambi contemporaneamente.
    *   - ADC_VREF
        - Riferimento di tensione per il convertitore analogico-digitale (ADC)
        - Un pin di ingresso speciale che imposta una tensione di riferimento per qualsiasi ingresso analogico.
    *   - AGND
        - Terra a 0 volt per il convertitore analogico-digitale (ADC)
        - Una connessione a terra speciale da utilizzare con il pin ADC_VREF.
    *   - 3V3(O)
        - Alimentazione a 3.3 volt
        - Una fonte di alimentazione a 3.3V, la stessa tensione a cui funziona internamente il tuo Pico W, generata dall'ingresso VSYS.
    *   - 3v3(E)
        - Abilita o disabilita l'alimentazione
        - Accendi o spegni l'alimentazione 3V3(O), può anche spegnere il tuo Pico W.
    *   - VSYS
        - Alimentazione da 2-5 volt
        - Un pin direttamente collegato all'alimentazione interna del tuo Pico, che non può essere spento senza spegnere anche il Pico W.
    *   - VBUS
        - Alimentazione a 5 volt
        - Una fonte di alimentazione a 5 V prelevata dalla porta micro USB del tuo Pico, usata per alimentare l'hardware che necessita di più di 3.3 V.

Il miglior posto per trovare tutto ciò di cui hai bisogno per iniziare con il tuo Raspberry Pi Pico W è `qui <https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html>`_.

Oppure puoi cliccare sui link qui sotto:

* `Scheda informativa del Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/pico-w-product-brief.pdf>`_
* `Scheda tecnica del Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf>`_
* `Iniziare con Raspberry Pi Pico: sviluppo in C/C++ <https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf>`_
* `SDK C/C++ di Raspberry Pi Pico <https://datasheets.raspberrypi.org/pico/raspberry-pi-pico-c-sdk.pdf>`_
* `Documentazione Doxygen a livello API per l'SDK C/C++ di Raspberry Pi Pico <https://raspberrypi.github.io/pico-sdk-doxygen/>`_
* `SDK Python di Raspberry Pi Pico <https://datasheets.raspberrypi.org/pico/raspberry-pi-pico-python-sdk.pdf>`_
* `Scheda tecnica RP2040 di Raspberry Pi <https://datasheets.raspberrypi.org/rp2040/rp2040-datasheet.pdf>`_
* `Progettazione hardware con RP2040 <https://datasheets.raspberrypi.org/rp2040/hardware-design-with-rp2040.pdf>`_
* `File di design del Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/RPi-PicoW-PUBLIC-20220607.zip>`_
* `File STEP del Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/PicoW-step.zip>`_