.. note:: 

    Ciao, benvenuto nella community SunFounder su Facebook per appassionati di Raspberry Pi, Arduino ed ESP32! Esplora più a fondo Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e affronta sfide tecniche grazie al supporto del nostro team e della community.
    - **Impara e condividi**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato a nuovi annunci di prodotto e contenuti esclusivi.
    - **Sconti speciali**: Approfitta di sconti riservati sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni speciali e concorsi con premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _remote_macosx:

Utente Mac OS X
==========================

Per gli utenti Mac, accedere direttamente al desktop del Raspberry Pi tramite VNC è più comodo rispetto all'uso del terminale. Puoi accedere tramite Finder inserendo la password dell’account dopo aver abilitato VNC sul Raspberry Pi.

Nota che questa modalità non cifra la comunicazione tra il Mac e il Raspberry Pi.
La comunicazione avviene all'interno della tua rete domestica o aziendale, quindi anche se non è protetta, non rappresenta un problema.
Tuttavia, se desideri maggiore sicurezza, puoi installare un’applicazione VNC come `VNC® Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_.

In alternativa, sarebbe utile utilizzare temporaneamente un monitor (TV), mouse e tastiera per aprire direttamente il desktop del Raspberry Pi e configurare VNC.
Se non li hai a disposizione, nessun problema: puoi comunque utilizzare il comando SSH per aprire la shell Bash del Raspberry Pi e configurare il VNC da lì.


* :ref:`have_temp_monitor`
* :ref:`no_temp_monitor`


.. _have_temp_monitor:

Hai un monitor (o TV) temporaneo?
---------------------------------------------------------------------

#. Collega un monitor (o TV), mouse e tastiera al Raspberry Pi e accendilo. Segui il menu in base ai numeri nella figura.


   .. image:: img/mac_01.png
       :align: center

#. Verrà visualizzata la seguente schermata. Nella scheda **Interfacce**, imposta **VNC** su **Abilitato** e clicca su **OK**.

   .. image:: img/mac_02.png
       :align: center


#. In alto a destra apparirà l’icona VNC e il server VNC si avvierà.

   .. image:: img/mac_03.png
       :align: center


#. Apri la finestra del server VNC cliccando sull'icona **VNC**, poi clicca sul pulsante **Menu** in alto a destra e seleziona **Opzioni**.

   .. image:: img/mac_04.png
       :align: center

#. Verrà visualizzata la schermata seguente dove potrai modificare le opzioni.

   .. image:: img/mac_05.png
       :align: center

   Imposta **Crittografia** su **Preferibilmente disattivata** e **Autenticazione** su **Password VNC**. 
    
#. Quando clicchi su **OK**, verrà visualizzata la schermata per inserire la password. Puoi usare la stessa password del Raspberry Pi o sceglierne una diversa, quindi inseriscila e clicca su **OK**.

   .. image:: img/mac_06.png
       :align: center

   Ora sei pronto per connetterti dal tuo Mac. Puoi scollegare il monitor.

**Da qui in poi, operazioni lato Mac.**

#. Ora seleziona **Connetti al server** dal menu del Finder, accessibile cliccando con il tasto destro.

   .. image:: img/mac_07.png
       :align: center

#. Inserisci ``vnc://<username>@<hostname>.local`` (oppure ``vnc://<username>@<IP address>``). Dopo averlo inserito, clicca su **Connetti**.

   .. image:: img/mac_08.png
       :align: center


#. Ti verrà chiesta una password: inseriscila.

   .. image:: img/mac_09.png
       :align: center

#. Verrà mostrato il desktop del Raspberry Pi, che potrai controllare direttamente dal Mac.

   .. image:: img/mac_10.png
       :align: center

.. _no_temp_monitor:

Non hai un monitor (o TV) temporaneo?
---------------------------------------------------------------------------

* Puoi utilizzare il comando SSH per accedere alla shell Bash del Raspberry Pi.
* Bash è la shell predefinita standard nei sistemi Linux.
* La shell consente di impartire comandi all'interno di Unix/Linux.
* La maggior parte delle operazioni può essere eseguita tramite shell.
* Dopo la configurazione del Raspberry Pi, potrai accedere al desktop tramite **Finder** dal Mac.


#. Digita ``ssh <username>@<hostname>.local`` per connetterti al Raspberry Pi.


   .. code-block:: shell

       ssh pi@raspberrypi.local


   .. image:: img/mac_11.png


#. Il messaggio seguente verrà mostrato solo al primo accesso: digita **yes**.

   .. code-block:: 

       The authenticity of host 'raspberrypi.local (2400:2410:2101:5800:635b:f0b6:2662:8cba)' can't be established.
       ED25519 key fingerprint is SHA256:oo7x3ZSgAo032wD1tE8eW0fFM/kmewIvRwkBys6XRwg.
       This key is not known by any other names
       Are you sure you want to continue connecting (yes/no/[fingerprint])?


#. Inserisci la password del Raspberry Pi. La password non verrà visualizzata mentre la digiti, quindi fai attenzione a non sbagliare.

   .. code-block:: 

       pi@raspberrypi.local's password: 
       Linux raspberrypi 5.15.61-v8+ #1579 SMP PREEMPT Fri Aug 26 11:16:44 BST 2022 aarch64

       The programs included with the Debian GNU/Linux system are free software;
       the exact distribution terms for each program are described in the
       individual files in /usr/share/doc/*/copyright.

       Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
       permitted by applicable law.
       Last login: Thu Sep 22 12:18:22 2022
       pi@raspberrypi:~ $ 




#. Configura il Raspberry Pi per consentire l'accesso VNC dal tuo Mac una volta effettuato l'accesso. Per prima cosa aggiorna il sistema operativo con i seguenti comandi:

   .. code-block:: shell

       sudo apt update
       sudo apt upgrade


   Quando richiesto ``Do you want to continue? [Y/n]``, premi ``Y``.

   L'aggiornamento potrebbe richiedere tempo, a seconda del numero di pacchetti da aggiornare.


#. Esegui il seguente comando per abilitare il **server VNC**:

   .. code-block:: shell

       sudo raspi-config

#. Verrà visualizzata la schermata seguente. Usa i tasti freccia per selezionare **3 Interface Options** e premi **Invio**.

   .. image:: img/mac_12.png
       :align: center

#. Poi seleziona **VNC**.

   .. image:: img/mac_13.png
       :align: center

#. Usa i tasti freccia per selezionare **<Yes>** -> **<OK>** -> **<Fine>** per completare la configurazione.

   .. image:: img/mac_14.png
       :align: center


#. Ora che il server VNC è attivo, configuriamo i parametri di connessione per il Mac.

   Per definire i parametri validi per tutti gli utenti, crea il file ``/etc/vnc/config.d/common.custom``.

   .. code-block:: shell

       sudo nano /etc/vnc/config.d/common.custom

   Inserisci ``Authentication=VncAuth`` poi premi ``Ctrl+X`` -> ``Y`` -> ``Enter`` per salvare ed uscire.

   .. image:: img/mac_15.png
       :align: center

#. Inoltre, imposta una password per accedere tramite VNC dal Mac. Può essere la stessa del Raspberry Pi o diversa.


   .. code-block:: shell

       sudo vncpasswd -service


#. Dopo la configurazione, riavvia il Raspberry Pi per applicare le modifiche.

   .. code-block:: shell

       sudo reboot

#. Ora seleziona **Connetti al server** dal menu del **Finder**, accessibile cliccando con il tasto destro.

   .. image:: img/mac_16.png
       :align: center

#. Inserisci ``vnc://<username>@<hostname>.local`` (o ``vnc://<username>@<IP address>``) e clicca su **Connect**.

   .. image:: img/mac_17.png
       :align: center


#. Ti verrà chiesta una password: inseriscila.

   .. image:: img/mac_18.png
       :align: center

#. Vedrai il desktop del Raspberry Pi e potrai controllarlo direttamente dal tuo Mac.

   .. image:: img/mac_19.png
       :align: center
