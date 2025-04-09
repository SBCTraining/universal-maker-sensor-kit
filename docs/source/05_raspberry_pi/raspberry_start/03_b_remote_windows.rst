.. note:: 

    Ciao, benvenuto nella community SunFounder su Facebook per appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri entusiasti.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e affronta sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima annunci e novità sui nostri prodotti.
    - **Sconti speciali**: Approfitta di offerte esclusive sui prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi e promozioni speciali.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _remote_windows:

Utenti Windows
=======================

Se utilizzi Windows, puoi accedere da remoto al tuo Raspberry Pi tramite PowerShell.

#. Premi i tasti ``Windows`` + ``R`` sulla tastiera per aprire il programma **Esegui**. Digita **powershell** nella casella di input. 

   .. image:: img/windows_01.png
       :align: center

#. Verifica che il tuo Raspberry Pi sia sulla stessa rete digitando ``ping <hostname>.local``.

   .. code-block:: shell

       ping raspberrypi.local

   .. image:: img/windows_02.png
       :width: 550
       :align: center

   * Se il terminale mostra il messaggio ``Impossibile trovare l'host <hostname>.local``, è possibile che il Raspberry Pi non sia connesso correttamente alla rete. Verifica la connessione.
   * Se non riesci a effettuare il ping su ``<hostname>.local``, prova a :ref:`get_ip` ed esegui ``ping <IP address>`` (es. ``ping 192.168.6.116``).
   * Se ricevi più risposte come "Risposta da <IP address>: byte=32 tempo<1ms TTL=64", significa che il tuo PC riesce a raggiungere il Raspberry Pi.

   .. raw:: html

      <br/>

#. Digita ``ssh <username>@<hostname>.local`` (oppure ``ssh <username>@<IP address>``).

   .. code-block:: shell

       ssh pi@raspberrypi.local


#. Potrebbe apparire il seguente messaggio:

   .. code-block::

       The authenticity of host 'raspberrypi.local (192.168.6.116)' can't be established.
       ECDSA key fingerprint is SHA256:7ggckKZ2EEgS76a557cddfxFNDOBBuzcJsgaqA/igz4.
       Are you sure you want to continue connecting (yes/no/[fingerprint])? 

   Digita "yes".

#. Inserisci la password impostata in precedenza. (Nel nostro esempio è ``raspberry``.)

   .. note::
       Quando inserisci la password, i caratteri non verranno mostrati nella finestra. È normale. Assicurati solo di digitare correttamente.

#. Ora sei connesso al Raspberry Pi e pronto per passare al passaggio successivo.

   .. image:: img/windows_03.png
       :width: 550
       :align: center

.. _windows_remote_desktop:

Desktop Remoto
------------------

Se non ti piace utilizzare la finestra del terminale per accedere al Raspberry Pi, puoi usare il desktop remoto per gestire facilmente i file con un’interfaccia grafica.

In questo caso utilizziamo `VNC® Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_.

**Abilitare il servizio VNC**

Il servizio VNC è già installato nel sistema. Di default è disattivato, quindi è necessario abilitarlo nella configurazione.

#. Digita il seguente comando:

   .. raw:: html

       <run></run>
    
   .. code-block:: shell 

       sudo raspi-config


#. Seleziona l'opzione **3** **Interfacing Options** usando le frecce direzionali, poi premi **Invio**.

   .. image:: img/windows_04.png
       :align: center

#. Seleziona quindi **VNC**.

   .. image:: img/windows_05.png
       :align: center

#. Usa i tasti freccia per selezionare **<Yes>** -> **<OK>** -> **<Finish>** per completare la configurazione.

   .. image:: img/windows_06.png
       :align: center

**Accesso tramite VNC**

#. Scarica e installa il programma `VNC Viewer <https://www.realvnc.com/en/connect/download/viewer/>`_ sul tuo computer.

#. Apri il programma appena completata l’installazione. Inserisci il nome host o l’indirizzo IP e premi Invio.

   .. image:: img/windows_07.png
       :align: center

#. Dopo aver inserito nome utente e password del Raspberry Pi, clicca su **OK**.

   .. image:: img/windows_08.png
       :align: center

#. Ora potrai vedere il desktop del Raspberry Pi.

   .. image:: img/windows_09.png
       :align: center
