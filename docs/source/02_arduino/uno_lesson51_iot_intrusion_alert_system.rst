
.. note:: 

   Ciao, benvenuti nella Comunità degli Appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Esplorate più a fondo Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

   **Perché unirsi?**

   - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
   - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
   - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime.
   - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
   - **Promozioni Festive e Regali**: Partecipa a regali e promozioni festive.

   👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _uno_iot_intrusion_alert_system:

Lezione 51: Sistema di Allarme Intrusione con Blynk
===================================================================



Questo progetto dimostra un semplice sistema di rilevamento intrusione domestico utilizzando un sensore a infrarossi passivi (PIR) (HC-SR501).
Quando il sistema è impostato sulla modalità 'Assente' attraverso l'app Blynk, il sensore PIR monitora i movimenti.
Qualsiasi movimento rilevato attiva una notifica sull'app Blynk, allertando l'utente di una possibile intrusione.


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
    *   - :ref:`cpn_pir_motion`
        - \-


Cablaggio
---------------------------

.. image:: img/Lesson_51_Iot_intrusion_alert_system_uno_bb.png
    :width: 100%


Configurazione di Blynk
-----------------------------

.. note::
    Se non sei familiare con Blynk, è vivamente consigliato leggere prima questi due tutorial. :ref:`iot_blynk_start` è una guida per principianti su Blynk, che include come configurare ESP8266 e registrarsi su Blynk. E :ref:`uno_iot_Flame` è un esempio semplice, ma la descrizione dei passaggi sarà più dettagliata.

**1 Crea un template**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Prima di tutto, dobbiamo stabilire un template su Blynk. Segui i passaggi sottostanti per creare un template **"Sistema di Allarme Intrusione"**.

.. image:: img/02-create_template_shadow.png
    :width: 80%
    :align: center

**2 Datastream**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Crea **Datastreams** di tipo **Pin Virtuale** nella pagina **Datastream** per ricevere dati da esp8266 e dalla scheda uno r4.

* Crea il Pin Virtuale V0 secondo il seguente schema:

  Imposta il nome del **Pin Virtuale V0** su **Modalità Assente**. Imposta il **TIPO DI DATO** su **Integer** e MIN e MAX su **0** e **1**.

  .. image:: img/02-datastream_1_shadow.png
      :width: 90%

* Crea il Pin Virtuale V1 secondo il seguente schema:

  Imposta il nome del **Pin Virtuale V1** su **Stato Corrente**. Imposta il **TIPO DI DATO** su **Stringa**.

  .. image:: img/02-datastream_2_shadow.png
      :width: 90%

Assicurati di avere impostato due Pin Virtuali secondo i passaggi sopra.

.. image:: img/02-datastream_3_shadow.png
    :width: 100%


.. raw:: html
    
    <br/> 

**3 Evento**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Successivamente, creeremo un **evento** che registra il rilevamento di intrusione e invia una notifica via email.

.. note::
    Si raccomanda di mantenere le impostazioni coerenti con le mie, altrimenti potrebbe essere necessario modificare il codice per eseguire il progetto. Assicurati che il **CODICE EVENTO** sia impostato su ``intrusion_detected``.

.. image:: img/02-event_1_shadow.png
    :width: 90%
    :align: center

Vai alla pagina **Notifications** e configura le impostazioni email.

.. image:: img/02-event_2_shadow.png
    :width: 90%
    :align: center

.. raw:: html
    
    <br/> 

**4 Web Dashboard**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dobbiamo anche configurare il **Web Dashboard** per interagire con il Sistema di Allarme Intrusione.

Trascina e rilascia un **Widget Interruttore** e un **Widget Etichetta** nella pagina **Web Dashboard**.

.. image:: img/02-web_dashboard_1_shadow.png
    :width: 100%
    :align: center

Nella pagina delle impostazioni del **Widget Interruttore**, seleziona **Datastream** come **Modalità Assente(V0)**. Imposta **ONLABEL** e **OFFLABEL** per mostrare "fuori casa" quando l'interruttore è acceso, e "a casa" quando è spento.

.. image:: img/02-web_dashboard_2_shadow.png
    :width: 100%
    :align: center

Nella pagina delle impostazioni del **Widget Etichetta**, seleziona **Datastream** come **Stato Corrente(V1)**.

.. image:: img/02-web_dashboard_3_shadow.png
    :width: 100%
    :align: center

**5 Salva il template**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Infine, ricorda di salvare il template.

.. image:: img/02-save_template_shadow.png
    :width: 70%
    :align: center

.. raw:: html
    
    <br/>  


Codice
-----------------------

#. Apri il file ``Lesson_51_Intrusion_alert_system.ino`` nel percorso ``universal-maker-sensor-kit\arduino_uno\Lesson_51_Intrusion_alert_system``, o copia questo codice nell'**Arduino IDE**.

   .. raw:: html
       
       <iframe src=https://create.arduino.cc/editor/sunfounder01/e94c0b5e-1fcd-46aa-bc95-0395efee1d32/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>

#. Crea un dispositivo Blynk utilizzando il template "Sistema di Allarme Intrusione". Poi, sostituisci ``BLYNK_TEMPLATE_ID``, ``BLYNK_TEMPLATE_NAME``, e ``BLYNK_AUTH_TOKEN`` con i tuoi. 

   .. code-block:: arduino
    
      #define BLYNK_TEMPLATE_ID "TMPxxxxxxx"
      #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
      #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxx"

#. Devi anche inserire il ``ssid`` e la ``password`` del WiFi che stai utilizzando. 

   .. code-block:: arduino

    char ssid[] = "your_ssid";
    char pass[] = "your_password";

#. Dopo aver selezionato la scheda e la porta corretti, clicca sul pulsante **Upload**.

#. Apri il monitor seriale (imposta il baudrate a 115200) e attendi un prompt come una connessione riuscita che appaia.

   .. image:: img/02-ready_1_shadow.png
    :width: 80%
    :align: center

   .. note::

       Se appare il messaggio ``ESP is not responding`` quando ti connetti, segui questi passaggi.

       * Assicurati che la batteria da 9V sia collegata.
       * Resetta il modulo ESP8266 collegando il pin RST a GND per 1 secondo, poi scollegarlo.
       * Premi il pulsante di reset sulla scheda R4.

       A volte, potrebbe essere necessario ripetere l'operazione sopra 3-5 volte, per favore sii paziente.


Analisi del Codice
---------------------------

#. **Configurazione & Librerie**

   Qui, vengono impostate le credenziali e le costanti per Blynk. Sono incluse le librerie necessarie per il modulo WiFi ESP8266 e Blynk.

   .. code-block:: arduino

      #define BLYNK_TEMPLATE_ID "TMPxxxx"
      #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
      #define BLYNK_AUTH_TOKEN "xxxxxx-"
      #define BLYNK_PRINT Serial

      #include <ESP8266_Lib.h>
      #include <BlynkSimpleShieldEsp8266.h>

#. **Configurazione WiFi**

   Configura le credenziali WiFi e imposta la comunicazione seriale software con il modulo ESP01.

   .. code-block:: arduino

      char ssid[] = "your_ssid";
      char pass[] = "your_password";

      SoftwareSerial EspSerial(2, 3);
      #define ESP8266_BAUD 115200
      ESP8266 wifi(&EspSerial);

#. **Configurazione Sensore PIR**

   Definisci il pin dove è collegato il sensore PIR e inizializza le variabili di stato.

   .. code-block:: arduino

      const int sensorPin = 8;
      int state = 0;
      int awayHomeMode = 0;
      BlynkTimer timer;

#. **Funzione setup()**

   Questa inizializza il sensore PIR come input, configura la comunicazione seriale, si connette al WiFi e configura Blynk.

   - Usiamo ``timer.setInterval(1000L, myTimerEvent)`` per impostare l'intervallo del timer in setup(), qui impostiamo per eseguire la funzione ``myTimerEvent()`` ogni **1000ms**. Puoi modificare il primo parametro di ``timer.setInterval(1000L, myTimerEvent)`` per cambiare l'intervallo tra le esecuzioni di ``myTimerEvent``.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

      void setup() {
         pinMode(sensorPin, INPUT);
         Serial.begin(115200);
         EspSerial.begin(ESP8266_BAUD);
         delay(10);
         Blynk.config(wifi, BLYNK_AUTH_TOKEN);
         Blynk.connectWiFi(ssid, pass);
         timer.setInterval(1000L, myTimerEvent);
      }

#. **Funzione loop()**

   La funzione loop esegue ripetutamente le funzioni Blynk e del timer Blynk.

   .. code-block:: arduino

      void loop() {
         Blynk.run();
         timer.run();
      }

#. **Interazione con l'App Blynk**

   Queste funzioni vengono chiamate quando il dispositivo si connette a Blynk e quando c'è un cambiamento nello stato del pin virtuale V0 sull'app Blynk.

   - Ogni volta che il dispositivo si connette al server Blynk, o si riconnette a causa di condizioni di rete scarse, la funzione ``BLYNK_CONNECTED()`` viene chiamata. Il comando ``Blynk.syncVirtual()`` richiede il valore di un singolo Pin Virtuale. Il Pin Virtuale specificato eseguirà la chiamata ``BLYNK_WRITE()``. Per maggiori dettagli, consulta |link_blynk_syncing|.

   - Ogni volta che il valore di un pin virtuale sul server BLYNK cambia, verrà attivato ``BLYNK_WRITE()``. Maggiori dettagli su |link_blynk_write|.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino
      
      // Questa funzione viene chiamata ogni volta che il dispositivo è connesso a Blynk.Cloud
      BLYNK_CONNECTED() {
         Blynk.syncVirtual(V0);
      }
      
      // Questa funzione viene chiamata ogni volta che lo stato del Pin Virtuale 0 cambia
      BLYNK_WRITE(V0) {
         awayHomeMode = param.asInt();
         // logica aggiuntiva
      }

#. **Gestione dei Dati**

   Ogni secondo, la funzione ``myTimerEvent()`` chiama ``sendData()``. Se la modalità assente è abilitata su Blynk, verifica il sensore PIR e invia una notifica a Blynk se viene rilevato un movimento.

   - Usiamo ``Blynk.virtualWrite(V1, "Somebody in your house! Please check!");`` per cambiare il testo di un'etichetta.

   - Usa ``Blynk.logEvent("intrusion_detected");`` per registrare l'evento su Blynk.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

      void myTimerEvent() {
         sendData();
      }

      void sendData() {
         if (awayHomeMode == 1) {
            state = digitalRead(sensorPin);  // Leggi lo stato del sensore PIR

            Serial.print("state:");
            Serial.println(state);
        
            // Se il sensore rileva movimento, invia un allarme all'app Blynk
            if (state == HIGH) {
              Serial.println("Somebody here!");
              Blynk.virtualWrite(V1, "Somebody in your house! Please check!");
              Blynk.logEvent("intrusion_detected");
            }
         }
      }


**Riferimenti**

- |link_blynk_doc|
- |link_blynk_quickstart| 
- |link_blynk_virtualWrite|
- |link_blynk_logEvent|
- |link_blynk_timer_intro|
- |link_blynk_syncing| 
- |link_blynk_write|