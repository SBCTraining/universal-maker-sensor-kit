.. note:: 

    Ciao, benvenuto nella community SunFounder su Facebook per appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima annunci e novità sui nuovi prodotti.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri articoli più recenti.
    - **Promozioni festive e giveaway**: Partecipa a concorsi ed eventi promozionali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

Per utenti Linux/Unix
==========================

#. Individua e apri il **Terminale** sul tuo sistema Linux/Unix.

#. Assicurati che il tuo Raspberry Pi sia connesso alla stessa rete. Verifica digitando ``ping <hostname>.local``. Ad esempio:

   .. code-block::

       ping raspberrypi.local

   Se il dispositivo è connesso alla rete, dovresti visualizzare l'indirizzo IP del Raspberry Pi.

   * Se il terminale mostra un messaggio come ``Impossibile trovare l'host pi.local. Controlla il nome e riprova.``, verifica di aver inserito correttamente l'hostname.
   * Se non riesci a ottenere l’indirizzo IP, controlla le impostazioni di rete o WiFi del Raspberry Pi.

#. Avvia una connessione SSH digitando ``ssh <username>@<hostname>.local`` oppure ``ssh <username>@<indirizzo IP>``. Ad esempio:

   .. code-block::

       ssh pi@raspberrypi.local

#. Al primo accesso, verrà visualizzato un messaggio di sicurezza. Digita ``yes`` per continuare.

   .. code-block::

       The authenticity of host 'raspberrypi.local (2400:2410:2101:5800:635b:f0b6:2662:8cba)' can't be established.
       ED25519 key fingerprint is SHA256:oo7x3ZSgAo032wD1tE8eW0fFM/kmewIvRwkBys6XRwg.
       Are you sure you want to continue connecting (yes/no/[fingerprint])?

#. Inserisci la password impostata in precedenza. Per motivi di sicurezza, i caratteri digitati non saranno visibili.

   .. note::
       È normale che i caratteri della password non vengano visualizzati nel terminale. Assicurati semplicemente di digitarla correttamente.



#. Una volta effettuato l’accesso con successo, il tuo Raspberry Pi sarà connesso e pronto per il passaggio successivo.
