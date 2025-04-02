.. note::

   Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

   **Warum beitreten?**

   - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
   - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
   - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
   - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
   - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

   👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _uno_iot_weather_monito:

Lesson 48: Wetterüberwachung mit ThingSpeak
=============================================================

Dieses Projekt sammelt Temperatur- und Druckdaten mithilfe eines atmosphärischen Drucksensors. Die gesammelten Daten werden dann in regelmäßigen Zeitintervallen über ein ESP8266-Modul und ein Wi-Fi-Netzwerk an die ThingSpeak-Cloud-Plattform übertragen.

Benötigte Komponenten
--------------------------

Für dieses Projekt benötigen wir folgende Komponenten.

Es ist definitiv praktisch, ein ganzes Kit zu kaufen, hier ist der Link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Name	
        - ITEMS IN THIS KIT
        - LINK
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Sie können sie auch separat von den untenstehenden Links kaufen.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Component Introduction
        - Purchase Link

    *   - Arduino UNO R3 or R4
        - |link_Uno_R3_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
    *   - :ref:`cpn_esp8266`
        - \-
    *   - :ref:`cpn_bmp280`
        - \-


Verkabelung
---------------------------

.. image:: img/Lesson_48_Iot_weather_monitor_uno_bb.png
    :width: 100%



Konfiguration von ThingSpeak
-----------------------------

|link_thingspeak| ™ ist ein IoT-Analyseplattformdienst, der es Ihnen ermöglicht, Live-Datenströme in der Cloud zu aggregieren, zu visualisieren und zu analysieren. ThingSpeak bietet sofortige Visualisierungen von Daten, die von Ihren Geräten an ThingSpeak gesendet werden. Mit der Möglichkeit, MATLAB®-Code in ThingSpeak auszuführen, können Sie eine Online-Analyse und Verarbeitung der Daten durchführen, während sie eintreffen. ThingSpeak wird häufig für die Prototypenerstellung und die Nachweisführung von IoT-Systemen verwendet, die Analyse erfordern.

.. image:: img/signup_tsp_ml.png
    :width: 80% 
    :align: center

.. raw:: html
    
    <br/>  

**1) Erstellung eines ThingSpeak-Kontos**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Das erste, was Sie tun müssen, ist ein Konto bei ThingSpeak zu erstellen. Seit der Zusammenarbeit mit MATLAB können Sie Ihre MathWorks-Anmeldeinformationen verwenden, um sich bei |link_thingspeak| anzumelden.

Wenn Sie noch keine haben, müssen Sie ein Konto bei MathWorks erstellen und sich bei der ThingSpeak-Anwendung anmelden.

.. image:: img/05-thingspeak_signup_shadow.png
    :width: 50%
    :align: center

**2) Erstellung des Kanals**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nach dem Anmelden erstellen Sie einen neuen Kanal, um die Daten zu speichern, indem Sie zu "Channels" > "My Channels" gehen und auf "New Channel" klicken.

.. image:: img/05-thingspeak_channel_1_shadow.png
    :width: 95%
    :align: center

Für dieses Projekt müssen wir einen Kanal namens "**Weather Monitor**" mit zwei Feldern erstellen: **Feld 1** für "**Temperatur**" und **Feld 2** für "**Atmosphärischen Druck**".

.. image:: img/05-thingspeak_channel_2_shadow.png
    :width: 95%
    :align: center

.. raw:: html
    
    <br/>  


Code
--------------------------- 


#. Öffnen Sie die Datei ``Lesson_48_Iot_Weather_Monitor.ino`` im Pfad ``universal-maker-sensor-kit\arduino_uno\Lesson_48_Iot_Weather_Monitor``, oder kopieren Sie diesen Code in **Arduino IDE**.

   .. note:: 
      Um die Bibliothek zu installieren, verwenden Sie den Arduino Library Manager und suchen Sie nach **"Adafruit BMP280"** und installieren Sie sie. 

   .. raw:: html
      
      <iframe src=https://create.arduino.cc/editor/sunfounder01/59eeae43-5dcc-46d7-833f-65fd2bdb3603/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


#. Sie müssen die ``mySSID`` und ``myPWD`` des WLANs eingeben, das Sie verwenden. 

   .. code-block:: arduino

    String mySSID = "your_ssid";     // WiFi SSID
    String myPWD = "your_password";  // WiFi Password

#. Sie müssen auch das ``myAPI`` mit Ihrem ThingSpeak Channel API-Schlüssel ändern.

   .. code-block:: arduino
    
      String myAPI = "xxxxxxxxxxxx";  // API Key

   .. image:: img/05-thingspeak_api_shadow.png
       :width: 80%
       :align: center
   
   
   Hier finden Sie **Ihren einzigartigen API-SCHLÜSSEL, den Sie privat halten müssen**. 

#. Nach Auswahl des richtigen Boards und Ports klicken Sie auf die **Upload**-Schaltfläche.

#. Öffnen Sie den Seriellen Monitor (stellen Sie die Baudrate auf **9600**) und warten Sie auf eine Meldung wie eine erfolgreiche Verbindung.

   .. image:: img/05-ready_1_shadow.png
          :width: 95%

   .. image:: img/05-ready_2_shadow.png
          :width: 95%

Codeanalyse
---------------------------


#. Initialisierung und Bluetooth-Einrichtung

   .. code-block:: arduino

      // Set up Bluetooth module communication
      #include <SoftwareSerial.h>
      const int bluetoothTx = 3;
      const int bluetoothRx = 4;
      SoftwareSerial bleSerial(bluetoothTx, bluetoothRx);
   
   Wir beginnen damit, die SoftwareSerial-Bibliothek einzuschließen, um uns bei der Bluetooth-Kommunikation zu helfen. Die TX- und RX-Pins des Bluetooth-Moduls werden dann definiert und mit den Pins 3 und 4 auf dem Arduino verbunden. Schließlich initialisieren wir das Objekt ``bleSerial`` für die Bluetooth-Kommunikation.
#. LED Pin-Definitionen

   .. code-block:: arduino

      // Pin numbers for each LED
      const int rledPin = 10;  //red
      const int yledPin = 11;  //yellow
      const int gledPin = 12;  //green

   Hier definieren wir, an welchen Arduino-Pins unsere LEDs angeschlossen sind. Die rote LED ist an Pin 10, die gelbe an Pin 11 und die grüne an Pin 12.

#. setup() Funktion

   .. code-block:: arduino

      void setup() {
         pinMode(rledPin, OUTPUT);
         pinMode(yledPin, OUTPUT);
         pinMode(gledPin, OUTPUT);

         Serial.begin(9600);
         bleSerial.begin(9600);
      }

   In der ``setup()`` Funktion setzen wir die LED-Pins auf ``OUTPUT``. Wir starten auch die serielle Kommunikation für sowohl das Bluetooth-Modul als auch die Standard-Serielle (die mit dem Computer verbunden ist) mit einer Baudrate von 9600.

#. Hauptschleife() für die Bluetooth-Kommunikation

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

   In unserer Hauptschleife ``loop()``, überprüfen wir kontinuierlich, ob Daten vom Bluetooth-Modul verfügbar sind. Wenn wir Daten empfangen, lesen wir das Zeichen und zeigen es im Seriellen Monitor an. Abhängig vom empfangenen Zeichen (R, Y oder G) schalten wir die entsprechende LED mit der ``toggleLights()`` Funktion um.

#. Funktion zum Umschalten der Lichter

   .. code-block:: arduino

      void toggleLights(int targetLight) {
         digitalWrite(rledPin, LOW);
         digitalWrite(yledPin, LOW);
         digitalWrite(gledPin, LOW);

         digitalWrite(targetLight, HIGH);
      }

   Diese Funktion, ``toggleLights()``, schaltet zuerst alle LEDs aus. Nachdem sichergestellt wurde, dass alle aus sind, schaltet sie die angegebene Ziel-LED ein. Dies stellt sicher, dass immer nur eine LED eingeschaltet ist.
