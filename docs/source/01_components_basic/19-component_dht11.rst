.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati e maker.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a omaggi e promozioni speciali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _cpn_dht11:

Modulo Sensore di Temperatura e Umidità (DHT11)
================================================

.. image:: img/19_dht11_module.png
    :width: 360
    :align: center

.. raw:: html

   <br/>

Il DHT11 è un sensore digitale combinato che misura temperatura e umidità, fornendo un’uscita a segnale digitale calibrata. Combina un modulo digitale dedicato con tecnologia di rilevamento della temperatura e dell’umidità, garantendo elevata affidabilità e un’ottima stabilità a lungo termine.

Specifiche
---------------------------
* Tensione di alimentazione: 3.3V - 5V  
* Tipo di segnale in uscita: Digitale  
* Intervallo di misura della temperatura: 0-50℃ ± 2℃  
* Intervallo di misura dell’umidità: 20-90%RH ± 5%RH  
* Precisione temperatura: ±2°C  
* Precisione umidità: ±5% RH

Pinout
---------------------------
* **VCC**: Ingresso di alimentazione positiva dal controllore principale.  
* **GND**: Collegamento a massa.  
* **S**: Questo pin trasmette i dati di temperatura e umidità al microcontrollore utilizzando un protocollo unidirezionale su singolo filo.

Principio di funzionamento
-----------------------------
Il modulo utilizza solo tre pin: VCC, GND e DATA. La comunicazione inizia con l’invio di un segnale di start sulla linea DATA verso il DHT11. Il DHT11 risponde con un segnale di conferma e successivamente invia 40 bit di dati relativi a umidità e temperatura (8 bit interi umidità + 8 bit decimali umidità + 8 bit interi temperatura + 8 bit decimali temperatura + 8 bit checksum).

.. image:: img/19_dht11_module_2.png
    :width: 300
    :align: center

.. raw:: html
    
    <br/>

Schema elettrico
---------------------------

.. csv-table:: 
   :widths: 30, 70

   |dht11_module|, |dht11_module_schematic|  
   |dht11_module_withLED|, |dht11_module_withLED_schematic|  

.. |dht11_module| image:: img/19_dht11_module.png  
   :width: 100px  
.. |dht11_module_withLED| image:: img/19_dht11_module_withLED.png  
   :width: 150px  
.. |dht11_module_schematic| image:: img/19_dht11_module_schematic.png  
   :width: 360px  
.. |dht11_module_withLED_schematic| image:: img/19_dht11_module_withLED_schematic.png  
   :width: 360px  


Esempi
---------------------------
* :ref:`uno_lesson19_dht11` (Arduino UNO)  
* :ref:`esp32_lesson19_dht11` (ESP32)  
* :ref:`pico_lesson19_dht11` (Raspberry Pi Pico)  
* :ref:`pi_lesson19_dht11` (Raspberry Pi)  

* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)  
* :ref:`esp32_plant_monitor` (ESP32)  
* :ref:`esp32_adafruit_io` (ESP32)