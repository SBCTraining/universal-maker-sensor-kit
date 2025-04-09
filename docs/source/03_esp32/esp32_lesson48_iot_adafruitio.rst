.. note::

    Ciao, benvenuto nella Comunità degli appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato ai nuovi annunci di prodotto e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_adafruit_io:

Lezione 48: Monitoraggio di Temperatura e Umidità con Adafruit IO
===========================================================================

In questo progetto, ti guideremo su come utilizzare una popolare piattaforma IoT. Esistono molte piattaforme gratuite (o a basso costo) disponibili online per gli appassionati di programmazione. Alcuni esempi sono Adafruit IO, Blynk, Arduino Cloud, ThingSpeak, e così via. L'uso di queste piattaforme è abbastanza simile. Qui, ci concentreremo su Adafruit IO.

Scriveremo un programma Arduino che utilizza il sensore DHT11 per inviare letture di temperatura e umidità alla dashboard di Adafruit IO. Puoi anche controllare un LED nel circuito tramite un interruttore sulla dashboard.

**Componenti Necessari**

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - INTRODUZIONE COMPONENTE
        - LINK DI ACQUISTO

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|

**Configurazione della Dashboard**

#. Visita |link_adafruit_io|, quindi clicca su **Start for free** per creare un account gratuito.

   .. image:: img/sp230516_102503.png

#. Compila il modulo per creare un account.

   .. image:: img/sp230516_102629.png

#. Dopo aver creato un account Adafruit, dovrai riaprire Adafruit io. Clicca su **Dashboards**, poi su **New Dashboard**.

   .. image:: img/sp230516_103347.png

#. Crea un **New Dashboard**.

   .. image:: img/sp230516_103744.png

#. Entra nella nuova **Dashboard** creata e crea un nuovo blocco.

   .. image:: img/sp230516_104234.png

#. Crea 1 blocco **Toggle**.

   .. image:: img/sp230516_105727.png

#. Successivamente, dovrai creare un nuovo feed qui. Questo toggle verrà utilizzato per controllare il LED, e nomineremo questo feed "LED".

   .. image:: img/sp230516_105641.png

#. Verifica il feed **LED**, poi procedi al passaggio successivo.

   .. image:: img/sp230516_105925.png

#. Completa le impostazioni del blocco (principalmente Titolo del Blocco, Testo On e Testo Off), poi clicca sul pulsante **Create block** in basso a destra per finire.

   .. image:: img/sp230516_110124.png

#. Dovremo anche creare due **Text Blocks** successivamente. Saranno utilizzati per visualizzare la temperatura e l'umidità. Quindi, crea due feed denominati **temperature** e **humidity**.

   .. image:: img/sp230516_110657.png

#. Dopo la creazione, la tua Dashboard dovrebbe apparire così:

   .. image:: img/sp230516_111134.png

#. Puoi regolare il layout utilizzando l'opzione **Edit Layout** sulla Dashboard.

   .. image:: img/sp230516_111240.png

#. Clicca su **API KEY**, e vedrai visualizzati il tuo username e **API KEY**. Annota questi dati poiché ti serviranno per il tuo codice.

   .. image:: img/sp230516_111641.png

**Esecuzione del Codice**

.. |dht11_module| image:: img/Lesson_19_dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_48_iot_adafruitio_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/Lesson_19_dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_48_iot_adafruitio_new_bb.png
   :width: 500px

#. Costruisci il circuito. 

   .. note:: 
      Il kit può contenere diverse versioni del modulo DHT11. Si prega di confermare il metodo di cablaggio secondo il modulo che hai.
   
   .. csv-table:: 
      :header: "modulo", "diagramma"
      :widths: 25, 75
   
      |dht11_module|, |dht11_module_circuit|
      |dht11_module_withLED|, |dht11_module_withLED_circuit|

#. Poi, collega l'ESP32 al computer tramite il cavo USB.

#. Apri il codice.

   * Apri il file ``Lesson_48_Adafruit_IO.ino`` situato nella directory ``universal-maker-sensor-kit\esp32\Lesson_48_Adafruit_IO``, oppure copia il codice nell'Arduino IDE.
   * Dopo aver selezionato la scheda (ESP32 Dev Module) e la porta appropriata, clicca sul pulsante **Carica**.
   * :ref:`unknown_com_port`
   * Qui si utilizzano la ``Adafruit_MQTT Library`` e la ``DHT sensor library``, che puoi installare dal **Library Manager**.

   .. raw:: html

       <iframe src=https://create.arduino.cc/editor/sunfounder01/987fb2fd-47e9-4a73-9020-6b2111eadd9c/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Trova le seguenti righe e sostituisci ``<SSID>`` e ``<PASSWORD>`` con i dettagli specifici della tua rete WiFi.

   .. code-block::  Arduino

       /************************* WiFi Access Point *********************************/

       #define WLAN_SSID "<SSID>"
       #define WLAN_PASS "<PASSWORD>"

#. Poi sostituisci ``<YOUR_ADAFRUIT_IO_USERNAME>`` con il tuo username Adafruit IO e ``<YOUR_ADAFRUIT_IO_KEY>`` con la **API KEY** che hai appena copiato.

   .. code-block::  Arduino

       // Configurazione account Adafruit IO
       // (per ottenere questi valori, visita https://io.adafruit.com e clicca su Active Key)
       #define AIO_USERNAME "<YOUR_ADAFRUIT_IO_USERNAME>"
       #define AIO_KEY      "<YOUR_ADAFRUIT_IO_KEY>"

#. Dopo aver selezionato la scheda corretta (ESP32 Dev Module) e la porta, clicca sul pulsante **Carica**.

#. Una volta che il codice è stato caricato con successo, osserverai il seguente messaggio nel monitor seriale, indicando una comunicazione riuscita con Adafruit IO.
    
   .. code-block:: 

       Adafruit IO MQTTS (SSL/TLS) Example

       Connecting to xxxxx
       WiFi connected
       IP address: 
       192.168.18.76
       Connecting to MQTT... MQTT Connected!
       Temperature: 27.10
       Humidity: 61.00

#. Torna su Adafruit IO. Ora puoi osservare le letture di temperatura e umidità sulla dashboard, o utilizzare l'interruttore LED per controllare lo stato acceso/spento del LED esterno collegato al circuito.

   .. image:: img/sp230516_143220.png
