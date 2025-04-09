.. note:: 

    Ciao, benvenuto nella community Facebook di SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci il mondo di Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci dei nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

Come creare, aprire o salvare uno Sketch?
============================================

#. Quando apri l’Arduino IDE per la prima volta o crei un nuovo sketch, vedrai una schermata come questa, in cui l’IDE crea automaticamente un nuovo file chiamato "sketch".

   .. image:: img/sp221014_173458.png

   Questi file sketch hanno un nome temporaneo predefinito che riflette la data di creazione. ``sketch_oct14a.ino`` significa "primo sketch del 14 ottobre". L’estensione ``.ino`` è il formato dei file di sketch per Arduino.

#. Ora proviamo a creare un nuovo sketch. Copia il codice seguente nell’IDE Arduino, sostituendo il codice originale.


   .. image:: img/create1.png

   .. code-block:: Arduino

       void setup() {
           // inserisci qui il codice di configurazione, eseguito una sola volta:
           pinMode(13,OUTPUT); 
       }

       void loop() {
           // inserisci qui il codice principale, eseguito ripetutamente:
           digitalWrite(13,HIGH);
           delay(500);
           digitalWrite(13,LOW);
           delay(500);
       }

#. Premi ``Ctrl+S`` oppure clicca su **File** -> **Salva**. Lo sketch verrà salvato per default nella cartella: ``C:\Users\{your_user}\Documents\Arduino``, ma puoi rinominarlo o scegliere un percorso differente.

   .. image:: img/create2.png

#. Dopo il salvataggio, vedrai che il nome dello sketch è stato aggiornato anche nella finestra dell’IDE.

   .. image:: img/create3.png

Continua con la prossima sezione per imparare come caricare lo sketch creato sulla tua scheda Arduino.