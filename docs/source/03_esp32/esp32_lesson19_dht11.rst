.. note::

    Ciao, benvenuto nella Comunità di Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci le tue conoscenze su Raspberry Pi, Arduino e ESP32 con altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con il supporto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato ad annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_lesson19_dht11:

Lezione 19: Modulo Sensore di Temperatura e Umidità (DHT11)
====================================================================

In questa lezione, imparerai come leggere la temperatura e l'umidità da un sensore DHT11 utilizzando una scheda di sviluppo ESP32. Copriremo anche l'interpretazione di queste letture e il calcolo dell'indice di calore sia in gradi Celsius che Fahrenheit. Questo progetto è ideale per i principianti nel campo della rilevazione ambientale, offrendo esperienza pratica nell'acquisizione dei dati dei sensori e nei concetti di base del monitoraggio climatico sulla piattaforma ESP32.

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
    *   - Kit Sensori Universale Maker
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Introduzione al Componente
        - Link d'acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_dht11`
        - |link_dht11_humiture_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
 

Cablaggio
---------------------------

.. note:: 
   Il kit può contenere diverse versioni del modulo DHT11. Si prega di confermare il metodo di cablaggio secondo il modulo che si possiede.

.. csv-table:: 
   :header: "module", "diagram"
   :widths: 25, 75

   |dht11_module|, |dht11_module_circuit|
   |dht11_module_withLED|, |dht11_module_withLED_circuit|

.. |dht11_module| image:: img/Lesson_19_dht11_module.png 
   :width: 100px

.. |dht11_module_circuit| image:: img/Lesson_19_DHT11_esp32_bb.png
   :width: 500px

.. |dht11_module_withLED| image:: img/Lesson_19_dht11_module_withLED.png
   :width: 150px

.. |dht11_module_withLED_circuit| image:: img/Lesson_19_DHT11_esp32_new_bb.png
   :width: 500px

Codice
---------------------------

.. note:: 
   Per installare la libreria, usa il Gestore delle Librerie di Arduino e cerca **"DHT sensor library"** e installala.

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/926830ca-9421-4852-ad72-ff75c1f10174/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

Analisi del Codice
---------------------------

1. Inclusione delle librerie necessarie e definizione delle costanti.
   Questa parte del codice include la libreria del sensore DHT e definisce il numero del pin e il tipo di sensore utilizzati in questo progetto.

   .. note:: 
      Per installare la libreria, usa il Gestore delle Librerie di Arduino e cerca **"DHT sensor library"** e installala.

   .. code-block:: arduino
    
      #include <DHT.h>
      #define DHTPIN 25       // Definisci il pin utilizzato per collegare il sensore
      #define DHTTYPE DHT11  // Definisci il tipo di sensore

2. Creazione dell'oggetto DHT.
   Qui creiamo un oggetto DHT usando il numero del pin e il tipo di sensore definiti.

   .. code-block:: arduino

      DHT dht(DHTPIN, DHTTYPE);  // Crea un oggetto DHT

3. Questa funzione viene eseguita una volta all'avvio della scheda di sviluppo ESP32. Inizializziamo la comunicazione seriale e il sensore DHT in questa funzione.

   .. code-block:: arduino

      void setup() {
        Serial.begin(9600);
        Serial.println(F("DHT11 test!"));
        dht.begin();  // Inizializza il sensore DHT
      }

4. Ciclo principale.
   La funzione ``loop()`` viene eseguita continuamente dopo la funzione di setup. Qui, leggiamo i valori di umidità e temperatura, calcoliamo l'indice di calore e stampiamo questi valori sul monitor seriale.  Se la lettura del sensore fallisce (ritorna NaN), stampa un messaggio di errore.

   .. note::
    
      L' |link_heat_index| è un modo per misurare quanto caldo si sente all'esterno combinando la temperatura dell'aria e l'umidità. È anche chiamato "temperatura percepita" o "temperatura apparente".

   .. code-block:: arduino

      void loop() {
        delay(2000);
        float h = dht.readHumidity();
        float t = dht.readTemperature();
        float f = dht.readTemperature(true);
        if (isnan(h) || isnan(t) || isnan(f)) {
          Serial.println(F("Failed to read from DHT sensor!"));
          return;
        }
        float hif = dht.computeHeatIndex(f, h);
        float hic = dht.computeHeatIndex(t, h, false);
        Serial.print(F("Humidity: "));
        Serial.print(h);
        Serial.print(F("%  Temperature: "));
        Serial.print(t);
        Serial.print(F("°C "));
        Serial.print(f);
        Serial.print(F("°F  Heat index: "));
        Serial.print(hic);
        Serial.print(F("°C "));
        Serial.print(hif);
        Serial.println(F("°F"));
      }