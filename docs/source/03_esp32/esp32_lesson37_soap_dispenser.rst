.. note::

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino e ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza di Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato alle nuove annunci di prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_soap_dispenser:

Lezione 37: Distributore Automatico di Sapone
=================================================

Il progetto del Distributore Automatico di Sapone utilizza una scheda Arduino Uno 
insieme a un sensore ad infrarossi per l'evitamento degli ostacoli e una pompa ad 
acqua. Il sensore rileva la presenza di un oggetto come una mano, che attiva la 
pompa dell'acqua per erogare il sapone.

Componenti Necessari
--------------------------

In questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ELEMENTI IN QUESTO KIT
        - LINK
    *   - Kit Sensori per Maker Universali
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link per l'Acquisto

    *   - ESP32 & Scheda di Sviluppo (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_ir_obstacle`
        - |link_obstacle_avoidance_module_buy|
    *   - :ref:`cpn_pump`
        - \-
    *   - :ref:`cpn_l9110`
        - \-
    *   - :ref:`cpn_power_module`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Cablaggio
-------------

.. image:: img/Lesson_37_Automatic_soap_dispenser_esp32_bb.png
    :width: 100%


Codice
------------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/f1923f60-5b82-497b-915f-ecc7ad46fea4/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>
    
Analisi del Codice
-------------------------

L'idea principale di questo progetto è creare un sistema di erogazione del sapone senza l'uso delle mani. Il sensore ad infrarossi per l'evitamento degli ostacoli rileva quando un oggetto (come una mano) è vicino. Al rilevamento di un oggetto, il sensore invia un segnale all'Arduino, che a sua volta attiva la pompa dell'acqua per erogare il sapone. La pompa rimane attiva per un breve periodo, erogando il sapone, poi si spegne.

1. **Definizione dei pin per il sensore e la pompa**

    In questo frammento di codice, definiamo i pin di Arduino che si collegano al sensore e alla pompa.
    Definiamo il pin 7 come il pin del sensore e useremo la variabile ``sensorValue`` per memorizzare i dati letti da questo sensore.
    Per la pompa dell'acqua, usiamo due pin, 9 e 10.
    
    .. code-block:: arduino
   
        // Definire i numeri dei pin per il sensore ad infrarossi per l'evitamento degli ostacoli
        const int sensorPin = 35;
        int sensorValue;

        // Definire i numeri dei pin per la pompa dell'acqua
        const int pump1A = 19;
        const int pump1B = 21;

2. **Impostazione del sensore e della pompa**

    Nella funzione ``setup()``, definiamo le modalità per i pin che stiamo usando.
    Il pin del sensore è impostato su ``INPUT`` poiché sarà utilizzato per ricevere dati dal sensore.
    I pin della pompa sono impostati su ``OUTPUT`` poiché invieranno comandi alla pompa.
    Assicuriamo che il pin ``pump1B`` inizi in stato ``LOW`` (spento),
    e iniziamo la comunicazione seriale con un baud rate di 9600.

    .. code-block:: arduino
    
        void setup() {
            // Impostare il pin del sensore come input
            pinMode(sensorPin, INPUT);

            // Inizializzare i pin della pompa come output
            pinMode(pump1A, OUTPUT);    
            pinMode(pump1B, OUTPUT);    

            // Mantenere pump1B basso
            digitalWrite(pump1A, LOW); 
            digitalWrite(pump1B, LOW);  

            Serial.begin(9600);
        }

3. **Controllo continuo del sensore e gestione della pompa**

   Nella funzione ``loop()``, l'Arduino legge costantemente il valore dal sensore usando ``digitalRead()`` e lo assegna a ``sensorValue()``. Poi stampa questo valore sul monitor seriale a scopo di debug. Se il sensore rileva un oggetto, ``sensorValue()`` sarà 0. Quando ciò accade, ``pump1A`` viene impostato su ``HIGH``, attivando la pompa, e un ritardo di 700 millisecondi permette alla pompa di erogare il sapone. La pompa viene poi disattivata impostando ``pump1A`` su ``LOW``, e un ritardo di 1 secondo dà tempo all'utente di allontanare la mano prima che il ciclo si ripeta.

   .. note:: 
   
      Se il sensore non funziona correttamente, regola il trasmettitore e il ricevitore IR per renderli paralleli. Inoltre, puoi ajustare il raggio di rilevamento usando il potenziometro incorporato.

   .. code-block:: arduino
   
        void loop() {
            sensorValue = digitalRead(sensorPin);
            Serial.println(sensorValue);

            // Se viene rilevato un oggetto, accendere la pompa per un breve periodo, poi spegnerla
            if (sensorValue == 0) {  
                digitalWrite(pump1A, HIGH);
                delay(700);
                digitalWrite(pump1A, LOW);
                delay(1000);
            }
        }
