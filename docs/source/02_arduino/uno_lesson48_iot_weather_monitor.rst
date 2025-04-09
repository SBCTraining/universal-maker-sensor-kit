.. note:: 
   Ciao, benvenuti nella Comunità degli Appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Approfondisci la tua conoscenza di Raspberry Pi, Arduino e ESP32 con altri appassionati.

   **Perché unirsi?**

   - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
   - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
   - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
   - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
   - **Promozioni Festive e Regali**: Partecipa a regali e promozioni festive.

   👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _uno_iot_weather_monito:

Lezione 48: Monitoraggio Meteo con ThingSpeak
=============================================================



Questo progetto raccoglie dati di temperatura e pressione utilizzando un Sensore di Pressione Atmosferica. I dati raccolti vengono poi trasmessi alla piattaforma cloud ThingSpeak tramite un modulo ESP8266 e una rete Wi-Fi a intervalli regolari.

Componenti Necessari
--------------------------

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

Puoi anche acquistarli separatamente dai link sottostanti.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione ai Componenti
        - Link di Acquisto

    *   - Arduino UNO R3 o R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_esp8266`
        - \-
    *   - :ref:`cpn_bmp280`
        - \-


Cablaggio
---------------------------

.. image:: img/Lesson_48_Iot_weather_monitor_uno_bb.png
    :width: 100%



Configurazione di ThingSpeak
-------------------------------

|link_thingspeak| ™ è un servizio di piattaforma analitica IoT che ti permette di aggregare, visualizzare e analizzare flussi di dati in tempo reale nel cloud. ThingSpeak fornisce visualizzazioni istantanee dei dati inviati dai tuoi dispositivi a ThingSpeak. Con la possibilità di eseguire codice MATLAB® in ThingSpeak, puoi eseguire analisi e elaborazioni dei dati in tempo reale. ThingSpeak è spesso utilizzato per prototipi e sistemi IoT di prova del concetto che richiedono analisi.

.. image:: img/signup_tsp_ml.png
    :width: 80% 
    :align: center

.. raw:: html
    
    <br/>  

**1) Creazione dell'account ThingSpeak**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

La prima cosa da fare è creare un account su ThingSpeak. Dalla collaborazione con MATLAB, puoi utilizzare le tue credenziali MathWorks per accedere a |link_thingspeak|.

Se non ne possiedi uno, devi creare un account con MathWorks e accedere all'applicazione ThingSpeak.

.. image:: img/05-thingspeak_signup_shadow.png
    :width: 50%
    :align: center


**2) Creazione del canale**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dopo aver effettuato l'accesso, crea un nuovo canale per archiviare i dati andando su "Canali" > "I Miei Canali" e cliccando su "Nuovo Canale".

.. image:: img/05-thingspeak_channel_1_shadow.png
    :width: 95%
    :align: center

Per questo progetto, dobbiamo creare un canale chiamato "**Weather Monitor**" con due campi: **Campo 1** per "**Temperatura**" e **Campo 2** per "**Pressione Atmosferica**".

.. image:: img/05-thingspeak_channel_2_shadow.png
    :width: 95%
    :align: center

.. raw:: html
    
    <br/>  


Codice
---------------------------


#. Apri il file ``Lesson_48_Iot_Weather_Monitor.ino`` nel percorso ``universal-maker-sensor-kit\arduino_uno\Lesson_48_Iot_Weather_Monitor``, o copia questo codice nell'**Arduino IDE**.

   .. note:: 
      Per installare la libreria, utilizza il Gestore Librerie di Arduino e cerca **"Adafruit BMP280"** e installala. 

   .. raw:: html
      
      <iframe src=https://create.arduino.cc/editor/sunfounder01/59eeae43-5dcc-46d7-833f-65fd2bdb3603/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Devi inserire il ``mySSID`` e il ``myPWD`` del WiFi che stai utilizzando. 

   .. code-block:: arduino

    String mySSID = "your_ssid";     // SSID WiFi
    String myPWD = "your_password";  // Password WiFi

#. Devi anche modificare il ``myAPI`` con la tua chiave API del canale ThingSpeak.

   .. code-block:: arduino
    
      String myAPI = "xxxxxxxxxxxx";  // Chiave API

   .. image:: img/05-thingspeak_api_shadow.png
       :width: 80%
       :align: center
   
   
   Qui puoi trovare **la tua unica CHIAVE API che devi mantenere privata**. 

#. Dopo aver selezionato la scheda corretta e la porta, clicca sul pulsante **Upload**.

#. Apri il monitor seriale (imposta il baudrate a **9600**) e attendi un prompt come una connessione riuscita che appaia.

   .. image:: img/05-ready_1_shadow.png
          :width: 95%

   .. image:: img/05-ready_2_shadow.png
          :width: 95%

Analisi del Codice
---------------------------


#. Inizializzazione e configurazione del Bluetooth

   .. code-block:: arduino

      // Impostazione della comunicazione con il modulo Bluetooth
      #include <SoftwareSerial.h>
      const int bluetoothTx = 3;
      const int bluetoothRx = 4;
      SoftwareSerial bleSerial(bluetoothTx, bluetoothRx);
   
   Iniziamo includendo la libreria SoftwareSerial, utile per la comunicazione Bluetooth. I pin TX e RX del modulo Bluetooth sono quindi definiti e associati ai pin 3 e 4 sull'Arduino. Infine, inizializziamo l'oggetto ``bleSerial`` per la comunicazione Bluetooth.

#. Definizioni dei pin dei LED

   .. code-block:: arduino

      // Numeri dei pin per ciascun LED
      const int rledPin = 10;  //rosso
      const int yledPin = 11;  //giallo
      const int gledPin = 12;  //verde

   Qui, definiamo a quali pin dell'Arduino sono connessi i nostri LED. Il LED rosso è sul pin 10, il giallo sul 11 e il verde sul 12.

#. Funzione setup()

   .. code-block:: arduino

      void setup() {
         pinMode(rledPin, OUTPUT);
         pinMode(yledPin, OUTPUT);
         pinMode(gledPin, OUTPUT);

         Serial.begin(9600);
         bleSerial.begin(9600);
      }

   Nella funzione ``setup()``, impostiamo i pin dei LED come ``OUTPUT``. Avviamo anche la comunicazione seriale sia per il modulo Bluetooth che per la seriale di default (collegata al computer) con un baud rate di 9600.

#. Ciclo principale loop() per la comunicazione Bluetooth

   .. code-block:: arduino

      void loop() {
         while (bleSerial.available() > 0) {
            character = bleSerial.read();
            Serial.println(character);

            if (character == 'R') {
               toggleLights(rledPin);
            } else if (character == 'Y') {
               toggleLights(yledPin);
            } else if (character == 'G') {
               toggleLights(gledPin);
            }
         }
      }

   All'interno del nostro ``loop()`` principale, controlliamo continuamente se sono disponibili dati dal modulo Bluetooth. Se riceviamo dati, leggiamo il carattere e lo visualizziamo nel monitor seriale. A seconda del carattere ricevuto (R, Y, o G), attiviamo il rispettivo LED usando la funzione ``toggleLights()``.

#. Funzione Toggle Lights

   .. code-block:: arduino

      void toggleLights(int targetLight) {
         digitalWrite(rledPin, LOW);
         digitalWrite(yledPin, LOW);
         digitalWrite(gledPin, LOW);

         digitalWrite(targetLight, HIGH);
      }

   Questa funzione, ``toggleLights()``, spegne prima tutti i LED. Dopo aver verificato che siano tutti spenti, accende il LED target specificato. Questo garantisce che solo un LED sia acceso alla volta.