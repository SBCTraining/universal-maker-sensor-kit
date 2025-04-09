.. note:: 

    Ciao, benvenuto nella community SunFounder dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32 su Facebook! Approfondisci Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto Esperto**: Risolvi problemi post-vendita e affronta sfide tecniche grazie al supporto del nostro team e della community.
    - **Impara e Condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime Esclusive**: Ottieni l’accesso anticipato agli annunci di nuovi prodotti e contenuti esclusivi.
    - **Sconti Speciali**: Approfitta di sconti esclusivi sui nostri ultimi prodotti.
    - **Promozioni Festive e Giveaway**: Partecipa a giveaway e promozioni stagionali.

    👉 Pronto per esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

.. _install_os:

Scrivere Raspberry Pi OS sulla Scheda SD
==============================================

**Passaggio 1**

Il team Raspberry Pi mette a disposizione uno strumento grafico semplice da usare per scrivere il sistema operativo sulla scheda SD, compatibile con Mac OS, Ubuntu 18.04 e Windows. È l’opzione più comoda per la maggior parte degli utenti, in quanto scarica e installa automaticamente l'immagine del sistema operativo sulla scheda SD.

Visita la pagina dei download: https://www.raspberrypi.org/software/. Scegli il **Raspberry Pi Imager** adatto al tuo sistema operativo. Una volta scaricato, aprilo per avviare l’installazione.

.. image:: img/installing_01.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 2**

Al lancio dell’installer, il tuo sistema operativo potrebbe visualizzare un avviso di sicurezza. Ad esempio, Windows potrebbe mostrare questo messaggio:

.. image:: img/installing_02.png
    :align: center

.. raw:: html

    <br/>

Se compare questo avviso, clicca su **Ulteriori informazioni** e poi su **Esegui comunque**. Continua seguendo le istruzioni a schermo per completare l’installazione di Raspberry Pi Imager.


**Passaggio 3**

Dopo l’installazione, apri il programma cliccando sull’icona **Raspberry Pi Imager** o eseguendo ``rpi-imager``.

.. image:: img/installing_03.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 4**

Clicca su **Scegli dispositivo** e seleziona il modello del tuo Raspberry Pi dall’elenco.

.. image:: img/installing_04.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 5**

Poi clicca su **Scegli OS** e seleziona il sistema operativo da installare.

.. image:: img/installing_05.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 6**

Inserisci il supporto di memoria preferito, come una scheda microSD, in un lettore SD integrato o esterno. Poi clicca su "Scegli memoria" e seleziona il dispositivo.

.. note:: 

   **Assicurati di selezionare il dispositivo corretto se ci sono più dispositivi collegati**; spesso puoi distinguerli in base alla capacità. Se hai dubbi, scollega gli altri dispositivi. **Tieni presente che l’installazione del sistema cancellerà tutti i dati presenti sul dispositivo selezionato.**

.. image:: img/installing_06.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 7**

Premi il pulsante **AVANTI** e scegli **MODIFICA IMPOSTAZIONI** per accedere alla pagina di personalizzazione del sistema operativo.

.. image:: img/installing_07.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 8**

Imposta il **nome host**.

.. note::

   L'opzione hostname definisce il nome che il Raspberry Pi trasmette alla rete usando mDNS. Una volta collegato il Raspberry Pi alla rete, sarà possibile accedervi da altri dispositivi con ``<hostname>.local`` o ``<hostname>.lan``.

.. image:: img/installing_08.png
    :align: center

.. raw:: html

    <br/>

Imposta **nome utente** e **password** per l’account amministratore del Raspberry Pi.

.. note::
   Il Raspberry Pi non ha una password predefinita, quindi è fondamentale impostarne una. Inoltre, puoi personalizzare il nome utente.

.. image:: img/installing_09.png
    :align: center

.. raw:: html

    <br/>

Configura la rete wireless inserendo il **SSID** e la **password** della tua rete.

.. note::

   Imposta il campo "Paese della rete Wi-Fi" utilizzando il codice a due lettere del tuo paese |link_alpha2_code|.

.. image:: img/installing_10.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 9**

Accedi alla pagina **SERVIZI**, abilita l'opzione **Attiva SSH** e scegli "Usa autenticazione con password" (consigliato per principianti). Clicca su **Save** per applicare le modifiche.

.. image:: img/installing_11.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 10**

Clicca sul pulsante **Yes**.

.. image:: img/installing_12.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 11**

Se la tua scheda SD contiene file, valuta la possibilità di fare un backup per evitare la perdita di dati. Se non serve, clicca su **Sì**.

.. image:: img/installing_13.png
    :align: center

.. raw:: html

    <br/>

**Passaggio 12**

Apparirà la finestra seguente al termine del processo di scrittura. Il processo richiede un po’ di tempo, che varia in base alla velocità di lettura/scrittura della scheda SD. Attendi con pazienza.

.. image:: img/installing_14.png
    :align: center

.. raw:: html

    <br/>

