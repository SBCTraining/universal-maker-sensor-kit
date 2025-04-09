.. note::

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e alle anteprime.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Omaggi**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_iot_owm:



Lezione 46: Meteo in Tempo Reale da @OpenWeatherMap
=======================================================

Il progetto IoT Open Weather Display sfrutta la scheda ESP32 e un modulo LCD I2C 1602 per creare un display di informazioni meteorologiche che recupera i dati dall'API di OpenWeatherMap. 

Questo progetto rappresenta un'eccellente introduzione all'utilizzo delle API, alla connettività Wi-Fi e alla visualizzazione dei dati su un modulo LCD utilizzando la scheda ESP32. Con l'IoT Open Weather Display, puoi accedere comodamente agli aggiornamenti meteorologici in tempo reale, rendendolo una soluzione ideale per ambienti domestici o uffici.

**Componenti Necessari**

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È sicuramente conveniente acquistare un kit completo, ecco il link:

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
    *   - :ref:`cpn_i2c_lcd1602`
        - |link_i2clcd1602_buy|

**Ottieni le chiavi API di OpenWeather**

|link_openweather| è un servizio online, di proprietà di OpenWeather Ltd, che fornisce dati meteorologici globali tramite API, inclusi dati meteorologici attuali, previsioni, nowcast e dati meteorologici storici per qualsiasi località geografica.

#. Visita |link_openweather| per accedere/creare un account.

    .. image:: img/OWM-1.png

#. Clicca sulla pagina delle API dalla barra di navigazione.

    .. image:: img/OWM-2.png

#. Trova **Current Weather Data** e clicca su Iscriviti.

    .. image:: img/OWM-3.png

#. Nella sezione **Current weather and forecasts collection**, iscriviti al servizio appropriato. Per il nostro progetto, la versione Gratuita è sufficiente.

    .. image:: img/OWM-4.png

#. Copia la chiave dalla pagina **API keys**.

    .. image:: img/OWM-5.png


**Completa il tuo dispositivo**

#. Costruisci il circuito.

    .. image:: img/Lesson_26_LCD1602_esp32_bb.png
        :width: 800

#. Apri il codice.

    * Apri il file ``Lesson_46_OpenWeatherMap.ino`` situato nella directory ``universal-maker-sensor-kit\esp32\Lesson_46_OpenWeatherMap``, o copia il codice nell'Arduino IDE.
    * Dopo aver selezionato la scheda (ESP32 Dev Module) e la porta appropriata, clicca sul pulsante **Carica**.
    * :ref:`unknown_com_port`
    * Le librerie ``LiquidCrystal I2C`` e ``Arduino_JSON`` sono utilizzate qui, puoi installarle dal **Library Manager**.

    .. raw:: html

        <iframe src=https://create.arduino.cc/editor/sunfounder01/5e262afa-97ca-45ba-807b-adf7650b30e8/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
         

#. Localizza le seguenti righe e modificale con il tuo ``<SSID>`` e ``<PASSWORD>``.


    .. code-block::  Arduino

        // Sostituisci le variabili successive con la tua combinazione SSID/Password
        const char* ssid = "<SSID>";
        const char* password = "<PASSWORD>";

#. Inserisci le chiavi API che hai copiato precedentemente in ``openWeatherMapApiKey``.

    .. code-block::  Arduino

        // Il tuo nome di dominio con percorso URL o indirizzo IP con percorso
        String openWeatherMapApiKey = "<openWeatherMapApiKey>";

#. Sostituisci con il codice del tuo paese e la città.

    .. code-block::  Arduino

        // Sostituisci con il codice del tuo paese e la città
        // Trova il codice del paese su https://openweathermap.org/find
        String city = "<CITY>";
        String countryCode = "<COUNTRY CODE>";

#. Dopo che il codice è stato eseguito, vedrai le informazioni meteorologiche e l'ora della tua località sul LCD I2C 1602.

.. note::
   Quando il codice è in esecuzione, se lo schermo è vuoto, puoi girare il potenziometro sul retro del modulo per aumentare il contrasto.

