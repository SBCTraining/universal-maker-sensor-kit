.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per esplorare a fondo Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto del nostro team e della community.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a novità e anteprime sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _cpn_traffic:

Modulo Semaforo
==========================

.. image:: img/29_traffic_light.png
    :width: 400
    :align: center

.. raw:: html
    
    <br/>

Il modulo semaforo è un piccolo dispositivo che può visualizzare le luci rosse, gialle e verdi, proprio come un vero semaforo. Può essere utilizzato per creare un modello di sistema semaforico o per imparare a controllare i LED con Arduino. Si distingue per le sue dimensioni compatte, il cablaggio semplice, l’uso mirato e l’installazione personalizzata. Può essere collegato a un pin PWM per regolare la luminosità del LED.

Principio di funzionamento
-----------------------------
Il modulo semaforo può essere controllato principalmente in due modi. Il metodo più semplice utilizza gli ingressi digitali dell’Arduino, dove un segnale HIGH o LOW accende o spegne direttamente il LED corrispondente. In alternativa, può essere utilizzata la PWM (modulazione della larghezza dell’impulso), specialmente se si desidera regolare la luminosità del LED.  
Il PWM è una tecnica che modifica il duty cycle di un segnale digitale per modulare la luminosità del LED. Il duty cycle rappresenta la percentuale di tempo in cui un segnale rimane attivo durante un periodo specifico. Ad esempio, un duty cycle del 50% implica che il segnale è attivo per metà tempo e inattivo per l’altra metà. Regolando il duty cycle è possibile variare l’intensità luminosa del LED.

Schema elettrico
---------------------------

.. image:: img/29_traffic_light_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Esempi
---------------------------
* :ref:`uno_lesson29_traffic_light_module` (Arduino UNO)  
* :ref:`esp32_lesson29_traffic_light_module` (ESP32)  
* :ref:`pico_lesson30_relay_module` (Raspberry Pi Pico)  
* :ref:`pi_lesson30_relay_module` (Raspberry Pi)  

* :ref:`uno_lesson30_relay_module` (Arduino UNO)  

* :ref:`uno_lesson42_touch_toggle_light` (Arduino UNO)  
* :ref:`uno_lesson47_bluetooth_traffic_light` (Arduino UNO)  
* :ref:`esp32_touch_toggle_light` (ESP32)