

.. note::

    Ciao, benvenuto nella Comunità di appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_iot_intrusion_alert_system:

Lezione 49: Sistema di Notifica di Intrusione basato su Blynk
=============================================================

Questo progetto dimostra un semplice sistema di rilevamento di intrusione domestica utilizzando un sensore di movimento PIR (HC-SR501).
Quando il sistema è impostato sulla modalità "Assente" attraverso l'app Blynk, il sensore PIR monitora i movimenti.
Qualsiasi movimento rilevato attiva una notifica sull'app Blynk, allertando l'utente di una possibile intrusione.

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
    *   - :ref:`cpn_pir_motion`
        - \-


1. Assemblaggio del Circuito
------------------------------------

.. image:: img/Lesson_12_PIR_Module_esp32_bb.png
    :width: 100%
    :align: center

2. Configurazione Blynk
---------------------------

**2.1 Inizializzazione di Blynk**

#. Naviga fino a |link_blynk| e seleziona **START FREE**. 

   .. image:: img/09_blynk_access.png
        :width: 90%

#. Inserisci la tua email per avviare il processo di registrazione.

   .. image:: img/09_blynk_sign_in.png
        :width: 70%
        :align: center

#. Conferma la tua registrazione tramite email.

    .. image:: img/09_blynk_password.png
        :width: 90%

#. Dopo la conferma, apparirà il **Blynk Tour**. Si consiglia di selezionare "Salta". Se appare anche **Quick Start**, considera di saltarlo.

    .. image:: img/09_blynk_tour.png
        :width: 90%

**2.2 Creazione di un Template**

#. Prima, crea un template in Blynk. Segui le istruzioni successive per creare il template **Intrusion Alert System**.

    .. image:: img/09_create_template_1_shadow.png
        :width: 700
        :align: center

#. Assegna un nome al template, seleziona **Hardware ESP32**, e seleziona **Connection Type** come **WiFi**, poi seleziona **Done**.

    .. image:: img/09_create_template_2_shadow.png
        :width: 700
        :align: center

**2.3 Generazione dei Datastream**

Apri il template appena configurato, creiamo due datastream.

#. Clicca su **Nuovo Datastream**.

    .. image:: img/09_blynk_new_datastream.png
        :width: 700
        :align: center

#. Nella finestra popup, scegli **Virtual Pin**.

    .. image:: img/09_blynk_datastream_virtual.png
        :width: 700
        :align: center

#. Nominare il **Virtual Pin V0** come **Modalità Assente**. Imposta il **TIPO DI DATO** come **Intero** con valori **MIN** e **MAX** come **0** e **1**.

    .. image:: img/09_create_template_shadow.png
        :width: 700
        :align: center

#. Analogamente, crea un altro datastream **Virtual Pin**. Nominalo **Current Status** e imposta il **TIPO DI DATO** come **Stringa**.

    .. image:: img/09_datastream_1_shadow.png
        :width: 700
        :align: center

**2.4 Configurazione di un Evento**

Successivamente, configureremo un evento che invia una notifica via email se viene rilevata un'intrusione.

#. Clicca su **Aggiungi Nuovo Evento**.

    .. image:: img/09_blynk_event_add.png

#. Definisci il nome dell'evento e il suo codice specifico. Per **TYPE**, scegli **Warning** e scrivi una breve descrizione per l'email da inviare quando si verifica l'evento. Puoi anche regolare la frequenza delle notifiche.

    .. note::
        
        Assicurati che il **EVENT CODE** sia impostato come ``intrusion_detected``. Questo è predefinito nel codice, quindi eventuali modifiche richiederebbero un aggiustamento del codice.

    .. image:: img/09_event_1_shadow.png
        :width: 700
        :align: center

#. Vai alla sezione **Notifications** per attivare le notifiche e configurare i dettagli dell'email.

    .. image:: img/09_event_2_shadow.png
        :width: 80%
        :align: center

.. raw:: html
    
    <br/> 

**2.5 Perfezionamento del Web Dashboard**

Assicurarsi che il **Web Dashboard** interagisca perfettamente con il Sistema di Allarme Intrusione è fondamentale.

#. Semplicemente trascina e posiziona sia il **Widget Interruttore** che il **Widget Etichetta** sul **Web Dashboard**.

    .. image:: img/09_web_dashboard_1_shadow.png
        :width: 100%
        :align: center

#. Quando passi il mouse sopra un widget, appariranno tre icone. Utilizza l'icona delle impostazioni per regolare le proprietà del widget.

    .. image:: img/09_blynk_dashboard_set.png
        :width: 100%
        :align: center

#. Nelle impostazioni del **Widget Interruttore**, seleziona **Datastream** come **Modalità Assente(V0)**. Imposta **ONLABEL** e **OFFLABEL** per visualizzare rispettivamente **"assente"** e **"casa"**.

    .. image:: img/09_web_dashboard_2_shadow.png
        :width: 100%
        :align: center

#. Nelle impostazioni del **Widget Etichetta**, seleziona **Datastream** come **Stato Corrente(V1)**.

    .. image:: img/09_web_dashboard_3_shadow.png
        :width: 100%
        :align: center

**2.6 Salvataggio del Template**

Infine, non dimenticare di salvare il tuo template.

    .. image:: img/09_save_template_shadow.png
        :width: 100%
        :align: center

**2.7 Creazione di un Dispositivo**

#. È il momento di creare un nuovo dispositivo.

    .. image:: img/09_blynk_device_new.png
        :width: 700
        :align: center

#. Clicca su **Da template** per iniziare con una nuova configurazione.

    .. image:: img/09_blynk_device_template.png
        :width: 700
        :align: center

#. Poi, scegli il template **Sistema di Allarme Intrusione** e clicca su **Crea**.

    .. image:: img/09_blynk_device_template2.png
        :width: 700
        :align: center

#. Qui, vedrai il ``Template ID``, ``Device Name``, e ``AuthToken``. Devi copiare questi nel tuo codice affinché l'ESP32 possa lavorare con Blynk.

    .. image:: img/09_blynk_device_code.png
        :width: 700
        :align: center

3. Esecuzione del Codice
-----------------------------
#. Prima di eseguire il codice, assicurati di installare la libreria ``Blynk`` dal **Library Manager** su Arduino IDE.

    .. image:: img/09_blynk_add_library.png
        :width: 700
        :align: center

#. Apri il file ``Lesson_49_Blynk_based_intrusion_system.ino``, che si trova nella directory ``universal-maker-sensor-kit\esp32\Lesson_49_Blynk_based_intrusion_system``. Puoi anche copiarne il contenuto nell'Arduino IDE.

    .. raw:: html

        <iframe src="https://app.arduino.cc/sketches/ddb3006a-befa-46c4-bc71-9e32bcfbe31d?view-mode=embed" style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
        

#. Sostituisci i segnaposto per ``BLYNK_TEMPLATE_ID``, ``BLYNK_TEMPLATE_NAME``, e ``BLYNK_AUTH_TOKEN`` con i tuoi ID unici.

    .. code-block:: arduino
    
        #define BLYNK_TEMPLATE_ID "TMPxxxxxxx"
        #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
        #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxx"

#. Devi anche inserire il ``ssid`` e la ``password`` della tua rete WiFi.

   .. code-block:: arduino

        char ssid[] = "your_ssid";
        char pass[] = "your_password";

#. Scegli la scheda corretta (**ESP32 Dev Module**) e la porta, poi clicca sul pulsante **Carica**.

#. Apri il monitor seriale (imposta il baud rate a 115200) e attendi un messaggio di connessione riuscita.

    .. image:: img/09_blynk_upload_code.png
        :align: center

#. Dopo una connessione riuscita, attivando l'interruttore in Blynk avvierà la sorveglianza del modulo PIR. Quando viene rilevato un movimento (stato di 1), dirà, "C'è qualcuno qui!" e invierà un allarme alla tua email.

    .. image:: img/09_blynk_code_alarm.png
        :width: 700
        :align: center

4. Spiegazione del Codice
-----------------------------

#. **Configurazione & Librerie**

   Qui, configuri le costanti Blynk e le credenziali. Includi anche le librerie necessarie per l'ESP32 e Blynk.

    .. code-block:: arduino

        /* Comment this out to disable prints and save space */
        #define BLYNK_PRINT Serial

        #define BLYNK_TEMPLATE_ID "xxxxxxxxxxx"
        #define BLYNK_TEMPLATE_NAME "Intrusion Alert System"
        #define BLYNK_AUTH_TOKEN "xxxxxxxxxxxxxxxxxxxxxxxxxxx"

        #include <WiFi.h>
        #include <WiFiClient.h>
        #include <BlynkSimpleEsp32.h>

#. **Configurazione WiFi**

   Inserisci le tue credenziali WiFi.

   .. code-block:: arduino

        char ssid[] = "your_ssid";
        char pass[] = "your_password";

#. **Configurazione Sensore PIR**

   Imposta il pin dove è collegato il sensore PIR e inizializza le variabili di stato.

   .. code-block:: arduino

      const int sensorPin = 14;
      int state = 0;
      int awayHomeMode = 0;
      BlynkTimer timer;

#. **Funzione setup()**

   Questa funzione inizializza il sensore PIR come input, configura la comunicazione seriale, si connette al WiFi e configura Blynk.

   - Usiamo ``timer.setInterval(1000L, myTimerEvent)`` per impostare l'intervallo del timer in ``setup()``, qui impostiamo l'esecuzione della funzione ``myTimerEvent()`` ogni **1000ms**. Puoi modificare il primo parametro di ``timer.setInterval(1000L, myTimerEvent)`` per cambiare l'intervallo tra le esecuzioni di ``myTimerEvent``.

   .. raw:: html
    
    <br/> 

   .. code-block:: arduino

        void setup() {

            pinMode(sensorPin, INPUT);  // Imposta il pin del sensore PIR come input
            Serial.begin(115200);           // Avvia la comunicazione seriale a 115200 baud per il debugging
            
            // Configura Blynk e connettiti al WiFi
            Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);
            
            timer.setInterval(1000L, myTimerEvent);  // Imposta una funzione da chiamare ogni secondo
        }

#. **Funzione loop()**

   La funzione loop esegue continuamente Blynk e le funzioni del timer Blynk.

   .. code-block:: arduino

        void loop() {
           Blynk.run();
           timer.run();
        }

#. **Interazione con l'App Blynk**

   Queste funzioni vengono chiamate quando il dispositivo si connette a Blynk e quando c'è un cambiamento nello stato del pin virtuale V0 sull'app Blynk.

   - Ogni volta che il dispositivo si connette al server Blynk, o si riconnette a causa di condizioni di rete scadenti, viene chiamata la funzione ``BLYNK_CONNECTED()``. Il comando ``Blynk.syncVirtual()`` richiede un singolo valore di Pin Virtuale. Il Pin Virtuale specificato eseguirà la chiamata ``BLYNK_WRITE()``. 

   - Ogni volta che il valore di un pin virtuale sul server BLYNK cambia, scatenerà ``BLYNK_WRITE()``.

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

   Ogni secondo, la funzione ``myTimerEvent()`` chiama ``sendData()``. Se la modalità assente è abilitata su Blynk, controlla il sensore PIR e invia una notifica a Blynk se viene rilevato un movimento.

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

              // Se il sensore rileva un movimento, invia un allarme all'app Blynk
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
