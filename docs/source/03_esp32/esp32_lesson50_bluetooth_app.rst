.. note::

    Ciao, benvenuto nella Comunità degli appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Perché Unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Impara & Condividi**: Scambia consigli e tutorial per potenziare le tue competenze.
    - **Anteprime Esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Sconti Speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _esp32_iot_bluetooth_app:

Lezione 50: Applicazione Android - Operazione LED RGB tramite Arduino e Bluetooth
======================================================================================

L'obiettivo di questo progetto è sviluppare un'applicazione Android capace di manipolare la tonalità di un LED RGB attraverso uno smartphone utilizzando la tecnologia Bluetooth.

Questa applicazione Android sarà costruita utilizzando una piattaforma web gratuita chiamata MIT App Inventor 2. Il progetto presenta un'eccellente opportunità per acquisire familiarità con l'interfaccia tra un Arduino e uno smartphone.


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
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_rgb`
        - \-

**1. Creazione dell'Applicazione Android**


L'applicazione Android sarà realizzata utilizzando una web application gratuita conosciuta come |link_appinventor|.
MIT App Inventor è un ottimo punto di partenza per lo sviluppo Android, grazie alle sue funzionalità intuitive di trascinamento che permettono la creazione di applicazioni semplificate.


Cominciamo.

#. Ecco la pagina di login: http://ai2.appinventor.mit.edu. Avrai bisogno di un account Google per registrarti a MIT App Inventor.

#. Dopo aver effettuato l'accesso, naviga in **Projects** -> **Import project (.aia) from my computer**. Successivamente, carica il file ``control_rgb_led.aia`` situato nel percorso ``esp32-starter-kit-main\c\codes\iot_10_bluetooth_app_inventor``.

   .. image:: img/10_ble_app_inventor1.png

#. Dopo aver caricato il file ``.aia``, vedrai l'applicazione su **MIT App Inventor**. Questo è un template pre-configurato. Puoi modificare questo template dopo aver acquisito familiarità con **MIT App Inventor** attraverso i passaggi seguenti.

   .. image:: img/10_ble_app_inventor2.png

#. In **MIT App Inventor**, hai 2 sezioni principali: il **Designer** e i **Blocchi**.

   .. image:: img/10_ble_app_inventor3.png

#. Il **Designer** ti permette di aggiungere pulsanti, testo, schermate e modificare l'estetica generale della tua applicazione.

   .. image:: img/10_ble_app_inventor2.png
   

#. Successivamente, hai la sezione **Blocchi**. La sezione **Blocchi** facilita la creazione di funzioni personalizzate per la tua applicazione.

   .. image:: img/10_ble_app_inventor5.png

#. Per installare l'applicazione su uno smartphone, naviga nella scheda **Build**.

   .. image:: img/10_ble_app_inventor6.png

   * Puoi generare un file ``.apk``. Dopo aver selezionato questa opzione, apparirà una pagina che ti permetterà di scegliere tra scaricare un file ``.apk`` o scansionare un codice QR per l'installazione. Segui la guida all'installazione per completare l'installazione dell'applicazione.
   * Se desideri caricare questa app su **Google Play** o un altro marketplace di app, puoi generare un file ``.aab``.


**2. Caricamento del codice**

#. Costruisci il circuito.

   .. image:: img/Lesson_28_RGB_LED_Module_esp32_bb.png

#. Successivamente, collega l'ESP32 al tuo computer tramite cavo USB.


#. Apri il file ``Lesson_50_Bluetooth_app_inventor.ino`` situato nella directory ``universal-maker-sensor-kit\esp32\Lesson_50_Bluetooth_app_inventor`` o copia il codice nell'Arduino IDE.

   .. raw:: html

      <iframe src=https://create.arduino.cc/editor/sunfounder01/07622bb5-31eb-4a89-b6f2-085f3332051f/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>





#. Dopo aver selezionato la scheda appropriata (**ESP32 Dev Module**) e la porta, clicca sul pulsante **Carica**.

**3. Connessione tra App e ESP32**

Assicurati che l'applicazione creata in precedenza sia installata sul tuo smartphone.

#. Inizialmente, attiva il **Bluetooth** sul tuo smartphone.

   .. image:: img/10_ble_mobile1.png
      :width: 500
      :align: center

#. Naviga nelle **Impostazioni Bluetooth** sul tuo smartphone e trova **ESP32RGB**.

   .. image:: img/10_ble_mobile2.png
      :width: 500
      :align: center


#. Dopo averlo cliccato, accetta la richiesta di **Accoppiamento** nella finestra popup.

   .. image:: img/10_ble_mobile3.png
      :width: 500
      :align: center

#. Ora apri l'applicazione **Control_RGB_LED** di recente installazione.

   .. image:: img/10_ble_mobile4.png
      :align: center

#. Nell'app, clicca su **Connetti Bluetooth** per stabilire una connessione tra l'app e l'ESP32.

   .. image:: img/10_ble_mobile5.png
      :width: 500
      :align: center

#. Seleziona il ``xx.xx.xx.xx.xx.xx ESP32RGB`` che compare. se hai modificato ``SerialBT.begin("ESP32RGB");`` nel codice, seleziona semplicemente il nome della tua impostazione.

   .. image:: img/10_ble_mobile6.png
      :width: 500
      :align: center

#. Se hai aspettato un po' e non vedi ancora nessun nome di dispositivo, potrebbe essere che questa APP non sia autorizzata a scandire i dispositivi circostanti. In questo caso, devi regolare manualmente le impostazioni.

   * Tieni premuta l'icona dell'APP e clicca su **Informazioni APP** risultanti. Se hai un altro metodo per accedere a questa pagina, segui quello.

      .. image:: img/10_ble_mobile8.png
         :width: 500
         :align: center

   * Naviga nella pagina **Permessi**.

      .. image:: img/10_ble_mobile9.png
         :width: 500
         :align: center

   * Trova **Dispositivi nelle vicinanze**, e seleziona **Sempre** per permettere a questa APP di scandire i dispositivi nelle vicinanze.

      .. image:: img/10_ble_mobile10.png
         :width: 500
         :align: center

   * Ora, riavvia l'APP e ripeti i passaggi 5 e 6 per connetterti con successo al Bluetooth.

#. Dopo una connessione riuscita, tornerai automaticamente alla pagina principale, dove verrà visualizzato connesso. Ora puoi regolare i valori RGB e cambiare il colore della visualizzazione RGB premendo il pulsante **Cambia Colore**.

   .. image:: img/10_ble_mobile7.png
      :width: 500
      :align: center
